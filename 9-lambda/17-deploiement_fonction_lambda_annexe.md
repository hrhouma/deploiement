# Annexe : Déploiement de Fonctions Lambda

## Comment Déployer une Fonction Lambda

Le déploiement d'une fonction Lambda implique de télécharger votre code et de configurer l'environnement d'exécution via la console AWS, AWS CLI, ou des outils comme AWS SAM ou Terraform.

### Exemple Pratique : Déployer une Fonction Lambda avec AWS CLI

Imaginons que vous avez une fonction Lambda simple que vous souhaitez déployer en utilisant AWS CLI.

### Étapes

1. **Préparez le Code** :
   - Créez un fichier `lambda_function.py` avec le code suivant :

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': json.dumps('Hello, World!')
    }
```

2. **Zippez le Code** :
   - Depuis votre terminal, zippez le fichier :
     ```bash
     zip function.zip lambda_function.py
     ```

3. **Déployez la Fonction avec AWS CLI** :
   - Utilisez la commande suivante pour créer et déployer la fonction Lambda :
     ```bash
     aws lambda create-function --function-name HelloWorldFunction      --zip-file fileb://function.zip --handler lambda_function.lambda_handler      --runtime python3.8 --role arn:aws:iam::123456789012:role/execution_role
     ```

4. **Tester la Fonction** :
   - Vous pouvez tester la fonction via la console AWS ou en configurant un déclencheur comme une API Gateway.

### Conclusion

Le déploiement de fonctions Lambda est un processus simple mais essentiel pour rendre votre code opérationnel dans le cloud. AWS CLI offre une méthode rapide et flexible pour déployer et gérer vos fonctions Lambda.
