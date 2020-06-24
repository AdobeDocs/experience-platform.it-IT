---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Esercitazioni sulla segmentazione
topic: tutorial
translation-type: tm+mt
source-git-commit: b0ef50e25c27aba121bb01c602867953eb2a5f7e
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---


# Esercitazioni sulla segmentazione

 Adobe Experience Platform Segmentation Service fornisce un&#39;interfaccia utente e RESTful API che consente di creare segmenti e generare audience dai dati del profilo cliente in tempo reale. Questi segmenti sono configurati e mantenuti a livello centrale su Platform e sono facilmente accessibili da qualsiasi soluzione Adobe. Per ulteriori informazioni sulla segmentazione, leggi la panoramica [del servizio di](../segmentation/home.md)segmentazione.

## Creare una definizione di segmento

Per definizione del segmento si intende il set di regole utilizzato per descrivere le caratteristiche o il comportamento chiave di un&#39;audience di destinazione. Una volta concettualizzate, le regole delineate in una definizione di segmento vengono utilizzate per determinare i membri di pubblico idonei per un segmento. Lo sviluppo, il test, l&#39;anteprima e il salvataggio di una definizione di segmento possono essere eseguiti utilizzando l&#39;interfaccia utente o le API di Platform. Per creare una definizione di segmento, segui l’esercitazione [sulla](../segmentation/tutorials/create-a-segment.md) creazione di un segmento API o la guida [utente per l’interfaccia utente di](../segmentation/ui/overview.md)Segment Builder.

## Valutazione di un segmento e risultati di accesso

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi valutare il segmento tramite una valutazione programmata o su richiesta. La valutazione pianificata (nota anche come &quot;segmentazione pianificata&quot;) consente di creare una pianificazione periodica per l’esecuzione di un processo di esportazione in un momento specifico, mentre la valutazione su richiesta comporta la creazione di un processo segmento per creare immediatamente l’audience. Per ulteriori informazioni, consulta l’esercitazione per [valutare e accedere ai risultati](../segmentation/tutorials/evaluate-a-segment.md)del segmento.

## Esportare i dati dei segmenti

Per esportare i segmenti contenenti dati di profilo è necessario innanzitutto [creare un set di dati in cui esportare](../segmentation/tutorials/create-dataset-export-segment.md)i dati, quindi avviare un nuovo processo di esportazione. I passaggi per generare un processo di esportazione si trovano nell’esercitazione [API di](../segmentation/tutorials/export-data.md)esportazione.

## Configurare i criteri di unione

 Adobe Experience Platform consente di unire dati provenienti da più origini e combinarli per visualizzare una visione completa di ogni singolo cliente. Quando si uniscono questi dati, i criteri di unione sono le regole utilizzate da Platform per determinare in che modo i dati verranno classificati come priorità e quali dati verranno combinati per creare tale visualizzazione unificata. Utilizzando le API RESTful o l&#39;interfaccia utente, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Per utilizzare i criteri di unione nell&#39;interfaccia utente di Platform, consultare la guida [utente relativa ai criteri di](../profile/ui/merge-policies.md)unione. Per lavorare con i criteri di unione utilizzando l&#39;API Profilo cliente in tempo reale, consulta la guida [per gli sviluppatori dei criteri di](../profile/api/merge-policies.md)unione.

## Applica la conformità all&#39;uso dei dati per i segmenti

I segmenti abilitati per l’uso in Profilo cliente in tempo reale contengono un ID criterio di unione all’interno della definizione del segmento. Questo criterio di unione contiene informazioni sui set di dati da includere nel segmento, che a loro volta contengono eventuali etichette di utilizzo dei dati applicabili. Per passaggi specifici relativi all&#39;applicazione della conformità dell&#39;utilizzo dei dati per un segmento di pubblico, segui l&#39;esercitazione sull&#39;applicazione della conformità dell&#39;uso [dei dati per i segmenti](../segmentation/tutorials/governance.md).

## Segmentazione in streaming

La segmentazione in streaming consente di valutare istantaneamente un cliente non appena un evento entra in un particolare gruppo di segmenti. Grazie a questa funzionalità, ora è possibile valutare la maggior parte delle regole del segmento in quanto i dati vengono passati  Adobe Experience Platform, il che significa che l&#39;appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati. Per saperne di più, visita la panoramica sulla segmentazione [in streaming](../segmentation/api/streaming-segmentation.md).

## Segmentazione multi-entità

La segmentazione multi-entità è la capacità di estendere i dati del profilo con dati aggiuntivi basati su prodotti, store o altre classi non di profilo. Una volta connessi, i dati di altre classi diventano disponibili come se fossero nativi dello schema Profilo. Per informazioni su come spostarsi, consulta la documentazione [sulla segmentazione](../segmentation/multi-entity-segmentation.md)multi-entità.