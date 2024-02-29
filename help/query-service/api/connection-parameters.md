---
keywords: Experience Platform;home;argomenti popolari;servizio query;guida api;parametri di connessione;servizio query;
solution: Experience Platform
title: Endpoint API per i parametri di connessione
description: Per recuperare i parametri di connessione per l’utilizzo del servizio interattivo, effettua una richiesta di GET all’endpoint /connection_parameters.
role: Developer
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# Endpoint &quot;connection parameters&quot;

## Chiamata API di esempio

La sezione seguente illustra la chiamata API che è possibile effettuare utilizzando [!DNL Query Service] API. La chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Richiedi parametri di connessione

Puoi recuperare i parametri di connessione effettuando una richiesta GET al `/connection_parameters` endpoint. Per ulteriori informazioni sui client che utilizzano i parametri di connessione per connettersi tramite il servizio interattivo, consulta la documentazione su [Client Query Service](../clients/overview.md).

**Formato API**

```http
GET /connection_parameters
```

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i parametri di connessione.

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
