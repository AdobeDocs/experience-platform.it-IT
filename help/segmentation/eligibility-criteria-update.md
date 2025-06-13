---
title: Aggiornamento dei criteri di idoneità alla segmentazione
description: Scopri gli aggiornamenti dei criteri di idoneità alla segmentazione che influenzano i tipi di pubblico che possono essere valutati utilizzando lo streaming e la segmentazione Edge.
hide: true
hidefromtoc: true
exl-id: c91c0f75-9bc8-4fa7-9d27-9b07d0ea560c
source-git-commit: 6935cee30adb59d52db6c6fed7036f81b54edd52
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 2%

---

# Aggiornamento dei criteri di idoneità alla segmentazione

>[!IMPORTANT]
>
>Tutte le definizioni di segmenti esistenti attualmente valutate utilizzando lo streaming o la segmentazione Edge continueranno a funzionare così come sono, a meno che non vengano modificate o aggiornate.

A partire dal 20 maggio 2025, verranno effettuati tre aggiornamenti che influiscono sull’idoneità alla segmentazione.

1. Set di regole idoneo
2. Idoneità all’intervallo temporale
3. Inclusione di dati batch nei tipi di pubblico in streaming
4. Criteri di unione attivi

## Set di regole {#ruleset}

Qualsiasi definizione di segmento **nuova o modificata** che corrisponde ai seguenti set di regole **non sarà più** valutata mediante streaming o segmentazione Edge. Verranno invece valutati utilizzando la segmentazione batch.

- Un singolo evento con una finestra temporale più lunga di 24 ore
   - Attiva un pubblico con tutti i profili che hanno visualizzato una pagina web negli ultimi 3 giorni.
- Un singolo evento senza finestra temporale
   - Attiva un pubblico con tutti i profili che hanno visualizzato una pagina web.

## Finestra temporale {#time-window}

Per valutare un pubblico con segmentazione in streaming, **deve** essere vincolato entro un intervallo di tempo di 24 ore.

## Inclusione di dati batch nei tipi di pubblico in streaming {#include-batch-data}

Prima di questo aggiornamento, era possibile creare una definizione di pubblico in streaming che combinasse origini dati in batch e in streaming. Tuttavia, con l’ultimo aggiornamento, la creazione di un pubblico con origini di dati in batch e in streaming verrà valutata utilizzando la segmentazione batch.

Se devi valutare una definizione di segmento utilizzando la segmentazione in streaming o Edge che corrisponde al set di regole aggiornato, devi creare esplicitamente un batch e un set di regole in streaming e combinarli utilizzando un segmento di segmenti. Il set di regole batch **deve** essere basato su uno schema di profilo.

Ad esempio, supponiamo che tu abbia due tipi di pubblico, con un pubblico che ospita i dati dello schema del profilo e gli altri dati dello schema dell’evento dell’esperienza di alloggio:

| Pubblico | Schema | Tipo di Source | Definizione query | ID pubblico |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Residenti in California | Profilo | Sorgente batch | L&#39;indirizzo dell&#39;abitazione è nello stato della California | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Pagamenti recenti | Evento esperienza | Origine streaming | Ha almeno un pagamento nelle ultime 24 ore | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Se desideri utilizzare il componente batch nel pubblico in streaming, devi fare riferimento al pubblico batch utilizzando un segmento di segmenti.

Quindi, un set di regole di esempio che combinasse i due tipi di pubblico si presenterebbe come segue:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

Il pubblico risultante *sarà* valutato utilizzando la segmentazione in streaming, poiché sfrutta l&#39;appartenenza del pubblico batch facendo riferimento al componente pubblico batch.

Tuttavia, se desideri combinare due tipi di pubblico con i dati dell&#39;evento, **non è possibile** semplicemente combinare i due eventi. È necessario creare entrambi i tipi di pubblico, quindi creare un altro pubblico che utilizza `inSegment` per fare riferimento a entrambi.

Ad esempio, supponiamo che tu abbia due tipi di pubblico, entrambi contenenti i dati dello schema dell’evento esperienza:

| Pubblico | Schema | Tipo di Source | Definizione query | ID pubblico |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Abbandoni recenti | Evento esperienza | Sorgente batch | Ha almeno un evento di abbandono nelle ultime 48 ore | `7deb246a-49b4-4687-95f9-6316df049948` |
| Pagamenti recenti | Evento esperienza | Origine streaming | Ha almeno un pagamento nelle ultime 24 ore | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

In questa situazione, devi creare un terzo pubblico come segue:

```
inSegment("7deb246a-49b4-4687-95f9-6316df049948") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

>[!IMPORTANT]
>
>Tutte le definizioni di segmenti esistenti che corrispondono ai set di regole rimarranno valutate utilizzando lo streaming o la segmentazione Edge fino a quando non verranno modificate.
>
>Inoltre, tutte le definizioni di segmenti esistenti che attualmente soddisfano gli altri criteri di valutazione della segmentazione in streaming o Edge rimarranno valutate con la segmentazione in streaming o Edge.

## Criterio di unione {#merge-policy}

Qualsiasi definizione di segmento **nuova o modificata** idonea per lo streaming o la segmentazione Edge **deve** essere nel criterio di unione &quot;Attivo su Edge&quot;.

Se non è impostato alcun criterio di unione attivo, è necessario [configurare il criterio di unione](../profile/merge-policies/ui-guide.md#configure) e impostarlo per essere attivo sul server Edge.
