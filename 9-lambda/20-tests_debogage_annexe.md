# Annexe : Tests et Débogage de Fonctions Lambda

## Pourquoi Tester et Déboguer vos Fonctions Lambda ?

Tester et déboguer vos fonctions Lambda est essentiel pour garantir qu'elles fonctionnent comme prévu et pour identifier les problèmes potentiels avant qu'ils n'affectent vos utilisateurs.

### Exemple Pratique : Tests Unitaires en Local

Imaginons que vous souhaitez tester une fonction Lambda localement avant de la déployer.

### Étapes

1. **Écrire des Tests Unitaires** :
   - Créez un fichier `test_lambda_function.py` avec le code suivant :

```python
import json
import pytest
from lambda_function import lambda_handler

def test_lambda_handler():
    event = {
        "body": json.dumps({"key": "value"})
    }
    response = lambda_handler(event, None)
    assert response['statusCode'] == 200
    assert json.loads(response['body']) == 'Hello, World!'
```

2. **Exécutez les Tests en Local** :
   - Utilisez `pytest` pour exécuter les tests localement :
     ```bash
     pytest test_lambda_function.py
     ```

### Débogage en Production

Pour déboguer une fonction Lambda en production, vous pouvez utiliser les outils suivants :

- **AWS CloudWatch Logs** : Capturez et analysez les logs générés par vos fonctions Lambda.
- **AWS X-Ray** : Tracez les requêtes à travers votre architecture serverless pour identifier les goulots d'étranglement et les erreurs.

### Exemple de Code : Ajout de Logs pour le Débogage

Vous pouvez ajouter des logs dans votre fonction Lambda pour capturer des informations essentielles pendant son exécution :

```python
import json
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)

def lambda_handler(event, context):
    logger.info(f"Received event: {event}")
    return {
        'statusCode': 200,
        'body': json.dumps('Hello, World!')
    }
```

### Conclusion

Les tests unitaires et le débogage sont des étapes cruciales dans le développement de fonctions Lambda robustes et fiables. Utiliser les bons outils et pratiques vous aidera à assurer la qualité et la performance de vos fonctions.
