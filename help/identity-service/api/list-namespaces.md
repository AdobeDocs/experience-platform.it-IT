---
keywords: Experience Platform;home;argomenti popolari;elenco dei namespace;elenco dei namespace
solution: Experience Platform
title: Elencare spazi dei nomi di identità disponibili
topic-legacy: API guide
description: Elenca tutti i namespace disponibili.
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '79'
ht-degree: 5%

---

# Elencare spazi dei nomi di identità disponibili

**Formato API**

```http
GET /idnamespace/identities
```

**Richiesta**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/idnamespace/identities' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta include un array di oggetti, ciascuno dei quali rappresenta uno spazio dei nomi disponibile. I namespace con un valore &quot;[!UICONTROL custom]&quot; di &quot;[!UICONTROL false]&quot; sono spazi dei nomi standard, mentre quelli con un valore &quot;[!UICONTROL custom]&quot; di &quot;[!UICONTROL true]&quot; sono spazi dei nomi creati dalla tua organizzazione.

>[!NOTE]
>
>Questa risposta è stata troncata per lo spazio.

```json
[
  {
        "updateTime": 1441122419000,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "CORE Namespace",
        "id": 0,
        "createTime": 1441122419000,
        "idType": "COOKIE",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1495153678000,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "ECID Namespace",
        "id": 4,
        "createTime": 1495153678000,
        "idType": "COOKIE",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1522783145000,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1522783145000,
        "idType": "COOKIE",
        "name": "AdCloud",
        "custom": false
    }
]
```

## Passaggi successivi

Procedi all’esercitazione successiva su [creare uno spazio dei nomi personalizzato](./create-custom-namespace.md)
