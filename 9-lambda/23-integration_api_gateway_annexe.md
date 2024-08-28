# Annexe : Intégration avec API Gateway

## Pourquoi Intégrer AWS Lambda avec API Gateway ?

API Gateway permet de créer et déployer des API sécurisées à grande échelle. Lorsqu'elle est combinée avec AWS Lambda, elle vous permet de créer des applications serverless puissantes et flexibles.

### Exemple Pratique : Créer une API Serverless avec API Gateway et Lambda

Imaginons que vous souhaitez créer une API qui appelle une fonction Lambda pour retourner un message personnalisé.

### Étapes

1. **Créer une Fonction Lambda** :
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

   - Déployez la fonction en suivant les étapes habituelles.

2. **Configurer API Gateway** :
   - Accédez à la console API Gateway sur AWS.
   - Créez une nouvelle API REST.
   - Ajoutez une nouvelle ressource, par exemple `/hello`.
   - Créez une méthode GET pour cette ressource et intégrez-la à la fonction Lambda que vous venez de créer.

3. **Tester l'API** :
   - Déployez l'API sur une nouvelle étape.
   - Ouvrez l'URL de l'API dans un navigateur, en ajoutant `?name=VotreNom` à la fin de l'URL pour tester la fonction Lambda.

### Conclusion

L'intégration d'AWS Lambda avec API Gateway vous permet de créer des API serverless rapidement et efficacement, idéales pour les applications modernes nécessitant une scalabilité et une flexibilité maximales.
