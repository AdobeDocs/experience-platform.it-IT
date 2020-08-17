---
keywords: Experience Platform;home;popular topics;enable dataset;Dataset;dataset
solution: Experience Platform
title: Guida utente dei set di dati
topic: datasets
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---


# Guida utente dei set di dati

Questa guida utente fornisce istruzioni sull&#39;esecuzione delle azioni comuni quando si utilizzano i set di dati nell&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida utente richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Set](overview.md)di dati: Il concetto di storage e gestione per la persistenza dei dati in [!DNL Experience Platform].
* [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Editor](../../xdm/tutorials/create-schema-ui.md)schema: Scoprite come creare schemi XDM personalizzati utilizzando l&#39; [!DNL Schema Editor] interfaccia [!DNL Platform] utente.
* [!DNL Real-time Customer Profile](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [!DNL Data Governance](../../data-governance/home.md): Assicurati la conformità a normative, restrizioni e criteri relativi all&#39;utilizzo dei dati dei clienti.

## Visualizzare i set di dati

Nell’ [!DNL Experience Platform] interfaccia utente, fate clic **[!UICONTROL Datasets]** nella barra di navigazione a sinistra per aprire il *[!UICONTROL Datasets]* dashboard. Il dashboard elenca tutti i set di dati disponibili per l&#39;organizzazione. I dettagli vengono visualizzati per ciascun dataset elencato, incluso il nome, lo schema a cui il dataset aderisce e lo stato dell&#39;assimilazione più recente.

![](../images/datasets/user-guide/browse_datasets.png)

Fare clic sul nome di un dataset per accedere alla *[!UICONTROL Dataset activity]* schermata e visualizzare i dettagli del set di dati selezionato. La scheda dell&#39;attività include un grafico che visualizza il tasso di utilizzo dei messaggi e un elenco di batch con esito positivo o negativo.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Anteprima di un dataset

Dalla *[!UICONTROL Dataset activity]* schermata, fai clic **[!UICONTROL Preview dataset]** vicino all&#39;angolo superiore destro dello schermo per visualizzare in anteprima fino a 100 righe di dati. Se il set di dati è vuoto, il collegamento di anteprima verrà disattivato e verrà detto **[!UICONTROL Preview not available]**.

![](../images/datasets/user-guide/click_to_preview.png)

Nella finestra di anteprima, la visualizzazione gerarchica dello schema per il dataset viene visualizzata a destra.

![](../images/datasets/user-guide/preview_dataset.png)

Per metodi più affidabili per accedere ai dati, [!DNL Experience Platform] fornisce servizi a valle come [!DNL Query Service] e [!DNL JupyterLab] per esplorare e analizzare i dati. Per ulteriori informazioni, consulta i documenti seguenti:

* [Panoramica di Servizio query](../../query-service/home.md)
* [Guida utente di JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Creare un dataset {#create}

Per creare un nuovo set di dati, fai clic su **[!UICONTROL Create dataset]** nel *[!UICONTROL Datasets]* dashboard.

![](../images/datasets/user-guide/click_to_create.png)

Nella schermata successiva vengono visualizzate le due opzioni seguenti per creare un nuovo set di dati:

* [Crea set di dati dallo schema](#create-a-dataset-with-an-existing-schema)
* [Crea set di dati da file CSV](#create-a-dataset-with-a-csv-file)

### Creare un dataset con uno schema esistente

Nella *[!UICONTROL Create dataset]* schermata fare clic **[!UICONTROL Create dataset from schema]** per creare un nuovo set di dati vuoto.

![](../images/datasets/user-guide/create_dataset_schema.png)

Viene *[!UICONTROL Select schema]* visualizzato il passaggio. Sfogliare l&#39;elenco dello schema e selezionare lo schema a cui il set di dati aderirà prima di fare clic **[!UICONTROL Next]**.

![](../images/datasets/user-guide/select_schema.png)

Viene *[!UICONTROL Configure dataset]* visualizzato il passaggio. Immettete un nome e una descrizione facoltative per il dataset, quindi fate clic **[!UICONTROL Finish]** per crearlo.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Creare un set di dati con un file CSV

Quando un set di dati viene creato utilizzando un file CSV, viene creato uno schema ad hoc per fornire al set di dati una struttura che corrisponde al file CSV fornito. Nella *[!UICONTROL Create dataset]* schermata fare clic sulla casella di testo **[!UICONTROL Create dataset from CSV file]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

Viene *[!UICONTROL Configure]* visualizzato il passaggio. Immettete il set di dati con un nome e una descrizione facoltativa, quindi fate clic **[!UICONTROL Next]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

Viene *[!UICONTROL Add data]* visualizzato il passaggio. Caricate il file CSV trascinandolo e rilasciandolo al centro dello schermo, oppure fate clic **[!UICONTROL Browse]** per esplorare la directory dei file. Il file può avere una dimensione massima di 10 gigabyte. Una volta caricato il file CSV, fate clic **[!UICONTROL Save]** per creare il set di dati.

>[!NOTE]
>
>I nomi delle colonne CSV devono iniziare con caratteri alfanumerici e possono contenere solo lettere, numeri e caratteri di sottolineatura.

![](../images/datasets/user-guide/add_csv_data.png)

## Abilita un set di dati per il profilo cliente in tempo reale

Ogni dataset ha la capacità di arricchire i profili dei clienti con i dati acquisiti. A tal fine, lo schema a cui aderisce il dataset deve essere compatibile per l&#39;utilizzo in [!DNL Real-time Customer Profile]. Uno schema compatibile soddisfa i seguenti requisiti:

* Lo schema ha almeno un attributo specificato come proprietà identity.
* Lo schema presenta una proprietà identity definita come identità primaria.

Per ulteriori informazioni sull&#39;abilitazione di uno schema per [!DNL Profile], vedere la guida [utente dell&#39;Editor](../../xdm/tutorials/create-schema-ui.md)schema.

Per abilitare un set di dati per il profilo, accedi alla *[!UICONTROL Dataset activity]* schermata corrispondente e fai clic sull’ **[!UICONTROL Profile]** interruttore all’interno della *[!UICONTROL Properties]* colonna. Una volta attivato, i dati acquisiti nel dataset verranno utilizzati anche per compilare i profili dei clienti.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

Se un dataset contiene già dei dati e viene quindi abilitato per [!DNL Profile], i dati esistenti non vengono utilizzati da [!DNL Profile]. Dopo che un set di dati è abilitato per [!DNL Profile], si consiglia di ripetere l&#39;acquisizione di tutti i dati esistenti per consentirne la compilazione nei profili cliente.

## Gestione e applicazione della governance dei dati su un dataset

L&#39;etichettatura e l&#39;applicazione dell&#39;uso dei dati (DULE) è il meccanismo di gestione dei dati di base per [!DNL Experience Platform]. Le etichette DULE consentono di classificare set di dati e campi in base ai criteri di utilizzo applicabili ai dati. Per ulteriori informazioni sulle etichette, vedere la panoramica [sulla governance dei](../../data-governance/home.md) dati o consultare la guida [utente relativa alle etichette di utilizzo dei](../../data-governance/labels/overview.md) dati per istruzioni su come applicare le etichette ai set di dati.

## Eliminare un dataset

È possibile eliminare un set di dati accedendo innanzitutto alla *[!UICONTROL Dataset activity]* schermata. Quindi, fate clic **[!UICONTROL Delete dataset]** per eliminarlo.

>[!NOTE]
>
>Non è possibile eliminare i set di dati creati e utilizzati da applicazioni e servizi  Adobe (come  Adobe Analytics, Adobe Audience Manager o [!DNL Decisioning Service]).

![](../images/datasets/user-guide/delete_dataset.png)

Viene visualizzata una casella di conferma. Fare clic **[!UICONTROL Delete]** per confermare l&#39;eliminazione del set di dati.

![](../images/datasets/user-guide/confirm_delete.png)

## Eliminare un set di dati abilitato per il profilo

Se un set di dati è abilitato per [!DNL Profile], eliminandolo nell’interfaccia utente il set di dati viene disattivato per l’inserimento, ma non elimina automaticamente il set di dati nel backend. Per eliminare completamente il dataset, inclusi i dati di profilo e identità forniti, è necessario effettuare un&#39;ulteriore richiesta di eliminazione. Per informazioni su come eliminare correttamente i dati dallo [!DNL Profile] store, consultate la [!DNL Real-time Customer Profile] guida [secondaria API sui processi del sistema dei profili, nota anche come &quot;richieste di eliminazione&quot;](../../profile/api/profile-system-jobs.md).

## Caricamento dei dati del monitor

Nell’ [!DNL Experience Platform] interfaccia utente, fate clic **[!UICONTROL Monitoring]** nel menu di navigazione a sinistra. Il *[!UICONTROL Monitoring]* dashboard consente di visualizzare gli stati dei dati in entrata provenienti dall’assimilazione batch o in streaming. Per visualizzare lo stato dei singoli batch, fare clic su *[!UICONTROL Batch end-to-end]* o *[!UICONTROL Streaming end-to-end]*. Le dashboard elencano tutte le esecuzioni batch o in streaming dell&#39;assimilazione, incluse quelle che hanno esito positivo, non sono riuscite o sono ancora in corso. Ogni elenco fornisce dettagli del batch, inclusi l’ID batch, il nome del set di dati di destinazione e il numero di record acquisiti. Se il set di dati di destinazione è abilitato per [!DNL Profile], viene visualizzato anche il numero di record di identità e profilo acquisiti.

![](../images/datasets/user-guide/batch_listing.png)

È possibile fare clic su un singolo utente **[!UICONTROL Batch ID]** per accedere al *[!UICONTROL Batch overview]* dashboard e visualizzare i dettagli del batch, compresi i log di errore in caso di errore durante il caricamento del batch.

![](../images/datasets/user-guide/batch_overview.png)

Se si desidera eliminare il batch, è possibile fare clic su **[!UICONTROL Delete batch]** trovato nella parte superiore destra del dashboard. In questo modo i record verranno rimossi anche dal set di dati a cui è stato originariamente assimilato il batch.

![](../images/datasets/user-guide/delete_batch.png)

## Passaggi successivi

Questa guida utente fornisce istruzioni per eseguire azioni comuni quando si utilizzano i set di dati nell&#39;interfaccia [!DNL Experience Platform] utente. Per i passaggi relativi all&#39;esecuzione di flussi di lavoro comuni [!DNL Platform] con set di dati, fare riferimento alle seguenti esercitazioni:

* [Creazione di un set di dati tramite le API](create.md)
* [Query dei dati del set di dati tramite l&#39;API Data Access](../../data-access/home.md)
* [Configurare un set di dati per il profilo cliente e il servizio identità in tempo reale mediante le API](../../profile/tutorials/dataset-configuration.md)