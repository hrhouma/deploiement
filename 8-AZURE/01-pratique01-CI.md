# DevOpsDemo Project Setup and Deployment

- https://aex.dev.azure.com/
- https://portal.azure.com/
  
# PARTIE # A – Création et déploiement manuel du projet

# A.1. Configuration du projet
1. Téléchargez le Framework dotnet .NET5
2. Ouvrez une console et exécutez les commandes suivantes :
    ```bash
    cd C:\Users\Haythem\Desktop
    dotnet --version
    dotnet --list-sdks
    dotnet --list-runtimes
    dotnet --help
    md DevopsDemo
    cd DevopsDemo
    dotnet new globaljson
    ls
    cat global.json
    dotnet --list-sdks
    nano global.json
    ```

3. Dépannage & troubleshooting : [How to change default dotnet SDK version](https://dev.to/polarbit/how-to-change-default-dotnet-sdk-version-43ph)

# A.2. Construction du projet et d’une page web simple ASP.NET
1. Exécutez les commandes suivantes pour construire le projet :
    ```bash
    cd C:\
    md DevopsDemo
    cd DevopsDemo
    dotnet new sln -o HelloWorldApp
    cd HelloWorldApp
    dir
    dotnet new mvc -n HelloWorldApp.web
    dir 
    code .
    cd HelloWorldApp.web
    dir
    dotnet build
    dotnet build --configuration debug 
    dotnet build --configuration release
    ```
2. Vérifiez la présence de deux dossiers Debug et Release :
    ```bash
    cd C:\DevopsDemo\HelloWorldApp\HelloWorldApp.web\bin\release\net7.0 
    dotnet HelloWorldApp.web.dll
    Vérifiez http://localhost:5000/
    ```

# A.3. Déploiement de la page web manuellement
1. Exécutez les commandes suivantes pour déployer le projet :
    ```bash
    cd C:\DevopsDemo\HelloWorldApp\HelloWorldApp.web
    dotnet new sln -o HelloWorldApp
    dotnet publish -o /out
    dotnet publish -c release -o /out
    cd C:\out\
    dotnet HelloWorldApp.web.dll
    Vérifiez http://localhost:5000/
    ```

# A.4. Gestion de version avec GIT
1. Exécutez les commandes suivantes pour configurer Git :
    ```bash
    cd C:\DevopsDemo\HelloWorldApp
    git init
    git status
    git config --global user.name "hrhouma"
    git config --global user.email "rehoumahaythem@gmail.com"
    git config --local user.name "hrhouma"
    git config --local user.email "rehoumahaythem@gmail.com"
    code .
    git add .
    git status
    git commit -m "first commit"
    ```

# A.5. Création d’un dépôt sur AZURE DEVOPS
1. Suivez les étapes suivantes pour créer un dépôt sur Azure DevOps :
    1. Allez à [Azure DevOps](https://dev.azure.com/)
   - https://aex.dev.azure.com/me?mkt=fr-FR
   - https://portal.azure.com/
    3. Créez un profil
    4. Créez une organisation
    5. Créez un projet `HelloWorldApp`
    6. Cliquez sur `Repos`
    7. Préparez-vous à faire le push du dépôt local au dépôt distant sur Azure DevOps :
        ```bash
        git remote help
        cat .git/config
        git remote remove origin
        ```
    8. Générez les identifiants (Credentials) sur Azure DevOps :
        - Username: `hrehouma`
        - Password: `vv2qfumwpirb3lcol6bynlkachvsnoigmic5afbx2r5dbxg7e5tq`
        ```bash
        git remote add origin https://hrehouma0084@dev.azure.com/hrehouma0084/HelloWorldApp/_git/HelloWorldApp
        git push -u origin --all
        ```
        
![image](https://github.com/user-attachments/assets/de60f76f-8aac-4ce9-8734-78e12a7c449f)
![image](https://github.com/user-attachments/assets/185ac433-cbbd-4965-8ee8-7e85943eec67)

    8. Section facultative : confirmation de la sauvegarde des informations sur votre ordinateur local via le gestionnaire d'identifiants.

# PARTIE # B – Intégration continue sur AZURE DEVOPS

# B.1. Configuration de la pipeline (classic editor pipeline)
1. Activez le `classic editor pipeline` au niveau organisationnel :
    1. Organisation settings => pipelines => settings => Disable creation of classic build pipelines + Disable creation of classic release pipelines => off.
    2. Project settings => pipelines => settings => Disable creation of classic build pipelines + Disable creation of classic release pipelines => off.

# B.2. Création de la pipeline CI (Méthode # 1 - classic editor pipeline)
1. Créez la pipeline CI en utilisant l'outil `classic editor pipeline` :
    1. Pipelines => new pipeline => Use the classic editor => Azure Repos Git => ASP.NET Core (SANS LE .NET Framework).
    2. RESTORE => Build => Test => Publish => Publish Artifact.
    3. Supprimez les 4 composants proposés après avoir choisi ASP.NET Core.
    4. Choisissez 3 composants `.NET CORE` et un composant `Publish Artifact: drop`.

## Premier Composant (1/4)
**RESTORE**
- Display name: Restore Libraries
- Command: restore
- Path to project(s): `**/*.csproj` (si ça ne fonctionne pas, il faut le changer d’abord dans Get Sources ou Agent Job)
- Arguments: NO

## Deuxième Composant (2/4)
**BUILD**
- Display name: Build
- Command: build
- Path to project(s): `**/*.csproj`
- Arguments: `--configuration $(BuildConfiguration)`

## Troisième Composant (3/4)
**PUBLISH**
- Display name: Publish
- Command: publish
- Path to project(s): `**/*.csproj`
- Arguments: `--configuration $(BuildConfiguration) --output $(build.artifactstagingdirectory)`
- Options: 
  - Cocher "zip published projects"
  - Cocher "add project's folder name to publish path"

## Quatrième Composant (4/4)
**PUBLISH ARTIFACT**
- Display name: Publish Artifact: drop
- Path to publish: `$(Build.ArtifactStagingDirectory)`
- Artifact name: drop
- Artifact publish location: Azure pipelines

# TRIGGER (AUTOMATISER)
1. Faites ce changement dans votre fichier HTML :
    ```html
    <p> changement 1 </p>
    ```

2. Exécutez les commandes suivantes pour valider et pousser vos changements :
    ```bash
    git status
    git add .
    git commit -m 'lancement du CI'
    git push -u origin --all
    ```

## B.3. Création de la pipeline CI (Méthode # 2 - YAML)
1. Créez la pipeline CI en utilisant le YAML :
    ```yaml
    trigger:
    - main

    pool:
      vmImage: 'ubuntu-22.04'

    steps:
    - task: UseDotNet@2
      inputs:
        packageType: 'sdk'
        version: '7.x'
        installationPath: $(Agent.ToolsDirectory)/dotnet

    - task: DotNetCoreCLI@2
      displayName: 'Restore Libraries'
      inputs:
        command: 'restore'
        projects: '**/*.csproj'

    - task: DotNetCoreCLI@2
      displayName: 'Build'
      inputs:
        command: 'build'
        projects: '**/*.csproj'
        arguments: '--configuration $(BuildConfiguration)'

    - task: DotNetCoreCLI@2
      displayName: 'Publish'
      inputs:
        command: 'publish'
        publishWebProjects: true
        projects: '**/*.csproj'
        arguments: '--configuration $(BuildConfiguration) --output $(Build.ArtifactStagingDirectory)'
        zipAfterPublish: true
        modifyOutputPath: true

    - task: PublishBuildArtifacts@1
      displayName: 'Publish Artifact'
      inputs:
        PathtoPublish: '$(Build.ArtifactStagingDirectory)'
        ArtifactName: 'drop'
        publishLocation: 'Container'
    ```

2. Faites ce changement dans votre fichier HTML :
    ```html
    <p> changement 2 </p>
    ```

3. Testez votre pipeline :
    ```bash
    git status
    git add .
    git commit -m 'lancement du CI'
    git push -u origin --all
    ```
