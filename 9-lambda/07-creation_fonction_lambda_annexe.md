# Annexe : Création d'une Fonction Lambda

## Comment Créer une Fonction Lambda

AWS Lambda permet de créer facilement des fonctions sans gérer les serveurs. Voici comment créer une fonction Lambda en quelques étapes simples.

### Exemple Pratique : Création d'une Fonction Lambda

Imaginons que vous souhaitez créer une fonction Lambda qui s'exécute lorsque des données sont envoyées via une API Gateway. Voici comment procéder.

### Code Exemple

```python
import json

def lambda_handler(event, context):
    # Analyse les données envoyées par l'API Gateway
    body = json.loads(event['body'])
    
    # Retourne une réponse simple
    return {
        'statusCode': 200,
        'body': json.dumps(f"Hello, {body['name']}!")
    }
```

### Explication de Code

- **`json.loads(event['body'])`** : Analyse les données JSON envoyées dans le corps de la requête HTTP.
- **`body['name']`** : Extrait le nom de la personne envoyé dans la requête.

### Déploiement de la Fonction

1. **Via la Console AWS** :
   - Accédez à AWS Lambda.
   - Créez une nouvelle fonction et collez le code ci-dessus.
   - Associez une API Gateway comme déclencheur pour tester la fonction.

2. **Via AWS CLI** :
   - Zippez votre fichier de code.
   - Utilisez la commande suivante :
     ```bash
     aws lambda create-function --function-name GreetUserFunction      --zip-file fileb://function.zip --handler lambda_function.lambda_handler      --runtime python3.8 --role arn:aws:iam::123456789012:role/execution_role
     ```

### Conclusion

Créer des fonctions Lambda est simple et direct, et permet de répondre rapidement à des événements, comme des requêtes HTTP via API Gateway.
