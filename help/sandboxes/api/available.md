---
keywords: Experience Platform;home;argomenti popolari;elenco sandbox disponibili;elenco sandbox disponibili;list sandbox
solution: Experience Platform
title: Endpoint API sandbox disponibile
description: Per elencare le sandbox disponibili per l’utente corrente, effettua una richiesta GET all’endpoint sandbox disponibile.
role: Developer
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 3%

---

# Endpoint sandbox disponibile

>[!NOTE]
>
>A differenza di altri endpoint forniti nell’API Sandbox, questo endpoint è disponibile per tutti gli utenti, inclusi quelli senza autorizzazioni di accesso all’amministrazione Sandbox.

Per elencare le sandbox disponibili per l’utente corrente, effettua una richiesta GET all’endpoint sandbox disponibile.

**Formato API**

```http
GET /{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parametri di query facoltativi in base ai quali filtrare i risultati. Consulta la [documento dell&#39;appendice](./appendix.md#query) per un elenco dei parametri disponibili. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di sandbox disponibili per l’utente corrente, inclusi dettagli quali `name`, `title`, `state`, e `type`.

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
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <ul><li>`creating`: la sandbox è stata creata ma è ancora in fase di provisioning da parte del sistema.</li><li>`active`: la sandbox viene creata e attivata.</li><li>`failed`: a causa di un errore, non è stato possibile eseguire il provisioning della sandbox da parte del sistema ed è disabilitata.</li><li>`deleted`: la sandbox è stata disabilitata manualmente.</li></ul> |
| `type` | Il tipo di sandbox, &quot;sviluppo&quot; o &quot;produzione&quot;. |
| `isDefault` | Una proprietà booleana che indica se questa sandbox è la sandbox di produzione predefinita per l’organizzazione. |
| `eTag` | Identificatore di una versione specifica della sandbox. Utilizzato per il controllo delle versioni e l’efficienza della memorizzazione nella cache, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |
