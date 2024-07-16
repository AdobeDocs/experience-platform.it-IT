---
keywords: Experience Platform;home;argomenti popolari;elenco sandbox
solution: Experience Platform
title: Endpoint API per tipi di sandbox
description: Per recuperare un elenco dei tipi di sandbox supportati per la tua organizzazione, devi eseguire una richiesta GET all’endpoint /sandboxTypes.
role: Developer
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 3%

---

# Endpoint &quot;sandbox types&quot;

Per recuperare un elenco dei tipi di sandbox supportati per la tua organizzazione, devi effettuare una richiesta GET all&#39;endpoint `/sandboxTypes`.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39;[[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e per le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recuperare un elenco di tipi di sandbox supportati

Per recuperare un elenco dei tipi di sandbox supportati per la tua organizzazione, devi effettuare una richiesta GET all&#39;endpoint `/sandboxTypes`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di tipi di sandbox supportati per la tua organizzazione.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
