---
keywords: Facebook;facebook;Social network;Social network;autenticazione social;autenticazione social network
title: Creare una destinazione social
type: Tutorial
description: Scopri come connettersi ai tuoi account di annunci social in Adobe Experience Platform.
exl-id: a0cdf2b7-b1e8-4a8e-9d5b-58a118e7b689
translation-type: tm+mt
source-git-commit: 805cb72e91e6446f74cc3461d39841740eb576c7
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Creare una destinazione social {#social-network-destinations-workflow}

## Panoramica {#overview}

Questa esercitazione utilizza [!DNL Facebook] come esempio, ma il flusso di lavoro Adobe Experience Platform è lo stesso per tutte le destinazioni social.

## Configurare la destinazione social : procedura dettagliata video {#video}

Il video seguente illustra come configurare una destinazione social e attivare segmenti in Adobe Experience Platform. Le fasi sono inoltre illustrate in sequenza nelle sezioni successive.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Seleziona destinazione social {#select-destination}

In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scorri fino alla categoria **[!UICONTROL Social]** . Seleziona la tua destinazione social preferita, quindi seleziona **[!UICONTROL Configure]**.

![Connessione alla destinazione social](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

## Passaggio account {#account}

Nel passaggio **Account**, se in precedenza hai impostato una connessione alla destinazione social, seleziona **[!UICONTROL Existing Account]** e seleziona la connessione esistente. In alternativa, puoi selezionare **[!UICONTROL New Account]** per impostare una nuova connessione alla destinazione social. Seleziona **[!UICONTROL Connect to destination]** per passare alla destinazione social selezionata per accedere e collegare Adobe Experience Cloud al tuo account social Ad.

>[!NOTE]
>
>Platform supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se immetti credenziali errate all’ID account social. In questo modo non completa il flusso di lavoro con credenziali errate.

![Connessione alla destinazione social - passaggio di autenticazione](../../assets/catalog/social/workflow/pre-connect.png)

Una volta confermate le credenziali e quando Adobe Experience Cloud è connesso al social network, puoi selezionare **[!UICONTROL Next]** per procedere al passaggio **[!UICONTROL Authentication]** .

![Credenziali confermate](../../assets/catalog/social/workflow/post-connect.png)

## Passaggio di autenticazione {#authentication}

Nel passaggio **[!UICONTROL Authentication]** , immetti un [!UICONTROL Name] e un [!UICONTROL Description] per il flusso di attivazione e compila il [!UICONTROL Account ID] del tuo account di annunci social network.

>[!IMPORTANT]
>
> * Per le destinazioni [!DNL Facebook], **[!UICONTROL Account ID]** è il tuo [!DNL Facebook Ad Account ID]. Puoi trovare questo ID in [!DNL Facebook Ads Manager]. Aggiungi il prefisso `act_` all’ID, come illustrato di seguito.
> * Per le destinazioni [!DNL LinkedIn], **[!UICONTROL Account ID]** è il tuo [!DNL LinkedIn Campaign Manager Account ID]. Puoi trovare questo ID in [!DNL LinkedIn Campaign Manager].


![Connessione alla destinazione social - passaggio di autenticazione](../../assets/catalog/social/workflow/authentication.png)

In questo passaggio, puoi anche selezionare qualsiasi **[!UICONTROL Marketing action]** da applicare a questa destinazione. Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

Selezionare **[!UICONTROL Create Destination]** dopo aver compilato i campi precedenti.

La destinazione viene ora creata. Puoi selezionare **[!UICONTROL Save & Exit]** se desideri attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva [Attivare i segmenti sui social network](#activate-segments), per il resto del flusso di lavoro.

## Attivare i segmenti sui social network {#activate-segments}

Per istruzioni su come attivare i segmenti sui social network, consulta [Attivare i dati sulle destinazioni](../../ui/activate-destinations.md).
