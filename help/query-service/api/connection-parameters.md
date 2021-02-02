---
keywords: ' Experience Platform;home;argomenti comuni;servizio query;guida API;parametri di connessione;servizio query;'
solution: Experience Platform
title: Guida per gli sviluppatori di Query Service
topic: connection parameters
description: È possibile recuperare i parametri di connessione per l'utilizzo del servizio interattivo effettuando una richiesta di GET all'endpoint /connection_parameters.
translation-type: tm+mt
source-git-commit: 648544bc60c0cee8ca8b167118391980b6c33d91
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 1%

---


# Parametri di connessione

## Chiamate API di esempio

Ora che hai compreso quali intestazioni utilizzare, sei pronto a iniziare a effettuare chiamate all&#39;API [!DNL Query Service]. Le sezioni seguenti descrivono le varie chiamate API che potete effettuare tramite l&#39;API [!DNL Query Service]. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Richiedi parametri di connessione

È possibile recuperare i parametri di connessione effettuando una richiesta di GET all&#39;endpoint `/connection_parameters`. Per ulteriori informazioni sui client che utilizzano i parametri di connessione per connettersi tramite il servizio interattivo, consultare la documentazione sui client [Query Service](../clients/overview.md).

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
