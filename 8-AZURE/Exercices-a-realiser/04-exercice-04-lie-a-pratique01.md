# Scala DevOpsDemo Project Setup and Deployment using Maven

## LIENS:
- https://aex.dev.azure.com/me?mkt=fr-FR
- https://portal.azure.com/

## PARTIE # A – Création et déploiement manuel du projet

### A.1. Configuration du projet
1. **Installez Java JDK 11+ et Maven** : Assurez-vous d'avoir installé Java Development Kit (JDK) version 11 ou supérieure et Maven.
2. **Ouvrez une console et exécutez les commandes suivantes** :
    ```bash
    cd C:\Users\Haythem\Desktop
    java -version  # Vérifiez que Java est installé
    mvn -version  # Vérifiez que Maven est installé
    mkdir ScalaDevopsDemo  # Créez un répertoire pour le projet
    cd ScalaDevopsDemo
    mvn archetype:generate -DgroupId=com.example -DartifactId=scala-devops-demo -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    cd scala-devops-demo
    ```

3. **Modifiez le fichier `pom.xml` pour inclure les dépendances Scala et Apache Spark** :
    ```xml
    <project xmlns="http://maven.apache.org/POM/4.0.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
        <groupId>com.example</groupId>
        <artifactId>scala-devops-demo</artifactId>
        <version>1.0-SNAPSHOT</version>

        <properties>
            <scala.version>2.12.10</scala.version>
            <maven.compiler.source>11</maven.compiler.source>
            <maven.compiler.target>11</maven.compiler.target>
        </properties>

        <dependencies>
            <dependency>
                <groupId>org.scala-lang</groupId>
                <artifactId>scala-library</artifactId>
                <version>${scala.version}</version>
            </dependency>
            <dependency>
                <groupId>org.apache.spark</groupId>
                <artifactId>spark-core_2.12</artifactId>
                <version>3.1.1</version>
            </dependency>
            <dependency>
                <groupId>org.apache.spark</groupId>
                <artifactId>spark-sql_2.12</artifactId>
                <version>3.1.1</version>
            </dependency>
        </dependencies>

        <build>
            <plugins>
                <plugin>
                    <groupId>net.alchim31.maven</groupId>
                    <artifactId>scala-maven-plugin</artifactId>
                    <version>4.5.3</version>
                    <executions>
                        <execution>
                            <goals>
                                <goal>compile</goal>
                                <goal>testCompile</goal>
                            </goals>
                        </execution>
                    </executions>
                </plugin>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.8.1</version>
                    <configuration>
                        <source>11</source>
                        <target>11</target>
                    </configuration>
                </plugin>
            </plugins>
        </build>
    </project>
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
    mvn clean compile exec:java -Dexec.mainClass="com.example.App"  # Compilez et exécutez l'application
    ```

### A.2. Gestion de version avec GIT
1. **Exécutez les commandes suivantes pour configurer Git** :
    ```bash
    cd C:\Users\Haythem\Desktop\ScalaDevopsDemo\scala-devops-demo
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

#### Premier Composant (1/4)
**NATURE DE LA COMPOSANTE**: `Use Java Version`
- **Display name**: Use Java 11
- **Task Version**: `0`
- **Version Spec**: `11`
- **Add to PATH**: `true`

#### Deuxième Composant (2/4)
**NATURE DE LA COMPOSANTE**: `Maven`
- **Display name**: Install dependencies
- **Goals**: `clean install`

#### Troisième Composant (3/4)
**NATURE DE LA COMPOSANTE**: `M

aven`
- **Display name**: Run tests
- **Goals**: `test`

#### Quatrième Composant (4/4)
**NATURE DE LA COMPOSANTE**: `Maven`
- **Display name**: Package application
- **Goals**: `package`

#### Cinquième Composant (5/5)
**NATURE DE LA COMPOSANTE**: `Publish Build Artifacts`
- **Display name**: Publish Artifact: drop
- **Path to publish**: `target`
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
1. **Créez la pipeline CI en utilisant le YAML** :

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

##### Étape 2 : Installer les dépendances et compiler le projet
2. **Install dependencies and compile project** : Cette tâche utilise Maven pour installer les dépendances et compiler le projet.
   - **script** : La section `script` contient les commandes shell à exécuter.
     - **mvn clean install** : Installe les dépendances et compile le projet.
   - **displayName** : Le nom affiché pour cette tâche, ici `Install dependencies and compile project`.
   ```yaml
   - script: |
       mvn clean install
     displayName: 'Install dependencies and compile project'
   ```

##### Étape 3 : Exécuter les tests
3. **Run tests** : Cette tâche utilise Maven pour exécuter les tests.
   - **script** : La section `script` contient les commandes shell à exécuter.
     - **mvn test** : Exécute les tests unitaires.
   - **displayName** : Le nom affiché pour cette tâche, ici `Run tests`.
   ```yaml
   - script: |
       mvn test
     displayName: 'Run tests'
   ```

##### Étape 4 : Packager l'application
4. **Package application** : Cette tâche utilise Maven pour créer un package de distribution pour l'application.
   - **script** : La section `script` contient les commandes shell à exécuter.
     - **mvn package** : Crée un package JAR pour l'application.
   - **displayName** : Le nom affiché pour cette tâche, ici `Package application`.
   ```yaml
   - script: |
       mvn package
     displayName: 'Package application'
   ```

##### Étape 5 : Publier les artefacts de build
5. **PublishBuildArtifacts@1** : Cette tâche publie les artefacts de build.
   - **displayName** : Le nom affiché pour cette tâche, ici `Publish Artifact`.
   - **PathtoPublish** : Le chemin vers les fichiers à publier. Ici, `target` signifie que les fichiers dans le répertoire `target` seront publiés.
   - **ArtifactName** : Le nom de l'artefact. Ici, `drop`.
   - **publishLocation** : L'emplacement de publication. Ici, `Container` signifie que les artefacts seront publiés dans un conteneur de stockage Azure DevOps.
   ```yaml
   - task: PublishBuildArtifacts@1
     inputs:
       PathtoPublish: 'target'
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

- script: |  # Tâche pour installer les dépendances et compiler le projet
    mvn clean install  # Installe les dépendances et compile le projet
  displayName: 'Install dependencies and compile project'  # Nom affiché pour cette étape

- script: |  # Tâche pour exécuter les tests
    mvn test  # Exécute les tests unitaires
  displayName: 'Run tests'  # Nom affiché pour cette étape

- script: |  # Tâche pour packager l'application
    mvn package  # Crée un package JAR pour l'application
  displayName: 'Package application'  # Nom affiché pour cette étape

- task: PublishBuildArtifacts@1  # Tâche pour publier les artefacts de build
  displayName: 'Publish Artifact'  # Nom affiché pour cette étape
  inputs:
    PathtoPublish: 'target'  # Chemin vers les fichiers à publier
    ArtifactName: 'drop'  # Nom de l'artefact
    publishLocation: 'Container'  # Emplacement de publication (Azure DevOps Container)
```
