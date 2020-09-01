---
keywords: Experience Platform;home;popular topics;list sandboxes
solution: Experience Platform
title: Elenca tutte le sandbox
topic: developer guide
description: Per elencare tutte le sandbox appartenenti all’organizzazione IMS (attive o meno), effettuate una richiesta di GET all’endpoint /sandbox.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 1%

---


# Elenca tutte le sandbox

Per elencare tutte le sandbox appartenenti all’organizzazione IMS (attive o meno), effettuate una richiesta di GET all’ `/sandboxes` endpoint.

**Formato API**

```http
GET /sandboxes
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di sandbox appartenenti alla vostra organizzazione, con dettagli quali `name`, `title`, `state`e `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della sandbox. Utilizzata a scopo di ricerca nelle chiamate API. |
| `title` | Nome visualizzato per la sandbox. |
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <br/><ul><li>**creazione**: La sandbox è stata creata, ma viene ancora fornita dal sistema.</li><li>**active**: La sandbox viene creata e attiva.</li><li>**non riuscito**: A causa di un errore, il provisioning della sandbox non è stato eseguito dal sistema ed è disabilitato.</li><li>**eliminato**: La sandbox è stata disattivata manualmente.</li></ul> |
| `type` | Il tipo di sandbox, &quot;development&quot; o &quot;production&quot;. |
| `isDefault` | Una proprietà booleana che indica se questa sandbox è la sandbox predefinita per l&#39;organizzazione. In genere si tratta della sandbox di produzione. |
| `eTag` | Identificatore per una versione specifica della sandbox. Utilizzato per il controllo della versione e l&#39;efficienza del caching, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |
