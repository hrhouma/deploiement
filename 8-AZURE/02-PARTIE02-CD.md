# 📘 Tutoriel Complet : Création d’Applications Web Azure pour Développement, Qualité et Production

Ce tutoriel vous guidera à travers toutes les étapes nécessaires pour créer des applications Web sur Azure, destinées aux environnements de Développement, Qualité, et Production. Nous couvrirons les étapes de configuration, de création, de déploiement et de vérification des applications Web.

---

## 🟢 Partie 1 : Introduction au Workflow CI/CD avec Azure DevOps

### 1️⃣ Présentation Générale du Workflow CI/CD

Un flux de travail typique de CI/CD (Intégration Continue et Déploiement Continu) utilisant **Azure DevOps** est conçu pour automatiser le processus de construction, de test, et de déploiement d'applications dans différents environnements (Dev, QA, Prod). Voici les éléments principaux du flux de travail :

- **Développeur** : Le processus commence avec un développeur qui effectue des modifications sur le code source à l'aide de **Visual Studio** ou **Visual Studio Code**.
  
- **Azure Repos (Git)** : Le code est ensuite poussé vers un dépôt Git hébergé sur **Azure Repos**, qui agit comme le gestionnaire de version centralisé où tout le code de l'application est stocké.
  
- **Azure Build Pipeline (CI)** : Une fois le code poussé, une pipeline de construction CI est déclenchée automatiquement, comprenant plusieurs étapes :
  - Récupération du code source depuis le dépôt.
  - Installation des outils nécessaires pour la construction.
  - Construction de la solution, incluant la compilation du code.
  - Exécution des tests pour vérifier que les modifications n'ont pas introduit de bugs.
  - Emballage des artefacts (fichiers exécutables, bibliothèques, etc.) produits par la construction.
  - Publication des artefacts dans **Azure Artifacts**, prêts pour le déploiement.

- **Azure Release Pipeline (CD)** : Après la publication des artefacts, une pipeline de release CD est déclenchée pour déployer l'application dans les différents environnements :
  - Déploiement de l'application dans l'environnement de **développement** (Dev).
  - Déploiement de l'application dans l'environnement de **test** (QA).
  - Déploiement de l'application dans l'environnement de **production** (Prod), avec un processus de swap entre le slot de staging et le slot de production pour un déploiement sans interruption.

### 2️⃣ Objectifs de la Partie 1

L'objectif de cette première partie est de vous familiariser avec le concept général du pipeline CI/CD et le rôle que chaque composant joue dans ce processus. Vous devez comprendre comment le code source passe de l'environnement de développement jusqu'à la production en passant par des étapes de construction, de test, et de validation.

### 3️⃣ Conclusion

Cette première partie vous offre une vue d'ensemble du processus CI/CD dans **Azure DevOps**. Dans les parties suivantes, nous allons plonger plus en détail dans la configuration de chaque étape du pipeline CD, en incluant les aspects pratiques et les meilleures pratiques pour garantir un déploiement fluide et sécurisé de vos applications.

---

## 🔵 Partie 2 : Configuration de l’Environnement Azure pour le Déploiement Continu

### 1️⃣ Connexion à Azure Portal

**Étape 1** : Accédez à **Azure Portal** et connectez-vous à votre compte **Microsoft Azure**. Une fois connecté, vous serez dirigé vers le tableau de bord principal d'Azure.

### 2️⃣ Création d’un Groupe de Ressources

**Étape 2** : Pour commencer la configuration, cliquez sur **"Resource groups"** dans le menu principal, puis sélectionnez **"Create"** pour créer un nouveau groupe de ressources. Un groupe de ressources est un conteneur qui regroupe les ressources Azure associées à une solution Azure.

### 3️⃣ Création d’un App Service

**Étape 3** : Après avoir créé le groupe de ressources, accédez à **"App Services"** dans le menu de gauche et cliquez sur **"Create"** pour commencer la création d'un service d'application.

**Étape 4** : Dans le formulaire de création de l'App Service, entrez les détails du projet :
- **Subscription** : Sélectionnez l’abonnement Azure auquel vous souhaitez associer cette application.
- **Resource Group** : Sélectionnez le groupe de ressources que vous avez créé à l’étape précédente.
- **Name** : Choisissez un nom unique pour votre application Web.
- **Publish** : Sélectionnez "Code" si vous déployez une application Web classique ou "Docker Container" pour déployer une application dans un conteneur Docker.
- **Runtime stack** : Sélectionnez la pile d’exécution (par exemple, .NET, Node.js) selon les besoins de votre application.
- **Operating System** : Choisissez le système d'exploitation, Linux ou Windows.
- **Region** : Choisissez la région Azure où vous souhaitez héberger votre application.
- **Pricing plan** : Choisissez un plan tarifaire en fonction des besoins en ressources et du trafic prévu.

### 4️⃣ Déploiement de l’Application Web

**Étape 5** : Après avoir configuré les paramètres de l’App Service, cliquez sur **"Review + create"** pour passer en revue les informations et créer le service. Une fois le service créé, vous serez redirigé vers le tableau de bord de l'App Service.

**Étape 6** : L'application Web que vous avez créée sera maintenant prête à recevoir des déploiements à partir de la pipeline CD.

### 5️⃣ Validation du Déploiement Local

**Étape 7** : Si vous avez déjà développé l'application localement, vous pouvez la tester en exécutant l'application sur votre machine locale à l'aide de l'URL `http://localhost:5000/`.

### 6️⃣ Configuration des Pipelines dans Azure DevOps

**Étape 8** : Accédez à votre compte **Azure DevOps** et vérifiez que votre projet est correctement configuré pour les pipelines CI/CD.

### 🔄 Résumé de la Partie 2

Dans cette partie, nous avons configuré l'environnement Azure pour le déploiement continu, en créant un groupe de ressources et un App Service pour héberger notre application. Nous avons également exploré comment valider le déploiement localement avant de procéder au déploiement dans le cloud via les pipelines Azure DevOps.

---

## 🟠 Partie 3 : Création d'une Application Web sur Azure App Service

### 1️⃣ Accès à la Création d'une Web App

**Étape 1** : Après avoir accédé à votre portail Azure, vous allez créer une nouvelle application Web en utilisant **Azure App Service**. Commencez par cliquer sur **"App Services"** dans le menu principal, puis sélectionnez **"Create"** pour démarrer le processus de création.

### 2️⃣ Détails du Projet

**Étape 2** : Remplissez les informations sous **"Project Details"** :
- **Subscription** : Sélectionnez l'abonnement Azure auquel l'application sera associée.
- **Resource Group** : Si vous n'avez pas encore de groupe de ressources, cliquez sur **"Create new"** pour en créer un nouveau. Donnez un nom pertinent à ce groupe, par exemple "DevopsDemo-rg".
- **Instance Details** : Choisissez un nom unique pour votre application Web, comme "dss-helloworldapp-dev".

### 3️⃣ Configuration des Paramètres de l'Application

**Étape 3** : Configurez les paramètres de l'application :
- **Publish** : Sélectionnez "Code" si vous souhaitez déployer une application web en code natif ou "Docker Container" si vous déployez une application dans un conteneur Docker.
- **Runtime stack** : Choisissez la pile d'exécution adaptée, comme ".NET 7 (STS)" si votre application est construite avec .NET Core.
- **Operating System** : Sélectionnez le système d'exploitation approprié, Linux ou Windows, selon les besoins de votre application.
- **Region** : Sélectionnez la région géographique où vous souhaitez déployer votre application, par exemple "East US".

### 4️⃣ Révision et Création de l'Application

**Étape 4** : Une fois que tous les paramètres sont correctement configurés, cliquez sur **"Review + create"**. Azure va vérifier les paramètres, et vous pourrez ensuite cliquer sur **"Create"** pour lancer la création de l'application Web.

### 5️⃣ Validation dans Azure DevOps

**Étape 5** : Une fois l'application Web créée, accédez à votre projet **Azure DevOps** pour vérifier que le dépôt de code source est correctement configuré. Vous verrez les fichiers de votre projet, notamment le fichier `.csproj` et les fichiers de configuration JSON.

### 🔄 Résumé de la Partie 3

Dans cette partie, vous avez appris à créer une application Web sur **Azure App Service**, en configurant les détails du projet, les paramètres de l'application, et en validant le tout dans **Azure DevOps**. Cette étape est cruciale pour préparer l'application au déploiement continu dans un environnement cloud.

---

## 🔴 Partie 3, 4 et 5 : Création des Applications Web Azure pour Développement, Qualité et Production

### 🟣 Création de l'Application Web pour Développement (Partie 3)

#### 1️⃣ Accès à la Création de l’Application Web

**Étape 1** : Accédez à **"App Services"** dans

 le portail Azure et cliquez sur **"Create"**. Sélectionnez **"Web App"** pour commencer la création de votre application Web de développement.

#### 2️⃣ Détails du Projet

**Étape 2** : Remplissez les informations sous **"Project Details"** :
- **Subscription** : Choisissez votre abonnement Azure.
- **Resource Group** : Créez un nouveau groupe de ressources nommé par exemple **"DevResourceGroup"**.
- **Instance Details** : Nommez votre application Web, par exemple **"dev-helloworldapp"**.

#### 3️⃣ Configuration des Paramètres de l'Application

**Étape 3** : Configurez les détails suivants :
- **Publish** : Sélectionnez "Code".
- **Runtime stack** : Choisissez ".NET 7".
- **Operating System** : Sélectionnez "Windows".
- **Region** : Choisissez "East US".

**Étape 4** : Cliquez sur **"Review + create"**, vérifiez les paramètres, puis cliquez sur **"Create"**.

#### 4️⃣ Vérification

**Étape 5** : Une fois le déploiement terminé, retournez à **"App Services"** pour vérifier que l'application Web de développement a bien été déployée.

---

### 🟡 Création de l'Application Web pour Qualité (Partie 4)

#### 1️⃣ Accès à la Création de l’Application Web

**Étape 1** : Répétez le processus de création de l'application Web en sélectionnant **"Create"** sous **"App Services"**. Cette fois, cette application sera destinée à l'environnement de **qualité**.

#### 2️⃣ Détails du Projet

**Étape 2** : Remplissez les informations sous **"Project Details"** :
- **Subscription** : Sélectionnez votre abonnement Azure.
- **Resource Group** : Créez un nouveau groupe de ressources nommé **"QAResourceGroup"**.
- **Instance Details** : Nommez votre application Web, par exemple **"qa-helloworldapp"**.

#### 3️⃣ Configuration des Paramètres de l'Application

**Étape 3** : Configurez les paramètres suivants :
- **Publish** : Sélectionnez "Code".
- **Runtime stack** : Choisissez ".NET 7".
- **Operating System** : Sélectionnez "Windows".
- **Region** : Choisissez "Canada Central".

**Étape 4** : Cliquez sur **"Review + create"**, vérifiez les paramètres, puis cliquez sur **"Create"**.

#### 4️⃣ Configuration du Monitoring

**Étape 5** : Dans l'onglet **"Monitoring"**, activez **Application Insights** pour surveiller les performances de l'application de qualité.

#### 5️⃣ Vérification

**Étape 6** : Après le déploiement, vérifiez que l'application Web de qualité a été correctement déployée en accédant à **"App Services"**.

---

### 🟠 Création de l'Application Web pour Production (Partie 5)

#### 1️⃣ Accès à la Création de l’Application Web

**Étape 1** : Pour l'application Web de **production**, suivez le même processus en sélectionnant **"Create"** sous **"App Services"**. Cette application sera destinée à l'environnement de production.

#### 2️⃣ Détails du Projet

**Étape 2** : Remplissez les informations sous **"Project Details"** :
- **Subscription** : Sélectionnez votre abonnement Azure.
- **Resource Group** : Créez un groupe de ressources nommé **"ProdResourceGroup"**.
- **Instance Details** : Nommez votre application Web, par exemple **"prod-helloworldapp"**.

#### 3️⃣ Configuration des Paramètres de l'Application

**Étape 3** : Configurez les paramètres suivants :
- **Publish** : Sélectionnez "Code".
- **Runtime stack** : Choisissez ".NET 7".
- **Operating System** : Sélectionnez "Windows".
- **Region** : Choisissez "East US".

**Étape 4** : Cliquez sur **"Review + create"**, vérifiez les paramètres, puis cliquez sur **"Create"**.

#### 4️⃣ Configuration du Monitoring

**Étape 5** : Activez **Application Insights** dans l'onglet **"Monitoring"** pour surveiller les performances de l'application en production.

#### 5️⃣ Ajout de Slots de Déploiement

**Étape 6** : Pour l'application de production, vous pouvez ajouter des slots de déploiement pour gérer les versions en préproduction et production.

#### 6️⃣ Vérification et Suivi

**Étape 7** : Suivez le déploiement depuis l'onglet **"Deployments"** et vérifiez que l'application Web de production est bien en ligne.

---

## 📝 **Résumé**

Vous avez maintenant créé trois applications Web Azure, chacune destinée à un environnement différent : **Développement**, **Qualité**, et **Production**. Chaque application est configurée avec des paramètres spécifiques et surveillée via **Application Insights** pour garantir des performances optimales dans chaque environnement.

---

⚙️ Si vous avez besoin de configurer les pipelines CI/CD pour automatiser ces déploiements ==> rehoumahaythem@gmail.com
