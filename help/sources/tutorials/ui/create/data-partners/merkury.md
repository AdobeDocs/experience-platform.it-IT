---
title: Creare una connessione e un flusso di dati di origine per la risoluzione delle identità Enterprise di Merkury nell’interfaccia utente
description: Scopri come creare una connessione sorgente per la risoluzione delle identità aziendali di Merkury utilizzando l’interfaccia utente di Adobe Experience Platform.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: cc87bff5ea19e2ffc9958bd645b4736d05773e3c
workflow-type: tm+mt
source-wordcount: '2015'
ht-degree: 0%

---

# Creare un [!DNL Merkury Enterprise Identity Resolution] connessione sorgente e flusso di dati nell’interfaccia utente

>[!NOTE]
>
>Il [!DNL Merkury Enterprise Identity Resolution] sorgente in versione beta. Leggi le [panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Questo tutorial descrive come creare un [!DNL Merkury Enterprise Identity Resolution] connessione sorgente e flusso di dati tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Raccogli le credenziali richieste

Per accedere al bucket in Experienci Platform, devi fornire valori validi per le seguenti credenziali:

| Credenziali | Descrizione |
| --- | --- |
| Chiave di accesso | ID della chiave di accesso per il bucket. Puoi recuperare questo valore dal tuo [!DNL Merkury] team. |
| Chiave segreta | ID della chiave segreta del bucket. Puoi recuperare questo valore dal tuo [!DNL Merkury] team. |
| Nome del bucket | Questo è il bucket di Merkury in cui verranno condivisi i file. Puoi recuperare questo valore dal tuo [!DNL Merkury] team. |

Per ulteriori informazioni sulla configurazione di [!DNL Merkury] e altri prerequisiti, leggi [[!DNL Merkury] panoramica dell’origine](../../../../connectors/data-partners/merkury.md).

## Connetti il tuo account Merkury

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL Partner dati]** categoria, seleziona **[!UICONTROL Merkury]** e quindi seleziona **[!UICONTROL Configurazione]**.

![Catalogo delle origini con l&#39;origine Merkury selezionata.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/catalog.png)

Il **[!UICONTROL Connetti a Merkury]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Crea un nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL Merkury] credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![La nuova interfaccia account per Merkury.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/new-account.png)

### Usa un account esistente

Per utilizzare un account esistente, seleziona **[!UICONTROL Account esistente]** e quindi selezionare [!DNL Merkury] account che desideri utilizzare. Seleziona **[!UICONTROL Avanti]** per procedere.

![Interfaccia account esistente per Merkury.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/existing-account.png)

>[!BEGINSHADEBOX]

**Formati di file supportati**

È possibile acquisire i seguenti formati di file con [!DNL Merkury] origine:

* Valori delimitatori separati (DSV): qualsiasi valore a carattere singolo può essere utilizzato come delimitatore per i file di dati in formato DSV.
* [!DNL JavaScript Object Notation] (JSON): i file di dati in formato JSON devono essere conformi a XDM.
* [!DNL Apache Parquet]: i file di dati formattati con Parquet devono essere conformi a XDM.
* File compressi: i file JSON e delimitati possono essere compressi come: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`, e `tar`.

>[!ENDSHADEBOX]

## Aggiungi dati

Dopo aver creato [!DNL Merkury] account, il **[!UICONTROL Aggiungi dati]** viene visualizzato un passaggio che fornisce un’interfaccia per esplorare [!DNL Merkury] gerarchia dei file e selezionare la cartella o il file specifico che si desidera portare all&#39;Experience Platform.

* La parte sinistra dell&#39;interfaccia è un browser di directory, che visualizza [!DNL Merkury] gerarchia dei file.
* La parte destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da una cartella o un file compatibile.

![La directory dei file e delle cartelle del flusso di lavoro sorgenti in cui è possibile selezionare i dati da acquisire.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/add-data.png)

Seleziona la cartella principale per accedere alla gerarchia delle cartelle. Da qui, puoi selezionare una singola cartella per acquisire tutti i file in essa contenuti in modo ricorsivo. Quando acquisisci un’intera cartella, assicurati che tutti i file in essa contenuti condividano lo stesso formato e schema di dati.

Dopo aver selezionato una cartella, l’interfaccia a destra viene aggiornata con un’anteprima del contenuto e della struttura del primo file della cartella selezionata.

![I dati selezionati per l’acquisizione e l’interfaccia di anteprima dei file.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/selected-data.png)


Durante questo passaggio, puoi effettuare diverse configurazioni dei dati prima di procedere. Seleziona innanzitutto **[!UICONTROL Formato dati]** quindi seleziona il formato dati appropriato per il file nel pannello a discesa visualizzato.

Nella tabella seguente vengono visualizzati i formati di dati appropriati per i tipi di file supportati:

| Tipo di file | Formato dati |
| --- | --- |
| CSV | [!UICONTROL Delimitato] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL XDM Parquet] |

### Seleziona un delimitatore di colonna

+++Selezionare questa opzione per visualizzare i passaggi relativi all&#39;impostazione di un delimitatore

Dopo aver configurato il formato dati, puoi impostare un delimitatore di colonna durante l’acquisizione di file delimitati. Seleziona la **[!UICONTROL Delimitatore]** e quindi selezionare un delimitatore dal menu a discesa. Il menu mostra le opzioni utilizzate più di frequente per i delimitatori, inclusa una virgola (`,`), una scheda (`\t`) e una pipe (`|`).

Se preferisci utilizzare un delimitatore personalizzato, seleziona **[!UICONTROL Personalizzato]** e inserisci un delimitatore a carattere singolo a tua scelta nella barra di input a comparsa.

+++

### Acquisire file compressi

+++ Seleziona per visualizzare i passaggi per acquisire i file compressi

Puoi anche acquisire file JSON o delimitati compressi specificandone il tipo di compressione.

In [!UICONTROL Seleziona dati] fase, seleziona un file compresso per l’acquisizione, quindi seleziona il tipo di file appropriato e se è conforme o meno a XDM. Quindi, seleziona **[!UICONTROL Tipo di compressione]** e quindi selezionare il tipo di file compresso appropriato per i dati di origine.

Per portare un file specifico su Platform, seleziona una cartella e quindi il file da acquisire. Durante questo passaggio, potete anche visualizzare in anteprima il contenuto di altri file all&#39;interno di una determinata cartella utilizzando l&#39;icona di anteprima accanto al nome di un file.

Al termine, seleziona **[!UICONTROL Successivo]**.

+++

## Fornisci i dettagli del flusso di dati

Il [!UICONTROL Dettagli del flusso di dati] consente di scegliere se utilizzare un set di dati esistente o nuovo. Durante questo processo, puoi anche configurare i dati da acquisire nel profilo e abilitare impostazioni come [!UICONTROL Diagnostica degli errori], [!UICONTROL Acquisizione parziale], e [!UICONTROL Avvisi].

### Usa un set di dati esistente

Per acquisire dati in un set di dati esistente, seleziona **[!UICONTROL Set di dati esistente]**. Puoi recuperare un set di dati esistente utilizzando [!UICONTROL Ricerca avanzata] oppure scorrendo l’elenco dei set di dati esistenti nel menu a discesa. Dopo aver selezionato un set di dati, fornisci un nome e una descrizione per il flusso di dati.

![Interfaccia del set di dati esistente.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/existing-dataset.png)

### Utilizza un nuovo set di dati

Per acquisire in un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]** quindi fornisci un nome per il set di dati di output e una descrizione facoltativa. Quindi, seleziona uno schema a cui mappare utilizzando [!UICONTROL Ricerca avanzata] oppure scorrendo l’elenco degli schemi esistenti nel menu a discesa. Dopo aver selezionato uno schema, fornisci un nome e una descrizione per il flusso di dati.

![La nuova interfaccia del set di dati.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/new-dataset.png)

### Abilita diagnostica profili ed errori

+++Seleziona per visualizzare i passaggi per abilitare la diagnostica degli errori e l’acquisizione del profilo

Quindi, seleziona la **[!UICONTROL Set di dati profilo]** attiva per abilitare il set di dati per Real-Time Customer Profile. Questo consente di creare una vista olistica degli attributi e dei comportamenti di un’entità. I dati di tutti i set di dati abilitati per il profilo verranno inclusi nel profilo e le modifiche verranno applicate al momento del salvataggio del flusso di dati.

[!UICONTROL Diagnostica degli errori] consente la generazione di messaggi di errore dettagliati per eventuali record errati che si verificano nel flusso di dati, mentre [!UICONTROL Acquisizione parziale] consente di acquisire dati contenenti errori, fino a una determinata soglia definita manualmente. Consulta la [panoramica dell’acquisizione in blocco parziale](../../../../../ingestion/batch-ingestion/partial.md) per ulteriori informazioni.

+++

### Abilita avvisi

+++Selezionare questa opzione per visualizzare i passaggi per l&#39;attivazione degli avvisi

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle origini tramite l’interfaccia utente](../../alerts.md).

Dopo aver fornito i dettagli del flusso di dati, seleziona **[!UICONTROL Successivo]**.

+++

## Mappare i campi dati su uno schema XDM

Il [!UICONTROL Mappatura] viene visualizzato un passaggio che fornisce un’interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia mapper e dei campi calcolati, vedi la [Guida dell’interfaccia utente per la preparazione dati](../../../../../data-prep/ui/mapping.md).

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Successivo]**.

![Interfaccia di mappatura.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/mapping.png)

## Pianificazione esecuzioni dell’acquisizione

Il [!UICONTROL Pianificazione] viene visualizzato un passaggio che consente di configurare una pianificazione di acquisizione per acquisire automaticamente i dati di origine selezionati utilizzando le mappature configurate. Per impostazione predefinita, la pianificazione è impostata su `Once`. Per regolare la frequenza di acquisizione, seleziona **[!UICONTROL Frequenza]** quindi seleziona un’opzione dal menu a discesa.

>[!TIP]
>
>L’intervallo e la retrocompilazione non sono visibili durante un’acquisizione una tantum.

![Interfaccia di pianificazione](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/schedule.png)

Se imposti la frequenza di acquisizione su `Minute`, `Hour`, `Day`, o `Week`, è necessario impostare un intervallo di tempo per stabilire un intervallo di tempo impostato tra ogni acquisizione. Ad esempio, una frequenza di acquisizione impostata su `Day` e un intervallo impostato su `15` significa che il flusso di dati è pianificato per acquisire i dati ogni 15 giorni.

Durante questo passaggio, puoi anche abilitare **retrocompilazione** e definisci una colonna per l’acquisizione incrementale dei dati. La retrocompilazione viene utilizzata per acquisire i dati storici, mentre la colonna definita per l’acquisizione incrementale consente di distinguere i nuovi dati dai dati esistenti.

Per ulteriori informazioni sulle configurazioni di pianificazione, consulta la tabella seguente.

| Campo | Descrizione |
| --- | --- |
| Frequenza | La frequenza con cui si verifica un’acquisizione. Le frequenze selezionabili comprendono `Once`, `Minute`, `Hour`, `Day`, e `Week`. |
| Interval | Numero intero che imposta l&#39;intervallo per la frequenza selezionata. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero e deve essere impostato su un valore maggiore o uguale a 15. |
| Ora di inizio | Una marca temporale UTC che indica quando è impostata per avvenire la prima acquisizione. L’ora di inizio deve essere maggiore o uguale all’ora UTC corrente. |
| Backfill | Valore booleano che determina quali dati vengono inizialmente acquisiti. Se la retrocompilazione è abilitata, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima acquisizione pianificata. Se la retrocompilazione è disattivata, verranno acquisiti solo i file caricati tra la prima esecuzione dell’acquisizione e l’ora di inizio. I file caricati prima dell’ora di avvio non verranno acquisiti. |

>[!NOTE]
>
>Per l’acquisizione in batch, ogni flusso di dati successivo seleziona i file da acquisire dall’origine in base ai **ultima modifica** timestamp. Ciò significa che i flussi di dati batch selezionano dall’origine i file che sono nuovi o che sono stati modificati dall’ultima esecuzione del flusso. Inoltre, devi assicurarti che vi sia un intervallo di tempo sufficiente tra il caricamento dei file e l’esecuzione di un flusso pianificata, perché i file che non sono completamente caricati nell’account di archiviazione cloud prima dell’esecuzione del flusso pianificata potrebbero non essere raccolti per l’acquisizione.

Al termine della configurazione della pianificazione di acquisizione, seleziona **[!UICONTROL Successivo]**.

## Verifica il flusso di dati

Il **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima di crearlo. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all’interno di tale file di origine.
* **[!UICONTROL Assegna set di dati e mappa campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui aderisce il set di dati.
* **[!UICONTROL Pianificazione]**: mostra il periodo attivo, la frequenza e l’intervallo della pianificazione di acquisizione.

Dopo aver rivisto il flusso di dati, fai clic su **[!UICONTROL Fine]** e lascia un po’ di tempo per creare il flusso di dati.

![La pagina di revisione.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/review.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un flusso di dati per portare dati batch dal tuo [!DNL Merkury] da sorgente a Experience Platform. Per ulteriori risorse, consulta la documentazione descritta di seguito.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni su tassi di acquisizione, successo ed errori. Per ulteriori informazioni su come monitorare il flusso di dati, consulta l’esercitazione su [monitoraggio di account e flussi di dati nell’interfaccia utente](../../monitor.md).

### Aggiornare il flusso di dati

Per aggiornare le configurazioni per la pianificazione, la mappatura e le informazioni generali dei flussi di dati, visita il tutorial su [aggiornamento dei flussi di dati di origine nell’interfaccia utente](../../update-dataflows.md)

### Eliminare il flusso di dati

Puoi eliminare i flussi di dati non più necessari o creati in modo errato utilizzando **[!UICONTROL Elimina]** funzione disponibile nella **[!UICONTROL Flussi dati]** Workspace. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l’esercitazione su [eliminazione di flussi di dati nell’interfaccia utente](../../delete.md).