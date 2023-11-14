---
solution: Experience Platform
title: Guida introduttiva alle API Media Edge
description: Guida introduttiva alle API Media Edge
exl-id: 76022dea-408b-4d8e-abd4-1a6de81beceb
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 4%

---

# Guida introduttiva all’API Media Edge

Questa guida fornisce istruzioni per eseguire con successo le interazioni iniziali con il servizio API Media Edge. Ciò include l’avvio di una sessione multimediale e quindi il tracciamento degli eventi inviati a una soluzione Adobe Experience Platform come Customer Journey Analytics (CJA). Il servizio API Media Edge viene avviato con l’endpoint di inizio sessione. Una volta avviata la sessione, è possibile tenere traccia di uno o più dei seguenti eventi:

* `play`
* `ping`
* `bitrateChange`
* `bufferStart`
* `pauseStart`
* `adBreakStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakComplete`
* `chapterStart`
* `chapterComplete`
* `chapterSkip`
* `error`
* `sessionEnd`
* `sessionComplete`
* `statesUpdate`

Ogni evento ha il proprio endpoint. Tutti gli endpoint API di Media Edge sono metodi POST, con corpi di richiesta JSON per i dati evento. Per ulteriori informazioni sugli endpoint API di Media Edge, sui parametri e sugli esempi, consulta la sezione [File Media Edge Swagger](swagger.md).

Questa guida illustra come tenere traccia dei seguenti eventi dopo l’avvio della sessione:

* [Avvio buffer](#buffer-start-event-request)
* [Play](#play-event-request)
* [Sessione completata](#session-complete-event-request)

## Implementazione dell’API {#implement-api}

A parte lievi differenze nel modello e nei percorsi chiamati, l’API Media Edge ha la stessa implementazione del [API Media Collection](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html). I dettagli di implementazione di Media Collection rimangono validi per l’API Media Edge, come descritto nella seguente documentazione:

* [Impostazione del tipo di richiesta HTTP nel lettore](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html)
* [Invio di eventi ping ](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html)
* [Condizioni di timeout ](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html)
* [Controllo dell’ordine degli eventi ](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html)

## Authorization {#authorization}

Attualmente, le API Media Edge non richiedono intestazioni di autorizzazione nelle richieste.


## Avvio della sessione {#start-session}

Per avviare la sessione multimediale sul server, utilizzare l&#39;endpoint di inizio sessione. Una risposta corretta include `sessionId`, che è un parametro obbligatorio per le richieste di eventi successive.

Prima di effettuare la richiesta di avvio della sessione, è necessario disporre dei seguenti elementi:

* Il `datastreamId`- parametro obbligatorio per la richiesta di inizio sessione POST. Per recuperare un `datastreamId`, vedi [Configurare uno stream di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=it).

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

Nell’esempio di richiesta precedente, il `eventType` il valore contiene il prefisso `media.` in base al [Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it) per specificare i domini.

Inoltre, la mappatura dei tipi di dati per `eventType` nell’esempio precedente sono i seguenti:

| eventType | tipi di dati |
| -------- | ------ |
| media.SessionStart | [sessionDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/sessiondetails.schema.md) |
| media.chapterStart | [chapterDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/chapterdetails.schema.md) |
| media.adBreakStart | [advertisingPodDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingpoddetails.schema.md) |
| media.adStart | [advertisingDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingdetails.schema.md) |
| media.error | [errorDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/errordetails.schema.md) |
| media.statesUpdate | [statesStart](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesstart): array[playerStateData], [statesEnd](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesend): array[playerStateData] |
| media.sessionStart, media.chapterStart, media.adStart | [customMetadata](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmcustommetadata) |
| tutto | [qoeDataDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/qoedatadetails.schema.md) |

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

Per ulteriori informazioni sui parametri e sugli esempi dell&#39;endpoint di inizio sessione, vedere [Media Edge Swagger](swagger.md) file.

Per ulteriori informazioni sui parametri dei dati multimediali XDM, consulta [Schema informazioni sui dettagli dei contenuti multimediali](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## Richiesta evento di avvio buffer {#buffer-start}

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

La risposta corretta indica uno stato di 200 e non include alcun contenuto.

Per ulteriori informazioni sui parametri e sugli esempi dell&#39;endpoint di avvio del buffer, vedere [Media Edge Swagger](swagger.md) file.


## Riproduci richiesta evento {#play-event}

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

Per ulteriori informazioni sui parametri e sugli esempi dell’endpoint Play, vedi [Media Edge Swagger](swagger.md) file.

## Richiesta evento sessione completata {#session-complete}

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

Per ulteriori informazioni sui parametri e sugli esempi dell&#39;endpoint Session Complete, vedere [Media Edge Swagger](swagger.md) file.

## Codici di risposta

La tabella seguente mostra i possibili codici di risposta risultanti dalle richieste API Media Edge:

| Stato | Descrizione |
| ---------- | --------- |
| 200 | La sessione è stata creata |
| 207 | Problema con uno dei servizi connessi a Edge Network (per ulteriori informazioni, vedere [guida alla risoluzione dei problemi](troubleshooting.md)) |
| 400 livelli | Richiesta non valida |
| Livello 500 | Errore del server |

## Ulteriori informazioni su questa funzione

* [Guida alla risoluzione dei problemi di Media Edge](troubleshooting.md)
* [Panoramica API di Media Edge](overview.md)
