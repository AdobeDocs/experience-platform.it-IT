---
keywords: Experience Platform;home;argomenti comuni;abilitare set di dati;set di dati;dataset;dataset;home;popular topic;enable dataset;Dataset;dataset
solution: Experience Platform
title: Guida dell’interfaccia utente dei set di dati
description: Scopri come eseguire azioni comuni quando si lavora con i set di dati nell’interfaccia utente di Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '3080'
ht-degree: 2%

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
>title="Numeri negativi nell’attività del set di dati"
>abstract="Nei record acquisiti, i numeri negativi indicano che un utente ha eliminato determinati batch in un intervallo di tempo selezionato."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_daysRemaining"
>title="Scadenza set di dati"
>abstract="Questa colonna indica il numero di giorni rimanenti al set di dati di destinazione prima della scadenza automatica."

In [!DNL Experience Platform] UI, seleziona **[!UICONTROL Set di dati]** nel menu di navigazione a sinistra per aprire **[!UICONTROL Set di dati]** dashboard. Il dashboard elenca tutti i set di dati disponibili per l’organizzazione. Vengono visualizzati i dettagli di ciascun set di dati elencato, compreso il nome, lo schema a cui il set di dati aderisce e lo stato dell’esecuzione di acquisizione più recente.

![L’interfaccia utente di Platform con l’elemento Set di dati evidenziato nella barra di navigazione a sinistra.](../images/datasets/user-guide/browse-datasets.png)

Seleziona il nome di un set di dati da [!UICONTROL Sfoglia] scheda per accedere ai relativi **[!UICONTROL Attività set di dati]** e visualizzare i dettagli del set di dati selezionato. La scheda attività include un grafico che mostra il tasso di utilizzo dei messaggi e un elenco di batch con esito positivo o negativo.

![Vengono evidenziate le metriche e le visualizzazioni del set di dati selezionato.](../images/datasets/user-guide/dataset-activity-1.png)
![Vengono evidenziati i batch di esempio relativi al set di dati selezionato.](../images/datasets/user-guide/dataset-activity-2.png)

## Altre azioni {#more-actions}

È possibile [!UICONTROL Elimina] o [!UICONTROL Abilitare un set di dati per il profilo] dal [!UICONTROL Set di dati] visualizzazione dettagli. Per visualizzare le azioni disponibili, seleziona **[!UICONTROL ... Altro]** in alto a destra nell’interfaccia utente. Viene visualizzato il menu a discesa.

![L’area di lavoro Set di dati con [!UICONTROL ... Altro] menu a discesa evidenziato.](../images/datasets/user-guide/more-actions.png)

Se si seleziona **[!UICONTROL Abilitare un set di dati per il profilo]**, viene visualizzata una finestra di conferma. Seleziona **[!UICONTROL Abilita]** per confermare la scelta.

>[!NOTE]
>
>Per abilitare un set di dati per il profilo, lo schema a cui il set di dati aderisce deve essere compatibile per l’utilizzo in Real-Time Customer Profile. Consulta la [Abilitare un set di dati per il profilo](#enable-profile) per ulteriori informazioni.

![La finestra di dialogo Abilita conferma set di dati.](../images/datasets/user-guide/profile-enable-confirmation-dialog.png)

Se si seleziona **[!UICONTROL Elimina]**, il [!UICONTROL Elimina set di dati] viene visualizzata una finestra di dialogo di conferma. Seleziona **[!UICONTROL Elimina]** per confermare la scelta.

>[!NOTE]
>
>Impossibile eliminare i set di dati di sistema.

Puoi anche eliminare un set di dati o aggiungere un set di dati da utilizzare con Real-Time Customer Profile dalle azioni in linea disponibili nella [!UICONTROL Sfoglia] scheda. Consulta la [sezione azioni in linea](#inline-actions) per ulteriori informazioni.

![Finestra di dialogo di conferma Elimina set di dati.](../images/datasets/user-guide/delete-confirmation-dialog.png)

## Azioni del set di dati in linea {#inline-actions}

L’interfaccia utente dei set di dati ora offre una raccolta di azioni in linea per ogni set di dati disponibile. Seleziona i puntini di sospensione (...) di un set di dati da gestire per visualizzare le opzioni disponibili in un menu a comparsa. Le azioni disponibili comprendono:

* [[!UICONTROL Anteprima set di dati]](#preview),
* [[!UICONTROL Gestire i dati e accedere alle etichette]](#manage-and-enforce-data-governance)
* [[!UICONTROL Abilita profilo unificato]](#enable-profile)
* [[!UICONTROL Gestione tag]](#manage-tags)
* [[!UICONTROL Sposta in cartelle]](#move-to-folders)
* [[!UICONTROL Elimina]](#delete).

Ulteriori informazioni su queste azioni disponibili sono disponibili nelle rispettive sezioni. Per informazioni su come gestire simultaneamente un numero elevato di set di dati, consulta [azioni in blocco](#bulk-actions) sezione.

### Visualizzare in anteprima un set di dati {#preview}

Puoi visualizzare in anteprima i dati di esempio del set di dati da entrambe le opzioni in linea di [!UICONTROL Sfoglia] e la scheda [!UICONTROL Attività set di dati] visualizzazione. Dalla sezione [!UICONTROL Sfoglia] , seleziona i puntini di sospensione (...) accanto al nome del set di dati da visualizzare in anteprima. Viene visualizzato un elenco di opzioni. Quindi, seleziona **[!UICONTROL Anteprima set di dati]** dall’elenco delle opzioni disponibili. Se il set di dati è vuoto, il collegamento di anteprima viene disattivato e indica invece che l’anteprima non è disponibile.

![La scheda Sfoglia dell’area di lavoro Set di dati con i puntini di sospensione e l’opzione Anteprima set di dati evidenziata per il set di dati selezionato.](../images/datasets/user-guide/preview-dataset-option.png)

Viene visualizzata la finestra di anteprima, in cui a destra è visualizzata la vista gerarchica dello schema per il set di dati.

![Viene visualizzata la finestra di dialogo di anteprima del set di dati con informazioni sulla struttura del set di dati e valori di esempio.](../images/datasets/user-guide/preview-dataset.png)

In alternativa, da **[!UICONTROL Attività set di dati]** schermata, seleziona **[!UICONTROL Anteprima set di dati]** nell’angolo in alto a destra dello schermo per visualizzare in anteprima fino a 100 righe di dati.

![Viene evidenziato il pulsante Anteprima set di dati.](../images/datasets/user-guide/select-preview.png)

Per metodi più affidabili per accedere ai dati, [!DNL Experience Platform] fornisce servizi a valle come [!DNL Query Service] e [!DNL JupyterLab] per esplorare e analizzare i dati. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica di Query Service](../../query-service/home.md)
* [Guida utente di JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

### Gestire e applicare la governance dei dati su un set di dati {#manage-and-enforce-data-governance}

Puoi gestire le etichette di governance dei dati per un set di dati selezionando le opzioni in linea di [!UICONTROL Sfoglia] scheda. Seleziona i puntini di sospensione (...) accanto al nome del set di dati che desideri gestire, seguiti da **[!UICONTROL Gestire i dati e accedere alle etichette]** dal menu a discesa.

Le etichette di utilizzo dei dati, applicate a livello di schema, ti consentono di categorizzare set di dati e campi in base ai criteri di utilizzo applicabili a tali dati. Consulta la [Panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni sulle etichette o fare riferimento a [guida utente delle etichette di utilizzo dati](../../data-governance/labels/overview.md) per istruzioni su come applicare etichette agli schemi per la propagazione ai set di dati.

## Abilitare un set di dati per Real-Time Customer Profile {#enable-profile}

Ogni set di dati ha la capacità di arricchire i profili dei clienti con i dati acquisiti. A questo scopo, lo schema a cui aderisce il set di dati deve essere compatibile per l’utilizzo in [!DNL Real-Time Customer Profile]. Uno schema compatibile soddisfa i seguenti requisiti:

* Lo schema ha almeno un attributo specificato come proprietà di identità.
* Lo schema ha una proprietà di identità definita come identità primaria.

Per ulteriori informazioni sull’abilitazione di uno schema per [!DNL Profile], vedere [Guida utente dell’Editor di schema](../../xdm/tutorials/create-schema-ui.md).

Puoi abilitare un set di dati per il profilo da entrambe le opzioni in linea di [!UICONTROL Sfoglia] e la scheda [!UICONTROL Attività set di dati] visualizzazione. Dalla sezione [!UICONTROL Sfoglia] scheda di [!UICONTROL Set di dati] nell’area di lavoro, seleziona i puntini di sospensione di un set di dati da abilitare per il profilo. Viene visualizzato un elenco di opzioni. Quindi, seleziona **[!UICONTROL Abilita profilo unificato]** dall’elenco delle opzioni disponibili.

![La scheda Sfoglia dell’area di lavoro Set di dati con i puntini di sospensione e Abilita profilo unificato evidenziati.](../images/datasets/user-guide/enable-for-profile.png)

In alternativa, dal set di dati di **[!UICONTROL Attività set di dati]** , seleziona la **[!UICONTROL Profilo]** attivare/disattivare all&#39;interno di **[!UICONTROL Proprietà]** colonna. Una volta abilitata, anche i dati acquisiti nel set di dati verranno utilizzati per popolare i profili dei clienti.

>[!NOTE]
>
>Se un set di dati contiene già dati ed è quindi abilitato per [!DNL Profile], i dati esistenti non vengono utilizzati automaticamente da [!DNL Profile]. Dopo aver abilitato un set di dati per [!DNL Profile], si consiglia di riacquisire tutti i dati esistenti per farli contribuire ai profili dei clienti.

![L’opzione Profilo è evidenziata all’interno della pagina dei dettagli del set di dati.](../images/datasets/user-guide/enable-dataset-profiles.png)

Anche i set di dati abilitati per il profilo possono essere filtrati in base a questo criterio. Consulta la sezione su come [filtrare i set di dati abilitati per il profilo](#filter-profile-enabled-datasets) per ulteriori informazioni.

### Gestire i tag dei set di dati {#manage-tags}

Aggiungi tag personalizzati creati per organizzare i set di dati e migliorare le funzionalità di ricerca, filtro e ordinamento. Dalla sezione [!UICONTROL Sfoglia] scheda di [!UICONTROL Set di dati] nell’area di lavoro, seleziona i puntini di sospensione di un set di dati che desideri gestire e poi **[!UICONTROL Gestione tag]** dal menu a discesa.

![La scheda Sfoglia dell’area di lavoro Set di dati con i puntini di sospensione e l’opzione Gestisci tag evidenziati per il set di dati selezionato.](../images/datasets/user-guide/manage-tags.png)

Il [!UICONTROL Gestione tag] viene visualizzata. Inserisci una breve descrizione per creare un tag personalizzato oppure scegli un tag preesistente per etichettare il set di dati. Seleziona **[!UICONTROL Salva]** per confermare le impostazioni.

![Viene evidenziata la finestra di dialogo Gestisci tag con tag personalizzati.](../images/datasets/user-guide/manage-tags-dialog.png)

Il [!UICONTROL Gestione tag] Questa finestra di dialogo può anche rimuovere i tag esistenti da un set di dati. Seleziona semplicemente la x accanto al tag da rimuovere e fai clic su **[!UICONTROL Salva]**.

Una volta aggiunto un tag a un set di dati, i set di dati possono essere filtrati in base al tag corrispondente. Consulta la sezione su come [filtrare i set di dati per tag](#enable-profile) per ulteriori informazioni.

Per ulteriori informazioni su come classificare gli oggetti business per individuare e classificare più facilmente gli oggetti, vedere la guida in linea [gestione delle tassonomie dei metadati](../../administrative-tags/ui/managing-tags.md). Questa guida descrive come un utente con le autorizzazioni appropriate può creare tag predefiniti, assegnare categorie ai tag ed eseguire tutte le operazioni CRUD correlate su tag e categorie di tag nell’interfaccia utente di Platform.

### Sposta in cartelle {#move-to-folders}

Per una migliore gestione dei set di dati, puoi inserire i set di dati all’interno di cartelle. Per spostare un set di dati in una cartella, seleziona i puntini di sospensione (...) accanto al nome del set di dati che desideri gestire, quindi fai clic su **[!UICONTROL Sposta nella cartella]** dal menu a discesa.

![Il [!UICONTROL Set di dati] dashboard con i puntini di sospensione e [!UICONTROL Sposta nella cartella] evidenziato.](../images/datasets/user-guide/move-to-folder.png)

Il [!UICONTROL Sposta] viene visualizzata la finestra di dialogo dataset to folder (set di dati nella cartella). Seleziona la cartella in cui desideri spostare il pubblico, quindi fai clic su **[!UICONTROL Sposta]**. Una notifica a comparsa informa che lo spostamento del set di dati è stato eseguito correttamente.

![Il [!UICONTROL Sposta] finestra di dialogo del set di dati con [!UICONTROL Sposta] evidenziato.](../images/datasets/user-guide/move-dialog.png)

>[!TIP]
>
>Puoi anche creare cartelle direttamente dalla finestra di dialogo Sposta set di dati. Per creare una cartella, seleziona l’icona Crea cartella (![Icona Crea cartella.](../images/datasets/user-guide/create-folder-icon.png)) in alto a destra nella finestra di dialogo.
>
>![Il [!UICONTROL Sposta] finestra di dialogo del set di dati con l’icona crea cartella evidenziata.](/help/catalog/images/datasets/user-guide/create-folder.png)

Una volta che il set di dati si trova in una cartella, puoi scegliere di visualizzare solo i set di dati che appartengono a una cartella specifica. Per aprire la struttura delle cartelle, seleziona l’icona mostra cartelle (![Icona Mostra cartelle](../images/datasets/user-guide/show-folders-icon.png)). Quindi, seleziona la cartella scelta per visualizzare tutti i set di dati associati.

![Il [!UICONTROL Set di dati] dashboard con la struttura di cartelle dei set di dati visualizzata, l’icona mostra cartelle e una cartella selezionata evidenziata.](../images/datasets/user-guide/folder-structure.png)

### Eliminare un set di dati {#delete}

Puoi eliminare un set di dati dalle azioni in linea del set di dati in [!UICONTROL Sfoglia] o in alto a destra del [!UICONTROL Attività set di dati] visualizzazione. Dalla sezione [!UICONTROL Sfoglia] , seleziona i puntini di sospensione (...) accanto al nome del set di dati da eliminare. Viene visualizzato un elenco di opzioni. Quindi, seleziona **[!UICONTROL Elimina]** dal menu a discesa.

![La scheda Sfoglia dell’area di lavoro Set di dati con i puntini di sospensione e l’opzione Elimina evidenziata per il set di dati selezionato.](../images/datasets/user-guide/inline-delete-dataset.png)

Viene visualizzata una finestra di dialogo di conferma. Seleziona **[!UICONTROL Elimina]** per confermare.

In alternativa, seleziona **[!UICONTROL Elimina set di dati]** dal **[!UICONTROL Attività set di dati]** schermo.

>[!NOTE]
>
>Set di dati creati e utilizzati dalle applicazioni e dai servizi Adobe (ad esempio Adobe Analytics, Adobe Audience Manager o [!DNL Offer Decisioning]) non può essere eliminato.

![Il pulsante Elimina set di dati è evidenziato nella pagina dei dettagli del set di dati.](../images/datasets/user-guide/delete-dataset.png)

Viene visualizzata una casella di conferma. Seleziona **[!UICONTROL Elimina]** per confermare l’eliminazione del set di dati.

![Viene visualizzata la finestra modale di conferma per l’eliminazione, con il pulsante Elimina evidenziato.](../images/datasets/user-guide/confirm-delete.png)

### Eliminare un set di dati abilitato per il profilo

Se un set di dati è abilitato per il profilo, eliminandolo tramite l’interfaccia utente verrà eliminato dal data lake, da Identity Service e anche da tutti i dati di profilo associati a tale set di dati nell’archivio Profili.

Puoi eliminare i dati profilo associati a un set di dati da [!DNL Profile] archiviare (lasciando i dati nel data lake) utilizzando l’API Real-Time Customer Profile. Per ulteriori informazioni, vedere [guida dell’endpoint API dei processi di sistema del profilo](../../profile/api/profile-system-jobs.md).

## Cercare e filtrare i set di dati {#search-and-filter}

Per cercare o filtrare l’elenco dei set di dati disponibili, seleziona l’icona del filtro (![Icona del filtro.](../images/datasets/user-guide/icon.png)) in alto a sinistra nell’area di lavoro. Nella barra a sinistra viene visualizzato un set di opzioni filtro. Esistono diversi metodi per filtrare i set di dati disponibili. Tra questi: [[!UICONTROL Mostra set di dati di sistema]](#show-system-datasets), [[!UICONTROL Incluso nel profilo]](#filter-profile-enabled-datasets), [[!UICONTROL Tag]](#filter-by-tag), [[!UICONTROL Data di creazione]](#filter-by-creation-date), [[!UICONTROL Data di modifica], [!UICONTROL Creato da]](#filter-by-creation-date), e [[!UICONTROL Schema]](#filter-by-schema).

L’elenco dei filtri applicati viene visualizzato sopra i risultati filtrati.

![Scheda Sfoglia dell’area di lavoro Set di dati con l’elenco dei filtri applicati evidenziato.](../images/datasets/user-guide/applied-filters.png)

### Mostra set di dati di sistema {#show-system-datasets}

Per impostazione predefinita, vengono visualizzati solo i set di dati in cui hai acquisito i dati. Se desideri visualizzare i set di dati generati dal sistema, seleziona la **[!UICONTROL Sì]** casella di controllo in [!UICONTROL Mostra set di dati di sistema] sezione. I set di dati generati dal sistema vengono utilizzati solo per elaborare altri componenti. Ad esempio, il set di dati di esportazione del profilo generato dal sistema viene utilizzato per elaborare il dashboard del profilo.

![Le opzioni di filtro dell’area di lavoro Set di dati con [!UICONTROL Mostra set di dati di sistema] sezione evidenziata.](../images/datasets/user-guide/show-system-datasets.png)

### Filtra set di dati abilitati per il profilo {#filter-profile-enabled-datasets}

I set di dati abilitati per i dati del profilo vengono utilizzati per popolare i profili dei clienti dopo l’acquisizione dei dati. Consulta la sezione su [abilitazione dei set di dati per il profilo](#enable-profile) per ulteriori informazioni.

Per filtrare il set di dati in base al fatto che siano stati abilitati per il profilo, seleziona la [!UICONTROL Sì] dalle opzioni del filtro.

![Le opzioni di filtro dell’area di lavoro Set di dati con [!UICONTROL Incluso nel profilo] sezione evidenziata.](../images/datasets/user-guide/included-in-profile.png)

### Filtrare i set di dati per tag {#filter-by-tag}

Inserisci il nome del tag personalizzato nella [!UICONTROL Tag] , quindi seleziona il tag dall’elenco delle opzioni disponibili per cercare e filtrare i set di dati corrispondenti a tale tag.

![Le opzioni di filtro dell’area di lavoro Set di dati con [!UICONTROL Tag] icona di input e filtro evidenziata.](../images/datasets/user-guide/filter-tags.png)

### Filtrare i set di dati per data di creazione {#filter-by-creation-date}

I set di dati possono essere filtrati per data di creazione in un periodo di tempo personalizzato. Può essere utilizzato per escludere dati storici o per generare informazioni sui dati cronologici e rapporti specifici. Scegli un [!UICONTROL Data di inizio] e un [!UICONTROL Data di fine] selezionando l’icona del calendario per ciascun campo. In seguito, nella scheda Sfoglia verranno visualizzati solo i set di dati conformi a tali criteri.

### Filtrare i set di dati per data di modifica {#filter-by-modified-date}

Simile al filtro per la data di creazione, puoi filtrare i set di dati in base alla data dell’ultima modifica. In [!UICONTROL Data di modifica] sezione, Scegli un [!UICONTROL Data di inizio] e un [!UICONTROL Data di fine] selezionando l’icona del calendario per ciascun campo. In seguito, nella scheda Sfoglia verranno visualizzati solo i set di dati modificati durante tale periodo.

### Filtra per schema {#filter-by-schema}

Puoi filtrare i set di dati in base allo schema che ne definisce la struttura. Seleziona l’icona a discesa o inserisci il nome dello schema nel campo di testo. Viene visualizzato un elenco di potenziali corrispondenze. Seleziona lo schema appropriato dall’elenco.

## Azioni in blocco {#bulk-actions}

Utilizza azioni in blocco per migliorare l’efficienza operativa ed eseguire più azioni su numerosi set di dati contemporaneamente. È possibile risparmiare tempo e mantenere una struttura di dati organizzata con azioni in blocco come [Sposta nella cartella](#move-to-folders), [Modifica tag](#manage-tags), e [Elimina](#delete) set di dati.

Per agire su più set di dati alla volta, seleziona singoli set di dati con la casella di controllo su ogni riga oppure seleziona un’intera pagina con la casella di controllo dell’intestazione di colonna. Una volta selezionata, viene visualizzata la barra delle azioni di massa.

![Scheda Sfoglia set di dati con numerosi set di dati selezionati ed evidenziata la barra delle azioni di massa.](../images/datasets/user-guide/bulk-actions.png)

Quando applichi azioni in blocco ai set di dati, si applicano le seguenti condizioni:

* Puoi selezionare i set di dati da pagine diverse dell’interfaccia utente.
* Se selezioni un filtro, i set di dati selezionati verranno reimpostati.

## Ordinare i set di dati per data di creazione {#sort}

Set di dati in [!UICONTROL Sfoglia] La scheda può essere ordinata in base a date ascendenti o discendenti. Seleziona la [!UICONTROL Creato] o [!UICONTROL Ultimo aggiornamento] intestazioni di colonna per alternare tra crescente e decrescente. Una volta selezionata, la colonna lo indica con una freccia su o giù a lato dell’intestazione della colonna.

![Scheda Sfoglia dell’area di lavoro Set di dati con le colonne Creato e Ultimo aggiornamento evidenziate.](../images/datasets/user-guide/ascending-descending-columns.png)

## Creare un set di dati {#create}

Per creare un nuovo set di dati, inizia selezionando **[!UICONTROL Crea set di dati]** nel **[!UICONTROL Set di dati]** dashboard.

![Viene evidenziato il pulsante Crea set di dati.](../images/datasets/user-guide/select-create.png)

Nella schermata successiva vengono presentate le due opzioni seguenti per la creazione di un nuovo set di dati:

* [Crea un set di dati dallo schema](#schema)
* [Crea set di dati da file CSV](#csv)

### Creare un set di dati con uno schema esistente {#schema}

In **[!UICONTROL Crea set di dati]** schermata, seleziona **[!UICONTROL Crea set di dati dallo schema]** per creare un nuovo set di dati vuoto.

![Viene evidenziato il pulsante Crea set di dati da schema.](../images/datasets/user-guide/create-dataset-schema.png)

Il **[!UICONTROL Seleziona schema]** viene visualizzato il passaggio. Sfoglia l’elenco degli schemi e seleziona lo schema a cui il set di dati aderirà prima di selezionare **[!UICONTROL Successivo]**.

![Viene visualizzato un elenco di schemi. Viene evidenziato lo schema che verrà utilizzato per creare il set di dati.](../images/datasets/user-guide/select-schema.png)

Il **[!UICONTROL Configurare il set di dati]** viene visualizzato il passaggio. Fornisci al set di dati un nome e una descrizione facoltativa, quindi seleziona **[!UICONTROL Fine]** per creare il set di dati.

![Vengono inseriti i dettagli di configurazione del set di dati. Ciò include dettagli quali il nome e la descrizione del set di dati.](../images/datasets/user-guide/configure-dataset-schema.png)

I set di dati possono essere filtrati dall’elenco dei set di dati disponibili nell’interfaccia utente con il filtro dello schema. Consulta la sezione su come [filtrare i set di dati per schema](#filter-by-schema) per ulteriori informazioni.

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

## Monitorare l’acquisizione dei dati

In [!DNL Experience Platform] UI, seleziona **[!UICONTROL Monitorare]** nel menu di navigazione a sinistra. Il **[!UICONTROL Monitorare]** la dashboard ti consente di visualizzare gli stati dei dati in entrata dall’acquisizione in batch o in streaming. Per visualizzare gli stati dei singoli batch, selezionare **[!UICONTROL Batch end-to-end]** o **[!UICONTROL Streaming end-to-end]**. Le dashboard elencano tutte le esecuzioni di acquisizione in batch o in streaming, incluse quelle che hanno avuto esito positivo, non sono riuscite o sono ancora in corso. Ogni elenco fornisce dettagli sul batch, tra cui l’ID del batch, il nome del set di dati di destinazione e il numero di record acquisiti. Se il set di dati di destinazione è abilitato per [!DNL Profile], viene visualizzato anche il numero di record di identità e profilo acquisiti.

![Viene visualizzata la schermata end-to-end del batch di monitoraggio. Vengono evidenziati sia il monitoraggio che il batch-to-batch.](../images/datasets/user-guide/batch-listing.png)

Puoi selezionare su un singolo **[!UICONTROL ID batch]** per accedere a **[!UICONTROL Panoramica batch]** e visualizzare i dettagli del batch, inclusi i registri di errore nel caso in cui il batch non venga acquisito.

![Vengono visualizzati i dettagli del batch selezionato. Ciò include il numero di record acquisiti, il numero di record non riusciti, lo stato del batch, la dimensione del file, l’ora di inizio e di fine dell’acquisizione, il set di dati e gli ID batch, l’ID organizzazione, il nome del set di dati e le informazioni di accesso.](../images/datasets/user-guide/batch-overview.png)

Se desideri eliminare il batch, seleziona **[!UICONTROL Elimina batch]** in alto a destra nel dashboard. L’eliminazione di un batch rimuove anche i relativi record dal set di dati in cui è stato originariamente acquisito il batch.

>[!NOTE]
>
>Se i dati acquisiti sono stati abilitati per il profilo ed elaborati, l’eliminazione di un batch non comporta l’eliminazione di tali dati dall’archivio Profili.

![Il pulsante Elimina batch è evidenziato nella pagina dei dettagli del set di dati.](../images/datasets/user-guide/delete-batch.png)

## Passaggi successivi

Questa guida utente fornisce istruzioni per eseguire azioni comuni quando si lavora con i set di dati in [!DNL Experience Platform] dell&#39;utente. Per i passaggi sull&#39;esecuzione di [!DNL Platform] flussi di lavoro che coinvolgono set di dati, consulta le seguenti esercitazioni:

* [Creare un set di dati utilizzando le API](create.md)
* [Eseguire query sui dati del set di dati utilizzando l’API di accesso ai dati](../../data-access/home.md)
* [Configurare un set di dati per Real-Time Customer Profile e Identity Service tramite API](../../profile/tutorials/dataset-configuration.md)
