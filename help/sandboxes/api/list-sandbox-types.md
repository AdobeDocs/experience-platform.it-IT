---
keywords: Experience Platform ;home;argomenti più comuni;sandbox elenco
solution: Experience Platform
title: Elenca i tipi di sandbox supportati nell'API
topic: developer guide
description: Potete recuperare un elenco dei tipi di sandbox supportati per la vostra organizzazione effettuando una richiesta di GET all'endpoint /sandboxTypes.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 2%

---


# Elenca i tipi di sandbox supportati nell&#39;API

Potete recuperare un elenco dei tipi di sandbox supportati per la vostra organizzazione effettuando una richiesta di GET all&#39;endpoint `/sandboxTypes`.

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
