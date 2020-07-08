---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Assimilazione di dati in  Adobe Experience Platform
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 0%

---


# Assimilazione di dati in  Adobe Experience Platform

 Adobe Experience Platform consente di importare facilmente i dati in Platform come file batch. Esempi di dati da assimilare possono includere dati di profilo da un file semplice in un sistema CRM (ad esempio un file parquet) o dati conformi a uno schema XDM (Experience Data Model) noto nel Registro di sistema dello schema.

## Introduzione

Per completare questa esercitazione, è necessario avere accesso a  Experience Platform. Se non disponete dell&#39;accesso a un&#39;organizzazione IMS in  Experience Platform, rivolgetevi al vostro amministratore di sistema prima di procedere.

Se preferite assimilare i dati utilizzando le API di inserimento dati, iniziate leggendo la guida [per gli sviluppatori di](../batch-ingestion/api-overview.md)inserimento batch.

## Area di lavoro DataSet

L&#39;area di lavoro Set di dati in  Experience Platform consente di visualizzare e gestire tutti i set di dati creati dall&#39;organizzazione IMS e di crearne di nuovi.

Visualizzare l&#39;area di lavoro Set di dati facendo clic su Set di **dati** nella barra di navigazione a sinistra. L&#39;area di lavoro Set di dati contiene un elenco di set di dati, tra cui colonne che mostrano _Nome_, _Creato_ (data e ora), _Origine_, _Schema_ e Stato ____ ultimo batch, nonché la data e l&#39;ora dell&#39;ultimo aggiornamento del set di dati.

>[!NOTE]
>
>Fate clic sull&#39;icona del filtro accanto alla barra di ricerca per utilizzare le funzionalità di filtro per visualizzare solo i set di dati abilitati per il profilo.

![Visualizza tutti i set di dati](../images/tutorials/ingest-batch-data/datasets_workspace.png)

## Creare un dataset

Per creare un set di dati, fare clic su **Crea set** di dati nell&#39;angolo superiore destro dell&#39;area di lavoro Set di dati.

Nella schermata **Crea set** di dati, selezionate se desiderate &quot;Crea set di dati dallo schema&quot; o &quot;Crea set di dati dal file CSV&quot;.

Per questa esercitazione, verrà utilizzato uno schema per creare il dataset. Fare clic su **Crea set di dati dallo schema** per continuare.

![Seleziona origine dati](../images/tutorials/ingest-batch-data/create_dataset.png)

## Seleziona schema set di dati

Nella schermata **Seleziona schema** , scegliere uno schema facendo clic sul pulsante di scelta accanto allo schema da utilizzare. Per questa esercitazione, il dataset verrà creato utilizzando lo schema Membri fedeltà. L&#39;utilizzo della barra di ricerca per filtrare gli schemi è un modo utile per individuare lo schema esatto che si sta cercando.

Dopo aver selezionato il pulsante di scelta accanto allo schema da utilizzare, fare clic su **Avanti**.

![Seleziona schema](../images/tutorials/ingest-batch-data/select_schema.png)

## Configura set di dati

Nella schermata **Configura set** di dati, verrà richiesto di assegnare al set di dati un **nome** e anche una **descrizione** del set di dati.

**Note sui nomi dei set di dati:**

- I nomi dei set di dati devono essere brevi e descrittivi in modo che il set di dati possa essere facilmente trovato nella libreria in un secondo momento.
- I nomi dei set di dati devono essere univoci, il che significa che devono essere sufficientemente specifici da non essere riutilizzati in futuro.
- È consigliabile fornire informazioni aggiuntive sul set di dati utilizzando il campo di descrizione, in quanto potrebbe aiutare altri utenti a distinguere tra set di dati in futuro.

Una volta che il dataset ha un nome e una descrizione, fare clic su **Fine**.

![Configura set di dati](../images/tutorials/ingest-batch-data/configure_dataset.png)

## Attività DataSet

È stato creato un set di dati vuoto e l&#39;utente è stato riportato nella scheda Attività **** DataSet nell&#39;area di lavoro Set di dati. Il nome del set di dati deve essere visualizzato nell’angolo in alto a sinistra dell’area di lavoro, insieme alla notifica che &quot;Non sono stati aggiunti batch&quot;. Questo è previsto perché non avete ancora aggiunto alcun batch a questo set di dati.

Sul lato destro dell&#39;area di lavoro Set di dati viene visualizzata la scheda **Informazioni** contenente informazioni relative al nuovo set di dati, quali ID _set di dati,_ Nome _,_ Descrizione _, Nome__tabella, NomeSchema_______, , Streaminge Sorgente. La scheda Informazioni include anche informazioni su quando il set di dati è stato _creato_ e sulla data dell&#39; _ultima modifica_ .

Nella scheda Informazioni è inoltre disponibile un interruttore _Profilo_ che consente di abilitare il dataset per l&#39;uso con il profilo cliente in tempo reale. L&#39;utilizzo di questa attivazione e il profilo cliente in tempo reale verranno spiegati più dettagliatamente nella sezione che segue.

![Attività DataSet](../images/tutorials/ingest-batch-data/dataset_activity.png)

## Abilita dataset per profilo cliente in tempo reale

I set di dati vengono utilizzati per l&#39;assimilazione di dati in  Experience Platform e i dati vengono utilizzati per identificare individui e unire insieme informazioni provenienti da più origini. Le informazioni unite sono denominate profilo cliente in tempo reale. Affinché Platform sappia quali informazioni includere nel profilo in tempo reale, i set di dati possono essere contrassegnati per l’inclusione tramite l’attivazione/disattivazione **Profilo** .

Per impostazione predefinita, questa opzione è disattivata. Se scegliete di attivare o disattivare il profilo, tutti i dati inseriti nel set di dati verranno utilizzati per identificare un singolo utente e unire il profilo in tempo reale.

Per ulteriori informazioni sul profilo cliente in tempo reale e per utilizzare le identità, consulta la documentazione del servizio [](../../identity-service/home.md) identità.

Per abilitare il set di dati per il profilo cliente in tempo reale, fai clic sul **profilo** nella scheda **Informazioni** .

![Attiva/disattiva profilo](../images/tutorials/ingest-batch-data/enable_dataset_unified_profile.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di confermare che si desidera abilitare il dataset per il profilo cliente in tempo reale.

![Abilita profilo, finestra di dialogo](../images/tutorials/ingest-batch-data/confirm_dataset_enable.png)

Fate clic su **Abilita** e l’interruttore diventa blu, a indicare che è attivato.

![Abilitato per profilo](../images/tutorials/ingest-batch-data/dataset_enabled.png)

## Aggiungere dati al dataset

I dati possono essere aggiunti in un set di dati in diversi modi. Puoi scegliere di utilizzare le API di inserimento dati o un partner ETL come Unifi o Informatica. Per questa esercitazione, i dati verranno aggiunti al dataset utilizzando la scheda **Aggiungi dati** all&#39;interno dell&#39;interfaccia utente.

Per iniziare ad aggiungere dati al dataset, fare clic sulla scheda **Aggiungi dati** . È ora possibile trascinare e rilasciare i file o cercare nel computer i file da aggiungere.

>[!NOTE]
>
>Platform supporta due tipi di file per l’assimilazione dei dati, parquet o JSON. È possibile aggiungere fino a cinque file alla volta, con una dimensione massima di file pari a 10 GB.

![Aggiungi dati, scheda](../images/tutorials/ingest-batch-data/add_data.png)

## Caricare un file

Dopo aver trascinato e rilasciato (o sfogliato e selezionato) un file parquet o JSON da caricare, Platform inizierà immediatamente a elaborare il file e nella scheda **Aggiungi dati** verrà visualizzata una finestra di dialogo di **** caricamento che mostra l’avanzamento del caricamento del file.

![Finestra di dialogo di caricamento](../images/tutorials/ingest-batch-data/uploading.png)

## Metriche DataSet

Al termine del caricamento del file, nella scheda Attività **** DataSet non viene più visualizzato &quot;Nessun batch aggiunto&quot;. Al contrario, la scheda Attività DataSet ora mostra le metriche DataSet. Tutte le metriche mostreranno &quot;0&quot; in questa fase perché il batch non è ancora caricato.

Nella parte inferiore della scheda è presente un elenco che mostra l&#39;ID __ batch dei dati appena acquisiti tramite il processo [&quot;Aggiungi dati a dataset&quot;](#add-data-to-dataset) . Sono incluse anche le informazioni relative al batch, inclusa la data _di inserimento_ , il numero di _record inseriti_ e lo _stato_ del batch corrente.

![Metriche DataSet](../images/tutorials/ingest-batch-data/batch_loading.png)

## Dettagli batch

Fare clic sull&#39;ID __ batch per visualizzare una panoramica **** batch, con dettagli aggiuntivi relativi al batch. Al termine del caricamento del batch, le informazioni relative al batch verranno aggiornate per mostrare il numero di _record inseriti_ e le dimensioni _del_ file. Lo _Stato_ viene modificato in &quot;Success&quot; o &quot;Failed&quot; (Operazione completata). Se il batch non riesce, la sezione Codice _di_ errore conterrà i dettagli relativi a eventuali errori durante l&#39;assimilazione.

Per ulteriori informazioni e domande frequenti sull’inserimento di batch, consulta la guida [alla risoluzione dei problemi di inserimento](../batch-ingestion/troubleshooting.md)batch.

Per tornare alla schermata Attività **** DataSet, fare clic sul nome del set di dati (_Dettagli_ fedeltà) nella breadcrumb.

![Panoramica batch](../images/tutorials/ingest-batch-data/batch_overview.png)

## Anteprima set di dati

Una volta pronto il set di dati, nella parte superiore della scheda Attività **set di dati viene visualizzata l&#39;opzione** Anteprima set **** di dati.

Fare clic su **Anteprima set** di dati per aprire una finestra di dialogo che mostra i dati di esempio dall&#39;interno del set di dati. Se il set di dati è stato creato utilizzando uno schema, i dettagli per lo schema del set di dati verranno visualizzati sul lato sinistro dell&#39;anteprima. È possibile espandere lo schema utilizzando le frecce per visualizzare la struttura dello schema. Ogni intestazione di colonna nei dati di anteprima rappresenta un campo nel dataset.

![Dettagli del set di dati](../images/tutorials/ingest-batch-data/dataset_details.png)

## Passaggi successivi

Dopo aver creato un set di dati e aver correttamente inserito i dati in  Experience Platform, è possibile ripetere questa procedura per creare un nuovo set di dati o per assimilare più dati nel set di dati esistente.

Per ulteriori informazioni sull&#39;inserimento batch, consulta la panoramica [sull&#39;inserimento](../batch-ingestion/overview.md)batch.
