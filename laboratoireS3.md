# Laboratoire S3

## Installation et configuration du CLI

* [Installer le client git](https://git-scm.com/)
  * Git bash vous embarque de nombreuses commandes Linux utiles pour s'entrainer avec S3 (cat, grep, touch, ls)
* [Installation du CLI - v2](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
* [Configuration du CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html#getting-started-quickstart-existing)
  * Les clés vous ont été partagées par oneDrive
* [Gestion des profiles](https://docs.aws.amazon.com/cli/v1/userguide/cli-configure-files.html#cli-configure-files-format-profile)
  * Vous devez créer un profile du nom de votre équipe et l'utiliser pour toute les futures commandes
  ```
  aws s3 <la commande> --profile devopsteam<xx>
  ```

## IAM Policy

Voici la "policy" qui vous a été attribuée:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:ListAllMyBuckets",
            "Resource": "arn:aws:s3:::*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
            ],
            "Resource": "arn:aws:s3:::devopsteam01-i346/*" 
        }
    ]
}
```

## Exploiter un S3

Attention:
* Vous devez utiliser la v2 du CLI
* Le client offre soit la commande s3, soit s3api. En priorité vous devez essayer "s3".

### Créer un bucket

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* Le bucket existe-t-il ?

```bash
aws s3 ls --profile devopsteam01-i346 | grep "devopsteam01"
```

```
[OUTPUT]
2025-01-27 22:23:30 devopsteam01-i346
2025-01-27 22:28:03 devopsteam02-i346
2025-01-27 22:28:05 devopsteam03-i346
2025-01-27 22:28:06 devopsteam04-i346
2025-01-27 22:28:08 devopsteam05-i346
2025-01-27 22:28:09 devopsteam06-i346
2025-01-27 22:28:11 devopsteam07-i346
2025-01-27 22:28:13 devopsteam08-i346
2025-01-27 22:28:14 devopsteam09-i346
2025-01-27 22:28:16 devopsteam10-i346
2025-02-03 19:32:33 devopsteam99-i346
```

* Créer un bucket (via un compte admin)

```bash
aws s3 mb s3://devopsteam99-i346 --region eu-central-1 --profile s3-admin
```

```
[OUTPUT]
make_bucket: devopsteam99-i346
```


### Uploader un fichier

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3 ls s3://devopsteam99-i346 ^
--profile devopsteam99-i346
```

```
[OUTPUT]
<empty>

```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 cp fileToUpload.txt s3://devopsteam99-i346/fileToUpload.txt ^
--profile devopsteam99-i346
```

```
[OUTPUT]
upload: .\fileToUpload.txt to s3://devopsteam99-i346/fileToUpload.txt
```

### Uploader un répertoire

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3 ls s3://devopsteam99-i346 ^
--profile devopsteam99-i346
```

```
[OUTPUT]
2025-02-23 09:09:10          0 fileToUpload.txt
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 cp folderToUpload s3://devopsteam99-i346/folderToUpload ^
--recursive ^
--profile devopsteam99-i346
```

```
[OUTPUT]
upload: folderToUpload\bob.txt to s3://devopsteam99-i346/folderToUpload/bob.txt
upload: folderToUpload\script.sql to s3://devopsteam99-i346/folderToUpload/script.sql
```

### Lister le contenu d'un "repertoire"

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3 ls s3://devopsteam99-i346 ^
--recursive ^
--profile devopsteam99-i346
```

```
[OUTPUT]
2025-02-23 09:09:10          0 fileToUpload.txt
2025-02-23 09:10:21          0 folderToUpload/bob.txt
2025-02-23 09:10:21          0 folderToUpload/script.sql
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 ls s3://devopsteam99-i346 ^
--recursive ^
--profile devopsteam99-i346
```

```
[OUTPUT]
2025-02-23 09:09:10          0 fileToUpload.txt
2025-02-23 09:10:21          0 folderToUpload/bob.txt
2025-02-23 09:10:21          0 folderToUpload/script.sql
```

### Synchroniser un répertoire local de sa machine avec un bucket

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3 ls s3://devopsteam99-i346 ^
--recursive ^
--profile devopsteam99-i346
```

```
[OUTPUT]
2025-02-23 09:09:10          0 fileToUpload.txt
2025-02-23 09:10:21          0 folderToUpload/bob.txt
2025-02-23 09:10:21          0 folderToUpload/script.sql
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 sync . s3://devopsteam99-i346/ ^
--profile devopsteam99-i346
```

```
[OUTPUT]
upload: .\Airplane-Transponder.jpg to s3://devopsteam99-i346/Airplane-Transponder.jpg
```

### Publier un fichier présent sur un bucket en générant un lien (url) temporaire

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3api head-object ^
--bucket devopsteam99-i346 ^
--key Airplane-Transponder.jpg ^
--profile devopsteam99-i346
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-23T08:12:59+00:00",
    "ContentLength": 17010,
    "ETag": "\"d0194f28e675232be0018b34d760fb92\"",
    "ContentType": "image/jpeg",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 presign s3://devopsteam99-i346/Airplane-Transponder.jpg ^
--expires-in 60 ^
--region eu-central-1 ^
--profile devopsteam99-i346
```

```
[OUTPUT]
https://devopsteam99-i346.s3.eu-central-1.amazonaws.com/Airplane-Transponder.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA2KFJKL4O6EAOCHBR%2F20250223%2Feu-central-1%2Fs3%2Faws4_request&X-Amz-Date=20250223T081917Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Signature=674d4a08094ad410c871d26aeb8a9166d267d798c6c633fb2b07ba7ee734e068
```

### Supprimer un fichier

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3api head-object ^
--bucket devopsteam99-i346 ^
--key fileToUpload.txt ^
--profile devopsteam99-i346
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-23T17:00:50+00:00",
    "ContentLength": 0,
    "ETag": "\"d41d8cd98f00b204e9800998ecf8427e\"",
    "ContentType": "text/plain",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 rm s3://devopsteam99-i346/fileToUpload.txt ^
--profile devopsteam99-i346
```

```
[OUTPUT]
delete: s3://devopsteam99-i346/fileToUpload.txt
```

### Vider un "repertoire"

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3 ls s3://devopsteam99-i346/folderToUpload ^
--recursive ^
--profile devopsteam99-i346
```

```
[OUTPUT]
2025-02-23 09:10:21          0 folderToUpload/bob.txt
2025-02-23 09:10:21          0 folderToUpload/script.sql
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 rm s3://devopsteam99-i346/folderToUpload ^
--recursive ^
--profile devopsteam99-i346
```

```
[OUTPUT]
delete: s3://devopsteam99-i346/folderToUpload/script.sql
delete: s3://devopsteam99-i346/folderToUpload/bob.txt
```

### Extraire uniquement les metadonnées d'un objet

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3api head-object ^
--bucket devopsteam99-i346 ^
--key Airplane-Transponder.jpg ^
--profile devopsteam99-i346
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-23T08:32:02+00:00",
    "ContentLength": 17010,
    "ETag": "\"d0194f28e675232be0018b34d760fb92\"",
    "ContentType": "image/jpeg",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3api get-object-attributes ^
--bucket devopsteam99-i346 ^
--key Airplane-Transponder.jpg ^
--object-attributes ObjectSize ^
--profile devopsteam99-i346
```

```
[OUTPUT]
{
{
    "LastModified": "2025-02-23T08:32:02+00:00",
    "ObjectSize": 17010
}
```

### Vider le bucket

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3 ls s3://devopsteam99-i346/ ^
--recursive ^
--profile devopsteam99-i346
```

```
[OUTPUT]
2025-02-23 09:32:02      17010 Airplane-Transponder.jpg
2025-02-23 09:09:10          0 fileToUpload.txt
2025-02-23 09:32:01          0 folderToUpload/bob.txt
2025-02-23 09:32:02          0 folderToUpload/script.sql
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 rm s3://devopsteam99-i346/ ^
--recursive ^
--profile devopsteam99-i346
```

```
[OUTPUT]
delete: s3://devopsteam99-i346/folderToUpload/bob.txt
delete: s3://devopsteam99-i346/folderToUpload/script.sql
delete: s3://devopsteam99-i346/fileToUpload.txt
delete: s3://devopsteam99-i346/Airplane-Transponder.jpg
```

---

## Questions d'analyse

Consigne : répondre en utilisant des sources officielles et en vous appuyant dessus pour répondre.

### Pourquoi est-il déconseillé de détruire un bucket S3 selon AWS ?

* [Sources AWS](https://docs.aws.amazon.com/fr_fr/AmazonS3/latest/userguide/delete-bucket.html)

si nous détruisons un bucket S3 avec le nom d'une personne et que la personne le recréer nous ne pouvons plus acceder au contenu de ce bucket.

### Quelle est la différence entre un Bucket S3 et Glacier ?

* [Sources AWS](https://managedserver.fr/aws-s3-et-aws-glacier-quelles-sont-les-diff%C3%A9rences/#La_differenza_di_prezzo_tra_Amazon_S3_e_Amazon_Glacier)

S3 est conçu pour l'archivage à long terme des données qui doivent être disponibles rapidement, tandis que Glacier est spécifiquement conçu pour l'archivage à long terme des données rarement utilisées.

### Reprenez l'IAM "Policy" et expliquer ce que vous pouvez en déduire au niveau des droits qui vous sont alloués

Consigne : Reprenez la "policy" et documenter chaque ligne

```json
{
    "Version": "2012-10-17", //la date de la version
    "Statement": [
        {
            "Effect": "Allow", //laisse un effet
            "Action": "s3:ListAllMyBuckets", //list tout les buckets qui existe
            "Resource": "arn:aws:s3:::*" //Cela désigne toutes les ressources dans le service Amazon S3
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
            ],
            "Resource": "arn:aws:s3:::devopsteam01-i346/*" 
        }
    ]
}
```



