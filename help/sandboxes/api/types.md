---
keywords: Experience Platform;home;argomenti popolari;elenco sandbox
solution: Experience Platform
title: Endpoint API per tipi di sandbox
description: Puoi recuperare un elenco dei tipi di sandbox supportati per la tua organizzazione effettuando una richiesta GET all’endpoint /sandboxTypes .
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# Endpoint per tipi di sandbox

Puoi recuperare un elenco dei tipi di sandbox supportati per la tua organizzazione effettuando una richiesta GET al `/sandboxTypes` punto finale.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco dei tipi di sandbox supportati

Puoi recuperare un elenco dei tipi di sandbox supportati per la tua organizzazione effettuando una richiesta GET al `/sandboxTypes` punto finale.

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

Una risposta corretta restituisce un elenco di tipi di sandbox supportati dalla tua organizzazione.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
