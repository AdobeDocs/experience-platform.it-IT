---
title: Esportare i set di dati nelle destinazioni di archiviazione cloud
type: Tutorial
description: Scopri come esportare i set di dati da Adobe Experience Platform nella posizione di archiviazione cloud preferita.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: ad33eaa48928b25502ef279f000b92f31e1667ca
workflow-type: tm+mt
source-wordcount: '2573'
ht-degree: 8%

---

# Esportare i set di dati nelle destinazioni dell’archiviazione cloud

>[!AVAILABILITY]
>
>* Questa funzionalità è disponibile per i clienti che hanno acquistato il pacchetto Real-Time CDP Prime o Ultimate, Adobe Journey Optimizer o il Customer Journey Analytics. Per ulteriori informazioni, contatta il rappresentante del tuo Adobe.

In questo articolo viene illustrato il flusso di lavoro necessario per esportare [set di dati](/help/catalog/datasets/overview.md) da Adobe Experience Platform nel percorso di archiviazione cloud preferito, ad esempio [!DNL Amazon S3], percorsi SFTP o [!DNL Google Cloud Storage] tramite l&#39;interfaccia utente di Experience Platform.

Puoi anche utilizzare le API Experience Platform per esportare i set di dati. Per ulteriori informazioni, consulta l&#39;esercitazione sull&#39;esportazione di [dataset API](/help/destinations/api/export-datasets.md).

## Set di dati disponibili per l’esportazione {#datasets-to-export}

I set di dati che puoi esportare variano in base all’applicazione di Experience Platform (Real-Time CDP, Adobe Journey Optimizer), al livello (Prime o Ultimate) ed eventuali componenti aggiuntivi acquistati (ad esempio, Data Distiller).

Utilizza la tabella seguente per capire quali tipi di set di dati puoi esportare in base all’applicazione, al livello di prodotto ed eventuali componenti aggiuntivi acquistati:

<table>
<thead>
  <tr>
    <th>Applicazione/componente aggiuntivo</th>
    <th>Livello</th>
    <th>Set di dati disponibili per l’esportazione</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Real-Time CDP</td>
    <td>Prime</td>
    <td>Set di dati di profili ed eventi di esperienza creati nell’interfaccia utente di Experience Platform dopo l’acquisizione o la raccolta di dati tramite Sources, Web SDK, Mobile SDK, Analytics Data Connector ed Audience Manager.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>Set di dati di profili ed eventi di esperienza creati nell’interfaccia utente di Experience Platform dopo l’acquisizione o la raccolta di dati tramite Sources, Web SDK, Mobile SDK, Analytics Data Connector ed Audience Manager.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets">Set di dati snapshot profilo generato dal sistema</a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Prime</td>
    <td>Consulta la documentazione di <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a>.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td>Consulta la documentazione di <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a>.</td>
  </tr>
  <tr>
    <td>Customer Journey Analytics</td>
    <td>Tutto</td>
    <td> Set di dati di profili ed eventi di esperienza creati nell’interfaccia utente di Experience Platform dopo l’acquisizione o la raccolta di dati tramite Sources, Web SDK, Mobile SDK, Analytics Data Connector ed Audience Manager.</td>
  </tr>
  <tr>
    <td>Data Distiller</td>
    <td>Data Distiller (componente aggiuntivo)</td>
    <td>Set di dati derivati creati tramite Query Service.</td>
  </tr>
</tbody>
</table>

## Esercitazione video {#video-tutorial}

Guarda il video seguente per una spiegazione end-to-end del flusso di lavoro descritto in questa pagina, i vantaggi dell’utilizzo della funzionalità di esportazione dei set di dati e alcuni casi d’uso consigliati.

>[!VIDEO](https://video.tv.adobe.com/v/3424392/)

## Destinazioni supportati {#supported-destinations}

Al momento, puoi esportare i set di dati nelle destinazioni di archiviazione cloud evidenziate nella schermata ed elencate di seguito.

![Pagina del catalogo delle destinazioni che mostra quali destinazioni supportano le esportazioni dei set di dati.](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Quando attivare tipi di pubblico o esportare set di dati {#when-to-activate-audiences-or-activate-datasets}

Alcune destinazioni basate su file nel catalogo Experience Platform supportano sia l’attivazione del pubblico che l’esportazione di set di dati.

* Considera l’attivazione di tipi di pubblico quando desideri che i dati siano strutturati in profili raggruppati per interessi o qualifiche di pubblico.
* In alternativa, puoi prendere in considerazione le esportazioni di set di dati quando desideri esportare set di dati non elaborati, che non sono raggruppati o strutturati in base agli interessi o alle qualifiche del pubblico. Puoi utilizzare questi dati per reporting, flussi di lavoro sulla scienza dei dati e molti altri casi d’uso. In qualità di amministratore, ingegnere dati o analista, ad esempio, puoi esportare i dati da Experience Platform per sincronizzarli con il data warehouse, utilizzarli in strumenti di analisi BI, in strumenti di ML cloud esterni o archiviarli nel sistema per esigenze di archiviazione a lungo termine.

Questo documento contiene tutte le informazioni necessarie per esportare i set di dati. Se desideri attivare *tipi di pubblico* nell&#39;archiviazione cloud o nelle destinazioni di e-mail marketing, leggi [Attiva dati pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md).

## Prerequisiti {#prerequisites}

Per esportare i set di dati nelle destinazioni dell&#39;archiviazione cloud, è necessario avere [connesso a una destinazione](./connect-destination.md). Se non lo hai già fatto, vai al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

### Autorizzazioni richieste {#permissions}

Per esportare i set di dati, è necessario **[!UICONTROL Visualizzare le destinazioni]**, **[!UICONTROL Visualizzare i set di dati]** e **[!UICONTROL Gestire e attivare le destinazioni dei set di dati]** [accedere alle autorizzazioni di controllo](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per assicurarti di disporre delle autorizzazioni necessarie per esportare i set di dati e che la destinazione supporti l’esportazione dei set di dati, sfoglia il catalogo delle destinazioni. Se una destinazione dispone di un controllo **[!UICONTROL Attiva]** o **[!UICONTROL Esporta set di dati]**, si dispone delle autorizzazioni appropriate.

## Seleziona la destinazione {#select-destination}

Segui le istruzioni per selezionare una destinazione in cui puoi esportare i set di dati:

1. Vai a **[!UICONTROL Connessioni > Destinazioni]** e seleziona la scheda **[!UICONTROL Catalogo]**.

   ![Scheda Catalogo di destinazione con il controllo Catalogo evidenziato.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Seleziona **[!UICONTROL Attiva]** o **[!UICONTROL Esporta set di dati]** nella scheda corrispondente alla destinazione in cui desideri esportare i set di dati.

   ![Scheda Catalogo di destinazione con controllo di attivazione evidenziato.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Seleziona **[!UICONTROL Set di dati di tipo dati]** e seleziona la connessione di destinazione in cui desideri esportare i set di dati, quindi seleziona **[!UICONTROL Avanti]**.

>[!TIP]
> 
>Se si desidera impostare una nuova destinazione per esportare i set di dati, selezionare **[!UICONTROL Configura nuova destinazione]** per attivare il flusso di lavoro [Connetti alla destinazione](/help/destinations/ui/connect-destination.md).

![Flusso di lavoro di attivazione della destinazione con il controllo Set di dati evidenziato.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. Viene visualizzata la visualizzazione **[!UICONTROL Seleziona set di dati]**. Procedi alla sezione successiva per [selezionare i set di dati](#select-datasets) per l&#39;esportazione.

## Seleziona i set di dati {#select-datasets}

Utilizza le caselle di controllo a sinistra dei nomi dei set di dati per selezionare i set di dati da esportare nella destinazione, quindi seleziona **[!UICONTROL Successivo]**.

![Flusso di lavoro di esportazione del set di dati che mostra il passaggio Seleziona set di dati in cui è possibile selezionare i set di dati da esportare.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Pianificare l’esportazione di set di dati {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Opzioni di esportazione dei file per i set di dati"
>abstract="Seleziona **Esporta file incrementali** per esportare solo i dati aggiunti al set di dati dopo l’ultima esportazione. <br> La prima esportazione di file incrementali include tutti i dati del set di dati, agendo come backfill. I file incrementali futuri includono solo i dati aggiunti al set di dati dopo la prima esportazione. <br> Seleziona **Esporta file completi** per esportare l’appartenenza completa di ogni set di dati a ogni esportazione. "

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_header"
>title="Aggiornare la data di fine per questo flusso di dati"
>abstract="Aggiornare la data di fine per questo flusso di dati"

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_body"
>title="Aggiornare la data di fine per questo corpo del flusso di dati"
>abstract="A causa dei recenti aggiornamenti di questa destinazione, il flusso di dati ora richiede una data di fine. Adobe ha impostato una data di fine predefinita al 1° maggio 2025. Effettua l’aggiornamento alla data di fine desiderata altrimenti le esportazioni di dati si interromperanno alla fata predefinita."

Utilizza il passaggio **[!UICONTROL Pianificazione]** per:

* Imposta una data di inizio e una data di fine, nonché una cadenza di esportazione per le esportazioni dei set di dati.
* Configura se i file del set di dati esportati devono esportare l’appartenenza completa al set di dati o solo modifiche incrementali all’appartenenza a ogni occorrenza di esportazione.
* Personalizza il percorso della cartella nel percorso di archiviazione in cui devono essere esportati i set di dati. Ulteriori informazioni su come [modificare il percorso della cartella di esportazione](#edit-folder-path).

Utilizza il controllo **[!UICONTROL Modifica pianificazione]** nella pagina per modificare la frequenza di esportazione delle esportazioni e per scegliere se esportare file completi o incrementali.

![Il controllo Modifica pianificazione è evidenziato nel passaggio Pianificazione.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlight.png)

L&#39;opzione **[!UICONTROL Esporta file incrementali]** è selezionata per impostazione predefinita. Questo attiva un’esportazione di uno o più file che rappresentano un’istantanea completa del set di dati. I file successivi sono aggiunte incrementali al set di dati dall’esportazione precedente. È inoltre possibile selezionare **[!UICONTROL Esporta file completi]**. In questo caso, seleziona la frequenza **[!UICONTROL Una volta]** per un&#39;esportazione completa una tantum del set di dati.

>[!IMPORTANT]
>
>La prima esportazione incrementale di file include tutti i dati esistenti nel set di dati, che funziona come retrocompilazione. L’esportazione può contenere uno o più file.

![Flusso di lavoro di esportazione del set di dati che mostra il passaggio di pianificazione.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Utilizza il selettore **[!UICONTROL Frequenza]** per selezionare la frequenza di esportazione:

   * **[!UICONTROL Giornaliero]**: pianifica le esportazioni di file incrementali una volta al giorno, ogni giorno, al momento specificato.
   * **[!UICONTROL Oraria]**: pianifica esportazioni di file incrementali ogni 3, 6, 8 o 12 ore.

2. Utilizza il selettore **[!UICONTROL Ora]** per scegliere l&#39;ora del giorno, in formato [!DNL UTC], in cui eseguire l&#39;esportazione.

3. Utilizza il selettore **[!UICONTROL Data]** per scegliere l&#39;intervallo in cui deve essere eseguita l&#39;esportazione.

4. Seleziona **[!UICONTROL Salva]** per salvare la pianificazione e procedere al passaggio **[!UICONTROL Rivedi]**.

>[!NOTE]
> 
>Per le esportazioni di set di dati, i nomi dei file hanno un formato predefinito, predefinito, che non può essere modificato. Per ulteriori informazioni ed esempi di file esportati, vedere la sezione [Verifica dell&#39;esportazione del set di dati completata](#verify).

## Modificare il percorso della cartella {#edit-folder-path}

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template"
>title="Modificare il percorso della cartella"
>abstract="Utilizza diverse macro fornite per personalizzare il percorso della cartella in cui vengono esportati i set di dati."

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template_preview"
>title="Anteprima del percorso della cartella del set di dati"
>abstract="Ottieni un’anteprima della struttura di cartelle creata nel percorso di archiviazione in base alle macro aggiunte in questa finestra."

Seleziona **[!UICONTROL Modifica percorso cartella]** per personalizzare la struttura delle cartelle nel percorso di archiviazione in cui vengono depositati i set di dati esportati.

![Il controllo del percorso della cartella di modifica è evidenziato nel passaggio di pianificazione.](/help/destinations/assets/ui/export-datasets/edit-folder-path.png)

È possibile utilizzare diverse macro disponibili per personalizzare il nome di una cartella desiderata. Fare doppio clic su una macro per aggiungerla al percorso della cartella e utilizzare `/` tra le macro per separare le cartelle.

![Selezione di macro evidenziata nella finestra modale della cartella personalizzata.](/help/destinations/assets/ui/export-datasets/custom-folder-path-macros.png)

Dopo aver selezionato le macro desiderate, è possibile visualizzare un&#39;anteprima della struttura di cartelle che verrà creata nel percorso di archiviazione. Il primo livello nella struttura delle cartelle rappresenta il **[!UICONTROL percorso cartella]** indicato quando si è [connessi alla destinazione](/help/destinations/ui/connect-destination.md##set-up-connection-parameters) per esportare i set di dati.

![Anteprima del percorso della cartella evidenziata nella finestra modale della cartella personalizzata.](/help/destinations/assets/ui/export-datasets/custom-folder-path-preview.png)

## Controlla {#review}

Nella pagina **[!UICONTROL Rivedi]** puoi visualizzare un riepilogo della selezione. Seleziona **[!UICONTROL Annulla]** per interrompere il flusso, **[!UICONTROL Indietro]** per modificare le impostazioni oppure **[!UICONTROL Fine]** per confermare la selezione e iniziare a esportare i set di dati nella destinazione.

![Flusso di lavoro di esportazione del set di dati che mostra il passaggio di revisione.](/help/destinations/assets/ui/export-datasets/review.png)

## Verificare l’esportazione del set di dati {#verify}

Durante l&#39;esportazione dei set di dati, Experience Platform crea uno o più file `.json` o `.parquet` nel percorso di archiviazione fornito. I nuovi file verranno archiviati nel percorso di archiviazione in base alla pianificazione di esportazione fornita.

In Experience Platform viene creata una struttura di cartelle nel percorso di archiviazione specificato, in cui vengono depositati i file del set di dati esportati. Il modello di esportazione delle cartelle predefinito è illustrato di seguito, ma è possibile [personalizzare la struttura delle cartelle con le macro preferite](#edit-folder-path).

>[!TIP]
> 
>Il primo livello in questa struttura di cartelle - `folder-name-you-provided` - rappresenta il **[!UICONTROL percorso cartella]** che hai indicato quando [ti sei connesso alla destinazione](/help/destinations/ui/connect-destination.md##set-up-connection-parameters) per esportare i set di dati.

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

Il nome di file predefinito viene generato in modo casuale e garantisce che i nomi di file esportati siano univoci.

### File di set di dati di esempio {#sample-files}

La presenza di questi file nel percorso di archiviazione conferma la riuscita dell’esportazione. Per comprendere la struttura dei file esportati, è possibile scaricare un file [.parquet di esempio](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) o [.json](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

#### File di set di dati compressi {#compressed-dataset-files}

Nel flusso di lavoro [connetti a destinazione](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options), è possibile selezionare i file del set di dati esportati da comprimere, come illustrato di seguito:

![Tipo di file e selezione della compressione durante la connessione a una destinazione per l&#39;esportazione di set di dati.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Quando vengono compressi, si noti la differenza di formato tra i due tipi di file:

* Durante l&#39;esportazione di file JSON compressi, il formato del file esportato è `json.gz`
* Durante l&#39;esportazione di file parquet compressi, il formato del file esportato è `gz.parquet`

Le esportazioni in file JSON sono supportate *solo in modalità compressa*. Le esportazioni in file Parquet sono supportate in modalità compressa e non compressa.

## Rimuovere i set di dati dalle destinazioni {#remove-dataset}

Per rimuovere i set di dati da un flusso di dati esistente, effettua le seguenti operazioni:

1. Accedi a [interfaccia utente Experience Platform](https://experience.adobe.com/platform/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Sfoglia]** dall&#39;intestazione superiore per visualizzare i flussi di dati di destinazione esistenti.

   ![Visualizzazione esplorazione di destinazione con una connessione di destinazione visualizzata e il resto offuscato.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Seleziona l&#39;icona del filtro ![Icona filtro](/help/images/icons/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

2. Dalla colonna **[!UICONTROL Dati attivazione]**, seleziona il controllo Set di dati per visualizzare tutti i set di dati mappati a questo flusso di dati di esportazione.

   ![L&#39;opzione di navigazione dei set di dati disponibili è evidenziata nella colonna Dati di attivazione.](../assets/ui/export-datasets/go-to-datasets-data.png)

3. Viene visualizzata la pagina **[!UICONTROL Dati attivazione]** per la destinazione. Utilizza le caselle di controllo a sinistra dell&#39;elenco dei set di dati per selezionare i set di dati da rimuovere, quindi seleziona **[!UICONTROL Rimuovi set di dati]** nella barra a destra per attivare la finestra di dialogo di conferma della rimozione dei set di dati.

   ![Finestra di dialogo Rimuovi set di dati che mostra il controllo Rimuovi set di dati nella barra a destra.](../assets/ui/export-datasets/bulk-remove-datasets.png)

4. Nella finestra di dialogo di conferma, seleziona **[!UICONTROL Rimuovi]** per rimuovere immediatamente il set di dati dalle esportazioni nella destinazione.

   ![Finestra di dialogo che mostra l&#39;opzione Conferma rimozione set di dati dal flusso di dati.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Diritti di esportazione del set di dati {#licensing-entitlement}

Consulta i documenti di descrizione del prodotto per capire la quantità di dati che hai diritto di esportare per ogni applicazione di Experience Platform all’anno. Ad esempio, puoi visualizzare la descrizione del prodotto Real-Time CDP [qui](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

I diritti all’esportazione di dati per diverse applicazioni non sono additivi. Ciò significa, ad esempio, che se acquisti Real-Time CDP Ultimate e Adobe Journey Optimizer Ultimate, il diritto all’esportazione del profilo sarà il più grande tra i due diritti, in base alle descrizioni del prodotto. Il volume di adesioni viene calcolato moltiplicando il numero totale di profili con licenza per 500 KB per Real-Time CDP Prime o 700 KB per Real-Time CDP Ultimate per determinare il volume di dati a cui hai diritto.

Se invece sono stati acquistati componenti aggiuntivi come Data Distiller, il limite di esportazione dei dati a cui hai diritto rappresenta la somma del livello prodotto e del componente aggiuntivo.

Puoi visualizzare e tenere traccia delle esportazioni dei profili rispetto ai limiti contrattuali nel [dashboard utilizzo licenze](/help/landing/license-usage-and-guardrails/license-usage-dashboard.md).

## Limitazioni note {#known-limitations}

Tieni presente le seguenti limitazioni per il rilascio di disponibilità generale delle esportazioni di set di dati:

* Attualmente, è possibile esportare solo file incrementali e non è possibile selezionare una data di fine per le esportazioni dei set di dati.
* Experience Platform può esportare più file anche per set di dati di piccole dimensioni. L’esportazione dei set di dati è progettata per l’integrazione tra sistemi e ottimizzata per le prestazioni, pertanto il numero di file esportati non è personalizzabile.
* I nomi di file esportati non sono attualmente personalizzabili.
* I set di dati creati tramite API non sono attualmente disponibili per l’esportazione.
* L’interfaccia utente non ti blocca attualmente l’eliminazione di un set di dati in fase di esportazione in una destinazione. Non eliminare i set di dati da esportare nelle destinazioni. [Rimuovere il set di dati](#remove-dataset) da un flusso di dati di destinazione prima di eliminarlo.
* Le metriche di monitoraggio per le esportazioni di set di dati sono attualmente combinate con i numeri per le esportazioni di profili, pertanto non riflettono i numeri di esportazione effettivi.
* I dati con una marca temporale precedente ai 365 giorni sono esclusi dalle esportazioni dei set di dati. Per ulteriori informazioni, visualizza [guardrail per esportazioni di set di dati pianificate](/help/destinations/guardrails.md#guardrails-for-scheduled-dataset-exports)

## Domande frequenti {#faq}

**È possibile generare un file senza una cartella se si salva solo in `/` come percorso della cartella? Inoltre, se non è necessario un percorso di cartella, in che modo verranno generati i file con nomi duplicati in una cartella o in un percorso?**

+++
A partire dalla versione di settembre 2024, è possibile personalizzare il nome della cartella e persino utilizzare `/` per esportare i file per tutti i set di dati nella stessa cartella. Questo Adobe non è consigliato per le destinazioni che esportano più set di dati, in quanto i nomi di file generati dal sistema che appartengono a set di dati diversi verranno combinati nella stessa cartella.
+++

**È possibile indirizzare il file manifesto a una cartella e i file di dati a un&#39;altra cartella?**

+++
No, non è possibile copiare il file manifesto in una posizione diversa.
+++

**È possibile controllare la sequenza o la tempistica di consegna dei file?**

+++
Sono disponibili opzioni per pianificare l’esportazione. Non sono disponibili opzioni per ritardare o sequenziare la copia dei file. Vengono copiati nel percorso di archiviazione non appena vengono generati.
+++

**Quali formati sono disponibili per il file manifesto?**

+++
Il file manifesto è in formato .json.
+++

**Esiste disponibilità API per il file manifesto?**

+++
Non è disponibile alcuna API per il file manifesto, ma include un elenco di file che comprendono l’esportazione.
+++

**È possibile aggiungere ulteriori dettagli al file manifesto (ad esempio, il numero di record)? In caso affermativo, in che modo?**

+++
Non è possibile aggiungere ulteriori informazioni al file manifesto. Il conteggio dei record è disponibile tramite l&#39;entità `flowRun` (interrogabile tramite API). Ulteriori informazioni nel monitoraggio delle destinazioni.
+++

**Come vengono suddivisi i file di dati? Quanti record per file?**

+++
I file di dati vengono suddivisi in base al partizionamento predefinito nel data lake di Experience Platform. I set di dati più grandi hanno un numero più elevato di partizioni. Il partizionamento predefinito non è configurabile dall&#39;utente in quanto è ottimizzato per la lettura.
+++

**È possibile impostare una soglia (numero di record per file)?**

+++
No, non è possibile.
+++

**Come si invia di nuovo un set di dati nel caso in cui l&#39;invio iniziale non sia valido?**

+++
I tentativi vengono eseguiti automaticamente per la maggior parte dei tipi di errori di sistema.
+++