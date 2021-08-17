---
keywords: attivare destinazioni di streaming di segmenti;attivare destinazioni di streaming di segmenti;attivare dati
title: Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming
type: Tutorial
seo-title: Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming
description: Scopri come attivare i dati del pubblico in Adobe Experience Platform mappando i segmenti sulle destinazioni di streaming dei segmenti.
seo-description: Scopri come attivare i dati del pubblico in Adobe Experience Platform mappando i segmenti sulle destinazioni di streaming dei segmenti.
source-git-commit: 65e74041aeb285cb80c67e47ccdaca18de9889fa
workflow-type: tm+mt
source-wordcount: '1165'
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

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Applica trasformazione"
>abstract="Seleziona questa opzione quando utilizzi campi sorgente con hash non crittografati per fare in modo che Adobe Experience Platform li hash automaticamente all’attivazione."

>[!IMPORTANT]
>
>Questo passaggio si applica solo ad alcune destinazioni di streaming di segmenti. Se le destinazioni non dispongono di un passaggio **[!UICONTROL Mapping]**, passa a [Pianifica esportazione segmento](#scheduling).

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

### Esempio di mappatura: attivazione dei dati sul pubblico in [!DNL Facebook Custom Audience] {#example-facebook}

Di seguito è riportato un esempio di mappatura corretta dell&#39;identità durante l&#39;attivazione dei dati sul pubblico in [!DNL Facebook Custom Audience].

Selezione dei campi di origine:

* Seleziona lo spazio dei nomi `Email` come identità di origine se gli indirizzi e-mail utilizzati non sono con hash.
* Seleziona lo spazio dei nomi `Email_LC_SHA256` come identità di origine se hai hashing gli indirizzi e-mail dei clienti durante l’inserimento dei dati in [!DNL Platform], in base a [!DNL Facebook] [requisiti di hashing e-mail](../catalog/social/facebook.md#email-hashing-requirements).
* Seleziona lo spazio dei nomi `PHONE_E.164` come identità di origine se i dati sono costituiti da numeri di telefono non crittografati. [!DNL Platform] cancellerà i numeri di telefono per conformarsi ai  [!DNL Facebook] requisiti.
* Seleziona lo spazio dei nomi `Phone_SHA256` come identità di origine se hai hashing i numeri di telefono durante l’inserimento dei dati in [!DNL Platform], in base ai [!DNL Facebook] [requisiti di hashing del numero di telefono](../catalog/social/facebook.md#phone-number-hashing-requirements).
* Seleziona lo spazio dei nomi `IDFA` come identità di origine se i dati sono costituiti da [!DNL Apple] ID dispositivo.
* Seleziona lo spazio dei nomi `GAID` come identità di origine se i dati sono costituiti da [!DNL Android] ID dispositivo.
* Seleziona lo spazio dei nomi `Custom` come identità di origine se i dati sono costituiti da un altro tipo di identificatori.

Selezione dei campi di destinazione:

* Selezionare lo spazio dei nomi `Email_LC_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `Email` o `Email_LC_SHA256`.
* Selezionare lo spazio dei nomi `Phone_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `PHONE_E.164` o `Phone_SHA256`.
* Selezionare i namespace `IDFA` o `GAID` come identità di destinazione quando i namespace di origine sono `IDFA` o `GAID`.
* Seleziona lo spazio dei nomi `Extern_ID` come identità di destinazione quando lo spazio dei nomi di origine è personalizzato.

>[!IMPORTANT]
>
>I dati provenienti da spazi dei nomi senza hash vengono automaticamente hashing da [!DNL Platform] al momento dell’attivazione.
> 
>I dati di origine degli attributi non vengono crittografati automaticamente. Quando il campo di origine contiene attributi senza hash, seleziona l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione.

![Mappatura identità](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

### Esempio di mappatura: attivazione dei dati sul pubblico in [!DNL Google Customer Match] {#example-gcm}

Questo è un esempio di mappatura corretta dell&#39;identità durante l&#39;attivazione dei dati sul pubblico in [!DNL Google Customer Match].

Selezione dei campi di origine:

* Seleziona lo spazio dei nomi `Email` come identità di origine se gli indirizzi e-mail utilizzati non sono con hash.
* Seleziona lo spazio dei nomi `Email_LC_SHA256` come identità di origine se hai hashing gli indirizzi e-mail dei clienti durante l’inserimento dei dati in [!DNL Platform], in base a [!DNL Google Customer Match] [requisiti di hashing e-mail](../catalog/social/../advertising/google-customer-match.md).
* Seleziona lo spazio dei nomi `PHONE_E.164` come identità di origine se i dati sono costituiti da numeri di telefono non crittografati. [!DNL Platform] cancellerà i numeri di telefono per conformarsi ai  [!DNL Google Customer Match] requisiti.
* Seleziona lo spazio dei nomi `Phone_SHA256_E.164` come identità di origine se hai hashing i numeri di telefono durante l’inserimento dei dati in [!DNL Platform], in base ai [!DNL Facebook] [requisiti di hashing del numero di telefono](../catalog/social/../advertising/google-customer-match.md).
* Seleziona lo spazio dei nomi `IDFA` come identità di origine se i dati sono costituiti da [!DNL Apple] ID dispositivo.
* Seleziona lo spazio dei nomi `GAID` come identità di origine se i dati sono costituiti da [!DNL Android] ID dispositivo.
* Seleziona lo spazio dei nomi `Custom` come identità di origine se i dati sono costituiti da un altro tipo di identificatori.

Selezione dei campi di destinazione:

* Selezionare lo spazio dei nomi `Email_LC_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `Email` o `Email_LC_SHA256`.
* Selezionare lo spazio dei nomi `Phone_SHA256_E.164` come identità di destinazione quando gli spazi dei nomi di origine sono `PHONE_E.164` o `Phone_SHA256_E.164`.
* Selezionare i namespace `IDFA` o `GAID` come identità di destinazione quando i namespace di origine sono `IDFA` o `GAID`.
* Seleziona lo spazio dei nomi `User_ID` come identità di destinazione quando lo spazio dei nomi di origine è personalizzato.

![Mappatura identità](../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

I dati provenienti da spazi dei nomi senza hash vengono automaticamente hashing da [!DNL Platform] al momento dell’attivazione.

I dati di origine degli attributi non vengono crittografati automaticamente. Quando il campo di origine contiene attributi senza hash, seleziona l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione.

![Trasformazione mappatura identità](../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

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
