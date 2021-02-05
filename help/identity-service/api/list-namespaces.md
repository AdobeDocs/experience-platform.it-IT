---
keywords: ' Experience Platform;home;argomenti comuni;elenco dei nomi;elenco dei nomi'
solution: Experience Platform
title: Elenca spazi dei nomi identità disponibili
topic: API guide
description: Elenca tutti gli spazi dei nomi disponibili.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '79'
ht-degree: 5%

---


# Elenca spazi dei nomi di identità disponibili

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

La risposta include un array di oggetti, con ogni oggetto che rappresenta uno spazio dei nomi disponibile. Gli spazi dei nomi con il valore &quot;[!UICONTROL custom]&quot; di &quot;[!UICONTROL false]&quot; sono spazi dei nomi standard, mentre quelli con il valore &quot;[!UICONTROL custom]&quot; di &quot;[!UICONTROL true]&quot; sono spazi dei nomi creati dall&#39;organizzazione.

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

Passate all&#39;esercitazione successiva per [creare uno spazio dei nomi personalizzato](./create-custom-namespace.md)