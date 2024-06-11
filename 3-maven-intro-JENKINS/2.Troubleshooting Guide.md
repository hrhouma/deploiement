# Troubleshooting Guide
### Problèmes de version de Java

Si vous utilisez une autre version de Java, vous devrez peut-être ajuster certaines parties de la configuration du projet pour qu'elles soient compatibles. Voici comment procéder :

1. **Mise à jour de la version Java dans le fichier `pom.xml` :**

   Ouvrez le fichier `pom.xml` et modifiez les propriétés de la version du compilateur Java pour qu'elles correspondent à la version installée sur votre machine. Par exemple, pour Java 11 :

   ```xml
   <properties>
       <maven.compiler.source>11</maven.compiler.source>
       <maven.compiler.target>11</maven.compiler.target>
   </properties>
   ```

2. **Vérification de la version de Java installée :**

   Utilisez la commande suivante pour vérifier la version de Java installée sur votre machine :

   ```bash
   java -version
   ```

3. **Changer de version de Java (si nécessaire) :**

   Si vous devez changer de version de Java, vous pouvez utiliser un gestionnaire de version Java comme SDKMAN. Par exemple, pour installer et utiliser Java 11 :

   ```bash
   sdk install java 11.0.11.hs-adpt
   sdk use java 11.0.11.hs-adpt
   ```
4. **Changer ordre dans le path si vous disposez de plusieurs versions (si nécessaire) :**
- Faire monter la version de java désirée et ensuite tester avec java --version
   
### Installation de Maven sur Ubuntu

Pour les utilisateurs d'Ubuntu, vous pouvez suivre les instructions détaillées dans ce [lien](https://phoenixnap.com/kb/install-maven-on-ubuntu) pour installer Maven.

- https://phoenixnap.com/kb/install-maven-on-ubuntu

# sinon
1. **Mise à jour des référentiels de paquets :**

   ```bash
   sudo apt update
   ```

2. **Installation de Maven :**

   ```bash
   sudo apt install maven
   ```

3. **Vérification de l'installation :**

   ```bash
   mvn -version
   ```

### Instructions supplémentaires et ressources pour installer JAVA et MAVEN 

Pour plus de détails et d'instructions supplémentaires, veuillez consulter ce document [Google Docs](https://docs.google.com/document/d/1IsFOXjifo4NSJlBN98T1fGzEIuoAQ-VPaxtPt8gzrzU/edit?usp=drive_link).
- https://phoenixnap.com/kb/install-maven-on-ubuntu
- https://docs.google.com/document/d/1IsFOXjifo4NSJlBN98T1fGzEIuoAQ-VPaxtPt8gzrzU/edit?usp=drive_link
- https://blog.devops.dev/java-base-application-build-with-maven-on-jenkins-540cad37370f (which java)
  

