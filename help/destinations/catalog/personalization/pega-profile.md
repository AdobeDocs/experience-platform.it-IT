---
title: Connettore profilo Pega
description: Utilizza il Connettore profilo Pega per Amazon S3 in Adobe Experience Platform per esportare dati di profilo completi o incrementali, o entrambi, nell’archivio cloud Amazon S3. In Pega Customer Decision Hub, i processi di dati possono essere pianificati in Customer Profile Designer per importare periodicamente dati di profilo dall’archiviazione Amazon S3.
source-git-commit: bdc6ef162e9684065b60a13670848dac64be21fd
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 1%

---


# Connettore profilo Pega

## Panoramica {#overview}

Utilizza la [!DNL Pega Profile Connector] in Adobe Experience Platform per creare una connessione in uscita diretta al tuo [!DNL Amazon Web Services] (AWS) Archiviazione S3 per esportare periodicamente i dati del profilo in file CSV da Adobe Experience Platform nei bucket S3. In [!DNL Pega Customer Decision Hub], è possibile pianificare i processi dati per importare i dati del profilo dall&#39;archiviazione S3 per aggiornare [!DNL Pega Customer Decision Hub] profilo.

Questo connettore consente di impostare l’esportazione iniziale dei dati del profilo e contribuisce inoltre a sincronizzare periodicamente i nuovi profili in [!DNL Pega Customer Decision Hub].  Disporre di dati aggiornati in Customer Decision Hub offre una visualizzazione migliore e aggiornata della base di dati dei clienti per le decisioni migliori da adottare in futuro.

>[!IMPORTANT]
>
>Questa pagina della documentazione è stata creata da Pegasystems. Per qualsiasi domanda o richiesta di aggiornamento, si prega di contattare Pega direttamente [qui](mailto:support@pega.com).

## Casi d’uso

Per aiutarti a capire meglio come e quando utilizzare la [!DNL Pega Profile Connector] destinazione : di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d&#39;uso 1

Un addetto al marketing desidera inizialmente configurare [!DNL Pega Customer Decision Hub] con dati di profilo caricati da Adobe Experience Platform. Si tratta di un carico completo iniziale seguito da carichi delta su base programmata.

### Caso d&#39;uso 2

Un addetto al marketing desidera disporre di dati di profilo aggiornati da Adobe Experience Platform disponibili in [!DNL Pega Customer Decision Hub] che migliora costantemente le informazioni Pega sui profili dei clienti.

## Prerequisiti {#prerequisites}

Prima di poter utilizzare questa destinazione per esportare dati da Adobe Experience Platform e importare profili in [!DNL Pega Customer Decision Hub], assicurati di completare i seguenti prerequisiti:

* Configura [!DNL Amazon S3] bucket e il percorso della cartella da utilizzare per l’esportazione e l’importazione di file di dati.
* Configura le [!DNL Amazon S3] chiave di accesso e [!DNL Amazon S3] chiave segreta: In [!DNL Amazon S3], genera un `access key - secret access key` per concedere a Platform l’accesso al tuo [!DNL Amazon S3] conto.
* Per connettere ed esportare correttamente i dati al tuo [!DNL Amazon S3] posizione di archiviazione, creare un utente IAM (Identity and Access Management) per [!DNL Platform] in [!DNL Amazon S3] e assegna autorizzazioni quali `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* Assicurati che [!DNL Pega Customer Decision Hub] l’istanza viene aggiornata alla versione 8.8 o successiva.

## Identità supportate {#supported-identities}

[!DNL Pega Customer Decision Hub] supporta l’attivazione di ID utente personalizzati descritti nella tabella seguente. Per ulteriori dettagli, consulta [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione |
|---|---|
| *CustomerID* | Identificatore utente comune che identifica in modo univoco un profilo in [!DNL Pega Customer Decision Hub] e Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Batch]** | Le destinazioni batch esportano file su piattaforme downstream con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni [destinazioni batch basate su file](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica a destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, compila i campi richiesti e seleziona **[!UICONTROL Connetti alla destinazione]**.

* **[!DNL Amazon S3]chiave di accesso** e **[!DNL Amazon S3]chiave segreta**: In [!DNL Amazon S3], genera un `access key - secret access key` per concedere a Adobe Experience Platform l’accesso al tuo [!DNL Amazon S3] conto. Ulteriori informazioni nel [Documentazione di Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Compila i dettagli della destinazione {#destination-details}

Dopo aver stabilito la connessione di autenticazione a [!DNL Amazon S3], fornire le seguenti informazioni per la destinazione:

![Immagine della schermata dell’interfaccia utente che mostra i campi completati per i dettagli della destinazione del connettore profilo Pega](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

Per configurare i dettagli della destinazione, compila i campi richiesti e seleziona **[!UICONTROL Successivo]**. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione della destinazione.
* **[!UICONTROL Nome blocco]**: immetti il nome della [!DNL Amazon S3] bucket utilizzato da questa destinazione.
* **[!UICONTROL Percorso cartella]**: immetti il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Tipo di compressione]**: Selezionare il tipo di compressione GZIP o NONE.

>[!TIP]
>
>Nel flusso di lavoro di destinazione di connessione puoi creare una cartella personalizzata nell’archivio Amazon S3 per file di segmento esportato. Leggi [Utilizzare le macro per creare una cartella nel percorso di archiviazione](/help/destinations/catalog/cloud-storage/overview.md#use-macros) per istruzioni.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Mappare attributi e identità {#map}

In **[!UICONTROL Mappatura]** puoi selezionare i campi attributo e identità da esportare per i profili. Puoi anche scegliere di modificare le intestazioni nel file esportato con qualsiasi nome descrittivo che desideri. Per ulteriori informazioni, consulta la sezione [fase di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) nell’esercitazione per l’interfaccia utente attiva destinazioni batch .

## Convalida esportazione dati {#exported-data}

Per [!DNL Pega Profile Connector] destinazioni, [!DNL Platform] crea un `.csv` file nel percorso di archiviazione Amazon S3 fornito dall&#39;utente. Per ulteriori informazioni sui file, vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) nell’esercitazione sull’attivazione dei segmenti.

Un&#39;importazione corretta dei dati del profilo da S3 inserisce i dati nel [!DNL Pega Customer] archivio dati del profilo. I dati del profilo cliente importati possono essere convalidati in [!DNL Pega Customer Profile Designer] , come illustrato nella figura seguente.
![Immagine della schermata dell’interfaccia utente in cui è possibile convalidare i dati del profilo di Adobe in Progettazione profili cliente](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

In [!DNL Pega Customer Decision Hub], gli amministratori di dati possono configurare i processi di elaborazione dati in [!DNL Customer Profile Designer] importare periodicamente dati di profilo da S3, come illustrato nella figura riportata di seguito. Consulta la sezione [risorse aggiuntive](#additional-resources) per ulteriori informazioni su come configurare i processi di dati per importare i dati di profilo da [!DNL Amazon S3].
![Immagine della schermata dell’interfaccia utente per configurare i processi di dati in Progettazione profili cliente](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## Risorse aggiuntive {#additional-resources}

Vedi [Importare processi di dati](https://academy.pega.com/topic/import-data-jobs/v1) in [!DNL Pega Customer Decision Hub].

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).



