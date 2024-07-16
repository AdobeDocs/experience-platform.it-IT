---
solution: Experience Platform
title: Generare dati di esempio per uno schema XDM nell’interfaccia utente
description: Scopri come generare dati JSON di esempio in base a uno schema esistente nell’interfaccia utente di Adobe Experience Platform.
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 19a9341a9f53559fe3f619b2f157015e53b25b64
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 14%

---

# Generare dati di esempio per uno schema XDM nell’interfaccia utente {#generate-sample-data-for-an-xdm-schema}

>[!CONTEXTUALHELP]
>id="platform_xdm_downloadsamplefile"
>title="Scaricare file di esempio"
>abstract="Genera un oggetto JSON di esempio conforme alla struttura dello schema scelto. Questo oggetto può fungere da modello per garantire che i dati siano formattati correttamente per l’acquisizione in set di dati che utilizzano tale schema. Il file JSON di esempio verrà scaricato dal browser."

Per acquisire i dati in Adobe Experience Platform, il formato e la struttura dei dati devono essere conformi a uno schema Experience Data Model (XDM) esistente. A seconda della complessità dello schema per un particolare set di dati, può essere difficile determinare la forma esatta dei dati prevista dal set di dati al momento dell’acquisizione.

Per qualsiasi schema definito nell’interfaccia utente Experience Platform, puoi generare un oggetto JSON di esempio conforme alla struttura dello schema. Questo oggetto può fungere da modello per tutti i dati acquisiti nei set di dati che utilizzano lo schema in questione.

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Schemi]** nell&#39;area di navigazione a sinistra. Nella scheda **[!UICONTROL Sfoglia]**, individua lo schema per il quale desideri generare i dati di esempio. Selezionala dall’elenco e la barra a destra si aggiorna per mostrare i dettagli dello schema. Da qui, seleziona **[!UICONTROL Scarica il file di esempio]**.

![Scheda Sfoglia dell&#39;area di lavoro Schemi con uno schema selezionato ed evidenziato il file di esempio di download.](../images/ui/sample/sample-data.png)

Un esempio di file JSON viene scaricato dal browser. Ora puoi utilizzare questo file come riferimento per strutturare i dati al momento dell’acquisizione in set di dati che utilizzano questo schema.

## Passaggi successivi

Questa guida illustra come generare un file JSON di esempio da uno schema XDM nell’interfaccia utente di Platform. Per informazioni su come generare dati di esempio utilizzando l&#39;API Schema Registry, consulta la [guida dell&#39;endpoint dei dati di esempio](../api/sample-data.md).

Quando sei pronto per iniziare a acquisire i dati, consulta l&#39;esercitazione su [mappatura di un file CSV su XDM](../../ingestion/tutorials/map-csv/overview.md) per scoprire come mappare un file di dati flat (ad esempio CSV) su uno schema XDM e acquisirlo in Platform. In alternativa, è possibile stabilire una [connessione di origine](../../sources/home.md) per inserire i dati da un&#39;origine esterna e mapparli su XDM.

Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemi] nell&#39;interfaccia utente, fare riferimento alla panoramica dell&#39;area di lavoro [[!UICONTROL Schemi]](./overview.md).
