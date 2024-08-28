# Annexe : Gestion des Politiques de Sécurité pour AWS Lambda

## Pourquoi les Politiques de Sécurité Sont Essentielles

Les politiques de sécurité IAM permettent de définir précisément quelles actions sont autorisées ou interdites pour vos fonctions Lambda. Cela vous aide à protéger vos ressources et à respecter les principes de moindre privilège.

### Exemple Pratique : Créer une Politique de Sécurité pour Lambda

Imaginons que vous souhaitiez que votre fonction Lambda puisse uniquement lire les objets d'un bucket S3 spécifique et publier des messages sur un sujet SNS.

### Étapes

1. **Créer une Politique IAM Personnalisée** :
   - Accédez à la console IAM sur AWS.
   - Créez une nouvelle politique avec les permissions suivantes :
     - Autoriser la lecture des objets dans un bucket S3 spécifique.
     - Autoriser la publication de messages sur un sujet SNS spécifique.

2. **Exemple de Politique JSON** :

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::my-bucket/*"
        },
        {
            "Effect": "Allow",
            "Action": "sns:Publish",
            "Resource": "arn:aws:sns:us-east-1:123456789012:MyTopic"
        }
    ]
}
```

3. **Attachez la Politique à un Rôle IAM** :
   - Créez un rôle IAM pour Lambda et attachez cette politique au rôle.

4. **Assignez le Rôle à Votre Fonction Lambda** :
   - Lors de la création ou de la modification de votre fonction Lambda, assignez ce rôle pour qu'il puisse accéder aux services S3 et SNS conformément aux règles définies.

### Conclusion

Les politiques de sécurité permettent de contrôler précisément ce que votre fonction Lambda peut faire, minimisant ainsi les risques de sécurité. Elles doivent être configurées soigneusement pour protéger vos ressources tout en permettant les actions nécessaires.
