# **Projet AWS - Concevoir et construire une application Web AWS de bout en bout à partir de zéro, étape par étape**

# Référence : https://www.youtube.com/watch?v=7m_q1ldzw0U
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
# Étape 2 : AWS Lambda


### <a href="#introduction">Revenir en haut</a>
<a name="ouvrir-lambda"></a>
## 2.1. Ouvrir le service AWS Lambda
![image](https://github.com/user-attachments/assets/a198d7d2-a5d0-4280-ac17-77aab4664ea5)
### <a href="#introduction">Revenir en haut</a>
<a name="creer-fonction-lambda"></a>
## 2.2. Créer une fonction Lambda "PowerOfMathFunction"
![image](https://github.com/user-attachments/assets/026c6927-61e1-4e9d-88cf-0efedc94c3bf)
### <a href="#introduction">Revenir en haut</a>
<a name="copier-code-python"></a>
## 2.3. Copier et coller le code Python
![image](https://github.com/user-attachments/assets/2636717f-f2a0-4b5d-a9fd-08f45f7d36ef)
### <a href="#introduction">Revenir en haut</a>
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
<a name="sauvegarder"></a>
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

# Étape 3 : Amazon API Gateway

# Cherchez API Gateway
![image](https://github.com/user-attachments/assets/2a8baacf-c72f-4145-ac5f-dc0ae4d94033)
# Créez une API REST
![image](https://github.com/user-attachments/assets/0c9f18c6-d2ba-459b-b02d-5b62f4bbf4ab)
# Paramétrez votre API REST
![image](https://github.com/user-attachments/assets/500e46e6-d8c9-44e2-8d73-2cbb73857f88)

# Créez une méthode
![image](https://github.com/user-attachments/assets/030ec3f2-a32e-46ae-b6af-0cc57c8b7097)
# Choisir POST
![image](https://github.com/user-attachments/assets/df671362-ea46-4ce2-9988-5057b30a4434)
# Configurez POST
![image](https://github.com/user-attachments/assets/3403524c-0300-4c37-84d8-1df686f64790)
# Enregistrez la configuration de Cors
![image](https://github.com/user-attachments/assets/f1366260-7e85-4019-b5f6-16975e6d1c81)

# Activez Cors
![image](https://github.com/user-attachments/assets/6f1c04a7-8f1d-4981-9911-20a4d768bfec)
![image](https://github.com/user-attachments/assets/15d660b5-937f-4d25-a1b7-ed978f29efda)
![image](https://github.com/user-attachments/assets/39ea9481-3c70-47bd-bb30-8d333c77a011)

# Deploy Cors
![image](https://github.com/user-attachments/assets/7ce167e2-01f0-4311-900b-44d6108455bc)
![image](https://github.com/user-attachments/assets/8db8611a-7824-4008-bc94-4e64109a3f8e)
![image](https://github.com/user-attachments/assets/7b67e12b-7a57-46db-8b45-b108a5a71530)
![image](https://github.com/user-attachments/assets/a4658d80-89a9-42ff-b44a-351e769a225f)

# Testez
![image](https://github.com/user-attachments/assets/a0faa598-ad02-4eac-aed2-3ff90210c8b9)

# Résultat
![image](https://github.com/user-attachments/assets/aa576781-7202-4bca-b33d-2f5b75fa0bb1)

# Architecture actuelle
![image](https://github.com/user-attachments/assets/6ed8c621-19ac-431f-a828-80708ce04159)








---
---
---
# Étape 4 : Amazon DynamoDB

# Cherchez les services DynamoDB dans AWS

![image](https://github.com/user-attachments/assets/9f8eab8a-17c2-440c-8281-4929156b90d5)

# Créer une table Amazon DynamoDB 
![image](https://github.com/user-attachments/assets/703dbdc4-01dc-4aca-a9f5-a81d35c631e8)

# Les détails de création d'une table

![image](https://github.com/user-attachments/assets/7332517d-367f-48ea-908f-7cd903cb62af)

# Finalisation de création de la table
![image](https://github.com/user-attachments/assets/da1d0a05-4d02-479d-83f9-07dfa237fec0)

# Observation de la table 
![image](https://github.com/user-attachments/assets/e2c3e00d-df4c-4664-aefc-6cae317b9ce7)

# Copier l'ARN
![image](https://github.com/user-attachments/assets/455ec86d-35f7-44be-9e80-1760d0ad8a51)

# Testez
![image](https://github.com/user-attachments/assets/78d3902d-f5bb-4d59-b188-d2517e989a83)





---
---
---
# Étape 5 : AWS Gestion des identités et des accès (IAM)

# Vérifier les permissions : 

![image](https://github.com/user-attachments/assets/013a32e0-2f90-41cb-ac15-2c0fc183953a)

# Créer une inline policy
![image](https://github.com/user-attachments/assets/aca1d276-cef4-42c1-96a5-738f13a16d6e)

# Copier le fichier json

![image](https://github.com/user-attachments/assets/604d5a57-b186-44e2-ba9c-bd1bb40c8fce)

# Mettre le bon ARN

![image](https://github.com/user-attachments/assets/74dac418-94e5-40f2-a6b4-0047f2298214)

# Créer la policy

![image](https://github.com/user-attachments/assets/d03e25cc-94ab-4a9c-ade0-23d9b7cb2b24)

# Vérifier les permissions dans DynamoDB

![image](https://github.com/user-attachments/assets/170e520a-8381-49b8-888d-b4024ad13f52)




---
---
---
# Étape 6 : Modifier la fonction Lambda pour insérer dans la base de données DynamoDB

![image](https://github.com/user-attachments/assets/e25996a1-eae7-4c55-b6c8-57082c1a1b89)

# Déployez
![image](https://github.com/user-attachments/assets/2114b6fe-5225-4b0c-b189-a61c61fee3fb)

# Testez
![image](https://github.com/user-attachments/assets/b375fbde-b443-4eba-b138-b8c06a739b7a)

# Vérifiez l'insertion dans la table de DynamoDB
![image](https://github.com/user-attachments/assets/d882643c-1e03-4352-bc36-6941d0d7b057)
![image](https://github.com/user-attachments/assets/2d8ac7fb-ecb0-424f-9571-f9c8ea61d746)

# Architecture actuelle 
![image](https://github.com/user-attachments/assets/e93aec61-141e-4e92-ad4d-04da58be25ad)





---
---
---
# Étape 7 : AWS Amplify - établir la liaison

![image](https://github.com/user-attachments/assets/6cf88b71-b280-4c6e-811b-2f90893b13f7)

# insertion du bon appel API dans fetch 

![image](https://github.com/user-attachments/assets/d7942862-c30d-4033-bb5d-b686273e2534)

# Compressez la fonction lambda
![image](https://github.com/user-attachments/assets/3116a500-99d9-44f1-9831-9135ee36513d)

# Cherchez le service Amplify
![image](https://github.com/user-attachments/assets/b917c0e2-9a65-49dc-abe8-f22c527d2ffa)
![image](https://github.com/user-attachments/assets/b1c53402-5164-4556-a482-e59fece3b67a)

# Téléversement du fichier index.zip  
![image](https://github.com/user-attachments/assets/59678066-c85b-4bc8-b62b-21405754250f)

# Testez 
![image](https://github.com/user-attachments/assets/05775c38-c8cd-4852-b85e-58d4a16c052f)
![image](https://github.com/user-attachments/assets/615a694a-df4f-40c9-af3f-015b8a292341)
![image](https://github.com/user-attachments/assets/5bb7a9d4-98e1-457e-87e9-1cd99da0b40d)

# Vérifiez dans la base de données
![image](https://github.com/user-attachments/assets/5edc1f3c-a715-4aa5-b50c-d643379cb827)

# Supprimez toutes les ressources

------------------
------------------
------------------



... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="etape4"></a>

... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="etape5"></a>

... contenu ...
### <a href="#introduction">Revenir en haut</a>
<a name="etape6"></a>

... contenu ...
### <a href="#introduction">Revenir en haut</a>































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
