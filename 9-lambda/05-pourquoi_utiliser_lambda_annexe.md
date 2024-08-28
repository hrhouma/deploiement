# Annexe : Pourquoi Utiliser AWS Lambda ?

## Avantages de l'Utilisation d'AWS Lambda

AWS Lambda est une solution idéale pour les applications nécessitant de la scalabilité, un coût optimisé et une gestion simplifiée de l'infrastructure.

### Cas d'Utilisation

1. **Traitement en Temps Réel** : Lambda peut traiter les données dès qu'elles arrivent, comme l'analyse de logs ou le traitement d'images.
2. **Backends pour API** : Utilisez Lambda pour créer des backends sans serveur qui évoluent automatiquement avec la demande.

### Exemple de Fonction Lambda

Voici une fonction qui transforme une image lorsqu'elle est téléchargée dans S3 :

```python
from PIL import Image
import boto3

def lambda_handler(event, context):
    s3 = boto3.client('s3')
    bucket = event['Records'][0]['s3']['bucket']['name']
    key = event['Records'][0]['s3']['object']['key']
    
    # Télécharger l'image
    response = s3.get_object(Bucket=bucket, Key=key)
    image = Image.open(response['Body'])
    
    # Transformation de l'image
    image = image.convert('L')  # Convertir en noir et blanc
    image.save('/tmp/transformed_image.png')
    
    # Sauvegarder l'image transformée dans S3
    s3.upload_file('/tmp/transformed_image.png', bucket, 'transformed_' + key)
    
    return 'Image transformée et sauvegardée avec succès!'
```

### Explication de Code

- **`Image.open(response['Body'])`** : Ouvre l'image téléchargée depuis S3.
- **`image.convert('L')`** : Convertit l'image en noir et blanc.
- **`s3.upload_file()`** : Télécharge l'image transformée dans S3.

### Conclusion

Lambda est un outil puissant pour une grande variété d'applications, de l'automatisation au traitement des données en temps réel.
