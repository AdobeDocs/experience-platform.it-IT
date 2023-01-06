---
keywords: Experience Platform;home;argomenti popolari;abilitare set di dati;set di dati;set di dati
solution: Experience Platform
title: Guida all’interfaccia utente dei set di dati
description: Scopri come eseguire azioni comuni quando si utilizzano i set di dati nell’interfaccia utente di Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 0%

---

# Guida all’interfaccia utente dei set di dati

Questa guida utente fornisce istruzioni sull’esecuzione delle azioni comuni quando si lavora con i set di dati all’interno dell’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida utente richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Set di dati](overview.md): Il costrutto di archiviazione e gestione per la persistenza dei dati in [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Editor di schema](../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi XDM personalizzati utilizzando [!DNL Schema Editor] all&#39;interno del [!DNL Platform] interfaccia utente.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Assicurati la conformità a normative, restrizioni e criteri sull&#39;utilizzo dei dati dei clienti.

## Visualizzare i set di dati {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="Numeri negativi nell’attività dei set di dati"
>abstract="I numeri negativi nei record acquisiti indicano che un utente ha eliminato alcuni batch in un intervallo di tempo selezionato."
>text="Learn more in documentation"

In [!DNL Experience Platform] Interfaccia utente, seleziona **[!UICONTROL Set di dati]** nella navigazione a sinistra per aprire il **[!UICONTROL Set di dati]** dashboard. Il dashboard elenca tutti i set di dati disponibili per l’organizzazione. Vengono visualizzati i dettagli di ciascun set di dati elencato, compreso il nome, lo schema a cui il set di dati aderisce e lo stato dell’esecuzione di acquisizione più recente.

![Immagine che evidenzia l&#39;elemento Set di dati nella barra di navigazione a sinistra.](../images/datasets/user-guide/browse-datasets.png)

Per impostazione predefinita, vengono visualizzati solo i set di dati in cui sono stati acquisiti. Se desideri visualizzare i set di dati generati dal sistema, abilita la **[!UICONTROL Mostra set di dati di sistema]** alternare. I set di dati generati dal sistema vengono utilizzati solo per elaborare altri componenti. Ad esempio, il set di dati di esportazione del profilo generato dal sistema viene utilizzato per elaborare il dashboard del profilo.

![Viene evidenziata l’opzione che consente di scegliere se visualizzare o meno i set di dati di sistema.](../images/datasets/user-guide/system-datasets.png)

Seleziona il nome di un set di dati per accedere al relativo **[!UICONTROL Attività set di dati]** visualizza i dettagli del set di dati selezionato. La scheda Attività include un grafico che mostra il tasso di utilizzo dei messaggi e un elenco di batch con esito positivo o negativo.

![I dettagli del set di dati selezionato vengono evidenziati.](../images/datasets/user-guide/dataset-activity-1.png)
![Vengono evidenziati i batch di esempio che appartengono al set di dati selezionato.](../images/datasets/user-guide/dataset-activity-2.png)

## Anteprima di un set di dati

Da **[!UICONTROL Attività set di dati]** schermata, seleziona **[!UICONTROL Anteprima set di dati]** nell’angolo in alto a destra dello schermo per visualizzare in anteprima fino a 100 righe di dati. Se il set di dati è vuoto, il collegamento di anteprima verrà disattivato e verrà invece indicato che l’anteprima non è disponibile.

![Il pulsante Anteprima set di dati è evidenziato.](../images/datasets/user-guide/select-preview.png)

Nella finestra di anteprima, la visualizzazione gerarchica dello schema per il set di dati viene visualizzata a destra.

![Viene visualizzata un’anteprima del set di dati. Vengono visualizzate informazioni sulla struttura e sui valori di esempio.](../images/datasets/user-guide/preview-dataset.png)

Per metodi più affidabili per accedere ai dati, [!DNL Experience Platform] fornisce servizi a valle quali [!DNL Query Service] e [!DNL JupyterLab] per esplorare e analizzare i dati. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica del servizio query](../../query-service/home.md)
* [Guida utente di JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Creare un set di dati {#create}

Per creare un nuovo set di dati, inizia selezionando **[!UICONTROL Creare un set di dati]** in **[!UICONTROL Set di dati]** dashboard.

![Il pulsante Crea set di dati è evidenziato.](../images/datasets/user-guide/select-create.png)

Nella schermata successiva, sono disponibili le due opzioni seguenti per la creazione di un nuovo set di dati:

* [Creare un set di dati dallo schema](#schema)
* [Creare un set di dati da file CSV](#csv)

### Creare un set di dati con uno schema esistente {#schema}

In **[!UICONTROL Creare un set di dati]** schermata, seleziona **[!UICONTROL Creare un set di dati dallo schema]** per creare un nuovo set di dati vuoto.

![Il pulsante Crea set di dati dallo schema è evidenziato.](../images/datasets/user-guide/create-dataset-schema.png)

La **[!UICONTROL Seleziona schema]** viene visualizzato il passaggio . Sfoglia l’elenco degli schemi e seleziona lo schema a cui si conformerà il set di dati prima di selezionare **[!UICONTROL Successivo]**.

![Viene visualizzato un elenco di schemi. Lo schema che verrà utilizzato per creare il set di dati viene evidenziato.](../images/datasets/user-guide/select-schema.png)

La **[!UICONTROL Configurare il set di dati]** viene visualizzato il passaggio . Fornisci il set di dati con un nome e una descrizione facoltativa, quindi seleziona **[!UICONTROL Fine]** per creare il set di dati.

![Vengono inseriti i dettagli di configurazione del set di dati. Ciò include dettagli quali il nome e la descrizione del set di dati.](../images/datasets/user-guide/configure-dataset-schema.png)

### Creare un set di dati con un file CSV {#csv}

Quando un set di dati viene creato utilizzando un file CSV, viene creato uno schema ad hoc per fornire al set di dati una struttura corrispondente al file CSV fornito. In **[!UICONTROL Creare un set di dati]** schermata, seleziona **[!UICONTROL Creare un set di dati da file CSV]**.

![Il pulsante Crea set di dati da file CSV è evidenziato.](../images/datasets/user-guide/create-dataset-csv.png)

La **[!UICONTROL Configura]** viene visualizzato il passaggio . Fornisci il set di dati con un nome e una descrizione facoltativa, quindi seleziona **[!UICONTROL Successivo]**.

![Vengono inseriti i dettagli di configurazione del set di dati. Ciò include dettagli quali il nome e la descrizione del set di dati.](../images/datasets/user-guide/configure-dataset-csv.png)

La **[!UICONTROL Aggiungi dati]** viene visualizzato il passaggio . Carica il file CSV trascinandolo e rilasciandolo al centro dello schermo, oppure seleziona **[!UICONTROL Sfoglia]** per esplorare la directory dei file. Le dimensioni del file possono essere fino a dieci gigabyte. Una volta caricato il file CSV, seleziona **[!UICONTROL Salva]** per creare il set di dati.

>[!NOTE]
>
>I nomi delle colonne CSV devono iniziare con caratteri alfanumerici e possono contenere solo lettere, numeri e caratteri di sottolineatura.

![Viene visualizzata la schermata Aggiungi dati. Viene evidenziata la posizione in cui puoi caricare il file CSV per il set di dati.](../images/datasets/user-guide/add-csv-data.png)

## Abilitare un set di dati per il profilo cliente in tempo reale {#enable-profile}

Ogni set di dati è in grado di arricchire i profili dei clienti con i relativi dati acquisiti. A tal fine, lo schema a cui aderisce il set di dati deve essere compatibile per l’utilizzo in [!DNL Real-Time Customer Profile]. Uno schema compatibile soddisfa i seguenti requisiti:

* Lo schema ha almeno un attributo specificato come proprietà Identity.
* Lo schema presenta una proprietà Identity definita come identità principale.

Per ulteriori informazioni sull&#39;abilitazione di uno schema per [!DNL Profile], vedi [Guida utente dell’Editor di schema](../../xdm/tutorials/create-schema-ui.md).

Per abilitare un set di dati per il profilo, accedi al relativo **[!UICONTROL Attività set di dati]** e seleziona la **[!UICONTROL Profilo]** all&#39;interno di **[!UICONTROL Proprietà]** colonna. Una volta attivato, i dati acquisiti nel set di dati verranno utilizzati anche per popolare i profili dei clienti.

>[!NOTE]
>
>Se un set di dati contiene già dati e viene quindi abilitato per [!DNL Profile], i dati esistenti non vengono utilizzati automaticamente da [!DNL Profile]. Dopo che un set di dati è abilitato per [!DNL Profile], ti consigliamo di riacquisire eventuali dati esistenti per contribuire ai profili dei clienti.

![L’opzione Profilo viene evidenziata nella pagina dei dettagli del set di dati.](../images/datasets/user-guide/enable-dataset-profiles.png)

## Gestire e applicare la governance dei dati su un set di dati

Le etichette di utilizzo dei dati ti consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. Consulta la sezione [Panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni sulle etichette, o fai riferimento alla sezione [guida utente delle etichette per l’utilizzo dei dati](../../data-governance/labels/overview.md) per istruzioni su come applicare le etichette ai set di dati.

## Eliminare un set di dati {#delete}

È possibile eliminare un set di dati accedendo per primo ai relativi **[!UICONTROL Attività set di dati]** schermo. Quindi, seleziona **[!UICONTROL Elimina set di dati]** per eliminarlo.

>[!NOTE]
>
>Set di dati creati e utilizzati da applicazioni e servizi Adobe (ad esempio Adobe Analytics, Adobe Audience Manager o [!DNL Offer Decisioning]) non può essere eliminata.

![Il pulsante Elimina set di dati è evidenziato nella pagina dei dettagli del set di dati.](../images/datasets/user-guide/delete-dataset.png)

Viene visualizzata una casella di conferma. Seleziona **[!UICONTROL Elimina]** per confermare l’eliminazione del set di dati.

![Viene visualizzata la finestra modale di conferma per l’eliminazione, con il pulsante Elimina evidenziato.](../images/datasets/user-guide/confirm-delete.png)

## Eliminare un set di dati abilitato per il profilo

Se un set di dati è abilitato per Profilo, l’eliminazione di tale set di dati tramite l’interfaccia utente lo elimina dal data lake, dal servizio Identity e dall’archivio profili in Platform.

È possibile eliminare un set di dati da [!DNL Profile] memorizza solo (lasciando i dati nel Data Lake) utilizzando l’API del profilo cliente in tempo reale. Per ulteriori informazioni, consulta la sezione [guida all’endpoint API per i processi di sistema dei profili](../../profile/api/profile-system-jobs.md).

## Monitoraggio dell’acquisizione di dati

In [!DNL Experience Platform] Interfaccia utente, seleziona **[!UICONTROL Monitoraggio]** nella navigazione a sinistra. La **[!UICONTROL Monitoraggio]** dashboard ti consente di visualizzare gli stati dei dati in entrata da un’acquisizione batch o in streaming. Per visualizzare lo stato dei singoli batch, selezionare una delle seguenti opzioni **[!UICONTROL Fine-end batch]** o **[!UICONTROL Streaming end-to-end]**. Nelle dashboard sono elencate tutte le esecuzioni di batch o streaming ingestion, incluse quelle che hanno esito positivo, non sono riuscite o sono ancora in corso. Ogni elenco fornisce i dettagli del batch, compreso l’ID batch, il nome del set di dati di destinazione e il numero di record acquisiti. Se il set di dati di destinazione è abilitato per [!DNL Profile], viene visualizzato anche il numero di record di identità e profilo acquisiti.

![Viene visualizzata la schermata end-to-end del batch di monitoraggio. Vengono evidenziati sia il monitoraggio che il batch-to-batch.](../images/datasets/user-guide/batch-listing.png)

Puoi selezionare una persona **[!UICONTROL ID batch]** per accedere al **[!UICONTROL Panoramica batch]** dashboard e visualizza i dettagli del batch, compresi i registri di errore in caso di errore durante l&#39;acquisizione del batch.

![Vengono visualizzati i dettagli del batch selezionato. Ciò include il numero di record acquisiti, il numero di record non riusciti, lo stato del batch, la dimensione del file, l’ora di inizio e fine dell’acquisizione, il set di dati e gli ID batch, l’ID organizzazione, il nome del set di dati e le informazioni di accesso.](../images/datasets/user-guide/batch-overview.png)

Se si desidera eliminare il batch, è possibile farlo selezionando **[!UICONTROL Elimina batch]** trovato in alto a destra del dashboard. In questo modo verranno rimossi anche i record dal set di dati a cui è stato originariamente acquisito il batch.

![Il pulsante Elimina batch viene evidenziato nella pagina dei dettagli del set di dati.](../images/datasets/user-guide/delete-batch.png)

## Passaggi successivi

Questa guida utente fornisce istruzioni per l’esecuzione delle azioni comuni quando si lavora con i set di dati in [!DNL Experience Platform] interfaccia utente. Per i passaggi relativi all’esecuzione di operazioni comuni [!DNL Platform] flussi di lavoro che coinvolgono set di dati, consulta le seguenti esercitazioni:

* [Creare un set di dati utilizzando le API](create.md)
* [Dati del set di dati di query tramite API di accesso ai dati](../../data-access/home.md)
* [Configurare un set di dati per il profilo cliente in tempo reale e il servizio Identity utilizzando le API](../../profile/tutorials/dataset-configuration.md)
