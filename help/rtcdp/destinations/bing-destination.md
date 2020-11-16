---
keywords: advertising; bing;
title: Destinazione Bing Microsoft
seo-title: La destinazione Microsoft Bing consente di inviare i dati del profilo a Microsoft Display Advertising.
description: Con la destinazione Microsoft Bing, è possibile eseguire il retargeting e campagne digitali mirate per l'audience in Microsoft Display Advertising.
seo-description: Con la destinazione Microsoft Bing, è possibile eseguire il retargeting e campagne digitali mirate per l'audience in Microsoft Display Advertising.
translation-type: tm+mt
source-git-commit: 43795e31f4e39dcabeaf6d69529e80cabe9c90c5
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---


# [!DNL Microsoft Bing] destinazione

## Panoramica {#overview}

La [!DNL Microsoft Bing] destinazione consente di inviare i dati del profilo a [!DNL Microsoft Display Advertising].

Per inviare i dati del profilo a [!DNL Microsoft Bing], è innanzitutto necessario connettersi alla destinazione.

## Specifiche di destinazione {#destination-specs}

Notate i seguenti dettagli specifici per la [!DNL Microsoft Bing] destinazione:

* Puoi inviare le seguenti [identità](../../identity-service/namespaces.md) alle [!DNL Microsoft Bing] destinazioni: [!DNL Microsoft ID].

## Casi d’uso {#use-cases}

In qualità di esperto di marketing, voglio poter utilizzare i segmenti generati [!DNL Microsoft Advertising IDs] per indirizzare gli utenti attraverso la pubblicità del display tra [!DNL Microsoft Advertising] i canali.

## Tipo di esportazione {#export-type}

**[!DNL Segment Export]** - tutti i membri di un segmento (pubblico) vengono esportati verso la [!DNL Microsoft Bing] destinazione.

## Prerequisiti   {#prerequisites}

Durante la configurazione della destinazione verrà richiesto di fornire le seguenti informazioni:

* [!UICONTROL Account ID]: questo è il vostro [!DNL Bing Ads CID], in formato intero.

## Connetti alla destinazione {#connect-destination}

1. In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Microsoft Bing], quindi **[!UICONTROL Configure]**.

   ![Configurare la destinazione di Microsoft Bing](assets/bing-destination-configure.png)

   >[!NOTE]
   >
   >Se esiste già una connessione con questa destinazione, è possibile visualizzare un **[!UICONTROL Activate]** pulsante sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consultate la sezione [Catalogo](../destinations/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

   ![Attiva destinazione Bing Microsoft](assets/bing-destination-activate.png)

1. Nel [!UICONTROL Authentication] passaggio, è necessario immettere i dettagli di connessione di destinazione:

   * **[!UICONTROL Name]**: Un nome con cui riconoscerete questa destinazione in futuro.
   * **[!UICONTROL Description]**: Descrizione che ti aiuterà a identificare questa destinazione in futuro.
   * **[!UICONTROL Account ID]**: Il [!DNL Bing Ads CID].
   * **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in Adobe Experience Platform](../privacy/data-governance-overview.md#destinations) . Per informazioni sui singoli casi di utilizzo marketing definiti dal Adobe , consulta la panoramica [sui criteri di utilizzo dei](../../data-governance/policies/overview.md#core-actions)dati.

   ![Autenticazione destinazione Bing Microsoft](assets/bing-destination-authentication.png)

1. Fai clic su **[!UICONTROL Create destination]**. La destinazione è stata creata. Puoi fare clic su [!UICONTROL Save & Exit] se vuoi attivare i segmenti in un secondo momento, oppure puoi fare clic su per continuare [!UICONTROL Next] il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva, [Attiva segmenti](#activate-segments), per il resto del flusso di lavoro.

## Attivare i segmenti {#activate-segments}

Consulta [Attivare profili e segmenti su una destinazione](activate-destinations.md#select-attributes) per informazioni sul flusso di lavoro di attivazione dei segmenti.

Nel passaggio della pianificazione [](activate-destinations.md#segment-schedule) Segmento, devi mappare manualmente i segmenti sul relativo ID o nome descrittivo nella destinazione.

Per la mappatura dei segmenti, si consiglia di utilizzare il nome del [!DNL Platform] segmento o una forma più breve, per facilitarne l’uso. Tuttavia, l’ID o il nome del segmento nella destinazione non deve necessariamente corrispondere a quello nel tuo [!DNL Platform] account. Qualsiasi valore inserito nel campo di mappatura verrà riflesso dalla destinazione.

![ID mappatura segmento](assets/segment-mapping-id.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella [!DNL Microsoft Bing] destinazione, controlla il tuo [!DNL Microsoft Bing Ads] account. Se l&#39;attivazione ha avuto esito positivo, l&#39;audience viene popolata nel vostro account.