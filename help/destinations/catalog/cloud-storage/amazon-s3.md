---
title: Connessione Amazon S3
description: Crea una connessione in uscita allo storage Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV da Adobe Experience Platform nei bucket S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 14%

---

# Connessione [!DNL Amazon S3] {#s3-connection}

## Registro modifiche destinazione {#changelog}

+++ Visualizza changelog


| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Gennaio 2024 | Aggiornamento della funzionalità e della documentazione | Il connettore di destinazione Amazon S3 ora supporta un nuovo tipo di autenticazione ruolo presunto. Ulteriori informazioni nella [sezione autenticazione](#assumed-role-authentication). |
| Luglio 2023 | Aggiornamento della funzionalità e della documentazione | Con la versione di Experience Platform di luglio 2023, la destinazione [!DNL Amazon S3] fornisce nuove funzionalità, come elencato di seguito: <br><ul><li>[Supporto per l&#39;esportazione del set di dati](/help/destinations/ui/export-datasets.md)</li><li>Nuove [opzioni di denominazione file](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>Possibilità di impostare intestazioni di file personalizzate nei file esportati tramite il [passaggio di mappatura migliorato](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Possibilità di personalizzare la formattazione dei file CSV esportati](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## Connettersi all&#39;archiviazione [!DNL Amazon S3] tramite API o interfaccia utente {#connect-api-or-ui}

* Per connettersi al percorso di archiviazione [!DNL Amazon S3] tramite l&#39;interfaccia utente di Experience Platform, leggere le sezioni [Connetti alla destinazione](#connect) e [Attiva i tipi di pubblico a questa destinazione](#activate) di seguito.
* Per connettersi al percorso di archiviazione [!DNL Amazon S3] a livello di programmazione, leggere la guida su come [attivare tipi di pubblico in destinazioni basate su file utilizzando l&#39;esercitazione API del servizio Flusso](../../api/activate-segments-file-based-destinations.md).

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Profile-based]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Tipo di esportazione basato su profilo Amazon S3 evidenziato nell&#39;UU.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Esporta i set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, consulta le esercitazioni:

* Come [esportare i set di dati utilizzando l&#39;interfaccia utente di Experience Platform](/help/destinations/ui/export-datasets.md).
* Come [esportare i set di dati a livello di programmazione utilizzando l&#39;API del servizio Flusso](/help/destinations/api/export-datasets.md).

## Formato file dei dati esportati {#file-format}

Durante l&#39;esportazione di *dati sul pubblico*, Experience Platform crea un file `.csv`, `parquet` o `.json` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta la sezione [formati di file supportati per l&#39;esportazione](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) nell&#39;esercitazione di Audience Activation.

Durante l&#39;esportazione di *set di dati*, Experience Platform crea un file `.parquet` o `.json` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta la sezione [Verifica dell&#39;esportazione dei set di dati](../../ui/export-datasets.md#verify) nell&#39;esercitazione sull&#39;esportazione dei set di dati.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL View Destinations]** e le **[!UICONTROL Manage Destinations]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Chiave pubblica RSA"
>abstract="Facoltativamente, puoi collegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Nel collegamento alla documentazione qui di seguito, trovi un esempio di chiave formattata correttamente."

Per autenticare nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connect to destination]**. La destinazione Amazon S3 supporta due metodi di autenticazione:

* Autenticazione chiave di accesso e chiave segreta
* Autenticazione del ruolo assunta

#### Autenticazione con chiave di accesso S3 e chiave segreta

Utilizza questo metodo di autenticazione quando desideri inserire la chiave di accesso e la chiave segreta di Amazon S3 per consentire ad Experience Platform di esportare dati nelle proprietà di Amazon S3.

![Immagine dei campi obbligatori quando si seleziona l&#39;autenticazione con chiave di accesso e chiave segreta.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* Chiave di accesso **[!DNL Amazon S3]** e chiave segreta **[!DNL Amazon S3]**: in [!DNL Amazon S3], genera una coppia `access key - secret access key` per concedere l&#39;accesso Experience Platform al tuo account [!DNL Amazon S3]. Ulteriori informazioni sono disponibili nella [documentazione di Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Encryption key]**: facoltativamente, è possibile allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

  ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell&#39;interfaccia utente.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Autenticazione con ruolo S3 assunto {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="Autenticazione del ruolo assunta"
>abstract="Utilizza questo tipo di autenticazione se preferisci non condividere le chiavi dell’account e le chiavi segrete con Adobe. Al contrario, Experience Platform si connette alla posizione Amazon S3 utilizzando l’accesso basato sul ruolo. Incolla l’ARN del ruolo creato in AWS per l’utente Adobe. Il pattern è simile a `arn:aws:iam::800873819705:role/destinations-role-customer` "

Utilizza questo tipo di autenticazione se preferisci non condividere le chiavi dell’account e le chiavi segrete con Adobe. Al contrario, Experience Platform si connette alla tua posizione Amazon S3 utilizzando l’accesso basato sui ruoli.

![Immagine dei campi obbligatori quando si seleziona l&#39;autenticazione del ruolo assunta.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

* **[!DNL Role]**: incolla l&#39;ARN del ruolo creato in AWS per l&#39;utente Adobe. Il modello è simile a `arn:aws:iam::800873819705:role/destinations-role-customer`. Per istruzioni dettagliate su come configurare correttamente l’accesso S3, consulta i passaggi seguenti.
* **[!UICONTROL Encryption key]**: facoltativamente, è possibile allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

A questo scopo, devi creare nella console AWS un ruolo presunto per Adobe con le [autorizzazioni necessarie](#minimum-permissions-iam-user) per scrivere nei bucket Amazon S3.

**Crea un criterio con le autorizzazioni richieste**

1. Apri la console AWS e vai a IAM > Criteri > Crea criterio.
2. Seleziona Editor criteri > JSON e aggiungi le autorizzazioni seguenti.

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "VisualEditor0",
               "Effect": "Allow",
               "Action": [
                   "s3:PutObject",
                   "s3:GetObject",
                   "s3:DeleteObject",
                   "s3:GetBucketLocation",
                   "s3:ListMultipartUploadParts"
               ],
               "Resource": "arn:aws:s3:::bucket/folder/*"
           },
           {
               "Sid": "VisualEditor1",
               "Effect": "Allow",
               "Action": [
                   "s3:ListBucket"
               ],
               "Resource": "arn:aws:s3:::bucket"
           }
       ]
   }
   ```

3. Nella pagina successiva immettere un nome per il criterio e salvarlo come riferimento. Questo nome di criterio è necessario per la creazione del ruolo nel passaggio successivo.

**Crea un ruolo utente nel tuo account cliente S3**

1. Apri la console AWS e vai a IAM > Ruoli > Crea nuovo ruolo.
2. Seleziona **Tipo di entità attendibile** > **Account AWS**
3. Seleziona **Un account AWS** > **Un altro account AWS** e immetti l&#39;ID account Adobe: `670664943635`
4. Aggiungere le autorizzazioni utilizzando il criterio creato in precedenza
5. Immettere un nome di ruolo, ad esempio `destinations-role-customer`. Il nome della mansione deve essere considerato riservato, come una password. Può contenere fino a 64 caratteri e può contenere caratteri alfanumerici e i seguenti caratteri speciali: `+=,.@-_`. Verifica quindi che:
   * L&#39;ID account Adobe `670664943635` è presente nella sezione **[!UICONTROL Select trusted entities]**
   * Il criterio creato in precedenza è presente in **[!UICONTROL Permissions policy summary]**

**Assegna ad Adobe il ruolo**

Dopo aver creato il ruolo in AWS, devi fornire il ruolo ARN ad Adobe. L&#39;ARN segue questo pattern: `arn:aws:iam::800873819705:role/destinations-role-customer`

Puoi trovare l’ARN nella pagina principale dopo aver creato il ruolo nella console AWS. Utilizzerai questo ARN durante la creazione della destinazione.

**Verificare le autorizzazioni del ruolo e le relazioni di trust**

Assicurati che il tuo ruolo disponga della seguente configurazione:

* **Autorizzazioni**: il ruolo deve disporre delle autorizzazioni per accedere a S3 (accesso completo o autorizzazioni minime fornite nel passaggio **Crea un criterio con le autorizzazioni richieste** sopra)
* **Relazioni di trust**: il ruolo deve avere l&#39;account Adobe radice (`670664943635`) nelle relazioni di trust

**Alternativa: limita a un utente Adobe specifico (facoltativo)**

Se preferisci non consentire l’intero account Adobe, puoi limitare l’accesso solo allo specifico utente Adobe. A tale scopo, modificare il criterio di attendibilità con la seguente configurazione:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::670664943635:user/destinations-adobe-user"
            },
            "Action": "sts:AssumeRole",
            "Condition": {}
        }
    ]
}
```

Per ulteriori informazioni, consulta la [documentazione di AWS sulla creazione di ruoli](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).



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

* **[!UICONTROL Name]**: immettere un nome che consenta di identificare la destinazione.
* **[!UICONTROL Description]**: immettere una descrizione della destinazione.
* **[!UICONTROL Bucket name]**: immettere il nome del bucket [!DNL Amazon S3] da utilizzare per questa destinazione.
* **[!UICONTROL Folder path]**: immettere il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL File type]**: selezionare il formato che Experience Platform deve utilizzare per i file esportati. Quando selezioni l&#39;opzione [!UICONTROL CSV], puoi anche [configurare le opzioni di formattazione del file](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: selezionare il tipo di compressione che Experience Platform deve utilizzare per i file esportati.
* **[!UICONTROL Include manifest file]**: attivare questa opzione se si desidera che le esportazioni includano un file JSON manifesto contenente informazioni sul percorso di esportazione, sulle dimensioni di esportazione e altro ancora. Il manifesto è denominato nel formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visualizza un [file manifesto di esempio](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Il file manifesto include i campi seguenti:
   * `flowRunId`: [esecuzione del flusso di dati](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) che ha generato il file esportato.
   * `scheduledTime`: ora in UTC in cui è stato esportato il file.
   * `exportResults.sinkPath`: il percorso nel percorso di archiviazione in cui è depositato il file esportato.
   * `exportResults.name`: nome del file esportato.
   * `size`: dimensione del file esportato, in byte.

>[!TIP]
>
>Nel flusso di lavoro della destinazione di connessione, puoi creare una cartella personalizzata nell’archiviazione Amazon S3 per file di pubblico esportato. Per istruzioni, leggere [Utilizzare le macro per creare una cartella nel percorso di archiviazione](overview.md#use-macros).

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli della connessione di destinazione, selezionare **[!UICONTROL Next]**.

### Autorizzazioni [!DNL Amazon S3] richieste {#required-s3-permission}

Per connettere ed esportare correttamente i dati nel percorso di archiviazione [!DNL Amazon S3], creare un utente di Gestione identità e accesso (IAM) per [!DNL Experience Platform] in [!DNL Amazon S3] e assegnare le autorizzazioni per le azioni seguenti:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

#### Autorizzazioni minime richieste per l’autenticazione dei ruoli assunta da IAM {#minimum-permissions-iam-user}

Quando configuri il ruolo IAM come cliente, accertati che il criterio di autorizzazione associato al ruolo includa le azioni richieste per la cartella di destinazione nel bucket e l&#39;azione `s3:ListBucket` per la radice del bucket. Di seguito è riportato un esempio dei criteri di autorizzazioni minime per questo tipo di autenticazione:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:GetBucketLocation",
                "s3:ListMultipartUploadParts"
            ],
            "Resource": "arn:aws:s3:::bucket/folder/*"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::bucket"
        }
    ]
}  
```

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Experience Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione profilo batch](../../ui/activate-batch-profile-destinations.md).

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controllare l&#39;archivio [!DNL Amazon S3] e assicurarsi che i file esportati contengano le popolazioni di profilo previste.

## Indirizzo IP inserisco nell&#39;elenco Consentiti {#ip-address-allow-list}

Se hai bisogno di aggiungere IP Adobe inserire nell&#39;elenco Consentiti a un inserisco nell&#39;elenco Consentiti di, consulta l&#39;articolo [Indirizzo IP &#x200B;](ip-address-allow-list.md).