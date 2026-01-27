---
title: Collegare Oracle Eloqua (V2) ad Experience Platform nell’interfaccia utente
description: Scopri come collegare il tuo account Oracle Eloqua ad Experience Platform nell’interfaccia utente.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 1%

---

# Connettere [!DNL Oracle Eloqua] (V2) ad Experience Platform nell&#39;interfaccia utente

Il connettore di origine [!DNL Oracle Eloqua (V2)] ti consente di collegare l&#39;account Oracle Eloqua con Adobe Experience Platform, consentendo l&#39;acquisizione automatizzata e scalabile dei dati di marketing B2B chiave, inclusi contatti, account, campagne e attività di coinvolgimento.

Utilizza questo connettore di origine per configurare l’autenticazione sicura, selezionare esattamente le entità dati Eloqua necessarie e mapparle sugli schemi standard Experience Data Model (XDM). Opzioni di pianificazione flessibili ti consentono di impostare sia caricamenti di dati iniziali che sincronizzazioni ricorrenti e incrementali, garantendo che i dati di marketing rimangano correnti e utilizzabili.

Basato sul framework di acquisizione aziendale di Adobe, il connettore di origine [!DNL Oracle Eloqua (V2)] fornisce una base affidabile ed estensibile per l&#39;ottimizzazione delle campagne, la misurazione delle prestazioni e la personalizzazione cross-channel.

Leggere questa guida per scoprire come collegare l&#39;account [!DNL Oracle Eloqua] a Adobe Experience Platform utilizzando l&#39;area di lavoro origini nell&#39;interfaccia utente di Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Raccogli le credenziali richieste {#credentials}

Per informazioni sull&#39;autenticazione, leggere la [[!DNL Eloqua] panoramica](../../../../connectors/marketing-automation/eloqua.md).

## Navigare nel catalogo delle origini {#catalog}

Nell&#39;interfaccia utente di Experience Platform, selezionare **[!UICONTROL Sources]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro *[!UICONTROL Sources]*. Scegliere una categoria o utilizzare la barra di ricerca per trovare l&#39;origine.

Per connettersi a [!DNL Eloqua], passare alla categoria *[!UICONTROL Marketing Automation]*, selezionare la scheda di origine **[!UICONTROL (V2) Oracle Eloqua]**, quindi selezionare **[!UICONTROL Set up]**.

>[!TIP]
>
>Le origini nel catalogo origini visualizzano l&#39;opzione **[!UICONTROL Set up]** quando una determinata origine non dispone ancora di un account autenticato. Una volta creato un account autenticato, questa opzione diventa **[!UICONTROL Add data]**.

![Scheda Eloqua nel catalogo delle origini con il pulsante Configura evidenziato.](../../../../images/tutorials/create/eloqua/catalog.png)

## Usa un account esistente {#existing}

Per utilizzare un account esistente, selezionare **[!UICONTROL Existing account]**, quindi selezionare l&#39;account [!DNL Eloqua] che si desidera utilizzare.

![Opzione account esistente selezionata nell&#39;interfaccia di creazione account.](../../../../images/tutorials/create/eloqua/existing.png)

## Crea un nuovo account {#new}

Per creare un nuovo account, seleziona **[!UICONTROL New account]** e fornisci un nome e una descrizione sotto [!UICONTROL Source connection details]. Quindi, in [!UICONTROL Account authentication], fornisci i valori per **ID client**, **Segreto client**, **Nome utente**, **Password** e **Endpoint base**. Per ulteriori informazioni su queste credenziali, leggere la [guida all&#39;autenticazione](../../../../connectors/marketing-automation/eloqua.md). Al termine, selezionare **[!UICONTROL Connect to source]** e attendere alcuni secondi prima di stabilire la connessione.

![Nuova interfaccia account con campi per i dettagli della connessione di origine e le credenziali di autenticazione.](../../../../images/tutorials/create/eloqua/new.png)

## Selezionare i dati

Utilizzare l&#39;interfaccia di selezione dei dati per selezionare l&#39;entità [!DNL Eloqua] che si desidera acquisire in Experience Platform.

>[!TIP]
>
>Quando selezioni i dati, noterai che, ad eccezione delle campagne, le altre entità visualizzano dati di esempio rappresentativi. Questo approccio consente di visualizzare in anteprima i campi e la struttura disponibili, in quanto [!DNL Eloqua] API pubbliche attualmente recuperano dati reali solo per le campagne. Per le altre entità, vengono forniti dati di esempio per supportare il flusso di lavoro di configurazione.

![Interfaccia di selezione dei dati che mostra le entità dati Eloqua disponibili.](../../../../images/tutorials/create/eloqua/select-data.png)

## Dettagli del set di dati e del flusso di dati {#details}

Successivamente, devi fornire informazioni sul set di dati e sul flusso di dati. Durante questo passaggio, puoi utilizzare un set di dati esistente o crearne uno nuovo. Inoltre, puoi facoltativamente abilitare il set di dati per l’acquisizione in Real-Time Customer Profile durante questo passaggio.

![Interfaccia dei dettagli del set di dati e del flusso di dati con opzioni per la configurazione delle proprietà del set di dati.](../../../../images/tutorials/create/eloqua/details.png)

## Mappatura {#mapping}

I mapping per [!DNL Eloqua] sono organizzati in quattro tipi di entità principali:

* **Account** - Record società/organizzazione da [!DNL Eloqua].
* **Attività** - Attività di marketing ed eventi di coinvolgimento da [!DNL Eloqua].
* **Campagne** - Record campagna di marketing da [!DNL Eloqua].
* **Contatti** - Record di singole persone da [!DNL Eloqua].

Se hai bisogno di accedere a campi aggiuntivi oltre a quelli forniti per impostazione predefinita, puoi aggiungere questi campi utilizzando il processo di mappatura della preparazione dati in Experience Platform. Se lo schema predefinito (standard) non supporta alcuni dei campi obbligatori, puoi definire uno schema personalizzato in Experience Platform. Utilizzare questa funzione per creare e mappare i campi necessari in modo da acquisire in modo semplice tutti i dati rilevanti da [!DNL Eloqua] in Experience Platform.

Riepilogo delle fasi successive:

* Esamina i campi mappati predefiniti disponibili con l’integrazione.
* Durante il passaggio di mappatura, includi eventuali campi aggiuntivi necessari da [!DNL Eloqua].
* Se nello schema standard non sono presenti nuovi campi, estendere o creare uno schema personalizzato in Experience Platform che includa questi campi.
* Completa la mappatura per garantire l’acquisizione di tutti i dati desiderati.

Per garantire che le informazioni CRM esterne vengano riflesse accuratamente, è sufficiente utilizzare la funzione del campo calcolato nella preparazione dati per aggiornare il segnaposto `{CRM_INSTANCE_ID}` con l&#39;ID istanza CRM specifico nel campo dei dati di origine. Questo offre la flessibilità di personalizzare l’integrazione in base alla configurazione specifica della tua organizzazione.

Per utilizzare l’editor dei campi calcolati, seleziona il campo di origine da aggiornare.

![Campo di origine Eloqua con campi calcolati.](../../../../images/tutorials/create/eloqua/select-calculated-field.png)

>[!BEGINTABS]

>[!TAB Salesforce]

Per [!DNL Salesforce] utenti, utilizzare l&#39;editor dei campi calcolati e aggiornare `{CRM_INSTANCE_ID}` con l&#39;ID istanza appropriato.

![Campo calcolato per Salesforce.](../../../../images/tutorials/create/eloqua/sf-field.png)

>[!TAB Microsoft Dynamics]

Per [!DNL Microsoft] utenti, utilizzare l&#39;editor dei campi calcolati e aggiornare `{CRM_INSTANCE_ID}` con l&#39;ID istanza appropriato.

![Campo calcolato per Dynamics.](../../../../images/tutorials/create/eloqua/dynamics-field.png)

>[!ENDTABS]

Dopo aver completato l&#39;aggiornamento dei campi calcolati, selezionare **[!UICONTROL Next]** per continuare.

![Interfaccia di mappatura che mostra le mappature dei campi per le entità dati Eloqua.](../../../../images/tutorials/create/eloqua/mapping.png)

## Pianificazione

>[!NOTE]
>
>Di seguito sono riportati i campi delta utilizzati internamente per il caricamento di dati incrementali:
>
>* **Contatti:** `C_DateModified`
>* **Account:** `M_DateModified`
>* **Attività:** `CreatedAt`
>* **Oggetti personalizzati:** `UpdatedAt`
>* **Campagna:** `updatedAt`

Al termine della mappatura, puoi configurare una pianificazione di acquisizione per il flusso di dati. Imposta [!UICONTROL Frequency] su `Once` per configurare un&#39;acquisizione unica. Per l&#39;acquisizione incrementale, puoi impostare [!UICONTROL Frequency] su `Hour`, `Day` o `Week`. Quando utilizzi l&#39;acquisizione incrementale, devi anche configurare [!UICONTROL Interval] per definire il periodo di tempo che intercorre tra le esecuzioni dell&#39;acquisizione. Ad esempio, se la frequenza di acquisizione è impostata su `Day` e l&#39;intervallo è impostato su `15`, il flusso di dati verrà pianificato in modo da acquisire i dati ogni 15 giorni.

La frequenza di acquisizione al minuto non è disponibile per l&#39;origine [!DNL Eloqua]. La pianificazione più frequente che puoi scegliere è oraria. Seleziona una pianificazione che corrisponda alle tue esigenze di aggiornamento dei dati. La scelta di una pianificazione più frequente comporterà un aumento dei costi di elaborazione.

![Interfaccia di pianificazione con opzioni per configurare la frequenza e l&#39;intervallo di acquisizione.](../../../../images/tutorials/create/eloqua/scheduling.png)

## Rivedi

Con la pianificazione dell&#39;acquisizione configurata, utilizza l&#39;interfaccia [!UICONTROL Review] per confermare i dettagli del flusso di dati. Seleziona **[!UICONTROL Finish]** per completare la configurazione e attendi alcuni istanti per l&#39;avvio del flusso di dati.

![L&#39;interfaccia di revisione visualizza un riepilogo della configurazione del flusso di dati prima del completamento.](../../../../images/tutorials/create/eloqua/review.png)

## Monitoraggio

Una volta selezionato, il flusso di dati eseguirà una retrocompilazione una tantum dei dati e la successiva sincronizzazione incrementale secondo la pianificazione specificata. Lo stato della sincronizzazione può essere monitorato passando al flusso di dati. Per ulteriori informazioni, leggere la guida sui [flussi di dati delle origini di monitoraggio nell&#39;interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

## Passaggi successivi

Hai completato l&#39;installazione e la configurazione dell&#39;origine [!DNL Eloqua] in Experience Platform. Una volta stabilito il flusso di dati, i dati di [!DNL Eloqua] verranno acquisiti in base alla pianificazione scelta e mappati agli schemi standard Experience Data Model (XDM). Continua a monitorare i flussi di dati ed esplora i dati acquisiti in Platform per ottenere informazioni approfondite e attivare casi di utilizzo di marketing. Per configurazioni più avanzate e la risoluzione dei problemi, consulta la relativa documentazione o rivolgiti alle risorse di supporto di Adobe.

Per ulteriori informazioni, consulta la seguente documentazione:

* [Panoramica sulle origini](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)
