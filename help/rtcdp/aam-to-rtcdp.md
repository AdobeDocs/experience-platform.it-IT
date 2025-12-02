---
title: Evoluzione da Audience Manager a Real-Time CDP
description: Comprendi le considerazioni prima di pianificare la migrazione da Audience Manager ad Adobe Real-Time CDP.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 67%

---

# Evoluzione da Audience Manager a Real-Time CDP

Man mano che la tua organizzazione inizia a utilizzare Adobe Real-Time CDP, esplora queste considerazioni per preparare i tuoi dati e comprendere le differenze principali tra queste due tecnologie. Questo articolo si rivolge a un pubblico di professionisti.

![Diagramma dell’evoluzione da Audience Manager a Real-Time CDP](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## &#x200B;1. Considerare l’architettura dei dati all’interno di Audience Manager

Nel considerare l’evoluzione da Audience Manager a Real-Time CDP, è giunto il momento di analizzare i tuoi [Segmenti di Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=it) e determinare quali [segnali](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=it), [caratteristiche](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=it) e [regole](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=it#segment-builder-section) compongono tali segmenti.

Inoltre, prendi in considerazione le origini dati attualmente utilizzate in Audience Manager.

Adobe consiglia di categorizzare i segmenti nel modo seguente:

* I segmenti che possono essere inviati ad Experience Platform tramite [[!UICONTROL Audience Manager Source Connector]](/help/sources/connectors/adobe-applications/audience-manager.md), in quanto non hanno dipendenze di dati, non hanno problemi di destinazione o attivazione e le loro regole di segmentazione possono essere create tramite il generatore di segmenti [di Real-Time CDP](/help/segmentation/ui/segment-builder.md) in un secondo momento.
* Segmenti con regole che possono essere supportate ma che possono contenere dati che non saranno disponibili in Real-Time CDP.
* Segmenti che non possono essere creati in Real-Time CDP e per i quali mancano funzionalità.

>[!TIP]
>
>Adobe Real-Time CDP offre [tre tipi di valutazione del segmento](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Batch], [!UICONTROL Streaming] e [!UICONTROL Edge]. La clientela che utilizza segmenti in tempo reale in Audience Manager può essere soggetta a restrizioni per l’attuale limite di 500 segmenti di streaming in Real-Time CDP. Ulteriori informazioni sui [guardrail di segmentazione](/help/profile/guardrails.md).

## &#x200B;2. Quali segmenti sono critici da inviare tramite [!UICONTROL Audience Manager Source Connector]?

In base ai criteri di valutazione, i segmenti che non hanno dipendenze di dati, nessun problema di destinazione o attivazione e le cui regole di segmentazione possono essere create tramite la raccolta dati di Real-Time CDP come [Adobe Experience Platform Web SDK](/help/collection/js/faq.md) devono essere inviati tramite il connettore di origine di Audience Manager in un secondo momento.

## &#x200B;3. Utilizzerai la destinazione [!UICONTROL Experience Cloud Audiences] per restituire i dati ad Audience Manager?

I segmenti con regole che possono essere supportate in Real-Time CDP ma con dipendenze di attivazione da Audience Manager possono essere inviati a Audience Manager tramite la scheda di destinazione [Tipi di pubblico di Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md).

## &#x200B;4. Di quali destinazioni disponi attualmente in Audience Manager che puoi iniziare a trasferire in Real-Time CDP?

Adobe consiglia vivamente che i segmenti attivati in Audience Manager in [destinazioni basate su persone](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=it) vengano inviati a Real-Time CDP tramite [!UICONTROL Audience Manager Source Connector], per poi essere attivati tramite Real-Time CDP.

Tutte le destinazioni basate su persone disponibili in Audience Manager - [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md) - sono disponibili anche in Real-Time CDP.

Sono disponibili partner aggiuntivi per dati e strategie multimediali di prime parti come [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) e [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md).

Real-Time CDP attualmente supporta più di 60 destinazioni in modalità nativa nel [catalogo](/help/destinations/catalog/overview.md), oltre 20 delle quali sono destinazioni pubblicitarie o social che supportano la corrispondenza del pubblico di prime parti.

## Passaggi successivi

Dopo aver letto questa pagina, ora disponi di una prima serie di considerazioni su cui riflettere mentre inizi la tua evoluzione da Audience Manager a Real-Time CDP.
