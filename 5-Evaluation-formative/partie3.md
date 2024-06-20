### Partie 3: Ajouter le Projet à Git et Configurer une Pipeline Jenkins

Dans cette partie, nous allons apprendre à ajouter notre projet à Git et à configurer une pipeline Jenkins pour vérifier les modifications et effectuer des builds automatiquement toutes les 5 minutes.

### Étape 1: Ajouter le Projet à Git

1. **Initialiser un dépôt Git dans le dossier de votre projet :**

   ```sh
   cd /path/to/your/project
   git init
   ```

2. **Ajouter tous les fichiers au dépôt :**

   ```sh
   git add .
   ```

3. **Valider les modifications :**

   ```sh
   git commit -m "Initial commit"
   ```

4. **Ajouter un dépôt distant (par exemple, sur GitHub) :**

   ```sh
   git remote add origin https://github.com/yourusername/yourrepository.git
   ```

5. **Pousser les modifications vers le dépôt distant :**

   ```sh
   git push -u origin master
   ```

### Étape 2: Configurer Jenkins

1. **Installer Jenkins :**

   Si Jenkins n'est pas encore installé, suivez les instructions officielles pour l'installer sur votre système : [Documentation Jenkins](https://www.jenkins.io/doc/book/installing/).

2. **Configurer Jenkins pour Git :**

   - Accédez à Jenkins : `http://your-jenkins-url:8080/`
   - Allez dans `Manage Jenkins` > `Manage Plugins`
   - Installez les plugins nécessaires pour Git (`Git plugin`) et Docker (`Docker plugin`).

### Étape 3: Créer un Fichier Jenkinsfile

Créez un fichier nommé `Jenkinsfile` à la racine de votre projet. Ce fichier définira votre pipeline Jenkins.

#### Jenkinsfile

```groovy
pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *') // Vérifie les modifications toutes les 5 minutes
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master', url: 'https://github.com/yourusername/yourrepository.git'
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    docker.build('yourimage:latest')
                }
            }
        }
        stage('Run Containers') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
```

### Étape 4: Configurer la Pipeline dans Jenkins

1. **Créer un nouveau projet dans Jenkins :**

   - Allez dans `New Item`, donnez un nom à votre projet et sélectionnez `Pipeline`.
   - Cliquez sur `OK`.

2. **Configurer la pipeline :**

   - Sous la section `Pipeline`, sélectionnez `Pipeline script from SCM`.
   - Choisissez `Git` et entrez l'URL de votre dépôt Git : `https://github.com/yourusername/yourrepository.git`.
   - Assurez-vous que la branche est `master`.
   - Spécifiez le chemin du script : `Jenkinsfile`.

3. **Sauvegarder et lancer la pipeline :**

   - Cliquez sur `Save`.
   - Allez dans `Build Now` pour démarrer la première exécution de la pipeline.

### Étape 5: Vérifier les Builds

1. **Accédez à votre tableau de bord Jenkins :**

   - Vous devriez voir les exécutions de votre pipeline toutes les 5 minutes.
   - Cliquez sur une exécution pour voir les logs et vérifier que tout fonctionne correctement.

2. **Vérifiez que les conteneurs Docker sont en cours d'exécution :**

   ```sh
   docker ps
   ```

   Vous devriez voir les conteneurs en cours d'exécution pour votre application Flask, PostgreSQL et Redis.

### Exemple Complet

Voici un récapitulatif des commandes et étapes :

```sh
# Étape 1: Initialiser le dépôt Git
cd /path/to/your/project
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/yourusername/yourrepository.git
git push -u origin master

# Étape 2: Installer Jenkins et les plugins nécessaires

# Étape 3: Créer le fichier Jenkinsfile
echo 'pipeline {
    agent any
    triggers {
        pollSCM("H/5 * * * *") // Vérifie les modifications toutes les 5 minutes
    }
    stages {
        stage("Clone Repository") {
            steps {
                git branch: "master", url: "https://github.com/yourusername/yourrepository.git"
            }
        }
        stage("Build Docker Images") {
            steps {
                script {
                    docker.build("yourimage:latest")
                }
            }
        }
        stage("Run Containers") {
            steps {
                sh "docker-compose up -d"
            }
        }
    }
}' > Jenkinsfile

# Étape 4: Configurer la pipeline dans Jenkins via l'interface web

# Étape 5: Vérifier les builds via l'interface web et avec Docker
docker ps
```

### Conclusion

En suivant ce tutoriel, vous avez appris à ajouter votre projet à Git et à configurer une pipeline Jenkins pour vérifier les modifications et effectuer des builds automatiquement toutes les 5 minutes. Vous pouvez désormais automatiser le déploiement de votre application Flask avec PostgreSQL et Redis.
