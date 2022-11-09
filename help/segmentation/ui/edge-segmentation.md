---
keywords: Experience Platform;home;argomenti popolari;segmentazione edge;Segmentazione;Servizio di segmentazione;servizio di segmentazione;guida interfaccia utente;bordo streaming;
solution: Experience Platform
title: Guida all’interfaccia utente di Segmentazione bordo
topic-legacy: ui guide
description: La segmentazione dei bordi è la capacità di valutare istantaneamente i segmenti in Platform sul bordo, abilitando casi d’uso di personalizzazione della pagina e della stessa pagina.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 95ffd09b81b49c8c7d65695a2fbc0fcd97b12c9e
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# Guida all’interfaccia utente per la segmentazione dei bordi

>[!NOTE]
>
>La segmentazione dei bordi è ora generalmente disponibile per tutti gli utenti di Platform. Se hai creato segmenti edge durante la versione beta, questi segmenti continueranno a essere operativi.

La segmentazione dei bordi è la capacità di valutare istantaneamente i segmenti in Adobe Experience Platform [sul bordo](../../edge/home.md), l’abilitazione di casi d’uso di personalizzazione pagina e pagina successiva.

>[!IMPORTANT]
>
> I dati edge saranno memorizzati in una posizione server perimetrale più vicina a quella in cui sono stati raccolti e possono essere memorizzati in una posizione diversa da quella designata come centro dati hub (o principal) di Adobe Experience Platform.
>
> Inoltre, il motore di segmentazione dei bordi rispetterà solo le richieste sul bordo in cui è presente **uno** identità principale contrassegnata, coerente con le identità principali non basate su edge.

## Tipi di query per segmentazione Edge

Attualmente è possibile valutare solo i tipi di query selezionati con la segmentazione edge. Le sezioni seguenti forniscono un elenco dei tipi di query che possono essere valutati con la segmentazione edge e quelli che non sono attualmente supportati.

### Tipi di query supportati {#query-types}

Una query può essere valutata con segmentazione edge se soddisfa uno dei criteri descritti nella tabella seguente.

>[!NOTE]
>
>Se la query corrisponde a uno qualsiasi dei tipi di query nella tabella seguente, verrà valutata automaticamente utilizzando la segmentazione edge. Il sistema determina automaticamente questa capacità in base all&#39;espressione della query.

| Tipo di query | Dettagli | Esempio | Esempio PQL |
| ---------- | ------- | ------- | ----------- |
| Evento singolo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. | Persone che hanno aggiunto un elemento al carrello. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Profilo singolo | Qualsiasi definizione di segmento che fa riferimento a un singolo attributo di solo profilo | Persone che vivono negli Stati Uniti d&#39;America. | `homeAddress.countryCode = "US"` |
| Singolo evento che fa riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un singolo evento in arrivo senza restrizioni di tempo. | Persone che vivono negli Stati Uniti che hanno visitato la homepage. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| Singolo evento ignorato con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in entrata negato e a uno o più attributi di profilo | Persone che vivono negli Stati Uniti e che hanno **not** Ho visitato la homepage. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Singolo evento in una finestra temporale | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo entro un determinato periodo di tempo. | Persone che hanno visitato la homepage nelle ultime 24 ore. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| Singolo evento con un attributo di profilo in una finestra temporale | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un singolo evento in arrivo entro un determinato periodo di tempo. | Persone che vivono negli Stati Uniti che hanno visitato la homepage nelle ultime 24 ore. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| Singolo evento ignorato con un attributo di profilo all&#39;interno di una finestra temporale | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un singolo evento in arrivo negato entro un periodo di tempo. | Persone che vivono negli Stati Uniti e che hanno **not** Ho visitato la homepage nelle ultime 24 ore. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)]))` |
| Evento di frequenza entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a un evento che si verifica un certo numero di volte all’interno di un intervallo di tempo di 24 ore. | Persone che hanno visitato la homepage **almeno** cinque volte nelle ultime 24 ore. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento di frequenza con un attributo di profilo entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un evento che si verifica un certo numero di volte all’interno di un intervallo di tempo di 24 ore. | Persone dagli Stati Uniti che hanno visitato la homepage **almeno** cinque volte nelle ultime 24 ore. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento di frequenza ignorato con un profilo entro una finestra temporale di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un evento negato che si verifica un certo numero di volte all’interno di un intervallo di tempo di 24 ore. | Persone che non hanno visitato la homepage **more** cinque volte nelle ultime 24 ore. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Più hit in arrivo in un profilo temporale di 24 ore | Una definizione di segmento che fa riferimento a più eventi che si verificano all’interno di un intervallo di tempo di 24 ore. | Persone che hanno visitato la homepage **o** Ho visitato la pagina di pagamento nelle ultime 24 ore. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Eventi multipli con un profilo entro una finestra temporale di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a più eventi che si verificano all’interno di un intervallo di tempo di 24 ore. | Persone dagli Stati Uniti che hanno visitato la homepage **e** Ho visitato la pagina di pagamento nelle ultime 24 ore. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segmento di segmenti | Qualsiasi definizione di segmento che contiene uno o più segmenti in batch o in streaming. | Persone che vivono negli Stati Uniti e si trovano nel segmento &quot;segmento esistente&quot;. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Query che fa riferimento a una mappa | Qualsiasi definizione di segmento che fa riferimento a una mappa di proprietà. | Persone che hanno aggiunto al carrello in base ai dati dei segmenti esterni. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

## Passaggi successivi

Questa guida spiega come valutare i segmenti con la segmentazione edge su Adobe Experience Platform. Per ulteriori informazioni sull’utilizzo dell’interfaccia utente di Experience Platform, consulta la sezione [Guida utente alla segmentazione](./overview.md). Per informazioni su come eseguire azioni simili e lavorare con i segmenti utilizzando le API di Experience Platform, visita il [guida API per la segmentazione edge](../api/edge-segmentation.md).

## Appendice

Nella sezione seguente sono elencate le domande frequenti sulla segmentazione dei bordi:

### Quanto tempo ci vuole perché un segmento sia disponibile su Edge Network?

Per rendere disponibile un segmento su Edge Network, è necessaria fino a un’ora.