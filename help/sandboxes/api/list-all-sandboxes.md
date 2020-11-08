---
keywords: Experience Platform;home;popular topics;list sandboxes
solution: Experience Platform
title: Elenca tutte le sandbox
topic: developer guide
description: Per elencare tutte le sandbox appartenenti all’organizzazione IMS (attive o meno), effettuate una richiesta di GET all’endpoint /sandbox.
translation-type: tm+mt
source-git-commit: 6326b3072737acf30ba2aee7081ce28dc9627a9a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 2%

---


# Elenca tutte le sandbox

Per elencare tutte le sandbox appartenenti all’organizzazione IMS (attive o meno), effettuate una richiesta di GET all’ `/sandboxes` endpoint.

**Formato API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parametri di query facoltativi per filtrare i risultati per. Per ulteriori informazioni, consulta la sezione sui parametri [di](#query) query. |

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
| `name` | Nome della sandbox. Utilizzata a scopo di ricerca nelle chiamate API. |
| `title` | Nome visualizzato per la sandbox. |
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <br/><ul><li>**creazione**: La sandbox è stata creata, ma viene ancora fornita dal sistema.</li><li>**active**: La sandbox viene creata e attiva.</li><li>**non riuscito**: A causa di un errore, il provisioning della sandbox non è stato eseguito dal sistema ed è disabilitato.</li><li>**eliminato**: La sandbox è stata disattivata manualmente.</li></ul> |
| `type` | Il tipo di sandbox, &quot;development&quot; o &quot;production&quot;. |
| `isDefault` | Una proprietà booleana che indica se questa sandbox è la sandbox predefinita per l&#39;organizzazione. In genere si tratta della sandbox di produzione. |
| `eTag` | Identificatore per una versione specifica della sandbox. Utilizzato per il controllo della versione e l&#39;efficienza del caching, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |

## Utilizzo dei parametri di query {#query}

L&#39; [[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) API supporta l&#39;utilizzo di parametri di query per visualizzare la pagina e filtrare i risultati quando vengono elencate le sandbox.

>[!NOTE]
>
>I parametri `limit` e di `offset` query devono essere specificati insieme. Se ne specificate solo uno, l&#39;API restituirà un errore. Se non si specifica alcun valore, il limite predefinito è 50 e l&#39;offset è 0.

| Parametro | Descrizione |
| --------- | ----------- |
| `limit` | Il numero massimo di record da restituire nella risposta. |
| `offset` | Il numero di entità dal primo record da cui iniziare (offset) l&#39;elenco di risposte. |