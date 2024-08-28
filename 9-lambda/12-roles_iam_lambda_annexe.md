# Annexe : Rôles IAM pour AWS Lambda

## Comprendre les Rôles IAM pour AWS Lambda

Les rôles IAM (Identity and Access Management) sont utilisés pour accorder à AWS Lambda les permissions nécessaires pour interagir avec d'autres services AWS en toute sécurité.

### Exemple Pratique : Créer un Rôle IAM pour Lambda

Imaginons que vous souhaitiez que votre fonction Lambda puisse accéder à S3 pour lire des fichiers et envoyer des notifications via SNS (Simple Notification Service).

### Étapes

1. **Créer un Rôle IAM avec les Permissions Nécessaires** :
   - Accédez à la console IAM sur AWS.
   - Créez un nouveau rôle avec le type "AWS Lambda".
   - Attachez les politiques gérées suivantes :
     - **AmazonS3ReadOnlyAccess** : Pour lire les objets dans S3.
     - **AmazonSNSFullAccess** : Pour envoyer des notifications via SNS.

2. **Assignez le Rôle à Votre Fonction Lambda** :
   - Lors de la création ou de la modification de votre fonction Lambda, assignez ce rôle IAM pour qu'il puisse accéder aux services S3 et SNS.

### Exemple de Code : Utilisation des Rôles IAM

Voici un exemple de fonction Lambda utilisant les rôles IAM pour lire un fichier depuis S3 et envoyer une notification via SNS :

```python
import boto3

def lambda_handler(event, context):
    s3 = boto3.client('s3')
    sns = boto3.client('sns')
    
    # Lire un fichier depuis S3
    response = s3.get_object(Bucket='my-bucket', Key='my-key')
    data = response['Body'].read().decode('utf-8')
    
    # Envoyer une notification via SNS
    sns.publish(
        TopicArn='arn:aws:sns:us-east-1:123456789012:MyTopic',
        Message=f'Data processed: {data}',
        Subject='Lambda SNS Notification'
    )
    
    return 'Notification envoyée avec succès!'
```

### Explication de Code

- **`s3.get_object()`** : Utilise le rôle IAM pour lire un fichier dans S3.
- **`sns.publish()`** : Utilise le rôle IAM pour envoyer une notification via SNS.

### Conclusion

Les rôles IAM sont essentiels pour sécuriser les interactions entre vos fonctions Lambda et d'autres services AWS. Une bonne gestion des rôles IAM permet de limiter les accès aux ressources sensibles tout en assurant un fonctionnement fluide de vos fonctions.
