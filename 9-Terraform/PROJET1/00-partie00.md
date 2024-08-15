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
