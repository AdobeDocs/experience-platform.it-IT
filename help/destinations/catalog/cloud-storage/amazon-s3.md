---
title: Connessione Amazon S3
description: Crea una connessione in uscita allo storage Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV da Adobe Experience Platform nei bucket S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 17%

---

# [!DNL Amazon S3] connessione {#s3-connection}

## Registro modifiche destinazione {#changelog}

+++ Visualizza changelog


| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Gennaio 2024 | Aggiornamento della funzionalità e della documentazione | Il connettore di destinazione Amazon S3 ora supporta un nuovo tipo di autenticazione ruolo presunto. Per ulteriori informazioni, consulta [sezione di autenticazione](#assumed-role-authentication). |
| Luglio 2023 | Aggiornamento della funzionalità e della documentazione | Con la versione di Experience Platform di luglio 2023, la [!DNL Amazon S3] destinazione offre nuove funzionalità, come elencato di seguito: <br><ul><li>[Supporto per l’esportazione del set di dati](/help/destinations/ui/export-datasets.md)</li><li>Nuove [opzioni di denominazione file](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>Possibilità di impostare intestazioni di file personalizzate nei file esportati tramite il [passaggio di mappatura migliorato](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Possibilità di personalizzare la formattazione dei file di dati CSV esportati](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## Connetti al tuo [!DNL Amazon S3] archiviazione tramite API o interfaccia utente {#connect-api-or-ui}

* Per connettersi al tuo [!DNL Amazon S3] percorso di archiviazione tramite l’interfaccia utente di Platform, leggi le sezioni [Connetti alla destinazione](#connect) e [Attiva il pubblico in questa destinazione](#activate) di seguito.
* Per connettersi al tuo [!DNL Amazon S3] percorso di archiviazione a livello di programmazione, leggere la guida su come [attivare i tipi di pubblico nelle destinazioni basate su file tramite l’esercitazione API del servizio Flow](../../api/activate-segments-file-based-destinations.md).

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportati | Descrizione |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni su [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Il tipo di esportazione basato su profilo Amazon S3 è evidenziato nella UU.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Esportare i set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, consulta le esercitazioni:

* Procedura [esportare i set di dati utilizzando l’interfaccia utente di Platform](/help/destinations/ui/export-datasets.md).
* Procedura [esportare i set di dati a livello di programmazione utilizzando l’API del servizio Flusso](/help/destinations/api/export-datasets.md).

## Formato file dei dati esportati {#file-format}

Durante l’esportazione *dati sul pubblico*, Platform crea un `.csv`, `parquet`, o `.json` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedere [formati di file supportati per l’esportazione](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) nell’esercitazione di Audience Activation.

Durante l’esportazione *set di dati*, Platform crea un `.parquet` o `.json` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedere [verificare la corretta esportazione del set di dati](../../ui/export-datasets.md#verify) nell’esercitazione esportare set di dati.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestire le destinazioni]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Chiave pubblica RSA"
>abstract="Facoltativamente, puoi collegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Nel collegamento alla documentazione qui di seguito, trovi un esempio di chiave formattata correttamente."

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**. La destinazione Amazon S3 supporta due metodi di autenticazione:

* Autenticazione chiave di accesso e chiave segreta
* Autenticazione del ruolo assunta

#### Autenticazione chiave di accesso e chiave segreta

Utilizza questo metodo di autenticazione quando vuoi inserire la chiave di accesso e la chiave segreta di Amazon S3 per consentire ad Experienci Platform di esportare dati nelle proprietà di Amazon S3.

![Immagine dei campi obbligatori quando si seleziona l’autenticazione con chiave di accesso e chiave segreta.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]chiave di accesso** e **[!DNL Amazon S3]chiave segreta**: In [!DNL Amazon S3], genera un `access key - secret access key` coppia per concedere a Platform l’accesso al tuo [!DNL Amazon S3] account. Per ulteriori informazioni, consulta [Documentazione di Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Chiave di crittografia]**: in alternativa, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

  ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Ruolo assunto {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="Autenticazione del ruolo assunta"
>abstract="Utilizza questo tipo di autenticazione se preferisci non condividere le chiavi dell’account e le chiavi segrete con Adobe. Al contrario, Experience Platform si connette alla posizione Amazon S3 utilizzando l’accesso basato sul ruolo. Incolla l’ARN del ruolo creato in AWS per l’utente Adobe. Il pattern è simile a `arn:aws:iam::800873819705:role/destinations-role-customer` "

![Immagine dei campi obbligatori quando si seleziona l’autenticazione per il ruolo assunto.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

Utilizza questo tipo di autenticazione se preferisci non condividere le chiavi dell’account e le chiavi segrete con Adobe. Al contrario, Experienci Platform si connette alla posizione Amazon S3 utilizzando l’accesso basato su ruolo.

A questo scopo, devi creare nella console AWS un utente che si presume sia, ad Adobe, con [autorizzazioni richieste a destra](#required-s3-permission) per scrivere nei bucket Amazon S3. Creare un **[!UICONTROL Entità attendibile]** in AWS con l’account Adobe **[!UICONTROL 670664943635]**. Per ulteriori informazioni, consulta [Documentazione di AWS sulla creazione di ruoli](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

* **[!DNL Role]**: incolla l’ARN del ruolo creato in AWS per l’utente Adobe. Il pattern è simile a `arn:aws:iam::800873819705:role/destinations-role-customer`.
* **[!UICONTROL Chiave di crittografia]**: in alternativa, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

### Inserire i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Nome del bucket"
>abstract="Deve contenere da 3 e 63 caratteri. Deve iniziare e terminare con una lettera o un numero. Deve contenere solo lettere minuscole, numeri o trattini (-). Non deve essere formattato come un indirizzo IP (ad esempio, 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Percorso della cartella"
>abstract="Deve contenere solo caratteri A-Z, a-z, 0-9 e può includere i seguenti caratteri speciali: `/!-_.'()"^[]+$%.*"`. Per creare una cartella per file di pubblico, inserisci la macro `/%SEGMENT_NAME%` o `/%SEGMENT_ID%` o `/%SEGMENT_NAME%/%SEGMENT_ID%` nel campo di testo. Le macro possono essere inserite solo alla fine del percorso della cartella. Nella documentazione trovi alcuni esempi di macro."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=it#use-macros" text="Utilizzare le macro per creare una cartella nel percorso di archiviazione"

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: immetti una descrizione di questa destinazione.
* **[!UICONTROL Nome bucket]**: immetti il nome del [!DNL Amazon S3] bucket da utilizzare per questa destinazione.
* **[!UICONTROL Percorso cartella]**: immetti il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Tipo di file]**: seleziona l’Experience Platform di formato da utilizzare per i file esportati. Quando si seleziona [!UICONTROL CSV] , è inoltre possibile [configurare le opzioni di formattazione del file](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato di compressione]**: seleziona il tipo di compressione che Experienci Platform deve utilizzare per i file esportati.
* **[!UICONTROL Includi file manifesto]**: attiva questa opzione se desideri che le esportazioni includano un file JSON manifesto contenente informazioni sulla posizione di esportazione, sulle dimensioni di esportazione e altro ancora. Il manifesto viene denominato utilizzando il formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visualizza un [file manifesto di esempio](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Il file manifesto include i campi seguenti:
   * `flowRunId`: Il [esecuzione del flusso di dati](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) che ha generato il file esportato.
   * `scheduledTime`: ora in UTC in cui è stato esportato il file.
   * `exportResults.sinkPath`: percorso nel percorso di archiviazione in cui viene depositato il file esportato.
   * `exportResults.name`: nome del file esportato.
   * `size`: dimensione del file esportato, in byte.

>[!TIP]
>
>Nel flusso di lavoro della destinazione di connessione, puoi creare una cartella personalizzata nell’archiviazione Amazon S3 per file di pubblico esportato. Letto [Utilizzare le macro per creare una cartella nel percorso di archiviazione](overview.md#use-macros) per istruzioni.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

### Obbligatorio [!DNL Amazon S3] autorizzazioni {#required-s3-permission}

Per connettere ed esportare correttamente i dati nel [!DNL Amazon S3] percorso di archiviazione, creare un utente di gestione delle identità e degli accessi (IAM) per [!DNL Platform] in [!DNL Amazon S3] e assegna le autorizzazioni per le azioni seguenti:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla [!DNL Amazon S3] e assicurati che i file esportati contengano le popolazioni di profilo previste.

## Indirizzo IP inserito nell&#39;elenco Consentiti {#ip-address-allow-list}

Consulta la sezione [Indirizzo IP inserito nell&#39;elenco Consentiti](ip-address-allow-list.md) articolo per aggiungere IP di Adobe a un inserisco nell&#39;elenco Consentiti di.