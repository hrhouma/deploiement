# Partie 1 : Pratique 3 – Jenkins + Maven (1/3)
## Introduction à MAVEN - Projet de calculatrice

- Ce projet démontre l'utilisation de Maven pour gérer le cycle de vie du développement d'une application calculatrice simple en Java.

## Prérequis

- Java JDK 1.8 ou supérieur
- Maven 3.6.3 ou supérieur

### Installation de Java

1. Téléchargez le JDK depuis [Oracle](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) ou utilisez un package manager comme `sdkman` pour l'installer :

```bash
sdk install java 11.0.11.hs-adpt
```

2. Vérifiez l'installation en exécutant :

```bash
java -version
```

### Installation de Maven

1. Téléchargez Maven depuis [Apache Maven](https://maven.apache.org/download.cgi).
2. Extrayez l'archive téléchargée et configurez la variable d'environnement `MAVEN_HOME` pointant vers le répertoire d'installation de Maven.
3. Ajoutez le répertoire `bin` de Maven au `PATH`.

Pour vérifier l'installation de Maven :

```bash
mvn -version
```

## Structure du projet

Voici la structure de dossiers du projet :

```
CalculatorProject/
|-- pom.xml
|-- src/
    |-- main/
    |   |-- java/
    |   |   |-- com/
    |   |       |-- example/
    |   |           |-- Calculator.java
    |-- test/
        |-- java/
            |-- com/
                |-- example/
                    |-- CalculatorTest.java
```

## Création de la structure du projet

### Commandes Maven couramment utilisées

Voici un ensemble de commandes Maven couramment utilisées. Ces commandes sont exécutées dans le terminal ou l'invite de commande (cmd) à la racine du projet, où se trouve le fichier pom.xml.

- Créer un projet Maven avec un archétype : `mvn archetype:generate`
- Compiler le projet : `mvn compile`
- Exécuter les tests unitaires : `mvn test`
- Construire le projet : `mvn package`
- Vérifier le projet : `mvn verify`
- Installer le projet : `mvn install`
- Déployer le projet : `mvn deploy`
- Nettoyer le projet : `mvn clean`
- Générer un site pour le projet : `mvn site`
- Analyser les dépendances : `mvn dependency:analyze`
- Mettre à jour les snapshots des dépendances : `mvn dependency:update-snapshots`

### Création manuelle du projet

Pour créer manuellement la structure de dossiers, suivez ces étapes :

1. Créer la structure de dossiers :

```bash
mkdir -p CalculatorProject/src/main/java/com/example
mkdir -p CalculatorProject/src/test/java/com/example
```

2. Créer les fichiers nécessaires :
   - Utilisez un éditeur de texte pour créer `Calculator.java` et `CalculatorTest.java` dans leurs dossiers respectifs.
   - Créez également le fichier `pom.xml` à la racine du projet (`CalculatorProject/`).

### Création automatique du projet - Utilisation de Maven Archetype

Maven propose un moyen plus rapide de générer une structure de projet de base grâce à la commande `archetype:generate`. Voici comment utiliser cette commande :

1. Ouvrez votre terminal ou invite de commande.
2. Naviguez vers le dossier où vous souhaitez créer votre projet.
3. Exécutez la commande Maven Archetype :

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=calculator -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

- `-DgroupId` définit l'identifiant de groupe de votre projet, généralement l'organisation ou l'espace de nommage.
- `-DartifactId` est le nom de votre projet, qui deviendra aussi le nom du dossier de base.
- `-DarchetypeArtifactId` spécifie l'archétype Maven à utiliser, `maven-archetype-quickstart` est un archétype de base pour les applications Java.
- `-DinteractiveMode=false` exécute la commande sans mode interactif pour éviter les invites de confirmation supplémentaires.

Après l'exécution, Maven créera un projet dans un dossier appelé `calculator` avec la structure souhaitée. Vous devrez peut-être ajuster les noms des packages et les contenus des fichiers `Calculator.java` et `CalculatorTest.java` pour correspondre à ceux fournis précédemment.

L'utilisation de l'archétype Maven est la manière la plus rapide et la plus conforme aux standards pour générer la structure d'un projet Java. Cela vous permet non seulement de gagner du temps mais aussi d'assurer que la structure du projet suit les conventions Maven, facilitant la maintenance et la compréhension pour les nouveaux développeurs.

## Création des fichiers de base

### Calculator.java

Créez le fichier `Calculator.java` dans le répertoire `src/main/java/com/example/` :

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

### CalculatorTest.java

Créez le fichier `CalculatorTest.java` dans le répertoire `src/test/java/com/example/` :

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

### pom.xml

Fichier `pom.xml` qui configure notre projet pour utiliser JUnit 4.12 pour les tests :

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

## Exécution des commandes Maven

Vous pouvez exécuter les commandes Maven mentionnées précédemment dans le terminal ou CMD à la racine du projet (CalculatorProject), là où se trouve le fichier `pom.xml`.

- Compiler le projet : `mvn compile`
- Exécuter les tests unitaires : `mvn test`
- Construire le projet (incluant les tests) : `mvn package`
- Nettoyer le projet : `mvn clean`
- Installer le projet dans le référentiel local Maven : `mvn install`
- Générer un site pour le projet : `mvn site`

Ce guide fournit les informations nécessaires pour créer et gérer le cycle de vie du projet Maven pour la calculatrice. La prochaine partie se concentrera sur l'intégration avec Jenkins pour automatiser le processus de build et de test.
