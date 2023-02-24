---
title: (Beta) Esportare i set di dati nelle destinazioni di archiviazione cloud
type: Tutorial
description: Scopri come esportare i set di dati da Adobe Experience Platform nella posizione di archiviazione cloud preferita.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: aebb1494a6ed667730997048d30a2ca3e00f9452
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 1%

---

# (Beta) Esportare i set di dati nelle destinazioni di archiviazione cloud

>[!IMPORTANT]
>
>* La funzionalità di esportazione dei set di dati è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.
>* Questa funzionalità beta supporta l’esportazione di dati di prima generazione, come definito in Real-time Customer Data Platform [descrizione del prodotto](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* Questa funzionalità è disponibile per i clienti che hanno acquistato il pacchetto Real-Time CDP Prime e Ultimate. Per ulteriori informazioni, contatta il tuo rappresentante Adobe.


Questo articolo spiega il flusso di lavoro necessario per esportare [set di dati](/help/catalog/datasets/overview.md) da Adobe Experience Platform alla posizione di archiviazione cloud preferita, ad esempio [!DNL Amazon S3], posizioni SFTP o [!DNL Google Cloud Storage] utilizzando l’interfaccia utente di Experience Platform.

Puoi anche utilizzare le API di Experience Platform per esportare i set di dati. Leggi la sezione [esercitazione API sui set di dati di esportazione](/help/destinations/api/export-datasets.md) per ulteriori informazioni.

## Quando attivare segmenti o esportare set di dati {#when-to-activate-segments-or-activate-datasets}

Alcune destinazioni basate su file nel catalogo di Experience Platform supportano sia l’attivazione dei segmenti che l’esportazione dei set di dati.

* Prendi in considerazione l’attivazione di segmenti quando desideri che i dati siano strutturati in profili raggruppati per interessi o qualifiche di pubblico.
* In alternativa, considera le esportazioni dei set di dati quando desideri esportare set di dati non elaborati, che non sono raggruppati o strutturati in base a interessi o qualifiche di pubblico. Puoi utilizzare questi dati per generare rapporti, flussi di lavoro di scienza dei dati, per soddisfare i requisiti di conformità e molti altri casi d’uso.

Questo documento contiene tutte le informazioni necessarie per esportare i set di dati. Per attivare i segmenti nell’archiviazione cloud o nelle destinazioni di marketing e-mail, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md).

## Prerequisiti {#prerequisites}

Per esportare i set di dati nelle destinazioni di archiviazione cloud, è necessario aver completato l&#39;esportazione [connesso a una destinazione](./connect-destination.md). Se non lo hai già fatto, vai alla [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

### Autorizzazioni necessarie {#permissions}

Per esportare i set di dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Visualizzare le destinazioni]**, **[!UICONTROL Attivare le destinazioni]** e **[!UICONTROL Gestire e attivare le destinazioni del set di dati]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per assicurarti di disporre delle autorizzazioni necessarie per esportare i set di dati e che la destinazione supporti l’esportazione dei set di dati, sfoglia il catalogo delle destinazioni. Se una destinazione ha un **[!UICONTROL Attiva]** o **[!UICONTROL Esportare i set di dati]** quindi disponi delle autorizzazioni appropriate.

## Seleziona la destinazione {#select-destination}

Segui le istruzioni per selezionare una destinazione in cui esportare i set di dati:

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, quindi seleziona la **[!UICONTROL Catalogo]** scheda .

   ![Scheda Catalogo di destinazione con controllo Catalogo evidenziato.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Seleziona **[!UICONTROL Attiva]** o **[!UICONTROL Esportare i set di dati]** sulla scheda corrispondente alla destinazione in cui desideri esportare i set di dati.

   ![Scheda del catalogo di destinazione con il controllo Attiva evidenziato.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Seleziona **[!UICONTROL Set di dati di tipo]** e selezionare la connessione di destinazione in cui si desidera esportare i set di dati, quindi selezionare **[!UICONTROL Successivo]**.

>[!TIP]
> 
>Se desideri impostare una nuova destinazione per l&#39;esportazione dei set di dati, seleziona **[!UICONTROL Configurare una nuova destinazione]** per attivare [Connetti alla destinazione](/help/destinations/ui/connect-destination.md) workflow.

![Flusso di lavoro di attivazione della destinazione con il controllo Dataset evidenziato.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. La **[!UICONTROL Seleziona set di dati]** viene visualizzata la vista. Procedi alla sezione successiva a [seleziona i set di dati](#select-datasets) per l&#39;esportazione.

## Seleziona i set di dati {#select-datasets}

Utilizza le caselle di controllo a sinistra dei nomi dei set di dati per selezionare i set di dati da esportare nella destinazione, quindi seleziona **[!UICONTROL Successivo]**.

![Flusso di lavoro di esportazione del set di dati che mostra il passaggio Seleziona set di dati in cui puoi selezionare i set di dati da esportare.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Pianificazione esportazione set di dati {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Opzioni di esportazione dei file per i set di dati"
>abstract="Seleziona **Esportare file incrementali** per esportare solo i dati aggiunti al set di dati dall’ultima esportazione. <br> La prima esportazione di file incrementali include tutti i dati del set di dati, fungendo da backfill. I file incrementali futuri includono solo i dati aggiunti al set di dati dalla prima esportazione."

In **[!UICONTROL Pianificazione]** puoi impostare una data di inizio e una cadenza di esportazione per le esportazioni dei set di dati.

La **[!UICONTROL Esportare file incrementali]** viene selezionata automaticamente. Questo attiva un’esportazione in cui il primo file è uno snapshot completo del set di dati e i file successivi sono aggiunte incrementali al set di dati dall’esportazione precedente.

>[!IMPORTANT]
>
>Il primo file incrementale esportato include tutti i dati esistenti nel set di dati, funzionando come backfill.

![Flusso di lavoro di esportazione del set di dati che mostra la fase di pianificazione.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Utilizza la **[!UICONTROL Frequenza]** selettore per selezionare la frequenza di esportazione:

   * **[!UICONTROL Giornaliero]**: Pianifica esportazioni incrementali di file una volta al giorno, ogni giorno, al momento specificato.
   * **[!UICONTROL Orario]**: Pianifica esportazioni di file incrementali ogni 3, 6, 8 o 12 ore.

2. Utilizza la **[!UICONTROL Time]** selettore per scegliere l’ora del giorno, in [!DNL UTC] formato, quando deve aver luogo l&#39;esportazione.

3. Utilizza la **[!UICONTROL Data]** selettore per scegliere l’intervallo in cui deve avvenire l’esportazione. Nella versione beta della funzione non è possibile impostare una data di fine per le esportazioni. Per ulteriori informazioni, consulta la sezione [limitazioni note](#known-limitations) sezione .

4. Seleziona **[!UICONTROL Successivo]** per salvare la pianificazione e procedere alla **[!UICONTROL Revisione]** passo.

>[!NOTE]
> 
>Per le esportazioni di set di dati, i nomi dei file hanno un formato predefinito e predefinito che non può essere modificato. Vedi la sezione [Verifica esportazione set di dati riuscita](#verify) per ulteriori informazioni ed esempi di file esportati.

## Revisione {#review}

Sulla **[!UICONTROL Revisione]** per visualizzare un riepilogo della selezione. Seleziona **[!UICONTROL Annulla]** per interrompere il flusso, **[!UICONTROL Indietro]** per modificare le impostazioni, oppure **[!UICONTROL Fine]** per confermare la selezione e iniziare l&#39;esportazione dei set di dati nella destinazione.

![Flusso di lavoro di esportazione del set di dati che mostra il passaggio di revisione.](/help/destinations/assets/ui/export-datasets/review.png)

## Verifica esportazione set di dati riuscita {#verify}

Quando si esportano i set di dati, Experience Platform crea un `.json` o `.parquet` nel percorso di archiviazione fornito. Attendi che un nuovo file venga depositato nel percorso di archiviazione in base alla pianificazione di esportazione fornita.

Experience Platform crea una struttura di cartelle nel percorso di archiviazione specificato, in cui vengono archiviati i file di set di dati esportati. Per ogni esportazione viene creata una nuova cartella, seguendo il pattern seguente:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

Il nome file predefinito viene generato in modo casuale e assicura che i nomi dei file esportati siano univoci.

### File di set di dati di esempio {#sample-files}

La presenza di questi file nel percorso di archiviazione conferma l’esito di un’esportazione. Per comprendere la struttura dei file esportati, puoi scaricare un esempio [file .parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) o [file .json](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

## Rimuovi set di dati dalla destinazione {#remove-dataset}

Per rimuovere un set di dati da un flusso di dati esistente, effettua le seguenti operazioni:

1. Accedi a [Interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Sfoglia]** dall’intestazione superiore per visualizzare i flussi di dati di destinazione esistenti.

   ![Visualizzazione Sfoglia di destinazione con una connessione di destinazione mostrata e il resto sfocato.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Seleziona l’icona del filtro ![Icona Filtro](../assets/ui/edit-activation/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello di ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

1. Da **[!UICONTROL Dati di attivazione]** seleziona il controllo set di dati per visualizzare tutti i set di dati mappati a questo flusso di dati di esportazione.

   ![L’opzione di navigazione dei set di dati disponibili evidenziata nella colonna Dati di attivazione .](../assets/ui/export-datasets/go-to-datasets-data.png)

1. La **[!UICONTROL Dati di attivazione]** viene visualizzata la pagina della destinazione. Seleziona **[!UICONTROL Rimuovi set di dati]** nella barra a destra per attivare la finestra di dialogo di conferma della rimozione del set di dati.

   ![Finestra di dialogo Rimuovi set di dati che mostra il controllo Rimuovi set di dati nella barra a destra.](../assets/ui/export-datasets/remove-dataset-control.png)

1. Nella finestra di dialogo di conferma, seleziona **[!UICONTROL Rimuovi]** per rimuovere immediatamente il set di dati dalle esportazioni alla destinazione.

   ![Finestra di dialogo che mostra l’opzione Conferma rimozione set di dati dal flusso di dati.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Limitazioni note {#known-limitations}

Tieni presente le seguenti limitazioni per la versione beta delle esportazioni di set di dati:

* Attualmente esiste un&#39;autorizzazione unica (**[!UICONTROL Gestire e attivare le destinazioni del set di dati]**) che include la gestione e l’attivazione delle autorizzazioni sulle destinazioni dei set di dati. Questi controlli verranno suddivisi in futuro in autorizzazioni più granulari. Consulta la sezione [autorizzazioni necessarie](#permissions) per un elenco completo delle autorizzazioni necessarie per esportare i set di dati.
* Attualmente, è possibile esportare solo file incrementali e non è possibile selezionare una data di fine per le esportazioni dei set di dati.
* I nomi dei file esportati non sono attualmente personalizzabili.
* L’interfaccia utente al momento non ti blocca l’eliminazione di un set di dati da esportare in una destinazione. Non eliminare i set di dati che vengono esportati nelle destinazioni. [Rimuovere il set di dati](#remove-dataset) da un flusso di dati di destinazione prima di eliminarlo.
* Le metriche di monitoraggio per le esportazioni di set di dati sono attualmente unite ai numeri per le esportazioni di profili in modo che non riflettano i veri numeri di esportazione.
