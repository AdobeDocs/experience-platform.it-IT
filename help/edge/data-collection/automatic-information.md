---
title: Informazioni raccolte automaticamente in Adobe Experience Platform Web SDK
description: Panoramica di ogni informazione raccolta automaticamente dall’SDK di Adobe Experience Platform.
keywords: raccogliere informazioni;contesto;configurare;dispositivo;screenHeight;screenHeight;screenOrientation;screenWidth;screen Width;screen Width;ambiente;viewportHeight;viewport Height;viewportWidth;viewport Width;crowserDetails;dettagli browser;implementazioneDetails;dettagli implementazione;nome;versione;placeContext;localTime;localTimezoneOffset;local Timezone;Offset fuso orario locale;timestamp;web;url;webPageDetails;web Page Details;webReferrer;web Referrer;orizzontale;portrait;
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 6%

---

# Informazioni raccolte automaticamente

Adobe Experience Platform Web SDK raccoglie automaticamente una serie di informazioni senza alcuna configurazione speciale. Tuttavia, se necessario, queste informazioni possono essere disattivate utilizzando `context` opzione in `configure` comando. [Consulta Configurazione dell’SDK](../fundamentals/configuring-the-sdk.md). Di seguito è riportato un elenco di queste informazioni. Il nome tra parentesi indica la stringa da utilizzare per la configurazione del contesto.

## Dispositivo (`device`)

Informazioni sul dispositivo. Ciò non include i dati che possono essere cercati lato server dalla stringa dell’agente utente.

### Altezza schermo

| **Percorso nel payload:** | **Esempio:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Altezza dello schermo (in pixel).

### Orientamento schermo

| **Percorso nel payload:** | **Valori possibili:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` o `portrait` |

Orientamento dello schermo.

### Larghezza schermo

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

Il tipo di ambiente attraverso il quale è emersa l’esperienza. Adobe Experience Platform Web SDK imposta sempre questo valore su `browser`.

### Altezza del riquadro di visualizzazione

| **Percorso nel payload:** | **Esempio:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

Altezza dell&#39;area contenuto del browser (in pixel).

### Larghezza del riquadro di visualizzazione

| **Percorso nel payload:** | **Esempio:** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

Larghezza (in pixel) dell’area del contenuto del browser.

## Dettagli di implementazione

Informazioni sull’SDK utilizzato per raccogliere l’evento.

### Nome

| **Percorso nel payload:** | **Esempio:** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

Identificatore del kit di sviluppo software (SDK).  Questo campo utilizza un URI per migliorare l’univocità tra gli identificatori forniti da diverse librerie software. Quando si utilizza la libreria autonoma, il valore è `https://ns.adobe.com/experience/alloy`. Quando la libreria viene utilizzata come parte dell’estensione tag, il valore è `https://ns.adobe.com/experience/alloy+reactor`.

### Versione

| **Percorso nel payload:** | **Esempio:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

Quando si utilizza la libreria indipendente, il valore è semplicemente la versione della libreria. Quando la libreria viene utilizzata come parte dell’estensione tag, si tratta della versione della libreria e dell’estensione tag unite con un segno &quot;+&quot;. Ad esempio, se la versione della libreria è 2.1.0 e la versione dell’estensione tag è 2.1.3, il valore sarà `2.1.0+2.1.3`.

### Ambiente

| **Percorso nel payload:** | **Esempio:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

Ambiente in cui sono stati raccolti i dati. Questo è sempre impostato su `browser`.

## Contesto del luogo (`placeContext`)

Informazioni sulla posizione dell’utente finale.

### Ora locale

| **Percorso nel payload:** | **Esempio:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Timestamp locale per l’utente finale in formato ISO esteso semplificato [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Offset fuso orario locale

| **Percorso nel payload:** | **Esempio:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Numero di minuti di offset dell&#39;utente da GMT.

## Marca temporale

| **Percorso nel payload:** | **Esempio:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

Il timestamp dell’evento.  Questa parte del contesto non può essere rimossa.

Timestamp UTC per l’utente finale in formato ISO esteso semplificato [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Dettagli web (`web`)

Dettagli sulla pagina su cui si trova l’utente.

### URL della pagina corrente

| **Percorso nel payload:** | **Esempio:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

URL della pagina corrente.

### URL referrer

| **Percorso nel payload:** | **Esempio:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

URL della pagina precedente visitata.
