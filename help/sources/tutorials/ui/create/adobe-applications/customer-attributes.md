---
keywords: Experience Platform;home;argomenti popolari;attributi del cliente
solution: Experience Platform
title: Creare una connessione sorgente attributi cliente nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente nell’interfaccia utente per inserire in Adobe Experience Platform i dati del profilo degli attributi del cliente.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 4%

---

# Creare una connessione sorgente Attributi del cliente nell&#39;interfaccia utente

Questa esercitazione fornisce passaggi per creare una connessione sorgente nell’interfaccia utente per inserire i dati del profilo Attributi del cliente in Adobe Experience Platform. Per ulteriori informazioni sugli attributi del cliente, consulta la sezione [Panoramica degli attributi del cliente](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=it).

>[!IMPORTANT]
>
>L&#39;origine Attributi del cliente al momento non supporta l&#39;abilitazione o la disattivazione dei flussi di dati.

## Creazione di una connessione sorgente

>[!NOTE]
>
>Se hai già stabilito una connessione di origine per i dati del profilo Attributi del cliente, l&#39;opzione per connettersi all&#39;origine è disabilitata.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in viene visualizzata una varietà di sorgenti con cui è possibile creare una connessione.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la [!UICONTROL Applicazioni di Adobe] categoria, seleziona **[!UICONTROL Attributi del cliente]** quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/customer-attributes/catalog.png)

### Seleziona origine dati attributi cliente

La [!UICONTROL Aggiungi dati] in questa schermata sono elencate tutte le origini dati disponibili per Attributi del cliente. È possibile selezionare un solo set di dati per connessione sorgente Attributi cliente.

>[!NOTE]
>
>I gruppi di campi, gli schemi e i set di dati vengono creati out-of-box come parte del provisioning del flusso. Rimarranno invariati e dovrai eliminarli manualmente, se necessario.

L&#39;evoluzione dello schema non è supportata dall&#39;origine degli attributi del cliente. Se l’input dello schema di un’origine dati attributi del cliente viene modificato, diventa incompatibile con Platform. Come soluzione alternativa, è possibile eliminare un flusso di dati degli attributi del cliente esistente, insieme al relativo set di dati, schema e gruppo di campi associati, quindi crearne uno nuovo con lo schema e l’origine dati aggiornati.

>[!IMPORTANT]
>
>Anche se puoi eliminare un flusso di dati degli attributi del cliente, il relativo set di dati rimane anche dopo l’eliminazione del flusso di dati. Consulta la guida su [eliminazione di un set di dati](../../../../../catalog/datasets/user-guide.md) per i passaggi su come eliminare manualmente un set di dati.

Per creare una nuova connessione, selezionare un’origine dati dall’elenco, quindi selezionare **[!UICONTROL Successivo]**.

![add-data](../../../../images/tutorials/create/customer-attributes/add-data.png)

### Fornire i dettagli del flusso di dati

La [!UICONTROL Dettaglio flusso di dati] viene visualizzato un passaggio che ti consente di fornire un nome e una breve descrizione per il flusso di dati. Durante questo processo, puoi anche configurare le impostazioni per [!UICONTROL Diagnostica degli errori], [!UICONTROL Acquisizione parziale]e [!UICONTROL Avvisi].

[!UICONTROL Diagnostica degli errori] consente la generazione dettagliata dei messaggi di errore per tutti i record errati che si verificano nel flusso di dati, mentre [!UICONTROL Acquisizione parziale] consente di acquisire dati contenenti errori, fino a una determinata soglia definita manualmente. Consulta la sezione [panoramica dell’acquisizione parziale in batch](../../../../../ingestion/batch-ingestion/partial.md) per ulteriori informazioni.

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sorgente tramite l’interfaccia utente](../../alerts.md).

Al termine della fornitura dei dettagli al flusso di dati, seleziona **[!UICONTROL Successivo]**.

![dettaglio del flusso di dati](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### Controlla il flusso di dati

La [!UICONTROL Revisione] viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: Mostra il tipo di origine, il percorso pertinente del file di origine scelto e il numero di colonne all&#39;interno del file di origine.
* **[!UICONTROL Assegna set di dati e campi mappa]**: Mostra il set di dati in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.

![revisione](../../../../images/tutorials/create/customer-attributes/review.png)

## Passaggi successivi

Una volta creata la connessione, vengono automaticamente creati uno schema di destinazione e un set di dati per contenere i dati in arrivo. Al termine dell’acquisizione iniziale, i dati del profilo degli attributi del cliente possono essere utilizzati dai servizi della piattaforma a valle, come [!DNL Real-Time Customer Profile] e [!DNL Segmentation Service]. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica di [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Panoramica di [!DNL Segmentation Service]](../../../../../segmentation/home.md)
