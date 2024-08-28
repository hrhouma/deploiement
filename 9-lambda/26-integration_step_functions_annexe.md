# Annexe : Intégration avec Step Functions

## Pourquoi Intégrer AWS Lambda avec Step Functions ?

AWS Step Functions permet de coordonner plusieurs services AWS en orchestrant des flux de travail complexes. L'intégration de Lambda avec Step Functions permet d'automatiser les processus multi-étapes de manière fiable et évolutive.

### Exemple Pratique : Orchestrer un Workflow avec Step Functions et Lambda

Imaginons que vous souhaitez créer un processus qui comprend plusieurs étapes, comme la validation de données, le traitement des commandes, et la notification des utilisateurs.

### Étapes

1. **Créer les Fonctions Lambda** :
   - Créez plusieurs fonctions Lambda pour chaque étape du workflow. Par exemple :
     - `validate_data.py`
     - `process_order.py`
     - `send_notification.py`

2. **Écrire le Code pour Chaque Fonction** :
   - Exemple pour `validate_data.py` :

```python
import json

def lambda_handler(event, context):
    # Validation de données fictive
    if 'order_id' in event:
        return {
            'statusCode': 200,
            'body': json.dumps('Validation Successful!')
        }
    else:
        raise Exception("Validation Failed")
```

3. **Créer un Workflow avec Step Functions** :
   - Accédez à la console Step Functions.
   - Créez un nouveau workflow en définissant les états et transitions entre vos fonctions Lambda.

```json
{
  "Comment": "Example of Step Function Workflow",
  "StartAt": "ValidateData",
  "States": {
    "ValidateData": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:validate_data",
      "Next": "ProcessOrder"
    },
    "ProcessOrder": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:process_order",
      "Next": "SendNotification"
    },
    "SendNotification": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:send_notification",
      "End": true
    }
  }
}
```

4. **Tester le Workflow** :
   - Exécutez le workflow dans Step Functions pour vérifier que toutes les étapes s'exécutent correctement.

### Conclusion

L'intégration de Step Functions avec Lambda permet de créer des workflows serverless puissants et orchestrés de manière fluide. Cette approche est idéale pour automatiser des processus complexes et garantir leur fiabilité.
