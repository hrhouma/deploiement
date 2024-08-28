# Annexe : Exemple Pratique - Automatisation de Déploiement de Fonctions Lambda

## Pourquoi Automatiser le Déploiement de Fonctions Lambda ?

Automatiser le déploiement de vos fonctions Lambda garantit que vos mises à jour sont déployées de manière cohérente et rapide, tout en réduisant les risques d'erreurs humaines. Cette automatisation s'intègre parfaitement dans un pipeline CI/CD.

### Exemple Pratique : Automatisation du Déploiement d'une Fonction Lambda

Imaginons que vous souhaitiez configurer un pipeline CI/CD qui automatise le déploiement d'une fonction Lambda à partir d'un dépôt GitHub.

### Étapes

1. **Préparer le Code Source** :
   - Créez un fichier `lambda_function.py` dans votre dépôt GitHub avec le code suivant :

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': json.dumps('Automated Deployment!')
    }
```

2. **Configurer le Workflow GitHub Actions** :
   - Créez un fichier `.github/workflows/deploy.yml` pour automatiser le déploiement :

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
      run: pip install -r requirements.txt

    - name: Zip Lambda function
      run: zip -r function.zip lambda_function.py

    - name: Deploy to AWS Lambda
      env:
        AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
        AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        AWS_REGION: "us-east-1"
      run: aws lambda update-function-code --function-name MyLambdaFunction --zip-file fileb://function.zip
```

3. **Ajouter les Clés AWS comme Secrets** :
   - Dans les paramètres de votre dépôt GitHub, ajoutez `AWS_ACCESS_KEY_ID` et `AWS_SECRET_ACCESS_KEY` comme secrets.

4. **Tester le Pipeline** :
   - Poussez un commit sur la branche `main` pour déclencher le workflow. Vérifiez que la fonction Lambda est automatiquement déployée après chaque mise à jour.

### Conclusion

Automatiser le déploiement de vos fonctions Lambda via un pipeline CI/CD permet de garantir des déploiements rapides, fiables et sans intervention manuelle, ce qui est essentiel pour maintenir une haute qualité et une efficacité opérationnelle.
