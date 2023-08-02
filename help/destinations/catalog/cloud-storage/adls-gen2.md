---
title: Connessione di Azure Data Lake Storage Gen2
description: Scopri come connettersi ad Azure Data Lake Storage Gen2 per attivare tipi di pubblico ed esportare set di dati.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 1%

---

# [!DNL Azure Data Lake Storage Gen2] connessione

## Panoramica {#overview}

Leggi questa pagina per scoprire come creare una connessione in uscita al tuo [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2]) data lake per esportare periodicamente file di dati da Experienci Platform.

## Connetti al tuo [!DNL ADLS Gen2] archiviazione tramite API o interfaccia utente {#connect-api-or-ui}

* Per connettersi al tuo [!DNL ADLS Gen2] percorso di archiviazione tramite l’interfaccia utente di Platform, leggi le sezioni [Connetti alla destinazione](#connect) e [Attiva il pubblico in questa destinazione](#activate) di seguito.
* Per connettersi al tuo [!DNL ADLS Gen2] percorso di archiviazione a livello di programmazione, leggere [Attiva i tipi di pubblico in destinazioni basate su file utilizzando l’esercitazione API del servizio Flusso](../../api/activate-segments-file-based-destinations.md).

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive tutti i tipi di pubblico che puoi esportare in questa destinazione.

Questa destinazione supporta l’attivazione di tutti i tipi di pubblico generati tramite l’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md).

*Inoltre*, questa destinazione supporta anche l’attivazione dei tipi di pubblico descritti nella tabella seguente.

| Tipo di pubblico | Descrizione |
---------|----------|
| Caricamenti personalizzati | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema applicabili (ad esempio il tuo PPID), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni su [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](/help/destinations/ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL URL]**: endpoint per [!DNL Azure Data Lake Storage Gen2]. Il modello di endpoint è: `abfss://<container>@<accountname>.dfs.core.windows.net`.
* **[!UICONTROL Tenant]**: informazioni tenant contenenti l’applicazione.
* **[!UICONTROL ID entità servizio]**: ID client dell’applicazione.
* **[!UICONTROL Chiave principale servizio]**: chiave dell’applicazione.
* **[!UICONTROL Chiave di crittografia]**: in alternativa, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

  ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Inserisci i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: inserisci il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
* **[!UICONTROL Percorso cartella]**: immetti il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Tipo di file]**: seleziona l’Experience Platform di formato da utilizzare per i file esportati. Quando si seleziona [!UICONTROL CSV] , è inoltre possibile [configurare le opzioni di formattazione del file](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato di compressione]**: seleziona il tipo di compressione che Experienci Platform deve utilizzare per i file esportati.
* **[!UICONTROL Includi file manifesto]**: attiva questa opzione se desideri che le esportazioni includano un file JSON manifesto che contiene informazioni sulla posizione di esportazione, sulle dimensioni di esportazione e altro ancora.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

### Pianificazione {#scheduling}

In **[!UICONTROL Pianificazione]** passaggio, puoi [impostare la pianificazione di esportazione](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) per [!DNL Azure Data Lake Storage Gen2] e puoi anche [configurare il nome dei file esportati](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappare attributi e identità {#map}

In **[!UICONTROL Mappatura]** fase, puoi selezionare l’attributo e i campi di identità da esportare per i profili. Puoi anche scegliere di modificare le intestazioni nel file esportato con qualsiasi nome descrittivo. Per ulteriori informazioni, vedere [passaggio di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) nell’esercitazione dell’interfaccia utente attiva destinazioni batch.

## (Beta) Esportare i set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, consulta le esercitazioni:

* Procedura [esportare i set di dati utilizzando l’interfaccia utente di Platform](/help/destinations/ui/export-datasets.md).
* Procedura [esportare i set di dati a livello di programmazione utilizzando l’API del servizio Flusso](/help/destinations/api/export-datasets.md).

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla [!DNL Azure Data Lake Storage Gen2] e assicurati che i file esportati contengano le popolazioni di profilo previste.
