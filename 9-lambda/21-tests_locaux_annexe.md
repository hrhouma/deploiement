# Annexe : Tests Locaux pour AWS Lambda

## Pourquoi Tester en Local ?

Tester vos fonctions Lambda en local vous permet d'identifier et de résoudre les problèmes avant de déployer votre code en production, réduisant ainsi les risques d'erreurs coûteuses.

### Exemple Pratique : Tester une Fonction Lambda en Local avec SAM CLI

Imaginons que vous souhaitez tester une fonction Lambda qui retourne un message "Hello, World!" avant de la déployer.

### Étapes

1. **Préparez le Code** :
   - Créez un fichier `app.py` avec le code suivant :

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': json.dumps('Hello, World!')
    }
```

2. **Créez un Template SAM** :
   - Créez un fichier `template.yaml` avec le contenu suivant :

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: 'AWS::Serverless-2016-10-31'
Resources:
  MyLambdaFunction:
    Type: 'AWS::Serverless::Function'
    Properties:
      Handler: app.lambda_handler
      Runtime: python3.8
      CodeUri: .
```

3. **Tester en Local avec SAM CLI** :
   - Exécutez la commande suivante pour tester la fonction en local :
     ```bash
     sam local invoke MyLambdaFunction --event event.json
     ```

   - Vous pouvez également utiliser `sam local start-api` pour simuler une API Gateway localement et tester les requêtes HTTP.

### Conclusion

Tester vos fonctions Lambda en local avec des outils comme SAM CLI vous permet de simuler l'environnement AWS et d'identifier les problèmes avant qu'ils ne deviennent critiques en production.
