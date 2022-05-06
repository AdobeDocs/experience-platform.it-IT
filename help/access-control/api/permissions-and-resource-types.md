---
keywords: Experience Platform;home;argomenti popolari;autorizzazioni di controllo accessi;tipi di risorse di controllo accessi;api di controllo accessi
solution: Experience Platform
title: Endpoint API di riferimento
topic-legacy: developer guide
description: Il controllo degli accessi in Adobe Experience Platform consente di gestire ruoli e autorizzazioni per varie funzionalità di Platform utilizzando Adobe Admin Console. È possibile elencare i nomi di tutte le autorizzazioni e i tipi di risorse effettuando una richiesta GET all'endpoint /acl/reference nell'API di controllo di accesso. Questi nomi possono quindi essere utilizzati nelle chiamate API per visualizzare i criteri efficaci per l’utente corrente.
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 2%

---

# Endpoint di riferimento

È possibile elencare i nomi di tutte le autorizzazioni e i tipi di risorse effettuando una richiesta GET al `/acl/reference` punto finale. Questi nomi possono quindi essere utilizzati nelle chiamate API a [visualizzare politiche efficaci](./effective-policies.md) per l&#39;utente corrente.

Un&#39;autorizzazione è un criterio gestito tramite Adobe Admin Console e viene mappata a zero o più criteri di tipo risorsa. Un tipo di risorsa è un criterio che abilita le funzionalità di lettura, scrittura e/o eliminazione per un tipo specifico di [!DNL Platform] risorsa (ad esempio set di dati o schemi).

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
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Risposta**

Una risposta corretta restituisce un `permissions` oggetto e `resource-types` oggetto , ciascuno contenente un elenco completo di nomi per le autorizzazioni di accesso o i tipi di risorse, rispettivamente.

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
