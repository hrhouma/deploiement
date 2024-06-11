# C'est quoi un Jenkinfile ?


## Guide Complet pour Débutants : Comment Écrire un Jenkinsfile

### Introduction
Un Jenkinsfile est un fichier texte qui contient la définition d'un pipeline Jenkins. Il utilise un langage spécifique au domaine (DSL) basé sur la syntaxe Groovy pour décrire les différentes étapes et actions du processus de build. Les Jenkinsfiles sont essentiels pour implémenter des pipelines d'intégration continue (CI) et de livraison continue (CD) de manière cohérente et versionnée.

### Création d'un Jenkinsfile
Pour créer un Jenkinsfile, suivez ces étapes :

1. **Créer un Jenkinsfile** : Commencez par créer un nouveau fichier nommé `Jenkinsfile` à la racine de votre dépôt de projet. Ce fichier ne doit pas avoir d'extension.

2. **Choisir la Syntaxe du Pipeline** : Jenkins supporte deux types de syntaxe de pipeline :
   - **Syntaxe Déclarative** : Un format structuré et lisible par les humains.
   - **Syntaxe Scriptée** : Un format plus flexible mais moins lisible pour les pipelines complexes.

### Syntaxe Déclarative
La syntaxe déclarative est recommandée pour la plupart des utilisateurs en raison de sa simplicité et de sa lisibilité. Voici un exemple :

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Ajoutez les étapes de build ici
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                // Ajoutez les étapes de test ici
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Ajoutez les étapes de déploiement ici
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Ajoutez les actions post-build ici
        }
    }
}
```

### Syntaxe Scriptée
La syntaxe scriptée offre plus de flexibilité mais peut être moins lisible pour les pipelines complexes. Voici un exemple de syntaxe scriptée :

```groovy
node {
    stage('Build') {
        echo 'Building...'
        // Ajoutez les étapes de build ici
    }

    stage('Test') {
        echo 'Testing...'
        // Ajoutez les étapes de test ici
    }

    stage('Deploy') {
        echo 'Deploying...'
        // Ajoutez les étapes de déploiement ici
    }

    post {
        always {
            echo 'Cleaning up...'
            // Ajoutez les actions post-build ici
        }
    }
}
```

### Configuration des Agents
Dans le bloc `agent` (pour la syntaxe déclarative) ou en utilisant `node` (pour la syntaxe scriptée), spécifiez où le build doit s'exécuter. Vous pouvez utiliser un nœud spécifique ou une image de conteneur.

### Actions Post-Build
Dans le bloc `post`, vous pouvez définir les actions post-build, telles que l'envoi de notifications, l'archivage des artefacts ou le déclenchement d'autres jobs Jenkins en fonction du résultat du build.

### Sauvegarder et Commiter
Sauvegardez le Jenkinsfile et commitez-le dans votre système de contrôle de version (par exemple, Git). Jenkins détectera et exécutera automatiquement le pipeline lorsque des modifications seront poussées dans le dépôt.

### Configuration du Job Jenkins
Sur votre serveur Jenkins, créez un nouveau job de pipeline, spécifiez l'emplacement du Jenkinsfile dans votre dépôt et configurez les paramètres ou déclencheurs nécessaires.

### Exécuter le Pipeline
Déclenchez le pipeline manuellement ou en fonction de vos déclencheurs configurés (par exemple, les modifications de code, les horaires).

### Suivi et Débogage
Utilisez l'interface web de Jenkins pour surveiller l'exécution du pipeline, consulter les logs et déboguer les éventuels problèmes.

### Conclusion
Un Jenkinsfile bien structuré permet de définir et d'automatiser efficacement les processus de build, de test et de déploiement. En utilisant soit la syntaxe déclarative soit la syntaxe scriptée, vous pouvez adapter le Jenkinsfile à vos besoins spécifiques et garantir une livraison continue de haute qualité pour vos projets.

# Référence : https://dev.to/msfaizi/how-to-write-jenkinsfile-a-comprehensive-guide-for-beginners-58d2
