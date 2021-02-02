---
keywords: ' Experience Platform;home;argomenti più comuni;abilitare set di dati;dataset'
solution: Experience Platform
title: Guida utente dei set di dati
topic: datasets
description: Questa guida utente per i set di dati fornisce istruzioni sulle operazioni più comuni quando si utilizzano i set di dati nell'interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: d2ace7cadb06f77bdf14b6a4ef83e879c4ca88fd
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 0%

---


# Guida utente dei set di dati

Questa guida utente fornisce istruzioni sull&#39;esecuzione delle azioni comuni quando si utilizzano i set di dati nell&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida utente richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Set](overview.md) di dati: Il concetto di storage e gestione per la persistenza dei dati in  [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Editor](../../xdm/tutorials/create-schema-ui.md) schema: Scoprite come creare schemi XDM personalizzati utilizzando l&#39;interfaccia  [!DNL Schema Editor] all&#39;interno dell&#39;interfaccia  [!DNL Platform] utente.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Assicurati la conformità a normative, restrizioni e criteri relativi all&#39;utilizzo dei dati dei clienti.

## Visualizzare i set di dati

Nell&#39;interfaccia di [!DNL Experience Platform], fare clic su **[!UICONTROL Datasets]** nella barra di navigazione a sinistra per aprire il dashboard di **[!UICONTROL Datasets]**. Il dashboard elenca tutti i set di dati disponibili per l&#39;organizzazione. I dettagli vengono visualizzati per ciascun dataset elencato, incluso il nome, lo schema a cui il dataset aderisce e lo stato dell&#39;assimilazione più recente.

![](../images/datasets/user-guide/browse_datasets.png)

Fare clic sul nome di un dataset per accedere alla relativa schermata **[!UICONTROL Dataset activity]** e visualizzare i dettagli del set di dati selezionato. La scheda dell&#39;attività include un grafico che visualizza il tasso di utilizzo dei messaggi e un elenco di batch con esito positivo o negativo.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Anteprima di un dataset

Dalla schermata **[!UICONTROL Dataset activity]**, fare clic su **[!UICONTROL Preview dataset]** nell&#39;angolo superiore destro dello schermo per visualizzare in anteprima fino a 100 righe di dati. Se il set di dati è vuoto, il collegamento di anteprima verrà disattivato e verrà invece indicato che l&#39;anteprima non è disponibile.

![](../images/datasets/user-guide/click_to_preview.png)

Nella finestra di anteprima, la visualizzazione gerarchica dello schema per il dataset viene visualizzata a destra.

![](../images/datasets/user-guide/preview_dataset.png)

Per metodi più affidabili per accedere ai dati, [!DNL Experience Platform] fornisce servizi a valle come [!DNL Query Service] e [!DNL JupyterLab] per esplorare e analizzare i dati. Per ulteriori informazioni, consulta i documenti seguenti:

* [Panoramica di Servizio query](../../query-service/home.md)
* [Guida utente di JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Creare un dataset {#create}

Per creare un nuovo dataset, fare clic su **[!UICONTROL Create dataset]** nel dashboard di **[!UICONTROL Datasets]**.

![](../images/datasets/user-guide/click_to_create.png)

Nella schermata successiva vengono visualizzate le due opzioni seguenti per creare un nuovo set di dati:

* [Crea set di dati dallo schema](#schema)
* [Crea set di dati da file CSV](#csv)

### Creare un dataset con uno schema esistente {#schema}

Nella schermata **[!UICONTROL Create dataset]**, fare clic su **[!UICONTROL Create dataset from schema]** per creare un nuovo set di dati vuoto.

![](../images/datasets/user-guide/create_dataset_schema.png)

Viene visualizzato il passaggio **[!UICONTROL Select schema]**. Sfogliate l&#39;elenco dello schema e selezionate lo schema a cui il set di dati aderirà prima di fare clic su **[!UICONTROL Next]**.

![](../images/datasets/user-guide/select_schema.png)

Viene visualizzato il passaggio **[!UICONTROL Configure dataset]**. Immettete un nome e una descrizione opzionale per il dataset, quindi fate clic su **[!UICONTROL Finish]** per creare il dataset.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Creare un set di dati con un file CSV {#csv}

Quando un set di dati viene creato utilizzando un file CSV, viene creato uno schema ad hoc per fornire al set di dati una struttura che corrisponde al file CSV fornito. Nella schermata **[!UICONTROL Create dataset]**, fare clic sulla casella con la dicitura **[!UICONTROL Create dataset from CSV file]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

Viene visualizzato il passaggio **[!UICONTROL Configure]**. Immettete il set di dati con un nome e una descrizione facoltativa, quindi fate clic su **[!UICONTROL Next]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

Viene visualizzato il passaggio **[!UICONTROL Add data]**. Caricate il file CSV trascinandolo e rilasciandolo al centro dello schermo, oppure fate clic su **[!UICONTROL Browse]** per esplorare la directory dei file. Il file può avere una dimensione massima di 10 gigabyte. Una volta caricato il file CSV, fate clic su **[!UICONTROL Save]** per creare il set di dati.

>[!NOTE]
>
>I nomi delle colonne CSV devono iniziare con caratteri alfanumerici e possono contenere solo lettere, numeri e caratteri di sottolineatura.

![](../images/datasets/user-guide/add_csv_data.png)

## Abilita un set di dati per il profilo cliente in tempo reale

Ogni dataset ha la capacità di arricchire i profili dei clienti con i dati acquisiti. A tal fine, lo schema a cui aderisce il dataset deve essere compatibile per l&#39;utilizzo in [!DNL Real-time Customer Profile]. Uno schema compatibile soddisfa i seguenti requisiti:

* Lo schema ha almeno un attributo specificato come proprietà identity.
* Lo schema presenta una proprietà identity definita come identità primaria.

Per ulteriori informazioni sull&#39;abilitazione di uno schema per [!DNL Profile], vedere la [Guida utente dell&#39;Editor di schema](../../xdm/tutorials/create-schema-ui.md).

Per abilitare un dataset per il profilo, accedete alla relativa schermata **[!UICONTROL Dataset activity]** e fate clic sull&#39;interruttore **[!UICONTROL Profile]** all&#39;interno della colonna **[!UICONTROL Properties]**. Una volta attivato, i dati acquisiti nel dataset verranno utilizzati anche per compilare i profili dei clienti.

>[!NOTE]
>
>Se un dataset contiene già dei dati e viene quindi abilitato per [!DNL Profile], i dati esistenti non vengono utilizzati automaticamente da [!DNL Profile]. Dopo che un set di dati è abilitato per [!DNL Profile], si consiglia di ripetere l&#39;acquisizione di tutti i dati esistenti per consentirne l&#39;aggiunta ai profili cliente.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

## Gestione e applicazione della governance dei dati su un dataset

Le etichette di utilizzo dei dati consentono di classificare set di dati e campi in base ai criteri di utilizzo applicabili ai dati. Per ulteriori informazioni sulle etichette, consultare la [Panoramica sulla governance dei dati](../../data-governance/home.md) oppure consultare la [guida utente delle etichette di utilizzo dei dati](../../data-governance/labels/overview.md) per istruzioni su come applicare le etichette ai set di dati.

## Eliminare un dataset

È possibile eliminare un dataset accedendo prima alla relativa schermata **[!UICONTROL Dataset activity]**. Quindi, fare clic su **[!UICONTROL Delete dataset]** per eliminarlo.

>[!NOTE]
>
>I set di dati creati e utilizzati da applicazioni e servizi  Adobe (ad esempio  Adobe Analytics, Adobe Audience Manager o [!DNL Offer Decisioning]) non possono essere eliminati.

![](../images/datasets/user-guide/delete_dataset.png)

Viene visualizzata una casella di conferma. Fare clic su **[!UICONTROL Delete]** per confermare l&#39;eliminazione del set di dati.

![](../images/datasets/user-guide/confirm_delete.png)

## Eliminare un set di dati abilitato per il profilo

Se un set di dati è abilitato per [!DNL Profile], eliminando tale set di dati tramite l&#39;interfaccia utente, esso verrà eliminato sia dal Data Lake che dallo store Profile all&#39;interno della piattaforma.

Puoi eliminare un dataset solo dallo store [!DNL Profile] (lasciando i dati nel Data Lake) utilizzando l&#39;API Profilo cliente in tempo reale. Per ulteriori informazioni, consultate la [guida per l&#39;endpoint API dei processi del sistema di profilo](../../profile/api/profile-system-jobs.md).

## Caricamento dei dati del monitor

Nell&#39;interfaccia di [!DNL Experience Platform], fare clic su **[!UICONTROL Monitoring]** nella barra di navigazione a sinistra. Il dashboard di **[!UICONTROL Monitoring]** consente di visualizzare gli stati dei dati in entrata provenienti dall&#39;inserimento batch o in streaming. Per visualizzare lo stato dei singoli batch, fare clic su **[!UICONTROL Batch end-to-end]** o **[!UICONTROL Streaming end-to-end]**. Le dashboard elencano tutte le esecuzioni batch o in streaming dell&#39;assimilazione, incluse quelle che hanno esito positivo, non sono riuscite o sono ancora in corso. Ogni elenco fornisce dettagli del batch, inclusi l’ID batch, il nome del set di dati di destinazione e il numero di record acquisiti. Se il set di dati di destinazione è abilitato per [!DNL Profile], viene visualizzato anche il numero di record di identità e di profilo acquisiti.

![](../images/datasets/user-guide/batch_listing.png)

È possibile fare clic su un singolo **[!UICONTROL Batch ID]** per accedere al dashboard **[!UICONTROL Batch overview]** e visualizzare i dettagli per il batch, compresi i registri di errore in caso di errore durante l&#39;acquisizione del batch.

![](../images/datasets/user-guide/batch_overview.png)

Se si desidera eliminare il batch, è possibile fare clic su **[!UICONTROL Delete batch]** nella parte superiore destra del dashboard. In questo modo i record verranno rimossi anche dal set di dati a cui è stato originariamente assimilato il batch.

![](../images/datasets/user-guide/delete_batch.png)

## Passaggi successivi

Questa guida utente fornisce istruzioni per eseguire azioni comuni quando si utilizzano i set di dati nell&#39;interfaccia utente [!DNL Experience Platform]. Per la procedura relativa all&#39;esecuzione di flussi di lavoro comuni [!DNL Platform] che coinvolgono set di dati, fare riferimento alle seguenti esercitazioni:

* [Creazione di un set di dati tramite le API](create.md)
* [Query dei dati del set di dati tramite l&#39;API Data Access](../../data-access/home.md)
* [Configurare un set di dati per il profilo cliente e il servizio identità in tempo reale mediante le API](../../profile/tutorials/dataset-configuration.md)