---
title: Attivazione estesa di Audience Manager
description: Scopri come attivare i tipi di pubblico di Audience Manager per destinazioni social e pubblicitarie tramite Audience Manager Expanded Activation.
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 2%

---

# Attivazione estesa di Audience Manager

Basato su Adobe Experience Platform, Audience Manager Expanded Activation consente agli utenti esistenti di [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) di attivare i propri tipi di pubblico sulle piattaforme di destinazione [social](../destinations/catalog/social/overview.md) e [advertising](../destinations/catalog/advertising/overview.md) da Real-Time CDP, ad esempio [Facebook](../destinations/catalog/social/facebook.md), [Google Ads](../destinations/catalog/advertising/google-ads-destination.md) e altro ancora.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] è disponibile solo per [!DNL Audience Manager] utenti esistenti.

## Terminologia {#terminology}

Audience Manager Expanded Activation utilizza concetti e componenti di Adobe Experience Platform. Per comprendere meglio il flusso di lavoro di attivazione espansa e i componenti che utilizzerai, assicurati di avere una conoscenza di base dei seguenti concetti:

* [Tipi di pubblico](../segmentation/ui/overview.md): i tipi di pubblico sono insiemi di persone che condividono comportamenti e/o caratteristiche simili. Questa raccolta di persone può essere generata da Adobe Experience Platform utilizzando le definizioni dei segmenti o la composizione del pubblico (pubblico generato da Experience Platform) oppure da fonti esterne, come caricamenti personalizzati (pubblico generato esternamente). In Attivazione espansa, i segmenti di Audience Manager (tipi di pubblico) vengono importati come [caricamenti personalizzati](../segmentation/ui/audience-portal.md#import-audience).
* [Connettori Source](../sources/home.md): i connettori Source (noti anche come origini) consentono agli utenti di Experience Platform di acquisire facilmente dati da più origini, consentendo la strutturazione, l&#39;etichettatura e il miglioramento dei dati tramite i servizi Experience Platform. I dati possono essere acquisiti da diverse origini, ad esempio archiviazione basata su cloud, software di terze parti e sistemi di gestione delle relazioni con i clienti.
* [Connettori di destinazione](../destinations/home.md): le destinazioni descrivono qualsiasi endpoint, ad esempio un&#39;applicazione Adobe, una piattaforma pubblicitaria, un servizio di archiviazione cloud o un servizio di marketing, in cui viene attivato e recapitato un pubblico. [!DNL Expanded Activation] supporta l&#39;attivazione dei tipi di pubblico per [advertising](../destinations/catalog/advertising/overview.md) e [social](../destinations/catalog/social/overview.md) connettori di destinazione.

## Prerequisiti {#prerequisites}

Prima di poter attivare i tipi di pubblico tramite Attivazione espansa, assicurati di soddisfare i prerequisiti descritti di seguito.

### Requisiti utente e ruolo {#permission-requirements}

Prima di poter utilizzare [!DNL Expanded Activation], è necessario creare un account utente da Admin Console e assegnarlo al ruolo [!DNL Expanded Activation]. Per istruzioni dettagliate su come eseguire questa operazione, vedere la pagina [amministrazione](administration.md).

### Requisiti del pubblico {#audience-requirements}

Per attivare i tipi di pubblico tramite [!DNL Expanded Activation], assicurati che i tipi di pubblico di Audience Manager siano basati su **indirizzi e-mail con hash**. Esistono due modi per garantire questo, in base all’utilizzo di Audience Manager:

* Se utilizzi la funzionalità [Destinazioni basate su persone di Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview), stai già acquisendo indirizzi e-mail con hash in Audience Manager. In questo caso non è necessario effettuare ulteriori operazioni. Puoi passare a [attivazione di tipi di pubblico tramite Attivazione espansa](activate-audiences.md).
* Se _non_ utilizza la funzionalità [Destinazioni basate su persone di Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview), devi creare una nuova origine dati in Audience Manager e utilizzarla per memorizzare gli indirizzi e-mail con hash. Per informazioni su come eseguire questa operazione, consulta la documentazione su [configurazione di un&#39;origine dati per flussi di lavoro e-mail con hash](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails). Dopo aver acquisito gli indirizzi e-mail con hash nell&#39;origine dati di Audience Manager, leggi la documentazione sull&#39;[attivazione di tipi di pubblico tramite attivazione espansa](activate-audiences.md).

## Passaggi successivi {#next-steps}

Ora che hai una migliore comprensione dei casi d&#39;uso e dei vantaggi dell&#39;utilizzo di [!DNL Expanded Activation], inizia a [configurare l&#39;account](administration.md) e quindi [attivare il pubblico](activate-audiences.md).
