---
keywords: 'pubblicità; bing; '
title: Connessione Microsoft Bing
description: Con la destinazione di connessione Microsoft Bing, è possibile eseguire il retargeting e campagne digitali mirate al pubblico in Microsoft Display Advertising.
translation-type: tm+mt
source-git-commit: 0ef107963f7da377070eb845fd7c24218a99464b
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# [!DNL Microsoft Bing] connection  {#bing-destination}

La destinazione [!DNL Microsoft Bing] ti aiuta a inviare i dati del profilo a [!DNL Microsoft Display Advertising].

Per inviare i dati del profilo a [!DNL Microsoft Bing], è necessario prima connettersi alla destinazione.

## Specifiche di destinazione {#destination-specs}

Tieni presente i seguenti dettagli specifici della destinazione [!DNL Microsoft Bing]:

* Puoi inviare le seguenti [identità](../../../identity-service/namespaces.md) alle destinazioni [!DNL Microsoft Bing]: [!DNL Microsoft ID].

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con [!DNL Microsoft Bing] e non hai abilitato in passato la [funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio ID di Experience Cloud (con Adobe Audience Manager o altre applicazioni), contatta la Consulenza Adobe o l’Assistenza clienti per abilitare le sincronizzazioni degli ID. Se in precedenza avevi impostato le integrazioni [!DNL Microsoft Bing] in Audience Manager, le sincronizzazioni ID che avevi configurato riportano a Platform.

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, voglio essere in grado di utilizzare segmenti generati da [!DNL Microsoft Advertising IDs] per indirizzare gli utenti tramite pubblicità display tra [!DNL Microsoft Advertising] canali.

## Tipo di esportazione {#export-type}

**[!DNL Segment Export]** - stai esportando tutti i membri di un segmento (pubblico) nella  [!DNL Microsoft Bing] destinazione.

## Prerequisiti {#prerequisites}

Durante la configurazione della destinazione, devi fornire le seguenti informazioni:

* [!UICONTROL Account ID]: questo è il  [!DNL Bing Ads CID], in formato intero.

## Connetti alla destinazione {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Microsoft Bing] e selezionare **[!UICONTROL Configure]**.

![Configurare la destinazione Microsoft Bing](../../assets/catalog/advertising/bing/configure.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.
>
>![Attiva destinazione Bing Microsoft](../../assets/catalog/advertising/bing/activate.png)

Nel passaggio [!UICONTROL Authentication] , è necessario inserire i dettagli di connessione di destinazione:

* **[!UICONTROL Name]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Account ID]**: Il [!DNL Bing Ads CID].
* **[!UICONTROL Marketing action]**: Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la pagina [Governance dei dati in Adobe Experience Platform](../../../data-governance/policies/overview.md) . Per informazioni sulle singole azioni di marketing definite da Adobe, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

![Autenticazione destinazione Microsoft Bing](../../assets/catalog/advertising/bing/authentication.png)

Fai clic su **[!UICONTROL Create destination]**. La destinazione viene ora creata. Puoi fare clic su [!UICONTROL Save & Exit] per attivare i segmenti in un secondo momento, oppure puoi fare clic su [!UICONTROL Next] per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva [Attiva segmenti](#activate-segments), per il resto del flusso di lavoro.

## Attiva segmenti {#activate-segments}

Per informazioni sul flusso di lavoro di attivazione dei segmenti, consulta [Attivare profili e segmenti su una destinazione](../../ui/activate-destinations.md#select-attributes) .

Nel passaggio [Pianificazione segmento](../../ui/activate-destinations.md#segment-schedule) , devi mappare manualmente i segmenti sul loro ID o nome descrittivo corrispondente nella destinazione.

Durante la mappatura dei segmenti, è consigliabile utilizzare il nome del segmento [!DNL Platform] o una sua forma più breve, per facilitarne l’utilizzo. Tuttavia, l&#39;ID o il nome del segmento nella destinazione non deve necessariamente corrispondere a quello nel tuo account [!DNL Platform] . Qualsiasi valore inserito nel campo di mappatura verrà riflesso dalla destinazione.

![ID mappatura segmento](../../assets/common/segment-mapping-id.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Microsoft Bing], controlla il tuo account [!DNL Microsoft Bing Ads]. Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nel tuo account.