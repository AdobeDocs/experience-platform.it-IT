---
title: Trasmetti dati dal database del Snowflake all’Experience Platform utilizzando l’interfaccia utente
type: Tutorial
description: Scopri come inviare dati dal database Snwoflake all’Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
source-git-commit: c80535cbb5dda55f1cf145f9f40bbcd40c78e63e
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 3%

---

# Trasmetti dati dal tuo [!DNL Snowflake] database da Experience Platform tramite l’interfaccia utente

Scopri come utilizzare l’interfaccia utente per inviare dati dal tuo [!DNL Snowflake] da database a Adobe Experience Platform seguendo questa guida.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Autenticazione

Leggi la guida su [impostazione prerequisiti per [!DNL Snowflake] dati in streaming](../../../../connectors/databases/snowflake-streaming.md) per informazioni sui passaggi da completare prima di acquisire i dati in streaming da [!DNL Snowflake] all&#39;Experience Platform.

## Utilizza il [!DNL Snowflake Streaming] origine in streaming [!DNL Snowflake] dati da Experience Platform

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto *Database* categoria, seleziona **[!DNL Snowflake Streaming]** e quindi selezionare **[!UICONTROL Aggiungi dati]**.

>[!TIP]
>
>Le origini che non dispongono di un account autenticato nel catalogo delle origini visualizzano **[!UICONTROL Configurazione]** opzione. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Il catalogo delle sorgenti nell’interfaccia utente di Experienci Platform, con la scheda sorgente Streaming di Snowflake selezionata.](../../../../images/tutorials/create/snowflake-streaming/catalog.png)

Il **[!UICONTROL Connetti account di streaming di Snowflake]** viene visualizzata. In questa pagina è possibile utilizzare credenziali nuove o esistenti.

>[!BEGINTABS]

>[!TAB Crea un nuovo account]

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e fornisci un nome, una descrizione facoltativa e le tue credenziali.

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![La nuova interfaccia di creazione account del flusso di lavoro sorgenti.](../../../../images/tutorials/create/snowflake-streaming/new.png)

| Credenziali | Descrizione |
| --- | --- |
| Account | Il nome del tuo [!DNL Snowflake] account. |
| Data warehouse | Il nome del tuo [!DNL Snowflake] data warehouse. I data warehouse gestiscono l’esecuzione delle query in [!DNL Snowflake]. Ogni [!DNL Snowflake] warehouse è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente per portare i dati all&#39;Experience Platform. |
| Database | Il nome del tuo [!DNL Snowflake] database. Il database contiene i dati da portare all&#39;Experience Platform. |
| Schema | (Facoltativo) Lo schema di database associato al tuo [!DNL Snowflake] account. |
| Nome utente | Il nome utente del [!DNL Snowflake] account. |
| Password | La password per [!DNL Snowflake] account. |
| Ruolo | (Facoltativo) Ruolo personalizzato che può essere fornito a un utente per una determinata connessione. Se non specificato, il valore predefinito è `public`. |

Per ulteriori informazioni sulla creazione dell’account, consulta la sezione su [configurazione delle impostazioni dei ruoli](../../../../connectors/databases/snowflake-streaming.md#configure-role-settings) nel [!DNL Snowflake Streaming] panoramica.

>[!TAB Usa un account esistente]

Per utilizzare un account esistente, seleziona **[!UICONTROL Account esistente]** quindi selezionare l&#39;account desiderato dal catalogo account esistente.

Seleziona **[!UICONTROL Avanti]** per procedere.

![Pagina di selezione account esistente del catalogo delle origini.](../../../../images/tutorials/create/snowflake-streaming/existing.png)

>[!ENDTABS]

## Selezionare i dati {#select-data}

>[!IMPORTANT]
>
>Per poter creare un flusso di dati in streaming, nella tabella sorgente deve esistere una colonna di marca temporale. La marca temporale è necessaria ad Experience Platform per sapere quando verranno acquisiti i dati e quando verranno inviati in streaming i dati incrementali. Puoi aggiungere retroattivamente una colonna timestamp per una connessione esistente e creare un nuovo flusso di dati.

Il [!UICONTROL Seleziona dati] viene visualizzato il passaggio. In questo passaggio, devi selezionare i dati da importare in Experienci Platform, configurare marche temporali e fusi orari e fornire un file di dati sorgente di esempio per l’acquisizione di dati non elaborati.

Utilizzare la directory del database a sinistra dello schermo e selezionare la tabella che si desidera importare in Experienci Platform.

![Interfaccia di selezione dei dati con una tabella di database selezionata.](../../../../images/tutorials/create/snowflake-streaming/select-table.png)

Quindi, seleziona il tipo di colonna timestamp della tabella. Puoi scegliere tra due tipi di colonne di marca temporale: `TIMESTAMP_NTZ` o  `TIMESTAMP_LTZ`. Se si seleziona un tipo di colonna `TIMESTAMP_NTZ`, è necessario specificare anche un fuso orario. Le colonne devono avere un vincolo non null. Per ulteriori informazioni, consulta la sezione su [limitazioni e domande frequenti]

In questo passaggio puoi anche configurare le impostazioni di retrocompilazione. La retrocompilazione determina quali dati vengono inizialmente acquisiti. Se la retrocompilazione è abilitata, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima acquisizione pianificata. In caso contrario, verranno acquisiti solo i file caricati tra la prima esecuzione dell’acquisizione e l’ora di inizio. I file caricati prima dell’ora di inizio non verranno acquisiti.

Seleziona la **[!UICONTROL Backfill]** attiva per abilitare la retrocompilazione.

![I passaggi di configurazione per marca temporale, fuso orario e backfill.](../../../../images/tutorials/create/snowflake-streaming/timezone.png)

Infine, seleziona **[!UICONTROL Scegli file]** per caricare un esempio di dati sorgente per creare il set di mappatura, che verrà utilizzato in un passaggio successivo per mappare i dati originali su Experience Data Model (XDM).

Al termine, seleziona **[!UICONTROL Successivo]** per procedere.

![Anteprima dei dati di esempio di origine.](../../../../images/tutorials/create/snowflake-streaming/preview.png)

## Fornisci i dettagli del set di dati e del flusso di dati {#provide-dataset-and-dataflow-details}

Quindi, devi fornire informazioni sul set di dati e sul flusso di dati.

### Dettagli del set di dati {#dataset-details}

Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). I dati acquisiti correttamente in Experienci Platform vengono memorizzati nel data lake come set di dati. Durante questo passaggio, puoi creare un nuovo set di dati o utilizzare un set di dati esistente.

>[!BEGINTABS]

>[!TAB Utilizza un nuovo set di dati]

Per utilizzare un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]**, quindi specifica un nome e una descrizione facoltativa per il set di dati. Devi anche selezionare uno schema Experience Data Model (XDM) a cui aderisce il set di dati.

![La nuova interfaccia per la selezione dei set di dati.](../../../../images/tutorials/create/snowflake-streaming/new-dataset.png)

| Dettagli nuovo set di dati | Descrizione |
| --- | --- |
| Nome set di dati di output | Nome del nuovo set di dati. |
| Descrizione | (Facoltativo) Breve panoramica del nuovo set di dati. |
| Schema | Elenco a discesa degli schemi esistenti nell’organizzazione. Puoi anche creare uno schema personalizzato prima del processo di configurazione sorgente. Per ulteriori informazioni, consulta la guida su [creazione di uno schema XDM nell’interfaccia utente](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Usa un set di dati esistente]

Se disponi già di un set di dati, seleziona **[!UICONTROL Set di dati esistente]** e quindi utilizzare il **[!UICONTROL Ricerca avanzata]** per visualizzare una finestra di tutti i set di dati dell’organizzazione, inclusi i rispettivi dettagli, ad esempio se sono abilitati per l’acquisizione in Real-Time Customer Profile.

![Interfaccia di selezione del set di dati esistente.](../../../../images/tutorials/create/snowflake-streaming/existing-dataset.png)

>[!ENDTABS]

+++Seleziona per i passaggi per abilitare l’acquisizione del profilo, la diagnostica degli errori e l’acquisizione parziale.

Se il set di dati è abilitato per Real-Time Customer Profile, durante questo passaggio puoi attivare/disattivare **[!UICONTROL Set di dati profilo]** per abilitare i dati per l’acquisizione del profilo. Puoi anche utilizzare questo passaggio per abilitare **[!UICONTROL Diagnostica degli errori]** e **[!UICONTROL Acquisizione parziale]**.

* **[!UICONTROL Diagnostica degli errori]**: Seleziona **[!UICONTROL Diagnostica degli errori]** per indicare all’origine di produrre diagnostica degli errori a cui fare successivamente riferimento durante il monitoraggio dell’attività del set di dati e dello stato del flusso di dati.
* **[!UICONTROL Acquisizione parziale]**: l’acquisizione in batch parziale consente di acquisire dati contenenti errori, fino a una determinata soglia configurabile. Questa funzione consente di acquisire correttamente in Experienci Platform tutti i dati accurati, mentre tutti i dati errati vengono raggruppati separatamente con informazioni sul motivo della validità.

+++

### Dettagli del flusso di dati {#dataflow-details}

Una volta configurato il set di dati, devi quindi fornire dettagli sul flusso di dati, tra cui un nome, una descrizione facoltativa e le configurazioni degli avvisi.

![Il passaggio di configurazione dei dettagli del flusso di dati.](../../../../images/tutorials/create/snowflake-streaming/dataflow-details.png)

| Configurazioni del flusso di dati | Descrizione |
| --- | --- |
| Nome flusso di dati | Nome del flusso di dati.  Per impostazione predefinita, viene utilizzato il nome del file che si sta importando. |
| Descrizione | (Facoltativo) Breve descrizione del flusso di dati. |
| Avvisi | Experienci Platform può generare avvisi basati su eventi a cui gli utenti possono abbonarsi. Queste opzioni richiedono un flusso di dati in esecuzione per attivarle. Per ulteriori informazioni, leggere [panoramica degli avvisi](../../alerts.md) <ul><li>**Inizio esecuzione flusso di dati origini**: seleziona questo avviso per ricevere una notifica all’inizio dell’esecuzione del flusso di dati.</li><li>**Esecuzione flusso di dati origini completata**: seleziona questo avviso per ricevere una notifica se il flusso di dati termina senza errori.</li><li>**Errore di esecuzione del flusso di dati origini**: seleziona questo avviso per ricevere una notifica se l’esecuzione del flusso di dati termina con errori.</li></ul> |

Al termine, seleziona **[!UICONTROL Successivo]** per procedere.

## Mappare i campi su uno schema XDM {#mapping}

Il [!UICONTROL Mappatura] viene visualizzato il passaggio. Utilizza l’interfaccia di mappatura per mappare i dati di origine sui campi dello schema appropriati prima di acquisire tali dati in Experienci Platform, quindi seleziona **[!UICONTROL Successivo]**. Per una guida dettagliata sull’utilizzo dell’interfaccia di mappatura, leggi [Guida dell’interfaccia utente per la preparazione dati](../../../../../data-prep/ui/mapping.md) per ulteriori informazioni.

![Interfaccia di mappatura del flusso di lavoro sorgenti.](../../../../images/tutorials/create/snowflake-streaming/mapping.png)

## Verifica il flusso di dati {#review}

Il passaggio finale nel processo di creazione del flusso di dati consiste nell’esaminare il flusso di dati prima di eseguirlo. Utilizza il **[!UICONTROL Revisione]** per rivedere i dettagli del nuovo flusso di dati prima che venga eseguito. I dettagli sono raggruppati nelle seguenti categorie:

* **Connessione**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e il numero di colonne all’interno di tale file di origine.
* **Assegna set di dati e mappa campi**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui aderisce il set di dati.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un po’ di tempo per creare il flusso di dati.

![Passaggio Revisione del flusso di lavoro origini.](../../../../images/tutorials/create/snowflake-streaming/review.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato un flusso di dati in streaming per [!DNL Snowflake] dati. Per ulteriori risorse, consulta la documentazione di seguito.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni su tassi di acquisizione, successo ed errori. Per ulteriori informazioni su come monitorare i flussi di dati in streaming, consulta l’esercitazione su [monitoraggio dei flussi di dati in streaming nell’interfaccia utente](../../monitor-streaming.md).

### Aggiornare il flusso di dati

Per aggiornare le configurazioni per la pianificazione, la mappatura e le informazioni generali dei flussi di dati, visita il tutorial su [aggiornamento dei flussi di dati di origine nell’interfaccia utente](../../update-dataflows.md).

### Eliminare il flusso di dati

Puoi eliminare i flussi di dati non più necessari o creati in modo errato utilizzando **[!UICONTROL Elimina]** funzione disponibile nella **[!UICONTROL Flussi dati]** Workspace. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l’esercitazione su [eliminazione di flussi di dati nell’interfaccia utente](../../delete.md).