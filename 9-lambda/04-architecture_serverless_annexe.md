# Annexe : Architecture Serverless

## Comprendre l'Architecture Serverless

L'architecture serverless permet aux développeurs de se concentrer sur l'écriture de code sans gérer l'infrastructure. AWS Lambda est au cœur de cette architecture.

### Exemple d'Architecture Serverless

Voici un exemple d'architecture où AWS Lambda est utilisé avec API Gateway et DynamoDB :

- **API Gateway** : Gère les requêtes HTTP et les transmet à Lambda.
- **AWS Lambda** : Exécute le code en réponse aux requêtes.
- **DynamoDB** : Stocke les données traitées par Lambda.

### Code Exemple : API Serverless avec Lambda

```python
import json
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('MyTable')

def lambda_handler(event, context):
    # Parse le corps de la requête HTTP
    body = json.loads(event['body'])
    
    # Écriture dans DynamoDB
    table.put_item(Item={
        'ID': body['id'],
        'Data': body['data']
    })
    
    return {
        'statusCode': 200,
        'body': json.dumps('Données enregistrées avec succès!')
    }
```

### Explication de Code

- **`dynamodb.Table('MyTable')`** : Se connecte à une table DynamoDB nommée "MyTable".
- **`table.put_item()`** : Écrit les données dans DynamoDB.

### Conclusion

L'architecture serverless simplifie grandement le développement d'applications scalables et performantes sans la gestion de serveurs.
