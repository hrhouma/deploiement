# Annexe : Intégration avec CI/CD pour AWS Lambda

## Pourquoi Intégrer AWS Lambda dans un Pipeline CI/CD ?

L'intégration de vos fonctions Lambda dans un pipeline CI/CD (Continuous Integration/Continuous Deployment) vous permet d'automatiser le déploiement et de garantir que votre code est testé et déployé de manière continue.

### Exemple Pratique : Utiliser AWS CodePipeline pour Déployer une Fonction Lambda

Imaginons que vous souhaitiez configurer un pipeline CI/CD pour déployer automatiquement une fonction Lambda à partir d'un dépôt GitHub.

### Étapes

1. **Configurer un Dépôt GitHub** :
   - Créez un dépôt GitHub et ajoutez votre code Lambda. Par exemple, un fichier `lambda_function.py` avec le code suivant :

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': json.dumps('Hello, CI/CD!')
    }
```

2. **Créer un Pipeline avec AWS CodePipeline** :
   - Accédez à la console AWS CodePipeline.
   - Créez un nouveau pipeline et choisissez GitHub comme source.
   - Configurez CodePipeline pour surveiller votre dépôt GitHub et déclencher le pipeline à chaque commit.

3. **Ajouter une Phase de Build avec AWS CodeBuild** :
   - Ajoutez une phase de build dans CodePipeline en utilisant AWS CodeBuild pour exécuter des tests unitaires ou packager votre code.
   - Exemple de fichier `buildspec.yml` :

```yaml
version: 0.2

phases:
  install:
    commands:
      - pip install -r requirements.txt
  build:
    commands:
      - pytest test_lambda_function.py
artifacts:
  files:
    - lambda_function.py
```

4. **Ajouter une Phase de Déploiement** :
   - Configurez CodePipeline pour déployer la fonction Lambda après un build réussi.
   - Sélectionnez la fonction Lambda que vous souhaitez mettre à jour.

5. **Tester le Pipeline CI/CD** :
   - Poussez un commit dans votre dépôt GitHub pour déclencher le pipeline.
   - Vérifiez que la fonction Lambda est mise à jour automatiquement après un build réussi.

### Conclusion

L'intégration d'AWS Lambda dans un pipeline CI/CD automatisé permet de maintenir la qualité du code tout en accélérant le déploiement. Cette approche améliore l'efficacité de votre workflow de développement.
