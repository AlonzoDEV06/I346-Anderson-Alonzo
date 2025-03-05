# Laboratoire EC2

## List all VPCS
[decrire le vpc]([https://git-scm.com/](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-vpcs.html?highlight=describe%20vpc))

  ```
aws ec2 describe-vpcs --query "Vpcs[*].VpcId" --output table

  ```
```
[OUTPUT]
---------------------------
|      DescribeVpcs       |
+-------------------------+
|  vpc-0a22d771f16ae549d  |
+-------------------------+

```

## List all Routes tables

Voici la "policy" qui vous a été attribuée:

```bash
aws ec2 describe-route-tables --query "RouteTables[*].RouteTableId" --output table

```

```
[OUTPUT]
---------------------------
|   DescribeRouteTables   |
+-------------------------+
|  rtb-0a9293aaf3c30b82c  |
|  rtb-0acd33fa1f46d6e21  |
|  rtb-069f0fe8e2ed1ff37  |
|  rtb-00b3f747f972f123a  |
|  rtb-01ebe5717e9104f85  |
|  rtb-0e48c9ae2d1e0e4b9  |
|  rtb-0f49e7901c1b634f0  |
|  rtb-005b030aec917782b  |
|  rtb-07bf97cd343c65b4c  |
|  rtb-09eea99d8ac647a5f  |
+-------------------------+
```


### Créer un bucket

```bash

```

```
[OUTPUT]

```

* Créer un bucket (via un compte admin)

```bash

```

```
[OUTPUT]

```


### Uploader un fichier

* [La commande à réaliser pour effecuter l'action demandée]

```bash

```

```
[OUTPUT]

```

### Uploader un répertoire

* [La commande à réaliser pour effecuter l'action demandée]

```bash

```

```
[OUTPUT]

```

### Lister le contenu d'un "repertoire"

* [La commande à réaliser pour effecuter l'action demandée]

```bash

```

```
[OUTPUT]

```

### Synchroniser un répertoire local de sa machine avec un bucket

* [La commande à réaliser pour effecuter l'action demandée]

```bash

```

```
[OUTPUT]

```

### Publier un fichier présent sur un bucket en générant un lien (url) temporaire

* [La commande à réaliser pour effecuter l'action demandée]

```bash

```

```
[OUTPUT]

```

### Supprimer un fichier

* [La commande à réaliser pour effecuter l'action demandée]

```bash

```

```
[OUTPUT]

```

### Vider un "repertoire"

* [La commande à réaliser pour effecuter l'action demandée]

```bash

```

```
[OUTPUT]

```

### Extraire uniquement les metadonnées d'un objet

* [La commande à réaliser pour effecuter l'action demandée]

```bash

```

### Vider le bucket

* [La commande à réaliser pour effecuter l'action demandée]

```bash

```

```
[OUTPUT]

```

---

