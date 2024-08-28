# Annexe : Gestion des Mises à Jour et du Versioning pour AWS Lambda

## Pourquoi le Versioning et la Gestion des Mises à Jour sont Cruciaux ?

Le versioning et la gestion des mises à jour permettent de déployer de nouvelles versions de vos fonctions Lambda sans perturber les services existants. Cela garantit que les mises à jour sont sûres et réversibles, et permet une gestion efficace des versions.

### Exemple Pratique : Implémenter le Versioning et Déployer des Mises à Jour

Imaginons que vous souhaitiez gérer les versions d'une fonction Lambda pour une API, tout en assurant une transition en douceur vers la nouvelle version.

### Étapes

1. **Activer le Versioning pour la Fonction Lambda** :
   - Accédez à la console AWS Lambda.
   - Déployez votre fonction Lambda en tant que nouvelle version en sélectionnant "Publish new version" après avoir effectué des modifications.

2. **Utiliser des Alias pour Gérer les Versions** :
   - Créez un alias pour la version stable de votre fonction, par exemple "prod".
   - Pointez l'alias vers la nouvelle version après avoir vérifié son bon fonctionnement.

   - Exemple de commande CLI pour créer un alias :

```bash
aws lambda create-alias --function-name MyLambdaFunction --name prod --function-version 2
```

3. **Configurer les Déploiements Canaris** :
   - Configurez un déploiement canari pour introduire progressivement la nouvelle version aux utilisateurs.
   - Définissez un pourcentage d'utilisation de la nouvelle version et surveillez les performances avant de basculer complètement.

   - Exemple de configuration de déploiement canari dans la console Lambda :

```json
{
    "Type": "AWS::Lambda::Alias",
    "Properties": {
        "FunctionName": "MyLambdaFunction",
        "FunctionVersion": "2",
        "Name": "prod",
        "RoutingConfig": {
            "AdditionalVersionWeights": {
                "1": 0.1
            }
        }
    }
}
```

4. **Surveiller et Réagir** :
   - Utilisez AWS CloudWatch pour surveiller la performance de chaque version.
   - Si des problèmes surviennent avec la nouvelle version, vous pouvez rapidement revenir à la version précédente en modifiant l'alias.

### Conclusion

Le versioning et la gestion des mises à jour sont essentiels pour maintenir la stabilité de vos fonctions Lambda tout en permettant des mises à jour fréquentes et sécurisées. En utilisant les alias et les déploiements canaris, vous pouvez minimiser les risques associés aux nouvelles versions.
