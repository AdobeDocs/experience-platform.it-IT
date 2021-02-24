---
keywords: Facebook;facebook;Social network;Social network;autenticazione social network;Social network;autenticazione social network
title: Creare una destinazione social network
type: Tutorial
description: Scopri come connettersi ai tuoi account di annunci social network in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 19e38faa84d365682e97c2ec1c6352d127c0ac29
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---


# Creare una destinazione social network {#social-network-destinations-workflow}

Questa esercitazione utilizza [!DNL Facebook] come esempio, ma il flusso di lavoro Adobe Experience Platform è lo stesso per tutte le destinazioni dei social network.

In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scorrere fino alla categoria **[!UICONTROL Social]**. Seleziona la destinazione desiderata per il social network, quindi seleziona **[!UICONTROL Configure]**.

![Connessione alla destinazione social network](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, fare riferimento alla sezione [Catalog](../../ui/destinations-workspace.md#catalog) della documentazione relativa all&#39;area di lavoro di destinazione.

Nel passaggio **Autenticazione**, se in precedenza è stata impostata una connessione alla destinazione di social network, selezionare **[!UICONTROL Existing Account]** e selezionare la connessione esistente. In alternativa, potete selezionare **[!UICONTROL New Account]** per impostare una nuova connessione alla destinazione del social network. Selezionate **[!UICONTROL Connect to destination]** per accedere alla destinazione social network selezionata e collegare Adobe Experience Cloud al vostro account annuncio social network.

>[!NOTE]
>
>La piattaforma supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se si immettono credenziali non corrette nell&#39;ID dell&#39;account di rete social. In questo modo si evita di completare il flusso di lavoro con credenziali non corrette.

![Connessione alla destinazione social network - passaggio di autenticazione](../../assets/catalog/social/workflow/pre-connect.png)

Una volta confermate le credenziali e che Adobe Experience Cloud è connesso al social network, potete selezionare **[!UICONTROL Next]** per passare al passaggio **[!UICONTROL Setup]**.

![Credenziali confermate](../../assets/catalog/social/workflow/post-connect.png)

Nel passaggio **[!UICONTROL Setup]**, immetti un [!UICONTROL Name] e un [!UICONTROL Description] per il flusso di attivazione e compila il [!UICONTROL Account ID] del tuo account di social network.

>[!IMPORTANT]
>
> Per le destinazioni [!DNL Facebook], **[!UICONTROL Account ID]** è [!DNL Facebook Ad Account ID]. Questo ID è disponibile nella cartella [!DNL Facebook Ads Manager]. Aggiungi l&#39;ID con `act_` come indicato di seguito:

![Connessione alla destinazione social network - passaggio di configurazione](../../assets/catalog/social/workflow/setup.png)

>[!IMPORTANT]
>
> Per le destinazioni [!DNL LinkedIn], **[!UICONTROL Account ID]** è [!DNL LinkedIn Campaign Manager Account ID]. Questo ID è disponibile nella cartella [!DNL LinkedIn Campaign Manager].

Inoltre in questo passaggio, è possibile selezionare qualsiasi **[!UICONTROL Marketing action]** da applicare a questa destinazione. Le azioni di marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi selezionare  azioni di marketing definite dal Adobe o creare azioni di marketing personalizzate. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sulle politiche di utilizzo dei dati](../../../data-governance/policies/overview.md).

Selezionare **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

La destinazione è stata creata. È possibile selezionare **[!UICONTROL Save & Exit]** se si desidera attivare i segmenti in un secondo momento oppure selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, per il resto del flusso di lavoro, vedi la sezione successiva, [Attivare i segmenti sulle reti sociali](#activate-segments).

## Attivare i segmenti sulle reti sociali {#activate-segments}

Per istruzioni su come attivare i segmenti nei social network, vedi [Activate Data to Destinations](../../ui/activate-destinations.md) (Attiva dati sulle destinazioni).