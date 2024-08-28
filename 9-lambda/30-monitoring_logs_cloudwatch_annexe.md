# Annexe : Monitoring et Logs avec CloudWatch pour AWS Lambda

## Pourquoi Utiliser CloudWatch pour le Monitoring et les Logs ?

Amazon CloudWatch est un service de surveillance et de gestion de journaux qui vous permet de suivre les performances de vos fonctions Lambda et de diagnostiquer les problèmes en temps réel.

### Exemple Pratique : Configurer CloudWatch pour une Fonction Lambda

Imaginons que vous souhaitez surveiller une fonction Lambda qui traite des commandes et génère des logs pour chaque commande traitée.

### Étapes

1. **Ajouter des Logs dans le Code Lambda** :
   - Créez un fichier `lambda_function.py` avec le code suivant :

```python
import json
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)

def lambda_handler(event, context):
    logger.info(f"Received event: {event}")
    
    order_id = event.get('order_id', 'Unknown')
    logger.info(f"Processing order with ID: {order_id}")
    
    return {
        'statusCode': 200,
        'body': json.dumps(f'Order {order_id} processed successfully!')
    }
```

2. **Déployer la Fonction et Activer CloudWatch** :
   - Déployez la fonction Lambda en suivant les étapes habituelles. CloudWatch Logs est automatiquement activé pour capturer les logs générés par la fonction.

3. **Surveiller les Logs dans CloudWatch** :
   - Accédez à la console CloudWatch sur AWS.
   - Allez dans la section "Logs" et recherchez le groupe de logs associé à votre fonction Lambda.
   - Vous pourrez voir tous les logs générés, filtrer par niveaux (INFO, ERROR), et rechercher des messages spécifiques.

4. **Configurer des Alarmes CloudWatch (Optionnel)** :
   - Si vous souhaitez être notifié en cas de problème, vous pouvez configurer des alarmes dans CloudWatch pour surveiller des métriques spécifiques, comme le taux d'erreurs ou la durée d'exécution.

### Conclusion

L'intégration de CloudWatch avec AWS Lambda permet de surveiller l'exécution de vos fonctions en temps réel, de diagnostiquer les problèmes rapidement et de maintenir une haute disponibilité de vos applications serverless.
