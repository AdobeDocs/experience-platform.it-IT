---
keywords: Experience Platform;home;argomenti popolari;preparazione dati;guida api;dati di esempio;
solution: Experience Platform
title: Endpoint API dati di esempio
description: Puoi utilizzare l’endpoint "/samples" nell’API di Adobe Experience Platform per recuperare, creare, aggiornare e convalidare a livello di programmazione i dati di esempio per la mappatura.
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 6%

---


# Endpoint di dati di esempio

È possibile utilizzare dati di esempio durante la creazione di uno schema per il set di mappatura. È possibile utilizzare l&#39;endpoint `/samples` nell&#39;API di preparazione dati per recuperare, creare e aggiornare a livello di programmazione i dati di esempio.

## Elencare dati di esempio

È possibile recuperare un elenco di tutti i dati di esempio di mappatura per l&#39;organizzazione effettuando una richiesta GET all&#39;endpoint `/samples`.

**Formato API**

L&#39;endpoint `/samples` supporta diversi parametri di query per filtrare i risultati. Al momento, è necessario includere entrambi i parametri `start` e `limit` come parte della richiesta.

```http
GET /samples?limit={LIMIT}&start={START}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{LIMIT}` | **Richiesto**. Specifica il numero di dati di esempio di mappatura restituiti. |
| `{START}` | **Richiesto**. Specifica l&#39;offset delle pagine dei risultati. Per ottenere la prima pagina dei risultati, impostare il valore su `start=0`. |

**Richiesta**

La richiesta seguente recupererà gli ultimi due dati di mappatura dei campioni all’interno della tua organizzazione.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sugli ultimi due oggetti di mappatura dei dati di esempio.

```json
{
    "data": [
        {
            "id": "2a429a0057ce47109a4b3e2bc256d755",
            "version": 0,
            "createdDate": 1582250863000,
            "modifiedDate": 1582250863000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        },
        {
            "id": "0248bfb352214f908bdd6cf9c19447e1",
            "version": 0,
            "createdDate": 1582250892000,
            "modifiedDate": 1582250892000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `sampleData` | |
| `sampleType` | |

## Creare dati di esempio

È possibile creare dati di esempio effettuando una richiesta POST all&#39;endpoint `/samples`.

```http
POST /samples
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sui dati di esempio appena creati.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Creare dati di esempio caricando un file

È possibile creare dati di esempio utilizzando un file effettuando una richiesta POST all&#39;endpoint `/samples/upload`.

**Formato API**

```http
POST /samples/upload
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sui dati di esempio appena creati.

```json
{
    "id": "1fb33209ed126bdcdc0b6c20bae49d8a",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Cercare un oggetto dati di esempio specifico

Per cercare un oggetto specifico di dati di esempio, devi fornire il relativo ID nel percorso di una richiesta GET all&#39;endpoint `/samples`.

**Formato API**

```http
GET /samples/{SAMPLE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SAMPLE_ID}` | ID dell’oggetto dati di esempio che desideri recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con le informazioni dell’oggetto dati di esempio che desideri recuperare.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404000,
    "modifiedDate": 1615335404000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Aggiorna dati di esempio

È possibile aggiornare un oggetto dati di esempio specifico fornendo il relativo ID nel percorso di una richiesta PUT all&#39;endpoint `/samples`.

**Formato API**

```http
PUT /samples/{SAMPLE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SAMPLE_ID}` | ID dell’oggetto dati di esempio da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna i dati di esempio specificati. In particolare, aggiorna il cognome da &quot;Smith&quot; a &quot;Lee&quot;.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sui dati di esempio aggiornati.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 1,
    "createdDate": 1615335404000,
    "modifiedDate": 1615337870375,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```
