# Annexe : Utilisation de CodePipeline avec AWS Lambda

## Pourquoi Utiliser AWS CodePipeline avec Lambda ?

AWS CodePipeline est un service d'intégration et de déploiement continu (CI/CD) qui vous permet d'automatiser les étapes de votre pipeline de déploiement. En l'intégrant avec AWS Lambda, vous pouvez automatiser le processus de déploiement de vos fonctions Lambda, réduisant ainsi les erreurs et accélérant la mise en production.

### Exemple Pratique : Configurer un Pipeline avec AWS CodePipeline

Imaginons que vous souhaitiez déployer automatiquement une fonction Lambda à partir d'un dépôt GitHub en utilisant AWS CodePipeline.

### Étapes

1. **Créer un Dépôt GitHub** :
   - Créez un dépôt GitHub avec le code source de votre fonction Lambda, par exemple :

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from CodePipeline!')
    }
```

2. **Configurer AWS CodePipeline** :
   - Accédez à la console AWS CodePipeline.
   - Créez un nouveau pipeline et choisissez GitHub comme source. Sélectionnez le dépôt que vous avez créé et configurez un déclencheur basé sur les commits.

3. **Ajouter une Étape de Build avec AWS CodeBuild** :
   - Configurez une étape de build pour installer les dépendances et exécuter des tests unitaires si nécessaire.
   - Utilisez un fichier `buildspec.yml` pour définir les commandes de build :

```yaml
version: 0.2

phases:
  install:
    commands:
      - pip install -r requirements.txt
  build:
    commands:
      - pytest
artifacts:
  files:
    - lambda_function.py
```

4. **Ajouter une Étape de Déploiement pour Lambda** :
   - Ajoutez une étape de déploiement dans le pipeline pour mettre à jour votre fonction Lambda.
   - Sélectionnez la fonction Lambda cible pour le déploiement.

5. **Tester le Pipeline** :
   - Poussez un nouveau commit dans le dépôt GitHub et observez comment CodePipeline déploie automatiquement les modifications à votre fonction Lambda.

### Conclusion

Utiliser AWS CodePipeline avec Lambda permet de mettre en place un processus de déploiement continu automatisé, garantissant que votre code est testé et déployé de manière fiable et efficace.
