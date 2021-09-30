---
keywords: attivare destinazioni di richiesta profilo;attivare dati;destinazioni di richiesta profilo
title: Attivare i dati del pubblico nelle destinazioni di richiesta del profilo (Beta)
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: Scopri come attivare i dati sul pubblico in Adobe Experience Platform mappando i segmenti sulle destinazioni di richiesta del profilo.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
source-git-commit: 0635828cf3f637e67d2cabda860ca452e61892d4
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Attivare i dati del pubblico nelle destinazioni di richiesta del profilo (Beta)

## Panoramica {#overview}

>[!IMPORTANT]
>
>Le destinazioni di richiesta del profilo in Adobe Experience Platform sono attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Questo articolo spiega il flusso di lavoro necessario per attivare i dati del pubblico nelle destinazioni di richiesta del profilo Adobe Experience Platform. Esempi di destinazioni di richieste di profilo sono le connessioni [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e [Personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md).

## Prerequisiti {#prerequisites}

Per attivare i dati nelle destinazioni, è necessario che [sia stato collegato correttamente a una destinazione](./connect-destination.md). Se non lo hai già fatto, vai al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

### Criterio di unione dei segmenti {#merge-policy}

Attualmente, le destinazioni di richiesta del profilo supportano solo l&#39;attivazione di segmenti che utilizzano il [criterio di unione predefinito](../../segmentation/ui/segment-builder.md#merge-policies).

## Seleziona la destinazione {#select-destination}

1. Vai a **[!UICONTROL Connessioni > Destinazioni]** e seleziona la scheda **[!UICONTROL Catalogo]** .

   ![Scheda Catalogo di destinazione](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Seleziona **[!UICONTROL Attiva i segmenti]** sulla scheda corrispondente alla destinazione in cui desideri attivare i segmenti, come illustrato nell&#39;immagine seguente.

   ![Pulsanti Attiva](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Seleziona la connessione di destinazione che desideri utilizzare per attivare i segmenti, quindi seleziona **[!UICONTROL Avanti]**.

   ![Seleziona destinazione](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Passa alla sezione successiva in [seleziona i segmenti](#select-segments).

## Selezionare i segmenti {#select-segments}

Usa le caselle di controllo a sinistra dei nomi dei segmenti per selezionare i segmenti che desideri attivare nella destinazione, quindi seleziona **[!UICONTROL Avanti]**.

![Selezionare segmenti](../assets/ui/activate-profile-request-destinations/select-segments.png)

## Esportazione di segmenti programmata {#scheduling}

Per impostazione predefinita, la pagina [!UICONTROL Pianificazione segmento] mostra solo i segmenti appena selezionati selezionati nel flusso di attivazione corrente.

![Nuovi segmenti](../assets/ui/activate-profile-request-destinations/new-segments.png)

Per visualizzare tutti i segmenti attivati nella destinazione, utilizza l’opzione di filtro e disabilita il filtro **[!UICONTROL Mostra solo nuovi segmenti]**.

![Tutti i segmenti](../assets/ui/activate-profile-request-destinations/all-segments.png)

Nella pagina **[!UICONTROL Pianificazione segmento]**, seleziona ogni segmento, quindi utilizza i selettori **[!UICONTROL Data di inizio]** e **[!UICONTROL Data di fine]** per configurare l’intervallo di tempo per l’invio dei dati alla destinazione.

![Pianificazione del segmento](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Seleziona **[!UICONTROL Avanti]** per passare alla pagina [!UICONTROL Rivedi].

## Revisione {#review}

Nella pagina **[!UICONTROL Rivedi]** puoi visualizzare un riepilogo della selezione. Seleziona **[!UICONTROL Annulla]** per interrompere il flusso, **[!UICONTROL Indietro]** per modificare le impostazioni oppure **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

>[!IMPORTANT]
>
>In questo passaggio, Adobe Experience Platform verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione dei segmenti finché non avrai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, consulta [Applicazione dei criteri](../../rtcdp/privacy/data-governance-overview.md#enforcement) nella sezione relativa alla governance dei dati .

![violazione dei criteri dei dati](../assets/common/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, selezionare **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

![Revisione](../assets/ui/activate-profile-request-destinations/review.png)

## Verificare l’attivazione dei segmenti {#verify}

Consulta la [documentazione sul monitoraggio della destinazione](../../dataflows/ui/monitor-destinations.md) per informazioni dettagliate su come monitorare il flusso di dati nelle tue destinazioni.