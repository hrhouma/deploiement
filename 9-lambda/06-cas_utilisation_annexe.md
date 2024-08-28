# Annexe : Cas d'Utilisation d'AWS Lambda

## Cas d'Utilisation Populaires

AWS Lambda peut être utilisé pour une variété de tâches, de l'automatisation des processus à la gestion des événements en temps réel.

### Exemple Pratique : Traitement de Données en Temps Réel

Imaginons que vous devez traiter des données de capteurs IoT en temps réel. Vous pouvez utiliser AWS Lambda pour analyser les données dès qu'elles sont reçues.

```python
import json

def lambda_handler(event, context):
    data = json.loads(event['body'])
    
    # Analyse des données
    temperature = data['temperature']
    if temperature > 30:
        return {
            'statusCode': 200,
            'body': json.dumps('Température élevée détectée!')
        }
    else:
        return {
            'statusCode': 200,
            'body': json.dumps('Température normale.')
        }
```

### Explication de Code

- **`json.loads(event['body'])`** : Analyse les données JSON reçues.
- **`temperature > 30`** : Vérifie si la température est supérieure à un seuil.

### Conclusion

Les cas d'utilisation de Lambda sont vastes, et il est facile d'intégrer Lambda dans des solutions complexes pour automatiser des tâches et traiter des données en temps réel.
