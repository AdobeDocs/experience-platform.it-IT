---
title: Flusso di lavoro destinazioni social network
seo-title: Flusso di lavoro destinazioni social network
description: Istruzioni per la connessione agli account degli annunci social network
seo-description: Istruzioni per la connessione agli account degli annunci social network
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---


# Flusso di lavoro di autenticazione delle destinazioni social network {#social-network-destinations-workflow}

## Flusso di lavoro per creare destinazioni social network

Questa esercitazione viene utilizzata [!DNL Facebook] come esempio, ma il flusso di lavoro in  Adobe Dati cliente in tempo reale sarà lo stesso per tutte le destinazioni dei social network, una volta aggiunto di nuovo al prodotto.

1. In **[!UICONTROL Destinations > Catalog]**, scorrete fino alla **[!UICONTROL Social]** categoria. Seleziona la destinazione preferita del social network, quindi seleziona **[!UICONTROL Connect destination]**.

   ![Connessione alla destinazione social network](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Nel passaggio **Autenticazione** , se in precedenza avete impostato una connessione alla destinazione di social network, selezionate **[!UICONTROL Existing Account]** e selezionate la connessione esistente. In alternativa, potete scegliere **[!UICONTROL New Account]** di impostare una nuova connessione alla destinazione del social network. Seleziona **[!UICONTROL Connect to destination]** e passerai alla destinazione social network selezionata per accedere e collegare Adobe Experience Cloud al tuo account Social Network Ad.

   >[!NOTE]
   >
   > Adobe CDP in tempo reale supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se immetti credenziali non corrette nell&#39;ID dell&#39;account del social network. In questo modo si evita di completare il flusso di lavoro con credenziali non corrette.

   ![Connessione alla destinazione social network - passaggio di autenticazione](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Una volta confermate le credenziali e che Adobe Experience Cloud è connesso al social network, potete scegliere **[!UICONTROL Next]** di procedere con il **[!UICONTROL Setup]** passaggio.

   ![Credenziali confermate](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Nel **[!UICONTROL Setup]** passaggio, immettete un **[!UICONTROL Name]** e un **[!UICONTROL Description]** per il flusso di attivazione e inserite il contenuto **[!UICONTROL Account ID]** del social network e dell’account. <br> Inoltre, in questo passaggio potete selezionare tutte le opzioni **[!UICONTROL Marketing use case]** che devono essere applicate a questa destinazione. I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti dal Adobe , consulta la panoramica [sui criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati. <br> Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

   >[!IMPORTANT]
   >
   > * Il caso d’uso marketing *Single Identity Personalization (Personalizzazione identità* singola) è selezionato per impostazione predefinita per le destinazioni dei social network e non può essere rimosso.
   > * Per [!DNL Facebook] le destinazioni. **[!UICONTROL Account ID]** è tuo [!DNL Facebook Ad Account ID]. Puoi trovare questo ID nel [!DNL Facebook Ads Manager]. Aggiungi l’ID con il prefisso `act_` indicato di seguito:


   ![Connessione alla destinazione social network - passaggio di configurazione](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. La destinazione è stata creata. Puoi scegliere **[!UICONTROL Save & Exit]** se attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva, [Attivare i segmenti sui social network](#activate-segments), per il resto del flusso di lavoro.

## Attivare i segmenti sui social network {#activate-segments}

Per istruzioni su come attivare i segmenti nei social network, vedi [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).