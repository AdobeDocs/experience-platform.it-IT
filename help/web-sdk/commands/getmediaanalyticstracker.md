---
title: getMediaAnalyticsTracker
description: Scopri come creare un oggetto Tracker di Media Analytics e utilizzarlo per tenere traccia degli eventi multimediali.
source-git-commit: 9384c1cc15441199e898d6cc0850e5422253f106
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---


# `getMediaAnalyticsTracker`

Questo comando Web SDK recupera un tracciatore Media Analytics. È possibile utilizzare questo comando per creare un&#39;istanza dell&#39;oggetto e quindi, utilizzando le stesse API fornite da [Libreria JS per contenuti multimediali](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), tieni traccia degli eventi multimediali.

Il `getMediaAnalyticsTracker` restituisce l’API legacy di Media Analytics.


| Nome metodo | Descrizione | Sintassi |
|-----------------|---|----------------|
| `getInstance` | Crea un&#39;istanza del file multimediale per tenere traccia della sessione di riproduzione. | `Media.getInstance()` |
| `createMediaObject` | Crea un oggetto contenente informazioni multimediali. Restituisce un oggetto vuoto se vengono passati parametri non validi. | `Media.createMediaObject(name, id, length, streamType, mediaType)` |
| `createAdBreakObject` | Crea un oggetto contenente informazioni sull&#39;interruzione. Restituisce un oggetto vuoto se vengono passati parametri non validi. | `Media.createAdBreakObject(name, position, startTime)` |
| `createAdObject` | Crea un oggetto contenente informazioni sull’annuncio. Restituisce un oggetto vuoto se vengono passati parametri non validi. | `Media.createAdObject(name, id, position, length)` |
| `createChapterObject` | Crea un oggetto contenente informazioni sul capitolo. Restituisce un oggetto vuoto se vengono passati parametri non validi. | `Media.createChapterObject(name, position, length, startTime)` |
| `createStateObject` | Crea un oggetto contenente informazioni sullo stato. Restituisce un oggetto vuoto se vengono passati parametri non validi. | `Media.createStateObject(name)` |
| `createQoEObject` | Crea un oggetto contenente informazioni QoE. Restituisce un oggetto vuoto se vengono passati parametri non validi. | `Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)` |

## Metodi di istanza

| Nome metodo | Descrizione | Sintassi |
|---|---|----|
| `trackSessionStart` | Traccia l’intenzione di inizio riproduzione. Viene avviata una sessione di tracciamento sull’istanza di tracciamento dei contenuti multimediali. | `trackerInstance.trackSessionStart(mediaInfo, contextData)` |
| `trackPlay` | Tracciare la riproduzione o la ripresa di contenuti multimediali dopo una pausa precedente. | `trackerInstance.trackPlay()` |
| `trackPause` | Tracciare la pausa dei contenuti multimediali. | `trackerInstance.trackPause()` |
| `trackComplete` | Tracciamento del contenuto multimediale completato. Chiama questo metodo solo quando il contenuto multimediale è stato completamente visualizzato. | `trackerInstance.trackComplete()` |
| `trackSessionEnd` | Tracciare la fine di una sessione di visualizzazione. Chiama questo metodo anche se l’utente non visualizza il contenuto multimediale fino al completamento. | `trackerInstance.trackSessionEnd()` |
| `trackError` | Traccia un errore che si è verificato durante la riproduzione di contenuti multimediali. | `trackerInstance.trackError("errorId")` |
| `trackEvent` | Tracciare un evento personalizzato. | `trackerInstance.trackEvent(event, info, contextData)` |
| `updatePlayhead` | Aggiorna la posizione della testina di riproduzione. | `trackerInstance.updatePlayhead(playhead)` |
| `updateQoEObject` | Aggiorna la qualità dell’esperienza. | `trackerInstance.updateQoEObject(qoe)` |

## Costanti

| Nome costante | Descrizione | Valore |
|-----------------|--|-----------------|
| `MediaType` | Tipo di file multimediale | `Video`, `Audio` |
| `StreamType` | Tipo di flusso | `VOD`, `Live`, `Linear`, `Podcast`, `Audiobook`, `AOD` |
| `VideoMetadataKeys` | Questo definisce le chiavi di metadati standard per i flussi video | `Show`, `Season`, `Episode`, `AssetId`, `Genre`, `FirstAirDate`, `FirstDigitalDate`, `Rating`, `Originator`, `Network`, `ShowType`, `AdLoad`, `MVPD`, `Authorized`, `DayPart`, `Feed`, `StreamFormat` |
| `AudioMetadataKeys` | Questo definisce le chiavi di metadati standard per i flussi audio. | `Artist`, `Album`, `Label`, `Author`, `Station`, `Publisher` |
| `AdMetadataKeys` | Definisce le chiavi di metadati standard per gli annunci. | `Advertiser`, `CampaignId`, `CreativeId`, `PlacementId`, `SiteId`, `CreativeUrl` |
| `Event` | Questo definisce il tipo di un evento di tracciamento. | `AdBreakStart`, `AdBreakComplete`, `AdStart`, `AdComplete`, `AdSkip`, `ChapterStart`, `ChapterComplete`, `ChapterSkip`, `SeekStart`, `SeekComplete`, `BufferStart`, `BufferComplete`, `BitrateChange`, `StateStart`, `StateEnd` |
| `PlayerState` | Questo definisce i valori standard per il tracciamento dello stato del lettore. | `FullScreen`, `ClosedCaption`, `Mute`, `PictureInPicture`, `InFocus` |
