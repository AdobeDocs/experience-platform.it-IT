---
title: Evoluzione da Audience Manager a Real-Time CDP
description: Comprendere le considerazioni prima di pianificare la migrazione da Audience Manager a Real-Time CDP.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 88%

---

# Evoluzione da Audience Manager a Real-Time CDP

Man mano che la tua organizzazione inizia a utilizzare Adobe Real-Time CDP, esplora queste considerazioni per preparare i tuoi dati e comprendere le differenze principali tra queste due tecnologie. Questo articolo è destinato ai professionisti.

![Diagramma dell’evoluzione da Audience Manager a Real-Time CDP](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Considerare l’architettura dei dati all’interno di Audience Manager

Nel considerare l’evoluzione da Audience Manager a Real-Time CDP, è giunto il momento di analizzare i tuoi [Segmenti di Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html) e determinare quali [segnali](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html), [caratteristiche](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html) e [regole](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html#segment-builder-section) compongono tali segmenti.

Inoltre, prendi in considerazione le origini dati attualmente utilizzate in Audience Manager.

Adobe consiglia di categorizzare i segmenti nel modo seguente:

* Segmenti che possono essere inviati ad Experienci Platform tramite [[!UICONTROL Connettore sorgente Audience Manager]](/help/sources/connectors/adobe-applications/audience-manager.md), poiché non hanno dipendenze di dati, non hanno problemi di destinazione o attivazione e le loro regole di segmentazione possono essere create tramite Real-Time CDP [Generatore di segmenti](/help/segmentation/ui/segment-builder.md) più tardi.
* Segmenti con regole che possono essere supportate ma che possono contenere dati che non saranno disponibili in Real-Time CDP.
* Segmenti che non possono essere creati in Real-Time CDP e per i quali mancano funzionalità.

>[!TIP]
>
>Adobe Real-Time CDP offre [tre tipi di valutazione dei segmenti](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Batch], [!UICONTROL Streaming] ed [!UICONTROL Edge]. La clientela che utilizza segmenti in tempo reale in Audience Manager può essere soggetta a restrizioni per l’attuale limite di 500 segmenti di streaming in Real-Time CDP. Ulteriori informazioni sui [guardrail di segmentazione](/help/profile/guardrails.md).

## 2. Quali segmenti è importante inviare tramite il [!UICONTROL Connettore di origine Audience Manager]?

In base ai criteri di valutazione, i segmenti che non hanno dipendenze di dati, nessun problema di destinazione o attivazione e le cui regole di segmentazione possono essere create tramite la raccolta dati di Real-Time CDP come [Adobe Experience Platform Web SDK](/help/web-sdk/faq.md) devono essere inviati tramite il connettore di origine di Audience Manager in un secondo momento.

## 3. Utilizzerai la destinazione [!UICONTROL Tipi di pubblico di Experience Cloud] per riportare i dati ad Audience Manager?

I segmenti con regole che possono essere supportate in Real-Time CDP ma con dipendenze di attivazione da Audience Manager possono essere inviati a Audience Manager tramite la scheda di destinazione [Tipi di pubblico di Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md).

## 4. Di quali destinazioni disponi attualmente in Audience Manager che puoi iniziare a trasferire in Real-Time CDP?

Adobe consiglia vivamente che i segmenti attivati in Audience Manager per le [destinazioni basate su persone](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=it) vengano inviati a Real-Time CDP tramite il [!UICONTROL Connettore di origine di Audience Manager], per poi eseguire l’attivazione tramite Real-Time CDP.

Tutte le destinazioni basate su persone disponibili in Audience Manager, come [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Customer Match di Google]](/help/destinations/catalog/advertising/google-customer-match.md) e [LinkedIn](/help/destinations/catalog/social/linkedin.md), sono disponibili anche in Real-Time CDP.

Altri dati di prime parti e partner per la strategia di contenuti multimediali, come [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) e [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) sono disponibili.

Real-Time CDP attualmente supporta più di 60 destinazioni in modalità nativa nel [catalogo](/help/destinations/catalog/overview.md), oltre 20 delle quali sono destinazioni pubblicitarie o social che supportano la corrispondenza del pubblico di prime parti.

## Passaggi successivi

Dopo aver letto questa pagina, ora disponi di una prima serie di considerazioni su cui riflettere mentre inizi la tua evoluzione da Audience Manager a Real-Time CDP.
