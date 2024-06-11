# A - Introduction au processus CI/CD avec un scénario réel

Le CI/CD (Intégration Continue / Déploiement Continu) est un ensemble de pratiques et d'outils utilisés par les équipes de développement pour livrer du code plus rapidement et de manière plus fiable. Il permet d'automatiser et de surveiller toutes les étapes du développement logiciel, de la compilation du code à son déploiement en production.

Pour illustrer ce concept, voici un scénario complet du début à la fin, montrant comment une équipe de développement peut utiliser le CI/CD pour gérer et déployer une application web.

# B - Scénario Réel: Développement d'une Application de Gestion de Tâches

## Contexte

Imaginons une équipe de développement travaillant sur une application web de gestion de tâches appelée "TaskMaster". L'équipe veut s'assurer que chaque modification de code est testée et déployée de manière fluide et rapide.

## Étapes Clés du Processus CI/CD

# 1. Configuration Initiale

- **Dépôt de Code** : L'équipe utilise GitHub pour héberger le code source de l'application.
- **Serveur CI** : Jenkins est configuré pour surveiller le dépôt GitHub et lancer des builds automatisés.
- **Environnements de Déploiement** : Il y a trois environnements : développement, staging, et production.

#  2. Développement et Intégration Continue (CI)

- **Feature Branches** : Les développeurs créent des branches de fonctionnalité pour travailler sur des nouvelles fonctionnalités ou des corrections de bugs.
- **Commit et Push** : Une fois qu'une fonctionnalité est développée, le développeur fait un commit et pousse les changements vers le dépôt GitHub.

##### Exemple:
```bash
git checkout -b feature/add-task
# Développement de la fonctionnalité
git add .
git commit -m "Add feature to create a new task"
git push origin feature/add-task
```

- **Build et Tests Automatisés** : Jenkins détecte le nouveau commit et déclenche un build. Il exécute ensuite une suite de tests automatisés pour s'assurer que les nouvelles modifications n'introduisent pas de régressions.

##### Jenkinsfile:
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
    }
    post {
        success {
            echo 'Build and tests passed.'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}
```

# 3. Revue de Code et Fusion

- **Pull Request (PR)** : Le développeur crée une pull request sur GitHub pour fusionner la branche de fonctionnalité dans la branche principale (`main`).
- **Revue de Code** : Les membres de l'équipe passent en revue le code, laissent des commentaires, et approuvent la PR.

# 4. Déploiement Continu (CD)

- **Fusion et Déploiement en Staging** : Une fois la PR approuvée, elle est fusionnée dans la branche `main`. Jenkins détecte cette fusion, construit l'application, et la déploie automatiquement dans l'environnement de staging pour des tests supplémentaires.

##### Exemple de Script de Déploiement:
```groovy
stage('Deploy to Staging') {
    steps {
        sh 'scp -r build/* user@staging-server:/var/www/taskmaster'
    }
}
```

- **Tests en Staging** : L'équipe QA effectue des tests manuels et automatisés dans l'environnement de staging pour s'assurer que tout fonctionne comme prévu.

# 5. Déploiement en Production

- **Déploiement Automatisé** : Si les tests en staging sont réussis, l'application est déployée en production. Cela peut être déclenché automatiquement ou manuellement après validation.

##### Exemple de Script de Déploiement en Production:
```groovy
stage('Deploy to Production') {
    steps {
        input 'Deploy to production?'
        sh 'scp -r build/* user@production-server:/var/www/taskmaster'
    }
}
```

- **Surveillance** : Une surveillance continue est mise en place pour détecter tout problème en production. Des outils comme Prometheus et Grafana peuvent être utilisés pour surveiller les performances et la santé de l'application.

# 6. Feedback et Amélioration Continue

- **Feedback Loop** : Les développeurs reçoivent des notifications et des rapports sur les performances et les erreurs en production. Ils utilisent ces informations pour améliorer le code et les processus de développement.

## Conclusion

Le processus CI/CD permet à l'équipe de "TaskMaster" de livrer du code de haute qualité rapidement et de manière fiable. Chaque modification est testée et déployée automatiquement, réduisant ainsi les risques de bugs en production et améliorant la collaboration entre les membres de l'équipe.

En adoptant ces pratiques, l'équipe peut se concentrer sur l'innovation et la création de nouvelles fonctionnalités, tout en assurant une expérience utilisateur stable et performante.
