# Annexe : Qu'est-ce que AWS Lambda ?

## Définition de AWS Lambda

AWS Lambda est un service de calcul serverless qui exécute votre code en réponse à des événements et alloue automatiquement les ressources nécessaires. Le terme "serverless" signifie que vous n'avez pas à gérer les serveurs ; tout est pris en charge par AWS.

### Exemple Simple pour Débutants

Voici un exemple simple de fonction Lambda en Python. Cette fonction prend un événement en entrée, et renvoie un message "Hello from Lambda!".

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }
```

### Explication de Code

- **`lambda_handler`** : C'est le nom de la fonction que Lambda appelle lorsque l'événement est déclenché.
- **`event`** : Contient les données de l'événement déclencheur.
- **`context`** : Contient des informations sur l'exécution de la fonction.

### Déploiement de la Fonction

1. **Via la Console AWS** :
   - Accédez à AWS Lambda.
   - Créez une nouvelle fonction et collez le code ci-dessus.
   - Déployez et testez la fonction.

2. **Via AWS CLI** :
   - Zippez votre fichier de code.
   - Utilisez la commande suivante :
     ```bash
     aws lambda create-function --function-name HelloWorldFunction      --zip-file fileb://function.zip --handler lambda_function.lambda_handler      --runtime python3.8 --role arn:aws:iam::123456789012:role/execution_role
     ```

### Conclusion

Lambda permet de créer et déployer facilement des fonctions sans se soucier de l'infrastructure sous-jacente. C'est un outil puissant pour les développeurs de tous niveaux.
