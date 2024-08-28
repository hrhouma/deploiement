# Annexe : Gestion de la Mémoire et du Temps d'Exécution pour AWS Lambda

## Pourquoi la Gestion de la Mémoire et du Temps d'Exécution est Importante ?

La gestion de la mémoire et du temps d'exécution est cruciale pour optimiser les performances et les coûts de vos fonctions Lambda. Une configuration inappropriée peut entraîner des dépassements de temps ou des coûts inutiles.

### Exemple Pratique : Ajuster la Mémoire et le Temps d'Exécution

Imaginons que vous souhaitez optimiser une fonction Lambda qui traite des images pour s'assurer qu'elle utilise la mémoire nécessaire sans dépasser le temps d'exécution alloué.

### Étapes

1. **Configurer la Mémoire** :
   - Accédez à la console AWS Lambda.
   - Sélectionnez votre fonction Lambda.
   - Dans les paramètres de configuration, ajustez la mémoire RAM allouée. AWS Lambda ajuste automatiquement la puissance de calcul proportionnellement à la mémoire allouée.

2. **Optimiser le Temps d'Exécution** :
   - Ajoutez du code pour mesurer le temps d'exécution et ajustez votre fonction en conséquence.

```python
import time
import json

def lambda_handler(event, context):
    start_time = time.time()
    
    # Votre code ici
    result = "Traitement de l'image terminé."
    
    end_time = time.time()
    execution_time = end_time - start_time
    
    return {
        'statusCode': 200,
        'body': json.dumps({
            'result': result,
            'execution_time': execution_time
        })
    }
```

3. **Tester les Ajustements** :
   - Testez la fonction après avoir ajusté la mémoire et vérifiez les logs pour voir si le temps d'exécution est réduit.
   - Si nécessaire, ajustez à nouveau la mémoire et optimisez le code pour améliorer la performance.

### Conclusion

Optimiser la mémoire et le temps d'exécution de vos fonctions Lambda est essentiel pour maintenir un bon équilibre entre performance et coût. En ajustant ces paramètres de manière appropriée, vous pouvez améliorer l'efficacité de vos fonctions Lambda.
