---
keywords: ' Experience Platform;home;argomenti comuni;autorizzazioni di controllo degli accessi;tipi di risorse di controllo degli accessi;access control api'
solution: Experience Platform
title: Endpoint API di riferimento
topic: developer guide
description: Il controllo degli accessi in Adobe Experience Platform consente di gestire ruoli e autorizzazioni per diverse funzionalità della piattaforma utilizzando l'Adobe Admin Console. Potete elencare i nomi di tutte le autorizzazioni e i tipi di risorse eseguendo una richiesta di GET all'endpoint /acl/reference nell'API di controllo di accesso. Questi nomi possono quindi essere utilizzati nelle chiamate API per visualizzare i criteri effettivi per l'utente corrente.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---


# Endpoint di riferimento

Puoi elencare i nomi di tutte le autorizzazioni e i tipi di risorse effettuando una richiesta di GET all&#39;endpoint `/acl/reference`. Questi nomi possono quindi essere utilizzati nelle chiamate API per [visualizzare criteri effettivi](./effective-policies.md) per l&#39;utente corrente.

Un&#39;autorizzazione è un criterio gestito tramite Adobe Admin Console e viene mappata a zero o più criteri di tipo risorsa. Un tipo di risorsa è un criterio che abilita funzionalità di lettura, scrittura e/o eliminazione per un tipo specifico di risorsa [!DNL Platform] (ad esempio set di dati o schemi).

**Formato API**

```http
GET /acl/reference
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Risposta**

Una risposta corretta restituisce un oggetto `permissions` e un oggetto `resource-types`, ciascuno dei quali contiene un elenco completo di nomi per le autorizzazioni di accesso o i tipi di risorse, rispettivamente.

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
