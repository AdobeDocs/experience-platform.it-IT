---
keywords: Experience Platform;home;argomenti popolari;servizio query;guida api;parametri di connessione;servizio query;
solution: Experience Platform
title: Endpoint API per i parametri di connessione
topic-legacy: connection parameters
description: È possibile recuperare i parametri di connessione per l'utilizzo del servizio interattivo effettuando una richiesta GET all'endpoint /connection_parameters.
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 1%

---

# Endpoint di connessione

## Chiamate API di esempio

Ora che conosci le intestazioni da utilizzare, sei pronto per iniziare a effettuare chiamate all’ API [!DNL Query Service]. Le sezioni seguenti illustrano le varie chiamate API che puoi effettuare tramite l’ API [!DNL Query Service] . Ciascuna chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Parametri di connessione della richiesta

Puoi recuperare i parametri di connessione effettuando una richiesta GET all’endpoint `/connection_parameters` . Per ulteriori informazioni sui client che utilizzano i parametri di connessione per la connessione tramite il servizio interattivo, consulta la documentazione sui [client del servizio query](../clients/overview.md).

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
