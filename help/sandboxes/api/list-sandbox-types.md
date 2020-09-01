---
keywords: Experience Platform;home;popular topics;list sandboxes
solution: Experience Platform
title: Elenca i tipi di sandbox supportati
topic: developer guide
description: Potete recuperare un elenco dei tipi di sandbox supportati per la vostra organizzazione effettuando una richiesta di GET all'endpoint /sandboxTypes.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 2%

---


# Elenca i tipi di sandbox supportati

Potete recuperare un elenco dei tipi di sandbox supportati per la vostra organizzazione effettuando una richiesta di GET all&#39; `/sandboxTypes` endpoint.

**Formato API**

```http
GET /sandboxTypes
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di tipi di sandbox supportati dalla vostra organizzazione.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
