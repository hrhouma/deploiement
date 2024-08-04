# Cours sur Azure DevOps (PARTIE 2 - CD)

#### Introduction

Azure DevOps est un ensemble de services permettant de planifier le travail, de collaborer au développement de code, et de créer et déployer des applications. Ce cours vous guidera à travers le processus de configuration d'un pipeline CI/CD pour déployer une application web sur Azure. 

#### Étapes de Création et Déploiement d'une Application Web

---

### 1. Introduction

#### Schéma dans la Vraie Vie
Un développeur reçoit des instructions de la part du Product Owner (PO) et de l'équipe, souvent mentionnées sur un outil de gestion de projet comme ASBL (similaire à Jira). Le développeur travaille sur son environnement de développement, comme Visual Studio, pour développer la fonctionnalité.

---

### 2. Création des Applications Web

#### Accéder au Portail Azure
1. **Portails Utilisés** : 
   - Portail Azure pour la gestion des ressources.
   - Azure DevOps pour l'intégration continue et le déploiement continu.

2. **Créer un Groupe de Ressources** :
   - Nommer le groupe "DevOpsDemo".

3. **Créer Trois Applications Web** :
   - Environnement de développement : "App-Dev".
   - Environnement de qualité : "App-QA".
   - Environnement de production : "App-Prod".

4. **Configuration** :
   - Utiliser l'abonnement Azure.
   - Créer les applications dans la région "Canada Central".
   - Désactiver Application Insights pour éviter des coûts supplémentaires.

---

### 3. Configuration des Pipelines CI/CD

#### Créer une Connexion de Service

1. **Paramètres du Projet** :
   - Allez dans les paramètres du projet dans Azure DevOps.
   - Créez une connexion de service Azure Resource Manager.

2. **Choisir les Paramètres** :
   - Sélectionner votre abonnement Azure.
   - Choisir le groupe de ressources "DevOpsDemo".
   - Donner un nom à la connexion (par exemple, "DevOpsConnection").

#### Configurer le Pipeline de Développement

1. **Créer un Pipeline** :
   - Allez dans la section "Pipelines" de votre projet Azure DevOps.
   - Sélectionnez "Azure service deployment".

2. **Configurer le Job de Développement** :
   - Choisir l'abonnement et la connexion de service créée.
   - Sélectionner l'application "App-Dev".
   - Ajouter les tâches nécessaires : installation des librairies, compilation, tests, packaging, et publication des artefacts.

---

### 4. Gestion des Environnements et Déploiement

#### Environnements de Travail
1. **Types d'Environnements** :
   - Développement
   - Qualité
   - Production

2. **Créer des Slots de Déploiement** :
   - Pour l'application de production, créer un slot de staging.

#### Déploiement Continu

1. **Automatisation des Déploiements** :
   - Configurer les pipelines pour qu'ils se déclenchent automatiquement lors de nouveaux commits.
   - Ajouter des conditions d'approbation pour chaque environnement.

2. **Gestion des Approvals** :
   - Définir des approbations manuelles pour le déploiement en QA et Production.
   - Désigner les responsables pour chaque étape d'approbation.

---

### 5. Exécution et Surveillance des Pipelines

#### Exécution des Pipelines

1. **Lancer le Pipeline** :
   - Exécuter le pipeline de développement et surveiller les logs pour vérifier que tout se passe bien.
   - Une fois validé, le déploiement se poursuit automatiquement vers les environnements QA et Production.

2. **Approuver les Étapes** :
   - Les responsables des environnements QA et Production doivent approuver les déploiements.

#### Surveillance des Déploiements

1. **Vérifier les Logs** :
   - Utiliser les journaux de pipeline pour surveiller l'avancement et les éventuels problèmes.

2. **Tester les Applications Déployées** :
   - Accéder aux applications déployées via leurs URLs pour vérifier que les changements ont été correctement appliqués.

---

### Conclusion

Ce cours vous a guidé à travers la configuration d'un pipeline CI/CD sur Azure DevOps pour déployer une application web. En suivant ces étapes, vous pouvez automatiser efficacement le processus de développement et de déploiement, tout en assurant un contrôle de qualité rigoureux grâce aux approbations manuelles.

---

### Ressources Supplémentaires

- [Documentation Azure DevOps](https://docs.microsoft.com/en-us/azure/devops/)
- [Tutoriels Azure](https://docs.microsoft.com/en-us/learn/azure/)
- [Communauté DevOps](https://devblogs.microsoft.com/devops/)

---

Merci pour votre attention et bonne continuation dans vos projets DevOps !
