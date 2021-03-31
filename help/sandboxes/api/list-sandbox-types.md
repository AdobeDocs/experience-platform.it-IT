---
keywords: Experience Platform;home;argomenti popolari;elenco sandbox
solution: Experience Platform
title: Elencare i tipi di sandbox supportati nell’API
topic: guida per sviluppatori
description: Puoi recuperare un elenco dei tipi di sandbox supportati per la tua organizzazione effettuando una richiesta GET all’endpoint /sandboxTypes .
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '83'
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
