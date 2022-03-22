---
keywords: Experience Platform;home;argomenti popolari;servizio query;guida api;parametri di connessione;servizio query;
solution: Experience Platform
title: Endpoint API per i parametri di connessione
topic-legacy: connection parameters
description: È possibile recuperare i parametri di connessione per l'utilizzo del servizio interattivo effettuando una richiesta GET all'endpoint /connection_parameters.
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: cff95575530e0db00d34ff1ea4c90e5422b6562d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# Endpoint di connessione

## Chiamata API di esempio

La sezione seguente illustra la chiamata API che puoi effettuare utilizzando [!DNL Query Service] API. La chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Parametri di connessione della richiesta

Puoi recuperare i parametri di connessione effettuando una richiesta GET al `/connection_parameters` punto finale. Per ulteriori informazioni sui client che utilizzano i parametri di connessione per la connessione tramite il servizio interattivo, consulta la documentazione in [Client del servizio query](../clients/overview.md).

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
