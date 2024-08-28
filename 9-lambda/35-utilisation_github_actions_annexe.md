# Annexe : Utilisation de GitHub Actions avec AWS Lambda

## Pourquoi Utiliser GitHub Actions avec AWS Lambda ?

GitHub Actions vous permet d'automatiser, de tester et de déployer votre code directement à partir de votre dépôt GitHub. Lorsqu'il est intégré à AWS Lambda, il vous permet de configurer un pipeline CI/CD pour déployer vos fonctions Lambda chaque fois qu'une modification est poussée sur votre dépôt.

### Exemple Pratique : Configurer un Workflow GitHub Actions pour Déployer une Fonction Lambda

Imaginons que vous souhaitiez déployer automatiquement une fonction Lambda à chaque fois qu'un commit est poussé sur la branche `main` de votre dépôt GitHub.

### Étapes

1. **Créer un Dépôt GitHub** :
   - Créez un dépôt GitHub avec le code source de votre fonction Lambda, par exemple :

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from GitHub Actions!')
    }
```

2. **Configurer un Workflow GitHub Actions** :
   - Créez un fichier `.github/workflows/deploy.yml` avec le contenu suivant :

```yaml
name: Deploy Lambda Function

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: 3.8

    - name: Install dependencies
      run: |
        pip install -r requirements.txt

    - name: Zip Lambda function
      run: zip -r function.zip lambda_function.py

    - name: Deploy to AWS Lambda
      env:
        AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
        AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        AWS_REGION: "us-east-1"
      run: |
        aws lambda update-function-code --function-name MyLambdaFunction --zip-file fileb://function.zip
```

3. **Ajouter vos Clés AWS en tant que Secrets** :
   - Dans les paramètres de votre dépôt GitHub, ajoutez `AWS_ACCESS_KEY_ID` et `AWS_SECRET_ACCESS_KEY` en tant que secrets pour permettre à GitHub Actions de déployer la fonction Lambda.

4. **Tester le Workflow** :
   - Poussez un commit dans la branche `main` et observez comment GitHub Actions déploie automatiquement les modifications à votre fonction Lambda.

### Conclusion

Utiliser GitHub Actions pour déployer vos fonctions Lambda permet d'automatiser votre pipeline CI/CD directement depuis votre dépôt GitHub, ce qui rend le déploiement rapide, fiable et facile à gérer.
