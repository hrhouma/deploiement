# DevOpsDemo Project Setup and Deployment

## PARTIE # A – Création et déploiement manuel du projet

### A.1. Configuration du projet
1. **Téléchargez le Framework dotnet .NET 5 et .NET 7** :
   - Vous pouvez télécharger .NET 5 à partir du [site officiel de .NET 5](https://dotnet.microsoft.com/download/dotnet/5.0).
   - Vous pouvez télécharger .NET 7 à partir du [site officiel de .NET 7](https://dotnet.microsoft.com/download/dotnet/7.0).

2. **Ouvrez une console et exécutez les commandes suivantes** :
    ```bash
    cd C:\Users\Haythem\Desktop  # Changez de répertoire pour votre bureau
    dotnet --version  # Vérifiez que .NET est installé et affichez la version installée
    dotnet --list-sdks  # Listez tous les SDK .NET installés
    dotnet --list-runtimes  # Listez tous les runtimes .NET installés
    dotnet --help  # Affichez l'aide pour les commandes .NET
    md DevopsDemo  # Créez un nouveau répertoire nommé DevopsDemo
    cd DevopsDemo  # Accédez au répertoire DevopsDemo
    dotnet new globaljson  # Créez un fichier global.json pour spécifier la version de .NET SDK à utiliser
    ls  # Listez les fichiers dans le répertoire pour vérifier que global.json a été créé
    cat .\global.json  # Affichez le contenu du fichier global.json
    dotnet --list-sdks  # Vérifiez à nouveau les SDK disponibles
    nano .\global.json  # Éditez le fichier global.json avec l'éditeur de texte nano (vous pouvez utiliser n'importe quel éditeur de texte)
    ```

    Exemple de contenu pour `global.json` pour utiliser .NET 7.0 :
    ```json
    {
      "sdk": {
        "version": "7.0.100"
      }
    }
    ```

3. **Dépannage & troubleshooting** : Si vous rencontrez des problèmes pour changer la version par défaut du SDK .NET, suivez ce guide [How to change default dotnet SDK version](https://dev.to/polarbit/how-to-change-default-dotnet-sdk-version-43ph).

### A.2. Construction du projet et d’une page web simple ASP.NET
1. **Exécutez les commandes suivantes pour construire le projet** :
    ```bash
    cd C:\  # Revenez à la racine de votre disque
    md DevopsDemo  # Créez un répertoire DevopsDemo si ce n'est pas déjà fait
    cd DevopsDemo  # Accédez au répertoire DevopsDemo
    dotnet new sln -o HelloWorldApp  # Créez une nouvelle solution nommée HelloWorldApp
    cd HelloWorldApp  # Accédez au répertoire HelloWorldApp
    dir  # Listez les fichiers dans le répertoire
    dotnet new mvc -n HelloWorldApp.web  # Créez un nouveau projet MVC nommé HelloWorldApp.web
    dir  # Listez les fichiers pour vérifier la création du projet
    code .  # Ouvrez le répertoire courant dans Visual Studio Code (ou tout autre éditeur de votre choix)
    cd HelloWorldApp.web  # Accédez au répertoire du projet web
    dir  # Listez les fichiers dans le répertoire du projet web
    dotnet build  # Construisez le projet
    dotnet build --configuration debug  # Construisez le projet en mode débogage
    dotnet build --configuration release  # Construisez le projet en mode release
    ```

2. **Vérifiez la présence de deux dossiers Debug et Release** :
    ```bash
    cd C:\DevopsDemo\HelloWorldApp\HelloWorldApp.web\bin\release\net7.0  # Accédez au répertoire de sortie en mode release
    dotnet HelloWorldApp.web.dll  # Exécutez l'application
    Vérifiez http://localhost:5000/  # Ouvrez votre navigateur et vérifiez que l'application fonctionne
    ```

### A.3. Déploiement de la page web manuellement
1. **Exécutez les commandes suivantes pour déployer le projet** :
    ```bash
    cd C:\DevopsDemo\HelloWorldApp\HelloWorldApp.web  # Accédez au répertoire du projet web
    dotnet new sln -o HelloWorldApp  # Créez une nouvelle solution nommée HelloWorldApp
    dotnet publish -o /out  # Publiez le projet dans le répertoire /out
    dotnet publish -c release -o /out  # Publiez le projet en mode release dans le répertoire /out
    cd C:\out\  # Accédez au répertoire de sortie
    dotnet HelloWorldApp.web.dll  # Exécutez l'application publiée
    Vérifiez http://localhost:5000/  # Ouvrez votre navigateur et vérifiez que l'application fonctionne
    ```

### A.4. Gestion de version avec GIT
1. **Exécutez les commandes suivantes pour configurer Git** :
    ```bash
    cd C:\DevopsDemo\HelloWorldApp  # Accédez au répertoire de la solution
    git init  # Initialisez un dépôt Git
    git status  # Vérifiez l'état du dépôt
    git config --global user.name "hrhouma"  # Configurez votre nom d'utilisateur Git global
    git config --global user.email "rehoumahaythem@gmail.com"  # Configurez votre email Git global
    git config --local user.name "hrhouma"  # Configurez votre nom d'utilisateur Git local
    git config --local user.email "rehoumahaythem@gmail.com"  # Configurez votre email Git local
    code .  # Ouvrez le répertoire courant dans Visual Studio Code (ou tout autre éditeur de votre choix)
    git add .  # Ajoutez tous les fichiers au dépôt
    git status  # Vérifiez l'état du dépôt
    git commit -m "first commit"  # Faites un commit initial
    ```

### A.5. Création d’un dépôt sur AZURE DEVOPS
1. **Suivez les étapes suivantes pour créer un dépôt sur Azure DevOps** :
    1. **Allez à [Azure DevOps](https://dev.azure.com/)**.
    2. **Créez un profil** si vous n'en avez pas encore.
    3. **Créez une organisation**.
    4. **Créez un projet `HelloWorldApp`**.
    5. **Cliquez sur `Repos`**.
    6. **Préparez-vous à faire le push du dépôt local au dépôt distant sur Azure DevOps** :
        ```bash
        git remote help  # Affichez l'aide pour les commandes remote
        cat .git/config  # Affichez la configuration actuelle du dépôt
        git remote remove origin  # Supprime le remote origin actuel s'il existe
        ```
    7. **Générez les identifiants (Credentials) sur Azure DevOps** :
        - **Username**: `hrehouma`
        - **Password**: `vv2qfumwpirb3lcol6bynlkachvsnoigmic5afbx2r5dbxg7e5tq`
        ```bash
        git remote add origin https://hrehouma0084@dev.azure.com/hrehouma0084/HelloWorldApp/_git/HelloWorldApp
        git push -u origin --all  # Poussez tous les commits vers le dépôt distant
        ```

    8. **Section facultative : confirmation de la sauvegarde des informations sur votre ordinateur local via le gestionnaire d'identifiants**.

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
    1. **Allez dans `Pipelines

` > `New pipeline` (Nouvelle pipeline)**.
    2. **Choisissez `Use the classic editor` (Utiliser l'éditeur classique)**.
    3. **Sélectionnez `Azure Repos Git` puis votre dépôt `HelloWorldApp`**.
    4. **Choisissez `ASP.NET Core` (sans le .NET Framework) comme type de projet**.
    5. **Supprimez les 4 composants proposés par défaut**.
    6. **Ajoutez les composants suivants** :

#### Premier Composant (1/4)
**NATURE DE LA COMPOSANTE**: `.NET Core`
- **Display name**: Restore Libraries
- **Task Version**: `2`
- **Command**: `restore`
- **Path to project(s)**: `**/*.csproj` (si ça ne fonctionne pas, il faut le changer d’abord dans Get Sources ou Agent Job)
- **Arguments**: NO

#### Deuxième Composant (2/4)
**NATURE DE LA COMPOSANTE**: `.NET Core`
- **Display name**: Build
- **Task Version**: `2`
- **Command**: `build`
- **Path to project(s)**: `**/*.csproj`
- **Arguments**: `--configuration $(BuildConfiguration)`

#### Troisième Composant (3/4)
**NATURE DE LA COMPOSANTE**: `.NET Core`
- **Display name**: Publish
- **Task Version**: `2`
- **Command**: `publish`
- **Path to project(s)**: `**/*.csproj`
- **Arguments**: `--configuration $(BuildConfiguration) --output $(build.artifactstagingdirectory)`
- **Options**: 
  - Cocher "zip published projects"
  - Cocher "add project's folder name to publish path"

#### Quatrième Composant (4/4)
**NATURE DE LA COMPOSANTE**: `Publish Build Artifacts`
- **Display name**: Publish Artifact: drop
- **Path to publish**: `$(Build.ArtifactStagingDirectory)`
- **Artifact name**: drop
- **Artifact publish location**: Azure pipelines

### TRIGGER (AUTOMATISER)
1. **Faites ce changement dans votre fichier HTML** :
    ```html
    <p> changement 1 </p>
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
    - task: UseDotNet@2
      inputs:
        packageType: 'sdk'
        version: '7.x'
        installationPath: $(Agent.ToolsDirectory)/dotnet

    - task: DotNetCoreCLI@2
      displayName: 'Restore Libraries'
      inputs:
        command: 'restore'
        projects: '**/*.csproj'

    - task: DotNetCoreCLI@2
      displayName: 'Build'
      inputs:
        command: 'build'
        projects: '**/*.csproj'
        arguments: '--configuration $(BuildConfiguration)'

    - task: DotNetCoreCLI@2
      displayName: 'Publish'
      inputs:
        command: 'publish'
        publishWebProjects: true
        projects: '**/*.csproj'
        arguments: '--configuration $(BuildConfiguration) --output $(Build.ArtifactStagingDirectory)'
        zipAfterPublish: true
        modifyOutputPath: true

    - task: PublishBuildArtifacts@1
      displayName: 'Publish Artifact'
      inputs:
        PathtoPublish: '$(Build.ArtifactStagingDirectory)'
        ArtifactName: 'drop'
        publishLocation: 'Container'
    ```

2. **Faites ce changement dans votre fichier HTML** :
    ```html
    <p> changement 2 </p>
    ```

3. **Testez votre pipeline** :
    ```bash
    git status
    git add .
    git commit -m 'lancement du CI'
    git push -u origin --all
    ```

-------

# Annexe :


### B.3. Création de la pipeline CI (Méthode # 2 - YAML)

1. **Créez la pipeline CI en utilisant le YAML** :
    - **trigger** : Cette section spécifie les branches qui déclencheront la pipeline. Ici, `main` signifie que chaque fois qu'un changement est poussé à la branche `main`, la pipeline sera déclenchée.
      ```yaml
      trigger:
      - main
      ```

    - **pool** : Cette section spécifie l'agent de build que la pipeline utilisera. Ici, `vmImage: 'ubuntu-22.04'` indique que la pipeline s'exécutera sur une machine virtuelle Ubuntu 22.04.
      ```yaml
      pool:
        vmImage: 'ubuntu-22.04'
      ```

    - **steps** : Cette section contient les différentes étapes que la pipeline exécutera. Chaque étape est une tâche (task) avec des paramètres spécifiques.

      1. **UseDotNet@2** : Cette tâche installe une version spécifique du SDK .NET sur l'agent de build.
         - **packageType** : Le type de package à installer, ici `sdk` pour le kit de développement logiciel.
         - **version** : La version du SDK .NET à installer, ici `7.x` signifie qu'on installe la version 7.x.
         - **installationPath** : Le chemin où le SDK sera installé sur l'agent de build.
         ```yaml
         - task: UseDotNet@2
           inputs:
             packageType: 'sdk'
             version: '7.x'
             installationPath: $(Agent.ToolsDirectory)/dotnet
         ```

      2. **DotNetCoreCLI@2 - Restore Libraries** : Cette tâche restaure les dépendances du projet .NET.
         - **displayName** : Le nom affiché pour cette tâche, ici `Restore Libraries`.
         - **command** : La commande à exécuter, ici `restore` pour restaurer les dépendances.
         - **projects** : Le chemin vers les fichiers de projet, ici `**/*.csproj` signifie tous les fichiers .csproj dans tous les sous-répertoires.
         ```yaml
         - task: DotNetCoreCLI@2
           displayName: 'Restore Libraries'
           inputs:
             command: 'restore'
             projects: '**/*.csproj'
         ```

      3. **DotNetCoreCLI@2 - Build** : Cette tâche construit le projet .NET.
         - **displayName** : Le nom affiché pour cette tâche, ici `Build`.
         - **command** : La commande à exécuter, ici `build` pour construire le projet.
         - **projects** : Le chemin vers les fichiers de projet, ici `**/*.csproj`.
         - **arguments** : Les arguments supplémentaires pour la commande de build, ici `--configuration $(BuildConfiguration)` signifie que la configuration de build (Debug ou Release) sera spécifiée par une variable de pipeline.
         ```yaml
         - task: DotNetCoreCLI@2
           displayName: 'Build'
           inputs:
             command: 'build'
             projects: '**/*.csproj'
             arguments: '--configuration $(BuildConfiguration)'
         ```

      4. **DotNetCoreCLI@2 - Publish** : Cette tâche publie le projet .NET.
         - **displayName** : Le nom affiché pour cette tâche, ici `Publish`.
         - **command** : La commande à exécuter, ici `publish` pour publier le projet.
         - **publishWebProjects** : Une option pour publier les projets web, ici `true`.
         - **projects** : Le chemin vers les fichiers de projet, ici `**/*.csproj`.
         - **arguments** : Les arguments supplémentaires pour la commande de publication, ici `--configuration $(BuildConfiguration) --output $(Build.ArtifactStagingDirectory)` signifie que la configuration de publication sera spécifiée par une variable de pipeline et le chemin de sortie sera défini par une autre variable de pipeline.
         - **zipAfterPublish** : Une option pour compresser les fichiers publiés, ici `true`.
         - **modifyOutputPath** : Une option pour modifier le chemin de sortie, ici `true`.
         ```yaml
         - task: DotNetCoreCLI@2
           displayName: 'Publish'
           inputs:
             command: 'publish'
             publishWebProjects: true
             projects: '**/*.csproj'
             arguments: '--configuration $(BuildConfiguration) --output $(Build.ArtifactStagingDirectory)'
             zipAfterPublish: true
             modifyOutputPath: true
         ```

      5. **PublishBuildArtifacts@1 - Publish Artifact** : Cette tâche publie les artefacts de build.
         - **displayName** : Le nom affiché pour cette tâche, ici `Publish Artifact`.
         - **PathtoPublish** : Le chemin vers les fichiers à publier, ici `$(Build.ArtifactStagingDirectory)` signifie que les fichiers publiés seront dans le répertoire spécifié par cette variable de pipeline.
         - **ArtifactName** : Le nom de l'artefact, ici `drop`.
         - **publishLocation** : L'emplacement de publication, ici `Container` signifie que les artefacts seront publiés dans un conteneur de stockage Azure DevOps.
         ```yaml
         - task: PublishBuildArtifacts@1
           displayName: 'Publish Artifact'
           inputs:
             PathtoPublish: '$(Build.ArtifactStagingDirectory)'
             ArtifactName: 'drop'
             publishLocation: 'Container'
         ```

---

### Détails supplémentaires pour les débutants

#### 1. **trigger**
- **trigger** : Cette section définit les branches qui déclencheront la pipeline. Le pipeline sera exécuté automatiquement chaque fois qu'un changement est poussé à la branche spécifiée. Ici, `main` signifie que la branche principale du dépôt déclenchera la pipeline.
  ```yaml
  trigger:
  - main
  ```

#### 2. **pool**
- **pool** : Cette section spécifie l'agent de build que la pipeline utilisera. Un agent est une machine sur laquelle Azure DevOps exécute vos étapes de pipeline. Ici, `vmImage: 'ubuntu-22.04'` indique que la pipeline s'exécutera sur une machine virtuelle Ubuntu 22.04.
  ```yaml
  pool:
    vmImage: 'ubuntu-22.04'
  ```

#### 3. **steps**
- **steps** : Cette section contient les différentes étapes que la pipeline exécutera. Chaque étape est une tâche (task) avec des paramètres spécifiques. Les étapes sont exécutées dans l'ordre où elles sont définies.

##### 3.1. **UseDotNet@2**
- **task: UseDotNet@2** : Cette tâche installe une version spécifique du SDK .NET sur l'agent de build.
  - **packageType** : Le type de package à installer. Ici, `sdk` signifie que nous installons le kit de développement logiciel .NET.
  - **version** : La version du SDK .NET à installer. Ici, `7.x` signifie que nous installons la version 7.x du SDK .NET.
  - **installationPath** : Le chemin où le SDK sera installé sur l'agent de build. `$(Agent.ToolsDirectory)/dotnet` est une variable de pipeline qui représente le répertoire d'installation des outils sur l'agent.
  ```yaml
  - task: UseDotNet@2
    inputs:
      packageType: 'sdk'
      version: '7.x'
      installationPath: $(Agent.ToolsDirectory)/dotnet
  ```

##### 3.2. **DotNetCoreCLI@2 - Restore Libraries**
- **task: DotNetCoreCLI@2** : Cette tâche exécute une commande CLI .NET Core.
  - **displayName** : Le nom affiché pour cette tâche, ici `Restore Libraries`.
  - **command** : La commande à exécuter. Ici, `restore` pour restaurer les dépendances du projet .NET.
  - **projects** : Le chemin vers les fichiers de projet. Ici, `**/*.csproj` signifie tous les fichiers .csproj dans tous les sous-répertoires.
  ```yaml
  - task: DotNetCoreCLI@2
    displayName: 'Restore Libraries'
    inputs:
      command: 'restore'
      projects: '**/*.csproj'
  ```

##### 3.3. **DotNetCoreCLI@2 - Build**
- **task: DotNetCoreCLI@2** : Cette tâche exécute une commande CLI .NET Core.
  - **displayName** : Le nom affiché pour cette tâche, ici `Build`.
  - **command** : La commande à exécuter. Ici, `build` pour construire le projet .NET.
  - **projects** : Le chemin vers les fichiers de projet. Ici, `**/*.csproj`.
  - **arguments** : Les arguments supplémentaires pour la commande de build. Ici, `--configuration $(BuildConfiguration)` signifie que la configuration de build (Debug ou Release) sera spécifiée par une variable de pipeline.
  ```yaml
  - task: DotNetCoreCLI@2
    displayName: 'Build'
    inputs:
      command: 'build'
      projects: '**/*.csproj'
      arguments: '--configuration $(BuildConfiguration)'
  ```

##### 3.4. **DotNetCoreCLI@2 - Publish**
- **task: Dot

NetCoreCLI@2** : Cette tâche exécute une commande CLI .NET Core.
  - **displayName** : Le nom affiché pour cette tâche, ici `Publish`.
  - **command** : La commande à exécuter. Ici, `publish` pour publier le projet .NET.
  - **publishWebProjects** : Une option pour publier les projets web. Ici, `true`.
  - **projects** : Le chemin vers les fichiers de projet. Ici, `**/*.csproj`.
  - **arguments** : Les arguments supplémentaires pour la commande de publication. Ici, `--configuration $(BuildConfiguration) --output $(Build.ArtifactStagingDirectory)` signifie que la configuration de publication sera spécifiée par une variable de pipeline et le chemin de sortie sera défini par une autre variable de pipeline.
  - **zipAfterPublish** : Une option pour compresser les fichiers publiés. Ici, `true`.
  - **modifyOutputPath** : Une option pour modifier le chemin de sortie. Ici, `true`.
  ```yaml
  - task: DotNetCoreCLI@2
    displayName: 'Publish'
    inputs:
      command: 'publish'
      publishWebProjects: true
      projects: '**/*.csproj'
      arguments: '--configuration $(BuildConfiguration) --output $(Build.ArtifactStagingDirectory)'
      zipAfterPublish: true
      modifyOutputPath: true
  ```

##### 3.5. **PublishBuildArtifacts@1 - Publish Artifact**
- **task: PublishBuildArtifacts@1** : Cette tâche publie les artefacts de build.
  - **displayName** : Le nom affiché pour cette tâche, ici `Publish Artifact`.
  - **PathtoPublish** : Le chemin vers les fichiers à publier. Ici, `$(Build.ArtifactStagingDirectory)` signifie que les fichiers publiés seront dans le répertoire spécifié par cette variable de pipeline.
  - **ArtifactName** : Le nom de l'artefact. Ici, `drop`.
  - **publishLocation** : L'emplacement de publication. Ici, `Container` signifie que les artefacts seront publiés dans un conteneur de stockage Azure DevOps.
  ```yaml
  - task: PublishBuildArtifacts@1
    displayName: 'Publish Artifact'
    inputs:
      PathtoPublish: '$(Build.ArtifactStagingDirectory)'
      ArtifactName: 'drop'
      publishLocation: 'Container'
  ```

---

### Commentaires + explications : 

```yaml
trigger:
- main  # Déclenche la pipeline sur les commits à la branche principale

pool:
  vmImage: 'ubuntu-22.04'  # Utilise une machine virtuelle Ubuntu 22.04 comme agent de build

steps:
- task: UseDotNet@2  # Installe une version spécifique du SDK .NET
  inputs:
    packageType: 'sdk'  # Installe le SDK .NET
    version: '7.x'  # Spécifie la version du SDK .NET à installer
    installationPath: $(Agent.ToolsDirectory)/dotnet  # Chemin d'installation du SDK

- task: DotNetCoreCLI@2  # Exécute une commande CLI .NET Core pour restaurer les dépendances
  displayName: 'Restore Libraries'  # Nom affiché pour cette étape
  inputs:
    command: 'restore'  # Commande pour restaurer les dépendances
    projects: '**/*.csproj'  # Chemin vers les fichiers de projet

- task: DotNetCoreCLI@2  # Exécute une commande CLI .NET Core pour construire le projet
  displayName: 'Build'  # Nom affiché pour cette étape
  inputs:
    command: 'build'  # Commande pour construire le projet
    projects: '**/*.csproj'  # Chemin vers les fichiers de projet
    arguments: '--configuration $(BuildConfiguration)'  # Arguments pour la commande de build

- task: DotNetCoreCLI@2  # Exécute une commande CLI .NET Core pour publier le projet
  displayName: 'Publish'  # Nom affiché pour cette étape
  inputs:
    command: 'publish'  # Commande pour publier le projet
    publishWebProjects: true  # Option pour publier les projets web
    projects: '**/*.csproj'  # Chemin vers les fichiers de projet
    arguments: '--configuration $(BuildConfiguration) --output $(Build.ArtifactStagingDirectory)'  # Arguments pour la commande de publication
    zipAfterPublish: true  # Compresse les fichiers publiés
    modifyOutputPath: true  # Modifie le chemin de sortie

- task: PublishBuildArtifacts@1  # Publie les artefacts de build
  displayName: 'Publish Artifact'  # Nom affiché pour cette étape
  inputs:
    PathtoPublish: '$(Build.ArtifactStagingDirectory)'  # Chemin vers les fichiers à publier
    ArtifactName: 'drop'  # Nom de l'artefact
    publishLocation: 'Container'  # Emplacement de publication
```

   
