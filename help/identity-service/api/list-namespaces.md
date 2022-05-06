---
keywords: Experience Platform;home;argomenti popolari;elenco dei namespace;elenco dei namespace
solution: Experience Platform
title: Elencare spazi dei nomi di identità disponibili
topic-legacy: API guide
description: Elenca tutti i namespace disponibili.
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 7%

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta include un array di oggetti, ciascuno dei quali rappresenta uno spazio dei nomi disponibile. Namespace con &quot;[!UICONTROL personalizzato]&quot; valore di &quot;[!UICONTROL false]&quot; sono spazi dei nomi standard, mentre quelli con &quot;[!UICONTROL personalizzato]&quot; valore di &quot;[!UICONTROL true]&quot; sono spazi dei nomi creati dalla tua organizzazione.

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
