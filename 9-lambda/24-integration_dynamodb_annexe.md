# Annexe : Intégration avec DynamoDB

## Pourquoi Intégrer AWS Lambda avec DynamoDB ?

DynamoDB est un service de base de données NoSQL géré par AWS, idéal pour les applications nécessitant une faible latence à n'importe quelle échelle. L'intégration de DynamoDB avec AWS Lambda permet de créer des applications serverless puissantes et évolutives.

### Exemple Pratique : Stocker des Données dans DynamoDB depuis une Fonction Lambda

Imaginons que vous souhaitez créer une fonction Lambda qui enregistre des informations d'utilisateur dans une table DynamoDB.

### Étapes

1. **Créer une Table DynamoDB** :
   - Accédez à la console DynamoDB sur AWS.
   - Créez une table nommée `Users` avec `UserID` comme clé primaire.

2. **Créer une Fonction Lambda** :
   - Créez un fichier `lambda_function.py` avec le code suivant :

```python
import json
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Users')

def lambda_handler(event, context):
    user_data = json.loads(event['body'])
    
    table.put_item(Item={
        'UserID': user_data['user_id'],
        'Name': user_data['name'],
        'Email': user_data['email']
    })
    
    return {
        'statusCode': 200,
        'body': json.dumps('User saved successfully!')
    }
```

   - Déployez la fonction en suivant les étapes habituelles.

3. **Configurer API Gateway** :
   - Créez une API dans API Gateway qui déclenche cette fonction Lambda.
   - Configurez une méthode POST pour accepter les données utilisateur et les passer à Lambda.

4. **Tester l'API** :
   - Déployez l'API et utilisez un outil comme Postman pour envoyer une requête POST avec les données utilisateur au format JSON.

### Conclusion

L'intégration de DynamoDB avec Lambda permet de créer des applications serverless qui stockent et gèrent efficacement des données en temps réel, offrant ainsi une scalabilité et une performance optimales.
