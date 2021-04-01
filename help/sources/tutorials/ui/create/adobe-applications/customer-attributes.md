---
keywords: Experience Platform;home;argomenti popolari;attributi del cliente
solution: Experience Platform
title: Creare una connessione sorgente attributi cliente nell’interfaccia utente
topic: ' - Panoramica'
type: Tutorial
description: Scopri come creare una connessione sorgente nell’interfaccia utente per raccogliere i dati del profilo degli attributi del cliente in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 08a3026e969a8739a8b57226c35a6d1d3150006e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 6%

---


# Creare una connessione sorgente Attributi del cliente nell&#39;interfaccia utente

Questa esercitazione fornisce passaggi per creare una connessione sorgente nell’interfaccia utente per la raccolta dei dati del profilo Attributi del cliente in Adobe Experience Platform. Per ulteriori informazioni sugli attributi del cliente, consulta la [Panoramica sugli attributi del cliente](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

>[!IMPORTANT]
>
>Le funzionalità di disattivazione, abilitazione ed eliminazione dei flussi di dati non sono attualmente supportate per l&#39;origine Attributi del cliente.

## Creazione di una connessione sorgente

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sources]** dal menu di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Sources]. Nella schermata [!UICONTROL Catalog] sono visualizzate diverse sorgenti con cui è possibile creare una connessione.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la categoria [!UICONTROL Adobe applications], selezionare **[!UICONTROL Customer Attributes]**, quindi selezionare **[!UICONTROL Add data]**.

>[!NOTE]
>
>Se hai già stabilito una connessione di origine per i dati del profilo Attributi del cliente, l&#39;opzione per connettersi all&#39;origine è disabilitata.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

La schermata [!UICONTROL Add data] elenca tutte le origini dati disponibili per Attributi del cliente. Per creare una nuova connessione, selezionare un’origine dati dall’elenco, quindi selezionare **[!UICONTROL Next]**.

>[!NOTE]
>
>È possibile selezionare un solo set di dati per connessione sorgente Attributi cliente.

![](../../../../images/tutorials/create/customer-attributes/add-data.png)

Viene visualizzato il passaggio [!UICONTROL Dataflow detail] , che consente di assegnare un nome e una breve descrizione al nuovo flusso di dati.

Durante questo processo, puoi anche abilitare [!UICONTROL Partial ingestion] e [!UICONTROL Error diagnostics]. [!UICONTROL Partial ingestion] consente di acquisire dati contenenti errori, fino a una determinata soglia che è possibile impostare,  [!UICONTROL Error diagnostics] fornendo al contempo dettagli su eventuali dati errati che vengono inseriti separatamente in batch. Per ulteriori informazioni, consulta la [panoramica sull’acquisizione parziale dei batch](../../../../../ingestion/batch-ingestion/partial.md).

![](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

Viene visualizzato il passaggio [!UICONTROL Review] , che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connection]**: Mostra il tipo di origine, il percorso pertinente del file di origine scelto e il numero di colonne all&#39;interno del file di origine.
* **[!UICONTROL Assign dataset & map fields]**: Mostra il set di dati in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Passaggi successivi

Una volta creata la connessione, vengono automaticamente creati uno schema di destinazione e un set di dati per contenere i dati in arrivo. Al termine dell’acquisizione iniziale, i dati del profilo degli attributi del cliente possono essere utilizzati dai servizi Platform a valle, ad esempio [!DNL Real-time Customer Profile] e [!DNL Segmentation Service]. Per ulteriori informazioni, consulta i seguenti documenti:

* [[!DNL Real-time Customer Profile] panoramica](../../../../../profile/home.md)
* [[!DNL Segmentation Service] panoramica](../../../../../segmentation/home.md)
