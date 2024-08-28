# Annexe : Écriture du Code Lambda

## Comment Écrire du Code pour AWS Lambda

Écrire du code pour AWS Lambda implique de respecter certaines conventions et de tirer parti des outils et bibliothèques disponibles pour optimiser l'exécution et la maintenance.

### Exemple Pratique : Écrire une Fonction Lambda

Imaginons que vous souhaitez écrire une fonction Lambda qui traite des données envoyées par une API et enregistre les résultats dans DynamoDB.

### Étapes

1. **Préparez votre Environnement** :
   - Assurez-vous que vous avez configuré AWS CLI et que vous avez les droits d'accès appropriés.

2. **Écrire le Code Lambda** :
   - Créez un fichier `lambda_function.py` avec le code suivant :

```python
import json
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('MyTable')

def lambda_handler(event, context):
    body = json.loads(event['body'])
    
    # Écrire les données dans DynamoDB
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

- **`boto3.resource('dynamodb')`** : Utilise la bibliothèque Boto3 pour interagir avec DynamoDB.
- **`table.put_item()`** : Insère des données dans la table DynamoDB.

### Déploiement de la Fonction

1. **Zippez le Code** :
   - Exécutez la commande suivante dans votre terminal :
     ```bash
     zip function.zip lambda_function.py
     ```

2. **Déployez la Fonction via AWS CLI** :
   - Utilisez la commande suivante pour déployer la fonction :
     ```bash
     aws lambda create-function --function-name MyLambdaFunction      --zip-file fileb://function.zip --handler lambda_function.lambda_handler      --runtime python3.8 --role arn:aws:iam::123456789012:role/execution_role
     ```

### Conclusion

Écrire du code pour Lambda nécessite de comprendre les particularités de l'environnement d'exécution serverless. En suivant ces étapes, vous pouvez créer des fonctions efficaces et évolutives.
