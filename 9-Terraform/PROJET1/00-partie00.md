
---
# Prérequis partie 01 - installation de Terraform
---

### 1. **Téléchargement de Terraform**
   - Rendez-vous sur la [page des téléchargements Terraform](https://www.terraform.io/downloads).
   - Sous la section **Windows**, cliquez sur le lien de téléchargement pour la version appropriée (généralement la version 64 bits).

### 2. **Extraction du fichier ZIP**
   - Une fois le fichier téléchargé (`terraform_<version>_windows_amd64.zip`), extrayez le contenu dans un répertoire de votre choix en utilisant un outil comme WinRAR ou 7-Zip.

### 3. **Déplacement de l'exécutable Terraform**
   - Après l'extraction, vous obtiendrez un fichier exécutable `terraform.exe`.
   - Déplacez ce fichier dans un répertoire de votre choix où vous souhaitez que Terraform soit installé, par exemple : `C:\Program Files\Terraform\`.

### 4. **Ajouter Terraform au PATH**
   - Pour utiliser Terraform depuis n'importe quel emplacement dans votre terminal, vous devez ajouter son chemin au `PATH`.
   - **Étapes** :
     1. Cliquez avec le bouton droit sur l'icône **Ce PC** ou **Ordinateur** sur votre bureau ou dans l'explorateur de fichiers et choisissez **Propriétés**.
     2. Cliquez sur **Paramètres système avancés** sur la gauche.
     3. Cliquez sur le bouton **Variables d'environnement...** en bas de la fenêtre.
     4. Dans la section **Variables système**, trouvez la variable nommée **Path** et sélectionnez-la, puis cliquez sur **Modifier...**.
     5. Dans la fenêtre qui s'ouvre, cliquez sur **Nouveau** et ajoutez le chemin du dossier où vous avez déplacé `terraform.exe` (par exemple `C:\Program Files\Terraform\`).
     6. Cliquez sur **OK** pour fermer toutes les fenêtres.

### 5. **Vérifier l'installation**
   - Ouvrez **l'Invite de commandes** (ou PowerShell) et tapez la commande suivante :
     ```sh
     terraform --version
     ```
   - Vous devriez voir la version de Terraform installée s'afficher, ce qui confirme que l'installation a été réussie.

### 6. **Configurer Terraform**
   - Avant d'utiliser Terraform, assurez-vous que vous avez les permissions nécessaires pour exécuter des commandes sur votre système.
   - Créez un nouveau répertoire pour vos projets Terraform et commencez à écrire vos fichiers `.tf`.

---
# Prérequis partie 02 - accorder à l'utilisateur IAM les permissions nécessaires pour gérer les ressources
---

Pour utiliser Terraform avec AWS, vous devez accorder à l'utilisateur IAM les permissions nécessaires pour gérer les ressources que vous prévoyez de créer, modifier ou supprimer. Voici une liste des politiques gérées par AWS que vous pouvez attacher à l'utilisateur IAM pour couvrir les cas d'utilisation les plus courants. Vous devez ajuster ces permissions en fonction des services AWS que vous prévoyez d'utiliser.

### 1. **Permissions Générales**
   - **AdministratorAccess** : Donne un accès complet à tous les services et ressources AWS. Utilisez cette politique si vous souhaitez que l'utilisateur ait un accès total, mais soyez prudent car cela donne également des droits d'accès très élevés.
   
   Cependant, si vous souhaitez accorder des permissions plus spécifiques, vous pouvez attacher les politiques suivantes en fonction des services que vous utilisez :

### 2. **Permissions pour EC2**
   - **AmazonEC2FullAccess** : Donne un accès complet aux services EC2, y compris la gestion des instances, des volumes EBS, des groupes de sécurité, etc.

### 3. **Permissions pour S3**
   - **AmazonS3FullAccess** : Donne un accès complet à tous les buckets et objets S3.

### 4. **Permissions pour RDS**
   - **AmazonRDSFullAccess** : Donne un accès complet à tous les services RDS, y compris la gestion des bases de données, des groupes de sécurité RDS, etc.

### 5. **Permissions pour IAM**
   - **IAMFullAccess** : Donne un accès complet à la gestion des utilisateurs, des groupes, des rôles et des politiques IAM.

### 6. **Permissions pour Lambda**
   - **AWSLambda_FullAccess** : Donne un accès complet à la gestion des fonctions Lambda, y compris leur création, modification et suppression.

### 7. **Permissions pour CloudWatch**
   - **CloudWatchFullAccess** : Donne un accès complet à la gestion des journaux, des tableaux de bord, des alarmes et des événements dans Amazon CloudWatch.

### 8. **Permissions pour Autoscaling**
   - **AutoScalingFullAccess** : Donne un accès complet à la gestion des groupes d'auto-scaling.

### 9. **Permissions pour VPC**
   - **AmazonVPCFullAccess** : Donne un accès complet à la gestion des réseaux VPC, des sous-réseaux, des passerelles, des routes, etc.

### 10. **Permissions pour SNS**
   - **AmazonSNSFullAccess** : Donne un accès complet à la gestion des topics et des abonnements SNS.

### **Exemple d'Utilisation**
Si vous prévoyez d'utiliser Terraform pour gérer EC2, S3, RDS, et Lambda, vous pouvez accorder les permissions suivantes à votre utilisateur IAM :
- **AmazonEC2FullAccess**
- **AmazonS3FullAccess**
- **AmazonRDSFullAccess**
- **AWSLambda_FullAccess**
- **IAMFullAccess** (si vous devez gérer des rôles pour Lambda)

### **Comment Attacher Ces Politiques**
1. Allez dans la console AWS et connectez-vous avec un compte ayant des privilèges d'administrateur.
2. Naviguez vers le service IAM.
3. Cliquez sur **Users** dans le panneau de gauche, puis sélectionnez l'utilisateur auquel vous souhaitez attacher les politiques.
4. Cliquez sur l'onglet **Permissions**.
5. Cliquez sur le bouton **Add permissions**.
6. Sélectionnez **Attach policies directly**.
7. Recherchez les politiques ci-dessus et cochez les cases correspondantes.
8. Cliquez sur **Next: Review**, puis sur **Add permissions**.

### **Remarque**
Il est recommandé de toujours suivre le principe du moindre privilège, c'est-à-dire de ne donner que les permissions strictement nécessaires pour exécuter les tâches prévues. Si vous n'êtes pas certain des permissions spécifiques dont vous avez besoin, commencez avec des politiques plus restrictives et ajoutez des permissions au fur et à mesure que vous rencontrez des limitations.
