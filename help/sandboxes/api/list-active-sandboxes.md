---
keywords: Experience Platform;home;argomenti popolari;elenco sandbox attive;elenco sandbox
solution: Experience Platform
title: Elencare sandbox attive per l’utente corrente nell’API
topic: guida per sviluppatori
description: È possibile elencare le sandbox attive per l’utente corrente effettuando una richiesta di GET all’endpoint principale.
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 2%

---


# Elencare le sandbox attive per l’utente corrente nell’API

>[!NOTE]
>
>A differenza di altri endpoint forniti nell’API Sandbox, questo endpoint è disponibile per tutti gli utenti, inclusi quelli senza autorizzazioni di accesso di amministrazione sandbox.

È possibile elencare le sandbox attive per l’utente corrente effettuando una richiesta di GET all’endpoint principale (`/`).

**Formato API**

```http
GET /{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parametri di query opzionali per filtrare i risultati in base a. Per ulteriori informazioni, consulta la sezione sui [parametri di query](#query) . |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

Una risposta corretta restituisce un elenco di sandbox attive per l’utente corrente, inclusi dettagli quali `name`, `title`, `state` e `type`.

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
        }
    ],
    "_page": {
        "limit": 3,
        "count": 1
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/?limit={limit}&offset={offset}",
            "templated": true
        }
    }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della sandbox. Utilizzato a scopo di ricerca nelle chiamate API. |
| `title` | Nome visualizzato della sandbox. |
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <ul><li>**creazione**: La sandbox è stata creata, ma viene comunque fornita dal sistema.</li><li>**attivo**: La sandbox viene creata e attiva.</li><li>**non riuscito**: A causa di un errore, il sistema non è in grado di eseguire il provisioning della sandbox ed è disabilitato.</li><li>**eliminato**: La sandbox è stata disabilitata manualmente.</li></ul> |
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
