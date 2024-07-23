**Bonjour à tous,**

Aujourd'hui, nous allons plonger dans un laboratoire pratique qui nous permettra de maîtriser les concepts de microservices et de Docker, tout en utilisant AWS comme plateforme principale. Ce laboratoire s'intègre de manière approfondie dans le cadre de notre cours de déploiement au sein du programme Big Data. Il s'agit d'une occasion exceptionnelle pour vous de mettre en pratique les compétences théoriques que nous avons couvertes en classe, en vous offrant une application concrète des concepts de conteneurisation, de déploiement de microservices et de gestion d'infrastructures cloud.

**Objectif du laboratoire :**

L'objectif principal de ce laboratoire est de vous familiariser avec la création de microservices et la mise en place d'un pipeline CI/CD en utilisant AWS. Au cours de ce laboratoire, vous serez mis au défi d'utiliser au moins 11 services AWS pour développer une solution complète de microservices et d'intégration continue/déploiement continu.

**Contexte du projet :**

Imaginez que vous travaillez pour une entreprise qui possède plusieurs franchises de cafés et qui a récemment acquis un fournisseur de grains de café. Le fournisseur utilise une application monolithique pour gérer les listes de fournisseurs de café. Cette application a des problèmes de fiabilité et de performance. Votre mission est de diviser cette application en microservices, afin d'améliorer la scalabilité et la résilience, et de mettre en place un pipeline CI/CD pour automatiser les déploiements.

**Résultats attendus :**

À la fin de ce laboratoire, vous devriez être capables de :

1. **Comprendre et déployer une application web Node.js** : Vous apprendrez comment coder et déployer une application Node.js qui se connecte à une base de données relationnelle. Cependant, rappelez-vous que Node.js n'est qu'un outil parmi d'autres que vous utiliserez pour atteindre les objectifs du laboratoire. L'objectif n'est pas de devenir des développeurs Node.js, mais de comprendre comment une application peut être déployée dans une architecture distribuée.

2. **Créer un environnement de développement intégré (IDE) sur AWS Cloud9** : Vous configurerez un environnement de développement et un référentiel de code pour stocker le code source de votre application.

3. **Diviser une application monolithique en microservices conteneurisés** : Vous transformerez une application monolithique en microservices indépendants et conteneurisés, ce qui permettra une meilleure scalabilité et résilience.

4. **Utiliser un registre de conteneurs (Amazon ECR)** : Vous apprendrez à stocker et gérer les versions des images Docker de vos microservices.

5. **Créer et gérer un cluster serverless (Amazon ECS)** : Vous configurerez un cluster ECS qui supportera vos microservices, tout en optimisant les coûts et la scalabilité.

6. **Configurer un Application Load Balancer** : Vous configurerez des groupes cibles et un équilibreur de charge pour diriger le trafic web de manière efficace entre vos microservices.

7. **Mettre en place un pipeline CI/CD avec AWS CodePipeline** : Vous créerez un pipeline de déploiement automatisé pour vos microservices, permettant des mises à jour continues et fiables de votre application.

**L'importance pour l'architecture Big Data :**

Ce laboratoire est particulièrement pertinent pour ceux d'entre vous qui se dirigent vers des carrières dans le Big Data. Les microservices et les architectures distribuées sont des piliers essentiels de la gestion des grandes quantités de données. En décomposant une application en microservices, vous apprenez à construire des systèmes qui peuvent évoluer horizontalement pour gérer des volumes massifs de données.

1. **Architecture distribuée** : Les microservices permettent de répartir les tâches sur plusieurs nœuds, ce qui est crucial pour traiter de grandes quantités de données. Vous comprendrez comment concevoir et déployer des architectures distribuées capables de traiter des volumes de données importants de manière efficace.

2. **Scalabilité et résilience** : Les systèmes de Big Data doivent être capables de s'adapter aux fluctuations de la charge de travail. Grâce aux microservices et à l'automatisation des déploiements, vous apprendrez à créer des systèmes qui peuvent évoluer facilement pour répondre à la demande.

3. **Intégration continue et déploiement continu (CI/CD)** : Dans un environnement Big Data, il est essentiel de pouvoir déployer rapidement et en toute sécurité des modifications et des mises à jour. Vous apprendrez à mettre en place des pipelines CI/CD qui assurent que les nouvelles fonctionnalités et les corrections de bugs sont déployées sans interruption des services.

**Phases du laboratoire :**

Le laboratoire est structuré en neuf phases principales, allant de la planification et de l'estimation des coûts, jusqu'à l'ajustement et la mise à l'échelle de vos microservices. Vous allez :

1. **Planifier la conception et estimer les coûts** : Créer un diagramme d'architecture et une estimation des coûts pour votre solution.
   - **Tâche 1.1 :** Créer un diagramme d'architecture détaillé en utilisant des outils comme AWS Architecture Icons pour illustrer les services AWS utilisés.
   - **Tâche 1.2 :** Utiliser l'outil de calcul des prix AWS pour estimer les coûts de fonctionnement de la solution sur une période de 12 mois, en tenant compte de la tarification des différents services AWS.

2. **Analyser l'infrastructure de l'application monolithique** : Vérifier et tester l'application existante avant de la transformer en microservices.
   - **Tâche 2.1 :** Vérifier l'accessibilité de l'application monolithique et observer son fonctionnement actuel.
   - **Tâche 2.2 :** Tester l'application web en ajoutant, modifiant et supprimant des fournisseurs pour comprendre les fonctionnalités existantes.
   - **Tâche 2.3 :** Analyser l'architecture logicielle et l'infrastructure de l'application monolithique.

3. **Créer un environnement de développement** : Configurer un IDE Cloud9 et copier le code source dans un référentiel Git.
   - **Tâche 3.1 :** Créer un environnement de développement Cloud9 et configurer les outils nécessaires.
   - **Tâche 3.2 :** Copier le code source de l'application monolithique dans l'IDE Cloud9.
   - **Tâche 3.3 :** Organiser le code en répertoires distincts pour les deux microservices.
   - **Tâche 3.4 :** Créer un référentiel Git dans CodeCommit et y pousser le code source.

4. **Configurer et tester les microservices dans Docker** : Modifier le code source et créer des conteneurs Docker pour vos microservices.
   - **Tâche 4.1 :** Ajuster les paramètres de sécurité pour permettre les tests de conteneurs Docker.
   - **Tâche 4.2 :** Modifier le code source pour le microservice client en supprimant les fonctionnalités de modification.
   - **Tâche 4.3 :** Créer un Dockerfile pour le microservice client et lancer un conteneur de test.
   - **Tâche 4.4 :** Modifier le code source pour le microservice employé et ajouter les fonctionnalités de modification et de suppression.
   - **Tâche 4.5 :** Créer un Dockerfile pour le microservice employé et lancer un conteneur de test.
   - **Tâche 4.6 :** Ajuster le port du microservice employé et recréer l'image Docker.
   - **Tâche 4.7 :** Enregistrer le code dans CodeCommit.

5. **Créer des référentiels ECR et un cluster ECS** : Stocker vos images Docker et configurer un cluster ECS.
   - **Tâche 5.1 :** Créer des référentiels ECR pour stocker les images Docker.
   - **Tâche 5.2 :** Créer un cluster ECS sans serveur pour exécuter les microservices.
   - **Tâche 5.3 :** Créer un référentiel CodeCommit pour les fichiers de déploiement.
   - **Tâche 5.4 :** Créer des fichiers de définition de tâches ECS et les enregistrer.
   - **Tâche 5.5 :** Créer des fichiers AppSpec pour CodeDeploy.
   - **Tâche 5.6 :** Pousser les fichiers de définition de tâches et AppSpec dans CodeCommit.

6. **Configurer un Application Load Balancer** : Mettre en place un équilibreur de charge pour diriger le trafic.
   - **Tâche 6.1 :** Créer des groupes cibles pour les microservices.
   - **Tâche 6.2 :** Créer un Application Load Balancer et configurer les règles de routage.

7. **Créer des services ECS** : Déployer vos microservices sur ECS.
   - **Tâche 7.1 :** Créer un service ECS pour le microservice client.
   - **Tâche 7.2 :** Créer un service ECS pour le microservice employé.

8. **Configurer CodeDeploy et CodePipeline** : Mettre en place des pipelines CI/CD pour vos microservices.
   - **Tâche 8.1 :** Créer une application CodeDeploy et des groupes de déploiement pour les microservices.
   - **Tâche 8.2 :** Créer un pipeline CI/CD pour le microservice client.
   - **Tâche 8.3 :** Tester le pipeline CI/CD pour le microservice client.
   - **Tâche 8.4 :** Créer un pipeline CI/CD pour le microservice employé.
   - **Tâche 8.5 :** Tester le pipeline CI/CD pour le microservice employé.
   - **Tâche 8.6 :** Observer comment CodeDeploy modifie les règles de l'écouteur de l'équilibreur de charge.

9. **Ajuster et mettre à l'échelle les microservices** : Optimiser et adapter vos microservices.
   - **Tâche 9.1 :** Limiter l'accès au microservice employé.
   - **Tâche 9.2 :** Ajuster l'interface utilisateur du microservice employé et pousser l'image mise à jour.
   - **Tâche 9.3 :** Vérifier l'exécution du pipeline et la mise à jour du microservice.
   - **Tâche 9.4 :** Tester l'accès au microservice employé.
   - **Tâche 9.5 :** Mettre à l'échelle le microservice client.

Préparez-vous à une session intense et enrichissante. Bonne chance à tous, et n'hésitez pas à poser des questions à tout moment. Let's get started!


