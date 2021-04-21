---
keywords: Experience Platform;home;argomenti popolari;elenco sandbox
solution: Experience Platform
title: Elencare sandbox nell’API
topic-legacy: developer guide
description: Per elencare tutte le sandbox appartenenti alla tua organizzazione IMS (attive o meno), invia una richiesta GET all’endpoint /sandbox.
exl-id: 5e7dc6e7-cb9c-41e0-a3ad-025b625f14ec
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%

---

# Elencare sandbox nell’API

Per elencare tutte le sandbox appartenenti all’organizzazione IMS (attive o meno), invia una richiesta di GET all’endpoint `/sandboxes`.

**Formato API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parametri di query opzionali per filtrare i risultati in base a. Per ulteriori informazioni, consulta la sezione sui [parametri di query](#query) . |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di sandbox appartenenti all’organizzazione, inclusi dettagli quali `name`, `title`, `state` e `type`.

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
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform-int.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della sandbox. Utilizzato a scopo di ricerca nelle chiamate API. |
| `title` | Nome visualizzato della sandbox. |
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <br/><ul><li>**creazione**: La sandbox è stata creata, ma viene comunque fornita dal sistema.</li><li>**attivo**: La sandbox viene creata e attiva.</li><li>**non riuscito**: A causa di un errore, il sistema non è in grado di eseguire il provisioning della sandbox ed è disabilitato.</li><li>**eliminato**: La sandbox è stata disabilitata manualmente.</li></ul> |
| `type` | Il tipo di sandbox, &quot;sviluppo&quot; o &quot;produzione&quot;. |
| `isDefault` | Proprietà booleana che indica se questa sandbox è la sandbox predefinita per l’organizzazione. In genere si tratta della sandbox di produzione. |
| `eTag` | Identificatore per una versione specifica della sandbox. Utilizzato per il controllo delle versioni e l’efficienza del caching, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |

## Utilizzo dei parametri di query {#query}

L&#39;API [[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) supporta l&#39;utilizzo di parametri di query per la pagina e filtrare i risultati durante l&#39;elenco delle sandbox.

>[!NOTE]
>
>I parametri di query `limit` e `offset` devono essere specificati insieme. Se ne specifichi una sola, l’API restituirà un errore. Se non specificate nessuno, il limite predefinito è 50 e l&#39;offset è 0.

| Parametro | Descrizione |
| --------- | ----------- |
| `limit` | Il numero massimo di record da restituire nella risposta. |
| `offset` | Il numero di entità dal primo record da cui avviare (offset) l&#39;elenco di risposte. |
