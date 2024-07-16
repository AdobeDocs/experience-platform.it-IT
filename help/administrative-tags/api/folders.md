---
title: Endpoint cartelle
description: Scopri come creare, aggiornare, gestire ed eliminare cartelle utilizzando le API di Adobe Experience Platform.
role: Developer
exl-id: ee43d699-725d-4ffd-a71b-049eeb3b4d7c
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 5%

---

# Endpoint &quot;cartelle&quot;

>[!IMPORTANT]
>
>L&#39;URL dell&#39;endpoint per questo set di endpoint è `https://experience.adobe.io`.

Le cartelle sono una funzionalità che consente di organizzare meglio gli oggetti aziendali per facilitarne la navigazione e la classificazione.

Questa guida fornisce informazioni utili per comprendere meglio le cartelle e include esempi di chiamate API per eseguire azioni di base utilizzando l’API.

## Introduzione

Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, incluse le intestazioni richieste e la lettura delle chiamate API di esempio.

## Recuperare un elenco di cartelle {#list}

Per recuperare un elenco di cartelle appartenenti alla tua organizzazione, devi eseguire una richiesta di GET all&#39;endpoint `/folder` e specificare il tipo di cartella e l&#39;ID della cartella principale.

**Formato API**

```http
GET /folder/{FOLDER_TYPE}/{PARENT_FOLDER_ID}/subfolders
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Tipo di oggetti contenuti nella cartella. I valori supportati sono `segment` e `dataset`. |
| `{PARENT_FOLDER_ID}` | ID della cartella principale da cui stai recuperando l’elenco delle cartelle. Per visualizzare un elenco di tutte le cartelle padre, utilizzare l&#39;ID cartella `root`. |

**Richiesta**

+++Una richiesta di esempio per elencare tutte le cartelle di set di dati di livello principale

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/root/subfolders
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di tutte le cartelle di livello principale per il set di dati nell’organizzazione.

+++Risposta di esempio contenente un elenco di tutte le cartelle di livello principale per il set di dati nell’organizzazione.

```json
{
    "id": "c626b4f7-223b-4486-8900-00c266e31dd1",
    "name": "ParentFolder",
    "noun": "Dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": null,
    "createdAt": "2023-01-12T03:31:00.118+00:00",
    "modifiedBy": null,
    "modifiedAt": "2023-01-13T05:47:06.718+00:00",
    "_links": null,
    "children": [
        {
            "id": "09d86b23-4819-471b-8a2a-05774ed268de",
            "name": "ChildFolder.1",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-12T12:51:39.284+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-12T12:51:39.284+00:00",
            "_links": null,
            "children": []
        },
        {
            "id": "fd2f6a68-ef65-470d-ab31-b02b7b2241ca",
            "name": "ChildFolder.2",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-13T03:38:40.006+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-13T03:38:40.006+00:00",
            "_links": null,
            "children": []
        }
    ]
}
```

+++

## Crea una nuova cartella {#create}

Per creare una nuova cartella, eseguire una richiesta POST all&#39;endpoint `/folder` e specificare il tipo di cartella.

**Formato API**

```http
POST /folder/{FOLDER_TYPE}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Tipo di oggetti contenuti nella cartella. I valori supportati sono `segment` e `dataset`. |

**Richiesta**

+++Richiesta di esempio per creare una nuova cartella.

```shell
curl -X POST https://experience.adobe.io/unifiedfolders/folder/dataset
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "name": "SampleFolder",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5"
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Nome della cartella da creare. |
| `parentId` | ID della cartella principale. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della cartella appena creata.

+++Risposta di esempio contenente i dettagli della cartella appena creata.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": null
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | ID della cartella appena creata. |
| `createdBy` | ID dell&#39;utente che ha creato la cartella. |
| `createdAt` | Il timestamp di quando è stata creata la cartella. |
| `modifiedBy` | ID dell’ultimo utente che ha modificato la cartella. |
| `modifiedAt` | Il timestamp dell’ultimo aggiornamento della cartella. |

+++

## Recuperare una cartella specifica {#get}

Per recuperare una cartella specifica appartenente alla tua organizzazione, devi eseguire una richiesta di GET all&#39;endpoint `/folder` e specificare il tipo di cartella e l&#39;ID della cartella.

**Formato API**

```http
GET /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Tipo di oggetti contenuti nella cartella. I valori supportati sono `segment` e `dataset`. |
| `{FOLDER_ID}` | ID della cartella da recuperare. |

**Richiesta**

+++Richiesta di esempio per recuperare una cartella specifica

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della cartella richiesta.

+++Risposta di esempio contenente i dettagli della cartella richiesta.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | ID della cartella richiesta. |
| `name` | Nome della cartella richiesta. |
| `parentId` | ID della cartella principale. |
| `createdBy` | ID dell&#39;utente che ha creato la cartella. |
| `createdAt` | Il timestamp di quando è stata creata la cartella. |
| `modifiedBy` | ID dell’ultimo utente che ha aggiornato la cartella. |
| `modifiedAt` | Il timestamp dell’ultimo aggiornamento della cartella. |
| `status` | Stato della cartella richiesta. I valori supportati includono `IN_USE` e `ARCHIVED`. |

+++

## Convalida una cartella specificata {#validate}

È possibile verificare se una cartella è idonea a contenere oggetti effettuando una richiesta di GET all&#39;endpoint `/folder/{FOLDER_TYPE}/{FOLDER_ID}/validate` e fornendo sia il tipo di cartella che l&#39;ID.

**Formato API**

```http
GET /folder/{FOLDER_TYPE}/{FOLDER_ID}/validate
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Tipo di oggetti contenuti nella cartella. I valori supportati sono `segment` e `dataset`. |
| `{FOLDER_ID}` | ID della cartella da convalidare. |

**Richiesta**

+++Richiesta di esempio per convalidare una cartella specifica

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, lo stato HTTP 200 restituisce i dettagli della cartella da convalidare.

+++Una risposta di esempio contiene i dettagli della cartella convalidata

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

+++

## Aggiornare una cartella specifica {#update}

Per aggiornare i dettagli di una cartella specifica appartenente alla tua organizzazione, devi eseguire una richiesta PATCH all&#39;endpoint `/folder` e specificare il tipo di cartella e l&#39;ID della cartella.

**Formato API**

```http
PATCH /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Tipo di oggetti contenuti nella cartella. I valori supportati sono `segment` e `dataset`. |
| `{FOLDER_ID}` | ID della cartella da aggiornare. |

**Richiesta**

+++Richiesta di esempio per aggiornare una cartella specifica

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '[{
    "op": "replace",
    "path": "/name",
    "value": "RenamedSampleFolder"
 }]'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sulla cartella appena aggiornata.

```json
{
    "id": "eafab5bf-3457-4b7f-b366-3c5399bd98f1",
    "name": "RenamedSampleFolder",
    "noun": "dataset",
    "parentFolderId": null,
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "183807A65A0F5D180A494004@AdobeID",
    "createdAt": "2024-03-05T01:42:36.910+00:00",
    "modifiedBy": "183807A65A0F5D180A494004@AdobeID",
    "modifiedAt": "2024-03-05T01:45:54.740+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/eafab5bf-3457-4b7f-b366-3c5399bd98f1"
        }
    },
    "namespace": null
}
```

## Eliminare una cartella specifica {#delete}

Per eliminare una cartella specifica appartenente alla tua organizzazione, devi eseguire una richiesta DELETE a `/folder` e specificare il tipo di cartella e l&#39;ID della cartella.

***Formato API**

```http
DELETE /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Tipo di oggetti contenuti nella cartella. I valori supportati sono `segment` e `dataset`. |
| `{FOLDER_ID}` | ID della cartella da eliminare. |

**Richiesta**

+++Richiesta di esempio per eliminare una cartella specifica

```shell
curl -X DELETE https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un corpo del messaggio che informa dell’eliminazione della cartella.

```json
{
    "message": "delete request accepted successfully"
}
```

## Passaggi successivi

Dopo aver letto questa guida, avrai acquisito maggiori conoscenze su come creare, gestire ed eliminare cartelle utilizzando l’API di Adobe Experience Platform.
