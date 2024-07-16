---
title: Attiva i tipi di pubblico potenziali nelle destinazioni
type: Tutorial
description: Scopri come attivare i tipi di pubblico potenziali per le destinazioni
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 13%

---

# Attiva tipi di pubblico potenziale

>[!AVAILABILITY]
>
>Questa funzionalità è disponibile per i clienti che hanno acquistato il pacchetto Real-Time CDP Prime e Ultimate. Per ulteriori informazioni, contatta il rappresentante del tuo Adobe.

Questo articolo spiega il flusso di lavoro necessario per esportare [tipi di pubblico potenziali](/help/segmentation/ui/prospect-audience.md) da Adobe Experience Platform nella destinazione preferita.

## Destinazioni supportati {#supported-destinations}

Vai a **[!UICONTROL Connessioni]** > **[!UICONTROL Destinazioni]** e seleziona la scheda **[!UICONTROL Catalogo]**. Utilizza il filtro **[!UICONTROL Tipi di dati]** e seleziona **[!UICONTROL Prospect]** per visualizzare le destinazioni che supportano l&#39;attivazione dei tipi di pubblico prospect. Attualmente, l’esportazione dei tipi di pubblico potenziali è disponibile solo per le destinazioni di archiviazione cloud.

![Destinazioni che supportano i tipi di pubblico potenziali.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Prerequisiti {#prerequisites}

* Devi innanzitutto acquisire [profili prospect](/help/profile/ui/prospect-profile.md) e creare [tipi di pubblico prospect](/help/segmentation/ui/prospect-audience.md) prima di poterli attivare nelle destinazioni a valle.
* Per attivare i tipi di pubblico potenziali nelle destinazioni, è necessario essersi collegati correttamente a una destinazione. Se non lo hai già fatto, vai al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare. Per ulteriori informazioni, leggi l&#39;esercitazione dell&#39;interfaccia utente su [connessione alle destinazioni](./connect-destination.md).

### Autorizzazioni richieste {#permissions}

Per attivare i tipi di pubblico potenziali, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e **[!UICONTROL Destinazioni attivazione]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per assicurarti di disporre delle autorizzazioni necessarie per attivare i tipi di pubblico potenziali, sfoglia il catalogo delle destinazioni. Se una destinazione dispone di un controllo **[!UICONTROL Attiva]**, si dispone delle autorizzazioni appropriate.

## Seleziona la destinazione {#select-destination}

Segui le istruzioni per selezionare una destinazione in cui puoi esportare i set di dati:

1. Vai a **[!UICONTROL Connessioni > Destinazioni]** e seleziona la scheda **[!UICONTROL Catalogo]**.

   ![Scheda Catalogo di destinazione con il controllo Catalogo evidenziato.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Seleziona **[!UICONTROL Attiva]** nella scheda corrispondente alla destinazione in cui desideri esportare i set di dati.

>[!TIP]
>
>Le destinazioni che possono esportare i tipi di pubblico dei profili sono indicate da un&#39;icona nell&#39;angolo superiore destro della scheda, simile alla destinazione evidenziata di seguito, oppure puoi utilizzare il filtro del tipo di dati per visualizzare solo le destinazioni che possono esportare i tipi di pubblico dei potenziali clienti, come [mostrato più in alto nella pagina](#supported-destinations).

![Pagina di destinazione di Amazon S3 in grado di esportare i tipi di pubblico del profilo evidenziati.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Seleziona **[!UICONTROL Tipo di dati Prospect]**, seguito dalla connessione di destinazione in cui desideri esportare i set di dati, quindi seleziona **[!UICONTROL Avanti]**.

>[!TIP]
> 
>Se desideri impostare una nuova destinazione per attivare i tipi di pubblico prospect, seleziona **[!UICONTROL Configura nuova destinazione]** per attivare il flusso di lavoro [Connetti alla destinazione](/help/destinations/ui/connect-destination.md).

![Flusso di lavoro di attivazione della destinazione con il controllo Prospect evidenziato.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Procedi alla sezione successiva per [selezionare i tipi di pubblico del tuo profilo](#select-profile-audiences) per l&#39;esportazione.

## Selezionare il pubblico potenziale {#select-prospect-audiences}

Utilizza le caselle di controllo a sinistra dei nomi dei tipi di pubblico potenziali per selezionare i tipi di pubblico che desideri esportare nella destinazione, quindi seleziona **[!UICONTROL Successivo]**. In questa vista vengono visualizzati solo i tipi di pubblico potenziali e non altri tipi di pubblico.

![Flusso di lavoro di esportazione del set di dati che mostra il passaggio Seleziona tipi di pubblico in cui è possibile selezionare i potenziali tipi di pubblico da esportare.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Pianificazione e passaggi successivi

Per il resto del flusso di lavoro di attivazione per esportare i tipi di pubblico potenziali, leggi il tutorial sull’attivazione dei dati in destinazioni basate su file. Continua dal passaggio [pianifica esportazione pubblico](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

>[!NOTE]
>
>Tieni presente che nel passaggio di pianificazione, il flusso di lavoro per attivare i tipi di pubblico potenziali ti consente solo di [esportare file completi](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). Le esportazioni di file incrementali non sono supportate.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## Altri casi d’uso ottenuti tramite il supporto dei dati dei partner {#other-use-cases}

Esplora altri casi d’uso abilitati tramite il supporto dei dati dei partner in Real-Time CDP:

* [Puoi integrare i profili di prime parti con attributi di partner di dati affidabili, per migliorare la base di dati, acquisire nuove informazioni sulla base dei clienti e una migliore ottimizzazione del pubblico.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Utilizza il supporto dati di terze parti in Real-Time CDP per [espandere la base di profili con i profili di potenziali clienti dei partner dati e interagisci con loro per acquisire o raggiungere nuovi clienti](/help/rtcdp/partner-data/prospecting.md).
* [Sfrutta il riconoscimento dei partner per personalizzare le esperienze in loco](/help/rtcdp/partner-data/onsite-personalization.md) durante la visita senza che l&#39;utente si autentichi o abbia una storia precedente con il tuo marchio.
