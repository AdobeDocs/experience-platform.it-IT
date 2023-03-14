---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;data model;audit;audit log;changelog;change log;rpc;
solution: Experience Platform
title: Endpoint API registro di controllo
description: L’endpoint /auditlog nell’API Schema Registry consente di recuperare un elenco cronologico delle modifiche apportate a una risorsa XDM esistente.
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 5%

---

# Endpoint del registro di controllo

Per ogni risorsa Experience Data Model (XDM), [!DNL Schema Registry] mantiene un registro di tutte le modifiche che si sono verificate tra diversi aggiornamenti. Il `/auditlog` endpoint nella [!DNL Schema Registry] API consente di recuperare un registro di audit per qualsiasi classe, gruppo di campi di schema, tipo di dati o schema specificato da ID.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[[!DNL Schema Registry] API di ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Prima di continuare, controlla [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

Il `/auditlog` l&#39;endpoint fa parte delle chiamate di procedura remota (RPC) supportate dalla [!DNL Schema Registry]. A differenza di altri endpoint nel [!DNL Schema Registry] API, gli endpoint RPC non richiedono intestazioni aggiuntive come `Accept` o `Content-Type`, e non utilizzare un `CONTAINER_ID`. Devono invece utilizzare il `/rpc` dello spazio dei nomi, come dimostrato nella chiamata API di seguito.

## Recuperare un registro di controllo per una risorsa

È possibile recuperare un registro di controllo per qualsiasi classe, gruppo di campi, tipo di dati o schema all&#39;interno della raccolta schemi specificando l&#39;ID della risorsa nel percorso di una richiesta di GET al `/auditlog` endpoint.

**Formato API**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{RESOURCE_ID}` | Il `meta:altId` o con codifica URL `$id` della risorsa di cui desideri recuperare il registro di controllo. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera il registro di audit per uno schema.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco cronologico delle modifiche apportate alla risorsa, dal più recente al meno recente.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "a14NMF0jd6BIfyXaHdTDl4bC4R0r9rht",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
        "xdmType": "schemas",
        "action": "remove",
        "path": "/meta:usageCount",
        "value": 0
      }
    ]
  },
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "pFQbgmWrdbJrNB9GdxTSGECpXYWspu68",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltySunday_ABC",
        "value": {
          "title": "LoyaltySundayABC",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltyMoxee_XYZ",
        "value": {
          "title": "LoyaltyMoxeeXYZ",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      }
    ]
  }
]
```

| Proprietà | Descrizione |
| --- | --- |
| `updates` | Matrice di oggetti, in cui ogni oggetto rappresenta una modifica apportata alla risorsa specificata o a una delle relative risorse dipendenti. |
| `id` | Il `$id` della risorsa che è stata modificata. Questo valore rappresenta in genere la risorsa specificata nel percorso della richiesta, ma può rappresentare una risorsa dipendente se questa è l’origine della modifica. |
| `xdmType` | Tipo di risorsa modificato. |
| `action` | Tipo di modifica apportata. |
| `path` | A [Puntatore JSON](../../landing/api-fundamentals.md#json-pointer) stringa che indica il percorso del campo specifico modificato o aggiunto. |
| `value` | Valore assegnato al campo nuovo o aggiornato. |

{style="table-layout:auto"}
