---
title: createMediaSession
description: Scopri come configurare Web SDK per gestire automaticamente le sessioni multimediali
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---


# `createMediaSession`

Il `createMediaSession` il comando fa parte del Web SDK `streamingMedia` componente. Puoi utilizzare questo componente per raccogliere i dati relativi alle sessioni multimediali sul tuo sito web. Consulta la `streamingMedia` [documentazione](configure/streamingmedia.md) per scoprire come configurare questo componente.

I dati raccolti possono includere informazioni su riproduzioni multimediali, pause, completamenti e altri eventi correlati. Una volta raccolti, puoi inviare questi dati a [适用于流媒体的 Adobe Analytics](https://experienceleague.adobe.com/it/docs/media-analytics/using/media-overview), per aggregare le metriche. Questa funzione fornisce una soluzione completa per il tracciamento e la comprensione del comportamento di consumo dei contenuti multimediali sul sito web.

Puoi creare sessioni multimediali in Web SDK in due modi:

* [Sessioni multimediali tracciate automaticamente](#automatic) consente a Web SDK di gestire l’invio di eventi ping per contenuti multimediali a [适用于流媒体的 Adobe Analytics](https://experienceleague.adobe.com/it/docs/media-analytics/using/media-overview). La frequenza di questi ping è determinata dalle impostazioni di configurazione del [streamingMedia](configure/streamingmedia.md) componente.
* [Sessioni multimediali tracciate manualmente](#manual) offre maggiore controllo sull&#39;invio di eventi ping di sessione a [适用于流媒体的 Adobe Analytics](https://experienceleague.adobe.com/it/docs/media-analytics/using/media-overview). Inoltre, è possibile memorizzare `sessionID` per sessioni multimediali.

## Creare una sessione multimediale con tracciamento automatico {#automatic}

Per avviare automaticamente il tracciamento di una sessione multimediale, chiama il `createMediaSession` con le opzioni descritte di seguito:

```javascript
    alloy("createMediaSession", {
        playerId: "movie-test",
        getPlayerDetails: () => {
            return {
                playhead: document.getElementById("movie-test").currentTime,
                qoeDataDetails: {
                    bitrate: 1000,
                    startupTime: 1000,
                    fps: 30,
                    droppedFrames: 10
                }
            };
        },
        xdm: {
            eventType: "media.sessionStart",
            mediaCollection: {
                sessionDetails: {
                    ...
                }
            }
        }
    });
```

| Proprietà | Tipo | Obbligatorio | Descrizione |
|---------|----------|---------|---------|
| `playerId` | Stringa | Sì | L’ID del lettore, un identificatore univoco che rappresenta la sessione multimediale. |
| `getPlayerDetails` | Funzione | Sì | Funzione che restituisce i dettagli del lettore. Questa funzione di callback verrà chiamata dall&#39;SDK Web prima di ogni evento multimediale per `playerId` fornite. |
| `xdm.eventType ` | Oggetto | No | Il tipo di evento multimediale. Se non specificato, viene impostato automaticamente su `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Oggetto | Sì | L’oggetto dei dettagli della sessione. Il `sessionDetails` L&#39;oggetto deve contenere le proprietà dei dettagli della sessione. Consulta la [Schema Media Collection](../../xdm/data-types/media-collection-details.md) per ulteriori informazioni. |


## Creare una sessione multimediale tracciata manualmente {#manual}

Per avviare manualmente il tracciamento di una sessione multimediale, chiama il `createMediaSession` con le opzioni descritte di seguito:

```javascript
const sessionPromise = alloy("createMediaSession", {
    xdm: {
        eventType: "media.sessionStart",
        mediaCollection: {
            playhead: 0,
            sessionDetails: {
                ...
            },
            qoeDataDetails: {
                bitrate: 1000,
                startupTime: 1000,
                fps: 30,
                droppedFrames: 10
            }
        }
    }
});
```

| Proprietà | Tipo | Obbligatorio | Descrizione |
|---------|----------|---------|---------|
| `xdm.eventType` | Oggetto | No | Il tipo di evento multimediale. Se non viene fornito, viene automaticamente impostato su `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Oggetto | Sì | L’oggetto dei dettagli della sessione. Il `sessionDetails` L&#39;oggetto deve contenere le proprietà dei dettagli della sessione. Consulta la [Schema Media Collection](../../xdm/data-types/media-collection-details.md) per ulteriori informazioni. |
| `xdm.mediaCollection.playhead` | Intero | Sì | La testina di riproduzione corrente. |
| `xdm.mediaCollection.qoeDataDetails` | Oggetto | No | La qualità dei dettagli dei dati sull’esperienza. Consulta la [Schema Media Collection](../../xdm/data-types/media-collection-details.md) per ulteriori informazioni. |
