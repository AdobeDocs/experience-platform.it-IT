---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Nomi elenco di autorizzazioni e tipi di risorse
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 1%

---


# Nomi elenco di autorizzazioni e tipi di risorse

Potete elencare i nomi di tutte le autorizzazioni e i tipi di risorse effettuando una richiesta di GET all&#39; `/acl/reference` endpoint. Questi nomi possono quindi essere utilizzati nelle chiamate API per [visualizzare i criteri](./effective-policies.md) effettivi per l&#39;utente corrente.

Un&#39; **autorizzazione** è un criterio gestito tramite Adobe Admin Console e mappato a zero o più criteri di tipo risorsa. Un tipo **di** risorsa è un criterio che abilita funzionalità di lettura, scrittura e/o eliminazione per un tipo specifico di [!DNL Platform] risorsa (ad esempio set di dati o schemi).

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

Una risposta corretta restituisce un `permissions` oggetto e un `resource-types` oggetto, ciascuno contenente un elenco completo di nomi per le autorizzazioni di accesso o i tipi di risorse, rispettivamente.

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
