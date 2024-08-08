# Python DevOpsDemo Project Setup and Deployment
## LIENS:
- https://aex.dev.azure.com/me?mkt=fr-FR
- https://portal.azure.com/

## PARTIE # A – Création et déploiement manuel du projet

### A.1. Configuration du projet
1. **Installez Python 3.8+ et pip** : Assurez-vous d'avoir installé Python 3.8 ou une version supérieure et pip (le gestionnaire de paquets Python).
2. **Ouvrez une console et exécutez les commandes suivantes** :
    ```bash
    cd C:\Users\Haythem\Desktop
    python --version  # Vérifiez que Python est installé
    pip --version  # Vérifiez que pip est installé
    mkdir PythonDevopsDemo  # Créez un répertoire pour le projet
    cd PythonDevopsDemo
    python -m venv venv  # Créez un environnement virtuel
    .\venv\Scripts\activate  # Activez l'environnement virtuel sur Windows
    # source venv/bin/activate  # Activez l'environnement virtuel sur MacOS/Linux
    pip install flask  # Installez Flask dans l'environnement virtuel
    ```

3. **Créez un fichier `app.py` avec le contenu suivant** :
    ```python
    from flask import Flask

    app = Flask(__name__)

    @app.route('/')
    def hello():
        return "Hello, World!"

    if __name__ == "__main__":
        app.run(debug=True)
    ```

4. **Testez l'application** :
    ```bash
    python app.py  # Exécutez l'application Flask
    ```
   Vérifiez http://localhost:5000/ dans votre navigateur pour voir l'application en cours d'exécution.

### A.2. Gestion de version avec GIT
1. **Exécutez les commandes suivantes pour configurer Git** :
    ```bash
    cd C:\Users\Haythem\Desktop\PythonDevopsDemo
    git init  # Initialisez un dépôt Git
    git status  # Vérifiez l'état du dépôt
    git config --global user.name "hrhouma"  # Configurez votre nom d'utilisateur Git global
    git config --global user.email "rehoumahaythem@gmail.com"  # Configurez votre email Git global
    git add .  # Ajoutez tous les fichiers au dépôt
    git status  # Vérifiez à nouveau l'état du dépôt
    git commit -m "first commit"  # Faites un commit initial
    ```

### A.3. Création d’un dépôt sur AZURE DEVOPS
1. **Suivez les étapes suivantes pour créer un dépôt sur Azure DevOps** :
    1. **Allez à [Azure DevOps](https://dev.azure.com/)**.
    2. **Créez un profil** si vous n'en avez pas encore.
    3. **Créez une organisation**.
    4. **Créez un projet `PythonDevopsDemo`**.
    5. **Cliquez sur `Repos`**.
    6. **Préparez-vous à faire le push du dépôt local au dépôt distant sur Azure DevOps** :
        ```bash
        git remote help  # Affiche l'aide pour les commandes remote
        cat .git/config  # Affiche la configuration actuelle du dépôt
        git remote remove origin  # Supprime le remote origin actuel s'il existe
        ```
    7. **Générez les identifiants (Credentials) sur Azure DevOps** :
        - **Username**: `hrehouma`
        - **Password**: `votre-mot-de-passe-généré`
        ```bash
        git remote add origin https://hrehouma0084@dev.azure.com/hrehouma0084/PythonDevopsDemo/_git/PythonDevopsDemo
        git push -u origin --all  # Poussez tous les commits vers le dépôt distant
        ```

## PARTIE # B – Intégration continue sur AZURE DEVOPS

### B.1. Configuration de la pipeline (classic editor pipeline)
1. **Activez le `classic editor pipeline` au niveau organisationnel** :
    1. **Allez dans `Organisation settings` (Paramètres de l'organisation)**.
    2. **Naviguez vers `Pipelines` > `Settings` (Paramètres)**.
    3. **Désactivez les options `Disable creation of classic build pipelines` (Désactiver la création de pipelines de build classiques) et `Disable creation of classic release pipelines` (Désactiver la création de pipelines de release classiques)** en les mettant sur `off`.
    4. **Allez dans `Project settings` (Paramètres du projet)**.
    5. **Naviguez vers `Pipelines` > `Settings` (Paramètres)**.
    6. **Désactivez les mêmes options (`Disable creation of classic build pipelines` et `Disable creation of classic release pipelines`) en les mettant sur `off`**.

### B.2. Création de la pipeline CI (Méthode # 1 - classic editor pipeline)
1. **Créez la pipeline CI en utilisant l'outil `classic editor pipeline`** :
    1. **Allez dans `Pipelines` > `New pipeline` (Nouvelle pipeline)**.
    2. **Choisissez `Use the classic editor` (Utiliser l'éditeur classique)**.
    3. **Sélectionnez `Azure Repos Git` puis votre dépôt `PythonDevopsDemo`**.
    4. **Choisissez `Python package` comme type de projet**.
    5. **Supprimez les composants proposés par défaut et ajoutez les composants suivants** :

#### Premier Composant (1/4)
**NATURE DE LA COMPOSANTE**: `Use Python Version`
- **Display name**: Use Python 3.x
- **Task Version**: `0`
- **Package type**: `Python`
- **Version Spec**: `3.x`
- **Add to PATH**: `true`

#### Deuxième Composant (2/4)
**NATURE DE LA COMPOSANTE**: `Command Line Script`
- **Display name**: Install dependencies
- **Script**: `pip install -r requirements.txt`

#### Troisième Composant (3/4)
**NATURE DE LA COMPOSANTE**: `Command Line Script`
- **Display name**: Run tests
- **Script**: `pytest`

#### Quatrième Composant (4/4)
**NATURE DE LA COMPOSANTE**: `Command Line Script`
- **Display name**: Package application
- **Script**: `python setup.py sdist bdist_wheel`

#### Cinquième Composant (5/5)
**NATURE DE LA COMPOSANTE**: `Publish Build Artifacts`
- **Display name**: Publish Artifact: drop
- **Path to publish**: `dist`
- **Artifact name**: drop
- **Artifact publish location**: Azure pipelines

### TRIGGER (AUTOMATISER)
1. **Faites ce changement dans votre fichier `app.py`** :
    ```python
    @app.route('/change')
    def change():
        return "Changement 1"
    ```

2. **Exécutez les commandes suivantes pour valider et pousser vos changements** :
    ```bash
    git status
    git add .
    git commit -m 'lancement du CI'
    git push -u origin --all
    ```

### B.3. Création de la pipeline CI (Méthode # 2 - YAML)
1. **Créez la pipeline CI en utilisant le YAML** :
    ```yaml
    trigger:
    - main

    pool:
      vmImage: 'ubuntu-22.04'

    steps:
    - task: UsePythonVersion@0
      inputs:
        versionSpec: '3.x'
        addToPath: true

    - script: |
        python -m venv venv
        source venv/bin/activate
        pip install -r requirements.txt
      displayName: 'Install dependencies'

    - script: |
        source venv/bin/activate
        pytest
      displayName: 'Run tests'

    - script: |
        source venv/bin/activate
        python setup.py sdist bdist_wheel
      displayName: 'Package application'

    - task: PublishBuildArtifacts@1
      inputs:
        PathtoPublish: 'dist'
        ArtifactName: 'drop'
        publishLocation: 'Container'
    ```

2. **Faites ce changement dans votre fichier `app.py`** :
    ```python
    @app.route('/change')
    def change():
        return "Changement 1"
    ```

3. **Testez votre pipeline** :
    ```bash
    git status
    git add .
    git commit -m 'lancement du CI'
    git push -u origin --all
    ```

