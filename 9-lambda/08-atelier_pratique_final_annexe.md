# Annexe : Atelier Pratique Final sur AWS Lambda

## Objectif de l'Atelier Pratique Final

L'objectif de cet atelier est de consolider les connaissances acquises tout au long du cours en réalisant un projet complet utilisant AWS Lambda, API Gateway, DynamoDB, et S3. Cet atelier permettra d'appliquer les concepts de création, déploiement, optimisation et intégration des fonctions Lambda.

### Projet : Création d'une Application Serverless Complète

Imaginons que vous devez créer une application serverless pour gérer un service de gestion d'images. Les utilisateurs peuvent télécharger des images, qui seront ensuite traitées par une fonction Lambda pour être redimensionnées et stockées dans S3. Les informations sur les images seront sauvegardées dans DynamoDB.

### Étapes

1. **Créer le Bucket S3 pour le Stockage des Images** :
   - Accédez à la console S3.
   - Créez un bucket nommé `image-upload-bucket`.
   - Configurez les permissions pour permettre à Lambda de lire et écrire dans ce bucket.

2. **Créer la Table DynamoDB pour les Métadonnées des Images** :
   - Accédez à la console DynamoDB.
   - Créez une table nommée `ImageMetadata` avec `ImageID` comme clé primaire.

3. **Développer la Fonction Lambda pour le Traitement des Images** :
   - Créez un fichier `lambda_function.py` avec le code suivant :

```python
import json
import boto3
from PIL import Image
import io

s3 = boto3.client('s3')
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('ImageMetadata')

def lambda_handler(event, context):
    bucket = event['Records'][0]['s3']['bucket']['name']
    key = event['Records'][0]['s3']['object']['key']
    
    # Télécharger l'image depuis S3
    response = s3.get_object(Bucket=bucket, Key=key)
    image = Image.open(io.BytesIO(response['Body'].read()))
    
    # Redimensionner l'image
    image = image.resize((128, 128))
    
    # Sauvegarder l'image redimensionnée dans S3
    buffer = io.BytesIO()
    image.save(buffer, 'JPEG')
    buffer.seek(0)
    
    s3.put_object(Bucket=bucket, Key=f'resized-{key}', Body=buffer)
    
    # Stocker les métadonnées dans DynamoDB
    table.put_item(Item={
        'ImageID': key,
        'ResizedImageKey': f'resized-{key}',
        'Bucket': bucket
    })
    
    return {
        'statusCode': 200,
        'body': json.dumps('Image processed and metadata saved successfully!')
    }
```

4. **Configurer API Gateway pour l'Interaction Utilisateur** :
   - Créez une API RESTful avec API Gateway.
   - Créez une méthode POST pour télécharger les images et déclencher la fonction Lambda.
   - Configurez une méthode GET pour récupérer les métadonnées des images depuis DynamoDB.

5. **Déployer l'Application et Tester** :
   - Déployez les ressources dans AWS et testez l'application en téléchargeant une image via l'API.
   - Vérifiez que l'image est redimensionnée et que les métadonnées sont enregistrées dans DynamoDB.

### Conclusion

Cet atelier pratique permet de mettre en œuvre tous les concepts abordés dans le cours, de la création à la gestion d'une application serverless complète. En réalisant ce projet, vous consolidez vos compétences en AWS Lambda et apprenez à orchestrer plusieurs services AWS pour créer des solutions robustes et scalables.
