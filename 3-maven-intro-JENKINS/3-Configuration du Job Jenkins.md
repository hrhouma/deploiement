# Intégration avec Jenkins

## Prérequis

- Jenkins installé et configuré.
- Java JDK 1.8 ou supérieur installé sur l'agent Jenkins.
- Maven 3.9 ou supérieur installé sur l'agent Jenkins.
- Accès à un dépôt de code source (par exemple, GitHub) contenant votre projet Maven.

### Configuration du Job Jenkins

1. **Créer un nouveau Job Jenkins :**

   - Ouvrez votre instance Jenkins.
   - Cliquez sur "New Item" pour créer un nouveau job.
   - Donnez un nom à votre job et sélectionnez "Pipeline". Cliquez sur "OK".

2. **Configurer le Contrôle de Source :**

   - Dans la configuration du job, sous "Pipeline", choisissez "Pipeline script from SCM".
   - Sélectionnez "Git" et fournissez l'URL de votre dépôt.
   - Ajoutez les informations d'identification si nécessaire.

3. **Définir le Jenkinsfile :**

   - Ajoutez un fichier nommé `Jenkinsfile` à la racine de votre dépôt Git avec le contenu suivant :

```groovy
pipeline {
    agent any

    tools {
        maven 'Maven 3.6.3'
        jdk 'OpenJDK 11'
    }

    stages {
        stage('Checkout') {
            steps {
                // Récupérer le code source du dépôt
                git branch: 'main', url: 'https://github.com/username/repository.git'
            }
        }

        stage('Compile') {
            steps {
                // Compiler le projet
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                // Exécuter les tests unitaires
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                // Construire le projet
                sh 'mvn package'
            }
        }

        stage('Clean') {
            steps {
                // Nettoyer le projet
                sh 'mvn clean'
            }
        }

        stage('Install') {
            steps {
                // Installer le projet dans le référentiel local Maven
                sh 'mvn install'
            }
        }

        stage('Site') {
            steps {
                // Générer un site pour le projet
                sh 'mvn site'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully.'
        }
        failure {
            echo 'Build failed.'
        }
        always {
            // Nettoyer après la fin du build
            echo 'Cleaning up...'
            sh 'mvn clean'
        }
    }
}
```

### Description des Étapes du Jenkinsfile

- **Checkout** : Récupère le code source du dépôt Git.
- **Compile** : Compile le code source du projet.
- **Test** : Exécute les tests unitaires définis dans le projet.
- **Package** : Construit le projet, incluant les tests, et crée un fichier JAR ou WAR.
- **Clean** : Nettoie le projet en supprimant les fichiers générés lors des builds précédents.
- **Install** : Installe le projet dans le référentiel local Maven.
- **Site** : Génère un site web pour le projet contenant des informations utiles comme la documentation de l'API JavaDoc, les rapports de couverture des tests, etc.

### Lancer le Build

1. **Enregistrer le job Jenkins :**

   - Après avoir configuré les sections ci-dessus, cliquez sur "Save" pour enregistrer votre job.

2. **Exécuter le Build :**

   - Cliquez sur "Build Now" dans le tableau de bord du job pour lancer un build.
   - Vous pouvez surveiller l'exécution du build et voir les étapes en cours dans la console de sortie.

### Résultats du Build

- En cas de succès, vous verrez un message indiquant que le build a été complété avec succès.
- En cas d'échec, vous verrez des messages d'erreur qui vous aideront à diagnostiquer les problèmes.
- Les artefacts construits (par exemple, les fichiers JAR) seront disponibles dans le répertoire `target` de votre projet.

### Conclusion

Ce guide fournit les étapes nécessaires pour configurer et exécuter le cycle de vie Maven de votre projet de calculatrice en utilisant Jenkins et un `Jenkinsfile`. Pour des fonctionnalités avancées et des configurations supplémentaires, consultez la documentation officielle de Jenkins et Maven.
