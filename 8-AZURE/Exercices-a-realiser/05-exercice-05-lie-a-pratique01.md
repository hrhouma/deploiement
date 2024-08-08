# Scala DevOpsDemo Project Setup and Deployment

## LIENS:
- https://aex.dev.azure.com/me?mkt=fr-FR
- https://portal.azure.com/

## PARTIE # A – Création et déploiement manuel du projet

### A.1. Configuration du projet
1. **Installez Java JDK 11+ et SBT** : Assurez-vous d'avoir installé Java Development Kit (JDK) version 11 ou supérieure et SBT (Simple Build Tool).
2. **Ouvrez une console et exécutez les commandes suivantes** :
    ```bash
    cd C:\Users\Haythem\Desktop
    java -version  # Vérifiez que Java est installé
    sbt sbtVersion  # Vérifiez que SBT est installé
    mkdir ScalaDevopsDemo  # Créez un répertoire pour le projet
    cd ScalaDevopsDemo
    sbt new scala/scala-seed.g8  # Créez un nouveau projet Scala avec SBT
    ```

3. **Modifiez le fichier `build.sbt` pour inclure les dépendances Apache Spark** :
    ```sbt
    name := "ScalaDevopsDemo"

    version := "0.1"

    scalaVersion := "2.12.10"

    libraryDependencies ++= Seq(
      "org.apache.spark" %% "spark-core" % "3.1.1",
      "org.apache.spark" %% "spark-sql" % "3.1.1"
    )
    ```

4. **Créez un fichier `src/main/scala/com/example/App.scala` avec le contenu suivant** :
    ```scala
    package com.example

    import org.apache.spark.sql.SparkSession

    object App {
      def main(args: Array[String]): Unit = {
        val spark = SparkSession.builder
          .appName("Scala DevOps Demo")
          .master("local[*]")
          .getOrCreate()

        val csvFile = "data/sample.csv"
        val df = spark.read.option("header", "true").csv(csvFile)

        df.show()

        spark.stop()
      }
    }
    ```

5. **Créez un fichier CSV d'exemple dans `data/sample.csv`** :
    ```csv
    name,age,city
    John Doe,30,New York
    Jane Doe,25,Los Angeles
    ```

6. **Testez l'application** :
    ```bash
    sbt run  # Compilez et exécutez l'application
    ```

### A.2. Gestion de version avec GIT
1. **Exécutez les commandes suivantes pour configurer Git** :
    ```bash
    cd C:\Users\Haythem\Desktop\ScalaDevopsDemo
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
    4. **Créez un projet `ScalaDevopsDemo`**.
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
        git remote add origin https://hrehouma0084@dev.azure.com/hrehouma0084/ScalaDevopsDemo/_git/ScalaDevopsDemo
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
    6. **Désactivez les mêmes options (`Disable creation of classic build pipelines` et `Disable creation de classic release pipelines`) en les mettant sur `off`**.

### B.2. Création de la pipeline CI (Méthode # 1 - classic editor pipeline)
1. **Créez la pipeline CI en utilisant l'outil `classic editor pipeline`** :
    1. **Allez dans `Pipelines` > `New pipeline` (Nouvelle pipeline)**.
    2. **Choisissez `Use the classic editor` (Utiliser l'éditeur classique)**.
    3. **Sélectionnez `Azure Repos Git` puis votre dépôt `ScalaDevopsDemo`**.
    4. **Choisissez `Maven` comme type de projet**.
    5. **Supprimez les composants proposés par défaut et ajoutez les composants suivants** :

#### Premier Composant (1/5)
**NATURE DE LA COMPOSANTE**: `Use Java Version`
- **Display name**: Use Java 11
- **Task Version**: `0`
- **Version Spec**: `11`
- **Add to PATH**: `true`

#### Deuxième Composant (2/5)
**NATURE DE LA COMPOSANTE**: `Use SBT Version`
- **Display name**: Use SBT 1.x
- **Task Version**: `0`
- **Version Spec**: `1.x`
- **Add to PATH**: `true`

#### Troisième Composant (3/5)
**NATURE DE LA COMPOSANTE**: `Command Line Script`
- **Display name**: Install dependencies
- **Script**: `sbt update`

#### Quatrième Composant (4/5)
**NATURE DE LA COMPOSANTE**: `Command Line Script`
- **Display name**: Run tests
- **Script**: `sbt test`

#### Cinquième Composant (5/5)
**NATURE DE LA COMPOSANTE**: `Command Line Script`
- **Display name**: Package application
- **Script**: `sbt assembly`

#### Sixième Composant (6/6)
**NATURE DE LA COMPOSANTE**: `Publish Build Artifacts`
- **Display name**: Publish Artifact: drop
- **Path to publish**: `target/scala-2.12`
- **Artifact name**: `drop`
- **Artifact publish location**: `Azure pipelines`

### TRIGGER (AUTOMATISER)
1. **Faites ce changement dans votre fichier `App.scala`** :
    ```scala
    package com.example

    import org.apache.spark.sql.SparkSession

    object App {
      def main(args: Array[String]): Unit = {
        val spark = SparkSession.builder
          .appName("Scala DevOps Demo")
          .master("local[*]")
          .getOrCreate()

        val csvFile = "data/sample.csv"
        val df = spark.read.option("header", "true").csv(csvFile)

        df.show()

        // Ajout de la nouvelle fonctionnalité
        val dfWithChange = df.withColumn("new_column", lit("Changement 1"))
        dfWithChange.show()

        spark.stop()
      }
    }
    ```

2. **Exécutez les commandes suivantes pour valider et pousser vos changements** :
    ```bash
    git status
    git add .
    git commit -m 'lancement du CI'
    git push -u origin --all
    ```

### B.3. Création de la pipeline CI (Méthode # 2 - YAML)
1. **Créez la pipeline CI en utilisant le YAML**

 :

#### Section `trigger`
- **trigger** : Cette section définit les branches qui déclencheront la pipeline. Chaque fois qu'un changement est poussé à la branche `main`, la pipeline sera exécutée automatiquement.
  ```yaml
  trigger:
  - main
  ```

#### Section `pool`
- **pool** : Cette section spécifie l'agent de build que la pipeline utilisera. Un agent est une machine sur laquelle Azure DevOps exécute vos étapes de pipeline. Ici, `vmImage: 'ubuntu-22.04'` signifie que la pipeline s'exécutera sur une machine virtuelle Ubuntu 22.04.
  ```yaml
  pool:
    vmImage: 'ubuntu-22.04'
  ```

#### Section `steps`
- **steps** : Cette section contient les différentes étapes que la pipeline exécutera. Chaque étape est une tâche (task) avec des paramètres spécifiques.

##### Étape 1 : Installer la version de Java
1. **UseJavaVersion@0** : Cette tâche installe une version spécifique de Java sur l'agent de build.
   - **versionSpec** : Spécifie la version de Java à installer, ici `11` signifie que nous installons Java 11.
   - **addToPath** : Ajoute Java au `PATH` de l'agent pour pouvoir utiliser les commandes Java directement.
   ```yaml
   - task: UseJavaVersion@0
     inputs:
       versionSpec: '11'
       addToPath: true
   ```

##### Étape 2 : Installer la version de SBT
2. **UseSbtVersion@0** : Cette tâche installe une version spécifique de SBT sur l'agent de build.
   - **versionSpec** : Spécifie la version de SBT à installer, ici `1.x` signifie que nous installons SBT 1.x.
   - **addToPath** : Ajoute SBT au `PATH` de l'agent pour pouvoir utiliser les commandes SBT directement.
   ```yaml
   - task: UseSbtVersion@0
     inputs:
       versionSpec: '1.x'
       addToPath: true
   ```

##### Étape 3 : Installer les dépendances et compiler le projet
3. **Install dependencies and compile project** : Cette tâche utilise SBT pour installer les dépendances et compiler le projet.
   - **script** : La section `script` contient les commandes shell à exécuter.
     - **sbt update** : Installe les dépendances.
     - **sbt compile** : Compile le projet.
   - **displayName** : Le nom affiché pour cette tâche, ici `Install dependencies and compile project`.
   ```yaml
   - script: |
       sbt update
       sbt compile
     displayName: 'Install dependencies and compile project'
   ```

##### Étape 4 : Exécuter les tests
4. **Run tests** : Cette tâche utilise SBT pour exécuter les tests.
   - **script** : La section `script` contient les commandes shell à exécuter.
     - **sbt test** : Exécute les tests unitaires.
   - **displayName** : Le nom affiché pour cette tâche, ici `Run tests`.
   ```yaml
   - script: |
       sbt test
     displayName: 'Run tests'
   ```

##### Étape 5 : Packager l'application
5. **Package application** : Cette tâche utilise SBT pour créer un package de distribution pour l'application.
   - **script** : La section `script` contient les commandes shell à exécuter.
     - **sbt assembly** : Crée un package JAR pour l'application.
   - **displayName** : Le nom affiché pour cette tâche, ici `Package application`.
   ```yaml
   - script: |
       sbt assembly
     displayName: 'Package application'
   ```

##### Étape 6 : Publier les artefacts de build
6. **PublishBuildArtifacts@1** : Cette tâche publie les artefacts de build.
   - **displayName** : Le nom affiché pour cette tâche, ici `Publish Artifact`.
   - **PathtoPublish** : Le chemin vers les fichiers à publier. Ici, `target/scala-2.12` signifie que les fichiers dans le répertoire `target/scala-2.12` seront publiés.
   - **ArtifactName** : Le nom de l'artefact. Ici, `drop`.
   - **publishLocation** : L'emplacement de publication. Ici, `Container` signifie que les artefacts seront publiés dans un conteneur de stockage Azure DevOps.
   ```yaml
   - task: PublishBuildArtifacts@1
     inputs:
       PathtoPublish: 'target/scala-2.12'
       ArtifactName: 'drop'
       publishLocation: 'Container'
   ```

---

### Exemple complet avec commentaires

```yaml
trigger:
- main  # Déclenche la pipeline sur les commits à la branche principale

pool:
  vmImage: 'ubuntu-22.04'  # Utilise une machine virtuelle Ubuntu 22.04 comme agent de build

steps:
- task: UseJavaVersion@0  # Installe une version spécifique de Java
  inputs:
    versionSpec: '11'  # Spécifie la version de Java à installer (11)
    addToPath: true  # Ajoute Java au PATH de l'agent

- task: UseSbtVersion@0  # Installe une version spécifique de SBT
  inputs:
    versionSpec: '1.x'  # Spécifie la version de SBT à installer (1.x)
    addToPath: true  # Ajoute SBT au PATH de l'agent

- script: |  # Tâche pour installer les dépendances et compiler le projet
    sbt update  # Installe les dépendances
    sbt compile  # Compile le projet
  displayName: 'Install dependencies and compile project'  # Nom affiché pour cette étape

- script: |  # Tâche pour exécuter les tests
    sbt test  # Exécute les tests unitaires
  displayName: 'Run tests'  # Nom affiché pour cette étape

- script: |  # Tâche pour packager l'application
    sbt assembly  # Crée un package JAR pour l'application
  displayName: 'Package application'  # Nom affiché pour cette étape

- task: PublishBuildArtifacts@1  # Tâche pour publier les artefacts de build
  displayName: 'Publish Artifact'  # Nom affiché pour cette étape
  inputs:
    PathtoPublish: 'target/scala-2.12'  # Chemin vers les fichiers à publier
    ArtifactName: 'drop'  # Nom de l'artefact
    publishLocation: 'Container'  # Emplacement de publication (Azure DevOps Container)
```

