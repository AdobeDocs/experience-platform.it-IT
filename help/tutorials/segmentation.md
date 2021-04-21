---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Tutorial sulla segmentazione
topic-legacy: tutorial
type: Tutorial
description: Il servizio di segmentazione di Adobe Experience Platform fornisce un’interfaccia utente e RESTful API che consente di creare segmenti e generare tipi di pubblico dai dati del profilo cliente in tempo reale. Questi segmenti sono configurati e mantenuti a livello centrale su Platform e sono facilmente accessibili da qualsiasi soluzione Adobe.
exl-id: e45de6b5-ff71-4908-ad79-898084763704
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Tutorial sulla segmentazione

Adobe Experience Platform [!DNL Segmentation Service] fornisce un’interfaccia utente e RESTful API che consente di creare segmenti e generare tipi di pubblico dai dati [!DNL Real-time Customer Profile]. Questi segmenti sono configurati e mantenuti a livello centrale su [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione di Adobe. Per ulteriori informazioni sulla segmentazione, inizia leggendo la [Panoramica del servizio di segmentazione](../segmentation/home.md).

## Creare una definizione di segmento

Una definizione di segmento è il set di regole utilizzato per descrivere le caratteristiche o il comportamento chiave di un pubblico target. Una volta concettualizzate, le regole descritte in una definizione di segmento vengono utilizzate per determinare i membri del pubblico qualificati per un segmento. Lo sviluppo, il test, l’anteprima e il salvataggio di una definizione di segmento possono essere eseguiti utilizzando l’ interfaccia utente o le API [!DNL Platform] . Per creare una definizione di segmento, segui il [tutorial sulla creazione di un segmento API](../segmentation/tutorials/create-a-segment.md) o la [guida utente dell’interfaccia utente del Generatore di segmenti](../segmentation/ui/overview.md).

## Valutazione di un segmento e risultati di accesso

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi valutarlo tramite una valutazione programmata o on demand. La valutazione pianificata (nota anche come &quot;segmentazione pianificata&quot;) consente di creare una pianificazione periodica per l’esecuzione di un processo di esportazione in un momento specifico, mentre la valutazione su richiesta comporta la creazione di un processo di segmento per generare il pubblico immediatamente. Per ulteriori informazioni, visita l’esercitazione per [valutare e accedere ai risultati dei segmenti](../segmentation/tutorials/evaluate-a-segment.md).

## Esportare i dati dei segmenti

Per esportare i segmenti contenenti dati [!DNL Profile] è necessario prima [creare un set di dati in cui esportare i dati](../segmentation/tutorials/create-dataset-export-segment.md), quindi avviare un nuovo processo di esportazione. I passaggi per generare un processo di esportazione si trovano nell&#39;esercitazione su [valutazione di un segmento](../segmentation/tutorials/evaluate-a-segment.md).

## Configurare i criteri di unione

Adobe Experience Platform consente di unire dati provenienti da più sorgenti e combinarli per visualizzare una visione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare tale visualizzazione unificata. Utilizzando le API RESTful o l&#39;interfaccia utente, è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la propria organizzazione. Per utilizzare i criteri di unione nell&#39;interfaccia utente [!DNL Platform], visita la [guida utente dei criteri di unione](../profile/ui/merge-policies.md). Per utilizzare i criteri di unione utilizzando l&#39;API [!DNL Real-time Customer Profile], consulta la [guida per gli sviluppatori dei criteri di unione](../profile/api/merge-policies.md).

## Applicare la conformità per l’utilizzo dei dati per i segmenti

I segmenti abilitati per l’uso in [!DNL Real-time Customer Profile] contengono un ID criterio di unione all’interno della relativa definizione del segmento. Questo criterio di unione contiene informazioni sui set di dati da includere nel segmento, che a loro volta contengono eventuali etichette di utilizzo dei dati applicabili. Per passaggi specifici sull&#39;applicazione della conformità per l&#39;utilizzo dei dati per un segmento di pubblico, segui il [tutorial sull&#39;applicazione della conformità per l&#39;utilizzo dei dati per i segmenti](../segmentation/tutorials/governance.md).

## Segmentazione streaming

La segmentazione in streaming è la capacità di valutare istantaneamente un cliente non appena un evento entra in un particolare gruppo di segmenti. Con questa funzionalità, la maggior parte delle regole del segmento può ora essere valutata quando i dati vengono trasmessi in Adobe Experience Platform, il che significa che l’appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati. Per ulteriori informazioni, visita la [panoramica sulla segmentazione in streaming](../segmentation/api/streaming-segmentation.md).

## Segmentazione su più entità

La segmentazione multi-entità è la capacità di estendere i dati [!DNL Profile] con dati aggiuntivi basati su prodotti, store o altre classi non di profilo. Una volta connessi, i dati provenienti da classi aggiuntive diventano disponibili come se fossero nativi dello schema [!DNL Profile]. Per informazioni sullo spostamento, consulta la [documentazione sulla segmentazione su più entità](../segmentation/multi-entity-segmentation.md).
