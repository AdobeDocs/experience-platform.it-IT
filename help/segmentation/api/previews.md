---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Anteprime
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Visualizza in anteprima la guida per gli sviluppatori

introduzione

- Creare una nuova anteprima
- Recuperare i risultati di un&#39;anteprima specifica
- Annullare o eliminare un&#39;anteprima specifica

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte dell&#39;API di segmentazione. Prima di continuare, consulta la guida [per lo sviluppatore di](./getting-started.md)segmentazione.

In particolare, la sezione [](./getting-started.md#getting-started) introduttiva della guida per gli sviluppatori di segmentazione include collegamenti a argomenti correlati, una guida alla lettura delle chiamate API di esempio nel documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API della piattaforma Experience.

## Creare una nuova anteprima

Potete creare una nuova anteprima effettuando una richiesta POST all’ `/preview` endpoint.

**Formato API**

```http
POST /preview
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
  "predicateType": "pql/text",
  "predicateModel": "_xdm.context.profile",
  "graphType": "pdg"
}
 '
```

body info

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) con i dettagli della nuova anteprima creata.

```json
{
  "state": "NEW",
  "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
  "previewQueryStatus": "NEW",
  "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
  "previewExecutionId": 0
}
```

info risposta, x-location non esiste.

## Recuperare i risultati di un&#39;anteprima specifica

Potete recuperare informazioni dettagliate su un&#39;anteprima specifica effettuando una richiesta GET all&#39; `/preview` endpoint e fornendo il valore dell&#39;anteprima `id` nel percorso della richiesta.

**Formato API**

```http
GET /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: Il `id` valore dell’anteprima da recuperare.

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sull&#39;anteprima specificata.

```json
{
  "state": "RESULT_READY",
  "page": {
    "offset": 0,
    "size": 0
  },
  "results": [],
  "link": {
    "nextPage": ""
  },
  "previewSampledResultsCount": 0
}
```

## Annullare o eliminare un&#39;anteprima specifica

Potete eliminare un&#39;anteprima specifica eseguendo una richiesta DELETE all&#39; `/preview` endpoint e fornendo il valore dell&#39;anteprima `id` nel percorso della richiesta.

**Formato API**

```http
DELETE /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}` Il `id` valore dell’anteprima da eliminare.

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con il seguente messaggio:

```json
{
  "status": true,
  "message": "KILLED"
}
```

## Passaggi successivi
