# Annexe : Automatisation avec EventBridge et AWS Lambda

## Pourquoi Utiliser EventBridge pour l'Automatisation ?

Amazon EventBridge est un service de bus d'événements qui facilite la connexion de vos applications en utilisant des données issues de vos propres applications, des services SaaS, et d'AWS. L'intégration avec AWS Lambda permet d'automatiser des processus basés sur des événements en temps réel.

### Exemple Pratique : Automatiser une Fonction Lambda avec EventBridge

Imaginons que vous souhaitiez déclencher une fonction Lambda automatiquement chaque fois qu'un événement spécifique se produit, comme l'arrivée d'un nouveau fichier dans un bucket S3.

### Étapes

1. **Créer la Fonction Lambda** :
   - Créez un fichier `lambda_function.py` avec le code suivant :

```python
import json

def lambda_handler(event, context):
    detail = event.get('detail', {})
    print(f"Received event: {json.dumps(detail)}")
    # Votre logique de traitement ici
    return {
        'statusCode': 200,
        'body': json.dumps('Event processed successfully!')
    }
```

2. **Déployer la Fonction Lambda** :
   - Déployez la fonction en suivant les étapes habituelles via AWS CLI ou la console AWS.

3. **Configurer EventBridge** :
   - Accédez à la console EventBridge sur AWS.
   - Créez un nouveau "Rule" (règle) qui déclenchera la fonction Lambda en fonction d'un événement spécifique, par exemple, l'ajout d'un objet dans un bucket S3.

4. **Définir le Pattern de l'Événement** :
   - Définissez un modèle d'événement qui correspond à l'événement que vous souhaitez surveiller, par exemple :

```json
{
  "source": ["aws.s3"],
  "detail-type": ["Object Created"],
  "detail": {
    "bucket-name": ["my-bucket"]
  }
}
```

5. **Associer la Règle à la Fonction Lambda** :
   - Sélectionnez votre fonction Lambda comme cible pour cette règle.

6. **Tester l'Automatisation** :
   - Téléchargez un fichier dans le bucket S3 configuré et vérifiez que la fonction Lambda est déclenchée automatiquement.

### Conclusion

En utilisant EventBridge avec AWS Lambda, vous pouvez automatiser des processus critiques et réagir en temps réel à des événements, créant ainsi des systèmes plus dynamiques et réactifs.
