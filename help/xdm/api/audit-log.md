---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;audit;audit log;changelog;change log;rpc;
solution: Experience Platform
title: Guida all'endpoint del registro di controllo
description: L'endpoint /auditlog nell'API del Registro di sistema dello schema consente di recuperare un elenco cronologico delle modifiche apportate a una risorsa XDM esistente.
topic: developer guide
translation-type: tm+mt
source-git-commit: eb5e34dc3b48a6fe0757635cad1df08caa68b019
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---


# Endpoint del registro di controllo

Per ogni risorsa Experience Data Model (XDM), il [!DNL Schema Registry] mantiene un registro di tutte le modifiche che si sono verificate tra diversi aggiornamenti. L&#39;endpoint `/auditlog` nell&#39;API [!DNL Schema Registry] consente di recuperare un registro di controllo per qualsiasi classe, mixin, tipo di dati o schema specificato dall&#39;ID.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mixin-registry.yaml). Prima di continuare, consultare la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per eseguire correttamente chiamate a qualsiasi API  Experience Platform.

L&#39;endpoint `/auditlog` fa parte delle chiamate di routine remote (RPC) supportate da [!DNL Schema Registry]. A differenza di altri endpoint nell&#39;API [!DNL Schema Registry], gli endpoint RPC non richiedono intestazioni aggiuntive come `Accept` o `Content-Type` e non utilizzano un `CONTAINER_ID`. Devono invece utilizzare lo spazio dei nomi `/rpc`, come dimostrato nella chiamata API di seguito.

## Recupero di un registro di controllo per una risorsa

È possibile recuperare un registro di controllo per qualsiasi classe, mixin, tipo di dati o schema nella Libreria schema specificando l&#39;ID della risorsa nel percorso di una richiesta di GET all&#39;endpoint `/auditlog`.

**Formato API**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{RESOURCE_ID}` | `meta:altId` o `$id` con codifica URL della risorsa di cui si desidera recuperare il registro di controllo. |

**Richiesta**

La seguente richiesta recupera il registro di controllo per un mixin `Restaurant`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco cronologico delle modifiche apportate alla risorsa, dalla più recente alla meno recente.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
    "auditTrails": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/brand",
        "value": {
          "title": "Brand",
          "description": "",
          "type": "string",
          "isRequired": false,
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/meta:usageCount",
        "value": 0
      }
    ],
    "updatedUser": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 1606255582281,
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "{SANDBOX_ID}"
  }
]
```

| Proprietà | Descrizione |
| --- | --- |
| `auditTrails` | Un array di oggetti, con ogni oggetto che rappresenta una modifica apportata alla risorsa specificata o a una delle risorse dipendenti. |
| `id` | La `$id` della risorsa modificata. Questo valore rappresenta in genere la risorsa specificata nel percorso della richiesta, ma può rappresentare una risorsa dipendente se questa è l&#39;origine della modifica. |
| `action` | Tipo di modifica apportata. |
| `path` | Una stringa [JSON Pointer](../../landing/api-fundamentals.md#json-pointer) che indica il percorso del campo specifico che è stato modificato o aggiunto. |
| `value` | Valore assegnato al campo nuovo o aggiornato. |