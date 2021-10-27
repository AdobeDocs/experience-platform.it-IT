---
keywords: Experience Platform;home;argomenti popolari;segmentazione edge;Segmentazione;Servizio di segmentazione;servizio di segmentazione;guida interfaccia utente;bordo streaming;
solution: Experience Platform
title: Guida all’interfaccia utente di Segmentazione bordo
topic-legacy: ui guide
description: La segmentazione dei bordi è la capacità di valutare istantaneamente i segmenti in Platform sul bordo, abilitando casi d’uso di personalizzazione della pagina e della stessa pagina.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: bb5a56557ce162395511ca9a3a2b98726ce6c190
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---

# Guida all’interfaccia utente per la segmentazione dei bordi (versione beta)

>[!IMPORTANT]
>
>La segmentazione dei bordi è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

La segmentazione dei bordi è la capacità di valutare istantaneamente i segmenti in Adobe Experience Platform [sul bordo](../../edge/home.md), l’abilitazione di casi d’uso di personalizzazione pagina e pagina successiva.

## Tipi di query per segmentazione Edge

Attualmente è possibile valutare solo i tipi di query selezionati con la segmentazione edge. Le sezioni seguenti forniscono un elenco dei tipi di query che possono essere valutati con la segmentazione edge e quelli che non sono attualmente supportati.

### Tipi di query supportati

Una query può essere valutata con segmentazione edge se soddisfa uno dei criteri descritti nella tabella seguente.

>[!NOTE]
>
>Se la query corrisponde a uno qualsiasi dei tipi di query nella tabella seguente, verrà valutata automaticamente utilizzando la segmentazione edge. Il sistema determina automaticamente questa capacità in base all&#39;espressione della query.

| Tipo di query | Dettagli | Esempio |
| ---------- | ------- | ------- |
| Evento singolo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. | Persone che hanno aggiunto un elemento al carrello. |
| Singolo evento che fa riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un singolo evento in arrivo senza restrizioni di tempo. | Persone che vivono negli Stati Uniti che hanno visitato la homepage. |
| Singolo evento ignorato con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in entrata negato e a uno o più attributi di profilo | Persone che vivono negli Stati Uniti e che hanno **not** Ho visitato la homepage. |
| Singolo evento in una finestra temporale di 24 ore | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo entro 24 ore. | Persone che hanno visitato la homepage nelle ultime 24 ore. |
| Singolo evento con un attributo di profilo entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un singolo evento in arrivo negato entro 24 ore. | Persone che vivono negli Stati Uniti che hanno visitato la homepage nelle ultime 24 ore. |
| Singolo evento ignorato con un attributo di profilo entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un singolo evento in arrivo negato entro 24 ore. | Persone che vivono negli Stati Uniti e che hanno **not** Ho visitato la homepage nelle ultime 24 ore. |
| Evento di frequenza entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a un evento che si verifica un certo numero di volte all’interno di un intervallo di tempo di 24 ore. | Persone che hanno visitato la homepage **almeno** cinque volte nelle ultime 24 ore. |
| Evento di frequenza con un attributo di profilo entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un evento che si verifica un certo numero di volte all’interno di un intervallo di tempo di 24 ore. | Persone dagli Stati Uniti che hanno visitato la homepage **almeno** cinque volte nelle ultime 24 ore. |
| Evento di frequenza ignorato con un profilo entro una finestra temporale di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un evento negato che si verifica un certo numero di volte all’interno di un intervallo di tempo di 24 ore. | Persone che non hanno visitato la homepage **more** cinque volte nelle ultime 24 ore. |
| Più hit in arrivo in un profilo temporale di 24 ore | Una definizione di segmento che fa riferimento a più eventi che si verificano all’interno di un intervallo di tempo di 24 ore. | Persone che hanno visitato la homepage **o** Ho visitato la pagina di pagamento nelle ultime 24 ore. |
| Eventi multipli con un profilo entro una finestra temporale di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a più eventi che si verificano all’interno di un intervallo di tempo di 24 ore. | Persone dagli Stati Uniti che hanno visitato la homepage **e** Ho visitato la pagina di pagamento nelle ultime 24 ore. |

## Passaggi successivi

Questa guida spiega come valutare i segmenti con la segmentazione edge su Adobe Experience Platform. Per ulteriori informazioni sull’utilizzo dell’interfaccia utente di Experience Platform, consulta la sezione [Guida utente alla segmentazione](./overview.md). Per informazioni su come eseguire azioni simili e lavorare con i segmenti utilizzando le API di Experience Platform, visita il [guida API per la segmentazione edge](../api/edge-segmentation.md).
