# Annexe : Création d'une Fonction Lambda via AWS SAM

## Utilisation d'AWS SAM pour Créer une Fonction Lambda

AWS SAM (Serverless Application Model) est un framework qui permet de définir et déployer des applications serverless, y compris les fonctions Lambda, à l'aide de templates YAML.

### Exemple Pratique : Créer une Fonction Lambda avec AWS SAM

Imaginons que vous souhaitez créer une fonction Lambda qui retourne un message personnalisé lorsqu'elle est déclenchée via une API Gateway.

### Étapes

1. **Préparez votre Code** :
   - Créez un répertoire de projet, par exemple `my-sam-app`.
   - À l'intérieur de ce répertoire, créez un fichier `app.py` avec le code suivant :

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': json.dumps('Hello, World!')
    }
```

2. **Créez un Template SAM** :
   - Dans le même répertoire, créez un fichier `template.yaml` avec le contenu suivant :

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
      Events:
        MyApi:
          Type: Api
          Properties:
            Path: /hello
            Method: get
```

3. **Déployez la Fonction avec SAM CLI** :
   - Depuis le terminal, naviguez jusqu'au répertoire de votre projet et exécutez les commandes suivantes pour déployer votre application SAM :
     ```bash
     sam build
     sam deploy --guided
     ```

4. **Tester la Fonction** :
   - Une fois déployée, SAM fournira une URL pour accéder à votre API. Ouvrez cette URL dans un navigateur pour tester la fonction.

### Conclusion

AWS SAM simplifie la création, le déploiement, et la gestion des applications serverless. C'est un outil puissant pour les développeurs qui veulent automatiser leurs workflows et gérer des infrastructures complexes avec simplicité.
