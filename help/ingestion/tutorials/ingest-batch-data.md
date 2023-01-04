---
keywords: Experience Platform;home;argomenti popolari;acquisizione;acquisire dati batch;tutorial;acquisizione batch;tutorial;guida interfaccia utente;
solution: Experience Platform
title: Inserire dati in Experience Platform
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform consente di importare facilmente i dati come file batch sotto forma di file Parquet o dati conformi a uno schema Experience Data Model (XDM) noto.
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 0%

---

# Inserire dati in Adobe Experience Platform

Adobe Experience Platform consente di importare facilmente i dati in [!DNL Platform] come file batch. Esempi di dati da acquisire possono includere dati di profilo provenienti da un file flat in un sistema CRM (ad esempio un file Parquet) o dati conformi a un file noto [!DNL Experience Data Model] Schema (XDM) nel Registro di sistema dello schema.

## Introduzione

Per completare questa esercitazione, devi disporre dell’accesso a [!DNL Experience Platform]. Se non hai accesso a un’organizzazione IMS in [!DNL Experience Platform]Prima di procedere, rivolgiti all’amministratore di sistema.

Se preferisci acquisire dati utilizzando le API di acquisizione dati, inizia leggendo il [Guida per gli sviluppatori di inserimento in batch](../batch-ingestion/api-overview.md).

## Area di lavoro dei set di dati

Area di lavoro dei set di dati all’interno di [!DNL Experience Platform] consente di visualizzare e gestire tutti i set di dati creati dall’organizzazione IMS e di crearne di nuovi.

Visualizzare l’area di lavoro Set di dati facendo clic su **[!UICONTROL Set di dati]** nella navigazione a sinistra. L’area di lavoro Set di dati contiene un elenco di set di dati, tra cui colonne che mostrano nome, data e ora create, origine, schema e stato dell’ultimo batch, nonché la data e l’ora dell’ultimo aggiornamento del set di dati.

>[!NOTE]
>
>Fai clic sull’icona del filtro accanto alla barra di ricerca per utilizzare le funzionalità di filtro per visualizzare solo i set di dati abilitati per [!DNL Profile].

![Visualizza tutti i set di dati](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Creare un set di dati

Per creare un set di dati, fai clic su **[!UICONTROL Crea set di dati]** nell’angolo in alto a destra dell’area di lavoro Set di dati .

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

Sulla **[!UICONTROL Crea set di dati]** schermata , seleziona se desideri &quot;[!UICONTROL Crea set di dati da schema]&quot; o &quot;[!UICONTROL Crea set di dati da file CSV]&quot;.

Per questa esercitazione, verrà utilizzato uno schema per creare il set di dati. Fai clic su **[!UICONTROL Crea set di dati da schema]** per continuare.

![Seleziona origine dati](../images/tutorials/ingest-batch-data/create-dataset.png)

## Seleziona schema set di dati

Sulla **[!UICONTROL Seleziona schema]** scegli uno schema facendo clic sul pulsante di scelta accanto allo schema che desideri utilizzare. Per questa esercitazione, il set di dati verrà creato utilizzando lo schema Membri fedeltà . L’utilizzo della barra di ricerca per filtrare gli schemi è un modo utile per trovare lo schema esatto che si sta cercando.

Dopo aver selezionato il pulsante di scelta accanto allo schema da utilizzare, fare clic su **[!UICONTROL Successivo]**.

![Seleziona schema](../images/tutorials/ingest-batch-data/select-schema.png)

## Configurare il set di dati

Sulla **[!UICONTROL Configura set di dati]** viene richiesto di assegnare un nome al set di dati e può anche fornire una descrizione del set di dati.

**Note sui nomi dei set di dati:**

- I nomi dei set di dati devono essere brevi e descrittivi in modo che il set di dati possa essere facilmente trovato nella libreria in un secondo momento.
- I nomi dei set di dati devono essere univoci, il che significa che devono anche essere sufficientemente specifici da non essere riutilizzati in futuro.
- È consigliabile fornire informazioni aggiuntive sul set di dati utilizzando il campo descrizione, in quanto potrebbe aiutare altri utenti a distinguere tra set di dati in futuro.

Una volta che il set di dati ha un nome e una descrizione, fai clic su **[!UICONTROL Fine]**.

![Configurare il set di dati](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Attività set di dati

Ora è stato creato un set di dati vuoto e sei stato restituito al **[!UICONTROL Attività set di dati]** nell’area di lavoro Set di dati. Dovresti visualizzare il nome del set di dati nell’angolo in alto a sinistra dell’area di lavoro, insieme a una notifica che indica che non sono stati aggiunti batch. Questo è da aspettarsi, in quanto non hai ancora aggiunto batch a questo set di dati.

Sul lato destro dell’area di lavoro Set di dati viene visualizzata la variabile **[!UICONTROL Info]** scheda contenente informazioni relative al nuovo set di dati quali ID set di dati, nome, descrizione, nome della tabella, schema, streaming e origine. La scheda Informazioni include anche informazioni su quando è stato creato il set di dati e la sua ultima data di modifica.

Anche nella scheda Informazioni è presente un  **[!UICONTROL Profilo]** attiva/disattiva utilizzato per abilitare il set di dati per l’utilizzo con [!DNL Real-Time Customer Profile]. Utilizzo di questo interruttore e [!DNL Real-Time Customer Profile], sarà spiegato più dettagliatamente nella sezione che segue.

![Attività set di dati](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Abilita set di dati per [!DNL Real-Time Customer Profile]

I set di dati vengono utilizzati per acquisire i dati in [!DNL Experience Platform]e che i dati vengono utilizzati in ultima analisi per identificare gli individui e unire le informazioni provenienti da più fonti. L&#39;informazione unita si chiama [!DNL Real-Time Customer Profile]. Per [!DNL Platform] per sapere quali informazioni devono essere incluse nel [!DNL Real-Time Profile], i set di dati possono essere contrassegnati per l’inclusione utilizzando **[!UICONTROL Profilo]** alternare.

Per impostazione predefinita, questa opzione è disattivata. Se scegli di attivare [!DNL Profile], tutti i dati acquisiti nel set di dati verranno utilizzati per identificare un individuo e unire le sue relazioni [!DNL Real-Time Profile].

Per ulteriori informazioni [!DNL Real-Time Customer Profile] e lavorando con le identità, controlla i [Servizio identità](../../identity-service/home.md) documentazione.

Per abilitare il set di dati per [!DNL Real-Time Customer Profile], fai clic su **[!UICONTROL Profilo]** attivare **[!UICONTROL Info]** scheda .

![Attiva/disattiva profilo](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di confermare l’abilitazione del set di dati per [!DNL Real-Time Customer Profile].

![Finestra di dialogo Abilita profilo](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Fai clic su **[!UICONTROL Abilita]** e l&#39;interruttore diventa blu e indica che è attivato.

![Abilitato per profilo](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Aggiungere dati al set di dati

I dati possono essere aggiunti in un set di dati in diversi modi. Puoi scegliere di utilizzare [!DNL Data Ingestion] API o un partner ETL come [!DNL Unifi] o [!DNL Informatica]. Per questa esercitazione, i dati verranno aggiunti al set di dati utilizzando **[!UICONTROL Aggiungi dati]** nell’interfaccia utente di .

Per iniziare ad aggiungere dati al set di dati, fai clic sul pulsante **[!UICONTROL Aggiungi dati]** scheda . È ora possibile trascinare e rilasciare i file o cercare nel computer i file che si desidera aggiungere.

>[!NOTE]
>
>Platform supporta due tipi di file per l’acquisizione di dati, Parquet o JSON. È possibile aggiungere fino a cinque file alla volta, con la dimensione massima di ciascun file pari a 1 GB.

![Aggiungi dati, scheda](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Caricare un file

Una volta trascinati e rilascia (o sfoglia e seleziona) un file Parquet o JSON da caricare, [!DNL Platform] inizierà immediatamente a elaborare il file e un **[!UICONTROL Caricamento]** nella finestra di dialogo **[!UICONTROL Aggiungi dati]** mostra l’avanzamento del caricamento del file.

![Finestra di dialogo di caricamento](../images/tutorials/ingest-batch-data/uploading-file.png)

## Metriche del set di dati

Al termine del caricamento del file, il **[!UICONTROL Attività set di dati]** La scheda non mostra più che &quot;non sono stati aggiunti batch&quot;. Invece, **[!UICONTROL Attività set di dati]** La scheda ora mostra le metriche del set di dati. Tutte le metriche mostrano &quot;0&quot; in questa fase, in quanto il batch non è ancora caricato.

Nella parte inferiore della scheda è presente un elenco che mostra il **[!UICONTROL ID batch]** dei dati appena acquisiti tramite [&quot;Aggiungi dati al set di dati&quot;](#add-data-to-dataset) processo. Sono incluse anche le informazioni relative al batch, tra cui data di acquisizione, numero di record acquisiti e stato del batch corrente.

![Metriche del set di dati](../images/tutorials/ingest-batch-data/batch-id.png)

## Dettagli batch

Fai clic sul pulsante **[!UICONTROL ID batch]** per visualizzare un **[!UICONTROL Panoramica batch]**, mostrando ulteriori dettagli relativi al batch. Al termine del caricamento del batch, le informazioni sul batch verranno aggiornate per mostrare il numero di record acquisiti e le dimensioni del file. Lo stato viene modificato anche in &quot;Completato&quot; o &quot;Non riuscito&quot;. Se il batch non riesce, **[!UICONTROL Codice di errore]** la sezione conterrà i dettagli relativi a eventuali errori durante l’acquisizione.

Per ulteriori informazioni e domande frequenti sull’acquisizione di batch, consulta la sezione [Guida alla risoluzione dei problemi di inserimento in batch](../batch-ingestion/troubleshooting.md).

Per tornare al **[!UICONTROL Attività set di dati]** fai clic sul nome del set di dati (**[!UICONTROL Dettagli fedeltà]**) nel breadcrumb.

![Panoramica batch](../images/tutorials/ingest-batch-data/batch-details.png)

## Anteprima set di dati

Una volta pronto il set di dati, un’opzione per **[!UICONTROL Anteprima set di dati]** viene visualizzato nella parte superiore della **[!UICONTROL Attività set di dati]** scheda .

Fai clic su **[!UICONTROL Anteprima set di dati]** per aprire una finestra di dialogo che mostra i dati di esempio dall’interno del set di dati. Se il set di dati è stato creato utilizzando uno schema, i dettagli dello schema del set di dati verranno visualizzati sul lato sinistro dell’anteprima. È possibile espandere lo schema utilizzando le frecce per visualizzare la struttura dello schema. Ogni intestazione di colonna nei dati di anteprima rappresenta un campo nel set di dati.

![Dettagli del set di dati](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Passaggi successivi e risorse aggiuntive

Ora che hai creato un set di dati e i dati sono stati correttamente acquisiti in [!DNL Experience Platform], puoi ripetere questi passaggi per creare un nuovo set di dati o per acquisire più dati nel set di dati esistente.

Per ulteriori informazioni sull’acquisizione batch, consulta la sezione [Panoramica sull’acquisizione in batch](../batch-ingestion/overview.md) e completa il tuo apprendimento guardando il video qui sotto.

>[!WARNING]
>
>La [!DNL Platform] L’interfaccia utente mostrata nel video seguente è obsoleta. Fai riferimento alla documentazione precedente per le ultime schermate e funzionalità dell’interfaccia utente.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
