---
keywords: Experience Platform;home;popular topics;query service;api guide;connection parameters;Query service;
solution: Experience Platform
title: Guida per gli sviluppatori di Query Service
topic: connection parameters
description: È possibile recuperare i parametri di connessione per l'utilizzo del servizio interattivo effettuando una richiesta di GET all'endpoint /connection_parameters.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 1%

---


# Parametri di connessione

## Chiamate API di esempio

Ora che hai compreso quali intestazioni utilizzare, sei pronto a iniziare a effettuare chiamate all&#39; [!DNL Query Service] API. Le sezioni seguenti descrivono le varie chiamate API che potete effettuare tramite l&#39; [!DNL Query Service] API. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Richiedi parametri di connessione per il servizio interattivo

È possibile recuperare i parametri di connessione per l&#39;utilizzo del servizio [](../creating-queries/writing-queries.md) interattivo effettuando una richiesta di GET all&#39; `/connection_parameters` endpoint. Per ulteriori informazioni sui client che utilizzano i parametri di connessione per connettersi tramite il servizio interattivo, consultare la documentazione sui client [](../clients/overview.md)Query Service.

**Formato API**

```http
GET /connection_parameters
```

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i parametri di connessione.

```json
{
    "username": "{USERNAME}",
    "dbName": "prod:all",
    "host": "{HOSTNAME}",
    "version": 1,
    "port": 80,
    "token": "{TOKEN}",
    "compressedToken": "{COMPRESSED_TOKEN}",
    "websocketHost": "{WEBSOCKET_HOSTNAME}"
}
```
