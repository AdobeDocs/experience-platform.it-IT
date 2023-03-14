---
keywords: Experience Platform;home;argomenti popolari;segmentazione edge;segmentazione;servizio di segmentazione;servizio di segmentazione;guida interfaccia utente;streaming edge;
solution: Experience Platform
title: Guida dell’interfaccia utente per la segmentazione di Edge
description: La segmentazione Edge consente di valutare i segmenti in Platform istantaneamente al limite, abilitando casi d’uso di personalizzazione della pagina corrente e successiva.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# Guida dell’interfaccia utente per la segmentazione Edge

>[!NOTE]
>
>La segmentazione Edge è ora generalmente disponibile per tutti gli utenti di Platform. Se hai creato segmenti edge durante la versione beta, questi segmenti continueranno a essere operativi.

La segmentazione Edge consente di valutare i segmenti in Adobe Experience Platform istantaneamente [sul bordo](../../edge/home.md), abilitando i casi d’uso per la personalizzazione della pagina stessa e successiva.

>[!IMPORTANT]
>
> I dati edge verranno memorizzati in una posizione del server perimetrale più vicina al punto in cui sono stati raccolti e possono essere memorizzati in una posizione diversa da quella designata come centro dati Adobe Experience Platform hub (o principale).
>
> Inoltre, il motore di segmentazione edge rispetta solo le richieste relative alla rete Edge in cui è presente **uno** identità contrassegnata primaria, coerente con le identità primarie non basate su edge.

## Tipi di query di segmentazione Edge {#query-types}

Attualmente solo i tipi di query selezionati possono essere valutati con la segmentazione Edge. Le sezioni seguenti forniscono un elenco di tipi di query che possono essere valutati con la segmentazione Edge e di quelli che non sono attualmente supportati.

Una query può essere valutata con segmentazione Edge se soddisfa uno qualsiasi dei criteri descritti nella tabella seguente.

>[!NOTE]
>
>Se la query corrisponde a uno dei tipi di query della tabella seguente, verrà valutata automaticamente utilizzando la segmentazione Edge. Il sistema determina automaticamente questa capacità in base all&#39;espressione della query.

| Tipo di query | Dettagli | Esempio | Esempio PQL |
| ---------- | ------- | ------- | ----------- |
| Evento singolo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. | Persone che hanno aggiunto un articolo al carrello. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Profilo singolo | Qualsiasi definizione di segmento che fa riferimento a un singolo attributo di solo profilo | Persone che vivono negli Stati Uniti. | `homeAddress.countryCode = "US"` |
| Singolo evento che fa riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un singolo evento in ingresso senza restrizioni temporali. | Persone che vivono negli Stati Uniti che hanno visitato la homepage. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| Evento singolo negativo con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo negato e a uno o più attributi di profilo | Persone che vivono negli Stati Uniti e hanno **non** ha visitato la homepage. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Singolo evento all’interno di una finestra temporale | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo entro un periodo di tempo impostato. | Persone che hanno visitato la home page nelle ultime 24 ore. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| Singolo evento con un attributo di profilo all’interno di una finestra temporale | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un singolo evento in arrivo entro un periodo di tempo impostato. | Persone che vivono negli Stati Uniti e che hanno visitato la homepage nelle ultime 24 ore. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| Singolo evento negativo con un attributo di profilo all’interno di una finestra temporale | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un singolo evento in arrivo negato in un periodo di tempo. | Persone che vivono negli Stati Uniti e hanno **non** ha visitato la homepage nelle ultime 24 ore. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)]))` |
| Evento di frequenza entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a un evento che si verifica un certo numero di volte entro un intervallo di tempo di 24 ore. | Persone che hanno visitato la home page **almeno** cinque volte nelle ultime 24 ore. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento di frequenza con un attributo di profilo entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e un evento che si verifica un certo numero di volte entro un intervallo di tempo di 24 ore. | Persone dagli Stati Uniti che hanno visitato la homepage **almeno** cinque volte nelle ultime 24 ore. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento di frequenza negato con un profilo entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un evento negato che si verifica un certo numero di volte entro un intervallo di tempo di 24 ore. | Persone che non hanno visitato la home page **altro** cinque volte nelle ultime 24 ore. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Più hit in arrivo in un profilo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a più eventi che si verificano entro un intervallo di tempo di 24 ore. | Persone che hanno visitato la home page **o** ha visitato la pagina di pagamento nelle ultime 24 ore. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Più eventi con un profilo entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e più eventi che si verificano entro un intervallo di tempo di 24 ore. | Persone dagli Stati Uniti che hanno visitato la homepage **e** ha visitato la pagina di pagamento nelle ultime 24 ore. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segmento di segmenti | Qualsiasi definizione di segmento che contiene uno o più segmenti batch o in streaming. | Persone che vivono negli Stati Uniti e si trovano nel segmento &quot;esistente&quot;. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Query che fa riferimento a una mappa | Qualsiasi definizione di segmento che fa riferimento a una mappa di proprietà. | Persone che sono state aggiunte al carrello in base ai dati dei segmenti esterni. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

Una definizione di segmento **non** essere abilitato per la segmentazione Edge nei seguenti scenari:

- La definizione del segmento include una combinazione di un singolo evento e un `inSegment` evento.
   - Tuttavia, se il segmento contenuto in `inSegment` evento è solo profilo, la definizione del segmento **will** essere abilitato per la segmentazione Edge.

## Passaggi successivi

Questa guida spiega come valutare i segmenti con segmentazione Edge in Adobe Experience Platform. Per ulteriori informazioni sull’utilizzo dell’interfaccia utente di Experience Platform, consulta la sezione [Guida utente alla segmentazione](./overview.md). Per scoprire come eseguire azioni simili e lavorare con i segmenti utilizzando le API Experience Platform, visita il [guida dell’API per la segmentazione Edge](../api/edge-segmentation.md).

## Appendice

Nella sezione seguente sono elencate le domande frequenti relative alla segmentazione Edge:

### Quanto tempo ci vuole affinché un segmento sia disponibile sulla rete Edge?

È necessaria fino a un’ora affinché un segmento sia disponibile sulla rete Edge.