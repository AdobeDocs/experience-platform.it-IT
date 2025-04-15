---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;connettori origini;campaign;campaign managed services
title: Creare una connessione sorgente Adobe Campaign Managed Cloud Services tramite l’interfaccia utente di Experience Platform
description: Scopri come collegare Adobe Experience Platform a Adobe Campaign Managed Cloud Services utilizzando l’interfaccia utente di Experience Platform.
exl-id: 067ed558-b239-4845-8c85-3bf9b1d4caed
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 6%

---

# Creare una connessione sorgente Adobe Campaign Managed Cloud Services tramite l’interfaccia utente di Experience Platform

Questo tutorial illustra i passaggi necessari per creare una connessione di origine e trasferire i dati Adobe Campaign Managed Cloud Services in Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Editor di schemi esercitazione](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l&#39;interfaccia Editor Schema.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono un singolo Experience Platform istanza in ambienti virtuali separati per aiutare a sviluppare ed evolvere applicazioni di esperienza digitale.

## Connettere Adobe Campaign Cloud Services gestito a Experience Platform

Nella interfaccia Experience Platform, selezionare **[!UICONTROL Origini]** dall&#39;navigazione sinistra per accesso&#39;area [!UICONTROL di lavoro Sorgenti] . Nella [!UICONTROL schermata Catalogo] vengono visualizzate numerose origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. È inoltre possibile utilizzare la barra ricerca per restringere le sorgenti visualizzate.

Nella categoria **[!UICONTROL Applicazioni Adobe]**, selezionare **[!UICONTROL Adobe Campaign Managed Cloud Services]**, quindi **[!UICONTROL Aggiungi dati]**.

![Catalogo origini che visualizza la scheda Adobe Campaign Managed Cloud Services.](../../../../images/tutorials/create/campaign/catalog.png)

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

Viene visualizzato il passaggio [!UICONTROL Seleziona dati] che fornisce un&#39;interfaccia per configurare la [!UICONTROL istanza Adobe Campaign], la [!UICONTROL mappatura Target] e il [!UICONTROL nome schema].

| Proprietà | Descrizione |
| --- | --- |
| istanza Adobe Campaign | Nome dell’istanza dell’ambiente Adobe Campaign in uso. |
| Mappatura target | Gli oggetti tecnici utilizzati da Campaign per consegnare i messaggi e contengono tutte le impostazioni tecniche necessarie per inviare le consegne. |
| Nome dello schema | Nome dell&#39;entità dello schema che si sta portando all Experience Platform. Opzioni includono Registro di consegna e Registro di tracciamento. |

![Interfaccia in cui è possibile configurare il istanza Adobe Campaign, il mapping dei destinazione e il nome dello schema.](../../../../images/tutorials/create/campaign/select-data.png)

Dopo aver fornito i valori per il istanza Campaign, il mapping del destinazione e il nome dello schema, la schermata viene aggiornata per visualizzare un&#39;anteprima dello schema e un set di dati di esempio. Al termine, selezionare **[!UICONTROL Successivo]**.

![Anteprima della gerarchia dello schema e campione del set di dati](../../../../images/tutorials/create/campaign/preview.png)

### Usa un set di dati esistente

La pagina [!UICONTROL Dettagli flusso di dati] consente di scegliere se utilizzare un set di dati esistente o configurarne uno nuovo per il flusso di dati.

Per utilizzare un set di dati esistente, selezionare **[!UICONTROL Set di dati esistente]**. Puoi recuperare un set di dati esistente utilizzando l&#39;opzione [!UICONTROL Ricerca avanzata] oppure scorrendo l&#39;elenco dei set di dati esistenti nel menu a discesa.

Con un set di dati selezionato, fornisci un nome per il flusso di dati e una descrizione facoltativa.

![Interfaccia per visualizzare l&#39;opzione del set di dati esistente.](../../../../images/tutorials/create/campaign/existing-dataset.png)

### Utilizza un nuovo set di dati

Per utilizzare un nuovo set di dati, selezionare **[!UICONTROL Nuovo set di dati]**, quindi specificare un nome per il set di dati di output e una descrizione facoltativa. Quindi, seleziona uno schema a cui mappare utilizzando l&#39;opzione [!UICONTROL Ricerca avanzata] o scorrendo l&#39;elenco degli schemi esistenti nel menu a discesa. Al termine, selezionare **[!UICONTROL Avanti]**.

![Interfaccia che visualizza la nuova opzione del set di dati.](../../../../images/tutorials/create/campaign/new-dataset.png)

### Abilita avvisi

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati. Seleziona un avviso dall&#39;elenco per iscriverti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, vedere la guida alla [sottoscrizione agli avvisi origini utilizzando il interfaccia](../../alerts.md).

Quando hai finito di fornire dettagli al flusso di dati, seleziona **[!UICONTROL Successivo]**.

![Una selezione di diversi tipi di avvisi che puoi abilitare per il flusso di dati.](../../../../images/tutorials/create/campaign/alerts.png)

### Mappatura dei campi dati a uno schema XDM

Viene visualizzato il [!UICONTROL passaggio Mapping] , che fornisce un&#39;interfaccia per mappare i campi di origine dallo schema di origine ai destinazione campi XDM appropriati nello schema destinazione.

Experience Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull&#39;utilizzo dell&#39;interfaccia mapper e dei campi calcolati, consulta la [guida dell&#39;interfaccia utente della preparazione dati](../../../../../data-prep/ui/mapping.md).

>[!IMPORTANT]
>
>Quando mappi i campi sorgente ai campi XDM di destinazione, assicurati di mappare il campo identità principale designato al relativo campo XDM di destinazione appropriato.
>
>Per ogni pubblico, puoi aggiungere fino a 20 campi da mappare su Adobe Campaign. È possibile modificare questo limite aggiornando il valore dell&#39;opzione `NmsCdp_Aep_Sources_Max_Columns` nella cartella Amministrazione > Piattaforma > Opzioni di Esplora campagne.

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Avanti]**.

![Struttura di mapping con quattro campi dati di origine mappati ai campi schema XDM corrispondenti.](../../../../images/tutorials/create/campaign/mapping.png)

### Verifica il flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Rivedi]**, che consente di rivedere il nuovo flusso di dati prima che venga creato. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno di tale file di origine.
* **[!UICONTROL Assegna set di dati e mappa i campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e attendi che venga creato un po&#39; di tempo.

![Pagina di revisione contenente informazioni sulla connessione e sul set di dati.](../../../../images/tutorials/create/campaign/review.png)

### Monitorare l’attività del set di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sui tassi di acquisizione e sui batch riusciti e non riusciti.

Per iniziare a visualizzare l&#39;attività del set di dati, seleziona **[!UICONTROL Flussi di dati]** nel catalogo delle origini.

![La pagina del catalogo origini con l&#39;intestazione dei flussi di dati scheda selezionata.](../../../../images/tutorials/create/campaign/dataflows.png)

Successivo, seleziona il set di dati destinazione dall&#39;elenco dei flussi di dati visualizzati.

![Elenco di flussi di dati esistenti con i Adobe Campaign i log di recapito destinazione il set di dati selezionato.](../../../../images/tutorials/create/campaign/target-dataset.png)

Viene visualizzata la pagina dell&#39;attività del set di dati. Da qui, è possibile visualizzare informazioni sulle prestazioni del flusso di dati, tra cui velocità di assimilazione, batch riusciti e batch non riusciti.

Questa pagina offre anche un’interfaccia per aggiornare la descrizione dei metadati del flusso di dati, abilitare l’acquisizione parziale e la diagnostica degli errori, nonché aggiungere nuovi dati al set di dati.

![Interfaccia con grafici che rappresentano il tasso di acquisizione di un set di dati selezionato.](../../../../images/tutorials/create/campaign/dataset-activity.png)


>[!IMPORTANT]
>
>Non è possibile eseguire la retrocompilazione dei registri eventi precedenti con l’origine Adobe Campaign Managed Cloud Services. Se è richiesta la retrocompilazione, utilizza un flusso di lavoro personalizzato o un’implementazione personalizzata per esportare i dati in Amazon S3 o Azure Blob, o da Amazon S3 o Azure Blob a un set di dati Adobe Experience Platform.


## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un flusso di dati per portare i dati dei registri di consegna e di tracciamento di Campaign v8 in Experience Platform. I dati in entrata possono ora essere utilizzati dai servizi di Experience Platform downstream come [!DNL Real-Time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica di [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Panoramica di [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
