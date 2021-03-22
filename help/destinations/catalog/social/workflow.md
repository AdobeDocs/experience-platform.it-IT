---
keywords: Facebook;facebook;Social network;Social network;autenticazione social network;autenticazione social network
title: Creare una destinazione di social network
type: Tutorial
description: Scopri come connettersi agli account di annunci social network in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Creare una destinazione social network {#social-network-destinations-workflow}

## Panoramica {#overview}

Questa esercitazione utilizza [!DNL Facebook] come esempio, ma il flusso di lavoro Adobe Experience Platform è lo stesso per tutte le destinazioni dei social network.

In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scorri fino alla categoria **[!UICONTROL Social]** . Seleziona la destinazione social network preferita, quindi seleziona **[!UICONTROL Configure]**.

![Connessione alla destinazione social network](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

## Passaggio di autenticazione {#authentication}

Nel passaggio **Autenticazione**, se in precedenza hai impostato una connessione alla destinazione di social network, seleziona **[!UICONTROL Existing Account]** e seleziona la connessione esistente. In alternativa, è possibile selezionare **[!UICONTROL New Account]** per impostare una nuova connessione alla destinazione di social network. Seleziona **[!UICONTROL Connect to destination]** per passare alla destinazione social network selezionata per accedere e collegare Adobe Experience Cloud al tuo account Ad social network.

>[!NOTE]
>
>Platform supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se immetti credenziali errate all’ID account di social network. In questo modo non completa il flusso di lavoro con credenziali errate.

![Connessione alla destinazione social network - passaggio di autenticazione](../../assets/catalog/social/workflow/pre-connect.png)

Una volta confermate le credenziali e quando Adobe Experience Cloud è connesso al social network, puoi selezionare **[!UICONTROL Next]** per procedere al passaggio **[!UICONTROL Setup]** .

![Credenziali confermate](../../assets/catalog/social/workflow/post-connect.png)

## Passaggio di installazione {#setup}

Nel passaggio **[!UICONTROL Setup]** , immetti un [!UICONTROL Name] e un [!UICONTROL Description] per il flusso di attivazione e compila il [!UICONTROL Account ID] del tuo account di annunci social network.

>[!IMPORTANT]
>
> Per le destinazioni [!DNL Facebook], **[!UICONTROL Account ID]** è il tuo [!DNL Facebook Ad Account ID]. Puoi trovare questo ID in [!DNL Facebook Ads Manager]. Aggiungi il prefisso ID con `act_` come mostrato di seguito:

![Connessione alla destinazione social network - passaggio di configurazione](../../assets/catalog/social/workflow/setup.png)

>[!IMPORTANT]
>
> Per le destinazioni [!DNL LinkedIn], **[!UICONTROL Account ID]** è il tuo [!DNL LinkedIn Campaign Manager Account ID]. Puoi trovare questo ID in [!DNL LinkedIn Campaign Manager].

Anche in questo passaggio, puoi selezionare qualsiasi **[!UICONTROL Marketing action]** che deve essere applicato a questa destinazione. Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

Selezionare **[!UICONTROL Create Destination]** dopo aver compilato i campi precedenti.

La destinazione viene ora creata. Puoi selezionare **[!UICONTROL Save & Exit]** se desideri attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva [Attivare i segmenti sui social network](#activate-segments), per il resto del flusso di lavoro.

## Attivare i segmenti sui social network {#activate-segments}

Per istruzioni su come attivare i segmenti sui social network, consulta [Attivare i dati sulle destinazioni](../../ui/activate-destinations.md).