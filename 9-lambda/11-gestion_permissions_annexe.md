# Annexe : Gestion des Permissions pour AWS Lambda

## Pourquoi la Gestion des Permissions est Essentielle

La gestion des permissions est cruciale pour assurer la sécurité et le bon fonctionnement de vos fonctions Lambda. AWS utilise IAM (Identity and Access Management) pour contrôler qui peut faire quoi sur vos ressources.

### Exemple Pratique : Configuration des Permissions pour une Fonction Lambda

Imaginons que vous souhaitiez que votre fonction Lambda puisse lire des objets dans un bucket S3 et écrire dans une table DynamoDB.

### Étapes

1. **Créer un Rôle IAM** :
   - Accédez à la console IAM sur AWS.
   - Créez un nouveau rôle et choisissez "AWS Lambda" comme type de rôle.
   - Attachez les politiques gérées suivantes :
     - **AmazonS3ReadOnlyAccess** : Permet à Lambda de lire des objets dans S3.
     - **AmazonDynamoDBFullAccess** : Permet à Lambda d'écrire et de lire des données dans DynamoDB.

2. **Assignez le Rôle à Votre Fonction Lambda** :
   - Lors de la création ou de la modification de votre fonction Lambda, spécifiez le rôle IAM que vous venez de créer.

### Exemple de Code : Utilisation des Permissions

Voici comment votre fonction Lambda peut utiliser ces permissions pour lire depuis S3 et écrire dans DynamoDB :

```python
import boto3

def lambda_handler(event, context):
    s3 = boto3.client('s3')
    dynamodb = boto3.resource('dynamodb')
    
    # Lire un fichier depuis S3
    response = s3.get_object(Bucket='my-bucket', Key='my-key')
    data = response['Body'].read().decode('utf-8')
    
    # Écrire des données dans DynamoDB
    table = dynamodb.Table('MyTable')
    table.put_item(Item={'ID': '123', 'Data': data})
    
    return 'Données traitées avec succès!'
```

### Explication de Code

- **`s3.get_object()`** : Utilise les permissions pour lire un objet dans S3.
- **`table.put_item()`** : Utilise les permissions pour écrire des données dans DynamoDB.

### Conclusion

Une gestion appropriée des permissions IAM est essentielle pour contrôler l'accès aux ressources AWS et assurer la sécurité de vos fonctions Lambda.
