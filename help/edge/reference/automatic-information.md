---
title: Informazioni raccolte automaticamente
seo-title: Informazioni raccolte automaticamente da Adobe Experience Platform Web SDK
description: Descrizione di ciascuna informazione raccolta automaticamente dall’SDK Adobe Experience Cloud
seo-description: Descrizione di ciascuna informazione raccolta automaticamente dall’SDK Adobe Experience Cloud
keywords: collect information;context;configure;device;screenHeight;screen Height;screenOrientation;screen Orientation;screenWidth;screen Width;environment;viewportHeight;viewport Height;viewportWidth;viewport Width;crowserDetails;browser details;implementationDetails;implementation Details;name;version;placeContext;localTime;local Time;localTimezoneOffset;local Timezone Offset;timestamp;web;url;webPageDetails;web Page Details;webReferrer;web Referrer;landscape;portrait;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 8%

---


# Informazioni raccolte automaticamente

Adobe Experience Cloud SDK raccoglie automaticamente una serie di informazioni senza alcuna configurazione speciale. Tuttavia, queste informazioni possono essere disattivate se necessario utilizzando l&#39; `context` opzione nel `configure` comando. [Consultate Configurazione dell’SDK](../fundamentals/configuring-the-sdk.md). Di seguito è riportato un elenco di queste informazioni. Il nome tra parentesi indica la stringa da utilizzare per la configurazione del contesto.

## Dispositivo (`device`)

Informazioni sul dispositivo. Ciò non include i dati che possono essere cercati sul lato server dalla stringa agente utente.

### Altezza schermo

| **Percorso in Payload:** | **Esempio:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Altezza in pixel dello schermo.

### Orientamento dello schermo

| **Percorso in Payload:** | **Valori possibili:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` o `portrait` |

Orientamento dello schermo.

### Larghezza schermo

| **Percorso in Payload:** | **Esempio:** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

Larghezza dello schermo (in pixel).

## Ambiente (`environment`)

Dettagli sull&#39;ambiente del browser.

### Tipo di ambiente

Browser

| **Percorso in Payload:** | **Esempio:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

Il tipo di ambiente attraverso cui è stata realizzata l&#39;esperienza. L’SDK Adobe Experience Platform per JavaScript viene sempre impostato `browser`.

### Altezza visualizzazione

| **Percorso in Payload:** | **Esempio:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

Altezza dell&#39;area contenuto del browser (in pixel).

### Larghezza visualizzazione

| **Percorso in Payload:** | **Esempio:** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

Larghezza dell&#39;area contenuto del browser (in pixel).

## Dettagli di implementazione

Informazioni sull’SDK utilizzato per raccogliere l’evento.

### Nome

| **Percorso in Payload:** | **Esempio:** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

Identificatore del kit di sviluppo software (SDK).  Questo campo utilizza un URI per migliorare l&#39;univocità tra gli identificatori forniti dalle diverse librerie software.

### Versione

| **Percorso in Payload:** | **Esempio:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

### Ambiente

| **Percorso in Payload:** | **Esempio:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |


## Inserisci contesto (`placeContext`)

Informazioni sulla posizione dell’utente finale.

### Ora locale

| **Percorso in Payload:** | **Esempio:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Timestamp locale per l’utente finale in formato ISO semplificato esteso [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Offset fuso orario locale

| **Percorso in Payload:** | **Esempio:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Numero di minuti in cui l&#39;utente viene spostato da GMT.

## Timestamp

| **Percorso in Payload:** | **Esempio:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

Il timestamp dell’evento.  Impossibile rimuovere questa parte del contesto.

marca temporale UTC per l&#39;utente finale in formato ISO semplificato esteso [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Dettagli Web (`web`)

Dettagli sulla pagina in cui è posizionato l’utente.

### URL pagina corrente

| **Percorso in Payload:** | **Esempio:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

URL della pagina corrente.

### URL referente

| **Percorso in Payload:** | **Esempio:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

L’URL della pagina precedente visitata.
