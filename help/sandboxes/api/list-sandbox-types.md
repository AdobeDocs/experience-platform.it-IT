---
keywords: Experience Platform;home;argomenti popolari;elenco sandbox
solution: Experience Platform
title: Elencare i tipi di sandbox supportati nell’API
topic-legacy: developer guide
description: Puoi recuperare un elenco dei tipi di sandbox supportati per la tua organizzazione effettuando una richiesta GET all’endpoint /sandboxTypes .
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 2%

---

# Elencare i tipi di sandbox supportati nell’API

Puoi recuperare un elenco dei tipi di sandbox supportati per la tua organizzazione effettuando una richiesta di GET all’endpoint `/sandboxTypes` .

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

Una risposta corretta restituisce un elenco di tipi di sandbox supportati dalla tua organizzazione.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
