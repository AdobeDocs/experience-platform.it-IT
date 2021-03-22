---
keywords: pubblicità; il banco commerciale;
title: Il collegamento del Trade Desk
description: 'Il Trade Desk è una piattaforma self-service per gli acquirenti di annunci che esegue il retargeting e campagne digitali mirate per il pubblico tra le varie fonti di visualizzazione, video e inventario mobile. '
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# [!DNL The Trade Desk] connection

## Panoramica {#overview}

[!DNL The Trade Desk] La destinazione ti consente di inviare i dati del profilo a  [!DNL The Trade Desk].

[!DNL The Trade Desk] è una piattaforma self-service per gli acquirenti di annunci che esegue il retargeting e campagne digitali mirate per il pubblico tra le sorgenti di visualizzazione, video e inventario mobile.

Per inviare i dati del profilo a [!DNL Trade Desk], è necessario prima connettersi alla destinazione.

## Specifiche di destinazione {#destination-specs}

Tieni presente i seguenti dettagli specifici della destinazione [!DNL Trade Desk]:

* Puoi inviare le seguenti [identità](../../../identity-service/namespaces.md) alle destinazioni [!DNL The Trade Desk]: [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con [!DNL The Trade Desk] e non hai abilitato in passato la [funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio ID di Experience Cloud (con Adobe Audience Manager o altre applicazioni), contatta la Consulenza Adobe o l’Assistenza clienti per abilitare le sincronizzazioni degli ID. Se in precedenza avevi impostato le integrazioni [!DNL The Trade Desk] in Audience Manager, le sincronizzazioni ID che avevi configurato riportano a Platform.

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, voglio essere in grado di utilizzare segmenti generati da [!DNL Trade Desk IDs] o ID dispositivo per creare campagne di retargeting o campagne digitali mirate al pubblico.

## Tipo di esportazione {#export-type}

**[!DNL Segment export]** - stai esportando tutti i membri di un segmento (pubblico) nella destinazione.

## Connetti alla destinazione {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL The Trade Desk] e selezionare **[!UICONTROL Configure]**.

![Configurare La Destinazione Del Desk Commerciale](../../assets/catalog/advertising/tradedesk/configure.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.
>
>![Attiva La Destinazione Del Scrivania](../../assets/catalog/advertising/tradedesk/activate.png)

Nel passaggio [!UICONTROL Authentication], è necessario inserire i dettagli di connessione [!DNL The Trade Desk]:

* **[!UICONTROL Name]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Account ID]**: Il [!DNL Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]**: Chiedi al tuo  [!DNL Trade Desk] rappresentante quale server regionale utilizzare. Questi sono i server regionali disponibili tra cui è possibile scegliere:

   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL North America East]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latin America]**

* **[!UICONTROL Marketing action]**: Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la pagina [Governance dei dati in Adobe Experience Platform](../../../data-governance/policies/overview.md) . Per informazioni sulle singole azioni di marketing definite da Adobe, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

![Passaggio di autenticazione del desktop commerciale](../../assets/catalog/advertising/tradedesk/authenticate.png)

Fai clic su **[!UICONTROL Create destination]**. La destinazione viene ora creata. Puoi fare clic su [!UICONTROL Save & Exit] se desideri attivare i segmenti in un secondo momento oppure puoi selezionare [!UICONTROL Next] per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva [Attiva segmenti](#activate-segments), per il resto del flusso di lavoro.

## Attiva segmenti {#activate-segments}

Per informazioni sul flusso di lavoro di attivazione dei segmenti, consulta [Attivare profili e segmenti su una destinazione](../../ui/activate-destinations.md#select-attributes) .

Nel passaggio [Pianificazione segmento](../../ui/activate-destinations.md#segment-schedule) , devi mappare manualmente i segmenti sul loro ID o nome descrittivo corrispondente nella destinazione.

Durante la mappatura dei segmenti, è consigliabile utilizzare il nome del segmento [!DNL Platform] o una sua forma più breve, per facilitarne l’utilizzo. Tuttavia, l&#39;ID o il nome del segmento nella destinazione non deve necessariamente corrispondere a quello nel tuo account [!DNL Platform] . Qualsiasi valore inserito nel campo di mappatura verrà riflesso dalla destinazione.

Se utilizzi più mappature dispositivo (ID cookie, [!DNL IDFA], [!DNL GAID]), assicurati di utilizzare lo stesso valore di mappatura per tutte e tre le mappature. [!DNL The Trade Desk] li aggrega in un singolo segmento, con una suddivisione a livello di dispositivo.

![ID mappatura segmento](../../assets/common/segment-mapping-id.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL The Trade Desk] , controlla il tuo account [!DNL Trade Desk] . Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nel tuo account.
