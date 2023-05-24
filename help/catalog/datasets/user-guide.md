---
keywords: Experience Platform;home;argomenti comuni;abilitare set di dati;set di dati;dataset;dataset;home;popular topic;enable dataset;Dataset;dataset
solution: Experience Platform
title: Guida dell’interfaccia utente dei set di dati
description: Scopri come eseguire azioni comuni quando si lavora con i set di dati nell’interfaccia utente di Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: f0cd059683531993398f0a81d6eda486276853e2
workflow-type: tm+mt
source-wordcount: '1485'
ht-degree: 7%

---

# Guida all’interfaccia utente dei set di dati

Questa guida utente fornisce istruzioni su come eseguire azioni comuni quando si lavora con set di dati nell’interfaccia utente di Adobe Experience Platform.

## Introduzione

La presente guida utente richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Set di dati](overview.md): costrutto di archiviazione e gestione per la persistenza dei dati in [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Editor schema](../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi XDM personalizzati utilizzando [!DNL Schema Editor] all&#39;interno del [!DNL Platform] dell&#39;utente.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): assicurati la conformità a normative, restrizioni e criteri relativi all’utilizzo dei dati dei clienti.

## Visualizzare i set di dati {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="Numeri negativi nelle attività sui set di dati"
>abstract="I numeri negativi nei record acquisiti indicano che un utente ha eliminato alcuni batch in un intervallo di tempo selezionato."
>text="Learn more in documentation"

In [!DNL Experience Platform] UI, seleziona **[!UICONTROL Set di dati]** nel menu di navigazione a sinistra per aprire **[!UICONTROL Set di dati]** dashboard. Il dashboard elenca tutti i set di dati disponibili per l’organizzazione. Vengono visualizzati i dettagli di ciascun set di dati elencato, compreso il nome, lo schema a cui il set di dati aderisce e lo stato dell’esecuzione di acquisizione più recente.

![Immagine che evidenzia l’elemento Set di dati nella barra di navigazione a sinistra.](../images/datasets/user-guide/browse-datasets.png)

Per impostazione predefinita, vengono visualizzati solo i set di dati che hai acquisito. Se desideri visualizzare i set di dati generati dal sistema, abilita **[!UICONTROL Mostra set di dati di sistema]** attivare/disattivare. I set di dati generati dal sistema vengono utilizzati solo per elaborare altri componenti. Ad esempio, il set di dati di esportazione del profilo generato dal sistema viene utilizzato per elaborare il dashboard del profilo.

![Viene evidenziato l’interruttore che consente di scegliere se visualizzare o meno i set di dati di sistema.](../images/datasets/user-guide/system-datasets.png)

Seleziona il nome di un set di dati per accedere ai relativi **[!UICONTROL Attività set di dati]** e visualizzare i dettagli del set di dati selezionato. La scheda attività include un grafico che mostra il tasso di utilizzo dei messaggi e un elenco di batch con esito positivo o negativo.

![Vengono evidenziati i dettagli del set di dati selezionato.](../images/datasets/user-guide/dataset-activity-1.png)
![I batch di esempio che appartengono al set di dati selezionato vengono evidenziati.](../images/datasets/user-guide/dataset-activity-2.png)

## Visualizzare in anteprima un set di dati

Dalla sezione **[!UICONTROL Attività set di dati]** schermata, seleziona **[!UICONTROL Anteprima set di dati]** nell’angolo in alto a destra dello schermo per visualizzare in anteprima fino a 100 righe di dati. Se il set di dati è vuoto, il collegamento di anteprima viene disattivato e indica invece che l’anteprima non è disponibile.

![Viene evidenziato il pulsante Anteprima set di dati.](../images/datasets/user-guide/select-preview.png)

Nella finestra di anteprima, a destra viene visualizzata la vista gerarchica dello schema per il set di dati.

![Viene visualizzata un’anteprima del set di dati. Vengono visualizzate informazioni sulla struttura, nonché valori campione.](../images/datasets/user-guide/preview-dataset.png)

Per metodi più affidabili per accedere ai dati, [!DNL Experience Platform] fornisce servizi a valle come [!DNL Query Service] e [!DNL JupyterLab] per esplorare e analizzare i dati. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica di Query Service](../../query-service/home.md)
* [Guida utente di JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Creare un set di dati {#create}

Per creare un nuovo set di dati, inizia selezionando **[!UICONTROL Creare un set di dati]** nella dashboard del set di dati.****

![Viene evidenziato il pulsante Crea set di dati.](../images/datasets/user-guide/select-create.png)

Nella schermata successiva vengono presentate le due opzioni seguenti per la creazione di un nuovo set di dati:

* [Creare un set di dati da uno schema](#schema)
* [Crea set di dati da file CSV](#csv)

### Creare un set di dati con uno schema esistente {#schema}

In **[!UICONTROL Crea set di dati]** schermata, seleziona **[!UICONTROL Crea set di dati dallo schema]** per creare un nuovo set di dati vuoto.

![Viene evidenziato il pulsante Crea set di dati da schema.](../images/datasets/user-guide/create-dataset-schema.png)

Il **[!UICONTROL Seleziona schema]** viene visualizzato il passaggio. Sfoglia l’elenco degli schemi e seleziona lo schema a cui il set di dati aderirà prima di selezionare **[!UICONTROL Successivo]**.

![Viene visualizzato un elenco di schemi. Viene evidenziato lo schema che verrà utilizzato per creare il set di dati.](../images/datasets/user-guide/select-schema.png)

Il **[!UICONTROL Configurare il set di dati]** viene visualizzato il passaggio. Fornisci al set di dati un nome e una descrizione facoltativa, quindi seleziona **[!UICONTROL Fine]** per creare il set di dati.

![Vengono inseriti i dettagli di configurazione del set di dati. Ciò include dettagli quali il nome e la descrizione del set di dati.](../images/datasets/user-guide/configure-dataset-schema.png)

### Creare un set di dati con un file CSV {#csv}

Quando un set di dati viene creato utilizzando un file CSV, viene creato uno schema ad hoc per fornire al set di dati una struttura che corrisponda al file CSV fornito. In **[!UICONTROL Crea set di dati]** schermata, seleziona **[!UICONTROL Crea set di dati da file CSV]**.

![Il pulsante Crea set di dati da file CSV è evidenziato.](../images/datasets/user-guide/create-dataset-csv.png)

Il **[!UICONTROL Configura]** viene visualizzato il passaggio. Fornisci al set di dati un nome e una descrizione facoltativa, quindi seleziona **[!UICONTROL Successivo]**.

![Vengono inseriti i dettagli di configurazione del set di dati. Ciò include dettagli quali il nome e la descrizione del set di dati.](../images/datasets/user-guide/configure-dataset-csv.png)

Il **[!UICONTROL Aggiungi dati]** viene visualizzato il passaggio. Carica il file CSV trascinandolo e rilasciandolo al centro dello schermo, oppure seleziona **[!UICONTROL Sfoglia]** per esplorare la directory dei file. Le dimensioni del file non possono superare i dieci GB. Una volta caricato il file CSV, seleziona **[!UICONTROL Salva]** per creare il set di dati.

>[!NOTE]
>
>I nomi delle colonne CSV devono iniziare con caratteri alfanumerici e possono contenere solo lettere, numeri e trattini bassi.

![Viene visualizzata la schermata Aggiungi dati. Viene evidenziato il percorso in cui puoi caricare il file CSV del set di dati.](../images/datasets/user-guide/add-csv-data.png)

## Abilitare un set di dati per Real-Time Customer Profile {#enable-profile}

Ogni set di dati ha la capacità di arricchire i profili dei clienti con i dati acquisiti. A questo scopo, lo schema a cui aderisce il set di dati deve essere compatibile per l’utilizzo in [!DNL Real-Time Customer Profile]. Uno schema compatibile soddisfa i seguenti requisiti:

* Lo schema ha almeno un attributo specificato come proprietà di identità.
* Lo schema ha una proprietà di identità definita come identità primaria.

Per ulteriori informazioni sull’abilitazione di uno schema per [!DNL Profile], vedere [Guida utente dell’Editor di schema](../../xdm/tutorials/create-schema-ui.md).

Per abilitare un set di dati per il profilo, accedi ai relativi **[!UICONTROL Attività set di dati]** e seleziona la **[!UICONTROL Profilo]** attivare/disattivare all&#39;interno di **[!UICONTROL Proprietà]** colonna. Una volta abilitata, anche i dati acquisiti nel set di dati verranno utilizzati per popolare i profili dei clienti.

>[!NOTE]
>
>Se un set di dati contiene già dati ed è quindi abilitato per [!DNL Profile], i dati esistenti non vengono utilizzati automaticamente da [!DNL Profile]. Dopo aver abilitato un set di dati per [!DNL Profile], si consiglia di riacquisire tutti i dati esistenti per farli contribuire ai profili dei clienti.

![L’opzione Profilo è evidenziata all’interno della pagina dei dettagli del set di dati.](../images/datasets/user-guide/enable-dataset-profiles.png)

## Gestire e applicare la governance dei dati su un set di dati {#manage-and-enforce-data-governance}

Le etichette di utilizzo dei dati, applicate a livello di schema, ti consentono di categorizzare set di dati e campi in base ai criteri di utilizzo applicabili a tali dati. Consulta la [Panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni sulle etichette o fare riferimento a [guida utente delle etichette di utilizzo dati](../../data-governance/labels/overview.md) per istruzioni su come applicare etichette agli schemi per la propagazione ai set di dati.

## Eliminare un set di dati {#delete}

Per eliminare un set di dati, devi prima accedere ai relativi **[!UICONTROL Attività set di dati]** schermo. Quindi, seleziona **[!UICONTROL Elimina set di dati]** per eliminarlo.

>[!NOTE]
>
>Set di dati creati e utilizzati dalle applicazioni e dai servizi Adobe (ad esempio Adobe Analytics, Adobe Audience Manager o [!DNL Offer Decisioning]) non può essere eliminato.

![Il pulsante Elimina set di dati è evidenziato nella pagina dei dettagli del set di dati.](../images/datasets/user-guide/delete-dataset.png)

Viene visualizzata una casella di conferma. Seleziona **[!UICONTROL Elimina]** per confermare l’eliminazione del set di dati.

![Viene visualizzata la finestra modale di conferma per l’eliminazione, con il pulsante Elimina evidenziato.](../images/datasets/user-guide/confirm-delete.png)

## Eliminare un set di dati abilitato per il profilo

Se un set di dati è abilitato per il profilo, eliminandolo tramite l’interfaccia utente verrà eliminato dal data lake, da Identity Service e dall’archivio profili in Platform.

Puoi eliminare un set di dati da [!DNL Profile] archivia solo (lasciando i dati nel Data Lake) utilizzando l’API Real-Time Customer Profile. Per ulteriori informazioni, vedere [guida dell’endpoint API dei processi di sistema del profilo](../../profile/api/profile-system-jobs.md).

## Monitoraggio dell’acquisizione di dati

In [!DNL Experience Platform] UI, seleziona **[!UICONTROL Monitorare]** nel menu di navigazione a sinistra. Il **[!UICONTROL Monitorare]** la dashboard ti consente di visualizzare gli stati dei dati in entrata dall’acquisizione in batch o in streaming. Per visualizzare gli stati dei singoli batch, selezionare **[!UICONTROL Batch end-to-end]** o **[!UICONTROL Streaming end-to-end]**. Le dashboard elencano tutte le esecuzioni di acquisizione in batch o in streaming, incluse quelle che hanno avuto esito positivo, non sono riuscite o sono ancora in corso. Ogni elenco fornisce dettagli sul batch, tra cui l’ID del batch, il nome del set di dati di destinazione e il numero di record acquisiti. Se il set di dati di destinazione è abilitato per [!DNL Profile], viene visualizzato anche il numero di record di identità e profilo acquisiti.

![Viene visualizzata la schermata end-to-end del batch di monitoraggio. Vengono evidenziati sia il monitoraggio che il batch-to-batch.](../images/datasets/user-guide/batch-listing.png)

Puoi selezionare su un singolo **[!UICONTROL ID batch]** per accedere a **[!UICONTROL Panoramica batch]** e visualizzare i dettagli del batch, inclusi i registri di errore nel caso in cui il batch non venga acquisito.

![Vengono visualizzati i dettagli del batch selezionato. Ciò include il numero di record acquisiti, il numero di record non riusciti, lo stato del batch, la dimensione del file, l’ora di inizio e di fine dell’acquisizione, il set di dati e gli ID batch, l’ID organizzazione, il nome del set di dati e le informazioni di accesso.](../images/datasets/user-guide/batch-overview.png)

Se si desidera eliminare il batch, è possibile farlo selezionando **[!UICONTROL Elimina batch]** in alto a destra nel dashboard. Così facendo, rimuoverà anche i suoi record dal set di dati in cui è stato originariamente acquisito il batch.

![Il pulsante Elimina batch è evidenziato nella pagina dei dettagli del set di dati.](../images/datasets/user-guide/delete-batch.png)

## Passaggi successivi

Questa guida utente fornisce istruzioni per eseguire azioni comuni quando si lavora con i set di dati in [!DNL Experience Platform] dell&#39;utente. Per i passaggi sull&#39;esecuzione di [!DNL Platform] flussi di lavoro che coinvolgono set di dati, consulta le seguenti esercitazioni:

* [Creare un set di dati utilizzando le API](create.md)
* [Eseguire query sui dati del set di dati utilizzando l’API di accesso ai dati](../../data-access/home.md)
* [Configurare un set di dati per Real-Time Customer Profile e Identity Service tramite API](../../profile/tutorials/dataset-configuration.md)
