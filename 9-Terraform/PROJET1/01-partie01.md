---
# 01 - Structure du projet
---

```
CORRECTION 1/
├── lambda_package/
│   ├── lambda_function.py
│   ├── log.py
│   └── webpage.py
├── autoscaling.tf
├── lambda_function.zip
├── log_sync_function.zip
├── main.tf
├── rds.tf
├── Readme
├── s3.tf
├── snapshot.tf
└── webpage_sync_function.zip
```


---
# 02 - Présentation du Projet
---

   - **But** : Ce projet déploie une application web avec une instance EC2 qui s'autoscale, une base de données RDS, et des fonctions Lambda pour gérer des tâches automatisées comme la création de snapshots et la synchronisation des logs.
   - **Composants** :
     - **Scripts Terraform** : Définissent l'infrastructure pour EC2, RDS, S3, Lambda, et l'autoscaling.
     - **Fonctions Lambda** : Automatisent la création de snapshots, la synchronisation des logs et des pages web.
     - **Buckets S3** : Stockent les logs et le contenu des pages web.
     - **Base de données RDS** : Base de données MySQL pour stocker les données de l'application.


---
# 03 - Architecture
---


```
          +-------------+
          |   Client    |
          +-------------+
                |
         +-----------------+
         | Load Balancer    |
         +-----------------+
                |
     +---------------------+
     | AutoScaling Group    |
     |   +-------------+    |
     |   | EC2 Instance |----|-----> S3 (Webpage)
     |   +-------------+    |
     +---------------------+
           |
       +-------+
       |  RDS  |<---> Lambda (Snapshot)
       +-------+
                |
            S3 (Logs)
```

---
# 04 - Étapes de Déploiement
---

   1. **Pré-requis** :
      - **Installer Terraform** : Vous pouvez installer Terraform en suivant les étapes ci-dessous :
        ```sh
        # Télécharger Terraform
        wget https://releases.hashicorp.com/terraform/1.3.0/terraform_1.3.0_linux_amd64.zip
        # Dézipper le fichier
        unzip terraform_1.3.0_linux_amd64.zip
        # Déplacer l'exécutable dans un répertoire du PATH
        sudo mv terraform /usr/local/bin/
        # Vérifier l'installation
        terraform --version
        ```

   2. **Configurer les Scripts Terraform** :
      - **Remplacer les champs** :
        - **AMI ID** : `ami-06b09bfacae1453cb`
        - **Nom du Key Pair** : `newtest`
        - **ID du Subnet** : `subnet-036ca4dafa83cd9c5`
        - **ID du VPC** : `vpc-09a2de34b89c213f3`

        Ces informations doivent être remplacées dans les fichiers `autoscaling.tf`, `main.tf`, `rds.tf`, et `s3.tf`.

      - **Comment obtenir ces informations** :
        - **AMI ID** : Vous pouvez obtenir l'ID de l'image AMI en utilisant la console AWS ou la commande suivante :
          ```sh
          aws ec2 describe-images --owners amazon --filters "Name=name,Values=amzn-ami-hvm-*" --query 'Images[*].[ImageId,Name]' --output text
          ```
        - **Nom du Key Pair** : Si vous n'avez pas encore un Key Pair, vous pouvez en créer un avec la commande suivante :
          ```sh
          aws ec2 create-key-pair --key-name newtest --query 'KeyMaterial' --output text > newtest.pem
          ```
        - **ID du Subnet** et **ID du VPC** : Vous pouvez obtenir ces IDs en utilisant la console AWS ou en exécutant :
          ```sh
          aws ec2 describe-subnets --query 'Subnets[*].{ID:SubnetId, VPC:VpcId}' --output table
          ```

   3. **Déployer l'infrastructure** :
      - **Initialiser Terraform** :
        ```sh
        terraform init
        ```
      - **Planifier le déploiement** :
        ```sh
        terraform plan
        ```
      - **Appliquer le plan** :
        ```sh
        terraform apply
        ```

   4. **Vérifier le Déploiement** :
      - **Vérifier les ressources** : Connectez-vous à la console AWS pour vérifier que les instances EC2, RDS, et les buckets S3 sont bien créés.
      - **Tester les Fonctions Lambda** : Assurez-vous que les fonctions Lambda sont déclenchées correctement par les règles CloudWatch.


---
# 05 - Détails des Fichiers
---

   - **lambda_function.py** :
     - **But** : Crée un snapshot d'un volume EBS spécifié.
     - **Instructions** :
       - Remplacez `your_volume_id` par l'ID réel du volume EBS.
   
   - **log.py** :
     - **But** : Synchronise les logs entre deux buckets S3.
     - **Instructions** :
       - Remplacez `php-log-bucket-name` et `php-webpage-bucket-name` par les noms réels des buckets S3.

   - **webpage.py** :
     - **But** : Synchronise le contenu des pages web entre deux buckets S3.
     - **Instructions** :
       - Remplacez `php-webpage-bucket-name` et `php-log-bucket-name` par les noms réels des buckets S3.

---
# 06 - Fichiers ZIP
---

   - **lambda_function.zip** : Contient le code Python pour la création des snapshots (`lambda_function.py`).
   - **log_sync_function.zip** : Contient le code Python pour la synchronisation des logs entre les buckets S3 (`log.py`).
   - **webpage_sync_function.zip** : Contient le code Python pour la synchronisation des pages web entre les buckets S3 (`webpage.py`).

---
# 06 - Conclusion
---

   - **Exécution** : Vous avez maintenant toutes les informations pour déployer ce projet. Suivez les étapes une par une, remplacez les valeurs par celles de votre environnement, et utilisez Terraform pour déployer l'infrastructure. Une fois déployé, surveillez vos ressources dans AWS pour vérifier leur bon fonctionnement.
