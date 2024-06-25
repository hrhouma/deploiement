### Tutoriel Complet : Création d'un Projet Maven avec Jenkins

---

#### Étape 1 : Créer le projet Maven

1. **Utilisation de Maven Archetype pour générer la structure du projet**

   Ouvrez votre terminal et exécutez la commande suivante pour créer automatiquement la structure du projet avec Maven :

   ```bash
   mvn archetype:generate -DgroupId=com.example -DartifactId=calculator -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

   - `-DgroupId` : Définit l'identifiant de groupe de votre projet, généralement l'organisation ou l'espace de nommage.
   - `-DartifactId` : Est le nom de votre projet, qui deviendra aussi le nom du dossier de base.
   - `-DarchetypeArtifactId` : Spécifie l'archétype Maven à utiliser, `maven-archetype-quickstart` est un archétype de base pour les applications Java.
   - `-DinteractiveMode=false` : Exécute la commande sans mode interactif pour éviter les invites de confirmation supplémentaires.

#### Étape 2 : Ajouter le code source

1. **Calculator.java**

   Remplacez le contenu de `src/main/java/com/example/App.java` par :

   ```java
   package com.example;

   public class Calculator {
       public int add(int a, int b) {
           return a + b;
       }

       public int subtract(int a, int b) {
           return a - b;
       }

       public int multiply(int a, int b) {
           return a * b;
       }

       public double divide(int a, int b) {
           if (b == 0) {
               throw new IllegalArgumentException("Division by zero.");
           }
           return (double) a / b;
       }
   }
   ```

2. **CalculatorTest.java**

   Remplacez le contenu de `src/test/java/com/example/AppTest.java` par :

   ```java
   package com.example;

   import org.junit.Assert;
   import org.junit.Test;

   public class CalculatorTest {
       private Calculator calculator = new Calculator();

       @Test
       public void testAdd() {
           Assert.assertEquals(5, calculator.add(2, 3));
       }

       @Test
       public void testSubtract() {
           Assert.assertEquals(1, calculator.subtract(3, 2));
       }

       @Test
       public void testMultiply() {
           Assert.assertEquals(6, calculator.multiply(2, 3));
       }

       @Test
       public void testDivide() {
           Assert.assertEquals(2.0, calculator.divide(4, 2), 0);
       }

       @Test(expected = IllegalArgumentException.class)
       public void testDivideByZero() {
           calculator.divide(1, 0);
       }
   }
   ```

3. **pom.xml**

   Assurez-vous que votre `pom.xml` contient la configuration suivante :

   ```xml
   <project xmlns="http://maven.apache.org/POM/4.0.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://www.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>

       <groupId>com.example</groupId>
       <artifactId>calculator</artifactId>
       <version>1.0-SNAPSHOT</version>

       <properties>
           <maven.compiler.source>1.8</maven.compiler.source>
           <maven.compiler.target>1.8</maven.compiler.target>
       </properties>

       <dependencies>
           <!-- JUnit dependency -->
           <dependency>
               <groupId>junit</groupId>
               <artifactId>junit</artifactId>
               <version>4.12</version>
               <scope>test</scope>
           </dependency>
       </dependencies>
   </project>
   ```

#### Étape 3 : Pousser le projet vers GitHub

1. **Initialiser le repository Git et pousser le projet vers GitHub**

   ```bash
   cd calculator
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <your-repository-url>
   git push -u origin master
   ```

#### Étape 4 : Créer le Jenkinsfile

1. **Jenkinsfile**

   À la racine de votre projet, créez un fichier nommé `Jenkinsfile` et ajoutez le contenu suivant :

   ```groovy
   pipeline {
       agent any
       environment {
           JAVA_HOME = 'C:\\Program Files\\Java\\jdk1.8.0_202'
           PYTHON_HOME = 'C:\\Users\\rehou\\AppData\\Local\\Microsoft\\WindowsApps'
           MAVEN_HOME = 'C:\\Users\\Haythem\\Documents\\apache-maven-3.9.0\\bin'
           PATH = "${env.PATH};${JAVA_HOME}\\bin;${PYTHON_HOME};${MAVEN_HOME}"
       }
       stages {
           stage('Checkout') {
               steps {
                   // Cloner le repository depuis GitHub
                   git branch: 'main', url: 'https://github.com/hrhouma/hello-jenkins-mvn.git'
               }
           }

           stage('Build') {
               steps {
                   // Nettoyer et compiler le projet avec Maven
                   sh 'mvn clean compile'
               }
           }

           stage('Test') {
               steps {
                   // Exécuter les tests unitaires
                   sh 'mvn test'
               }
           }

           stage('Package') {
               steps {
                   // Packager le projet en JAR
                   sh 'mvn package'
               }
           }

           stage('Archive Artifacts') {
               steps {
                   // Archiver les artefacts générés (JAR)
                   archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
               }
           }
       }

       post {
           always {
               // Publier les résultats des tests, si disponibles
               junit '**/target/surefire-reports/*.xml'
           }
       }
   }
   ```

2. **Pousser le Jenkinsfile dans le repository GitHub**

   ```bash
   cd calculator
   git add Jenkinsfile
   git commit -m "Add Jenkinsfile with environment variables"
   git push origin master
   ```

#### Étape 5 : Configurer Jenkins

1. **Configurer un nouveau job Jenkins**
   - Ouvrez votre instance Jenkins et créez un nouveau job de type "Pipeline".
   - Donnez un nom à votre job et sélectionnez "Pipeline", puis cliquez sur "OK".
   - Dans la configuration du job, dans la section "Pipeline", sélectionnez "Pipeline script from SCM".
   - Dans "SCM", choisissez "Git" et entrez l'URL de votre repository GitHub.
   - Spécifiez la branche (`main`) et le chemin du Jenkinsfile (`Jenkinsfile`).

2. **Exécuter le job**
   - Sauvegardez votre job et exécutez-le. Jenkins va cloner le repository, exécuter les étapes définies dans le Jenkinsfile (checkout, build, test, package), et archiver les artefacts générés.

Avec ces étapes, votre pipeline Jenkins est configuré pour construire et tester votre projet Maven en utilisant les environnements Java et Python spécifiés.
