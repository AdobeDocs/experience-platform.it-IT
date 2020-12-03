---
keywords: cloud storage destination;cloud storage
title: Flusso di lavoro per destinazioni di archiviazione cloud
seo-title: Flusso di lavoro per destinazioni di archiviazione cloud
type: Tutorial
description: Istruzioni per la connessione alle posizioni di archiviazione cloud
seo-description: Istruzioni per la connessione alle posizioni di archiviazione cloud
translation-type: tm+mt
source-git-commit: 24c8dd0f01d7ea14b2fa5827722e797bd209f50c
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# Flusso di lavoro per creare destinazioni di archiviazione cloud

## Panoramica

Questa pagina spiega come collegarsi alle posizioni di archiviazione cloud nella piattaforma dati cliente in tempo reale.

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleziona la destinazione di archiviazione cloud preferita, quindi seleziona **[!UICONTROL Configure]**.

![Connessione alla destinazione di archiviazione cloud](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un **[!UICONTROL Activate]** pulsante sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consultate la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

Nel **[!UICONTROL Authentication]** passaggio, se in precedenza avete impostato una connessione alla destinazione di archiviazione cloud, selezionate **[!UICONTROL Existing Account]** e selezionate la connessione esistente. In alternativa, potete scegliere **[!UICONTROL New Account]** di impostare una nuova connessione alla destinazione di archiviazione cloud. Compilate le credenziali di autenticazione dell&#39;account e selezionate **[!UICONTROL Connect to destination]**. Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Questa chiave pubblica **deve** essere scritta come una stringa codificata Base64.

Per informazioni dettagliate sulle credenziali immesse nel passaggio [Autenticazione](./amazon-s3.md) , vedere [[!DNL Amazon Kinesis]](./amazon-kinesis.md) destinazione, destinazione, [[!DNL Azure Event Hubs]](./azure-event-hubs.md) destinazione e destinazione [SFTP](./sftp.md) Amazon S3 **, nel passaggio** Autenticazione.

>[!NOTE]
>
>CDP in tempo reale supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se vengono inserite credenziali non corrette nel percorso di archiviazione cloud. In questo modo si evita di completare il flusso di lavoro con credenziali non corrette.

![Connessione alla destinazione di archiviazione cloud - passaggio di autenticazione](../../assets/catalog/cloud-storage/workflow/destination-account.png)

Nel **[!UICONTROL Setup]** passaggio, immettete un **[!UICONTROL Name]** e un **[!UICONTROL Description]** per il flusso di attivazione.

Inoltre, in questo passaggio potete selezionare tutte le opzioni **[!UICONTROL Marketing use case]** che devono essere applicate a questa destinazione. I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti dal Adobe , consulta la panoramica [sui criteri di utilizzo dei](../../../data-governance/policies/overview.md#core-actions)dati.

Per  destinazioni Amazon S3, inserire i file **[!UICONTROL Bucket name]** e **[!UICONTROL Folder path]** nella destinazione di archiviazione cloud in cui verranno consegnati. Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

![Connessione  destinazione di archiviazione cloud Amazon S3 - passaggio di autenticazione](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

Per le destinazioni SFTP, inserite la **[!UICONTROL Folder path]** posizione in cui verranno inviati i file. Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

![Connessione alla destinazione di archiviazione cloud SFTP - passaggio di autenticazione](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

Per [!DNL Amazon Kinesis] le destinazioni, specifica il nome del flusso di dati esistente nel tuo [!DNL Amazon Kinesis] account. CDP in tempo reale esporta i dati in questo flusso. Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

![Connessione alla destinazione di archiviazione cloud Kinesis - passaggio di autenticazione](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

Per [!DNL Azure Event Hubs] le destinazioni, specifica il nome del flusso di dati esistente nel tuo [!DNL Amazon Event Hubs] account. CDP in tempo reale esporta i dati in questo flusso. Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

![Connessione alla destinazione di archiviazione cloud degli hub eventi - passaggio di autenticazione](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

La destinazione è stata creata. Puoi scegliere **[!UICONTROL Save & Exit]** se attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva, [Attivare i segmenti](#activate-segments), per consentire al resto del flusso di lavoro di esportare i dati.

## Attivare i segmenti {#activate-segments}

Consulta [Attivare profili e segmenti su una destinazione](../../ui/activate-destinations.md) per informazioni sul flusso di lavoro di attivazione dei segmenti.