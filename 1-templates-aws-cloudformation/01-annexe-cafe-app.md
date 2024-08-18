### Explication des Fonctions Intrinsèques

1. **`!Ref`**:
   - **Description** : La fonction `Ref` retourne la valeur d'un paramètre ou l'identifiant d'une ressource définie dans le template. C'est utile pour faire référence à des valeurs configurées dynamiquement.
   - **Exemple dans le template** : 
     ```yaml
     InstanceType: !Ref InstanceTypeParameter
     ```
     Ici, `!Ref InstanceTypeParameter` renvoie la valeur du paramètre `InstanceTypeParameter` choisi (comme `t2.micro`).

2. **`!GetAtt`**:
   - **Description** : `GetAtt` permet d'obtenir un attribut spécifique d'une ressource AWS. Par exemple, pour une instance EC2, vous pouvez obtenir son adresse IP publique ou son ID.
   - **Exemple dans le template** : 
     ```yaml
     WebServerPublicIP:
       Value: !GetAtt 'CafeInstance.PublicIp'
     ```
     Ici, `!GetAtt 'CafeInstance.PublicIp'` récupère l'adresse IP publique de l'instance EC2 `CafeInstance`.

3. **`!FindInMap`**:
   - **Description** : `FindInMap` récupère une valeur spécifique d'un mappage défini dans la section `Mappings`. Cela vous permet de définir des valeurs différentes selon la région ou d'autres paramètres.
   - **Exemple dans le template** :
     ```yaml
     KeyName: !FindInMap 
       - RegionMap
       - !Ref 'AWS::Region'
       - keypair
     ```
     Ici, `!FindInMap` recherche dans le mappage `RegionMap` pour récupérer la clé SSH associée à la région AWS actuelle.

4. **`!ImportValue`**:
   - **Description** : `ImportValue` permet d'importer des valeurs exportées par d'autres stacks CloudFormation. C'est très utile pour partager des ressources entre différents stacks.
   - **Exemple dans le template** :
     ```yaml
     VpcId: !ImportValue
       'Fn::Sub': '${CafeNetworkParameter}-VpcID'
     ```
     Ici, `!ImportValue` est utilisé pour importer l'ID du VPC correspondant à `CafeNetworkParameter-VpcID` d'un autre stack.

5. **`!Sub`**:
   - **Description** : `Sub` (Substitute) permet d'insérer des valeurs de variables dans des chaînes de caractères. Vous pouvez également l'utiliser avec des expressions comme `${}` pour des substitutions plus complexes.
   - **Exemple dans le template** :
     ```yaml
     VpcId: !ImportValue
       'Fn::Sub': '${CafeNetworkParameter}-VpcID'
     ```
     Ici, `!Sub` est utilisé pour créer dynamiquement une chaîne de caractères en combinant la valeur de `CafeNetworkParameter` avec `-VpcID`.

     Un autre exemple est l'utilisation dans la section `UserData` :
     ```yaml
     Fn::Base64:
       !Sub |
         #!/bin/bash
         yum -y update
         ...
     ```
     Ici, `!Sub` est utilisé pour insérer du texte dans le script `UserData`, permettant potentiellement l'insertion de variables si nécessaire.

6. **`Fn::Base64`**:
   - **Description** : `Fn::Base64` encode une chaîne de caractères en Base64, souvent utilisée pour les scripts `UserData` dans EC2 afin qu'ils puissent être correctement interprétés par l'instance.
   - **Exemple dans le template** :
     ```yaml
     Fn::Base64:
       !Sub |
         #!/bin/bash
         yum -y update
         yum install -y httpd mariadb-server wget
         ...
     ```
     Ici, le script bash est encodé en Base64 avant d'être transmis à l'instance EC2 pour être exécuté au démarrage.

### Résumé
- Ces fonctions vous permettent de créer des templates CloudFormation dynamiques et modulaires, en réutilisant des valeurs, en accédant à des attributs spécifiques, en important des valeurs d'autres stacks, et en substituant des variables dans des chaînes de caractères. 
- Cela rend vos templates plus flexibles et adaptés à divers environnements AWS.


# Table comparative

- Voici une table comparative des fonctions intrinsèques utilisées dans votre template AWS CloudFormation : `!Ref`, `!GetAtt`, `!FindInMap`, `!ImportValue`, `!Sub`, et `Fn::Base64`.

| **Fonction**   | **Description**                                                                                           | **Usage Principal**                                                                 | **Exemple**                                                                                      |
|----------------|-----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| **`!Ref`**     | Retourne la valeur d'un paramètre ou l'ID d'une ressource définie dans le template.                        | Obtenir la valeur d'un paramètre ou l'identifiant d'une ressource.                  | `InstanceType: !Ref InstanceTypeParameter`                                                       |
| **`!GetAtt`**  | Récupère la valeur d'un attribut spécifique d'une ressource AWS.                                           | Accéder à une propriété spécifique d'une ressource AWS (comme l'IP d'une instance). | `WebServerPublicIP: !GetAtt 'CafeInstance.PublicIp'`                                             |
| **`!FindInMap`**| Récupère une valeur spécifique dans un mappage défini dans la section `Mappings` du template.              | Chercher des valeurs dynamiques selon des paramètres comme la région AWS.           | `KeyName: !FindInMap - RegionMap - !Ref 'AWS::Region' - keypair`                                 |
| **`!ImportValue`**| Importe une valeur exportée par un autre stack CloudFormation.                                          | Partager des valeurs entre différents stacks CloudFormation.                        | `VpcId: !ImportValue 'Fn::Sub': '${CafeNetworkParameter}-VpcID'`                                 |
| **`!Sub`**     | Effectue une substitution de variables dans une chaîne de caractères.                                      | Insérer dynamiquement des valeurs dans des chaînes de caractères.                   | `VpcId: !Sub '${CafeNetworkParameter}-VpcID'`                                                    |
| **`Fn::Base64`**| Encode une chaîne de caractères en Base64.                                                                | Encoder un script ou du texte à transmettre à une ressource comme EC2.              | `Fn::Base64: !Sub | #!/bin/bash yum -y update ...`                                               |

### Explication des Colonnes :

- **Fonction** : Le nom de la fonction intrinsèque utilisée dans AWS CloudFormation.
- **Description** : Une brève explication de ce que fait la fonction.
- **Usage Principal** : Indique le cas d'utilisation principal ou la raison pour laquelle vous utiliseriez cette fonction.
- **Exemple** : Un exemple tiré du template pour illustrer comment la fonction est utilisée.

Cette table permet de comparer rapidement les différentes fonctions intrinsèques et de comprendre comment et pourquoi chacune est utilisée dans un template CloudFormation.
