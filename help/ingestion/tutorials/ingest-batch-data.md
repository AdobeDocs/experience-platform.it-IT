---
keywords: ' Experience Platform;home;argomenti popolari;assimilazione;assimilare dati batch;esercitazione;inserimento batch;esercitazione;tutorial;ui guide;'
solution: Experience Platform
title: Caricamento di dati in Adobe Experience Platform
topic: tutorial
type: Tutorial
description: Adobe Experience Platform consente di importare facilmente i dati come file batch sotto forma di file Parquet o dati conformi a uno schema XDM (Experience Data Model) noto.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '1262'
ht-degree: 0%

---


# Caricamento di dati in Adobe Experience Platform

Adobe Experience Platform consente di importare facilmente i dati in [!DNL Platform] come file batch. Esempi di dati da assimilare possono includere dati di profilo da un file semplice in un sistema CRM (ad esempio un file Parquet) o dati conformi a uno schema [!DNL Experience Data Model] (XDM) noto nel Registro di sistema dello schema.

## Introduzione

Per completare questa esercitazione, è necessario avere accesso a [!DNL Experience Platform]. Se non disponete dell&#39;accesso a un&#39;organizzazione IMS in [!DNL Experience Platform], rivolgetevi all&#39;amministratore di sistema prima di procedere.

Se preferisci assimilare i dati utilizzando le API di inserimento dati, inizia leggendo la [Guida per sviluppatori di inserimento batch](../batch-ingestion/api-overview.md).

## Area di lavoro DataSet

L&#39;area di lavoro Set di dati all&#39;interno di [!DNL Experience Platform] consente di visualizzare e gestire tutti i set di dati creati dall&#39;organizzazione IMS e di crearne di nuovi.

Visualizzare l&#39;area di lavoro Set di dati facendo clic su **[!UICONTROL Datasets]** nella barra di navigazione a sinistra. L&#39;area di lavoro Set di dati contiene un elenco di set di dati, tra cui colonne che mostrano nome, data e ora create, origine, schema e ultimo stato batch, nonché la data e l&#39;ora dell&#39;ultimo aggiornamento del set di dati.

>[!NOTE]
>
>Fate clic sull&#39;icona del filtro accanto alla barra di ricerca per utilizzare le funzionalità di filtro per visualizzare solo i set di dati abilitati per [!DNL Profile].

![Visualizza tutti i set di dati](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Creare un dataset

Per creare un set di dati, fare clic su **[!UICONTROL Create Dataset]** nell&#39;angolo superiore destro dell&#39;area di lavoro Set di dati.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

Nella schermata **[!UICONTROL Create Dataset]**, selezionare se si desidera &quot;[!UICONTROL Create Dataset from Schema]&quot; o &quot;[!UICONTROL Create Dataset from CSV File]&quot;.

Per questa esercitazione, verrà utilizzato uno schema per creare il dataset. Fare clic su **[!UICONTROL Create Dataset from Schema]** per continuare.

![Seleziona origine dati](../images/tutorials/ingest-batch-data/create-dataset.png)

## Seleziona schema set di dati

Nella schermata **[!UICONTROL Select Schema]**, scegliere uno schema facendo clic sul pulsante di scelta accanto allo schema da utilizzare. Per questa esercitazione, il dataset verrà creato utilizzando lo schema Membri fedeltà. L&#39;utilizzo della barra di ricerca per filtrare gli schemi è un modo utile per individuare lo schema esatto che si sta cercando.

Dopo aver selezionato il pulsante di scelta accanto allo schema da utilizzare, fare clic su **[!UICONTROL Next]**.

![Seleziona schema](../images/tutorials/ingest-batch-data/select-schema.png)

## Configura set di dati

Nella schermata **[!UICONTROL Configure Dataset]**, sarà necessario assegnare al dataset un nome e potrebbe anche fornire una descrizione del set di dati.

**Note sui nomi dei set di dati:**

- I nomi dei set di dati devono essere brevi e descrittivi in modo che il set di dati possa essere facilmente trovato nella libreria in un secondo momento.
- I nomi dei set di dati devono essere univoci, il che significa che devono essere sufficientemente specifici da non essere riutilizzati in futuro.
- È consigliabile fornire informazioni aggiuntive sul set di dati utilizzando il campo di descrizione, in quanto potrebbe aiutare altri utenti a distinguere tra set di dati in futuro.

Una volta che il dataset ha un nome e una descrizione, fare clic su **[!UICONTROL Finish]**.

![Configura set di dati](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Attività DataSet

È stato creato un set di dati vuoto e si è tornati alla scheda **[!UICONTROL Dataset Activity]** nell&#39;area di lavoro Set di dati. Il nome del set di dati deve essere visualizzato nell’angolo in alto a sinistra dell’area di lavoro, insieme alla notifica che &quot;Non sono stati aggiunti batch&quot;. Questo è previsto perché non avete ancora aggiunto alcun batch a questo set di dati.

Sul lato destro dell&#39;area di lavoro Set di dati viene visualizzata la scheda **[!UICONTROL Info]** contenente informazioni relative al nuovo set di dati come ID dataset, nome, descrizione, nome tabella, schema, streaming e origine. La scheda Informazioni include inoltre informazioni sulla data di creazione del set di dati e sulla data dell&#39;ultima modifica.

Nella scheda Informazioni è presente anche un interruttore **[!UICONTROL Profile]** che viene utilizzato per abilitare il dataset per l&#39;uso con [!DNL Real-time Customer Profile]. L&#39;utilizzo di questa attivazione e [!DNL Real-time Customer Profile] verrà descritto più dettagliatamente nella sezione che segue.

![Attività DataSet](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Abilita set di dati per [!DNL Real-time Customer Profile]

I set di dati vengono utilizzati per l&#39;assimilazione di dati in [!DNL Experience Platform] e tali dati vengono utilizzati per identificare individui e unire insieme informazioni provenienti da più origini. Le informazioni unite vengono denominate [!DNL Real-Time Customer Profile]. Affinché [!DNL Platform] sappia quali informazioni includere nella [!DNL Real-Time Profile], i set di dati possono essere contrassegnati per l&#39;inclusione utilizzando l&#39;interruttore **[!UICONTROL Profile]**.

Per impostazione predefinita, questa opzione è disattivata. Se si sceglie di attivare [!DNL Profile], tutti i dati inseriti nel dataset verranno utilizzati per identificare un singolo e unire insieme il relativo [!DNL Real-Time Profile].

Per ulteriori informazioni su [!DNL Real-time Customer Profile] e sull&#39;utilizzo delle identità, consultare la documentazione relativa al [Servizio identità](../../identity-service/home.md).

Per abilitare il set di dati per [!DNL Real-time Customer Profile], fare clic sull&#39;opzione **[!UICONTROL Profile]** nella scheda **[!UICONTROL Info]**.

![Attiva/disattiva profilo](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di confermare che si desidera abilitare il dataset per [!DNL Real-time Customer Profile].

![Abilita finestra di dialogo Profilo](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Fare clic su **[!UICONTROL Enable]** e l&#39;interruttore diventa blu, a indicare che è attivato.

![Abilitato per profilo](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Aggiungere dati al dataset

I dati possono essere aggiunti in un set di dati in diversi modi. Potete scegliere di utilizzare le [!DNL Data Ingestion] API o un partner ETL come [!DNL Unifi] o [!DNL Informatica]. Per questa esercitazione, i dati verranno aggiunti al dataset utilizzando la scheda **[!UICONTROL Add Data]** nell&#39;interfaccia utente.

Per iniziare ad aggiungere dati al dataset, fare clic sulla scheda **[!UICONTROL Add Data]**. È ora possibile trascinare e rilasciare i file o cercare nel computer i file da aggiungere.

>[!NOTE]
>
>La piattaforma supporta due tipi di file per l&#39;assimilazione dei dati, Parquet o JSON. È possibile aggiungere fino a cinque file alla volta, con una dimensione massima di file pari a 10 GB.

![Aggiungi dati, scheda](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Caricare un file

Dopo aver trascinato e rilasciato (o sfogliare e selezionare) un file Parquet o JSON che si desidera caricare, [!DNL Platform] inizierà immediatamente a elaborare il file e nella scheda **[!UICONTROL Uploading]** verrà visualizzata una finestra di dialogo che mostra l&#39;avanzamento del caricamento del file.**[!UICONTROL Add Data]**

![Finestra di dialogo di caricamento](../images/tutorials/ingest-batch-data/uploading-file.png)

## Metriche DataSet

Al termine del caricamento del file, nella scheda **[!UICONTROL Dataset Activity]** non viene più visualizzato &quot;Nessun batch aggiunto&quot;. Al contrario, la scheda **[!UICONTROL Dataset Activity]** ora mostra le metriche del set di dati. Tutte le metriche mostreranno &quot;0&quot; in questa fase perché il batch non è ancora caricato.

Nella parte inferiore della scheda è presente un elenco che mostra la **[!UICONTROL Batch ID]** dei dati appena acquisiti tramite il processo [&quot;Add data to dataset&quot;](#add-data-to-dataset). Sono incluse anche le informazioni relative al batch, inclusa la data di acquisizione, il numero di record acquisiti e lo stato corrente del batch.

![Metriche DataSet](../images/tutorials/ingest-batch-data/batch-id.png)

## Dettagli batch

Fare clic su **[!UICONTROL Batch ID]** per visualizzare un **[!UICONTROL Batch Overview]**, mostrando ulteriori dettagli relativi al batch. Al termine del caricamento del batch, le informazioni relative al batch verranno aggiornate per mostrare il numero di record acquisiti e la dimensione del file. Anche lo stato diventa &quot;Success&quot; o &quot;Failed&quot; (Successo). Se il batch non riesce, la sezione **[!UICONTROL Error Code]** conterrà dettagli relativi a eventuali errori durante l&#39;assimilazione.

Per ulteriori informazioni e domande frequenti sull&#39;inserimento di batch, consultare la [Guida alla risoluzione dei problemi di inserimento di batch](../batch-ingestion/troubleshooting.md).

Per tornare alla schermata **[!UICONTROL Dataset Activity]**, fare clic sul nome del set di dati (**[!UICONTROL Loyalty Details]**) nella breadcrumb.

![Panoramica batch](../images/tutorials/ingest-batch-data/batch-details.png)

## Anteprima set di dati

Una volta pronto il set di dati, nella parte superiore della scheda **[!UICONTROL Dataset Activity]** viene visualizzata l&#39;opzione **[!UICONTROL Preview Dataset]**.

Fare clic su **[!UICONTROL Preview Dataset]** per aprire una finestra di dialogo che mostra i dati di esempio dall&#39;interno del dataset. Se il set di dati è stato creato utilizzando uno schema, i dettagli per lo schema del set di dati verranno visualizzati sul lato sinistro dell&#39;anteprima. È possibile espandere lo schema utilizzando le frecce per visualizzare la struttura dello schema. Ogni intestazione di colonna nei dati di anteprima rappresenta un campo nel dataset.

![Dettagli del set di dati](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Passaggi successivi e risorse aggiuntive

Dopo aver creato un dataset e aver correttamente inserito i dati in [!DNL Experience Platform], è possibile ripetere questi passaggi per creare un nuovo dataset o per inserire più dati nel dataset esistente.

Per saperne di più sull&#39;inserimento in batch, leggere la [Panoramica sull&#39;inserimento in batch](../batch-ingestion/overview.md) e completare l&#39;apprendimento guardando il video sottostante.

>[!WARNING]
>
>L&#39;interfaccia [!DNL Platform] mostrata nel video seguente è obsoleta. Per informazioni sulle ultime funzionalità e videate dell’interfaccia, consulta la documentazione precedente.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)