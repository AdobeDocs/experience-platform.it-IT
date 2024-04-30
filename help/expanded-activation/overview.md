---
title: Audience Manager di attivazione espansa
description: Scopri come attivare i tipi di pubblico di Audienci Manager nelle destinazioni social e pubblicitarie tramite Audienci Manager Expanded Activation.
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# Audience Manager di attivazione espansa

Basata su Adobe Experience Platform, l&#39;attivazione espansa di Audienci Manager aiuta gli [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) gli utenti attivino i propri tipi di pubblico su [social](../destinations/catalog/social/overview.md) e [pubblicità](../destinations/catalog/advertising/overview.md) piattaforme di destinazione da Real-Time CDP, ad esempio [Facebook](../destinations/catalog/social/facebook.md), [Google Ads](../destinations/catalog/advertising/google-ads-destination.md), e altro ancora.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] è disponibile solo per gli [!DNL Audience Manager] utenti.

## Terminologia {#terminology}

Audienci Manager Expanded Activation utilizza concetti e componenti di Adobe Experience Platform. Per comprendere meglio il flusso di lavoro di attivazione espansa e i componenti che utilizzerai, assicurati di avere una conoscenza di base dei seguenti concetti:

* [Tipi di pubblico](../segmentation/ui/overview.md): i tipi di pubblico sono insiemi di persone che condividono comportamenti e/o caratteristiche simili. Questa raccolta di persone può essere generata da Adobe Experience Platform utilizzando le definizioni dei segmenti o la composizione del pubblico (pubblico generato da Platform) oppure da fonti esterne, come caricamenti personalizzati (pubblico generato esternamente). In Attivazione espansa, i segmenti di Audience Manager (tipi di pubblico) vengono importati come [caricamenti personalizzati](../segmentation/ui/overview.md#import-audience).
* [Connettori sorgente](../sources/home.md): i connettori di sorgenti (noti anche come sorgenti) consentono agli utenti Experienci Platform di acquisire facilmente dati da più sorgenti, consentendo la strutturazione, l’etichettatura e il miglioramento dei dati utilizzando i servizi di Experience Platform. I dati possono essere acquisiti da diverse origini, ad esempio archiviazione basata su cloud, software di terze parti e sistemi di gestione delle relazioni con i clienti.
* [Connettori di destinazione](../destinations/home.md): le destinazioni descrivono qualsiasi endpoint, ad esempio un’applicazione di Adobe, una piattaforma pubblicitaria, un servizio di archiviazione cloud o un servizio di marketing, in cui viene attivato e distribuito un pubblico. [!DNL Expanded Activation] supporta l’attivazione di tipi di pubblico per [pubblicità](../destinations/catalog/advertising/overview.md) e [social](../destinations/catalog/social/overview.md) connettori di destinazione.

## Prerequisiti {#prerequisites}

Prima di poter attivare i tipi di pubblico tramite Attivazione espansa, assicurati di soddisfare i prerequisiti descritti di seguito.

### Requisiti utente e ruolo {#permission-requirements}

Prima di usare [!DNL Expanded Activation], è necessario creare un account utente dall’Admin Console e assegnarlo al [!DNL Expanded Activation] ruolo. Consulta la [amministrazione](administration.md) per istruzioni dettagliate su come eseguire questa operazione.

### Requisiti del pubblico {#audience-requirements}

Per attivare i tipi di pubblico tramite [!DNL Expanded Activation], assicurati che i tipi di pubblico di Audienci Manager siano basati su **indirizzi e-mail con hash**. Esistono due modi per garantire questo, in base all’utilizzo del tuo Audience Manager:

* Se utilizzi il [Audience Manager di destinazioni basate su persone](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) , in questo caso si stanno già acquisendo gli indirizzi e-mail con hash in Audienci Manager. In questo caso non è necessario effettuare ulteriori operazioni. Puoi passare a [attivazione di tipi di pubblico tramite attivazione espansa](activate-audiences.md).
* Se sei _non_ utilizzando [Audience Manager di destinazioni basate su persone](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) funzionalità, devi creare una nuova origine dati in Audienci Manager e utilizzarla per memorizzare indirizzi e-mail con hash. Consulta la documentazione su [configurazione di un’origine dati per flussi di lavoro e-mail con hash](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) per scoprire come eseguire questa operazione. Dopo aver acquisito gli indirizzi e-mail con hash nell’origine dati dell’Audience Manager, consulta la documentazione su [attivazione di tipi di pubblico tramite attivazione espansa](activate-audiences.md).

## Passaggi successivi {#next-steps}

Ora che hai una migliore comprensione dei casi d’uso e dei vantaggi dell’utilizzo di [!DNL Expanded Activation], inizio [configurazione dell’account](administration.md) e poi [attivare i tipi di pubblico](activate-audiences.md).

