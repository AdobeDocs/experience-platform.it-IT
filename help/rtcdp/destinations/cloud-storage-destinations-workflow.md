---
keywords: cloud storage destination;cloud storage
title: Flusso di lavoro per destinazioni di archiviazione cloud
seo-title: Flusso di lavoro per destinazioni di archiviazione cloud
description: Istruzioni per la connessione alle posizioni di archiviazione cloud
seo-description: Istruzioni per la connessione alle posizioni di archiviazione cloud
translation-type: tm+mt
source-git-commit: 2dfa46906374151628d46c309df724a59f8dc50e
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# Flusso di lavoro per creare destinazioni di archiviazione cloud

## Panoramica

In questa pagina viene illustrato come connettersi alle posizioni di archiviazione cloud  Adobe Real-time Customer Data Platform (Piattaforma dati cliente in tempo reale).

1. In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleziona la destinazione di archiviazione cloud preferita, quindi seleziona **[!UICONTROL Configure]**.

   ![Connessione alla destinazione di archiviazione cloud](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

   >[!NOTE]
   >
   >Se esiste già una connessione con questa destinazione, è possibile visualizzare un **[!UICONTROL Activate]** pulsante sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consultate la sezione [Catalogo](/help/rtcdp/destinations/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

2. Nel **[!UICONTROL Authentication]** passaggio, se in precedenza avete impostato una connessione alla destinazione di archiviazione cloud, selezionate **[!UICONTROL Existing Account]** e selezionate la connessione esistente. In alternativa, potete scegliere **[!UICONTROL New Account]** di impostare una nuova connessione alla destinazione di archiviazione cloud. Compilate le credenziali di autenticazione dell&#39;account e selezionate **[!UICONTROL Connect to destination]**. <br> Per informazioni dettagliate sulle credenziali immesse nel passaggio [Autenticazione](/help/rtcdp/destinations/amazon-s3-destination.md) , vedere [!DNL Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) destinazione, destinazione, [!DNL Azure Event Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md) destinazione e destinazione [SFTP](/help/rtcdp/destinations/sftp-destination.md) Amazon S3 **, nel passaggio** Autenticazione.

   >[!NOTE]
   >
   > Adobe CDP in tempo reale supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se nel percorso di archiviazione cloud vengono inserite credenziali non corrette. In questo modo si evita di completare il flusso di lavoro con credenziali non corrette.

   ![Connessione alla destinazione di archiviazione cloud - passaggio di autenticazione](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Nel **[!UICONTROL Setup]** passaggio, immettete un **[!UICONTROL Name]** e un **[!UICONTROL Description]** per il flusso di attivazione. <br>
Inoltre, in questo passaggio potete selezionare tutte le opzioni **[!UICONTROL Marketing use case]** che devono essere applicate a questa destinazione. I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti dal Adobe , consulta la panoramica [sui criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati. <br>
Per  destinazioni Amazon S3, inserire i file **[!UICONTROL Bucket name]** e **[!UICONTROL Folder path]** nella destinazione di archiviazione cloud in cui verranno consegnati. Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

   ![Connessione  destinazione di archiviazione cloud Amazon S3 - passaggio di autenticazione](/help/rtcdp/destinations/assets/amazon-s3-setup-step.png)

   Per le destinazioni SFTP, inserite la **[!UICONTROL Folder path]** posizione in cui verranno inviati i file. Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

   ![Connessione alla destinazione di archiviazione cloud SFTP - passaggio di autenticazione](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

   Per [!DNL Amazon Kinesis] le destinazioni, specifica il nome del flusso di dati esistente nel tuo [!DNL Amazon Kinesis] account.  Adobe CDP in tempo reale esporta i dati in questo flusso. Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

   ![Connessione alla destinazione di archiviazione cloud Kinesis - passaggio di autenticazione](/help/rtcdp/destinations/assets/kinesis-destinations-setup-step.png)

   Per [!DNL Azure Event Hubs] le destinazioni, specifica il nome del flusso di dati esistente nel tuo [!DNL Amazon Kinesis] account.  Adobe CDP in tempo reale esporta i dati in questo flusso. Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

   ![Connessione alla destinazione di archiviazione cloud Kinesis - passaggio di autenticazione](/help/rtcdp/destinations/assets/eventhubs-destinations-setup-step.png)

4. La destinazione è stata creata. Puoi scegliere **[!UICONTROL Save & Exit]** se attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva, [Attivare i segmenti](#activate-segments), per consentire al resto del flusso di lavoro di esportare i dati.

## Attivare i segmenti {#activate-segments}

Consulta [Attivare profili e segmenti su una destinazione](/help/rtcdp/destinations/activate-destinations.md) per informazioni sul flusso di lavoro di attivazione dei segmenti.