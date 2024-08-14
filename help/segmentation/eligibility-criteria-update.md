---
title: Aggiornamento dei criteri di idoneità alla segmentazione
description: Scopri gli aggiornamenti dei criteri di idoneità alla segmentazione che influenzano i tipi di pubblico che possono essere valutati utilizzando lo streaming e la segmentazione Edge.
hide: true
hidefromtoc: true
source-git-commit: 0bbee2100ed6fdc0f40457965e195d07de6eb2a1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Aggiornamento dei criteri di idoneità alla segmentazione

A partire dal 24 settembre 2024, verranno effettuati due aggiornamenti che influiscono sull’idoneità alla segmentazione.

1. Tipi di query di segmentazione in streaming e edge
2. Criteri di unione per lo streaming e la segmentazione Edge

## Tipi di query

Qualsiasi definizione di segmento **nuova o modificata** che corrisponde ai seguenti tipi di query **non sarà più** valutata mediante streaming o segmentazione Edge. Verranno invece valutati utilizzando la segmentazione batch.

- Un singolo evento con una finestra temporale più lunga di 24 ore
   - Attiva un pubblico con tutti i profili che hanno visualizzato una pagina web negli ultimi 3 giorni.
- Un singolo evento senza finestra temporale
   - Attiva un pubblico con tutti i profili che hanno visualizzato una pagina web.

Se devi valutare una definizione di segmento utilizzando lo streaming o la segmentazione Edge che corrisponde al tipo di query aggiornato, puoi creare esplicitamente un batch e una query in streaming e combinarli utilizzando un segmento di segmenti.

Ad esempio, se devi attivare un pubblico con tutti i profili che hanno visualizzato una pagina web negli ultimi 3 giorni utilizzando la segmentazione in streaming, puoi creare le seguenti query:

- Q1 (Streaming): tutti i profili che hanno visualizzato una pagina web nelle ultime 24 ore
- Q2 (Batch): tutti i profili che hanno visualizzato una pagina web negli ultimi 3 giorni

Poi, si possono combinare facendo riferimento al primo o al secondo trimestre.

Allo stesso modo, se devi attivare un pubblico con tutti i profili che hanno visualizzato una pagina web, puoi creare le seguenti query:

- Q3 (Streaming): tutti i profili che hanno visualizzato una pagina web nelle ultime 24 ore
- Q4 (Batch): tutti i profili che hanno visualizzato una pagina web.

In seguito, è possibile combinarle facendo riferimento al terzo o al quarto trimestre.

>[!IMPORTANT]
>
>Tutte le definizioni di segmenti esistenti che corrispondono ai tipi di query rimarranno valutate utilizzando lo streaming o la segmentazione Edge fino a quando non verranno modificate.
>
>Inoltre, tutte le definizioni di segmenti esistenti che attualmente soddisfano gli altri criteri di valutazione della segmentazione in streaming o Edge rimarranno valutate con la segmentazione in streaming o Edge.

## Criterio di unione

Qualsiasi definizione di segmento **nuova o modificata** idonea per lo streaming o la segmentazione Edge **deve** essere nel criterio di unione &quot;Attivo su Edge&quot;.

Tutte le definizioni di segmenti esistenti valutate utilizzando lo streaming o la segmentazione Edge continueranno a funzionare così come sono.
