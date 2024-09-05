-------
# **EXEMPLE 1: Azure Pipelines (Flask App)**
-------

```yaml
trigger:
- main

variables:
  projectName: 'my-flask-app'
  resourceGroupName: 'my-flask-app-rg'
  location: 'eastus'
  appServicePlanName: 'my-flask-app-plan'
  webAppName: 'my-flask-app'
  environmentName: 'production'

stages:
- stage: Build
  jobs:
  - job: BuildJob
    pool:
      vmImage: 'ubuntu-latest'
    steps:
    - task: UsePythonVersion@0
      inputs:
        versionSpec: '3.9'
    
    - script: |
        python -m venv antenv
        source antenv/bin/activate
        pip install -r requirements.txt
      displayName: 'Install dependencies'
    
    - script: |
        pip install pytest
        pip install pytest-cov
        pytest tests --doctest-modules --junitxml=junit/test-results.xml --cov=. --cov-report=xml
      displayName: 'Run tests'

    - task: PublishTestResults@2
      inputs:
        testResultsFormat: 'JUnit'
        testResultsFiles: '**/test-results.xml'
      condition: succeededOrFailed()

    - task: PublishCodeCoverageResults@1  
      inputs:
        codeCoverageTool: 'cobertura'
        summaryFileLocation: '$(System.DefaultWorkingDirectory)/**/coverage.xml'

    - task: ArchiveFiles@2
      inputs:
        rootFolderOrFile: '$(System.DefaultWorkingDirectory)'
        includeRootFolder: false
        archiveType: 'zip'
        archiveFile: '$(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip' 
        replaceExistingArchive: true

    - publish: $(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip
      artifact: drop

- stage: Deploy
  jobs:
  - deployment: DeployWeb
    displayName: Deploy Web App
    environment: $(environmentName)
    pool: 
      vmImage: 'ubuntu-latest'
    strategy:
      runOnce:
        deploy:
          steps:
          - task: AzureWebApp@1
            displayName: 'Deploy Azure Web App'
            inputs:
              azureSubscription: 'Resource Manager Connection'
              appName: '$(webAppName)'
              appType: 'webApp'
              deployToSlotOrASE: true
              resourceGroupName: '$(resourceGroupName)'
              slotName: 'production'
              deploymentMethod: 'auto'
              packageForLinux: '$(Pipeline.Workspace)/drop/$(Build.BuildId).zip'

          - task: AzureAppServiceSettings@1
            inputs:
              azureSubscription: 'Resource Manager Connection'
              appName: '$(webAppName)'
              resourceGroupName: '$(resourceGroupName)'
              appSettings: | 
                [
                  {
                    "name": "SCM_DO_BUILD_DURING_DEPLOYMENT",
                    "value": "true"
                  },
                  {
                    "name": "FLASK_ENV", 
                    "value": "production"
                  }
                ]
```

---

-------
# **EXEMPLE 2: Azure Pipelines (Windows with .NET)**
-------

```yaml
trigger:
- main

pool:
  vmImage: 'windows-latest'

variables:
  solution: '**/*.sln'
  buildPlatform: 'Any CPU'
  buildConfiguration: 'Release'

stages:
- stage: Build
  jobs:
  - job: Build
    steps:
    - task: NuGetToolInstaller@1

    - task: NuGetCommand@2
      inputs:
        restoreSolution: '$(solution)'

    - task: SonarQubePrepare@5
      inputs:
        SonarQube: 'SonarQube'
        scannerMode: 'MSBuild'
        projectKey: 'your-project-key'
        projectName: 'Your Project Name'

    - task: VSBuild@1
      inputs:
        solution: '$(solution)'
        msbuildArgs: '/p:DeployOnBuild=true /p:WebPublishMethod=Package /p:PackageAsSingleFile=true /p:SkipInvalidConfigurations=true /p:PackageLocation="$(build.artifactStagingDirectory)"'
        platform: '$(buildPlatform)'
        configuration: '$(buildConfiguration)'

    - task: VSTest@2
      inputs:
        platform: '$(buildPlatform)'
        configuration: '$(buildConfiguration)'
        codeCoverageEnabled: true

    - task: SonarQubeAnalyze@5

    - task: SonarQubePublish@5
      inputs:
        pollingTimeoutSec: '300'

    - task: PublishCodeCoverageResults@1
      inputs:
        codeCoverageTool: 'cobertura'
        summaryFileLocation: '$(System.DefaultWorkingDirectory)/**/*coverage.cobertura.xml'

    - task: PublishBuildArtifacts@1
      inputs:
        PathtoPublish: '$(Build.ArtifactStagingDirectory)'
        ArtifactName: 'drop'
        publishLocation: 'Container'

- stage: Test
  jobs:
  - job: IntegrationTests
    steps:
    - task: DownloadBuildArtifacts@0
      inputs:
        buildType: 'current'
        downloadType: 'single'
        artifactName: 'drop'
        downloadPath: '$(System.ArtifactsDirectory)'

    - script: |
        echo Running integration tests...
        # Add your integration test commands here

- stage: Security
  jobs:
  - job: SecurityScan
    steps:
    - task: WhiteSource@21
      inputs:
        projectName: 'Your Project Name'
        productName: 'Your Product Name'

- stage: Deploy
  jobs:
  - deployment: DeployToStaging
    pool:
      vmImage: 'windows-latest'
    environment: 'staging'
    strategy:
      runOnce:
        deploy:
          steps:
          - task: AzureWebApp@1
            inputs:
              azureSubscription: 'Your Azure Subscription'
              appName: 'Your App Name'
              package: '$(System.ArtifactsDirectory)/**/*.zip'
```

---
# **EXEMPLE 3: Jenkins Pipeline (Flask App with Docker and AWS ECS)**
-------

```groovy
pipeline {
    agent any
    
    environment {
        AWS_REGION = 'us-east-1'
        AWS_ACCOUNT_ID = '123456789012'
        PYTHON_VERSION = '3.9'
        FLASK_ENV = 'production'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Setup Python') {
            steps {
                sh "pyenv install ${PYTHON_VERSION} -s"
                sh "pyenv global ${PYTHON_VERSION}"
                sh "pip install --upgrade pip"
                sh "pip install -r requirements.txt"
            }
        }
        
        stage('Test') {
            steps {
                sh "pip install pytest pytest-cov"
                sh "pytest tests --doctest-modules --junitxml=junit/test-results.xml --cov=. --cov-report=xml"
            }
            post {
                always {
                    junit 'junit/test-results.xml'
                    cobertura coberturaReportFile: 'coverage.xml'
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                sh 'pip install bandit'
                sh 'bandit -r . -f custom'
                sh 'trivy fs .'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("flask-app:${env.BUILD_NUMBER}")
                }
            }
        }
        
        stage('Push to ECR') {
            steps {
                script {
                    docker.withRegistry("https://${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com", "ecr:${AWS_REGION}:aws-credentials") {
                        docker.image("flask-app:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
        
        stage('Deploy to ECS') {
            steps {
                withAWS(region: "${AWS_REGION}", credentials: 'aws-credentials') {
                    sh "aws ecs update-service --cluster my-cluster --service my-flask-service --force-new-deployment"
                }
            }
        }
        
        stage('Deploy CloudFormation') {
            steps {
                withAWS(region: "${AWS_REGION}", credentials: 'aws-credentials') {
                    cfnUpdate(stack:'flask-app-stack', file:'cloudformation-template.yaml', params:['ImageTag=${env.BUILD_NUMBER}'])
                }
            }
        }
    }
    
    post {
        success {
            snsPublish(
                topicArn: "arn:aws:sns:${AWS_REGION}:${AWS_ACCOUNT_ID}:deployment-notifications",
                subject: "Successful deployment: ${env.JOB_NAME}",
                message: "Build ${env.BUILD_NUMBER} deployed successfully"
            )
        }
        failure {
            snsPublish(
                topicArn: "arn:aws:sns:${AWS_REGION}:${AWS_ACCOUNT_ID}:deployment-notifications",
                subject: "Failed deployment: ${env.JOB_NAME}",
                message: "Build ${env.BUILD_NUMBER} failed"
            )
        }
    }
}
```

---
# **EXEMPLE 4: Jenkins Pipeline (Maven Project with AWS Services)**
-------

```groovy
pipeline {
    agent any
    
    environment {
        AWS_REGION = 'us-east-1'
        AWS_ACCOUNT_ID = '123456789012'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        


        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Security Scan') {
            steps {
                sh 'trivy fs .'
            }
        }
        
        stage('CodeBuild') {
            steps {
                awsCodeBuild projectName: 'my-project',
                             credentialsType: 'keys',
                             region: "${AWS_REGION}",
                             sourceControlType: 'jenkins'
            }
        }
        
        stage('Push to ECR') {
            steps {
                script {
                    docker.withRegistry("https://${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com", "ecr:${AWS_REGION}:aws-credentials") {
                        docker.image('my-image:latest').push()
                    }
                }
            }
        }
        
        stage('Deploy to S3') {
            steps {
                withAWS(region: "${AWS_REGION}", credentials: 'aws-credentials') {
                    s3Upload(file: 'target/myapp.jar', bucket: 'my-app-bucket', path: "builds/myapp-${BUILD_NUMBER}.jar")
                }
            }
        }
        
        stage('Deploy CloudFormation') {
            steps {
                withAWS(region: "${AWS_REGION}", credentials: 'aws-credentials') {
                    cfnUpdate(stack:'my-stack', file:'template.yaml', params:['InstanceType=t2.micro'])
                }
            }
        }
        
        stage('Deploy to Elastic Beanstalk') {
            steps {
                withAWS(region: "${AWS_REGION}", credentials: 'aws-credentials') {
                    sh 'eb use my-app-environment'
                    sh 'eb deploy'
                }
            }
        }
    }
    
    post {
        success {
            snsPublish(
                topicArn: "arn:aws:sns:${AWS_REGION}:${AWS_ACCOUNT_ID}:deployment-notifications",
                subject: "Successful deployment: ${env.JOB_NAME}",
                message: "Build ${env.BUILD_NUMBER} deployed successfully"
            )
        }
        failure {
            snsPublish(
                topicArn: "arn:aws:sns:${AWS_REGION}:${AWS_ACCOUNT_ID}:deployment-notifications",
                subject: "Failed deployment: ${env.JOB_NAME}",
                message: "Build ${env.BUILD_NUMBER} failed"
            )
        }
    }
}
```

---
# **EXEMPLE 5: Jenkins Pipeline (Flask Application with Docker and Kubernetes)**
-------

```groovy
pipeline {
    agent any
    
    environment {
        DOCKER_HUB_REPO = 'your-dockerhub-username/flask-app'
        DOCKER_HUB_CREDENTIALS = 'dockerhub-credentials-id'
        KUBECONFIG_CREDENTIALS = 'kubeconfig-credentials-id'
        CLUSTER_NAME = 'your-k8s-cluster'
        NAMESPACE = 'default'
        APP_NAME = 'flask-app'
        IMAGE_TAG = "${env.BUILD_NUMBER}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_REPO}:${IMAGE_TAG}")
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', "${DOCKER_HUB_CREDENTIALS}") {
                        docker.image("${DOCKER_HUB_REPO}:${IMAGE_TAG}").push()
                    }
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                withCredentials([file(credentialsId: "${KUBECONFIG_CREDENTIALS}", variable: 'KUBECONFIG')]) {
                    sh """
                    kubectl set image deployment/${APP_NAME} ${APP_NAME}=${DOCKER_HUB_REPO}:${IMAGE_TAG} -n ${NAMESPACE}
                    kubectl rollout status deployment/${APP_NAME} -n ${NAMESPACE}
                    """
                }
            }
        }
        
        stage('Post-deployment verification') {
            steps {
                withCredentials([file(credentialsId: "${KUBECONFIG_CREDENTIALS}", variable: 'KUBECONFIG')]) {
                    sh """
                    kubectl get pods -n ${NAMESPACE}
                    kubectl describe deployment/${APP_NAME} -n ${NAMESPACE}
                    """
                }
            }
        }
    }
    
    post {
        success {
            echo "Deployment to Kubernetes was successful!"
        }
        failure {
            echo "Deployment to Kubernetes failed!"
        }
    }
}
```

---
# **EXEMPLE 6: Jenkins Pipeline (Flask Application with Docker and Amazon EKS)**
-------

```groovy
pipeline {
    agent any
    
    environment {
        DOCKER_HUB_REPO = 'your-dockerhub-username/flask-app'
        DOCKER_HUB_CREDENTIALS = 'dockerhub-credentials-id'
        AWS_REGION = 'us-east-1'
        EKS_CLUSTER_NAME = 'your-eks-cluster'
        NAMESPACE = 'default'
        APP_NAME = 'flask-app'
        IMAGE_TAG = "${env.BUILD_NUMBER}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_REPO}:${IMAGE_TAG}")
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', "${DOCKER_HUB_CREDENTIALS}") {
                        docker.image("${DOCKER_HUB_REPO}:${IMAGE_TAG}").push()
                    }
                }
            }
        }
        
        stage('Configure AWS EKS Credentials') {
            steps {
                withAWS(region: "${AWS_REGION}", credentials: 'aws-credentials') {
                    sh """
                    aws eks update-kubeconfig --name ${EKS_CLUSTER_NAME} --region ${AWS_REGION}
                    """
                }
            }
        }
        
        stage('Deploy to EKS') {
            steps {
                sh """
                kubectl set image deployment/${APP_NAME} ${APP_NAME}=${DOCKER_HUB_REPO}:${IMAGE_TAG} -n ${NAMESPACE}
                kubectl rollout status deployment/${APP_NAME} -n ${NAMESPACE}
                """
            }
        }
        
        stage('Post-deployment verification') {
            steps {
                sh """
                kubectl get pods -n ${NAMESPACE}
                kubectl describe deployment/${APP_NAME} -n ${NAMESPACE}
                """
            }
        }
    }
    
    post {
        success {
            echo "Deployment to Amazon EKS was successful!"
        }
        failure {
            echo "Deployment to Amazon EKS failed!"
        }
    }
}
```

---
# **EXEMPLE 7: Jenkins Pipeline (Flask Application with Docker and Azure AKS)**
-------

```groovy
pipeline {
    agent any
    
    environment {
        DOCKER_HUB_REPO = 'your-dockerhub-username/flask-app'
        DOCKER_HUB_CREDENTIALS = 'dockerhub-credentials-id'
        AZURE_CREDENTIALS = 'azure-service-principal-id'
        AKS_CLUSTER_NAME = 'your-aks-cluster'
        RESOURCE_GROUP = 'your-resource-group'
        NAMESPACE = 'default'
        APP_NAME = 'flask-app'
        IMAGE_TAG = "${env.BUILD_NUMBER}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_REPO}:${IMAGE_TAG}")
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', "${DOCKER_HUB_CREDENTIALS}") {
                        docker.image("${DOCKER_HUB_REPO}:${IMAGE_TAG}").push()
                    }
                }
            }
        }
        
        stage('Configure Azure AKS Credentials') {
            steps {
                withAzureServicePrincipal(azureServicePrincipal: "${AZURE_CREDENTIALS}", tenantId: 'your-tenant-id', subscriptionId: 'your-subscription-id') {
                    sh """
                    az aks get-credentials --resource-group ${RESOURCE_GROUP} --name ${AKS_CLUSTER_NAME}
                    """
                }
            }
        }
        
        stage('Deploy to AKS') {
            steps {
                sh """
                kubectl set image deployment/${APP_NAME} ${APP_NAME}=${DOCKER_HUB_REPO}:${IMAGE_TAG} -n ${NAMESPACE}
                kubectl rollout status deployment/${APP_NAME} -n ${NAMESPACE}
                """
            }
        }
        
        stage('Post-deployment verification') {
            steps {
                sh """
                kubectl get pods -n ${NAMESPACE}
                kubectl describe deployment/${APP_NAME} -n ${NAMESPACE}
                """
            }
        }
    }
    
    post {
        success {
            echo "Deployment to Azure AKS was successful!"
        }
        failure {
            echo "Deployment to Azure AKS failed!"
        }
    }
}
```

----

-----

---
# **EXEMPLE 8: AWS CloudFormation (Flask App with Docker and ECR)**
-------
# modèle CloudFormation complet pour déployer une application Flask dans un repository ECR avec une tâche ECS Fargate

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: "Déploiement d'une application Flask avec Docker sur Amazon ECR via CloudFormation."

Parameters:
  RepositoryName:
    Type: String
    Default: "flask-app-repo"
    Description: "Nom du repository ECR pour l'application Flask."

Resources:
  FlaskAppECRRepository:
    Type: "AWS::ECR::Repository"
    Properties: 
      RepositoryName: !Ref RepositoryName
      LifecyclePolicy:
        LifecyclePolicyText: |
          {
            "rules": [
              {
                "rulePriority": 1,
                "description": "Expire images older than 30 days",
                "selection": {
                  "tagStatus": "any",
                  "countType": "sinceImagePushed",
                  "countUnit": "days",
                  "countNumber": 30
                },
                "action": {
                  "type": "expire"
                }
              }
            ]
          }

  FlaskAppTaskExecutionRole:
    Type: "AWS::IAM::Role"
    Properties: 
      AssumeRolePolicyDocument:
        Version: "2012-10-17"
        Statement:
          - Effect: Allow
            Principal:
              Service: ecs-tasks.amazonaws.com
            Action: sts:AssumeRole
      Policies:
        - PolicyName: "ECSTaskExecutionRolePolicy"
          PolicyDocument:
            Version: "2012-10-17"
            Statement:
              - Effect: Allow
                Action:
                  - ecr:GetDownloadUrlForLayer
                  - ecr:BatchCheckLayerAvailability
                  - ecr:BatchGetImage
                  - logs:CreateLogStream
                  - logs:PutLogEvents
                Resource: "*"

  FlaskAppCluster:
    Type: "AWS::ECS::Cluster"
    Properties: 
      ClusterName: "FlaskAppCluster"

  FlaskAppTaskDefinition:
    Type: "AWS::ECS::TaskDefinition"
    Properties: 
      Family: "FlaskAppTaskDefinition"
      Cpu: "256"
      Memory: "512"
      NetworkMode: "awsvpc"
      RequiresCompatibilities: 
        - FARGATE
      ExecutionRoleArn: !GetAtt FlaskAppTaskExecutionRole.Arn
      ContainerDefinitions:
        - Name: "flask-app"
          Image: !Sub "${AWS::AccountId}.dkr.ecr.${AWS::Region}.amazonaws.com/${RepositoryName}:latest"
          Essential: true
          PortMappings:
            - ContainerPort: 5000
          LogConfiguration:
            LogDriver: "awslogs"
            Options:
              awslogs-group: "/ecs/flask-app"
              awslogs-region: !Ref "AWS::Region"
              awslogs-stream-prefix: "ecs"

  FlaskAppService:
    Type: "AWS::ECS::Service"
    Properties: 
      Cluster: !Ref FlaskAppCluster
      DesiredCount: 1
      TaskDefinition: !Ref FlaskAppTaskDefinition
      LaunchType: "FARGATE"
      NetworkConfiguration:
        AwsvpcConfiguration:
          AssignPublicIp: ENABLED
          SecurityGroups: 
            - !Ref FlaskAppSecurityGroup
          Subnets: 
            - !Ref PublicSubnet

  FlaskAppSecurityGroup:
    Type: "AWS::EC2::SecurityGroup"
    Properties:
      GroupDescription: "Autoriser l'accès HTTP pour l'application Flask"
      VpcId: !Ref VPC
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: "0.0.0.0/0"

Outputs:
  ECRRepositoryUri:
    Description: "URI du repository ECR pour l'application Flask"
    Value: !GetAtt FlaskAppECRRepository.RepositoryUri
```

