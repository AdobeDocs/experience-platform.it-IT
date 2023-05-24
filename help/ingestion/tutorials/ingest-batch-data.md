---
keywords: Experience Platform;home;argomenti popolari;inserimento;inserire dati batch;esercitazione;inserimento batch;tutorial;guida interfaccia utente;
solution: Experience Platform
title: Acquisire dati in Experience Platform
type: Tutorial
description: Adobe Experience Platform consente di importare facilmente i dati come file batch sotto forma di file Parquet o dati conformi a uno schema Experience Data Model (XDM) noto.
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 1%

---

# Acquisire dati in Adobe Experience Platform

Adobe Experience Platform consente di importare facilmente i dati in [!DNL Platform] come file batch. Esempi di dati da acquisire possono includere dati di profilo da un file flat in un sistema di gestione delle relazioni con i clienti (come un file Parquet) o dati conformi a un file noto [!DNL Experience Data Model] (XDM) nel registro degli schemi.

## Introduzione

Per completare questa esercitazione, devi avere accesso a [!DNL Experience Platform]. Se non hai accesso a un’organizzazione in [!DNL Experience Platform], contattare l&#39;amministratore di sistema prima di procedere.

Se preferisci acquisire i dati utilizzando le API di acquisizione dati, leggi innanzitutto [Guida per gli sviluppatori sull’acquisizione in batch](../batch-ingestion/api-overview.md).

## Area di lavoro Set di dati

L’area di lavoro Set di dati in [!DNL Experience Platform] consente di visualizzare e gestire tutti i set di dati creati dalla tua organizzazione, nonché di crearne di nuovi.

Visualizzare l’area di lavoro Set di dati facendo clic su **[!UICONTROL Set di dati]** nel menu di navigazione a sinistra. L’area di lavoro Set di dati contiene un elenco di set di dati, incluse le colonne con nome, data e ora di creazione, origine, schema e ultimo stato batch, nonché la data e l’ora dell’ultimo aggiornamento del set di dati.

>[!NOTE]
>
>Fai clic sull’icona del filtro accanto alla barra di ricerca per utilizzare le funzionalità di filtro per visualizzare solo i set di dati abilitati per [!DNL Profile].

![Visualizza tutti i set di dati](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Creare un set di dati

Per creare un set di dati, fai clic su **[!UICONTROL Crea set di dati]** nell’angolo in alto a destra dell’area di lavoro Set di dati.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

Il giorno **[!UICONTROL Crea set di dati]** , seleziona se desideri &quot;[!UICONTROL Crea set di dati dallo schema]&quot; o &quot;[!UICONTROL Crea set di dati da file CSV]&quot;.

Per questa esercitazione, verrà utilizzato uno schema per creare il set di dati. Clic **[!UICONTROL Crea set di dati dallo schema]** per continuare.

![Seleziona origine dati](../images/tutorials/ingest-batch-data/create-dataset.png)

## Seleziona schema set di dati

Il giorno **[!UICONTROL Seleziona schema]** scegliere uno schema facendo clic sul pulsante di opzione accanto allo schema che si desidera utilizzare. Per questa esercitazione, il set di dati verrà creato utilizzando lo schema Membri fedeltà. L’utilizzo della barra di ricerca per filtrare gli schemi è utile per trovare lo schema esatto desiderato.

Dopo aver selezionato il pulsante di opzione accanto allo schema da utilizzare, fai clic su **[!UICONTROL Successivo]**.

![Seleziona schema](../images/tutorials/ingest-batch-data/select-schema.png)

## Configurare il set di dati

Il giorno **[!UICONTROL Configurare il set di dati]** schermata, ti verrà richiesto di assegnare un nome al set di dati e di fornirne anche una descrizione.

**Note sui nomi dei set di dati:**

- I nomi dei set di dati devono essere brevi e descrittivi in modo che il set di dati possa essere facilmente trovato in un secondo momento nella libreria.
- I nomi dei set di dati devono essere univoci, ovvero devono essere sufficientemente specifici da non poter essere riutilizzati in futuro.
- È consigliabile fornire informazioni aggiuntive sul set di dati utilizzando il campo descrizione, in quanto in futuro potrebbe aiutare altri utenti a distinguere tra i set di dati.

Una volta che il set di dati ha un nome e una descrizione, fai clic su **[!UICONTROL Fine]**.

![Configurare il set di dati](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Attività set di dati

È stato creato un set di dati vuoto e ora sei stato reindirizzato al **[!UICONTROL Attività set di dati]** nell’area di lavoro Set di dati. Dovresti visualizzare il nome del set di dati nell’angolo in alto a sinistra dell’area di lavoro, insieme a una notifica che informa che &quot;Non è stato aggiunto alcun batch&quot;. Ciò è previsto perché non hai ancora aggiunto batch a questo set di dati.

Sul lato destro dell’area di lavoro Set di dati verrà visualizzato il file **[!UICONTROL Info]** scheda contenente informazioni relative al nuovo set di dati, ad esempio ID set di dati, nome, descrizione, nome tabella, schema, streaming e origine. La scheda Info include anche informazioni su quando è stato creato il set di dati e sulla data dell’ultima modifica.

Anche nella scheda Info è presente un  **[!UICONTROL Profilo]** che viene utilizzato per abilitare il set di dati per l’utilizzo con [!DNL Real-Time Customer Profile]. Utilizzo di questo interruttore e [!DNL Real-Time Customer Profile], verrà spiegato più dettagliatamente nella sezione che segue.

![Attività set di dati](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Abilita set di dati per [!DNL Real-Time Customer Profile]

I set di dati vengono utilizzati per acquisire i dati in [!DNL Experience Platform]e che i dati vengano infine utilizzati per identificare gli individui e unire le informazioni provenienti da più origini. Queste informazioni unite vengono definite [!DNL Real-Time Customer Profile]. Per ottenere [!DNL Platform] per sapere quali informazioni includere nella [!DNL Real-Time Profile], i set di dati possono essere contrassegnati per l’inclusione utilizzando **[!UICONTROL Profilo]** attivare/disattivare.

Per impostazione predefinita, questa opzione è disattivata. Se scegli di attivare [!DNL Profile], tutti i dati acquisiti nel set di dati verranno utilizzati per identificare un individuo e unire i [!DNL Real-Time Profile].

Per ulteriori informazioni su [!DNL Real-Time Customer Profile] e, lavorando con le identità, consulta la sezione [Servizio identità](../../identity-service/home.md) documentazione.

Per abilitare il set di dati per [!DNL Real-Time Customer Profile], fare clic su **[!UICONTROL Profilo]** attivare/disattivare **[!UICONTROL Info]** scheda.

![Attiva/disattiva profilo](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Verrà visualizzata una finestra di dialogo in cui ti viene richiesto di confermare che desideri abilitare il set di dati per [!DNL Real-Time Customer Profile].

![Finestra di dialogo Abilita profilo](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Clic **[!UICONTROL Abilita]** e l’interruttore diventa blu, a indicare che è attivato.

![Abilitato per il profilo](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Aggiungi dati al set di dati

I dati possono essere aggiunti a un set di dati in diversi modi. Puoi scegliere di utilizzare [!DNL Data Ingestion] API o un partner ETL come [!DNL Unifi] o [!DNL Informatica]. Per questa esercitazione, i dati verranno aggiunti al set di dati utilizzando **[!UICONTROL Aggiungi dati]** nell’interfaccia utente.

Per iniziare ad aggiungere dati al set di dati, fai clic sul pulsante **[!UICONTROL Aggiungi dati]** scheda. È ora possibile trascinare e rilasciare i file o cercare nel computer i file che si desidera aggiungere.

>[!NOTE]
>
>Platform supporta due tipi di file per l’acquisizione dei dati, Parquet o JSON. È possibile aggiungere fino a cinque file alla volta, con la dimensione massima di ogni file pari a 1 GB.

![Scheda Aggiungi dati](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Carica un file

Una volta trascinato (o sfogliato e selezionato) un file Parquet o JSON da caricare, [!DNL Platform] inizierà immediatamente a elaborare il file e un **[!UICONTROL Carica]** verrà visualizzata sulla **[!UICONTROL Aggiungi dati]** che mostra l’avanzamento del caricamento del file.

![Finestra di dialogo Caricamento](../images/tutorials/ingest-batch-data/uploading-file.png)

## Metriche del set di dati

Al termine del caricamento del file, **[!UICONTROL Attività set di dati]** La scheda non mostra più che &quot;Non è stato aggiunto alcun batch&quot;. Al contrario, **[!UICONTROL Attività set di dati]** La scheda ora mostra le metriche dei set di dati. Tutte le metriche mostrano &quot;0&quot; in questa fase perché il batch non è ancora stato caricato.

Nella parte inferiore della scheda è riportato un elenco che mostra **[!UICONTROL ID batch]** dei dati appena acquisiti tramite il [&quot;Aggiungi dati al set di dati&quot;](#add-data-to-dataset) processo. Sono incluse anche le informazioni relative al batch, tra cui data di acquisizione, numero di record acquisiti e stato corrente del batch.

![Metriche del set di dati](../images/tutorials/ingest-batch-data/batch-id.png)

## Dettagli batch

Fai clic sul pulsante **[!UICONTROL ID batch]** per visualizzare un **[!UICONTROL Panoramica batch]**, che mostra ulteriori dettagli relativi al batch. Una volta completato il caricamento del batch, le informazioni sul batch vengono aggiornate per mostrare il numero di record acquisiti e la dimensione del file. Lo stato cambia anche in &quot;Completato&quot; o &quot;Non riuscito&quot;. Se il batch non riesce, **[!UICONTROL Codice di errore]** questa sezione conterrà i dettagli relativi a eventuali errori durante l’acquisizione.

Per ulteriori informazioni e domande frequenti relative all’acquisizione in batch, consulta [Guida alla risoluzione dei problemi di acquisizione in batch](../batch-ingestion/troubleshooting.md).

Per tornare al **[!UICONTROL Attività set di dati]** , fai clic sul nome del set di dati (**[!UICONTROL Dettagli fedeltà]**) nel breadcrumb.

![Panoramica batch](../images/tutorials/ingest-batch-data/batch-details.png)

## Anteprima set di dati

Quando il set di dati è pronto, è disponibile un’opzione per **[!UICONTROL Anteprima set di dati]** viene visualizzato nella parte superiore del **[!UICONTROL Attività set di dati]** scheda.

Clic **[!UICONTROL Anteprima set di dati]** per aprire una finestra di dialogo che mostra dati di esempio dall’interno del set di dati. Se il set di dati è stato creato utilizzando uno schema, i dettagli dello schema del set di dati verranno visualizzati sul lato sinistro dell’anteprima. Puoi espandere lo schema utilizzando le frecce per visualizzare la struttura dello schema. Ogni intestazione di colonna nei dati di anteprima rappresenta un campo nel set di dati.

![Dettagli del set di dati](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Passaggi successivi e risorse aggiuntive

Ora che hai creato un set di dati e hai acquisito correttamente i dati in [!DNL Experience Platform], puoi ripetere questi passaggi per creare un nuovo set di dati o acquisire più dati nel set di dati esistente.

Per ulteriori informazioni sull’acquisizione batch, leggi [Panoramica sull’acquisizione in batch](../batch-ingestion/overview.md) e completa il tuo apprendimento guardando il video seguente.

>[!WARNING]
>
>Il [!DNL Platform] L’interfaccia utente mostrata nel video seguente non è aggiornata. Per le schermate e le funzionalità più recenti dell’interfaccia utente, consulta la documentazione precedente.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
