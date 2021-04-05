---
keywords: destinazione di archiviazione cloud;archiviazione cloud
title: Creare una destinazione di archiviazione cloud
type: Tutorial
description: Istruzioni per la connessione alle posizioni di archiviazione cloud
seo-description: Istruzioni per la connessione alle posizioni di archiviazione cloud
exl-id: 58003c1e-2f70-4e28-8a38-3be00da7cc3c
translation-type: tm+mt
source-git-commit: 1e33a7b48e20d7afe9f10b206a6fd68433b205db
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Creare una destinazione di archiviazione cloud

## Panoramica {#overview}

Questa pagina spiega come connettersi alle posizioni di archiviazione cloud in Adobe Experience Platform.

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleziona la destinazione di archiviazione cloud preferita, quindi seleziona **[!UICONTROL Configure]**.

![Connessione alla destinazione di archiviazione cloud](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

## Passaggio account {#account}

Nel passaggio **[!UICONTROL Account]**, se in precedenza hai impostato una connessione alla destinazione di archiviazione cloud, seleziona **[!UICONTROL Existing Account]** e seleziona la connessione esistente. In alternativa, è possibile selezionare **[!UICONTROL New Account]** per impostare una nuova connessione alla destinazione di archiviazione cloud. Immetti le credenziali di autenticazione del tuo account e seleziona **[!UICONTROL Connect to destination]**. Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come stringa codificata [!DNL Base64].

Per informazioni specifiche sulle credenziali immesse nel passaggio **Autenticazione** , consulta [Destinazione Amazon S3](./amazon-s3.md), [[!DNL Amazon Kinesis]](./amazon-kinesis.md), destinazione [[!DNL Azure Event Hubs]](./azure-event-hubs.md) e [Destinazione SFTP](./sftp.md) .

>[!NOTE]
>
>Platform supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se immetti credenziali errate nel percorso di archiviazione cloud. In questo modo non completa il flusso di lavoro con credenziali errate.

![Connessione alla destinazione di archiviazione cloud - passaggio dell&#39;account](../../assets/catalog/cloud-storage/workflow/destination-account.png)

## Passaggio di autenticazione {#authentication}

Nel passaggio **[!UICONTROL Authentication]** immetti un **[!UICONTROL Name]** e un **[!UICONTROL Description]** per il flusso di attivazione.

A questo passaggio, puoi anche selezionare qualsiasi **[!UICONTROL Marketing action]** che deve essere applicato a questa destinazione. Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

Per le destinazioni Amazon S3, inserisci **[!UICONTROL Bucket name]** e **[!UICONTROL Folder path]** nella destinazione di archiviazione cloud in cui verranno consegnati i file. Selezionare **[!UICONTROL Create Destination]** dopo aver compilato i campi precedenti.

![Connessione alla destinazione di archiviazione cloud Amazon S3 - passaggio di autenticazione](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

Per le destinazioni SFTP, inserisci **[!UICONTROL Folder path]** dove verranno consegnati i file. Selezionare **[!UICONTROL Create Destination]** dopo aver compilato i campi precedenti.

![Connessione alla destinazione di archiviazione cloud SFTP - passaggio di autenticazione](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

Per le destinazioni [!DNL Amazon Kinesis] , fornisci il nome del flusso di dati esistente nel tuo account [!DNL Amazon Kinesis] . Platform esporta i dati in questo flusso. Selezionare **[!UICONTROL Create Destination]** dopo aver compilato i campi precedenti.

![Connessione alla destinazione di archiviazione cloud Kinesis - passaggio di autenticazione](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

Per le destinazioni [!DNL Azure Event Hubs] , fornisci il nome del flusso di dati esistente nel tuo account [!DNL Amazon Event Hubs] . Platform esporta i dati in questo flusso. Selezionare **[!UICONTROL Create Destination]** dopo aver compilato i campi precedenti.

![Connessione alla destinazione di archiviazione cloud di Event Hubs - passaggio di autenticazione](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

La destinazione viene ora creata. Puoi selezionare **[!UICONTROL Save & Exit]** se desideri attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. Leggi la sezione [Attiva segmenti](#activate-segments) per il resto del flusso di lavoro per esportare i dati.

## Utilizzare le macro per creare una cartella nel percorso di archiviazione{#use-macros}

Per creare una cartella personalizzata per ciascun file di segmento nel percorso di archiviazione, è possibile utilizzare le macro nel campo di immissione del percorso della cartella. Inserire le macro alla fine del campo di input, come illustrato di seguito.

![Come utilizzare le macro per creare una cartella nell&#39;archivio](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Gli esempi seguenti fanno riferimento a un segmento di esempio `Luxury Audience` con ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

### Macro 1 - `%SEGMENT_NAME%`

Ingresso: `acme/campaigns/2021/%SEGMENT_NAME%`

Percorso cartella nel percorso di archiviazione: `acme/campaigns/2021/Luxury Audience`

### Macro 2 - `%SEGMENT_ID%`

Ingresso: `acme/campaigns/2021/%SEGMENT_ID%`

Percorso cartella nel percorso di archiviazione: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

### Macro 3 - `%SEGMENT_NAME%/%SEGMENT_ID%`

Ingresso: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`

Percorso cartella nel percorso di archiviazione: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`



## Attiva segmenti {#activate-segments}

Per informazioni sul flusso di lavoro di attivazione dei segmenti, consulta [Attivare profili e segmenti su una destinazione](../../ui/activate-destinations.md) .
