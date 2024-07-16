---
title: Attivare i tipi di pubblico Audience Manager tramite attivazione espansa
description: Scopri come attivare i tipi di pubblico di Audience Manager nelle destinazioni social e pubblicitarie tramite Audience Manager Expanded Activation.
exl-id: 4105f5c5-db69-414f-9ee4-8630b0a86da7
source-git-commit: 2222e9fbf75f3082d331868f820247e0c0ce3ba2
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Attivare i tipi di pubblico tramite Attivazione espansa di Audience Manager

Questa pagina descrive il flusso di lavoro end-to-end da seguire per attivare i tipi di pubblico da Audience Manager alle piattaforme di destinazione supportate da Attivazione espansa.

## Prima di iniziare {#before-you-begin}

I passaggi descritti in questa guida presuppongono che tu abbia letto la [pagina Panoramica di Expanded Activation](overview.md) e che tu abbia confermato di soddisfare i prerequisiti per l&#39;attivazione del pubblico.

>[!IMPORTANT]
>
>Per attivare i tipi di pubblico tramite [!DNL Expanded Activation], assicurati che i tipi di pubblico di Audience Manager siano basati su **indirizzi e-mail con hash**. Per ulteriori dettagli, vedi [prerequisiti](overview.md#prerequisites).

## Passaggio 1: configurare la connessione sorgente Audience Manager {#configure-source}

Il [connettore di origine Audience Manager](../sources/connectors/adobe-applications/audience-manager.md) invia i dati del pubblico raccolti in Adobe Audience Manager per l&#39;attivazione nelle piattaforme di destinazione supportate dall&#39;attivazione espansa.

Segui la guida su come [creare una connessione sorgente di Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) per configurare il connettore di origine.

![Immagine dell&#39;interfaccia utente di Platform che mostra la scheda Sources (Origini) con la connessione di origine Audience Manager.](assets/sources-tab.png)

>[!TIP]
>
>Il connettore di origine di Adobe Audience Manager è l’unico connettore di origine disponibile in Attivazione espansa.
>
>Se desideri acquisire tipi di pubblico in base a identificatori aggiuntivi, devi acquistare un&#39;edizione di [Real-Time CDP](../rtcdp/overview.md). Per ulteriori informazioni, contatta il rappresentante di Adobe.

### Visualizzare e monitorare i tipi di pubblico acquisiti {#view-audiences}

I tipi di pubblico inseriti in Attivazione espansa da Audience Manager sono disponibili per la visualizzazione nel dashboard **[!UICONTROL Tipi di pubblico]**.

Per visualizzare i tipi di pubblico, passa a **[!UICONTROL Cliente]** -> **[!UICONTROL Tipi di pubblico]** -> **[!UICONTROL Sfoglia]**.

![Immagine dell&#39;interfaccia utente di Platform che mostra la pagina Tipi di pubblico.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* Il pubblico può richiedere fino a 48 ore per essere popolato completamente in Attivazione espansa. Questo vale anche per gli aggiornamenti ai tipi di pubblico Audience Manager esistenti.
>* I tipi di pubblico di Audience Manager appena creati non vengono visualizzati automaticamente in Attivazione espansa. Per acquisire nuovi segmenti in Attivazione espansa, devi aggiungerli tramite il connettore di origine dell’Audience Manager.

Dopo aver configurato il connettore di origine di Audience Manager, passa al [passaggio 2](#create-destination-connection).

## Passaggio 2: creare una nuova connessione di destinazione {#create-destination-connection}

Prima di poter inviare i tipi di pubblico di Audience Manager alla piattaforma di destinazione scelta, devi creare una connessione a una piattaforma di destinazione.

Nella barra laterale a sinistra, vai a **[!UICONTROL Connessioni]** -> **[!UICONTROL Destinazioni]** -> **[!UICONTROL Catalogo]**.

Le categorie disponibili per [!DNL Expanded Activation] sono [advertising](../destinations/catalog/advertising/overview.md) e [social](../destinations/catalog/social/overview.md).

![Immagine dell&#39;interfaccia utente di Platform che mostra il catalogo di destinazione per l&#39;attivazione espansa.](assets/destination-catalog.png)

Per creare una nuova connessione a una piattaforma di destinazione, seguire la guida su [come creare una nuova connessione di destinazione](../destinations/ui/connect-destination.md). Quindi, passare al [passaggio 3](#activate-audiences).

## Passaggio 3: attivare i tipi di pubblico nella destinazione {#activate-audiences}

Dopo aver acquisito correttamente [i tipi di pubblico Audience Manager](#configure-source) e [creato una nuova connessione di destinazione](#create-destination-connection), ora puoi attivare i tipi di pubblico nella piattaforma di destinazione desiderata.

![Immagine dell&#39;interfaccia utente di Platform che mostra il catalogo di destinazione per l&#39;attivazione espansa.](assets/activate-audiences.png)

Per attivare i tipi di pubblico nella tua destinazione, segui la guida su [come attivare i tipi di pubblico nelle destinazioni di streaming](../destinations/ui/activate-segment-streaming-destinations.md).

## Verificare l’attivazione del pubblico {#verify}

Per informazioni dettagliate su come monitorare il flusso di dati verso le destinazioni, consulta la [documentazione sul monitoraggio della destinazione](../dataflows/ui/monitor-destinations.md).
