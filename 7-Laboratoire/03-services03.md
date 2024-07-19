

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


```
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

