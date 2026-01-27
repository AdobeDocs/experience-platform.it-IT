---
title: Collegare l’account Salesforce Marketing Cloud (V2) ad Experience Platform tramite l’interfaccia utente
description: Scopri come collegare il tuo account Salesforce Marketing Cloud (V2) ad Experience Platform tramite l’interfaccia utente.
source-git-commit: 91bf8bf6e6f7030574d693484ce9797800c2d5dd
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 1%

---

# Connetti [!DNL Salesforce Marketing Cloud] ad Experience Platform

Leggere questa guida per scoprire come collegare l&#39;account [!DNL Salesforce Marketing Cloud] a Adobe Experience Platform utilizzando l&#39;area di lavoro origini nell&#39;interfaccia utente di Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL Salesforce Marketing Cloud] panoramica](../../../../connectors/marketing-automation/sfmc.md#prerequisites).

## Navigare nel catalogo delle origini

Nell&#39;interfaccia utente di Experience Platform, selezionare **[!UICONTROL Sources]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro *[!UICONTROL Sources]*. Scegliere una categoria o utilizzare la barra di ricerca per trovare l&#39;origine.

Per connettersi a [!DNL Salesforce Marketing Cloud], passare alla categoria *[!UICONTROL Marketing Automation]*, selezionare la scheda di origine **[!UICONTROL (V2) Salesforce Marketing Cloud]**, quindi selezionare **[!UICONTROL Set up]**.

>[!TIP]
>
>Le origini nel catalogo origini visualizzano l&#39;opzione **[!UICONTROL Set up]** quando una determinata origine non dispone ancora di un account autenticato. Una volta creato un account autenticato, questa opzione diventa **[!UICONTROL Add data]**.

![Catalogo delle origini con l&#39;origine Marketing Cloud di Salesforce selezionata.](../../../../images/tutorials/create/sfmc/catalog.png)

## Usa un account esistente {#existing}

Per utilizzare un account esistente, selezionare **[!UICONTROL Existing account]**, quindi selezionare l&#39;account [!DNL Salesforce Marketing Cloud] che si desidera utilizzare.

![Interfaccia account esistente del flusso di lavoro origini](../../../../images/tutorials/create/sfmc/existing.png)

## Crea un nuovo account {#new}

Per creare un nuovo account, seleziona **[!UICONTROL New account]** e fornisci un nome e una descrizione sotto [!UICONTROL Source connection details]. Quindi, in [!UICONTROL Account authentication], fornisci i valori per **ID client**, **Segreto client** e **Endpoint base**. Per ulteriori informazioni su queste credenziali, leggere la [guida all&#39;autenticazione](../../../../connectors/marketing-automation/sfmc.md#gather-required-credentials). Al termine, selezionare **[!UICONTROL Connect to source]** e attendere alcuni secondi prima di stabilire la connessione.

![Nuova interfaccia account del flusso di lavoro di origine.](../../../../images/tutorials/create/sfmc/new.png)

## Selezionare i dati

L&#39;origine [!DNL Salesforce Marketing Cloud] supporta l&#39;acquisizione dei dati solo da [!DNL Salesforce Marketing Cloud] estensioni dati.

Utilizza l&#39;interfaccia [!UICONTROL Select data] per selezionare l&#39;estensione di dati che desideri acquisire dall&#39;istanza di [!DNL Salesforce Marketing Cloud]. Dopo aver selezionato l’estensione dati, puoi utilizzare il pannello Anteprima per confermare che il set di dati contenga i campi previsti prima di procedere.

![Il passaggio di dati di selezione del flusso di lavoro origini](../../../../images/tutorials/create/sfmc/select-data.png)

## Dettagli del set di dati e del flusso di dati

Successivamente, devi fornire informazioni sul set di dati e sul flusso di dati. Durante questo passaggio, puoi utilizzare un set di dati esistente o crearne uno nuovo. Inoltre, puoi facoltativamente abilitare il set di dati per l’acquisizione in Real-Time Customer Profile durante questo passaggio.

![Il set di dati e il passaggio dei dettagli del flusso di dati del flusso di lavoro delle origini.](../../../../images/tutorials/create/sfmc/dataset-details.png)

## Mappatura

In [!DNL Salesforce Marketing Cloud], le estensioni dati non sono considerate oggetti standard. Pertanto, non esistono campi di mappatura predefiniti o fissi per uno schema Experience Platform. Mentre la preparazione dati in Experience Platform esegue un allineamento ottimale tra i campi sorgente da [!DNL Salesforce Marketing Cloud] e lo schema XDM (Experience Data Model) di destinazione, ci possono essere ancora alcuni casi in cui è necessaria una revisione o un adeguamento manuale per risolvere campi non mappati o errati.

![Passaggio di mappatura del flusso di lavoro di origine.](../../../../images/tutorials/create/sfmc/mapping.png)

## Pianificare un flusso di dati

Al termine della mappatura, puoi configurare una pianificazione di acquisizione per il flusso di dati. Imposta [!UICONTROL Frequency] su `Once` per configurare un&#39;acquisizione unica. Per l&#39;acquisizione incrementale, puoi impostare [!UICONTROL Frequency] su `Hour`, `Day` o `Week`. Quando utilizzi l&#39;acquisizione incrementale, devi anche configurare [!UICONTROL Interval] per definire il periodo di tempo che intercorre tra le esecuzioni dell&#39;acquisizione. Ad esempio, se la frequenza di acquisizione è impostata su `Day` e l&#39;intervallo è impostato su `15`, il flusso di dati verrà pianificato in modo da acquisire i dati ogni 15 giorni.

>[!TIP]
>
> La frequenza di acquisizione al minuto non è disponibile per l&#39;origine [!DNL Salesforce Marketing Cloud]. La pianificazione più frequente che puoi scegliere è oraria. Seleziona una pianificazione che corrisponda alle tue esigenze di aggiornamento dei dati. La scelta di una pianificazione più frequente comporterà un aumento dei costi di elaborazione.

Per abilitare la sincronizzazione incrementale, devi selezionare un campo delta (data/ora) nel set di dati. Se il set di dati non contiene un campo delta appropriato, non potrai creare il flusso di dati.

![Passaggio di pianificazione del flusso di lavoro di origine.](../../../../images/tutorials/create/sfmc/schedule.png)

## Rivedi

Con la pianificazione dell&#39;acquisizione configurata, utilizza l&#39;interfaccia [!UICONTROL Review] per confermare i dettagli del flusso di dati. Seleziona **[!UICONTROL Finish]** per completare la configurazione e attendi alcuni istanti per l&#39;avvio del flusso di dati.

![Passaggio di revisione del flusso di lavoro origini.](../../../../images/tutorials/create/sfmc/review.png)

## Monitoraggio

Una volta selezionato, il flusso di dati eseguirà una retrocompilazione una tantum dei dati e la successiva sincronizzazione incrementale secondo la pianificazione specificata. Lo stato della sincronizzazione può essere monitorato passando al flusso di dati. Per ulteriori informazioni, leggere la guida sui [flussi di dati delle origini di monitoraggio nell&#39;interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

## Passaggi successivi

Questa esercitazione ti ha guidato attraverso la connessione dell&#39;account [!DNL Salesforce Marketing Cloud] (V2) ad Experience Platform tramite l&#39;interfaccia utente. Hai imparato a selezionare o creare un account di origine, fornire le credenziali richieste, scegliere le estensioni di dati da acquisire, specificare i dettagli del set di dati e del flusso di dati, mappare i dati, impostare una pianificazione per l’acquisizione dei dati e monitorare i flussi di dati. Seguendo questi passaggi, hai integrato correttamente i tuoi dati di [!DNL Salesforce Marketing Cloud] con Experience Platform per l&#39;attivazione e l&#39;analisi.

Per ulteriori informazioni, consulta la seguente documentazione:

* [Panoramica sulle origini](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)

