---
keywords: Experience Platform;home;argomenti popolari;attributi del cliente
solution: Experience Platform
title: Creare una connessione Source per gli attributi del cliente nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente nell’interfaccia utente per inserire i dati del profilo degli attributi del cliente in Adobe Experience Platform.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# Creare una connessione sorgente Attributi del cliente nell’interfaccia utente

Questo tutorial descrive i passaggi necessari per creare una connessione sorgente nell’interfaccia utente per inserire i dati del profilo Attributi del cliente in Adobe Experience Platform. Per ulteriori informazioni su Attributi del cliente, consulta la [Panoramica sugli attributi del cliente](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=it).

>[!IMPORTANT]
>
>L’origine Attributi del cliente al momento non supporta l’abilitazione o la disabilitazione dei flussi di dati.

## Creare una connessione sorgente

>[!NOTE]
>
>Se hai già stabilito una connessione di origine per i dati del profilo Attributi del cliente, l’opzione per connettersi con l’origine è disabilitata.

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare una connessione.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Nella categoria [!UICONTROL Applicazioni di Adobe], selezionare **[!UICONTROL Attributi del cliente]**, quindi **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/customer-attributes/catalog.png)

### Seleziona origine dati attributi cliente

Nella schermata [!UICONTROL Aggiungi dati] sono elencate tutte le origini dati disponibili per Attributi del cliente. È possibile selezionare un solo set di dati per connessione di origine Attributi del cliente.

>[!NOTE]
>
>I gruppi di campi, gli schemi e i set di dati vengono creati come parte del provisioning del flusso. Rimarranno invariate e dovrai eliminarle manualmente, se necessario.

L’evoluzione dello schema non è supportata dall’origine degli attributi del cliente. Se l’input dello schema di un’origine dati degli attributi del cliente viene modificato, diventa incompatibile con Platform. Come soluzione alternativa, puoi eliminare un flusso di dati attributi del cliente esistente, insieme al set di dati, allo schema e al gruppo di campi associati, quindi crearne uno nuovo con lo schema e l’origine dati aggiornati.

>[!IMPORTANT]
>
>Anche se puoi eliminare un flusso di dati di attributi cliente, il relativo set di dati corrispondente rimane invariato anche dopo l’eliminazione del flusso di dati. Consulta la guida sull&#39;[eliminazione di un set di dati](../../../../../catalog/datasets/user-guide.md) per i passaggi su come eliminare manualmente un set di dati.

Per creare una nuova connessione, selezionare un&#39;origine dati dall&#39;elenco, quindi selezionare **[!UICONTROL Avanti]**.

![add-data](../../../../images/tutorials/create/customer-attributes/add-data.png)

### Fornisci i dettagli del flusso di dati

Viene visualizzato il passaggio [!UICONTROL Dettagli flusso di dati], che consente di fornire un nome e una breve descrizione per il flusso di dati. Durante questo processo, puoi anche configurare le impostazioni per [!UICONTROL Diagnostica errori], [!UICONTROL Acquisizione parziale] e [!UICONTROL Avvisi].

[!UICONTROL Diagnostica errori] consente la generazione di messaggi di errore dettagliati per eventuali record errati che si verificano nel flusso di dati, mentre [!UICONTROL L&#39;acquisizione parziale] consente di acquisire dati contenenti errori, fino a una determinata soglia definita manualmente. Per ulteriori informazioni, consulta la [panoramica sull&#39;acquisizione batch parziale](../../../../../ingestion/batch-ingestion/partial.md).

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi di origini tramite l&#39;interfaccia utente](../../alerts.md).

Dopo aver fornito i dettagli al flusso di dati, seleziona **[!UICONTROL Avanti]**.

![dettagli flusso di dati](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### Verifica flusso di dati

Viene visualizzato il passaggio [!UICONTROL Rivedi], che consente di rivedere il nuovo flusso di dati prima che venga creato. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e il numero di colonne all&#39;interno di tale file di origine.
* **[!UICONTROL Assegna set di dati e mappa i campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.

![revisione](../../../../images/tutorials/create/customer-attributes/review.png)

## Passaggi successivi

Una volta creata la connessione, vengono automaticamente creati uno schema di destinazione e un set di dati per contenere i dati in arrivo. Al termine dell&#39;acquisizione iniziale, i dati del profilo degli attributi del cliente possono essere utilizzati dai servizi Platform a valle come [!DNL Real-Time Customer Profile] e [!DNL Segmentation Service]. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica di [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Panoramica di [!DNL Segmentation Service]](../../../../../segmentation/home.md)
