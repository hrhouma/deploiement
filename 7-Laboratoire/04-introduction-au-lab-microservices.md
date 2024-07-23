⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰
#  1 - Objectif de ce laboratoire :
⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰

- Le présent laboratoire, centré sur l'utilisation des microservices et de Docker en conjonction avec AWS. Il vise à illustrer et à renforcer de manière pratique les compétences théoriques enseignées, en offrant une application concrète des concepts de conteneurisation, de déploiement de microservices, et de gestion d'infrastructures cloud. Par ce biais, les étudiants peuvent approfondir leur compréhension des méthodes modernes de gestion des applications Big Data, en particulier en ce qui concerne la scalabilité, la résilience et l'efficacité opérationnelle.

⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰
# 2 - Introduction aux concepts visées
⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰

## **1. Compréhension des Architectures**
- **Concepts de base** : Le cours de déploiement enseigne les différentes architectures de systèmes, notamment les architectures monolithiques et microservices. Le laboratoire permet aux étudiants de voir concrètement comment une application peut être transformée d'une architecture monolithique à une architecture de microservices.
- **Avantages des Microservices** : En déployant des microservices, les étudiants apprennent les avantages pratiques tels que la scalabilité, la résilience et la flexibilité, qui sont essentiels pour gérer des applications Big Data.

## **2. Utilisation de Docker**
- **Conteneurisation** : Docker est un outil clé pour le déploiement d'applications. Dans le cadre du programme Big Data, savoir conteneuriser des applications permet de gérer efficacement les ressources et de déployer des applications de manière cohérente dans différents environnements.
- **Gestion des Conteneurs** : Les étudiants apprennent à créer, déployer et gérer des conteneurs Docker, ce qui est crucial pour les environnements de production Big Data.

## **3. Déploiement sur AWS**
- **Amazon ECS** : Le cours de déploiement couvre l'utilisation de services cloud pour le déploiement d'applications. En utilisant Amazon ECS, les étudiants apprennent à déployer des microservices de manière scalable et résiliente, en utilisant les meilleures pratiques de l'industrie.
- **Mise à l'Échelle** : Le laboratoire montre comment mettre à l'échelle les microservices indépendamment, une compétence essentielle pour gérer des charges de travail variables dans les applications Big Data.

## **4. Gestion et Surveillance**
- **AWS CloudWatch** : La surveillance des performances des microservices via AWS CloudWatch est une compétence clé pour assurer la disponibilité et la performance des applications Big Data.
- **Mise à Jour et Maintenance** : Le laboratoire enseigne également comment mettre à jour et maintenir des microservices déployés, ce qui est crucial pour les environnements de production.

⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰
# 3 - Étapes du Laboratoire et concept par étape
⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰

## **Étape 1 : Introduction aux Microservices**
- **Concept** : Introduction aux architectures de systèmes.
- **Laboratoire** : Compréhension des microservices et de leurs avantages.

## **Étape 2 : Déploiement d'une Application Monolithique dans Docker**
- **Concept** : Utilisation de Docker pour la conteneurisation.
- **Laboratoire** : Création et déploiement d'une image Docker pour une application monolithique.

## **Étape 3 : Transformation de l'Application en Microservices**
- **Concept** : Découpage et conception de microservices.
- **Laboratoire** : Transformation d'une application monolithique en microservices indépendants.

## **Étape 4 : Déploiement des Microservices sur AWS**
- **Concept** : Utilisation des services cloud pour le déploiement.
- **Laboratoire** : Déploiement des microservices sur Amazon ECS et utilisation d'un Load Balancer.

## **Étape 5 : Gestion et Mise à l'Échelle**
- **Concept** : Surveillance et mise à l'échelle des applications.
- **Laboratoire** : Utilisation d'AWS CloudWatch pour la surveillance et mise à l'échelle des microservices.

⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰
# 4 - Objectifs spécifiques 
⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰


1. **Comprendre les architectures monolithiques vs microservices** : Apprendre pourquoi les microservices sont souvent préférés pour les applications modernes.
2. **Déployer une application monolithique dans un conteneur Docker** : Voir comment Docker simplifie le déploiement et la gestion des applications.
3. **Découper l'application monolithique en microservices** : Transformer une application monolithique en plusieurs microservices indépendants.
4. **Déployer les microservices sur AWS** : Utiliser Amazon ECS pour gérer les conteneurs et assurer la scalabilité et la résilience de l'application.

⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰
# 5 - Étapes en profondeur 
⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰



### **1. Introduction aux Microservices**
- **Définition** : Les microservices sont une approche architecturale où une application est composée de petits services indépendants qui communiquent entre eux via des APIs bien définies[3][4].
- **Avantages** :
  - **Scalabilité** : Chaque microservice peut être mis à l'échelle indépendamment.
  - **Résilience** : La défaillance d'un microservice n'affecte pas les autres.
  - **Flexibilité** : Les équipes peuvent utiliser différentes technologies pour différents services.

### **2. Déploiement d'une Application Monolithique dans Docker**
- **Docker** : Une plateforme qui permet de créer, déployer et gérer des conteneurs.
- **Étapes** :
  1. **Installer Docker** : Suivre les instructions pour installer Docker sur votre machine.
  2. **Créer une image Docker** : Utiliser un Dockerfile pour définir l'environnement de l'application.
  3. **Exécuter le conteneur** : Utiliser la commande `docker run` pour démarrer l'application dans un conteneur.

### **3. Transformation de l'Application en Microservices**
- **Découpage de l'application** : Identifier les composants de l'application qui peuvent être transformés en services indépendants.
- **Création des microservices** :
  1. **Développer chaque microservice** : Créer des services indépendants pour chaque fonctionnalité de l'application.
  2. **Conteneuriser chaque microservice** : Créer une image Docker pour chaque microservice.
  3. **Stocker les images** : Utiliser Amazon ECR (Elastic Container Registry) pour stocker les images Docker.

### **4. Déploiement des Microservices sur AWS**
- **Amazon ECS (Elastic Container Service)** : Un service de gestion de conteneurs qui permet de déployer et gérer des applications conteneurisées.
- **Étapes** :
  1. **Créer un cluster ECS** : Utiliser AWS Management Console pour créer un cluster.
  2. **Déployer les services** : Utiliser la commande `aws ecs update-service` pour déployer chaque microservice sur le cluster[1].
  3. **Utiliser un Load Balancer** : Configurer un Application Load Balancer (ALB) pour diriger le trafic vers les microservices appropriés.

### **5. Gestion et Mise à l'Échelle**
- **Surveillance** : Utiliser AWS CloudWatch pour surveiller les performances des microservices.
- **Mise à l'échelle** : Ajuster le nombre de conteneurs en fonction de la charge de travail[2].

⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰
# 6 - Services AWS utilisés dans le projet et leurs rôles
⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰


| **Service AWS**                | **Rôle**                                                         | **Description**                                                                                                                                       |
|--------------------------------|------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| Utilisateurs                   | Accès aux services                                               | Clients et employés interagissent avec l'application via un navigateur web.                                                                            |
| Application Load Balancer (ALB)| Répartition du trafic                                            | Distribue les requêtes des utilisateurs vers les microservices appropriés en fonction des règles de routage définies.                                   |
| ECS (Elastic Container Service)| Hébergement des microservices                                    | Service pour déployer, gérer et faire évoluer des conteneurs Docker sur AWS.                                                                            |
| Docker Containers              | Conteneurisation des applications                                | Conteneurs encapsulant les microservices, assurant leur portabilité et leur isolation.                                                                 |
| ECR (Elastic Container Registry)| Stockage des images Docker                                      | Service de registre Docker entièrement géré pour stocker, gérer et déployer des images Docker.                                                         |
| CodeCommit                     | Référentiel de code source                                       | Service de contrôle de version basé sur Git pour stocker le code source des microservices et les fichiers de configuration.                            |
| CodePipeline                   | Automatisation du CI/CD                                          | Service de livraison continue pour automatiser les étapes de construction, de test et de déploiement du code.                                          |
| CodeDeploy                     | Déploiement automatique                                          | Service pour automatiser les déploiements d'applications sur divers services de calcul tels qu'Amazon ECS et AWS Lambda.                                |
| RDS (Relational Database Service)| Stockage de données                                            | Service de base de données relationnelle pour stocker les données de l'application, comme les informations sur les fournisseurs.                       |
| CloudWatch                     | Surveillance et journalisation                                   | Service de surveillance et de gestion des journaux pour collecter et suivre les métriques, collecter et surveiller les fichiers journaux.              |

⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰
# 7 - Explication des rôles
⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰

1. **Utilisateurs** : Les clients et les employés accèdent à l'application via un navigateur web.
2. **Application Load Balancer (ALB)** : Il répartit le trafic des utilisateurs entre les microservices en fonction des règles de routage définies.
3. **ECS (Elastic Container Service)** : Héberge et exécute les microservices dans des conteneurs Docker, permettant la gestion et la mise à l'échelle automatique.
4. **Docker Containers** : Ils encapsulent les microservices, assurant leur portabilité et leur isolation par rapport à l'infrastructure sous-jacente. 
5. **ECR (Elastic Container Registry)** : Stocke et gère les images Docker utilisées par les microservices, facilitant leur déploiement. 
6. **CodeCommit** : Stocke le code source et les fichiers de configuration des microservices, permettant le versionnage et la collaboration. 
7. **CodePipeline** : Automatise le pipeline de CI/CD, orchestrant les étapes de construction, de test et de déploiement des microservices. 
8. **CodeDeploy** : Automatiser les déploiements des microservices sur ECS, permettant des mises à jour continues et fiables. 
9. **RDS (Relational Database Service)** : Fournit une base de données relationnelle pour stocker les données de l'application, telle que les informations sur les fournisseurs. 
10. **CloudWatch** : Surveille les performances des services et collecte les journaux, aidant à détecter et à diagnostiquer les problèmes. 

## **Diagramme de l'Architecture**

```plaintext
+-----------------+   +--------------------------------------------+   +-----------------+
|   Utilisateurs  |   |        Application Load Balancer (ALB)     |   |   Utilisateurs  |
| (Clients & Empl)|-->|--------------------------------------------|<--|   (Clients)     |
+-----------------+   |                                            |   +-----------------+
                      |               |                |            |
                      |               |                |            |
                      v               v                v            v
               +-----------------+   +--------------------+   +--------------------+
               | Customer Service|   | Employee Service   |   | Customer Service   |
               |     (ECS)       |   |      (ECS)         |   |      (ECS)         |
               +-----------------+   +--------------------+   +--------------------+
                      |                    |                   |           |
                      |                    |                   |           |
                      v                    v                   v           v
               +-----------------+   +--------------------+   +--------------------+
               |  Docker Cont.   |   |   Docker Cont.     |   |   Docker Cont.     |
               +-----------------+   +--------------------+   +--------------------+
                      |                    |                   |           |
                      |                    |                   |           |
                      v                    v                   v           v
               +-----------------+   +--------------------+   +--------------------+
               |       ECR       |   |        ECR         |   |        ECR         |
               +-----------------+   +--------------------+   +--------------------+
                      |                    |                   |           |
                      |                    |                   |           |
                      v                    v                   v           v
               +-----------------+   +--------------------+   +--------------------+
               |   CodeCommit    |   |    CodeCommit      |   |    CodeCommit      |
               +-----------------+   +--------------------+   +--------------------+
                      |                    |                   |           |
                      |                    |                   |           |
                      v                    v                   v           v
               +-----------------+   +--------------------+   +--------------------+
               |  CodePipeline   |   |   CodePipeline     |   |   CodePipeline     |
               +-----------------+   +--------------------+   +--------------------+
                      |                    |                   |           |
                      |                    |                   |           |
                      v                    v                   v           v
               +-----------------+   +--------------------+   +--------------------+
               |  CodeDeploy     |   |    CodeDeploy      |   |    CodeDeploy      |
               +-----------------+   +--------------------+   +--------------------+
                      |                    |                   |           |
                      |                    |                   |           |
                      v                    v                   v           v
               +-----------------+   +--------------------+   +--------------------+
               |       RDS       |   |         RDS        |   |         RDS        |
               +-----------------+   +--------------------+   +--------------------+
                      |                    |                   |           |
                      |                    |                   |           |
                      v                    v                   v           v
               +-----------------+   +--------------------+   +--------------------+
               |    CloudWatch   |   |     CloudWatch     |   |     CloudWatch     |
               +-----------------+   +--------------------+   +--------------------+
```

Ce diagramme illustre les principaux composants de l'architecture, leur interconnexion, et comment les services AWS sont utilisés pour gérer les *(1) microservices*, *(2) le déploiement*, et *(3) la surveillance*.


⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰
# 8 - Tâches
⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰


# Phase 1 : Planification de la conception et estimation des coûts
- **Tâche 1.1 : Créer un diagramme d'architecture**
- **Tâche 1.2 : Élaborer une estimation des coûts**

# Phase 2 : Analyse de l'infrastructure de l'application monolithique
- **Tâche 2.1 : Vérifier la disponibilité de l'application monolithique**
- **Tâche 2.2 : Tester l'application web monolithique**
- **Tâche 2.3 : Analyser le mode d'exécution de l'application monolithique**

# Phase 3 : Création d'un environnement de développement et enregistrement du code dans un référentiel Git
- **Tâche 3.1 : Créer un IDE AWS Cloud9 comme environnement de travail**
- **Tâche 3.2 : Copier le code de l'application dans votre IDE**
- **Tâche 3.3 : Créer des répertoires de travail avec un code de démarrage pour les deux microservices**
- **Tâche 3.4 : Créer un référentiel Git pour le code des microservices et pousser le code dans CodeCommit**

# Phase 4 : Configuration de l'application comme deux microservices et test de ceux-ci dans des conteneurs Docker
- **Tâche 4.1 : Ajuster les paramètres de groupe de sécurité de l'instance AWS Cloud9**
- **Tâche 4.2 : Modifier le code source du microservice client**
- **Tâche 4.3 : Créer le fichier Dockerfile du microservice client et lancer un conteneur de test**
- **Tâche 4.4 : Modifier le code source du microservice employé**
- **Tâche 4.5 : Créer le fichier Dockerfile du microservice employé et lancer un conteneur de test**
- **Tâche 4.6 : Ajuster le port du microservice employé et recréer l'image**
- **Tâche 4.7 : Enregistrer le code dans CodeCommit**

# Phase 5 : Création de référentiels ECR, d'un cluster ECS, de définitions de tâche et de fichiers AppSpec
- **Tâche 5.1 : Créer des référentiels ECR et charger les images Docker**
- **Tâche 5.2 : Créer un cluster ECS**
- **Tâche 5.3 : Créer un référentiel CodeCommit pour stocker les fichiers de déploiement**
- **Tâche 5.4 : Créer des fichiers de définition de tâches pour chaque microservice et les enregistrer auprès d'Amazon ECS**
- **Tâche 5.5 : Créer des fichiers AppSpec pour CodeDeploy pour chaque microservice**
- **Tâche 5.6 : Mettre à jour les fichiers et les enregistrer dans CodeCommit**

# Phase 6 : Création de groupes cibles et d'un Application Load Balancer
- **Tâche 6.1 : Créer quatre groupes cibles**
- **Tâche 6.2 : Créer un groupe de sécurité et un Application Load Balancer, et configurer des règles d'acheminement du trafic**

# Phase 7 : Création de deux services Amazon ECS
- **Tâche 7.1 : Créer le service ECS pour le microservice client**
- **Tâche 7.2 : Créer le service Amazon ECS pour le microservice employé**

# Phase 8 : Configuration de CodeDeploy et CodePipeline
- **Tâche 8.1 : Créer une application et des groupes de déploiement CodeDeploy**
- **Tâche 8.2 : Créer un pipeline pour le microservice client**
- **Tâche 8.3 : Tester le pipeline CI/CD pour le microservice client**
- **Tâche 8.4 : Créer un pipeline pour le microservice employé**
- **Tâche 8.5 : Tester le pipeline CI/CD pour le microservice employé**
- **Tâche 8.6 : Observer comment CodeDeploy a modifié les règles de l'écouteur de l'équilibreur de charge**

# Phase 9 : Ajustement du code du microservice pour relancer l'exécution d'un pipeline
- **Tâche 9.1 : Limiter l'accès au microservice employé**
- **Tâche 9.2 : Ajuster l'interface utilisateur pour le microservice employé et pousser l'image mise à jour dans Amazon ECR**
- **Tâche 9.3 : Vérifier que le pipeline employé a été exécuté et que le microservice a été mis à jour**
- **Tâche 9.4 : Tester l'accès au microservice employé**
- **Tâche 9.5 : Mettre à l'échelle le microservice client**

## **Conclusion**

Ce laboratoire permet aux étudiants d'appliquer les concepts théoriques appris dans le cours de déploiement du programme Big Data. En travaillant sur des cas pratiques de déploiement, de gestion et de mise à l'échelle des microservices, les étudiants acquièrent des compétences essentielles pour gérer des environnements Big Data modernes et complexes.

⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰
# Annexe-01: 
⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰

### Commandes et Description dans les Commentaires

# Phase 1 : Planification de la conception et estimation des coûts
```yaml
# Aucune commande spécifique à exécuter pour cette phase
```

# Phase 2 : Analyse de l'infrastructure de l'application monolithique
```bash
# Vérifier la disponibilité de l'application monolithique
sudo lsof -i :80  # Liste des fichiers ouverts par le processus écoutant sur le port 80

# Analyser le mode d'exécution de l'application monolithique
ps -ef | head -1  # Affiche les informations de l'en-tête du processus
ps -ef | grep node  # Recherche les processus associés au nœud
```

# Phase 3 : Création d'un environnement de développement et enregistrement du code dans un référentiel Git
```bash
# Créer un IDE AWS Cloud9
aws cloud9 create-environment-ec2 --name MicroservicesIDE --instance-type t3.small --image-id amazonlinux-2 --subnet-id subnet-xxxxxxxx  # Crée un environnement Cloud9

# Copier le code de l'application dans votre IDE
scp -r -i ~/environment/labsuser.pem ubuntu@<instance-ip>:/home/ubuntu/resources/codebase_partner/* ~/environment/temp/  # Copie le code source de l'application vers l'IDE Cloud9

# Initialiser le répertoire Git et pousser le code dans CodeCommit
cd ~/environment/microservices
git init  # Initialise un nouveau référentiel Git
git branch -m dev  # Renomme la branche principale en dev
git add .  # Ajoute tous les fichiers au suivi Git
git commit -m 'two unmodified copies of the application code'  # Valide les modifications avec un message
git remote add origin https://git-codecommit.us-east-1.amazonaws.com/v1/repos/microservices  # Ajoute le référentiel distant
git push -u origin dev  # Pousse les modifications vers le référentiel distant sur la branche dev
```

# Phase 4 : Configuration de l'application comme deux microservices et test de ceux-ci dans des conteneurs Docker
```bash
# Ajuster les paramètres de groupe de sécurité de l'instance AWS Cloud9
aws ec2 authorize-security-group-ingress --group-id sg-xxxxxxxx --protocol tcp --port 8080-8081 --cidr 0.0.0.0/0  # Autorise le trafic entrant sur les ports 8080 et 8081

# Créer une image Docker pour le microservice client et lancer un conteneur de test
cd ~/environment/microservices/customer
docker build --tag customer .  # Crée une image Docker à partir du Dockerfile
docker run -d --name customer_1 -p 8080:8080 -e APP_DB_HOST="$dbEndpoint" customer  # Exécute un conteneur Docker à partir de l'image

# Créer une image Docker pour le microservice employé et lancer un conteneur de test
cd ~/environment/microservices/employee
docker build --tag employee .  # Crée une image Docker à partir du Dockerfile
docker run -d --name employee_1 -p 8081:8081 -e APP_DB_HOST="$dbEndpoint" employee  # Exécute un conteneur Docker à partir de l'image
```

# Phase 5 : Création de référentiels ECR, d'un cluster ECS, de définitions de tâche et de fichiers AppSpec
```bash
# Autoriser le client Docker à se connecter à Amazon ECR
account_id=$(aws sts get-caller-identity | grep Account | cut -d '"' -f4)
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin $account_id.dkr.ecr.us-east-1.amazonaws.com  # Connecte Docker à Amazon ECR

# Créer des référentiels ECR et charger les images Docker
docker tag customer:latest $account_id.dkr.ecr.us-east-1.amazonaws.com/customer:latest  # Balise l'image Docker client
docker tag employee:latest $account_id.dkr.ecr.us-east-1.amazonaws.com/employee:latest  # Balise l'image Docker employé
docker push $account_id.dkr.ecr.us-east-1.amazonaws.com/customer:latest  # Pousse l'image Docker client vers ECR
docker push $account_id.dkr.ecr.us-east-1.amazonaws.com/employee:latest  # Pousse l'image Docker employé vers ECR

# Créer un cluster ECS
aws ecs create-cluster --cluster-name microservices-serverlesscluster  # Crée un cluster ECS

# Enregistrer les définitions de tâche dans Amazon ECS
aws ecs register-task-definition --cli-input-json file://taskdef-customer.json  # Enregistre la définition de tâche pour le client
aws ecs register-task-definition --cli-input-json file://taskdef-employee.json  # Enregistre la définition de tâche pour l'employé
```

# Phase 6 : Création de groupes cibles et d'un Application Load Balancer
```bash
# Créer des groupes cibles
aws elbv2 create-target-group --name customer-tg-one --protocol HTTP --port 8080 --vpc-id vpc-xxxxxxxx --health-check-path /  # Crée un groupe cible pour le client
aws elbv2 create-target-group --name customer-tg-two --protocol HTTP --port 8080 --vpc-id vpc-xxxxxxxx --health-check-path /  # Crée un deuxième groupe cible pour le client
aws elbv2 create-target-group --name employee-tg-one --protocol HTTP --port 8080 --vpc-id vpc-xxxxxxxx --health-check-path /admin/suppliers  # Crée un groupe cible pour l'employé
aws elbv2 create-target-group --name employee-tg-two --protocol HTTP --port 8080 --vpc-id vpc-xxxxxxxx --health-check-path /admin/suppliers  # Crée un deuxième groupe cible pour l'employé

# Créer un groupe de sécurité et un Application Load Balancer, configurer des règles d'acheminement du trafic
aws ec2 create-security-group --group-name microservices-sg --description "Microservices SG" --vpc-id vpc-xxxxxxxx  # Crée un groupe de sécurité
aws ec2 authorize-security-group-ingress --group-id sg-xxxxxxxx --protocol tcp --port 80 --cidr 0.0.0.0/0  # Autorise le trafic entrant sur le port 80
aws ec2 authorize-security-group-ingress --group-id sg-xxxxxxxx --protocol tcp --port 8080 --cidr 0.0.0.0/0  # Autorise le trafic entrant sur le port 8080
aws elbv2 create-load-balancer --name microservicesLB --subnets subnet-xxxxxxxx subnet-yyyyyyyy --security-groups sg-xxxxxxxx  # Crée un Application Load Balancer
aws elbv2 create-listener --load-balancer-arn arn:aws:elasticloadbalancing:us-east-1:xxxxxxxxxxxx:loadbalancer/app/microservicesLB/xxxxxxxxxxxxxxxx --protocol HTTP --port 80 --default-actions Type=forward,TargetGroupArn=arn:aws:elasticloadbalancing:us-east-1:xxxxxxxxxxxx:targetgroup/customer-tg-two/xxxxxxxxxxxxxxxx  # Crée un écouteur sur le port 80
aws elbv2 create-listener --load-balancer-arn arn:aws:elasticloadbalancing:us-east-1:xxxxxxxxxxxx:loadbalancer/app/microservicesLB/xxxxxxxxxxxxxxxx --protocol HTTP --port 8080 --default-actions Type=forward,TargetGroupArn=arn:aws:elasticloadbalancing:us-east-1:xxxxxxxxxxxx:targetgroup/customer-tg-one/xxxxxxxxxxxxxxxx  # Crée un écouteur sur le port 8080
```

# Phase 7 : Création de deux services Amazon ECS
```bash
# Créer le service ECS pour le microservice client
aws ecs create-service --service-name customer-microservice --cli-input-json file://create-customer-microservice-tg-two.json  # Crée le service ECS pour le client

# Créer le service ECS pour le microservice employé
aws ecs create-service --service-name employee-microservice --cli-input-json file://create-employee-microservice-tg-two.json  # Crée le service ECS pour l'employé
```

# Phase 8 : Configuration de CodeDeploy et CodePipeline
```bash
# Créer une application CodeDeploy
aws deploy create-application --application-name microservices --compute-platform ECS  # Crée une application CodeDeploy

# Créer des groupes de déploiement CodeDeploy
aws deploy create-deployment-group --application-name microservices --deployment-group-name microservices-customer --service-role-arn arn:aws:iam::xxxxxxxxxxxx:role/DeployRole --deployment-config-name CodeDeployDefault.ECSAllAtOnce --ecs-services clusterName=microservices-serverlesscluster,serviceName=customer-microservice --load-balancer-info targetGroupPairInfoList={targetGroups=[{name=customer-tg-two},{name=customer-tg-one}],prodTrafficRoute={listenerArns=[arn:aws:elasticloadbalancing:us-east-1:xxxxxxxxxxxx:listener/app/microservicesLB/xxxxxxxxxxxxxxxx]}}  # Crée un groupe de déploiement pour le client

aws deploy create-deployment-group --application-name microservices --deployment-group-name microservices-employee --service-role-arn arn:aws:iam

::xxxxxxxxxxxx:role/DeployRole --deployment-config-name CodeDeployDefault.ECSAllAtOnce --ecs-services clusterName=microservices-serverlesscluster,serviceName=employee-microservice --load-balancer-info targetGroupPairInfoList={targetGroups=[{name=employee-tg-two},{name=employee-tg-one}],prodTrafficRoute={listenerArns=[arn:aws:elasticloadbalancing:us-east-1:xxxxxxxxxxxx:listener/app/microservicesLB/xxxxxxxxxxxxxxxx]}}  # Crée un groupe de déploiement pour l'employé

# Créer un pipeline CodePipeline
aws codepipeline create-pipeline --cli-input-json file://create-pipeline.json  # Crée un pipeline CodePipeline
```

# Annexe-02

# Mettre à jour le conteneur client en cours d'exécution sur AWS Cloud9
```bash
# Arrêter et supprimer le conteneur spécifié (nom supposé customer_1)
docker rm -f customer_1  # Supprime le conteneur customer_1

# Se positionner dans le répertoire contenant le Dockerfile avant de créer une nouvelle image
cd ~/environment/microservices/customer  # Change de répertoire vers ~/environment/microservices/customer

# Construire une nouvelle image à partir des fichiers source les plus récents et écraser toute image existante
docker build --tag customer .  # Crée une nouvelle image Docker pour le client

# Vérifier que la variable dbEndpoint est définie dans votre session terminal
dbEndpoint=$(cat ~/environment/microservices/customer/app/config/config.js | grep 'APP_DB_HOST' | cut -d '"' -f2)  # Extrait l'endpoint de la base de données à partir du fichier de configuration
echo $dbEndpoint  # Affiche la valeur de l'endpoint de la base de données

# Créer et exécuter un nouveau conteneur à partir de l'image (et passer l'emplacement de la DB au conteneur)
docker run -d --name customer_1 -p 8080:8080 -e APP_DB_HOST="$dbEndpoint" customer  # Exécute un nouveau conteneur Docker pour le client

# URL pour tester le microservice s'exécutant sur le conteneur de test AWS Cloud9
echo "Customer microservice test container running at http://"$(curl ifconfig.me):8080  # Affiche l'URL pour tester le conteneur client
```

# Mettre à jour le conteneur employé en cours d'exécution sur AWS Cloud9
```bash
# Arrêter et supprimer le conteneur spécifié (nom supposé employee_1)
docker rm -f employee_1  # Supprime le conteneur employee_1

# Se positionner dans le répertoire contenant le Dockerfile avant de créer une nouvelle image
cd /home/ec2-user/environment/microservices/employee  # Change de répertoire vers /home/ec2-user/environment/microservices/employee

# Construire une nouvelle image à partir des fichiers source les plus récents et écraser toute image existante
docker build --tag employee .  # Crée une nouvelle image Docker pour l'employé

# Vérifier que la variable dbEndpoint est définie dans votre session terminal
dbEndpoint=$(cat ~/environment/microservices/customer/app/config/config.js | grep 'APP_DB_HOST' | cut -d '"' -f2)  # Extrait l'endpoint de la base de données à partir du fichier de configuration
echo $dbEndpoint  # Affiche la valeur de l'endpoint de la base de données

# Créer et exécuter un nouveau conteneur à partir de l'image (et passer l'emplacement de la DB au conteneur)
docker run -d --name employee_1 -p 8081:8081 -e APP_DB_HOST="$dbEndpoint" employee  # Exécute un nouveau conteneur Docker pour l'employé

# URL pour tester le microservice s'exécutant sur le conteneur de test AWS Cloud9
echo "Employee microservice test container running at http://"$(curl ifconfig.me):8081/admin/suppliers  # Affiche l'URL pour tester le conteneur employé
```

# Référence : Autres commandes Docker
```bash
# Lister les conteneurs en cours d'exécution
docker container ls  # Affiche la liste des conteneurs Docker en cours d'exécution

# Arrêter et supprimer le conteneur spécifié
docker rm -f <container>  # Supprime le conteneur spécifié

# Lister les images
docker images  # Affiche la liste des images Docker

# Créer une nouvelle image à partir d'un Dockerfile (doit être dans le même répertoire que le Dockerfile)
docker build --tag <tag-for-image> .  # Crée une nouvelle image Docker à partir d'un Dockerfile

# Exécuter un conteneur à partir d'une image
docker run -d --name <name-to-give-container> -p <port>:<port> <image-tag>  # Exécute un conteneur Docker à partir d'une image

# Lister les conteneurs Docker en cours d'exécution
docker ps  # Affiche la liste des conteneurs Docker en cours d'exécution
```

# Référence : Analyser le réseau et consulter les journaux Docker
```bash
# Commandes utiles pour voir ce qui se passe
sudo lsof -i :8080  # Affiche les fichiers ouverts par le processus écoutant sur le port 8080
sudo lsof -i :8081  # Affiche les fichiers ouverts par le processus écoutant sur le port 8081
ps -ef | head -1; ps -ef | grep docker  # Affiche les processus Docker en cours d'exécution

# Visualisation des journaux Docker - retourne les numéros des conteneurs
sudo ls /var/lib/docker/containers  # Liste les répertoires des conteneurs Docker

# Voir les journaux pour un conteneur où vous connaissez le numéro du conteneur
sudo less /var/lib/docker/containers/<container-number>/*.log  # Affiche les journaux d'un conteneur spécifique

# Voir les adresses IP utilisées par les conteneurs Docker
docker inspect network bridge  # Affiche les informations réseau du pont Docker
```

# Réassocier les groupes cibles à l'équilibreur de charge
```bash
# Accéder à la console Amazon EC2 et configurer les écouteurs et règles de l'Application Load Balancer manuellement
# Aucune commande CLI pour cette étape, effectuer les configurations via la console AWS
```

# Conseils de dépannage
```bash
# Vérifier les journaux Amazon CloudWatch pour obtenir les détails des erreurs
# Utiliser la console AWS CloudWatch

# Vérifier que votre instance AWS Cloud9 est exécutée dans le Sous-réseau public 1
# Utiliser la console AWS VPC

# Vérifier les détails du déploiement dans la console Amazon ECS
# Utiliser la console AWS ECS

# Vérifier les événements dans la console AWS CloudTrail
# Utiliser la console AWS CloudTrail

# Consulter les journaux dans la console CloudWatch
# Utiliser la console AWS CloudWatch
```


# Citations :


[2] https://aws.amazon.com/tutorials/break-monolith-app-microservices-ecs-docker-ec2/

[3] https://aws.amazon.com/fr/microservices/

[4] https://docs.aws.amazon.com/whitepapers/latest/microservices-on-aws/microservices-on-aws.html

[5] https://www.youtube.com/watch?v=_ep_yKuDWkE

[6] https://docker-curriculum.com


