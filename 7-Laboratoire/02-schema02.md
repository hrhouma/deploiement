Voici un schéma simplifié en ASCII de l'architecture proposée :

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

Ce diagramme illustre les principaux composants de l'architecture, leur interconnexion, et comment les services AWS sont utilisés pour gérer les microservices, le déploiement, et la surveillance.
