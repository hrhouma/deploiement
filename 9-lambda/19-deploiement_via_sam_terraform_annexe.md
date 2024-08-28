# Annexe : Déploiement de Fonctions Lambda via AWS SAM ou Terraform

## Utiliser AWS SAM ou Terraform pour Déployer des Fonctions Lambda

AWS SAM (Serverless Application Model) et Terraform sont deux outils puissants pour déployer et gérer vos fonctions Lambda de manière automatisée et répétable.

### Exemple Pratique : Déployer une Fonction Lambda avec AWS SAM

Imaginons que vous souhaitez déployer une fonction Lambda simple qui retourne un message "Hello, World!" en utilisant AWS SAM.

### Étapes avec AWS SAM

1. **Préparez le Code et le Template SAM** :
   - Créez un fichier `app.py` avec le code suivant :

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': json.dumps('Hello, World!')
    }
```

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
      Events:
        MyApi:
          Type: Api
          Properties:
            Path: /hello
            Method: get
```

2. **Déployez avec SAM CLI** :
   - Depuis le terminal, naviguez jusqu'au répertoire de votre projet et exécutez les commandes suivantes pour déployer votre application SAM :
     ```bash
     sam build
     sam deploy --guided
     ```

### Exemple Pratique : Déployer une Fonction Lambda avec Terraform

Imaginons maintenant que vous souhaitiez déployer la même fonction Lambda en utilisant Terraform.

### Étapes avec Terraform

1. **Créez un Fichier Terraform** :
   - Créez un fichier `main.tf` avec le contenu suivant :

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_lambda_function" "hello_world" {
  function_name = "HelloWorldFunction"
  handler       = "app.lambda_handler"
  runtime       = "python3.8"
  role          = "arn:aws:iam::123456789012:role/execution_role"
  filename      = "function.zip"
}

resource "aws_apigatewayv2_api" "api" {
  name          = "MyAPI"
  protocol_type = "HTTP"
}
```

2. **Déployez avec Terraform CLI** :
   - Depuis le terminal, exécutez les commandes suivantes pour déployer votre fonction Lambda :
     ```bash
     terraform init
     terraform apply
     ```

### Conclusion

AWS SAM et Terraform offrent des méthodes puissantes pour déployer et gérer vos fonctions Lambda. Le choix de l'outil dépend de vos préférences et de l'infrastructure que vous souhaitez gérer.
