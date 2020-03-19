---
title: Flusso di lavoro per destinazioni di archiviazione cloud
seo-title: Flusso di lavoro per destinazioni di archiviazione cloud
description: Istruzioni per la connessione alle posizioni di archiviazione cloud
seo-description: Istruzioni per la connessione alle posizioni di archiviazione cloud
translation-type: tm+mt
source-git-commit: 225f18bd0d092bdae7b4cc99c278e850be9cfd56

---


# Flusso di lavoro per creare destinazioni di archiviazione cloud

## Panoramica

In questa pagina viene illustrato come connettersi alle posizioni di archiviazione cloud nella piattaforma dati cliente Adobe in tempo reale.

1. In **[!UICONTROL Connessioni > Destinazioni]**, seleziona la destinazione di archiviazione cloud preferita, quindi seleziona la destinazione **[!UICONTROL di]** Connect.

   ![Connessione alla destinazione di archiviazione cloud](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Nel passaggio **Autenticazione** , se in precedenza avete impostato una connessione alla destinazione di archiviazione cloud, selezionate Account **** esistente e selezionate la connessione esistente. In alternativa, potete selezionare **[!UICONTROL Nuovo account]** per impostare una nuova connessione alla destinazione di archiviazione cloud. Compilate le credenziali di autenticazione dell&#39;account e selezionate **[!UICONTROL Connetti a destinazione]**.

   >[!NOTE]
   >
   >Adobe Real-time CDP supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se vengono immesse credenziali non corrette nel percorso di archiviazione cloud. In questo modo si evita di completare il flusso di lavoro con credenziali non corrette.

   ![Connessione alla destinazione di archiviazione cloud - passaggio di autenticazione](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Nel passaggio **[!UICONTROL Configurazione]** , immettete un **[!UICONTROL nome]** e una **[!UICONTROL destinazione]** per il flusso di attivazione e inserite il percorso **[!UICONTROL della]** cartella nella destinazione di archiviazione cloud in cui verranno inviati i file. Dopo aver compilato i campi sopra, selezionate **[!UICONTROL Crea destinazione]** .

   ![Connessione alla destinazione di archiviazione cloud - passaggio di autenticazione](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. La destinazione è stata creata. Puoi selezionare **[!UICONTROL Salva ed esci]** se vuoi attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Avanti]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva, [Attivare i segmenti](#activate-segments), per il resto del flusso di lavoro,

## Attivare i segmenti {#activate-segments}

Consulta [Attivare profili e segmenti su una destinazione](/help/rtcdp/destinations/activate-destinations.md) per informazioni sul flusso di lavoro di attivazione dei segmenti.