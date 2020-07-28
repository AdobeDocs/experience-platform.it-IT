---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Elenca i tipi di sandbox supportati
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 4%

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
