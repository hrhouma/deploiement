# Annexe : Déploiement d'une Fonction Lambda via la Console AWS

## Déployer une Fonction Lambda en Utilisant la Console AWS

La console AWS est un moyen intuitif et accessible de déployer vos fonctions Lambda sans avoir besoin d'utiliser des commandes en ligne. Voici un guide étape par étape pour vous aider à déployer une fonction Lambda via la console AWS.

### Exemple Pratique : Déployer une Fonction Lambda

Imaginons que vous avez une fonction Lambda simple qui retourne un message "Hello, World!" et que vous souhaitez la déployer via la console AWS.

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

2. **Accédez à la Console AWS** :
   - Connectez-vous à votre compte AWS.
   - Allez dans le service Lambda.

3. **Créez une Nouvelle Fonction** :
   - Cliquez sur "Create Function".
   - Choisissez "Author from scratch".
   - Donnez un nom à votre fonction, par exemple "HelloWorldFunction".
   - Sélectionnez Python 3.8 comme runtime.

4. **Ajoutez le Code** :
   - Collez le code de votre fonction dans l'éditeur de la console AWS.

5. **Configurez le Déclencheur (Optionnel)** :
   - Si vous souhaitez déclencher la fonction via une API Gateway, vous pouvez le configurer dans la section "Add trigger".

6. **Déployez et Testez** :
   - Cliquez sur "Deploy".
   - Créez un événement de test dans l'onglet "Test" pour voir le résultat.

### Conclusion

Déployer une fonction Lambda via la console AWS est une méthode simple et rapide, idéale pour les débutants qui veulent se familiariser avec les fonctions Lambda et leur déploiement dans le cloud.
