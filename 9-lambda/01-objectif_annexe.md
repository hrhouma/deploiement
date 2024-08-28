# Annexe : Objectif - Introduction à AWS Lambda

## Qu'est-ce qu'une fonction Lambda ?

Une fonction Lambda est essentiellement un morceau de code qui s'exécute en réponse à un événement déclencheur. Cela signifie que vous écrivez du code, l'uploadez sur AWS Lambda, et AWS s'occupe de tout le reste, comme la gestion des serveurs ou la scalabilité.

### Exemple Simple pour Débutants

Imaginons que vous souhaitez créer une fonction Lambda qui retourne un message "Hello, World!" lorsqu'elle est déclenchée. Voici comment vous pourriez écrire cette fonction en Python :

```python
def lambda_handler(event, context):
    return "Hello, World!"
```

### Explication de Code

- **`lambda_handler`** : C'est le nom de la fonction principale que AWS Lambda exécutera. Vous pouvez le nommer comme vous voulez, mais il doit correspondre au handler que vous configurez dans AWS.
- **`event`** : Cet argument contient les données envoyées au moment du déclenchement de la fonction. Par exemple, si votre fonction est déclenchée par une requête HTTP, `event` contiendra des informations sur cette requête.
- **`context`** : Cet argument contient des informations sur l'exécution de la fonction, comme le temps restant pour l'exécution ou l'identité de l'utilisateur.

### Comment Déployer cette Fonction ?

1. **Via la Console AWS** :
   - Connectez-vous à votre compte AWS.
   - Accédez au service Lambda.
   - Cliquez sur "Create Function".
   - Donnez un nom à votre fonction, choisissez "Python 3.8" comme runtime, et collez le code dans l'éditeur.
   - Déployez et testez la fonction en cliquant sur "Test".

2. **Via AWS CLI** :
   - Écrivez votre code dans un fichier `lambda_function.py`.
   - Zippez ce fichier : `zip function.zip lambda_function.py`.
   - Créez la fonction en utilisant AWS CLI :
     ```bash
     aws lambda create-function --function-name HelloWorldFunction      --zip-file fileb://function.zip --handler lambda_function.lambda_handler      --runtime python3.8 --role arn:aws:iam::123456789012:role/execution_role
     ```

### Pourquoi Utiliser Lambda ?

Lambda est particulièrement utile pour les développeurs débutants car il simplifie grandement le processus de déploiement d'applications. Vous n'avez pas besoin de configurer ou de gérer des serveurs, ce qui vous permet de vous concentrer uniquement sur l'écriture du code.
