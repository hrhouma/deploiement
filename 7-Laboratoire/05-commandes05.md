### Commandes et Description 

# Phase 1 : Planification de la conception et estimation des coûts
```yaml
# Aucune commande spécifique à exécuter pour cette phase
# Objectif : Comprendre les exigences du projet, définir les microservices nécessaires, et estimer les coûts associés à l'utilisation des services AWS.
```

# Phase 2 : Analyse de l'infrastructure de l'application monolithique
```bash
# Vérifier la disponibilité de l'application monolithique
sudo lsof -i :80  # Liste les fichiers ouverts par le processus écoutant sur le port 80 pour vérifier si l'application monolithique écoute sur ce port.

# Analyser le mode d'exécution de l'application monolithique
ps -ef | head -1  # Affiche les informations de l'en-tête du processus pour comprendre les options disponibles.
ps -ef | grep node  # Recherche les processus associés à Node.js pour identifier les processus liés à l'application monolithique.
```

# Phase 3 : Création d'un environnement de développement et enregistrement du code dans un référentiel Git
```bash
# Créer un IDE AWS Cloud9
aws cloud9 create-environment-ec2 --name MicroservicesIDE --instance-type t3.small --image-id amazonlinux-2 --subnet-id subnet-xxxxxxxx  # Crée un environnement Cloud9 basé sur une instance EC2 avec Amazon Linux 2.

# Copier le code de l'application dans votre IDE
scp -r -i ~/environment/labsuser.pem ubuntu@<instance-ip>:/home/ubuntu/resources/codebase_partner/* ~/environment/temp/  # Copie le code source de l'application depuis une instance distante vers l'IDE Cloud9.

# Initialiser le répertoire Git et pousser le code dans CodeCommit
cd ~/environment/microservices  # Change de répertoire vers le dossier microservices.
git init  # Initialise un nouveau référentiel Git local.
git branch -m dev  # Renomme la branche principale en dev pour le développement.
git add .  # Ajoute tous les fichiers au suivi Git.
git commit -m 'two unmodified copies of the application code'  # Valide les modifications avec un message de commit.
git remote add origin https://git-codecommit.us-east-1.amazonaws.com/v1/repos/microservices  # Ajoute le référentiel distant CodeCommit.
git push -u origin dev  # Pousse les modifications vers le référentiel distant sur la branche dev.
```

# Phase 4 : Configuration de l'application comme deux microservices et test de ceux-ci dans des conteneurs Docker
```bash
# Ajuster les paramètres de groupe de sécurité de l'instance AWS Cloud9
aws ec2 authorize-security-group-ingress --group-id sg-xxxxxxxx --protocol tcp --port 8080-8081 --cidr 0.0.0.0/0  # Autorise le trafic entrant sur les ports 8080 et 8081.

# Créer une image Docker pour le microservice client et lancer un conteneur de test
cd ~/environment/microservices/customer  # Change de répertoire vers le dossier customer.
docker build --tag customer .  # Crée une image Docker à partir du Dockerfile dans le dossier actuel.
docker run -d --name customer_1 -p 8080:8080 -e APP_DB_HOST="$dbEndpoint" customer  # Exécute un conteneur Docker à partir de l'image customer, avec la variable d'environnement APP_DB_HOST définie.

# Créer une image Docker pour le microservice employé et lancer un conteneur de test
cd ~/environment/microservices/employee  # Change de répertoire vers le dossier employee.
docker build --tag employee .  # Crée une image Docker à partir du Dockerfile dans le dossier actuel.
docker run -d --name employee_1 -p 8081:8081 -e APP_DB_HOST="$dbEndpoint" employee  # Exécute un conteneur Docker à partir de l'image employee, avec la variable d'environnement APP_DB_HOST définie.
```

# Phase 5 : Création de référentiels ECR, d'un cluster ECS, de définitions de tâche et de fichiers AppSpec
```bash
# Autoriser le client Docker à se connecter à Amazon ECR
account_id=$(aws sts get-caller-identity | grep Account | cut -d '"' -f4)  # Récupère l'ID du compte AWS actuel.
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin $account_id.dkr.ecr.us-east-1.amazonaws.com  # Connecte Docker à Amazon ECR en utilisant le mot de passe généré.

# Créer des référentiels ECR et charger les images Docker
docker tag customer:latest $account_id.dkr.ecr.us-east-1.amazonaws.com/customer:latest  # Balise l'image Docker customer avec l'URI du référentiel ECR.
docker tag employee:latest $account_id.dkr.ecr.us-east-1.amazonaws.com/employee:latest  # Balise l'image Docker employee avec l'URI du référentiel ECR.
docker push $account_id.dkr.ecr.us-east-1.amazonaws.com/customer:latest  # Pousse l'image Docker customer vers ECR.
docker push $account_id.dkr.ecr.us-east-1.amazonaws.com/employee:latest  # Pousse l'image Docker employee vers ECR.

# Créer un cluster ECS
aws ecs create-cluster --cluster-name microservices-serverlesscluster  # Crée un cluster ECS nommé microservices-serverlesscluster.

# Enregistrer les définitions de tâche dans Amazon ECS
aws ecs register-task-definition --cli-input-json file://taskdef-customer.json  # Enregistre la définition de tâche pour le client en utilisant le fichier taskdef-customer.json.
aws ecs register-task-definition --cli-input-json file://taskdef-employee.json  # Enregistre la définition de tâche pour l'employé en utilisant le fichier taskdef-employee.json.
```

# Phase 6 : Création de groupes cibles et d'un Application Load Balancer
```bash
# Créer des groupes cibles
aws elbv2 create-target-group --name customer-tg-one --protocol HTTP --port 8080 --vpc-id vpc-xxxxxxxx --health-check-path /  # Crée un groupe cible pour le microservice client sur le port 8080 avec une vérification de santé sur '/'.
aws elbv2 create-target-group --name customer-tg-two --protocol HTTP --port 8080 --vpc-id vpc-xxxxxxxx --health-check-path /  # Crée un deuxième groupe cible pour le microservice client.
aws elbv2 create-target-group --name employee-tg-one --protocol HTTP --port 8080 --vpc-id vpc-xxxxxxxx --health-check-path /admin/suppliers  # Crée un groupe cible pour le microservice employé avec une vérification de santé sur '/admin/suppliers'.
aws elbv2 create-target-group --name employee-tg-two --protocol HTTP --port 8080 --vpc-id vpc-xxxxxxxx --health-check-path /admin/suppliers  # Crée un deuxième groupe cible pour le microservice employé.

# Créer un groupe de sécurité et un Application Load Balancer, configurer des règles d'acheminement du trafic
aws ec2 create-security-group --group-name microservices-sg --description "Microservices SG" --vpc-id vpc-xxxxxxxx  # Crée un groupe de sécurité nommé microservices-sg.
aws ec2 authorize-security-group-ingress --group-id sg-xxxxxxxx --protocol tcp --port 80 --cidr 0.0.0.0/0  # Autorise le trafic entrant sur le port 80 pour le groupe de sécurité.
aws ec2 authorize-security-group-ingress --group-id sg-xxxxxxxx --protocol tcp --port 8080 --cidr 0.0.0.0/0  # Autorise le trafic entrant sur le port 8080 pour le groupe de sécurité.
aws elbv2 create-load-balancer --name microservicesLB --subnets subnet-xxxxxxxx subnet-yyyyyyyy --security-groups sg-xxxxxxxx  # Crée un Application Load Balancer nommé microservicesLB.
aws elbv2 create-listener --load-balancer-arn arn:aws:elasticloadbalancing:us-east-1:xxxxxxxxxxxx:loadbalancer/app/microservicesLB/xxxxxxxxxxxxxxxx --protocol HTTP --port 80 --default-actions Type=forward,TargetGroupArn=arn:aws:elasticloadbalancing:us-east-1:xxxxxxxxxxxx:targetgroup/customer-tg-two/xxxxxxxxxxxxxxxx  # Crée un écouteur sur le port 80 pour le groupe cible customer-tg-two.
aws elbv2 create-listener --load-balancer-arn arn:aws:elasticloadbalancing:us-east-1:xxxxxxxxxxxx:loadbalancer/app/microservicesLB/xxxxxxxxxxxxxxxx --protocol HTTP --port 8080 --default-actions Type=forward,TargetGroupArn=arn:aws:elasticloadbalancing:us-east-1:xxxxxxxxxxxx:targetgroup/customer-tg-one/xxxxxxxxxxxxxxxx  # Crée un écouteur sur le port 8080 pour le groupe cible customer-tg-one.
```

# Phase 7 : Création de deux services Amazon ECS
```bash
# Créer le service ECS pour le microservice client
aws ecs create-service --service-name customer-microservice --cli-input-json file://create-customer-microservice-tg-two.json  # Crée le service ECS

 customer-microservice en utilisant la configuration dans create-customer-microservice-tg-two.json.

# Créer le service ECS pour le microservice employé
aws ecs create-service --service-name employee-microservice --cli-input-json file://create-employee-microservice-tg-two.json  # Crée le service ECS employee-microservice en utilisant la configuration dans create-employee-microservice-tg-two.json.
```

# Phase 8 : Création d'un déploiement CodeDeploy
```bash
# Créer des applications CodeDeploy pour chaque microservice
aws deploy create-application --application-name customer-codedeploy-app --compute-platform ECS  # Crée une application CodeDeploy pour le microservice client.
aws deploy create-application --application-name employee-codedeploy-app --compute-platform ECS  # Crée une application CodeDeploy pour le microservice employé.

# Créer des groupes de déploiement pour chaque microservice
aws deploy create-deployment-group --application-name customer-codedeploy-app --auto-scaling-groups CodeDeployASG --service-role arn:aws:iam::xxxxxxxxxxxx:role/DeployRole --deployment-config-name CodeDeployDefault.ECSAllAtOnce --ecs-services clusterName=microservices-serverlesscluster,serviceName=customer-microservice --load-balancer-info targetGroupPairInfoList={targetGroups=[{name=customer-tg-two},{name=customer-tg-one}],prodTrafficRoute={listenerArns=[arn:aws:elasticloadbalancing:us-east-1:xxxxxxxxxxxx:listener/app/microservicesLB/xxxxxxxxxxxxxxxx]}}  # Crée un groupe de déploiement pour le microservice client.
aws deploy create-deployment-group --application-name employee-codedeploy-app --auto-scaling-groups CodeDeployASG --service-role arn:aws:iam::xxxxxxxxxxxx:role/DeployRole --deployment-config-name CodeDeployDefault.ECSAllAtOnce --ecs-services clusterName=microservices-serverlesscluster,serviceName=employee-microservice --load-balancer-info targetGroupPairInfoList={targetGroups=[{name=employee-tg-two},{name=employee-tg-one}],prodTrafficRoute={listenerArns=[arn:aws:elasticloadbalancing:us-east-1:xxxxxxxxxxxx:listener/app/microservicesLB/xxxxxxxxxxxxxxxx]}}  # Crée un groupe de déploiement pour le microservice employé.
```

# Phase 9 : Création d'un pipeline CodePipeline
```bash
# Créer un pipeline CodePipeline en utilisant une configuration JSON
aws codepipeline create-pipeline --cli-input-json file://create-pipeline.json  # Crée un pipeline CodePipeline en utilisant le fichier de configuration create-pipeline.json.
```

# Annexe : Mettre à jour les conteneurs clients et employés en cours d'exécution sur AWS Cloud9

# Mettre à jour le conteneur client
```bash
# Arrêter et supprimer le conteneur spécifié (nom supposé customer_1)
docker rm -f customer_1  # Arrête et supprime le conteneur Docker nommé customer_1.

# Se positionner dans le répertoire contenant le Dockerfile avant de créer une nouvelle image
cd ~/environment/microservices/customer  # Change de répertoire vers ~/environment/microservices/customer.

# Construire une nouvelle image à partir des fichiers source les plus récents et écraser toute image existante
docker build --tag customer .  # Crée une nouvelle image Docker pour le microservice client.

# Vérifier que la variable dbEndpoint est définie dans votre session terminal
dbEndpoint=$(cat ~/environment/microservices/customer/app/config/config.js | grep 'APP_DB_HOST' | cut -d '"' -f2)  # Extrait l'endpoint de la base de données à partir du fichier de configuration du microservice client.
echo $dbEndpoint  # Affiche l'endpoint de la base de données.

# Créer et exécuter un nouveau conteneur à partir de l'image (et passer l'emplacement de la DB au conteneur)
docker run -d --name customer_1 -p 8080:8080 -e APP_DB_HOST="$dbEndpoint" customer  # Exécute un nouveau conteneur Docker pour le microservice client avec la variable d'environnement APP_DB_HOST définie.

# URL pour tester le microservice s'exécutant sur le conteneur de test AWS Cloud9
echo "Customer microservice test container running at http://"$(curl ifconfig.me):8080  # Affiche l'URL pour tester le conteneur du microservice client.
```

# Mettre à jour le conteneur employé
```bash
# Arrêter et supprimer le conteneur spécifié (nom supposé employee_1)
docker rm -f employee_1  # Arrête et supprime le conteneur Docker nommé employee_1.

# Se positionner dans le répertoire contenant le Dockerfile avant de créer une nouvelle image
cd /home/ec2-user/environment/microservices/employee  # Change de répertoire vers /home/ec2-user/environment/microservices/employee.

# Construire une nouvelle image à partir des fichiers source les plus récents et écraser toute image existante
docker build --tag employee .  # Crée une nouvelle image Docker pour le microservice employé.

# Vérifier que la variable dbEndpoint est définie dans votre session terminal
dbEndpoint=$(cat ~/environment/microservices/customer/app/config/config.js | grep 'APP_DB_HOST' | cut -d '"' -f2)  # Extrait l'endpoint de la base de données à partir du fichier de configuration du microservice employé.
echo $dbEndpoint  # Affiche l'endpoint de la base de données.

# Créer et exécuter un nouveau conteneur à partir de l'image (et passer l'emplacement de la DB au conteneur)
docker run -d --name employee_1 -p 8081:8081 -e APP_DB_HOST="$dbEndpoint" employee  # Exécute un nouveau conteneur Docker pour le microservice employé avec la variable d'environnement APP_DB_HOST définie.

# URL pour tester le microservice s'exécutant sur le conteneur de test AWS Cloud9
echo "Employee microservice test container running at http://"$(curl ifconfig.me):8081/admin/suppliers  # Affiche l'URL pour tester le conteneur du microservice employé.
```

# Référence : Autres commandes Docker
```bash
# Lister les conteneurs en cours d'exécution
docker container ls  # Affiche la liste des conteneurs Docker en cours d'exécution.

# Arrêter et supprimer le conteneur spécifié
docker rm -f <container>  # Arrête et supprime le conteneur Docker spécifié par son nom ou son ID.

# Lister les images Docker disponibles
docker images  # Affiche la liste des images Docker disponibles localement.

# Créer une nouvelle image à partir d'un Dockerfile
docker build --tag <tag-for-image> .  # Crée une nouvelle image Docker à partir d'un Dockerfile dans le répertoire actuel.

# Exécuter un conteneur à partir d'une image Docker
docker run -d --name <name-to-give-container> -p <port>:<port> <image-tag>  # Exécute un conteneur Docker en arrière-plan à partir d'une image Docker spécifiée, en mappant les ports spécifiés.

# Lister les conteneurs Docker en cours d'exécution
docker ps  # Affiche la liste des conteneurs Docker en cours d'exécution.
```

# Référence : Analyser le réseau et consulter les journaux Docker
```bash
# Commandes utiles pour voir ce qui se passe
sudo lsof -i :8080  # Affiche les fichiers ouverts par le processus écoutant sur le port 8080 pour diagnostiquer les problèmes réseau.
sudo lsof -i :8081  # Affiche les fichiers ouverts par le processus écoutant sur le port 8081 pour diagnostiquer les problèmes réseau.
ps -ef | head -1; ps -ef | grep docker  # Affiche les processus Docker en cours d'exécution pour vérifier l'état des conteneurs.

# Visualisation des journaux Docker - retourne les numéros des conteneurs
sudo ls /var/lib/docker/containers  # Liste les répertoires des conteneurs Docker pour accéder aux journaux spécifiques.

# Voir les journaux pour un conteneur où vous connaissez le numéro du conteneur
sudo less /var/lib/docker/containers/<container-number>/*.log  # Affiche les journaux d'un conteneur Docker spécifique pour le dépannage.

# Voir les adresses IP utilisées par les conteneurs Docker
docker inspect network bridge  # Affiche les informations réseau du pont Docker pour voir les adresses IP des conteneurs.
```

# Réassocier les groupes cibles à l'équilibreur de charge
```bash
# Accéder à la console Amazon EC2 et configurer les écouteurs et règles de l'Application Load Balancer manuellement
# Aucune commande CLI pour cette étape, effectuer les configurations via la console AWS.
```

# Conseils de dépannage
```bash
# Vérifier les journaux Amazon CloudWatch pour obtenir les détails des erreurs
# Utiliser la console AWS CloudWatch pour vérifier les journaux.

# Vérifier que votre instance AWS Cloud9 est exécutée dans le Sous-réseau public 1
# Utiliser la console AWS VPC pour vérifier la configuration du sous-réseau.

# Vérifier les détails du déploiement dans la console Amazon ECS et AWS CodeDeploy
# Utiliser les consoles AWS ECS et CodeDeploy pour surveiller l'état des déploiements et services.
```

