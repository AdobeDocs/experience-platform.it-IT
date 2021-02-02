---
keywords: 'pubblicità; bing; '
title: Destinazione Bing Microsoft
seo-title: La destinazione Microsoft Bing consente di inviare i dati del profilo a Microsoft Display Advertising.
description: Con la destinazione Microsoft Bing, è possibile eseguire il retargeting e campagne digitali mirate per l'audience in Microsoft Display Advertising.
seo-description: Con la destinazione Microsoft Bing, è possibile eseguire il retargeting e campagne digitali mirate per l'audience in Microsoft Display Advertising.
translation-type: tm+mt
source-git-commit: 95f57f9d1b3eeb0b16ba209b9774bd94f5758009
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---


# [!DNL Microsoft Bing] destinazione

## Panoramica {#overview}

La destinazione [!DNL Microsoft Bing] consente di inviare i dati del profilo a [!DNL Microsoft Display Advertising].

Per inviare i dati del profilo a [!DNL Microsoft Bing], è innanzitutto necessario connettersi alla destinazione.

## Specifiche di destinazione {#destination-specs}

Notate i seguenti dettagli specifici della destinazione [!DNL Microsoft Bing]:

* È possibile inviare le seguenti [identità](../../../identity-service/namespaces.md) alle [!DNL Microsoft Bing] destinazioni: [!DNL Microsoft ID].

## Casi d’uso {#use-cases}

In qualità di esperto di marketing, voglio poter utilizzare i segmenti generati da [!DNL Microsoft Advertising IDs] per indirizzare gli utenti attraverso la pubblicità video attraverso i canali [!DNL Microsoft Advertising].

## Tipo di esportazione {#export-type}

**[!DNL Segment Export]** - tutti i membri di un segmento (pubblico) vengono esportati verso la  [!DNL Microsoft Bing] destinazione.

## Prerequisiti {#prerequisites}

Durante la configurazione della destinazione verrà richiesto di fornire le seguenti informazioni:

* [!UICONTROL Account ID]: questo è il vostro  [!DNL Bing Ads CID], in formato intero.

## Connetti alla destinazione {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Microsoft Bing], quindi selezionare **[!UICONTROL Configure]**.

![Configurare la destinazione di Microsoft Bing](../../assets/catalog/advertising/bing/configure.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, fare riferimento alla sezione [Catalog](../../ui/destinations-workspace.md#catalog) della documentazione relativa all&#39;area di lavoro di destinazione.
>
>![Attiva destinazione Bing Microsoft](../../assets/catalog/advertising/bing/activate.png)

Nel passaggio [!UICONTROL Authentication], è necessario immettere i dettagli di connessione di destinazione:

* **[!UICONTROL Name]**: Un nome con cui riconoscerete questa destinazione in futuro.
* **[!UICONTROL Description]**: Descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Account ID]**: Il [!DNL Bing Ads CID].
* **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, vedere la pagina [Governance dei dati in Adobe Experience Platform](../../../data-governance/policies/overview.md). Per informazioni sui singoli casi d&#39;uso di marketing definiti dal Adobe , vedere la [panoramica dei criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

![Autenticazione destinazione Bing Microsoft](../../assets/catalog/advertising/bing/authentication.png)

Fai clic su **[!UICONTROL Create destination]**. La destinazione è stata creata. È possibile fare clic su [!UICONTROL Save & Exit] se si desidera attivare i segmenti in un secondo momento oppure fare clic su [!UICONTROL Next] per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, vedere la sezione successiva, [Attiva segmenti](#activate-segments), per il resto del flusso di lavoro.

## Attivare i segmenti {#activate-segments}

Per informazioni sul flusso di lavoro di attivazione dei segmenti, vedere [Attivare profili e segmenti in una destinazione](../../ui/activate-destinations.md#select-attributes).

Nel passaggio [Programmazione segmenti](../../ui/activate-destinations.md#segment-schedule), devi mappare manualmente i segmenti sul relativo ID o nome descrittivo nella destinazione.

Per la mappatura dei segmenti, si consiglia di utilizzare il nome del segmento [!DNL Platform] o una forma più breve, per semplificare l&#39;utilizzo. Tuttavia, l&#39;ID o il nome del segmento nella destinazione non deve corrispondere a quello nell&#39;account [!DNL Platform]. Qualsiasi valore inserito nel campo di mappatura verrà riflesso dalla destinazione.

![ID mappatura segmento](../../assets/common/segment-mapping-id.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Microsoft Bing], controlla il tuo account [!DNL Microsoft Bing Ads]. Se l&#39;attivazione ha avuto esito positivo, l&#39;audience viene popolata nel vostro account.