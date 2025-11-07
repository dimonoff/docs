# Transfert de fichiers

Un transfert de fichiers peut se faire dans deux directions: de Fundamentum vers un ou des appareil(s),
ou d'un appareil vers Fundamentum.

## Transfert d'un ou plusieurs fichier(s) de Fundamentum vers un ou des appareil(s)

### En utilisant l'API

Vue d'ensemble

![Vue d'ensemble du transfert de fichiers](../.gitbook/assets/file-transfer-cloud-to-device.svg)

Étapes détaillées:

1. Créer le transfert
   - Appelez l'[API](https://api.fundamentum-iot.com/docs#/operations/storeFileTransfer) pour créer un transfert avec la direction cloud-to-device 
   - Spécifiez la liste de fichiers que vous souhaitez transférer
   - Spécifiez la liste d'appareils auquel vous souhaitez transférer les fichiers
   - Le service vous retournera le transfert ainsi qu'une url de téléversement pour chacun des fichiers spécifiés

2. Téléverser le ou les fichier(s) à transférer
   - Pour chacun des fichiers indiqués dans le transfert: téléversez à l'aide de l'url présignée précédemment obtenue

   ```shell
   curl --upload-file {CHEMIN_VERS_VOTRE_FICHIER} {URL_DE_TELEVERSEMENT}
   ```
   
3. Exécuter le transfert
   - Appelez l'[API](https://api.fundamentum-iot.com/docs#/operations/executeFileTransfer) avec l'identifiant du transfert créé précédemment
   - Les fichiers à transférer doivent tous être téléversés
   - Les fichiers seront ensuite envoyés au(x) appareil(s) spécifié(s)
   - Le edge daemon de chaque appareil recevra le transfert et émettra un évènement GRPC
   - Sur chaque appareil, vous devez avoir un programme qui écoute cet évènement GRPC, accepte le transfert, et télécharge le fichier à l'endroit spécifié
   - Vous pouvez voir le résultat du transfert dans l'onglet Actions de la page de votre appareil dans le Fundamentum Hub

### En utilisant le CLI de Fundamentum

Le CLI vous permet d'envoyer un seul fichier à un seul appareil. Il exécute les 3 étapes précédentes en une seule commmande.
Il faut d'abord authentifier le CLI:

```shell
fun login

fun devices transfer cloud-to-device -d {ID_DE_VOTRE_APPAREIL} -p {ID_DU_PROJET_DE_VOTRE_APPAREIL} \
   -r {ID_DU_REGISTRE_DE_VOTRE_APPAREIL} -f {CHEMIN_LOCAL_DU_FICHIER_À_TRANSFÉRER} \
   --remote-path {CHEMIN_SUR_L_APPAREIL_OÙ_SERA_SAUVEGARDÉ_LE_FICHIER} --context {CONTEXT_D_AUTHENTIFICATION_DU_CLI}
```

## Transfert d'un ou plusieurs fichier(s) d'un appareil vers Fundamentum

### En utilisant l'API

Vue d'ensemble

![Vue d'ensemble du transfert de fichiers](../.gitbook/assets/file-transfer-device-to-cloud.svg)

Étapes détaillées:

1. Créer le transfert
   - Appelez l'[API](https://api.fundamentum-iot.com/docs#/operations/storeFileTransfer) pour créer un transfert avec la direction device-to-cloud
   - Vous ne pouvez cibler qu'un seul appareil
   - Vous ne pouvez demander qu'un seul fichier
   
2. Exécuter le transfert
   - Appelez l'[API](https://api.fundamentum-iot.com/docs#/operations/executeFileTransfer) avec l'identifiant du transfert créé précédemment
   - La requête du fichier demandé sera envoyé à l'appareil spécifié
   - Le edge daemon de l'appareil recevra le transfert et émettra un évènement GRPC
   - Sur l'appareil, vous devez avoir un programme qui écoute cet évènement GRPC, accepte le transfert, et y téléverse le fichier depuis l'endroit spécifié

3. Demander les fichiers (polling)
   - Appelez l'[API](https://api.fundamentum-iot.com/docs#/operations/getFileTransferFiles) avec l'identifiant du transfert créé précédemment
   - Si le fichier a été téléversé par l'appareil, cet API vous retournera l'url de téléchargement de celui-ci
   - Répétez cet appel plusieurs fois jusqu'à ce que vous obteniez l'url
   - Téléchargez le fichier depuis cet url

   ```shell
   curl -o {CHEMIN_OÙ_VOUS_VOULEZ_SAUVEGARDER_LE_FICHIER} {URL_DE_TÉLÉCHARGEMENT}
   ```

### En utilisant le CLI de Fundamentum

Le CLI vous permet de demander un fichier à un appareil. Il exécute les 3 étapes précédentes en une seule commmande.
Il faut d'abord authentifier le CLI:

```shell
fun login

fun devices transfer cloud-to-device -d {ID_DE_VOTRE_APPAREIL} -p {ID_DU_PROJET_DE_VOTRE_APPAREIL} \
   -r {ID_DU_REGISTRE_DE_VOTRE_APPAREIL} -f {CHEMIN_LOCAL_DU_FICHIER_À_TRANSFÉRER} \
   --remote-path {CHEMIN_SUR_L_APPAREIL_OÙ_SERA_SAUVEGARDÉ_LE_FICHIER} --context {CONTEXT_D_AUTHENTIFICATION_DU_CLI}
```