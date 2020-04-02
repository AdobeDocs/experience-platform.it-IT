---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Stime
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7

---


# Stime

introduzione

- Recuperare i risultati di un processo di stima specifico

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte dell&#39;API di segmentazione. Prima di continuare, consulta la guida [per lo sviluppatore di](./getting-started.md)segmentazione.

In particolare, la sezione [](./getting-started.md#getting-started) introduttiva della guida per gli sviluppatori di segmentazione include collegamenti a argomenti correlati, una guida alla lettura delle chiamate API di esempio nel documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API della piattaforma Experience.

## Recuperare i risultati di un processo di stima specifico

È possibile recuperare i dettagli di un processo di stima specifico eseguendo una richiesta GET all&#39; `/estimate` endpoint e fornendo il valore del processo `id` di stima nel percorso della richiesta.

**Formato API**

```http
GET /estimate/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: Il `id` valore del processo stimato da recuperare.

**Richiesta**

La richiesta seguente recupera i risultati di un processo di stima specifico.

//è necessario ottenere un ID di anteprima

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/{PREVIEW_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli del processo stimato.

```json
{
  "estimatedSize": 0,
  "numRowsToRead": 1,
  "state": "RESULT_READY",
  "profilesReadSoFar": 1,
  "standardError": 0,
  "error": {
    "description": "",
    "traceback": ""
  },
  "profilesMatchedSoFar": 0,
  "totalRows": 1,
  "confidenceInterval": "95%",
  "_links": {
    "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
  }
}
```

## Passaggi successivi

Ora che sai come recuperare i risultati dei lavori stimati, puoi migliorare