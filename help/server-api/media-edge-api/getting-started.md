---
keywords: Experience Platform;media edge;argomenti popolari;intervallo di date
solution: Experience Platform
title: Guida introduttiva alle API Media Edge
description: Guida introduttiva alle API Media Edge
exl-id: null
source-git-commit: 8592bcc7a6d6700ec9b689b98d07a15f0b9301b2
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 5%

---


# Guida introduttiva all’API Media Edge

Questa guida fornisce istruzioni per eseguire con successo le interazioni iniziali con il servizio API Media Edge. Ciò include l’avvio di una sessione multimediale e quindi il tracciamento degli eventi inviati a una soluzione Adobe Experience Platform (AEP) come Customer Journey Analytics (CJA). Il servizio API Media Edge viene avviato con l’endpoint di inizio sessione. Una volta avviata la sessione, è possibile tenere traccia di uno o più dei seguenti eventi:

* play
* ping
* bitrateChange
* bufferStart
* pauseStart
* adBreakStart
* adStart
* adComplete
* adSkip
* adBreakComplete
* chapterStart
* chapterComplete
* chapterSkip
* error
* sessionEnd
* sessionComplete
* statesUpdate

Ogni evento ha il proprio endpoint. Tutti gli endpoint API di Media Edge sono metodi POST, con corpi di richiesta JSON per i dati evento. Per ulteriori informazioni sugli endpoint, i parametri e gli esempi dell’API Media Edge, vedi il file Media Edge Swagger.

Questa guida illustra come tenere traccia dei seguenti eventi dopo l’avvio della sessione:

* Avvio buffer
* Play
* Sessione completata

## Implementazione dell’API

A parte lievi differenze nel modello e nei percorsi denominati, l’API Media Edge è la stessa dell’API Media Collection. I dettagli di implementazione di Media Collection rimangono validi per l’API Media Edge, come descritto nella seguente documentazione:

* [Impostazione del tipo di richiesta HTTP nel lettore](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Invio di eventi ping ](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Condizioni di timeout ](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html?lang=en)
* [Controllo dell’ordine degli eventi ](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html?lang=en)

## Authorization

Attualmente, le API Media Edge non richiedono intestazioni di autorizzazione nelle richieste.


## Avvio della sessione

Per avviare la sessione multimediale sul server, utilizzare l&#39;endpoint di inizio sessione. Una risposta corretta include `sessionId`, che è un parametro obbligatorio per le richieste di eventi successive.

Prima di effettuare la richiesta di avvio della sessione, è necessario disporre dei seguenti elementi:

* Il `datastreamId` è un parametro obbligatorio per la richiesta di avvio della sessione POST. Per recuperare un `datastreamId`, vedi [Configurare uno stream di dati](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en).

* Un oggetto JSON per il payload della richiesta che contiene i dati minimi richiesti (come mostrato nella richiesta di esempio seguente).

Una volta ottenute queste informazioni, fornisci `datastreamId` nell’invito seguente:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionStart?configId={datastream ID} \`

### Richiesta di esempio

L’esempio seguente mostra una richiesta cURL di avvio sessione:

```
curl -i --request POST '{uri}/ee/va/v1/sessionStart?configId={dataStreamId}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Media Analytics API Sample",
            "playerName": "sample-html5-api-player",
            "contentType": "VOD",
            "length": 60,
            "channel": "sample-channel",
            "appVersion": "va-api-1.0.0"
          },
          "playhead": 0
        }
      }
    }
  ]
}'
```

Nell’esempio di richiesta precedente, il `eventType` il valore contiene il prefisso `media` in base al [Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it) per specificare i domini.

Inoltre, la mappatura dei tipi di dati per `eventType` nell’esempio precedente sono i seguenti (i campi di sola generazione rapporti non devono essere presenti nel payload):

| eventType | tipi di dati | campi solo reporting (ignorati) |
| -------- | ------ | ---------- |
| mediaSessionStart | sessionDetails | ID, adCount, averageMinuteAudience,chapterCount, estimatedStreams, hasPauseImpactedStreams, hasProgress10, hasProgress25, hasProgress50, hasProgress75, hasProgress95, hasSegmentView, isCompleted, isDownloaded, isFederated, isPlayed, isViewed, pauseCount, pauseTime, secondsSinceLastCall, segmento, timePlayed, totalTimePlayed, uniqueTimePlayed, pev3 pccr |
| media.chapterStart | chapterDetails | ID, isCompleted, isStarted, timePlayed |
| media.adBreakStart | advertisingPodDetails | ID |
| media.adStart | advertisingDetails | ID, isCompleted, isStarted, timePlayed |
| media.error | errorDetails | - |
| media.statesUpdate | statesStart: array[playerStateData], statesEnd: Array[playerStateData] | playerStateData.isSet, playerStateData.count, playerStateData.time |
| media.sessionStart, media.chapterStart, media.adStart | customMetadata | - |
| tutto | qoeDataDetails | bitrateAverage, bitrateAverageBucket, bitrateChangeCount, bufferCount, bufferTime, errorCount, externalErrors, hasBitrateChangeImpactedStreams, hasBufferImpactedStreams, hasDroppedFrameImpactedStreams, hasErrorImpactedStreams, hasStallImpactedStreams, isDroppedBeforeStart, mediaSdkErrors, playerSdkErrors, stallCount, stallTime |

### Esempio di risposta

L’esempio seguente mostra una risposta corretta per la richiesta di avvio della sessione:

```
HTTP/2 200
x-request-id: 99603f5c-95cf-49ad-9afb-0ba6c5867fd7
x-rate-limit-remaining: 599
vary: Origin
date: Tue, 07 Mar 2023 14:37:58 GMT
x-konductor: 23.3.2:367bc7dc
x-adobe-edge: IRL1;6
server: jag
content-type: application/json;charset=utf-8
strict-transport-security: max-age=31536000; includeSubDomains
cache-control: no-cache, no-store, max-age=0, no-transform
x-xss-protection: 1; mode=block
x-content-type-options: nosniff

{
    "requestId": "df14bca1-ba0f-4574-ae80-a4e24a960c00",
    "handle": [
        {
            "payload": [
                {
                    "sessionId": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333"
                }
            ],
            "type": "media-analytics:new-session",
            "eventIndex": 0
        },
        {
            "payload": [
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_cluster",
                    "value": "irl1",
                    "maxAge": 1800
                },
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_identity",
                    "value": "CiY1MTkxMDM4OTc1MzkwMTY4NTQ1NjAxNDg4OTgzODU5MTAzMDcyMVIPCKKt8KnsMBgBKgRJUkwx8AGirfCp7DA=",
                    "maxAge": 34128000
                }
            ],
            "type": "state:store"
        }
    ]
}
```

Nell’esempio di risposta precedente, il `sessionId` viene visualizzato come `af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333`. Utilizzerai questo ID nelle richieste di eventi successive come parametro obbligatorio.

Per ulteriori informazioni sui parametri e sugli esempi dell’endpoint di inizio sessione, vedi il file Media Edge Swagger.

Per ulteriori informazioni sui parametri dei dati multimediali XDM, consulta [Schema informazioni sui dettagli dei contenuti multimediali](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## Richiesta evento di avvio buffer

L’evento di avvio del buffer viene segnalato all’avvio del buffering sul lettore multimediale. La riattivazione del buffer non è un evento nel servizio API, ma viene dedotta quando un evento di riproduzione viene inviato dopo l’avvio del buffer. Per effettuare una richiesta di evento di avvio del buffer, utilizzare `sessionId` nel payload di una chiamata al seguente endpoint:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart \`

### Richiesta di esempio

L’esempio seguente mostra una richiesta cURL di avvio del buffer:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

Nell’esempio di richiesta precedente, lo stesso `sessionId` che viene restituito nella chiamata precedente viene utilizzato come parametro obbligatorio nella richiesta di avvio del buffer.

Per ulteriori informazioni sui parametri e sugli esempi dell’endpoint di avvio del buffer, vedi il file Media Edge Swagger.

La risposta corretta indica uno stato di 200 e non include alcun contenuto.

## Riproduci richiesta evento

L’evento Play viene inviato quando il lettore multimediale passa allo stato di &quot;riproduzione&quot; da un altro stato, ad esempio &quot;buffering&quot;, &quot;messo in pausa&quot; o &quot;errore&quot;. Per effettuare una richiesta di evento Play, utilizza `sessionId` nel payload di una chiamata al seguente endpoint:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/play \`

### Richiesta di esempio

L’esempio seguente mostra una richiesta Play cURL:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/play' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

La risposta corretta indica uno stato di 200 e non include alcun contenuto.

Per ulteriori informazioni sui parametri e sugli esempi dell’endpoint Play, consulta il file Media Edge Swagger.

## Richiesta evento sessione completata

L’evento Sessione completata viene inviato quando viene raggiunta la fine del contenuto principale. Per effettuare una richiesta di evento Sessione completa, utilizza `sessionId` nel payload di una chiamata al seguente endpoint:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete \`

### Richiesta di esempio

L’esempio seguente mostra una richiesta cURL di completamento sessione:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

La risposta corretta indica uno stato di 200 e non include alcun contenuto.

## Codici di risposta

La tabella seguente mostra i possibili codici di risposta risultanti dalle richieste API Media Edge:

| Stato | Descrizione |
| ---------- | --------- |
| 200 | La sessione è stata creata |
| 207 | Problema con uno dei servizi che si connettono a Experience Edge Network (per ulteriori informazioni, consulta la guida alla risoluzione dei problemi) |
| 400 livelli | Richiesta non valida |
| Livello 500 | Errore del server |

Per ulteriori informazioni sulla gestione degli errori e dei codici di risposta non riusciti, consulta la guida alla risoluzione dei problemi di Media Edge.


