**Bonjour à tous,**

Aujourd'hui, nous allons nous plonger dans un laboratoire pratique passionnant qui va vous permettre de maîtriser les concepts de microservices et de Docker, tout en utilisant AWS comme plateforme principale. Ce laboratoire s'inscrit parfaitement dans le cadre de notre cours de déploiement au sein du programme Big Data.

**Objectif du laboratoire :**

L'objectif principal de ce laboratoire est de vous familiariser avec la création de microservices et la mise en place d'un pipeline CI/CD en utilisant AWS. Vous serez amenés à utiliser au moins 11 services AWS pour développer une solution complète de microservices et d'intégration continue/déploiement continu.

**Contexte du projet :**

Imaginez que vous travaillez pour une entreprise qui possède plusieurs franchises de cafés et qui a récemment acquis un fournisseur de grains de café. Le fournisseur utilise une application monolithique pour gérer les listes de fournisseurs de café, mais cette application présente des problèmes de fiabilité et de performance. Votre mission est de diviser cette application en microservices pour améliorer sa scalabilité et sa résilience, et de mettre en place un pipeline CI/CD pour automatiser les déploiements.

**Résultats attendus :**

À la fin de ce laboratoire, vous devriez être capables de :

1. Comprendre et déployer une application web Node.js
2. Créer un environnement de développement intégré (IDE) sur AWS Cloud9
3. Diviser une application monolithique en microservices conteneurisés
4. Utiliser un registre de conteneurs (Amazon ECR)
5. Créer et gérer un cluster serverless (Amazon ECS)
6. Configurer un Application Load Balancer
7. Mettre en place un pipeline CI/CD avec AWS CodePipeline

**L'importance pour l'architecture Big Data :**

Ce laboratoire est particulièrement pertinent pour vos futures carrières dans le Big Data :

1. **Architecture distribuée** : Vous apprendrez à concevoir des systèmes capables de traiter efficacement de grands volumes de données.
2. **Scalabilité et résilience** : Vous créerez des systèmes pouvant s'adapter facilement aux fluctuations de la charge de travail.
3. **Intégration continue et déploiement continu (CI/CD)** : Vous mettrez en place des pipelines assurant des déploiements rapides et sûrs.

**Phases du laboratoire :**

Le laboratoire est structuré en neuf phases principales :

1. **Planifier la conception et estimer les coûts**
   - Créer un diagramme d'architecture détaillé
   - Estimer les coûts de fonctionnement sur 12 mois

2. **Analyser l'infrastructure de l'application monolithique**
   - Vérifier l'accessibilité de l'application existante
   - Tester les fonctionnalités de l'application web
   - Analyser l'architecture logicielle et l'infrastructure

3. **Créer un environnement de développement**
   - Configurer un IDE Cloud9
   - Copier et organiser le code source
   - Créer un référentiel Git dans CodeCommit

4. **Configurer et tester les microservices dans Docker**
   - Ajuster les paramètres de sécurité
   - Modifier le code source pour les microservices client et employé
   - Créer des Dockerfiles et lancer des conteneurs de test

5. **Créer des référentiels ECR et un cluster ECS**
   - Créer des référentiels ECR pour stocker les images Docker
   - Configurer un cluster ECS serverless
   - Créer et enregistrer des fichiers de définition de tâches ECS et AppSpec

6. **Configurer un Application Load Balancer**
   - Créer des groupes cibles pour les microservices
   - Configurer un équilibreur de charge et les règles de routage

7. **Créer des services ECS**
   - Déployer les microservices client et employé sur ECS

8. **Configurer CodeDeploy et CodePipeline**
   - Créer une application CodeDeploy et des groupes de déploiement
   - Mettre en place et tester des pipelines CI/CD pour les microservices

9. **Ajuster et mettre à l'échelle les microservices**
   - Optimiser l'accès et l'interface utilisateur des microservices
   - Tester la mise à l'échelle des microservices

# Schéma de l'architecture proposée :

```
+--------------------+                  +--------------------+
|    Utilisateurs    |                  |    Utilisateurs    |
|  (Clients & Employés)                 |      (Clients)     |
+--------------------+                  +--------------------+
            |                                 |
            |                                 |
            |                                 |
        +------------------------------------------+
        |      Application Load Balancer (ALB)     |
        +------------------------------------------+
               |                       |
               |                       |
+------------------------+    +------------------------+
|    Employee Service    |    |    Customer Service    |
|    (ECS Fargate)       |    |    (ECS Fargate)       |
+------------------------+    +------------------------+
            |                                 |
            |                                 |
+------------------------+    +------------------------+
|    Docker Containers   |    |    Docker Containers   |
+------------------------+    +------------------------+
            |                                 |
            |                                 |
+------------------------+    +------------------------+
|         ECR            |    |         ECR            |
| (Elastic Container     |    | (Elastic Container     |
|     Registry)          |    |     Registry)          |
+------------------------+    +------------------------+
            |                                 |
            |                                 |
+------------------------+    +------------------------+
|       CodeCommit       |    |       CodeCommit       |
+------------------------+    +------------------------+
            |                                 |
            |                                 |
+------------------------+    +------------------------+
|       CodePipeline     |    |       CodePipeline     |
+------------------------+    +------------------------+
            |                                 |
            |                                 |
+------------------------+    +------------------------+
|       CodeDeploy       |    |       CodeDeploy       |
+------------------------+    +------------------------+
            |                                 |
            |                                 |
+------------------------+    +------------------------+
|          RDS           |    |          RDS           |
| (Relational Database   |    | (Relational Database   |
|       Service)         |    |       Service)         |
+------------------------+    +------------------------+
            |                                 |
            |                                 |
+------------------------+    +------------------------+
|       CloudWatch       |    |       CloudWatch       |
|    (Monitoring &       |    |    (Monitoring &       |
|     Logging)           |    |     Logging)           |
+------------------------+    +------------------------+
```

Voici un tableau détaillant chaque service AWS utilisé dans le projet, son rôle, et ce qu'il fait :

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

### Explication des rôles

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


# services AWS utilisé dans le projet, et leurs rôles : 

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




**Conclusion :**

Ce laboratoire vous offre une opportunité unique de mettre en pratique des concepts essentiels pour le Big Data et le déploiement d'applications à grande échelle. Vous allez acquérir des compétences précieuses en matière de conteneurisation, de microservices et d'automatisation des déploiements, qui sont cruciales dans l'industrie actuelle.

Préparez-vous à une session intense et enrichissante. N'hésitez pas à poser des questions à tout moment durant le laboratoire. Bonne chance à tous, et que l'aventure commence !

