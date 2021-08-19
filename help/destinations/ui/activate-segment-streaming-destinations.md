---
keywords: attivare destinazioni di streaming di segmenti;attivare destinazioni di streaming di segmenti;attivare dati
title: Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming
type: Tutorial
seo-title: Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming
description: Scopri come attivare i dati del pubblico in Adobe Experience Platform mappando i segmenti sulle destinazioni di streaming dei segmenti.
seo-description: Scopri come attivare i dati del pubblico in Adobe Experience Platform mappando i segmenti sulle destinazioni di streaming dei segmenti.
source-git-commit: c3e273c66ffe0542258e5418104e0bcf154f5235
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---


# Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming

## Panoramica {#overview}

Questo articolo spiega il flusso di lavoro necessario per attivare i dati del pubblico nelle destinazioni di streaming dei segmenti di Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Per attivare i dati nelle destinazioni, è necessario che [sia stato collegato correttamente a una destinazione](./connect-destination.md). Se non lo hai già fatto, vai al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

## Seleziona la destinazione {#select-destination}

1. Vai a **[!UICONTROL Connessioni > Destinazioni]** e seleziona la scheda **[!UICONTROL Sfoglia]** .

   ![Scheda Sfoglia per destinazione](../assets/ui/activate-segment-streaming-destinations/browse-tab.png)

1. Seleziona il pulsante **[!UICONTROL Aggiungi segmenti]** corrispondente alla destinazione in cui desideri attivare i segmenti, come illustrato nell’immagine seguente.

   ![Pulsanti Attiva](../assets/ui/activate-segment-streaming-destinations/activate-buttons-browse.png)

1. Passa alla sezione successiva in [seleziona i segmenti](#select-segments).

## Selezionare i segmenti {#select-segments}

Usa le caselle di controllo a sinistra dei nomi dei segmenti per selezionare i segmenti che desideri attivare nella destinazione, quindi seleziona **[!UICONTROL Avanti]**.

![Selezionare segmenti](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## Mappare attributi e identità {#mapping}

>[!IMPORTANT]
>
>Questo passaggio si applica solo ad alcune destinazioni di streaming di segmenti. Se la destinazione non dispone di un passaggio **[!UICONTROL Mapping]**, passa a [Pianifica esportazione segmento](#scheduling).

Alcune destinazioni di streaming di segmenti richiedono di selezionare gli attributi di origine o i namespace di identità da mappare come identità di destinazione nella destinazione.

1. Nella pagina **[!UICONTROL Mappatura]**, seleziona **[!UICONTROL Aggiungi nuova mappatura]**.

   ![Aggiungi nuova mappatura](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Selezionare la freccia a destra della voce **[!UICONTROL Campo origine]**.

   ![Selezionare il campo di origine](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. Nella pagina **[!UICONTROL Seleziona campo di origine]**, utilizza le opzioni **[!UICONTROL Seleziona attributi]** o **[!UICONTROL Seleziona namespace identità]** per passare alle due categorie di campi di origine disponibili. Seleziona gli attributi di profilo e gli spazi dei nomi di identità disponibili [!DNL XDM] per eseguire la mappatura sulla destinazione, quindi scegli **[!UICONTROL Seleziona]**.

   ![Seleziona la pagina del campo di origine](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Seleziona il pulsante a destra della voce **[!UICONTROL Campo di destinazione]**.

   ![Selezionare il campo di destinazione](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. Nella pagina **[!UICONTROL Seleziona campo di destinazione]** , seleziona lo spazio dei nomi dell’identità di destinazione in cui desideri mappare il campo di origine e scegli **[!UICONTROL Seleziona]**.

   ![Seleziona la pagina del campo di destinazione](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Per aggiungere altre mappature, ripeti i passaggi da 1 a 5.

### Applica trasformazione {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Applica trasformazione"
>abstract="Seleziona questa opzione quando utilizzi campi sorgente con hash non crittografati per fare in modo che Adobe Experience Platform li hash automaticamente all’attivazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#apply-transformation" text="Ulteriori informazioni nella documentazione"

Quando mappi attributi di origine con hash non crittografati su attributi di destinazione per cui si prevede di eseguire l’hashing della destinazione (ad esempio: `email_lc_sha256` o `phone_sha256`), seleziona l&#39;opzione **Applica trasformazione** affinché Adobe Experience Platform esegua automaticamente l&#39;hash degli attributi di origine all&#39;attivazione.

![Mappatura identità](/help/destinations/assets/ui/activate-segment-streaming-destinations/mapping-summary.png)


## Esportazione di segmenti programmata {#scheduling}

1. Nella pagina **[!UICONTROL Pianificazione segmento]**, seleziona ogni segmento, quindi utilizza i selettori **[!UICONTROL Data di inizio]** e **[!UICONTROL Data di fine]** per configurare l’intervallo di tempo per l’invio dei dati alla destinazione.

   ![Pianificazione del segmento](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * Per alcune destinazioni è necessario selezionare **[!UICONTROL Origine del pubblico]** per ciascun segmento, utilizzando il menu a discesa sotto i selettori del calendario. Se la destinazione non include questo selettore, salta questo passaggio.

      ![ID mappatura](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Alcune destinazioni richiedono la mappatura manuale dei segmenti [!DNL Platform] sulla loro controparte nella destinazione di destinazione. A questo scopo, seleziona ogni segmento, quindi inserisci l’ID del segmento corrispondente dalla piattaforma di destinazione nel campo **[!UICONTROL ID mappatura]** . Se la destinazione non include questo campo, salta questo passaggio.

      ![ID mappatura](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Alcune destinazioni richiedono l’immissione di un **[!UICONTROL ID app]** durante l’attivazione dei segmenti [!DNL IDFA] o [!DNL GAID]. Se la destinazione non include questo campo, salta questo passaggio.

      ![ID app](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Seleziona **[!UICONTROL Avanti]** per passare alla pagina [!UICONTROL Rivedi].

## Revisione {#review}

Nella pagina **[!UICONTROL Rivedi]** puoi visualizzare un riepilogo della selezione. Seleziona **[!UICONTROL Annulla]** per interrompere il flusso, **[!UICONTROL Indietro]** per modificare le impostazioni oppure **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

>[!IMPORTANT]
>
>In questo passaggio, Adobe Experience Platform verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione dei segmenti finché non avrai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, consulta [Applicazione dei criteri](../../rtcdp/privacy/data-governance-overview.md#enforcement) nella sezione relativa alla governance dei dati .

![violazione dei criteri dei dati](../assets/common/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, selezionare **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

![Revisione](../assets/ui/activate-segment-streaming-destinations/review.png)

## Verificare l’attivazione dei segmenti {#verify}

Controlla il tuo account di destinazione. Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nella piattaforma di destinazione.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
