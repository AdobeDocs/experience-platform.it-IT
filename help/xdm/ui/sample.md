---
solution: Experience Platform
title: Genera dati di esempio per uno schema XDM nell'interfaccia utente
description: Scopri come generare dati JSON di esempio basati su uno schema esistente nell’interfaccia utente di Adobe Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 8d6916890a94300dc68d018d56579df9616c177c
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Generazione di dati di esempio per uno schema XDM nell&#39;interfaccia utente

Per trasferire i dati in Adobe Experience Platform, il formato e la struttura dei dati devono essere conformi a uno schema XDM (Experience Data Model) esistente. A seconda della complessità dello schema per un particolare set di dati, può essere difficile determinare la forma esatta dei dati che il set di dati prevede al momento dell&#39;assimilazione.

Per qualsiasi schema definito nell&#39;interfaccia utente del Experience Platform , è possibile generare un oggetto JSON di esempio conforme alla struttura dello schema. Questo oggetto può fungere da modello per qualsiasi dato assimilato in set di dati che utilizzano lo schema in questione.

Nell&#39;interfaccia utente della piattaforma, selezionate **[!UICONTROL Schemas]** nel menu di navigazione a sinistra. Nella scheda **[!UICONTROL Browse]**, individuare lo schema per il quale si desidera generare i dati di esempio. Selezionatela dall&#39;elenco e nella barra laterale destra vengono aggiornati i dettagli relativi allo schema. Da qui, selezionare **[!UICONTROL Download sample file]**.

![](../images/ui/sample/sample-data.png)

Un file JSON di esempio viene scaricato dal browser. È ora possibile utilizzare questo file come riferimento per la struttura dei dati durante l&#39;assimilazione in set di dati che utilizzano questo schema.

## Passaggi successivi

In questa guida è stato illustrato come generare un file JSON di esempio da uno schema XDM nell&#39;interfaccia utente della piattaforma. Per informazioni su come generare dati di esempio utilizzando l&#39;API del Registro di sistema dello schema, vedere la [guida dell&#39;endpoint di dati di esempio](../api/sample-data.md).

Una volta pronti per iniziare l&#39;assimilazione dei dati, vedete l&#39;esercitazione su [mappatura di un file CSV su XDM](../../ingestion/tutorials/map-a-csv-file.md) per apprendere come mappare un file di dati semplice (ad esempio un CSV) su uno schema XDM e come assimilarlo nella piattaforma. In alternativa, è possibile stabilire una [connessione di origine](../../sources/home.md) per inserire i dati da un&#39;origine esterna e mapparli su XDM.

Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemas] nell&#39;interfaccia utente, fare riferimento alla [[!UICONTROL Schemas] panoramica dell&#39;area di lavoro](./overview.md).