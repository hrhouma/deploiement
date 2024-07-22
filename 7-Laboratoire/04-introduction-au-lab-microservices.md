⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰
#  1 - Objectif de ce laboratoire :
⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰

- Le présent laboratoire, centré sur l'utilisation des microservices et de Docker en conjonction avec AWS, s'inscrit de manière cohérente et approfondie dans le cadre du cours de déploiement dispensé au sein du programme Big Data. Il vise à illustrer et à renforcer de manière pratique les compétences théoriques enseignées, en offrant une application concrète des concepts de conteneurisation, de déploiement de microservices, et de gestion d'infrastructures cloud. Par ce biais, les étudiants peuvent approfondir leur compréhension des méthodes modernes de gestion des applications Big Data, en particulier en ce qui concerne la scalabilité, la résilience et l'efficacité opérationnelle.

⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰⏰
# 2 - Concepts visées
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

# 3 - Étapes du Laboratoire en Relation avec le Cours**

# **Étape 1 : Introduction aux Microservices**
- **Cours** : Introduction aux architectures de systèmes.
- **Laboratoire** : Compréhension des microservices et de leurs avantages.

# **Étape 2 : Déploiement d'une Application Monolithique dans Docker**
- **Cours** : Utilisation de Docker pour la conteneurisation.
- **Laboratoire** : Création et déploiement d'une image Docker pour une application monolithique.

# **Étape 3 : Transformation de l'Application en Microservices**
- **Cours** : Découpage et conception de microservices.
- **Laboratoire** : Transformation d'une application monolithique en microservices indépendants.

# **Étape 4 : Déploiement des Microservices sur AWS**
- **Cours** : Utilisation des services cloud pour le déploiement.
- **Laboratoire** : Déploiement des microservices sur Amazon ECS et utilisation d'un Load Balancer.

# **Étape 5 : Gestion et Mise à l'Échelle**
- **Cours** : Surveillance et mise à l'échelle des applications.
- **Laboratoire** : Utilisation d'AWS CloudWatch pour la surveillance et mise à l'échelle des microservices.

## **Conclusion**

Ce laboratoire permet aux étudiants d'appliquer les concepts théoriques appris dans le cours de déploiement du programme Big Data. En travaillant sur des cas pratiques de déploiement, de gestion et de mise à l'échelle des microservices, les étudiants acquièrent des compétences essentielles pour gérer des environnements Big Data modernes et complexes.

## **Objectifs du Laboratoire**

1. **Comprendre les architectures monolithiques vs microservices** : Apprendre pourquoi les microservices sont souvent préférés pour les applications modernes.
2. **Déployer une application monolithique dans un conteneur Docker** : Voir comment Docker simplifie le déploiement et la gestion des applications.
3. **Découper l'application monolithique en microservices** : Transformer une application monolithique en plusieurs microservices indépendants.
4. **Déployer les microservices sur AWS** : Utiliser Amazon ECS pour gérer les conteneurs et assurer la scalabilité et la résilience de l'application.

## **Étapes du Laboratoire**

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

## **Services AWS utilisés dans le projet et leurs rôles :**

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

## **Explication des rôles**

1. **Utilisateurs** : Les clients et les employés accèdent à l'application via un navigateur web.
2. **Application Load Balancer (ALB)** : Il répartit le trafic des utilisateurs entre les microservices en fonction des règles de routage définies.
3. **ECS (Elastic Container Service)** : Héberge et exécute les microservices dans des conteneurs Docker, permettant la gestion et la mise à l'échelle automatique.
4. **Docker Containers** : Ils encapsulent les microservices

, assurant leur portabilité et leur isolation par rapport à l'infrastructure sous-jacente.
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

# Citations :


[2] https://aws.amazon.com/tutorials/break-monolith-app-microservices-ecs-docker-ec2/

[3] https://aws.amazon.com/fr/microservices/

[4] https://docs.aws.amazon.com/whitepapers/latest/microservices-on-aws/microservices-on-aws.html

[5] https://www.youtube.com/watch?v=_ep_yKuDWkE

[6] https://docker-curriculum.com
