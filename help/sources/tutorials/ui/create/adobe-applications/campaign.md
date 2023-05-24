---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;connettori origini;campaign;campaign managed services
title: Creare una connessione sorgente Adobe Campaign Managed Cloud Services tramite l’interfaccia utente di Platform
description: Scopri come collegare Adobe Experience Platform a Adobe Campaign Managed Cloud Services utilizzando l’interfaccia utente di Platform.
exl-id: 067ed558-b239-4845-8c85-3bf9b1d4caed
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 6%

---

# Creare una connessione sorgente Adobe Campaign Managed Cloud Services tramite l’interfaccia utente di Platform

Questo tutorial illustra i passaggi necessari per creare una connessione di origine e trasferire i dati Adobe Campaign Managed Cloud Services in Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Sorgenti](../../../../home.md): Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [Sandbox](../../../../../sandboxes/home.md): Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Connettere Adobe Campaign Managed Cloud Services a Platform

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. È inoltre possibile utilizzare la barra di ricerca per limitare le origini visualizzate.

Sotto **[!UICONTROL applicazioni Adobe]** categoria, seleziona **[!UICONTROL Adobe Campaign Managed Cloud Services]** e quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini che visualizza la scheda Adobe Campaign Managed Cloud Services.](../../../../images/tutorials/create/campaign/catalog.png)

### Selezionare i dati {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Istanza dell’ambiente Adobe Campaign"
>abstract="Nome dell’ambiente Adobe Campaign che desideri utilizzare."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="Mappatura target"
>abstract="Le mappature target sono oggetti tecnici utilizzati da Campaign per consegnare i messaggi e contengono tutte le impostazioni tecniche necessarie per l’invio (indirizzi, numeri di telefono, indicatori di consenso, identificatori aggiuntivi e così via)."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="Nome dello schema"
>abstract="Nome dell’entità definita nel database di Adobe Campaign."
>text="Learn more in documentation"

Il [!UICONTROL Seleziona dati] viene visualizzato un passaggio che fornisce un’interfaccia per configurare [!UICONTROL istanza Adobe Campaign], [!UICONTROL Mappatura target], e [!UICONTROL Nome schema].

| Proprietà | Descrizione |
| --- | --- |
| istanza Adobe Campaign | Nome dell’istanza dell’ambiente Adobe Campaign in uso. |
| Mappatura target | Gli oggetti tecnici utilizzati da Campaign per consegnare i messaggi e contengono tutte le impostazioni tecniche necessarie per inviare le consegne. |
| Nome dello schema | Nome dell’entità schema che stai portando in Platform. Le opzioni includono registro di consegna e registro di tracciamento. |

![Un’interfaccia in cui puoi configurare l’istanza Adobe Campaign, la mappatura del target e il nome dello schema.](../../../../images/tutorials/create/campaign/select-data.png)

Dopo aver fornito i valori per l’istanza Campaign, la mappatura del target e il nome dello schema, lo schermo si aggiorna per visualizzare un’anteprima dello schema e un set di dati di esempio. Al termine, seleziona **[!UICONTROL Successivo]**.

![Un’anteprima della gerarchia dello schema e un esempio del set di dati](../../../../images/tutorials/create/campaign/preview.png)

### Usa un set di dati esistente

Il [!UICONTROL Dettagli del flusso di dati] consente di scegliere se utilizzare un set di dati esistente o configurarne uno nuovo per il flusso di dati.

Per utilizzare un set di dati esistente, seleziona **[!UICONTROL Set di dati esistente]**. Puoi recuperare un set di dati esistente utilizzando [!UICONTROL Ricerca avanzata] oppure scorrendo l’elenco dei set di dati esistenti nel menu a discesa.

Con un set di dati selezionato, fornisci un nome per il flusso di dati e una descrizione facoltativa.

![Interfaccia che visualizza l’opzione del set di dati esistente.](../../../../images/tutorials/create/campaign/existing-dataset.png)

### Utilizza un nuovo set di dati

Per utilizzare un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]** quindi fornisci un nome per il set di dati di output e una descrizione facoltativa. Quindi, seleziona uno schema a cui mappare utilizzando [!UICONTROL Ricerca avanzata] oppure scorrendo l’elenco degli schemi esistenti nel menu a discesa. Al termine, seleziona **[!UICONTROL Successivo]**.

![Un’interfaccia che visualizza la nuova opzione del set di dati.](../../../../images/tutorials/create/campaign/new-dataset.png)

### Abilita avvisi

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati. Seleziona un avviso dall’elenco per iscriverti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle origini tramite l’interfaccia utente](../../alerts.md).

Una volta completati i dettagli del flusso di dati, seleziona **[!UICONTROL Successivo]**.

![Una selezione di diversi tipi di avviso che è possibile abilitare per il flusso di dati.](../../../../images/tutorials/create/campaign/alerts.png)

### Mappare i campi dati su uno schema XDM

Il [!UICONTROL Mappatura] viene visualizzato un passaggio che fornisce un’interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia mapper e dei campi calcolati, vedi la [Guida dell’interfaccia utente per la preparazione dati](../../../../../data-prep/ui/mapping.md).

>[!IMPORTANT]
>
>Quando mappi i campi sorgente ai campi XDM di destinazione, assicurati di mappare il campo identità principale designato al relativo campo XDM di destinazione appropriato.

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Successivo]**.

![Una struttura di mappatura con quattro campi dati di origine mappati ai corrispondenti campi schema XDM.](../../../../images/tutorials/create/campaign/mapping.png)

### Verifica il flusso di dati

Il **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima di crearlo. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all’interno di tale file di origine.
* **[!UICONTROL Assegna set di dati e mappa campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui aderisce il set di dati.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un po’ di tempo per creare il flusso di dati.

![Una pagina di revisione che visualizza le informazioni sulla connessione e sul set di dati.](../../../../images/tutorials/create/campaign/review.png)

### Monitorare l’attività del set di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sui tassi di acquisizione e sui batch riusciti e non riusciti.

Per iniziare a visualizzare l’attività del set di dati, seleziona **[!UICONTROL Flussi dati]** nel catalogo delle origini.

![Pagina del catalogo delle origini con la scheda dell’intestazione dei flussi di dati selezionata.](../../../../images/tutorials/create/campaign/dataflows.png)

Quindi, seleziona il set di dati di destinazione dall’elenco dei flussi di dati visualizzati.

![Elenco dei flussi di dati esistenti con il set di dati di destinazione Registri di consegna di Adobe Campaign selezionato.](../../../../images/tutorials/create/campaign/target-dataset.png)

Viene visualizzata la pagina dell’attività del set di dati. Da qui puoi visualizzare informazioni sulle prestazioni del flusso di dati, tra cui il tasso di acquisizione, i batch riusciti e i batch non riusciti.

Questa pagina offre anche un’interfaccia per aggiornare la descrizione dei metadati del flusso di dati, abilitare l’acquisizione parziale e la diagnostica degli errori, nonché aggiungere nuovi dati al set di dati.

![Un’interfaccia con grafici che rappresentano il tasso di acquisizione di un set di dati selezionato.](../../../../images/tutorials/create/campaign/dataset-activity.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un flusso di dati per portare i dati dei registri di consegna e di tracciamento di Campaign v8 su Platform. I dati in arrivo possono ora essere utilizzati da servizi Platform a valle come [!DNL Real-Time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica di [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Panoramica di [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
