---
title: Flusso di lavoro per destinazioni di archiviazione cloud
seo-title: Flusso di lavoro per destinazioni di archiviazione cloud
description: Istruzioni per la connessione alle posizioni di archiviazione cloud
seo-description: Istruzioni per la connessione alle posizioni di archiviazione cloud
translation-type: tm+mt
source-git-commit: 60b10aa823af55d6f38651308dc93eeb57a7fee6

---


# Flusso di lavoro per creare destinazioni di archiviazione cloud

## Panoramica

In questa pagina viene illustrato come connettersi alle posizioni di archiviazione cloud nella piattaforma dati cliente Adobe in tempo reale.

1. In **[!UICONTROL Connections > Destinations]**, seleziona la destinazione di archiviazione cloud preferita, quindi seleziona **[!UICONTROL Connect destination]**.

   ![Connessione alla destinazione di archiviazione cloud](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

1. Nel passaggio **Autenticazione** , se in precedenza avete impostato una connessione alla destinazione di archiviazione cloud, selezionate **[!UICONTROL Existing Account]** e selezionate la connessione esistente. In alternativa, potete scegliere **[!UICONTROL New Account]** di impostare una nuova connessione alla destinazione di archiviazione cloud. Compilate le credenziali di autenticazione dell&#39;account e selezionate **[!UICONTROL Connect to destination]**. Per informazioni specifiche sulle credenziali immesse nel passaggio [Autenticazione](/help/rtcdp/destinations/amazon-s3-destination.md) , vedere destinazione [Amazon S3 e destinazione](/help/rtcdp/destinations/sftp-destination.md) **** SFTP.

   >[!NOTE]
   >
   >Adobe Real-time CDP supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se vengono immesse credenziali non corrette nel percorso di archiviazione cloud. In questo modo si evita di completare il flusso di lavoro con credenziali non corrette.

   ![Connessione alla destinazione di archiviazione cloud - passaggio di autenticazione](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

1. Nel **[!UICONTROL Setup]** passaggio, immettete un **[!UICONTROL Name]** e un **[!UICONTROL Description]** per il flusso di attivazione. <br>
Per le destinazioni Amazon S3, inserite i file **[!UICONTROL Bucket name]** e **[!UICONTROL Folder path]** nella destinazione di archiviazione cloud in cui verranno consegnati. Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

   ![Connessione alla destinazione di archiviazione cloud Amazon S3 - passaggio di autenticazione](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

   Per le destinazioni SFTP, inserite la **[!UICONTROL Folder path]** posizione in cui verranno inviati i file.

   ![Connessione alla destinazione di archiviazione cloud SFTP - passaggio di autenticazione](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

1. La destinazione è stata creata. Puoi scegliere **[!UICONTROL Save & Exit]** se attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva, [Attivare i segmenti](#activate-segments), per consentire al resto del flusso di lavoro di esportare i dati.

## Attivare i segmenti {#activate-segments}

Consulta [Attivare profili e segmenti su una destinazione](/help/rtcdp/destinations/activate-destinations.md) per informazioni sul flusso di lavoro di attivazione dei segmenti.