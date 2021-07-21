---
keywords: Experience Platform;home;argomenti popolari;segmentazione edge;Segmentazione;Servizio di segmentazione;servizio di segmentazione;guida interfaccia utente;bordo streaming;
solution: Experience Platform
title: Guida all’interfaccia utente di Segmentazione bordo
topic-legacy: ui guide
description: La segmentazione dei bordi è la capacità di valutare istantaneamente i segmenti in Platform sul bordo, abilitando casi d’uso di personalizzazione della pagina e della stessa pagina.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 8375d5a35ef652335c60b4b8b4571bf42ec1924a
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 4%

---

# Guida all’interfaccia utente per la segmentazione dei bordi (versione beta)

>[!NOTE]
>
>La segmentazione dei bordi è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

La segmentazione dei bordi è la capacità di valutare i segmenti in Adobe Experience Platform istantaneamente sul bordo, abilitando casi d’uso di personalizzazione della pagina stessa e di pagina successiva.

## Tipi di query per segmentazione Edge

È possibile valutare una query con segmentazione edge se soddisfa uno dei seguenti criteri:

| Tipo di query | Dettagli | Esempio |
| ---------- | ------- | ------- |
| Hit in entrata | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| Hit in entrata che fa riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo, senza restrizioni di tempo, e a uno o più attributi di profilo. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| Query di frequenza | Qualsiasi definizione di segmento che fa riferimento a un evento che si verifica almeno un certo numero di volte. |  |
| Query di frequenza che fa riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a un evento che si verifica almeno un determinato numero di volte e presenta uno o più attributi di profilo. |  |

Se la query corrisponde a uno qualsiasi dei tipi di query di cui sopra, verrà valutata automaticamente utilizzando la segmentazione edge.

I seguenti tipi di query sono **non** attualmente supportati per la segmentazione edge:

| Tipo di query | Dettagli |
| ---------- | ------- |
| Intervallo di tempo relativo | Se una query fa riferimento a una finestra temporale, non può essere valutata utilizzando la segmentazione edge. |
| Negazione | Se una query contiene una negazione o un evento `not`, non può essere valutata utilizzando la segmentazione edge. |
| Eventi multipli | Se una query contiene più di un evento, non può essere valutata utilizzando la segmentazione edge. |

## Passaggi successivi

Questa guida utente spiega come valutare i segmenti con la segmentazione edge su Adobe Experience Platform.

Per ulteriori informazioni sull&#39;utilizzo dell&#39;interfaccia utente di Adobe Experience Platform, consulta la [Guida utente alla segmentazione](./overview.md). Per informazioni su come eseguire azioni simili e lavorare con segmenti utilizzando l’interfaccia utente di Adobe Experience Platform, visita la [guida API di segmentazione edge](../api/edge-segmentation.md).
