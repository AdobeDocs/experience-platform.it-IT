---
keywords: Experience Platform;media edge;argomenti popolari;intervallo di date
solution: Experience Platform
title: Guida introduttiva alle API Media Edge
description: Guida alla risoluzione dei problemi delle API Media Edge
source-git-commit: b4687fa7f1a2eb8f206ad41eae0af759b0801b83
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---


# Guida alla risoluzione dei problemi dell’API Media Edge

Questa guida fornisce istruzioni per la risoluzione dei problemi relativi alla gestione degli errori e per ottenere risposte corrette.

## Utilizzo di strumenti di risposta agli errori

Per facilitare la risoluzione dei problemi relativi a risposte non riuscite, gli errori sono accompagnati da un corpo di risposta contenente un oggetto errore. In questo caso, il corpo della risposta contiene i dettagli del problema, definiti da [RFC 7807 - Dettagli del problema per le API HTTP](https://datatracker.ietf.org/doc/html/rfc7807). Per migliorare l’esperienza utente dell’API, i dettagli del problema sono descrittivi (i dettagli delle chiavi dell’array vengono visualizzati utilizzando JsonPath nel campo mancante o non valido). Sono anche cumulativi (tutti i campi non validi verranno segnalati nella stessa richiesta).


## Convalida degli avvii della sessione

La maggior parte dei problemi nella creazione delle richieste di avvio sessione si traduce in una risposta 207 con più stati.
Il payload è simile agli errori non irreversibili dell’API del server di rete Experience Edge. Tutti gli errori di Media Analytics hanno il seguente tipo:  `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. I numeri visualizzati nella risposta corrispondono allo stato di errore.

L’esempio seguente mostra un corpo di risposta per una richiesta di inizio sessione privo di un campo obbligatorio e con un campo non valido.

```
{
    "requestId": "d4be4f91-a535-41e7-80c6-bdd031d3a365",
    "handle": [
        ...
    ],
    "errors": [
        {
            "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
            "status": 400,
            "title": "Invalid request",
            "report": {
                "eventIndex": 0,
                "details": [
                    {
                        "name": "$.xdm.mediaCollection.sessionDetails.name",
                        "reason": "Missing required field"
                    },
                    {
                        "name": "$.xdm.timestamp",
                        "reason": "Field should respect ISO 8601 standard for presenting date and time with offset to UTC (e.g. 2022-05-19T19:31:02Z, 2022-05-19T21:31:02+02:00, 2022-05-19T21:31:02.234+02:00)"
                    }
                ]
            }
        }
    ]
}
```

Nell’esempio precedente, entrambi i problemi sono rilevati da `name` e `reason` in `details`: viene visualizzato il primo motivo `missing required field` e il secondo descrive la non conformità alla norma ISO 8601.


>[!NOTE]
>
> Per gli errori causati a monte da Media Analytics, l’Adobe consiglia di continuare a elaborare la sessione multimediale generata.

## Convalida degli eventi

La maggior parte delle richieste di evento non valide genera una risposta di richiesta 400 non valida. In questi casi, il payload è simile agli errori irreversibili dell’API del server di rete Experience Edge.

Per le richieste di eventi, il servizio API Media Edge include controlli aggiuntivi che non vengono acquisiti nel modello XDM stesso. Ciò include una verifica che il percorso `eventType` corrisponde al payload della richiesta `eventType`.


L’esempio seguente mostra un’ `eventType` mancata corrispondenza con un `adBreakStart` payload inviato a `ee/va/v1/chapterStart`:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": "The payload eventType adBreakStart was different from the path eventType chapterStart"
    }
}
```

L’esempio seguente mostra un ulteriore controllo API Media Edge che trova un `chapterStart` chiamata mancante `chapterDetails` informazioni:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": [
            {
                "name": "$.events[0].xdm.mediaCollection.chapterDetails",
                "reason": "Missing required field"
            }
        ]
    }
}
```

## Gestione degli errori a 400 e 500 livelli

Nella tabella seguente vengono fornite istruzioni per la gestione degli errori di risposta dello stato:


| Codice di errore | Descrizione |
| ---------- | --------- |
| 4xx Richiesta non valida | La maggior parte degli errori 4xx (ad esempio 400, 403, 404) non deve essere ritentata dall’utente. Se la richiesta viene ritentata, la risposta non riesce. L’utente deve risolvere l’errore prima di ritentare la richiesta. Gli eventi che causano codici di stato 4xx non vengono tracciati, il che potrebbe potenzialmente influenzare la precisione dei dati nelle sessioni che hanno ricevuto risposte 4xx. |
| 410 Non più disponibile | Indica che la sessione destinata al tracciamento non viene più calcolata sul lato server. Il motivo più comune è che la sessione è più lunga di 24 ore. Dopo aver ricevuto il numero 410, prova ad avviare una nuova sessione e a tracciarla. |
| 429 Troppe richieste | Questo codice di risposta indica che il server limita la velocità delle richieste. Segui le **Riprova dopo** nell’intestazione della risposta. Tutte le risposte che tornano devono contenere il codice di risposta HTTP con un codice di errore specifico del dominio. |
| 500 Errore interno del server | 500 errori sono errori generici e onnicomprensivi. Gli errori 500 non devono essere ritentati, ad eccezione degli errori 502, 503 e 504. |
| 502 Gateway non valido | Questo codice di errore indica che il server, mentre funge da gateway, ha ricevuto una risposta non valida dai server upstream. Ciò può verificarsi a causa di problemi di rete tra i server. Il problema di rete temporaneo può risolversi da solo, pertanto ritentare la richiesta potrebbe risolvere il problema. |
| Servizio non disponibile | Questo codice di errore indica che il servizio non è al momento disponibile. Ciò può verificarsi durante i periodi di manutenzione. I destinatari di errori 503 possono ritentare la richiesta, ma devono anche seguire la **Riprova dopo** istruzioni per l’intestazione. |


Eventi in coda quando le risposte della sessione sono lente

Dopo aver avviato una sessione di tracciamento dei contenuti multimediali, il lettore multimediale può attivarsi prima che venga restituita la risposta di Avvio sessione (con il parametro ID sessione) dal backend. In questo caso, l’app deve mettere in coda tutti gli eventi di tracciamento che arrivano tra la richiesta di sessione e la relativa risposta. Quando la Risposta sessioni arriva, devi prima elaborare tutti gli eventi in coda, quindi puoi iniziare l’elaborazione degli eventi live.

Per ottenere risultati ottimali, consulta il Lettore di riferimento nella tua distribuzione per istruzioni su come elaborare gli eventi prima di ricevere un ID sessione.

L’esempio seguente mostra un metodo per elaborare gli eventi prima della ricezione di un ID sessione:


```
// For event payload format, see "Request body" sections of "Session Start Request", "Event Requests" respectively.  *
 
VideoPlayer.prototype._collectEvent = function(event) {
    var sessionID = event.events[0].xdm.mediaCollection.sessionID
    var eventType = event.events[0].xdm.eventType.substring("media.".length);
    // If we don't have a Session ID yet,
    // queue the event and return...
    if (sessionId === undefined) {
        console.log("[Player] Queueing event")
        _pendingEvents.push(event)
        return;
    }
 
    // If we DO have a Session ID, process the
    // tracking event...
    apiClient.request({
        "baseUrl": `${endpoint}`,
        "path": `ee/va/v1/${eventType}`,
        "method": `POST`,
        "data": `${event}`
    }).then((response) => {
        if (eventType === "sessionStart") {
            var newSessionID = response.json().handle.filter((h) => h.type === "media-analytics:new-session")[0].payload[0].sessionId;
            _processPendingEvents(newSessionID);
        }
        […]
    }
}
 
VideoPlayer.prototype._processPendingEvents function(sessionID) {
    _pendingEvents.forEach((event) => {
        event.events[0].xdm.mediaCollection.sessionID = sessionID;
        _collectEvent(event);
    });
    _pendingEvents = [];
}
```


