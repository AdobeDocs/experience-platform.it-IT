---
solution: Experience Platform
title: Generare dati di esempio per uno schema XDM nell’interfaccia utente
description: Scopri come generare dati JSON di esempio basati su uno schema esistente nell’interfaccia utente di Adobe Experience Platform.
topic-legacy: user guide
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Generare dati di esempio per uno schema XDM nell’interfaccia utente

Per acquisire i dati in Adobe Experience Platform, il formato e la struttura dei dati devono essere conformi a uno schema Experience Data Model (XDM) esistente. A seconda della complessità dello schema per un particolare set di dati, può essere difficile determinare la forma esatta dei dati che il set di dati si aspetta al momento dell’acquisizione.

Per qualsiasi schema definito nell’interfaccia utente di Experience Platform, puoi generare un oggetto JSON di esempio conforme alla struttura dello schema. Questo oggetto può fungere da modello per tutti i dati acquisiti nei set di dati che utilizzano lo schema in questione.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Schemas]** nel menu di navigazione a sinistra. Nella scheda **[!UICONTROL Browse]** , individua lo schema per il quale desideri generare i dati di esempio. Selezionala dall’elenco e la barra a destra si aggiorna per visualizzare i dettagli dello schema. Da qui, seleziona **[!UICONTROL Download sample file]**.

![](../images/ui/sample/sample-data.png)

Un file JSON di esempio viene scaricato dal browser. Ora puoi utilizzare questo file come riferimento per strutturare i dati durante l’acquisizione in set di dati che utilizzano questo schema.

## Passaggi successivi

Questa guida illustra come generare un file JSON di esempio da uno schema XDM nell’interfaccia utente di Platform. Per informazioni su come generare dati di esempio utilizzando l&#39;API del Registro di sistema dello schema, consulta la [guida per l&#39;endpoint di dati di esempio](../api/sample-data.md).

Quando sei pronto per iniziare ad acquisire i dati, consulta l’esercitazione su [mappatura di un file CSV su XDM](../../ingestion/tutorials/map-a-csv-file.md) per scoprire come mappare un file di dati flat (ad esempio un CSV) su uno schema XDM e assimilarlo in Platform. In alternativa, è possibile stabilire una [connessione di origine](../../sources/home.md) per inserire i dati da un&#39;origine esterna e mapparli su XDM.

Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemas] nell&#39;interfaccia utente, consulta la [[!UICONTROL Schemas] panoramica dell&#39;area di lavoro](./overview.md).
