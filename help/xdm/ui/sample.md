---
solution: Experience Platform
title: Generare dati di esempio per uno schema XDM nell’interfaccia utente
description: Scopri come generare dati JSON di esempio basati su uno schema esistente nell’interfaccia utente di Adobe Experience Platform.
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Generare dati di esempio per uno schema XDM nell’interfaccia utente

Per acquisire i dati in Adobe Experience Platform, il formato e la struttura dei dati devono essere conformi a uno schema Experience Data Model (XDM) esistente. A seconda della complessità dello schema per un particolare set di dati, può essere difficile determinare la forma esatta dei dati che il set di dati si aspetta al momento dell’acquisizione.

Per qualsiasi schema definito nell’interfaccia utente di Experience Platform, puoi generare un oggetto JSON di esempio conforme alla struttura dello schema. Questo oggetto può fungere da modello per tutti i dati acquisiti nei set di dati che utilizzano lo schema in questione.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Schemi]** nella navigazione a sinistra. Sotto la **[!UICONTROL Sfoglia]** individuare lo schema per il quale si desidera generare i dati di esempio. Selezionala dall’elenco e la barra a destra si aggiorna per visualizzare i dettagli dello schema. Da qui, seleziona **[!UICONTROL Scarica il file di esempio]**.

![](../images/ui/sample/sample-data.png)

Un file JSON di esempio viene scaricato dal browser. Ora puoi utilizzare questo file come riferimento per strutturare i dati durante l’acquisizione in set di dati che utilizzano questo schema.

## Passaggi successivi

Questa guida illustra come generare un file JSON di esempio da uno schema XDM nell’interfaccia utente di Platform. Per informazioni su come generare dati di esempio utilizzando l’API del Registro di sistema dello schema, consulta [guida all’endpoint dati di esempio](../api/sample-data.md).

Quando sei pronto per iniziare l’acquisizione dei dati, consulta l’esercitazione su [mappatura di un file CSV in XDM](../../ingestion/tutorials/map-csv/overview.md) per scoprire come mappare un file di dati flat (ad esempio un CSV) su uno schema XDM e trasferirlo in Platform. In alternativa, è possibile stabilire un [connessione sorgente](../../sources/home.md) per inserire i dati da un’origine esterna e mapparli su XDM.

Per ulteriori informazioni sulle funzionalità del [!UICONTROL Schemi] nell’interfaccia utente, fai riferimento alla [[!UICONTROL Schemi] panoramica dell&#39;area di lavoro](./overview.md).
