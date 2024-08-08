---
title: Creare una connessione e un flusso di dati Source per la risoluzione delle identità aziendali di Merkury nell’interfaccia utente
description: Scopri come creare una connessione sorgente per la risoluzione delle identità aziendali di Merkury utilizzando l’interfaccia utente di Adobe Experience Platform.
last-substantial-update: 2023-12=12
badge: Beta
exl-id: 2af48c18-76f9-4615-8e76-8f030a312a8f
source-git-commit: d048109141168b33795753c4706dac64cdf29ca5
workflow-type: tm+mt
source-wordcount: '2143'
ht-degree: 1%

---

# Crea una connessione di origine [!DNL Merkury Enterprise Identity Resolution] e un flusso di dati nell&#39;interfaccia utente

>[!NOTE]
>
>L&#39;origine [!DNL Merkury Enterprise Identity Resolution] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../../../home.md#terms-and-conditions).

Questo tutorial illustra i passaggi necessari per creare una connessione di origine [!DNL Merkury Enterprise Identity Resolution] e un flusso di dati utilizzando l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Raccogli le credenziali richieste

Per accedere al bucket in Experience Platform, devi fornire valori validi per le seguenti credenziali:

| Credenziali | Descrizione |
| --- | --- |
| Chiave di accesso | ID della chiave di accesso per il bucket. Puoi recuperare questo valore dal tuo team [!DNL Merkury]. |
| Chiave segreta | ID della chiave segreta del bucket. Puoi recuperare questo valore dal tuo team [!DNL Merkury]. |
| Nome del bucket | Questo è il bucket di Merkury in cui verranno condivisi i file. Puoi recuperare questo valore dal tuo team [!DNL Merkury]. |

Per ulteriori informazioni sulla configurazione per [!DNL Merkury] e altri prerequisiti, leggere la [[!DNL Merkury] panoramica origine](../../../../connectors/data-partners/merkury.md).

## Connetti il tuo account Merkury

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Partner dati]**, selezionare **[!UICONTROL Merkury]**, quindi **[!UICONTROL Configurazione]**.

![Catalogo delle origini con l&#39;origine Merkury selezionata.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Merkury]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Crea un nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali [!DNL Merkury]. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Nuova interfaccia account per Merkury.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/new-account.png)

### Usa un account esistente

Per utilizzare un account esistente, selezionare **[!UICONTROL Account esistente]**, quindi selezionare l&#39;account [!DNL Merkury] che si desidera utilizzare. Seleziona **[!UICONTROL Avanti]** per procedere.

![Interfaccia account esistente per Merkury.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/existing-account.png)

>[!BEGINSHADEBOX]

**Formati di file supportati**

È possibile acquisire i seguenti formati di file con l&#39;origine [!DNL Merkury]:

* Valori delimitatori separati (DSV): qualsiasi valore a carattere singolo può essere utilizzato come delimitatore per i file di dati in formato DSV.
* [!DNL JavaScript Object Notation] (JSON): i file di dati in formato JSON devono essere conformi a XDM.
* [!DNL Apache Parquet]: i file di dati in formato Parquet devono essere conformi a XDM.
* File compressi: JSON e file delimitati possono essere compressi come: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip` e `tar`.

>[!ENDSHADEBOX]

## Aggiungi dati

Dopo aver creato l&#39;account [!DNL Merkury], viene visualizzato il passaggio **[!UICONTROL Aggiungi dati]**, che fornisce un&#39;interfaccia per esplorare la gerarchia dei file [!DNL Merkury] e selezionare la cartella o il file specifico da portare in Experience Platform.

* La parte sinistra dell&#39;interfaccia è un browser di directory, che visualizza la gerarchia dei file [!DNL Merkury].
* La parte destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da una cartella o un file compatibile.

![Directory di file e cartelle del flusso di lavoro di origine in cui è possibile selezionare i dati che si desidera acquisire.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/add-data.png)

Seleziona la cartella principale per accedere alla gerarchia delle cartelle. Da qui, puoi selezionare una singola cartella per acquisire tutti i file in essa contenuti in modo ricorsivo. Quando acquisisci un’intera cartella, assicurati che tutti i file in essa contenuti condividano lo stesso formato e schema di dati.

Dopo aver selezionato una cartella, l’interfaccia a destra viene aggiornata con un’anteprima del contenuto e della struttura del primo file della cartella selezionata.

![Dati selezionati per l&#39;acquisizione e interfaccia di anteprima file.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/selected-data.png)


Durante questo passaggio, puoi effettuare diverse configurazioni dei dati prima di procedere. Selezionare innanzitutto **[!UICONTROL Formato dati]**, quindi selezionare il formato dati appropriato per il file nel pannello a discesa visualizzato.

Nella tabella seguente vengono visualizzati i formati di dati appropriati per i tipi di file supportati:

| Tipo di file | Formato dei dati |
| --- | --- |
| CSV | [!UICONTROL Delimitato] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL Parquet XDM] |

### Seleziona un delimitatore di colonna

+++Selezionare questa opzione per visualizzare i passaggi relativi all&#39;impostazione di un delimitatore

Dopo aver configurato il formato dati, puoi impostare un delimitatore di colonna durante l’acquisizione di file delimitati. Selezionare l&#39;opzione **[!UICONTROL Delimitatore]**, quindi selezionare un delimitatore dal menu a discesa. Il menu visualizza le opzioni utilizzate più di frequente per i delimitatori, tra cui una virgola (`,`), una tabulazione (`\t`) e una barra verticale (`|`).

Se preferisci utilizzare un delimitatore personalizzato, seleziona **[!UICONTROL Personalizzato]** e immetti un delimitatore a carattere singolo nella barra di input a comparsa.

+++

### Acquisire file compressi

+++ Seleziona per visualizzare i passaggi per acquisire i file compressi

Puoi anche acquisire file JSON o delimitati compressi specificandone il tipo di compressione.

Nel passaggio [!UICONTROL Seleziona dati], seleziona un file compresso per l&#39;acquisizione, quindi seleziona il tipo di file appropriato e se è conforme o meno a XDM. Selezionare **[!UICONTROL Tipo di compressione]**, quindi selezionare il tipo di file compresso appropriato per i dati di origine.

Per portare un file specifico su Platform, seleziona una cartella e quindi il file da acquisire. Durante questo passaggio, potete anche visualizzare in anteprima il contenuto di altri file all&#39;interno di una determinata cartella utilizzando l&#39;icona di anteprima accanto al nome di un file.

Al termine, selezionare **[!UICONTROL Avanti]**.

+++

## Fornisci i dettagli del flusso di dati

La pagina [!UICONTROL Dettagli flusso di dati] consente di scegliere se utilizzare un set di dati esistente o nuovo. Durante questo processo, puoi anche configurare i dati da acquisire nel profilo e abilitare impostazioni come [!UICONTROL Diagnostica errori], [!UICONTROL Acquisizione parziale] e [!UICONTROL Avvisi].

### Usa un set di dati esistente

Per acquisire dati in un set di dati esistente, seleziona **[!UICONTROL Set di dati esistente]**. Puoi recuperare un set di dati esistente utilizzando l&#39;opzione [!UICONTROL Ricerca avanzata] oppure scorrendo l&#39;elenco dei set di dati esistenti nel menu a discesa. Dopo aver selezionato un set di dati, fornisci un nome e una descrizione per il flusso di dati.

![Interfaccia del set di dati esistente.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/existing-dataset.png)

### Utilizza un nuovo set di dati

Per acquisire in un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]**, quindi fornisci un nome per il set di dati di output e una descrizione facoltativa. Quindi, seleziona uno schema a cui mappare utilizzando l&#39;opzione [!UICONTROL Ricerca avanzata] o scorrendo l&#39;elenco degli schemi esistenti nel menu a discesa. Dopo aver selezionato uno schema, fornisci un nome e una descrizione per il flusso di dati.

![Nuova interfaccia del set di dati.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/new-dataset.png)

### Abilita diagnostica profili ed errori

+++Seleziona per visualizzare i passaggi per abilitare la diagnostica degli errori e l’acquisizione del profilo

Quindi, seleziona il **[!UICONTROL Set di dati profilo]** per abilitare il set di dati per Real-Time Customer Profile. Questo consente di creare una vista olistica degli attributi e dei comportamenti di un’entità. I dati di tutti i set di dati abilitati per il profilo verranno inclusi nel profilo e le modifiche verranno applicate al momento del salvataggio del flusso di dati.

[!UICONTROL Diagnostica errori] consente la generazione di messaggi di errore dettagliati per eventuali record errati che si verificano nel flusso di dati, mentre [!UICONTROL L&#39;acquisizione parziale] consente di acquisire dati contenenti errori, fino a una determinata soglia definita manualmente. Per ulteriori informazioni, consulta la [panoramica sull&#39;acquisizione batch parziale](../../../../../ingestion/batch-ingestion/partial.md).

+++

### Abilita avvisi

+++Selezionare questa opzione per visualizzare i passaggi per l&#39;attivazione degli avvisi

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi di origini tramite l&#39;interfaccia utente](../../alerts.md).

Dopo aver fornito i dettagli al flusso di dati, seleziona **[!UICONTROL Avanti]**.

+++

## Mappare i campi dati su uno schema XDM

Viene visualizzato il passaggio [!UICONTROL Mappatura] che fornisce un&#39;interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull&#39;utilizzo dell&#39;interfaccia mapper e dei campi calcolati, consulta la [guida dell&#39;interfaccia utente della preparazione dati](../../../../../data-prep/ui/mapping.md).

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Avanti]**.

![Interfaccia di mappatura.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/mapping.png)

## Pianificazione esecuzioni dell’acquisizione

Viene visualizzato il passaggio [!UICONTROL Pianificazione], che consente di configurare una pianificazione di acquisizione per acquisire automaticamente i dati di origine selezionati utilizzando le mappature configurate. Per impostazione predefinita, la pianificazione è impostata su `Once`. Per regolare la frequenza di acquisizione, seleziona **[!UICONTROL Frequenza]**, quindi scegli un&#39;opzione dal menu a discesa.

>[!TIP]
>
>L’intervallo e la retrocompilazione non sono visibili durante un’acquisizione una tantum.

![Interfaccia di pianificazione](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/schedule.png)

Se imposti la frequenza di acquisizione su `Minute`, `Hour`, `Day` o `Week`, devi impostare un intervallo per stabilire un intervallo di tempo impostato tra ogni acquisizione. Ad esempio, se la frequenza di acquisizione è impostata su `Day` e l&#39;intervallo è impostato su `15`, il flusso di dati verrà pianificato in modo da acquisire i dati ogni 15 giorni.

Durante questo passaggio, puoi anche abilitare **backfill** e definire una colonna per l&#39;acquisizione incrementale dei dati. La retrocompilazione viene utilizzata per acquisire i dati storici, mentre la colonna definita per l’acquisizione incrementale consente di distinguere i nuovi dati dai dati esistenti.

Per ulteriori informazioni sulle configurazioni di pianificazione, consulta la tabella seguente.

| Configurazione pianificazione | Descrizione |
| --- | --- |
| Frequenza | Configura la frequenza per indicare la frequenza con cui deve essere eseguito il flusso di dati. Puoi impostare la frequenza su: <ul><li>**Una volta**: imposta la frequenza su `once` per creare un&#39;acquisizione unica. Le configurazioni di intervallo e backfill non sono disponibili quando crei un flusso di dati di acquisizione una tantum. Per impostazione predefinita, la frequenza di pianificazione è impostata su una volta.</li><li>**Minuti**: imposta la frequenza su `minute` per pianificare il flusso di dati in modo da acquisire i dati al minuto.</li><li>**Ora**: imposta la frequenza su `hour` per pianificare il flusso di dati per acquisire i dati su base oraria.</li><li>**Giorno**: imposta la frequenza su `day` per pianificare il flusso di dati in modo da acquisire i dati su base giornaliera.</li><li>**Settimana**: imposta la frequenza su `week` per pianificare il flusso di dati in modo da acquisire i dati su base settimanale.</li></ul> |
| Intervallo | Dopo aver selezionato una frequenza, puoi configurare l’impostazione dell’intervallo per stabilire l’intervallo di tempo tra ogni acquisizione. Ad esempio, se imposti la frequenza su giorno e configuri l’intervallo su 15, il flusso di dati verrà eseguito ogni 15 giorni. Impossibile impostare l&#39;intervallo su zero. Il valore dell&#39;intervallo minimo accettato per ciascuna frequenza è il seguente:<ul><li>**Una volta**: n/d</li><li>**Minuto**: 15</li><li>**Ora**: 1</li><li>**Giorno**: 1</li><li>**Settimana**: 1</li></ul> |
| Ora di inizio | La marca temporale per l’esecuzione prevista, presentata in fuso orario UTC. |
| Retrocompilazione | La retrocompilazione determina quali dati vengono inizialmente acquisiti. Se la retrocompilazione è abilitata, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima acquisizione pianificata. Se la retrocompilazione è disattivata, verranno acquisiti solo i file caricati tra la prima esecuzione dell’acquisizione e l’ora di inizio. I file caricati prima dell’ora di inizio non verranno acquisiti. |

>[!NOTE]
>
>Per l&#39;acquisizione in batch, ogni flusso di dati successivo seleziona i file da acquisire dall&#39;origine in base alla marca temporale **ultima modifica**. Ciò significa che i flussi di dati batch selezionano dall’origine i file che sono nuovi o che sono stati modificati dall’ultima esecuzione del flusso. Inoltre, devi assicurarti che vi sia un intervallo di tempo sufficiente tra il caricamento dei file e l’esecuzione di un flusso pianificata, perché i file che non sono completamente caricati nell’account di archiviazione cloud prima dell’esecuzione del flusso pianificata potrebbero non essere raccolti per l’acquisizione.

Al termine della configurazione della pianificazione di acquisizione, seleziona **[!UICONTROL Avanti]**.

## Verifica il flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Rivedi]**, che consente di rivedere il nuovo flusso di dati prima che venga creato. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno di tale file di origine.
* **[!UICONTROL Assegna set di dati e mappa i campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.
* **[!UICONTROL Pianificazione]**: mostra il periodo, la frequenza e l&#39;intervallo attivi della pianificazione di acquisizione.

Dopo aver rivisto il flusso di dati, fai clic su **[!UICONTROL Fine]** e attendi un po&#39; di tempo per la creazione del flusso di dati.

![Pagina di revisione.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/review.png)

## Passaggi successivi

Seguendo questa esercitazione, è stato creato un flusso di dati per portare i dati batch dall&#39;origine [!DNL Merkury] all&#39;Experience Platform. Per ulteriori risorse, consulta la documentazione descritta di seguito.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni su tassi di acquisizione, successo ed errori. Per ulteriori informazioni su come monitorare il flusso di dati, visita l&#39;esercitazione su [account di monitoraggio e flussi di dati nell&#39;interfaccia utente](../../monitor.md).

### Aggiornare il flusso di dati

Per aggiornare le configurazioni per la pianificazione, la mappatura e le informazioni generali dei flussi di dati, visita il tutorial su [aggiornamento dei flussi di dati di origine nell&#39;interfaccia utente](../../update-dataflows.md)

### Eliminare il flusso di dati

È possibile eliminare i flussi di dati non più necessari o creati in modo errato utilizzando la funzione **[!UICONTROL Elimina]** disponibile nell&#39;area di lavoro **[!UICONTROL Flussi di dati]**. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l&#39;esercitazione su [eliminazione dei flussi di dati nell&#39;interfaccia utente](../../delete.md).
