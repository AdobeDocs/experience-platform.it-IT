---
title: Attivare i tipi di pubblico Audienci Manager tramite attivazione espansa
description: Scopri come attivare i tipi di pubblico di Audienci Manager nelle destinazioni social e pubblicitarie tramite Audienci Manager Expanded Activation.
source-git-commit: 19fb369a7faa0c5ac27a34db7b848b0332cb8695
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Attivare i tipi di pubblico tramite Attivazione espansa di Audienci Manager

Questa pagina descrive il flusso di lavoro end-to-end da seguire per attivare i tipi di pubblico da Audienci Manager alle piattaforme di destinazione supportate da Attivazione espansa.

## Prima di iniziare {#before-you-begin}

I passaggi descritti in questa guida presuppongono che tu abbia letto [Pagina Panoramica di Attivazione espansa](overview.md) e hai confermato di soddisfare i prerequisiti per l’attivazione di audience.

>[!IMPORTANT]
>
>Per attivare i tipi di pubblico tramite [!DNL Expanded Activation], assicurati che il pubblico di Audience Manager sia basato su **indirizzi e-mail con hash**. Consulta la [prerequisiti](overview.md#prerequisites) per ulteriori dettagli.

## Passaggio 1: configurare la connessione sorgente Audienci Manager {#configure-source}

Il [Connettore sorgente in Audience Manager](../sources/connectors/adobe-applications/audience-manager.md) invia i dati del pubblico raccolti in Adobe Audience Manager per l’attivazione nelle piattaforme di destinazione supportate da Expanded Activation.

Segui la guida su come [creazione di una connessione sorgente di Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) per configurare il connettore di origine.

![Immagine dell’interfaccia utente di Platform che mostra la scheda Sources (Sorgenti) con la connessione sorgente di Audience Manager.](assets/sources-tab.png)

>[!TIP]
>
>Il connettore di origine di Adobe Audience Manager è l’unico connettore di origine disponibile in Attivazione espansa.
>
>Per acquisire tipi di pubblico in base a identificatori aggiuntivi, è necessario acquistare un’edizione di [Real-Time CDP](../rtcdp/overview.md). Per ulteriori informazioni, contatta il rappresentante di Adobe.

### Visualizzare e monitorare i tipi di pubblico acquisiti {#view-audiences}

I tipi di pubblico che inserisci in Attivazione espansa da Audienci Manager sono disponibili per la visualizzazione in **[!UICONTROL Tipi di pubblico]** dashboard.

Per visualizzare i tipi di pubblico, vai a **[!UICONTROL Cliente]** -> **[!UICONTROL Tipi di pubblico]** -> **[!UICONTROL Sfoglia]**.

![Immagine dell’interfaccia utente di Platform che mostra la pagina Tipi di pubblico.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* Il pubblico può richiedere fino a 48 ore per essere popolato completamente in Attivazione espansa. Questo vale anche per gli aggiornamenti ai tipi di pubblico Audienci Manager esistenti.
>* I tipi di pubblico di Audience Manager appena creati non vengono visualizzati automaticamente in Attivazione espansa. Per acquisire nuovi segmenti in Attivazione espansa, devi aggiungerli tramite il connettore di origine dell’Audience Manager.

Dopo aver configurato il connettore di origine di Audience Manager, passa a [passaggio 2](#create-destination-connection).

## Passaggio 2: creare una nuova connessione di destinazione {#create-destination-connection}

Prima di poter inviare i tipi di pubblico di Audience Manager alla piattaforma di destinazione scelta, devi creare una connessione a una piattaforma di destinazione.

Nella barra laterale a sinistra, vai a **[!UICONTROL Connessioni]** -> **[!UICONTROL Destinazioni]** -> **[!UICONTROL Catalogo]**.

Le categorie di destinazione disponibili per [!DNL Expanded Activation] sono [pubblicità](../destinations/catalog/advertising/overview.md) e [social](../destinations/catalog/social/overview.md).

![Immagine dell’interfaccia utente di Platform che mostra il catalogo di destinazione per l’attivazione espansa.](assets/destination-catalog.png)

Per creare una nuova connessione a una piattaforma di destinazione, segui la guida su [come creare una nuova connessione di destinazione](../destinations/ui/connect-destination.md). Quindi, passa a [passaggio 3](#activate-audiences).

## Passaggio 3: attivare i tipi di pubblico nella destinazione {#activate-audiences}

Dopo aver completato correttamente [pubblico Audienci Manager acquisito](#configure-source) e [ha creato una nuova connessione di destinazione](#create-destination-connection), ora puoi attivare i tipi di pubblico nella piattaforma di destinazione desiderata.

![Immagine dell’interfaccia utente di Platform che mostra il catalogo di destinazione per l’attivazione espansa.](assets/activate-audiences.png)

Per attivare i tipi di pubblico nella destinazione, segui la guida su [come attivare i tipi di pubblico nelle destinazioni di streaming](../destinations/ui/activate-segment-streaming-destinations.md).

## Verificare l’attivazione del pubblico {#verify}

Controlla la [documentazione di monitoraggio della destinazione](../dataflows/ui/monitor-destinations.md) per informazioni dettagliate su come monitorare il flusso di dati verso le destinazioni.