---
keywords: attivare destinazioni di richiesta profilo;attivare dati;destinazioni di richiesta profilo
title: Attivare i dati del pubblico nelle destinazioni di richiesta del profilo
type: Tutorial
description: Scopri come attivare i dati sul pubblico in Adobe Experience Platform mappando i segmenti sulle destinazioni di richiesta del profilo.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: cda4591021c5b0a0bd6f43765d72b5867ec59aea
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# Attivare i dati del pubblico nelle destinazioni di richiesta del profilo

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

## Panoramica {#overview}

Questo articolo spiega il flusso di lavoro necessario per attivare i dati del pubblico nelle destinazioni di richiesta del profilo Adobe Experience Platform. Se utilizzati insieme con [segmentazione dei bordi](../../segmentation/ui/edge-segmentation.md), queste destinazioni abilitano casi d’uso per la personalizzazione della stessa pagina e della pagina successiva sulle proprietà web. Ulteriori informazioni [abilitare i casi d’uso per la personalizzazione tra pagine e pagine successive](/help/destinations/ui/configure-personalization-destinations.md).

Esempi di destinazioni di richieste di profilo sono le [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e [Personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md) connessioni.

## Prerequisiti {#prerequisites}

Per attivare i dati nelle destinazioni, è necessario aver completato l&#39;operazione [connesso a una destinazione](./connect-destination.md). Se non lo hai già fatto, vai alla [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni di personalizzazione supportate e configura la destinazione che desideri utilizzare.

### Criterio di unione dei segmenti {#merge-policy}

Attualmente, le destinazioni di richiesta del profilo supportano solo l’attivazione di segmenti che utilizzano il [Criteri di unione attivi su Edge](../../segmentation/ui/segment-builder.md#merge-policies) impostato come predefinito.

## Seleziona la destinazione {#select-destination}

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, quindi seleziona la **[!UICONTROL Catalogo]** scheda .

   ![Scheda Catalogo di destinazione](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Seleziona **[!UICONTROL Attivare i segmenti]** sulla scheda corrispondente alla destinazione di personalizzazione in cui desideri attivare i segmenti, come illustrato di seguito.

   ![Pulsanti Attiva](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Seleziona la connessione di destinazione che desideri utilizzare per attivare i segmenti, quindi seleziona **[!UICONTROL Successivo]**.

   ![Seleziona destinazione](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Passa alla sezione successiva in [seleziona i segmenti](#select-segments).

## Selezionare i segmenti {#select-segments}

Utilizza le caselle di controllo a sinistra dei nomi dei segmenti per selezionare i segmenti che desideri attivare nella destinazione, quindi seleziona **[!UICONTROL Successivo]**.

![Selezionare segmenti](../assets/ui/activate-profile-request-destinations/select-segments.png)

## (Beta) Mappatura attributi {#map-attributes}

>[!IMPORTANT]
>
>La fase di mappatura, che abilita la personalizzazione basata sugli attributi per [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) e [destinazioni di personalizzazione generiche](/help/destinations/catalog/personalization/custom-personalization.md), è attualmente in versione beta e la tua organizzazione potrebbe non averne ancora accesso. Questa documentazione è soggetta a modifiche.

Seleziona gli attributi in base ai quali desideri abilitare i casi di utilizzo della personalizzazione per gli utenti. Ciò significa che se il valore di un attributo cambia o se viene aggiunto un attributo a un profilo, quel profilo diventerà membro del segmento e verrà attivato nella destinazione di personalizzazione.

L’aggiunta di attributi è facoltativa e puoi comunque procedere al passaggio successivo e abilitare la personalizzazione della stessa pagina e della pagina successiva senza selezionare gli attributi. Se non aggiungi attributi in questo passaggio, la personalizzazione si verificherà comunque in base alle qualifiche di appartenenza del segmento e di mappa di identità per i profili.

![Immagine che mostra la fase di mappatura con un attributo selezionato](../assets/ui/activate-profile-request-destinations/mapping-step.png)

### Selezionare gli attributi di origine {#select-source-attributes}

Per aggiungere gli attributi di origine, seleziona la **[!UICONTROL Aggiungi nuovo campo]** sul controllo **[!UICONTROL Campo di origine]** cerca o fai clic sul campo dell’attributo XDM desiderato, come illustrato di seguito.

![Registrazione su schermo che mostra come selezionare un attributo di destinazione nella fase di mappatura](../assets/ui/activate-profile-request-destinations/mapping-step-select-attribute.gif)

### Selezionare gli attributi di destinazione {#select-target-attributes}

>[!NOTE]
>
>Alcune destinazioni richiedono di selezionare solo gli attributi di origine, mentre altre richiedono sia gli attributi di origine che quelli di destinazione.
>
>Attualmente, il [Adobe Target V2](../catalog/personalization/adobe-target-connection.md) la destinazione richiede solo gli attributi di origine, mentre [Personalizzazione personalizzata con attributi](../catalog/personalization/custom-personalization.md) richiede gli attributi di origine e di destinazione.

Per aggiungere gli attributi di destinazione, seleziona la **[!UICONTROL Aggiungi nuovo campo]** sul controllo **[!UICONTROL Campo di destinazione]** e digitare il nome dell&#39;attributo personalizzato a cui si desidera mappare l&#39;attributo di origine.

![Registrazione su schermo che mostra come selezionare un attributo XDM nella fase di mappatura](../assets/ui/activate-profile-request-destinations/mapping-step-select-target-attribute.gif)

## Esportazione di segmenti programmata {#scheduling}

Per impostazione predefinita, la [!UICONTROL Pianificazione del segmento] mostra solo i segmenti appena selezionati selezionati selezionati nel flusso di attivazione corrente.

![Nuovi segmenti](../assets/ui/activate-profile-request-destinations/new-segments.png)

Per visualizzare tutti i segmenti che vengono attivati nella destinazione, utilizza l’opzione di filtro e disattiva il **[!UICONTROL Mostra solo nuovi segmenti]** filtro.

![Tutti i segmenti](../assets/ui/activate-profile-request-destinations/all-segments.png)

Sulla **[!UICONTROL Pianificazione del segmento]** , seleziona ogni segmento, quindi utilizza la **[!UICONTROL Data di inizio]** e **[!UICONTROL Data di fine]** selettori per configurare l’intervallo di tempo per l’invio di dati alla destinazione.

![Pianificazione del segmento](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Seleziona **[!UICONTROL Successivo]** per passare al [!UICONTROL Revisione] pagina.

## Revisione {#review}

Sulla **[!UICONTROL Revisione]** per visualizzare un riepilogo della selezione. Seleziona **[!UICONTROL Annulla]** per interrompere il flusso, **[!UICONTROL Indietro]** per modificare le impostazioni, oppure **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

>[!IMPORTANT]
>
>In questo passaggio, Adobe Experience Platform verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione dei segmenti finché non avrai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, vedi [Applicazione delle politiche](../../rtcdp/privacy/data-governance-overview.md#enforcement) nella sezione documentazione sulla governance dei dati .

![violazione dei criteri dei dati](../assets/common/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, seleziona **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

![Revisione](../assets/ui/activate-profile-request-destinations/review.png)

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->