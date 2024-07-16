---
title: createMediaSession
description: Scopri come configurare Web SDK per gestire automaticamente le sessioni multimediali
exl-id: abcb26f6-7249-4235-99eb-e4b9aeecff3e
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---

# `createMediaSession`

Il comando `createMediaSession` fa parte del componente Web SDK `streamingMedia`. Puoi utilizzare questo componente per raccogliere i dati relativi alle sessioni multimediali sul tuo sito web. Per informazioni su come configurare questo componente, consulta la `streamingMedia` [documentazione](configure/streamingmedia.md).

I dati raccolti possono includere informazioni su riproduzioni multimediali, pause, completamenti e altri eventi correlati. Una volta raccolti, puoi inviare questi dati a [适用于流媒体的 Adobe Analytics](https://experienceleague.adobe.com/it/docs/media-analytics/using/media-overview) per aggregare le metriche. Questa funzione fornisce una soluzione completa per il tracciamento e la comprensione del comportamento di consumo dei contenuti multimediali sul sito web.

Puoi creare sessioni multimediali in Web SDK in due modi:

* [Le sessioni multimediali con tracciamento automatico](#automatic) consentono a Web SDK di gestire l&#39;invio di eventi ping multimediali a [适用于流媒体的 Adobe Analytics](https://experienceleague.adobe.com/it/docs/media-analytics/using/media-overview). La frequenza di questi ping è determinata dalle impostazioni di configurazione del componente [streamingMedia](configure/streamingmedia.md).
* [Le sessioni multimediali con tracciamento manuale](#manual) offrono maggiore controllo sull&#39;invio di eventi ping di sessione a [适用于流媒体的 Adobe Analytics](https://experienceleague.adobe.com/it/docs/media-analytics/using/media-overview). È inoltre possibile archiviare `sessionID` per le sessioni multimediali.

## Creare una sessione multimediale con tracciamento automatico {#automatic}

Per avviare automaticamente il tracciamento di una sessione multimediale, chiamare il metodo `createMediaSession` con le opzioni descritte di seguito:

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
| `getPlayerDetails` | Funzione | Sì | Funzione che restituisce i dettagli del lettore. Questa funzione di callback verrà chiamata dall&#39;SDK Web prima di ogni evento multimediale per `playerId` fornito. |
| `xdm.eventType ` | Oggetto | No | Il tipo di evento multimediale. Se non specificato, viene impostato automaticamente su `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Oggetto | Sì | L’oggetto dei dettagli della sessione. L&#39;oggetto `sessionDetails` deve contenere le proprietà dei dettagli della sessione. Per ulteriori informazioni, consulta la documentazione dello schema [Media Collection](../../xdm/data-types/media-collection-details.md). |


## Creare una sessione multimediale tracciata manualmente {#manual}

Per avviare manualmente il tracciamento di una sessione multimediale, chiamare il metodo `createMediaSession` con le opzioni descritte di seguito:

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
| `xdm.eventType` | Oggetto | No | Il tipo di evento multimediale. Se non specificato, viene automaticamente impostato su `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Oggetto | Sì | L’oggetto dei dettagli della sessione. L&#39;oggetto `sessionDetails` deve contenere le proprietà dei dettagli della sessione. Per ulteriori informazioni, consulta la documentazione dello schema [Media Collection](../../xdm/data-types/media-collection-details.md). |
| `xdm.mediaCollection.playhead` | Intero | Sì | La testina di riproduzione corrente. |
| `xdm.mediaCollection.qoeDataDetails` | Oggetto | No | La qualità dei dettagli dei dati sull’esperienza. Per ulteriori informazioni, consulta la documentazione dello schema [Media Collection](../../xdm/data-types/media-collection-details.md). |
