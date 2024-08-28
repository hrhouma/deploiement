# Annexe : Exemple Pratique - Création d'une API Serverless

## Créer une API Serverless avec AWS Lambda et API Gateway

Dans cet exemple, nous allons créer une API RESTful simple qui retourne un message personnalisé en utilisant AWS Lambda et API Gateway.

### Étapes

1. **Préparer le Code Lambda** :
   - Créez un fichier `lambda_function.py` avec le code suivant :

```python
import json

def lambda_handler(event, context):
    name = event['queryStringParameters']['name']
    return {
        'statusCode': 200,
        'body': json.dumps(f'Hello, {name}!')
    }
```

2. **Déployer la Fonction Lambda** :
   - Déployez la fonction en suivant les étapes habituelles via AWS CLI ou la console AWS.

3. **Configurer API Gateway** :
   - Accédez à la console API Gateway.
   - Créez une nouvelle API REST.
   - Ajoutez une ressource `/hello`.
   - Ajoutez une méthode GET pour la ressource et intégrez-la avec la fonction Lambda déployée.

4. **Déployer l'API** :
   - Déployez l'API sur une nouvelle étape (par exemple, `prod`).
   - Vous recevrez une URL pour accéder à votre API.

5. **Tester l'API** :
   - Ouvrez l'URL de l'API dans un navigateur en ajoutant `?name=VotreNom` à la fin de l'URL pour tester la fonction Lambda.

### Conclusion

Ce simple exemple montre comment AWS Lambda et API Gateway peuvent être utilisés ensemble pour créer des API serverless efficaces et évolutives.
