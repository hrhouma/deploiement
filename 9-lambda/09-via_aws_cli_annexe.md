# Annexe : Création d'une Fonction Lambda via AWS CLI

## Utilisation de l'AWS CLI pour Créer une Fonction Lambda

L'interface en ligne de commande AWS (CLI) est un outil puissant pour gérer vos services AWS directement depuis le terminal. Voici comment créer une fonction Lambda via AWS CLI.

### Exemple Pratique : Créer une Fonction Lambda

Imaginons que vous souhaitez créer une fonction Lambda qui s'exécute lorsque des données sont envoyées à l'API Gateway.

### Étapes

1. **Préparez votre Code** :
   - Créez un fichier `lambda_function.py` avec le code suivant :

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': json.dumps('Hello, World!')
    }
```

2. **Zippez le Fichier** :
   - Depuis le terminal, exécutez la commande suivante pour zipper le fichier :
     ```bash
     zip function.zip lambda_function.py
     ```

3. **Créez la Fonction via AWS CLI** :
   - Utilisez la commande suivante pour créer la fonction Lambda :
     ```bash
     aws lambda create-function --function-name HelloWorldFunction      --zip-file fileb://function.zip --handler lambda_function.lambda_handler      --runtime python3.8 --role arn:aws:iam::123456789012:role/execution_role
     ```

4. **Tester la Fonction** :
   - Utilisez la console AWS pour déclencher la fonction ou configurez une API Gateway pour l'appeler.

### Conclusion

L'utilisation de l'AWS CLI pour créer des fonctions Lambda est une méthode flexible qui vous permet d'automatiser le déploiement et la gestion des fonctions. C'est idéal pour les développeurs qui souhaitent intégrer Lambda dans leurs workflows CI/CD.
