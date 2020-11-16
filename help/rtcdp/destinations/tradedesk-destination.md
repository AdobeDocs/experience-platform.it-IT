---
keywords: advertising; the trade desk;
title: Destinazione scrivania
seo-title: Destinazione scrivania
description: 'Il Trade Desk è una piattaforma self-service per gli acquirenti di annunci che esegue retargeting e campagne digitali mirate per il pubblico attraverso fonti di visualizzazione, video e inventario mobile. '
seo-description: Il Trade Desk è una piattaforma self-service per gli acquirenti di annunci che esegue retargeting e campagne digitali mirate per il pubblico attraverso fonti di visualizzazione, video e inventario mobile.
translation-type: tm+mt
source-git-commit: 43795e31f4e39dcabeaf6d69529e80cabe9c90c5
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# [!DNL The Trade Desk] destinazione

## Panoramica {#overview}

[!DNL The Trade Desk] la destinazione consente di inviare i dati del profilo a [!DNL The Trade Desk].

[!DNL The Trade Desk] è una piattaforma self-service per gli acquirenti di annunci che consente di eseguire il retargeting e campagne digitali mirate per il pubblico attraverso le origini di visualizzazione, video e inventario mobile.

Per inviare i dati del profilo a [!DNL The Trade Desk], è innanzitutto necessario connettersi alla destinazione.

## Specifiche di destinazione {#destination-specs}

Notate i seguenti dettagli specifici per la [!DNL The Trade Desk] destinazione:

* Puoi inviare le seguenti [identità](../../identity-service/namespaces.md) alle [!DNL The Trade Desk] destinazioni: [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

## Casi d’uso {#use-cases}

In qualità di esperto di marketing, voglio poter utilizzare i segmenti generati da ID dispositivo [!DNL Trade Desk IDs] o dispositivo per creare retargeting o campagne digitali mirate per l&#39;audience.

## Tipo di esportazione {#export-type}

**[!DNL Segment export]** - tutti i membri di un segmento (pubblico) vengono esportati verso la destinazione.

## Connetti alla destinazione {#connect-destination}

1. In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL The Trade Desk], quindi **[!UICONTROL Configure]**.

   ![Configurare La Destinazione Del Desktop Commerciale](assets/tradedesk-destination-configure.png)

   >[!NOTE]
   >
   >Se esiste già una connessione con questa destinazione, è possibile visualizzare un **[!UICONTROL Activate]** pulsante sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consultate la sezione [Catalogo](../destinations/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

       ![Attiva Destinazione Scrivania Commerciale](assets/tradedesk-destination-activate.png)
   
2. Nel [!UICONTROL Authentication] passaggio, è necessario inserire i dettagli di [!DNL The Trade Desk] connessione:

   * **[!UICONTROL Name]**: Un nome con cui riconoscerete questa destinazione in futuro.
   * **[!UICONTROL Description]**: Descrizione che ti aiuterà a identificare questa destinazione in futuro.
   * **[!UICONTROL Account ID]**: Il [!DNL Trade Desk] [!UICONTROL Account ID].
   * **[!UICONTROL Client Secret]**: Il `clientSecret` parametro utilizzato nelle credenziali [!DNL OAuth2] client.
   * **[!UICONTROL Server Location]**: Chiedi al tuo [!DNL The Trade Desk] rappresentante quale server regionale utilizzare. Sono disponibili i seguenti server regionali:

      * **[!UICONTROL Europe]**
      * **[!UICONTROL Singapore]**
      * **[!UICONTROL Tokyo]**
      * **[!UICONTROL North America East]**
      * **[!UICONTROL North America West]**
      * **[!UICONTROL Latin America]**
   * **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in Adobe Experience Platform](../privacy/data-governance-overview.md#destinations) . Per informazioni sui singoli casi di utilizzo marketing definiti dal Adobe , consulta la panoramica [sui criteri di utilizzo dei](../../data-governance/policies/overview.md#core-actions)dati.

   ![Passaggio Autenticazione Desktop Commerciale](assets/tradedesk-destination-authentication.png)

3. Fai clic su **[!UICONTROL Create destination]**. La destinazione è stata creata. Puoi fare clic su [!UICONTROL Save & Exit] se vuoi attivare i segmenti in un secondo momento, oppure puoi selezionare [!UICONTROL Next] per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva, [Attiva segmenti](#activate-segments), per il resto del flusso di lavoro.

## Attivare i segmenti {#activate-segments}

Consulta [Attivare profili e segmenti su una destinazione](activate-destinations.md#select-attributes) per informazioni sul flusso di lavoro di attivazione dei segmenti.

Nel passaggio della pianificazione [](activate-destinations.md#segment-schedule) Segmento, devi mappare manualmente i segmenti sul relativo ID o nome descrittivo nella destinazione.

Per la mappatura dei segmenti, si consiglia di utilizzare il nome del [!DNL Platform] segmento o una forma più breve, per facilitarne l’uso. Tuttavia, l’ID o il nome del segmento nella destinazione non deve necessariamente corrispondere a quello nel tuo [!DNL Platform] account. Qualsiasi valore inserito nel campo di mappatura verrà riflesso dalla destinazione.

Se utilizzate più mappature dispositivo (ID cookie [!DNL IDFA], [!DNL GAID]), accertatevi di utilizzare lo stesso valore di mappatura per tutte e tre le mappature. [!DNL The Trade Desk] vengono aggregati tutti in un singolo segmento, con una suddivisione a livello di dispositivo.

![ID mappatura segmento](assets/segment-mapping-id.png)


## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella [!DNL The Trade Desk] destinazione, controlla il tuo [!DNL The Trade Desk] account. Se l&#39;attivazione ha avuto esito positivo, l&#39;audience viene popolata nel vostro account.
