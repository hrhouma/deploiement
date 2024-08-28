# Annexe : Exemple Pratique - Optimisation d'une Fonction Lambda

## Pourquoi Optimiser une Fonction Lambda ?

L'optimisation des fonctions Lambda permet d'améliorer les performances, de réduire les coûts et de s'assurer que vos applications serverless sont aussi efficaces que possible.

### Exemple Pratique : Optimiser une Fonction Lambda pour Réduire le Temps d'Exécution

Imaginons que vous avez une fonction Lambda qui traite des données volumineuses et que vous souhaitez réduire le temps d'exécution en optimisant le code et les ressources allouées.

### Étapes

1. **Analyser les Bottlenecks dans le Code** :
   - Identifiez les sections du code qui prennent le plus de temps à s'exécuter.
   - Utilisez des outils de profilage si nécessaire pour comprendre où se trouvent les goulots d'étranglement.

2. **Optimiser le Code** :
   - Évitez les opérations lourdes dans la boucle principale.
   - Utilisez des bibliothèques optimisées pour le traitement des données.
   - Exemple de code avant optimisation :

```python
import json

def lambda_handler(event, context):
    data = event['data']
    result = []
    for item in data:
        processed = item ** 2  # Exemple d'opération lourde
        result.append(processed)
    return {
        'statusCode': 200,
        'body': json.dumps(result)
    }
```

   - Exemple de code après optimisation :

```python
import json
import numpy as np

def lambda_handler(event, context):
    data = np.array(event['data'])
    result = np.square(data).tolist()  # Utilisation de Numpy pour optimiser l'opération
    return {
        'statusCode': 200,
        'body': json.dumps(result)
    }
```

3. **Ajuster les Ressources Allouées** :
   - Accédez à la console AWS Lambda et augmentez la mémoire allouée si nécessaire.
   - Notez que l'augmentation de la mémoire allouée peut réduire le temps d'exécution mais aussi augmenter les coûts. Trouvez le bon équilibre.

4. **Tester et Mesurer les Améliorations** :
   - Testez la fonction après optimisation pour voir si le temps d'exécution a été réduit.
   - Consultez les logs CloudWatch pour comparer les performances avant et après optimisation.

### Conclusion

L'optimisation des fonctions Lambda est une étape essentielle pour maximiser les performances et minimiser les coûts dans vos applications serverless. En suivant ces étapes, vous pouvez rendre vos fonctions plus efficaces et économiquement viables.
