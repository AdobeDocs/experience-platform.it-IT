---
keywords: attivare destinazioni di richiesta profilo;attivare dati;destinazioni di richiesta profilo
title: Attivare i dati del pubblico nelle destinazioni di richiesta del profilo (Beta)
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: Scopri come attivare i dati sul pubblico in Adobe Experience Platform mappando i segmenti sulle destinazioni di richiesta del profilo.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: d0660f29df93659990d80353f86dcbf856afb733
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Attivare i dati del pubblico nelle destinazioni di richiesta del profilo

## Panoramica {#overview}

Questo articolo spiega il flusso di lavoro necessario per attivare i dati del pubblico nelle destinazioni di richiesta del profilo Adobe Experience Platform. Esempi di destinazioni di richieste di profilo sono le [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e [Personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md) connessioni.

## Prerequisiti {#prerequisites}

Per attivare i dati nelle destinazioni, è necessario aver completato l&#39;operazione [connesso a una destinazione](./connect-destination.md). Se non lo hai già fatto, vai alla [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

### Criterio di unione dei segmenti {#merge-policy}

Attualmente, le destinazioni di richiesta del profilo supportano solo l’attivazione di segmenti che utilizzano il [Criteri di unione attivi su Edge](../../segmentation/ui/segment-builder.md#merge-policies) impostato come predefinito.

## Seleziona la destinazione {#select-destination}

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, quindi seleziona la **[!UICONTROL Catalogo]** scheda .

   ![Scheda Catalogo di destinazione](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Seleziona **[!UICONTROL Attivare i segmenti]** sulla scheda corrispondente alla destinazione in cui desideri attivare i segmenti, come illustrato di seguito.

   ![Pulsanti Attiva](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Seleziona la connessione di destinazione che desideri utilizzare per attivare i segmenti, quindi seleziona **[!UICONTROL Successivo]**.

   ![Seleziona destinazione](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Passa alla sezione successiva in [seleziona i segmenti](#select-segments).

## Selezionare i segmenti {#select-segments}

Utilizza le caselle di controllo a sinistra dei nomi dei segmenti per selezionare i segmenti che desideri attivare nella destinazione, quindi seleziona **[!UICONTROL Successivo]**.

![Selezionare segmenti](../assets/ui/activate-profile-request-destinations/select-segments.png)

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

## Verificare l’attivazione dei segmenti {#verify}

Controlla la [documentazione sul monitoraggio della destinazione](../../dataflows/ui/monitor-destinations.md) per informazioni dettagliate su come monitorare il flusso di dati verso le destinazioni.
