---
keywords: Experience Platform;home;argomenti popolari;segmentazione edge;Segmentazione;Servizio di segmentazione;servizio di segmentazione;guida interfaccia utente;bordo streaming;
solution: Experience Platform
title: Guida all’interfaccia utente di Segmentazione bordo
topic-legacy: ui guide
description: La segmentazione dei bordi è la capacità di valutare istantaneamente i segmenti in Platform sul bordo, abilitando casi d’uso di personalizzazione della pagina e della stessa pagina.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 6bb1f417b5856f153adebe4deaac4fab264ef3a8
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 3%

---

# Guida all’interfaccia utente per la segmentazione dei bordi (versione beta)

>[!IMPORTANT]
>
>La segmentazione dei bordi è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

La segmentazione dei bordi è la capacità di valutare i segmenti in Adobe Experience Platform istantaneamente [sul bordo](../../edge/home.md), abilitando casi d’uso di personalizzazione della pagina e di pagina successiva.

## Tipi di query per segmentazione Edge

Attualmente è possibile valutare solo i tipi di query selezionati con la segmentazione edge. Le sezioni seguenti forniscono un elenco dei tipi di query che possono essere valutati con la segmentazione edge e quelli che non sono attualmente supportati.

### Tipi di query supportati

Una query può essere valutata con segmentazione edge se soddisfa uno dei criteri descritti nella tabella seguente.

>[!NOTE]
>
>Se la query corrisponde a uno qualsiasi dei tipi di query nella tabella seguente, verrà valutata automaticamente utilizzando la segmentazione edge. Il sistema determina automaticamente questa capacità in base all&#39;espressione della query.

| Tipo di query | Dettagli | Esempio |
| ---------- | ------- | ------- |
| Hit in entrata | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| Hit in entrata che fa riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo, senza restrizioni di tempo, e a uno o più attributi di profilo. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| Hit in arrivo con una finestra temporale di 24 ore | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo entro 24 ore |  |
| Hit in arrivo che si riferisce a un profilo con una finestra temporale di 24 ore | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo entro 24 ore e a uno o più attributi di profilo |  |

### Tipi di query non attualmente supportati

I seguenti tipi di query sono **non** attualmente supportati per la segmentazione edge:

| Tipo di query | Dettagli |
| ---------- | ------- |
| Eventi multipli | Se una query contiene più di un evento, non può essere valutata utilizzando la segmentazione edge. |
| Query di frequenza | Qualsiasi definizione di segmento che fa riferimento a un evento che si verifica almeno un certo numero di volte. |  |
| Query di frequenza che fa riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a un evento che si verifica almeno un determinato numero di volte e presenta uno o più attributi di profilo. |  |

## Passaggi successivi

Questa guida spiega come valutare i segmenti con la segmentazione edge su Adobe Experience Platform. Per ulteriori informazioni sull&#39;utilizzo dell&#39;interfaccia utente di Experience Platform, consulta la [Guida utente alla segmentazione](./overview.md). Per informazioni su come eseguire azioni simili e lavorare con segmenti utilizzando le API di Experience Platform, visita la [guida API di segmentazione edge](../api/edge-segmentation.md).
