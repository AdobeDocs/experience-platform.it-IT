---
title: Flusso di lavoro destinazioni social network
seo-title: Flusso di lavoro destinazioni social network
description: Istruzioni per la connessione agli account degli annunci social network
seo-description: Istruzioni per la connessione agli account degli annunci social network
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---


# Flusso di lavoro di autenticazione delle destinazioni social network {#social-network-destinations-workflow}

## Flusso di lavoro per creare destinazioni social network

Questa esercitazione utilizza Facebook come esempio, ma il flusso di lavoro in Adobe Real-time Customer Data Platform sarà lo stesso per tutte le destinazioni dei social network, una volta aggiunto di nuovo al prodotto.

1. In **[!UICONTROL Destinations > Catalog]**, scorrete fino alla **[!UICONTROL Social]** categoria. Seleziona la destinazione preferita del social network, quindi seleziona **[!UICONTROL Connect destination]**.

   ![Connessione alla destinazione social network](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Nel passaggio **Autenticazione** , se in precedenza avete impostato una connessione alla destinazione di social network, selezionate **[!UICONTROL Existing Account]** e selezionate la connessione esistente. In alternativa, potete scegliere **[!UICONTROL New Account]** di impostare una nuova connessione alla destinazione del social network. Seleziona **[!UICONTROL Connect to destination]** e passa alla destinazione social network selezionata per accedere e collegare Adobe Experience Cloud al tuo account annuncio social network.

   >[!NOTE]
   >
   >Adobe Real-time CDP supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se immetti credenziali non corrette nell&#39;ID dell&#39;account del social network. In questo modo si evita di completare il flusso di lavoro con credenziali non corrette.

   ![Connessione alla destinazione social network - passaggio di autenticazione](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Una volta confermate le credenziali e che Adobe Experience Cloud è connesso al social network, puoi scegliere **[!UICONTROL Next]** di procedere con il **[!UICONTROL Setup]** passaggio.

   ![Credenziali confermate](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Nel **[!UICONTROL Setup]** passaggio, immettete un **[!UICONTROL Name]** e un **[!UICONTROL Description]** per il flusso di attivazione e inserite il contenuto **[!UICONTROL Account ID]** del social network e dell’account. <br> Inoltre, in questo passaggio potete selezionare tutte le opzioni **[!UICONTROL Marketing use case]** che devono essere applicate a questa destinazione. I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra i casi di utilizzo di marketing definiti da Adobe oppure creare un tuo caso di utilizzo di marketing. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti da Adobe, consulta la panoramica [dei criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati. <br> Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

   >[!IMPORTANT]
   >
   > * Il caso d’uso marketing *Single Identity Personalization (Personalizzazione identità* singola) è selezionato per impostazione predefinita per le destinazioni dei social network e non può essere rimosso.
   > * Destinazioni Facebook. **[!UICONTROL Account ID]** è l&#39;ID del tuo account pubblicitario Facebook. Puoi trovare questo ID in Facebook Ads Manager. Aggiungi l’ID con il prefisso `act_` indicato di seguito:


   ![Connessione alla destinazione social network - passaggio di configurazione](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. La destinazione è stata creata. Puoi scegliere **[!UICONTROL Save & Exit]** se attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva, [Attivare i segmenti sui social network](#activate-segments), per il resto del flusso di lavoro.

## Attivare i segmenti sui social network {#activate-segments}

Per istruzioni su come attivare i segmenti nei social network, vedi [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).