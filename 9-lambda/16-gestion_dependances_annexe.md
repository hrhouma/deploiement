# Annexe : Gestion des Dépendances dans AWS Lambda

## Pourquoi la Gestion des Dépendances est Importante

Lorsque vous écrivez du code pour AWS Lambda, il est souvent nécessaire d'inclure des bibliothèques externes. La gestion des dépendances garantit que votre fonction Lambda dispose de tout ce dont elle a besoin pour s'exécuter correctement.

### Exemple Pratique : Inclure une Bibliothèque Externe en Python

Imaginons que vous souhaitez utiliser la bibliothèque `requests` pour faire des appels HTTP depuis votre fonction Lambda.

### Étapes

1. **Installer la Bibliothèque** :
   - Depuis votre terminal, exécutez la commande suivante pour installer la bibliothèque `requests` dans un répertoire spécifique :
     ```bash
     pip install requests -t .
     ```

2. **Écrire le Code Lambda** :
   - Créez un fichier `lambda_function.py` avec le code suivant :

```python
import requests

def lambda_handler(event, context):
    response = requests.get('https://jsonplaceholder.typicode.com/todos/1')
    return {
        'statusCode': 200,
        'body': response.text
    }
```

3. **Zippez les Fichiers** :
   - Zippez tous les fichiers du répertoire, y compris les dépendances installées :
     ```bash
     zip -r function.zip .
     ```

4. **Déployez la Fonction via AWS CLI** :
   - Utilisez la commande suivante pour déployer la fonction Lambda :
     ```bash
     aws lambda create-function --function-name MyFunctionWithDependencies      --zip-file fileb://function.zip --handler lambda_function.lambda_handler      --runtime python3.8 --role arn:aws:iam::123456789012:role/execution_role
     ```

### Conclusion

La gestion des dépendances est essentielle pour s'assurer que toutes les bibliothèques nécessaires sont disponibles lors de l'exécution de votre fonction Lambda. En suivant ces étapes, vous pouvez facilement inclure et utiliser des bibliothèques externes dans vos fonctions Lambda.
