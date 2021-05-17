---
title: Raccolta automatica di informazioni nell’SDK per web di Adobe Experience Platform
description: Panoramica di ogni informazione che l’SDK di Adobe Experience Platform raccoglie automaticamente.
keywords: raccogliere informazioni;contesto;configurare;dispositivo;altezza schermo;altezza schermo;orientamento dello schermo;orientamento dello schermo;larghezza dello schermo;larghezza dello schermo;ambiente;finestraAltezza;altezza;altezza del riquadro di visualizzazione;larghezza del riquadro di visualizzazione;larghezza del riquadro di visualizzazione;dettagli del browser;dettagli dell'implementazione;dettagli di implementazione;nome;versione;contesto;ora locale;ora locale;ora locale;fuso orarioOffset;fuso orario locale;offset;timestamp;web;url;webPageDetails;dettagli pagina web;webReferrer;web Referrer;orizzontale;verticale;
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 0f671a967a67761e0cfef6fa0d022e3c3790c2d8
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 6%

---

# Informazioni raccolte automaticamente

Adobe Experience Platform Web SDK raccoglie automaticamente una serie di informazioni senza alcuna configurazione speciale. Tuttavia, queste informazioni possono essere disattivate se necessario utilizzando l&#39;opzione `context` nel comando `configure`. [Consulta Configurazione dell’SDK](../fundamentals/configuring-the-sdk.md). Di seguito è riportato un elenco di queste informazioni. Il nome tra parentesi indica la stringa da utilizzare per la configurazione del contesto.

## Dispositivo (`device`)

Informazioni sul dispositivo. Ciò non include i dati che possono essere cercati lato server dalla stringa dell&#39;agente utente.

### Altezza schermo

| **Percorso nel payload:** | **Esempio:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Altezza dello schermo (in pixel).

### Orientamento dello schermo

| **Percorso nel payload:** | **Valori possibili:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` oppure `portrait` |

Orientamento dello schermo.

### Larghezza dello schermo

| **Percorso nel payload:** | **Esempio:** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

Larghezza dello schermo (in pixel).

## Ambiente (`environment`)

Dettagli sull’ambiente del browser.

### Tipo di ambiente

Browser

| **Percorso nel payload:** | **Esempio:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

Il tipo di ambiente attraverso cui è emersa l’esperienza. L’SDK per web Adobe Experience Platform imposta sempre questo valore su `browser`.

### Altezza del riquadro di visualizzazione

| **Percorso nel payload:** | **Esempio:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

Altezza dell’area contenuto del browser (in pixel).

### Larghezza visualizzazione

| **Percorso nel payload:** | **Esempio:** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

Larghezza dell’area contenuto del browser (in pixel).

## Dettagli di implementazione

Informazioni sull’SDK utilizzato per raccogliere l’evento.

### Nome

| **Percorso nel payload:** | **Esempio:** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

Identificatore del kit di sviluppo software (SDK).  Questo campo utilizza un URI per migliorare l’univocità tra gli identificatori forniti da diverse librerie software. Quando si utilizza la libreria autonoma, il valore è `https://ns.adobe.com/experience/alloy`. Quando la libreria viene utilizzata come parte dell&#39;estensione del Platform launch, il valore è `https://ns.adobe.com/experience/alloy+reactor`.

### Versione

| **Percorso nel payload:** | **Esempio:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

Quando si utilizza la libreria autonoma, il valore è semplicemente la versione della libreria. Quando la libreria viene utilizzata come parte dell&#39;estensione del Platform launch, si tratta della versione della libreria e della versione dell&#39;estensione del Platform launch unita a un &quot;+&quot;. Ad esempio, se la versione della libreria fosse 2.1.0 e la versione dell&#39;estensione del Platform launch fosse 2.1.3, il valore sarebbe `2.1.0+2.1.3`.

### Ambiente

| **Percorso nel payload:** | **Esempio:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

Ambiente in cui sono stati raccolti i dati. È sempre impostato su `browser`.

## Posiziona contesto (`placeContext`)

Informazioni sulla posizione dell’utente finale.

### Ora locale

| **Percorso nel payload:** | **Esempio:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Timestamp locale per l&#39;utente finale in formato ISO semplificato esteso [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Offset fuso orario locale

| **Percorso nel payload:** | **Esempio:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Numero di minuti in cui l’utente viene offset da GMT.

## Timestamp

| **Percorso nel payload:** | **Esempio:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

La marca temporale dell’evento.  Impossibile rimuovere questa parte del contesto.

marca temporale UTC per l&#39;utente finale in formato ISO esteso semplificato [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Dettagli Web (`web`)

Dettagli sulla pagina su cui si trova l’utente.

### URL della pagina corrente

| **Percorso nel payload:** | **Esempio:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

URL della pagina corrente.

### URL di riferimento

| **Percorso nel payload:** | **Esempio:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

URL della pagina precedente visitata.
