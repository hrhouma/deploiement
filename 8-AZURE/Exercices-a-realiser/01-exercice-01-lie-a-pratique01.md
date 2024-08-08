# Python DevOpsDemo Project Setup and Deployment

## PARTIE # A – Création et déploiement manuel du projet

### A.1. Configuration du projet
1. Installez Python 3.8+ et pip
2. Ouvrez une console et exécutez les commandes suivantes :
    ```bash
    cd C:\Users\Haythem\Desktop
    python --version
    pip --version
    mkdir PythonDevopsDemo
    cd PythonDevopsDemo
    python -m venv venv
    .\venv\Scripts\activate  # Sur Windows
    source venv/bin/activate  # Sur MacOS/Linux
    pip install flask
    ```

3. Créez un fichier `app.py` avec le contenu suivant :
    ```python
    from flask import Flask

    app = Flask(__name__)

    @app.route('/')
    def hello():
        return "Hello, World!"

    if __name__ == "__main__":
        app.run(debug=True)
    ```

4. Testez l'application :
    ```bash
    python app.py
    ```
   Vérifiez http://localhost:5000/

### A.2. Gestion de version avec GIT
1. Exécutez les commandes suivantes pour configurer Git :
    ```bash
    cd C:\Users\Haythem\Desktop\PythonDevopsDemo
    git init
    git status
    git config --global user.name "hrhouma"
    git config --global user.email "rehoumahaythem@gmail.com"
    git add .
    git status
    git commit -m "first commit"
    ```

### A.3. Création d’un dépôt sur AZURE DEVOPS
1. Suivez les étapes suivantes pour créer un dépôt sur Azure DevOps :
    1. Allez à [Azure DevOps](https://dev.azure.com/)
    2. Créez un profil
    3. Créez une organisation
    4. Créez un projet `PythonDevopsDemo`
    5. Cliquez sur `Repos`
    6. Préparez-vous à faire le push du dépôt local au dépôt distant sur Azure DevOps :
        ```bash
        git remote help
        cat .git/config
        git remote remove origin
        ```
    7. Générez les identifiants (Credentials) sur Azure DevOps :
        - Username: `hrehouma`
        - Password: `votre-mot-de-passe-généré`
        ```bash
        git remote add origin https://hrehouma0084@dev.azure.com/hrehouma0084/PythonDevopsDemo/_git/PythonDevopsDemo
        git push -u origin --all
        ```

## PARTIE # B – Intégration continue sur AZURE DEVOPS

### B.1. Configuration de la pipeline (classic editor pipeline)
1. Activez le `classic editor pipeline` au niveau organisationnel :
    1. Organisation settings => pipelines => settings => Disable creation of classic build pipelines + Disable creation of classic release pipelines => off.
    2. Project settings => pipelines => settings => Disable creation of classic build pipelines + Disable creation of classic release pipelines => off.

### B.2. Création de la pipeline CI (Méthode # 1 - classic editor pipeline)
1. Créez la pipeline CI en utilisant l'outil `classic editor pipeline` :
    1. Pipelines => new pipeline => Use the classic editor => Azure Repos Git => Python package.
    2. Supprimez les composants proposés et ajoutez les composants suivants :

#### Premier Composant (1/4)
**RESTORE**
- Display name: Install dependencies
- Command: `pip install -r requirements.txt`

#### Deuxième Composant (2/4)
**BUILD**
- Display name: Run tests
- Command: `pytest`

#### Troisième Composant (3/4)
**PUBLISH**
- Display name: Package application
- Command: `python setup.py sdist bdist_wheel`

#### Quatrième Composant (4/4)
**PUBLISH ARTIFACT**
- Display name: Publish Artifact: drop
- Path to publish: `dist`
- Artifact name: drop
- Artifact publish location: Azure pipelines

### TRIGGER (AUTOMATISER)
1. Faites ce changement dans votre fichier `app.py` :
    ```python
    @app.route('/change')
    def change():
        return "Changement 1"
    ```

2. Exécutez les commandes suivantes pour valider et pousser vos changements :
    ```bash
    git status
    git add .
    git commit -m 'lancement du CI'
    git push -u origin --all
    ```

### B.3. Création de la pipeline CI (Méthode # 2 - YAML)
1. Créez la pipeline CI en utilisant le YAML :
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

2. Faites ce changement dans votre fichier `app.py` :
    ```python
    @app.route('/change')
    def change():
        return "Changement 1"
    ```

3. Testez votre pipeline :
    ```bash
    git status
    git add .
    git commit -m 'lancement du CI'
    git push -u origin --all
    ```
