# **Projet AWS - Concevoir et construire une application Web AWS de bout en bout à partir de zéro, étape par étape**

---

## <a href="#introduction">**1. Introduction**</a>
   - <a href="#services-que-nous-allons-utiliser">Services que nous allons utiliser</a>
   - <a href="#de-quoi-avons-nous-besoin">De quoi avons-nous besoin ?</a>
   - <a href="#plus-de-details">Plus de détails : De quoi avons-nous besoin pour créer une application web simple ?</a>

## <a href="#architecture">**2. Architecture**</a>

## <a href="#etape-1-aws-amplify">**3. Étape 1 : AWS Amplify**</a>
   - <a href="#creer-un-fichier-html">3.1. Créer un fichier HTML</a>
     - <a href="#creer-un-fichier-texte-simple">3.1.1. Créer un fichier texte simple</a>
     - <a href="#renommer-le-fichier">3.1.2. Renommer le fichier texte en fichier HTML (index.html)</a>
     - <a href="#ouvrir-le-fichier">3.1.3. Ouvrir le fichier avec Notepad++</a>
     - <a href="#ajouter-le-code-html">3.1.4. Ajouter le code de la page HTML</a>
     - <a href="#compresser-le-fichier">3.1.5. Compresser le fichier en ZIP</a>
   - <a href="#deployer-le-site">3.2. Déployer le site dans AWS Amplify</a>
     - <a href="#chercher-le-service-amplify">3.2.1. Chercher le service AWS Amplify</a>
     - <a href="#demarrer-le-service">3.2.2. Démarrer le service AWS Amplify</a>
     - <a href="#deployer-sans-git">3.2.3. Déployer sans Git provider ou référentiel Git</a>
     - <a href="#drag-and-drop">3.2.4. Effectuer un Drag and Drop</a>
     - <a href="#sauvegarder-et-deployer">3.2.5. Sauvegarder et déployer</a>
     - <a href="#ouvrir-le-lien-du-domaine">3.2.6. Ouvrir le lien du Domaine sur votre navigateur</a>
     - <a href="#observer-la-page-html">3.2.7. Observer votre page HTML</a>

## <a href="#etape-2-aws-lambda">**4. Étape 2 : AWS Lambda**</a>
   - <a href="#ouvrir-le-service-lambda">4.1. Ouvrir le service AWS Lambda</a>
   - <a href="#creer-une-fonction-lambda">4.2. Créer une fonction Lambda "PowerOfMathFunction"</a>
   - <a href="#copier-et-coller-le-code">4.3. Copier et coller le code Python</a>
   - <a href="#sauvegarder-la-fonction">4.4. Sauvegarder</a>
   - <a href="#deployer-la-fonction">4.5. Déployer</a>
   - <a href="#configurer-un-evenement-test">4.6. Configurer un événement de test</a>
   - <a href="#finaliser-et-coller-le-code">4.7. Finaliser l'événement de test et copier/coller le code</a>
   - <a href="#tester-la-fonction">4.8. Tester</a>

## <a href="#etape-3-amazon-api-gateway">**5. Étape 3 : Amazon API Gateway**</a>

## <a href="#etape-4-amazon-dynamodb">**6. Étape 4 : Amazon DynamoDB**</a>

## <a href="#etape-5-aws-iam">**7. Étape 5 : AWS Gestion des identités et des accès (IAM)**</a>

## <a href="#etape-6-retour-amplify">**8. Étape 6 : AWS Amplify**</a>



# **Projet AWS - Concevoir et construire une application Web AWS de bout en bout à partir de zéro, étape par étape**

---

## [**1. Introduction**](#introduction)
   - [Services que nous allons utiliser](#services)
   - [De quoi avons-nous besoin ?](#besoin)
   - [Plus de détails : De quoi avons-nous besoin pour créer une application web simple ?](#details)

## [**2. Architecture**](#architecture)

## [**3. Étape 1 : AWS Amplify**](#etape1)
   - [3.1. Créer un fichier HTML](#fichier-html)
     - [3.1.1. Créer un fichier texte simple](#fichier-texte-simple)
     - [3.1.2. Renommer le fichier texte en fichier HTML (index.html)](#renommer-fichier)
     - [3.1.3. Ouvrir le fichier avec Notepad++](#ouvrir-notepad)
     - [3.1.4. Ajouter le code de la page HTML](#ajouter-code-html)
     - [3.1.5. Compresser le fichier en ZIP](#compresser-fichier)
   - [3.2. Déployer le site dans AWS Amplify](#deployer-site-amplify)
     - [3.2.1. Chercher le service AWS Amplify](#chercher-service)
     - [3.2.2. Démarrer le service AWS Amplify](#demarrer-service)
     - [3.2.3. Déployer sans Git provider ou référentiel Git](#deployer-sans-git)
     - [3.2.4. Effectuer un Drag and Drop](#drag-and-drop)
     - [3.2.5. Sauvegarder et déployer](#sauvegarder-deployer)
     - [3.2.6. Ouvrir le lien du Domaine sur votre navigateur](#ouvrir-lien)
     - [3.2.7. Observer votre page HTML](#observer-page-html)

## [**4. Étape 2 : AWS Lambda**](#etape2)
   - [4.1. Ouvrir le service AWS Lambda](#ouvrir-lambda)
   - [4.2. Créer une fonction Lambda "PowerOfMathFunction"](#creer-fonction-lambda)
   - [4.3. Copier et coller le code Python](#copier-code-python)
   - [4.4. Sauvegarder](#sauvegarder)
   - [4.5. Déployer](#deployer)
   - [4.6. Configurer un événement de test](#configurer-test)
   - [4.7. Finaliser l'événement de test et copier/coller le code](#finaliser-coller-code)
   - [4.8. Tester](#tester)

## [**5. Étape 3 : Amazon API Gateway**](#etape3)

## [**6. Étape 4 : Amazon DynamoDB**](#etape4)

## [**7. Étape 5 : AWS Gestion des identités et des accès (IAM)**](#etape5)

## [**8. Étape 6 : AWS Amplify**](#etape6)

---





---
# Introduction: 
---

**Services que nous allons utiliser**

1. AWS Amplify
2. AWS Lambda
3. Amazon API Gateway
4. Amazon DynamoDB
5. AWS Gestion des identités et des accès (IAM)

![image](https://github.com/user-attachments/assets/c5d587dc-9a57-4ff7-acb2-a278150d397b)


**De quoi avons-nous besoin ?**

1. Une solution pour créer/héberger une page Web (AWS Amplify)
2. Un moyen d'invoquer la fonctionnalité mathématique (AWS Lambda)
3. Un moyen de faire des calculs (Amazon API Gateway)
4. Un endroit pour stocker/renvoyer le résultat des calculs (DynamoDB)
5. Une manière de gérer les permissions (IAM)

**plus de détails : De quoi avons-nous besoin pour créer une application web simple ?**

1. **Créer et héberger une page Web (AWS Amplify)** : On a besoin d'un endroit pour construire et mettre en ligne notre site web, afin que tout le monde puisse y accéder.

2. **Appeler les fonctions mathématiques (AWS Lambda)** : On a besoin d'un service qui permet de lancer des calculs ou des opérations mathématiques quand on en a besoin, comme une calculatrice automatisée.

3. **Faire les calculs (Amazon API Gateway)** : On a besoin d'un moyen pour que notre site web puisse demander à la calculatrice de faire les calculs et obtenir les résultats.

4. **Stocker et récupérer les résultats (DynamoDB)** : On a besoin d'un endroit où sauvegarder les résultats des calculs pour pouvoir les récupérer plus tard si nécessaire.

5. **IAM pour insérer dans la base de données DynamoDB**, **Gérer les permissions (IAM)** : On a besoin d'une manière de dire qui a le droit de faire quoi avec notre base de données. Par exemple, on peut utiliser IAM pour donner à certaines personnes ou services l'autorisation d'ajouter ou de modifier des données dans notre base de données DynamoDB. C'est un peu comme donner une clé spéciale à quelqu'un pour qu'il puisse entrer dans une pièce et y déposer ou y changer quelque chose, mais sans lui donner accès à toute la maison.

# Architecture 

![image](https://github.com/user-attachments/assets/adbeb35f-d3d8-4989-8beb-009ea55b937b)

### <a href="#introduction">Revenir en haut</a>
---
---
---
# Étape 1. AWS Amplify
---
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇
## 1.1. Créer un fichier html
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇

## 1.1.1. Créer un fichier texte simple
![image](https://github.com/user-attachments/assets/e880d685-f20f-4a7c-9ac3-e71e230e2258)

## 1.1.2. Renommer le fichier texte en fichier html (index.html)
![image](https://github.com/user-attachments/assets/71d91bef-a0b7-4fc4-ad93-105273b2b493)

## 1.1.3.  Ouvrir le fichier avec notepad++
![image](https://github.com/user-attachments/assets/6d7e6a67-adc7-4078-830d-9ec93b63e750)

## 1.1.4.  Ajoutez le code de la page html suivant
![image](https://github.com/user-attachments/assets/142c554c-d265-4432-9532-df9fca7637af)

### Ce code crée une page web simple avec le texte "To the Power of Math!" affiché dans le titre de la page et également dans le corps du document.

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>To the Power of Math!</title>
</head>
<body>
    To the Power of Math!
</body>
</html>
```

## 1.1.5.  Compressez dans un fichier zip
![image](https://github.com/user-attachments/assets/3303a295-1683-40a3-a3f5-ca0173a73b4b)

🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇
## 1.2. Déployez le site dans AWS Amplify
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇

## 1.2.1. Cherchez le service AWS Amplify
![image](https://github.com/user-attachments/assets/79e1cc86-757a-41aa-b3d8-2867893890fc)
## 1.2.2. Démarrer le service AWS Amplify
![image](https://github.com/user-attachments/assets/d91891d6-2a4e-41b6-97a8-f4c6b02b44be)
![image](https://github.com/user-attachments/assets/51f5da10-e953-4b97-99a1-fb2898c5ed3d)
## 1.2.3. Déployez sans un Git provider ou référentiel Git
![image](https://github.com/user-attachments/assets/9129ed56-e54b-4a7d-9d1f-8d3d8411d0f9)
## 1.2.4. Effectuer un Drag and Drop 
![image](https://github.com/user-attachments/assets/593a3fab-68db-44ed-a49f-c52b8aaaf12b)
## 1.2.5. Sauvegarder et déployer
![image](https://github.com/user-attachments/assets/b6209ec0-0184-467b-9d87-36f3c4c12632)
## 1.2.6. Ouvrir le lien du Domaine sur votre navigateur 
![image](https://github.com/user-attachments/assets/577741fa-7613-4e82-8274-6a7357c59064)

## 1.2.7. Observez votre page html
![image](https://github.com/user-attachments/assets/39ed933e-7b19-4e51-9122-1b2e274a7e6a)

### <a href="#introduction">Revenir en haut</a>
---
---
---
# Étape 2. AWS Lambda
---

## 2.1. Ouvrir le service AWS Lambda
![image](https://github.com/user-attachments/assets/a198d7d2-a5d0-4280-ac17-77aab4664ea5)
## 2.2. Créez une fonction Lambda PowerOfMathFunction
![image](https://github.com/user-attachments/assets/026c6927-61e1-4e9d-88cf-0efedc94c3bf)
## 2.3. Copiez et collez le code python
![image](https://github.com/user-attachments/assets/2636717f-f2a0-4b5d-a9fd-08f45f7d36ef)

## Copiez le code suivant 

```python
# import the JSON utility package
import json
# import the Python math library
import math

# define the handler function that the Lambda service will use as an entry point
def lambda_handler(event, context):

    # extract the two numbers from the Lambda service's event object
    mathResult = math.pow(int(event['base']), int(event['exponent']))

    # return a properly formatted JSON object
    return {
        'statusCode': 200,
        'body': json.dumps('Your result is ' + str(mathResult))
    }
```

### Ce code est destiné à être exécuté dans un environnement AWS Lambda. Lorsqu'il est appelé, il effectue un calcul de puissance basé sur les valeurs fournies dans l'objet `event`, puis renvoie le résultat sous forme de réponse JSON.

## 2.4. Sauvegardez
![image](https://github.com/user-attachments/assets/c4e92397-5525-4d3f-b2d4-28dd499b2ff6)
## 2.5. Déployez
![image](https://github.com/user-attachments/assets/154c4e46-f3db-4f03-8a90-146fe7c08e26)

## 2.6. Configurez un événement de Test
![image](https://github.com/user-attachments/assets/0ee5ab11-9bad-4be6-8f06-ead1e148a38d)

![image](https://github.com/user-attachments/assets/2aa8539a-717f-448c-901b-3beca153d842)
## 2.7. Finalisez l'événement de Test et copier coller le code
![image](https://github.com/user-attachments/assets/3f361ece-8920-4aee-b3a2-d5860c00b4c7)

```json
{
    "base": 2,
    "exponent": 3
}
```

## 2.9. Testez
![image](https://github.com/user-attachments/assets/a37028ac-68a6-4abf-ba78-340ff582bb9a)

### <a href="#introduction">Revenir en haut</a>
---
---
---
# Étape 3. Amazon API Gateway
---




### <a href="#introduction">Revenir en haut</a>

---
---
---
# Étape 4. Amazon DynamoDB
---

### <a href="#introduction">Revenir en haut</a>
---
---
---
---
# Étape 5. AWS Gestion des identités et des accès (IAM)
---

### <a href="#introduction">Revenir en haut</a>
---
---
---
# Étape 6. AWS Amplify
---

### <a href="#introduction">Revenir en haut</a>




<a name="introduction"></a>
# Introduction

**Services que nous allons utiliser**  
... contenu ...

<a name="services"></a>
### Services que nous allons utiliser
... contenu ...

<a name="besoin"></a>
### De quoi avons-nous besoin ?
... contenu ...

<a name="details"></a>
### Plus de détails : De quoi avons-nous besoin pour créer une application web simple ?
... contenu ...

<a name="architecture"></a>
# Architecture
... contenu ...

<a name="etape1"></a>
# Étape 1 : AWS Amplify

<a name="fichier-html"></a>
## 1.1. Créer un fichier HTML
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="fichier-texte-simple"></a>
### 1.1.1. Créer un fichier texte simple
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="renommer-fichier"></a>
### 1.1.2. Renommer le fichier texte en fichier HTML (index.html)
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="ouvrir-notepad"></a>
### 1.1.3. Ouvrir le fichier avec Notepad++
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="ajouter-code-html"></a>
### 1.1.4. Ajouter le code de la page HTML
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="compresser-fichier"></a>
### 1.1.5. Compresser le fichier en ZIP
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="deployer-site-amplify"></a>
## 1.2. Déployer le site dans AWS Amplify
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="chercher-service"></a>
### 1.2.1. Chercher le service AWS Amplify
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="demarrer-service"></a>
### 1.2.2. Démarrer le service AWS Amplify
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="deployer-sans-git"></a>
### 1.2.3. Déployer sans Git provider ou référentiel Git
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="drag-and-drop"></a>
### 1.2.4. Effectuer un Drag and Drop
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="sauvegarder-deployer"></a>
### 1.2.5. Sauvegarder et déployer
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="ouvrir-lien"></a>
### 1.2.6. Ouvrir le lien du Domaine sur votre navigateur
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="observer-page-html"></a>
### 1.2.7. Observer votre page HTML
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="etape2"></a>
# Étape 2 : AWS Lambda
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="ouvrir-lambda"></a>
## 2.1. Ouvrir le service AWS Lambda
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="creer-fonction-lambda"></a>
## 2.2. Créer une fonction Lambda "PowerOfMathFunction"
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="copier-code-python"></a>
## 2.3. Copier et coller le code Python
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="sauvegarder"></a>
## 2.4. Sauvegarder
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="deployer"></a>
## 2.5. Déployer
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="configurer-test"></a>
## 2.6. Configurer un événement de test
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="finaliser-coller-code"></a>
## 2.7. Finaliser l'événement de test et copier/coller le code
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="tester"></a>
## 2.8. Tester
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="etape3"></a>
# Étape 3 : Amazon API Gateway
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="etape4"></a>
# Étape 4 : Amazon DynamoDB
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="etape5"></a>
# Étape 5 : AWS Gestion des identités et des accès (IAM)
... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="etape6"></a>
# Étape 6 : AWS Amplify
... contenu ...
### <a href="#introduction">Revenir en haut</a>
