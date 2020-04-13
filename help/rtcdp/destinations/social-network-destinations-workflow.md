---
title: Flusso di lavoro destinazioni social network
seo-title: Flusso di lavoro destinazioni social network
description: Istruzioni per la connessione agli account degli annunci social network
seo-description: Istruzioni per la connessione agli account degli annunci social network
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (Beta) Flusso di lavoro di autenticazione delle destinazioni social network {#social-network-destinations-workflow}


>[!IMPORTANT]
>
>Il flusso di lavoro per la creazione di destinazioni social network in Adobe Real-time CDP è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e la funzionalità sono soggette a modifiche.

## Flusso di lavoro per creare destinazioni di archiviazione cloud

Questa esercitazione utilizza Facebook come esempio, ma il flusso di lavoro in Adobe Real-time Customer Data Platform sarà lo stesso per tutte le destinazioni Social Network, una volta aggiunto al prodotto.

1. In **[!UICONTROL Connections > Destinations]**, scorrete fino alla **[!UICONTROL Social]** categoria. Seleziona la destinazione preferita del social network, quindi seleziona **[!UICONTROL Connect destination]**.

   ![Connessione alla destinazione social network](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Nel passaggio **Autenticazione** , se in precedenza avete impostato una connessione alla destinazione di social network, selezionate **[!UICONTROL Existing Account]** e selezionate la connessione esistente. In alternativa, potete scegliere **[!UICONTROL New Account]** di impostare una nuova connessione alla destinazione del social network. Seleziona **[!UICONTROL Connect to destination]** e passa alla destinazione social network selezionata per accedere e collegare Adobe Experience Cloud al tuo account annuncio social network.

   >[!NOTE]
   >
   >Adobe Real-time CDP supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se immetti credenziali non corrette nell&#39;ID dell&#39;account del social network. In questo modo si evita di completare il flusso di lavoro con credenziali non corrette.

   ![Connessione alla destinazione social network - passaggio di autenticazione](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Una volta confermate le credenziali e che Adobe Experience Cloud è connesso al social network, puoi scegliere **[!UICONTROL Next]** di procedere con il **[!UICONTROL Setup]** passaggio.

   ![Credenziali confermate](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Nel **[!UICONTROL Setup]** passaggio, immettete un **[!UICONTROL Name]** e un **[!UICONTROL Description]** per il flusso di attivazione e inserite il contenuto **[!UICONTROL Account ID]** del social network e dell’account. Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

   >[!IMPORTANT]
   >
   >Destinazioni Facebook. **[!UICONTROL Account ID]** è l&#39;ID del tuo account pubblicitario Facebook. Puoi trovare questo ID in Facebook Ads Manager. Aggiungi l’ID con il prefisso `act_` indicato di seguito:

   ![Connessione alla destinazione social network - passaggio di configurazione](/help/rtcdp/destinations/assets/social-network-step.png)

5. La destinazione è stata creata. Puoi scegliere **[!UICONTROL Save & Exit]** se attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva, [Attivare i segmenti sui social network](#activate-segments), per il resto del flusso di lavoro.

## Attivare i segmenti sui social network {#activate-segments}

Per istruzioni su come attivare i segmenti nei social network, vedi [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).