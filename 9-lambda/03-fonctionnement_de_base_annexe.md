# Annexe : Fonctionnement de Base d'AWS Lambda

## Comment Fonctionne AWS Lambda ?

AWS Lambda exécute votre code en réponse à des événements, sans que vous ayez à gérer les serveurs. Voici comment cela fonctionne en détail.

### Exemple

Imaginez que vous souhaitez créer une fonction qui lit des données depuis un bucket S3 lorsque de nouveaux fichiers sont ajoutés. Voici comment vous pourriez écrire cette fonction en Python :

```python
import boto3

def lambda_handler(event, context):
    s3 = boto3.client('s3')
    bucket = event['Records'][0]['s3']['bucket']['name']
    key = event['Records'][0]['s3']['object']['key']
    
    # Lire le contenu du fichier
    response = s3.get_object(Bucket=bucket, Key=key)
    content = response['Body'].read().decode('utf-8')
    
    return content
```

### Explication de Code

- **`boto3.client('s3')`** : Crée un client S3 pour interagir avec les services S3.
- **`event['Records'][0]['s3']`** : Accède aux détails de l'événement déclencheur, dans ce cas, l'ajout d'un fichier S3.
- **`s3.get_object()`** : Télécharge le fichier depuis S3.

### Déploiement de la Fonction

- Déployez cette fonction en suivant les mêmes étapes que précédemment, et configurez un déclencheur S3 pour tester la fonction.

### Conclusion

Ce simple exemple montre comment Lambda peut être utilisé pour automatiser des tâches courantes comme la gestion des fichiers S3.
