---
solution: Experience Platform
title: Guida dell’interfaccia utente di segmentazione di Edge
description: Scopri come utilizzare la segmentazione Edge per valutare le definizioni dei segmenti in Platform istantaneamente al limite, abilitando casi di utilizzo di personalizzazione della pagina stessa e successiva.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 057db1432493a8443eb91b0fc371d0bdffb3de86
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---

# Guida all’interfaccia utente per la segmentazione Edge

>[!NOTE]
>
>La segmentazione di Edge è ora generalmente disponibile per tutti gli utenti di Platform. Se hai creato definizioni di segmenti edge durante la versione beta, queste definizioni di segmenti continueranno a essere operative.

La segmentazione di Edge consente di valutare i segmenti in Adobe Experience Platform [ istantaneamente al limite](../../web-sdk/home.md), abilitando casi di utilizzo di personalizzazione della pagina stessa e successiva.

>[!IMPORTANT]
>
> I dati edge verranno memorizzati in una posizione del server perimetrale più vicina al punto in cui sono stati raccolti e possono essere memorizzati in una posizione diversa da quella designata come centro dati Adobe Experience Platform hub (o principale).
>
> Inoltre, il motore di segmentazione Edge rispetterà solo le richieste sul server Edge in cui è presente **una** identità primaria contrassegnata, il che è coerente con le identità primarie non basate su Edge.

## Tipi di query di segmentazione di Edge {#query-types}

Attualmente solo i tipi di query selezionati possono essere valutati con la segmentazione Edge. Le sezioni seguenti forniscono un elenco di tipi di query che possono essere valutati con la segmentazione Edge e di quelli che non sono attualmente supportati.

Una query può essere valutata con segmentazione Edge se soddisfa uno qualsiasi dei criteri descritti nella tabella seguente.

>[!NOTE]
>
>Se la query corrisponde a uno dei tipi di query della tabella seguente, verrà valutata automaticamente utilizzando la segmentazione Edge. Il sistema determina automaticamente questa capacità in base all&#39;espressione della query.

| Tipo di query | Dettagli |
| ---------- | ------- |
| Evento singolo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. |
| Singolo evento entro una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo. |
| Evento singolo con finestra temporale | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo con una finestra temporale. |
| Solo profilo | Qualsiasi definizione di segmento che fa riferimento solo a un attributo di profilo. |
| Singolo evento con un attributo di profilo entro un intervallo di tempo relativo inferiore a 24 ore | Qualsiasi definizione di segmento che si riferisce a un singolo evento in arrivo, con uno o più attributi di profilo, e si verifica entro un intervallo di tempo relativo inferiore a 24 ore. |
| Segmento di segmenti | Qualsiasi definizione di segmento che contiene uno o più segmenti batch o in streaming. **Nota:** se si utilizza un segmento di segmenti, l&#39;annullamento del profilo avverrà **ogni 24 ore**. |
| Più eventi con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a più eventi **nelle ultime 24 ore** e (facoltativamente) ha uno o più attributi di profilo. |

Una definizione di segmento **non** verrà abilitata per la segmentazione Edge nel seguente scenario:

- La definizione del segmento include una combinazione di un singolo evento e un evento `inSegment`.
   - Tuttavia, se la definizione del segmento contenuta nell&#39;evento `inSegment` è solo di profilo, la definizione del segmento **sarà** abilitata per la segmentazione Edge.
- La definizione del segmento utilizza &quot;Ignora anno&quot; come parte dei vincoli di tempo.

## Passaggi successivi

Questa guida spiega come valutare le definizioni dei segmenti con la segmentazione Edge in Adobe Experience Platform. Per ulteriori informazioni sull&#39;utilizzo dell&#39;interfaccia utente di Experience Platform, leggere la [Guida utente per la segmentazione](./overview.md). Per informazioni su come eseguire azioni simili e lavorare con le definizioni dei segmenti utilizzando le API Experience Platform, visita la [guida dell&#39;API di segmentazione Edge](../api/edge-segmentation.md).

## Appendice

Nella sezione seguente sono elencate le domande frequenti relative alla segmentazione Edge:

### Quanto tempo ci vuole affinché la definizione di un segmento sia disponibile nell’Edge Network?

È necessaria fino a un’ora perché la definizione di un segmento sia disponibile nell’Edge Network.
