---
title: Evoluzione da Audience Manager a Real-Time CDP
description: Comprendi le considerazioni prima di pianificare la migrazione da Audience Manager a Real-Time CDP.
source-git-commit: 147e95cce203933d591fc807d9d20bcbc06e68e3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Evoluzione da Audience Manager a Real-Time CDP

Man mano che la tua organizzazione inizia a utilizzare Adobe Real-Time CDP, esamina queste considerazioni per preparare i dati e comprendere le differenze fondamentali tra le due tecnologie. Questo articolo è destinato a un pubblico di professionisti.

![Diagramma dell’evoluzione da Audience Manager a Real-Time CDP](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Considerare l’architettura dei dati all’interno di Audience Manager

Considerando l&#39;evoluzione da Audience Manager a Real-Time CDP, è giunto il momento di analizzare [Segmenti di Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=en) e determinare quali [Segnali](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=en), [caratteristiche](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=en), e [regole](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=en#segment-builder-section) sono che compongono quei segmenti.

Inoltre, pensa alle origini dati attualmente utilizzate in Audience Manager.

L’Adobe consiglia di categorizzare i segmenti come segue:

* Segmenti che possono essere inviati ad Experience Platform tramite [[!UICONTROL Connettore sorgente Audience Manager]](/help/sources/connectors/adobe-applications/audience-manager.md), poiché non hanno dipendenze di dati, non hanno problemi di destinazione o attivazione e le loro regole di segmentazione possono essere create tramite Real-time CDP [Generatore di segmenti](/help/segmentation/ui/segment-builder.md) più tardi.
* Segmenti con regole che possono essere supportate ma che possono contenere dati che non saranno disponibili in Real-Time CDP.
* Segmenti che non possono essere creati in Real-time CDP e per i quali mancano delle funzionalità.

>[!TIP]
>
>Offerte Adobe Real-Time CDP [tre tipi di valutazione dei segmenti](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Batch], [!UICONTROL Streaming], e [!UICONTROL Bordo]. I clienti che utilizzano segmenti in tempo reale in Audience Manager possono essere soggetti a restrizioni per l’attuale limite di 500 segmenti di streaming in Real-Time CDP. Ulteriori informazioni su [guardrail di segmentazione](/help/profile/guardrails.md).

## 2. Quali segmenti sono critici da inviare tramite [!UICONTROL Connettore sorgente Audience Manager]?

In base ai loro criteri di valutazione, i segmenti che non hanno dipendenze di dati, nessuna sfida di destinazione o attivazione e le loro regole di segmentazione possono essere creati tramite la raccolta dati di Real-Time CDP come [Adobe Experience Platform Web SDK](/help/edge/web-sdk-faq.md) in una data successiva devono essere inviati tramite il connettore di origine di Audience Manager.

## 3. Utilizzerai il [!UICONTROL Tipi di pubblico di Experience Cloud] destinazione per riportare i dati ad Audience Manager?

I segmenti con regole che possono essere supportate in Real-Time CDP ma con dipendenze di attivazione da Audience Manager possono essere inviati ad Audience Manager tramite [Tipi di pubblico di Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md) scheda di destinazione.

## 4. Quali destinazioni hai attualmente in Audience Manager per iniziare a trasferire in Real-Time CDP?

L’Adobe consiglia vivamente che i segmenti attivati nell’Audience Manager a [destinazioni basate su persone](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=en) ricevere notifiche push in Real-Time CDP tramite [!UICONTROL Connettore sorgente Audience Manager], per poi eseguire l&#39;attivazione tramite Real-Time CDP.

Tutte le destinazioni basate su persone sono disponibili in Audience Manager: [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Customer Match di Google]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md) - sono disponibili anche in Real-Time CDP.

Altri partner di prime parti per la strategia di dati e media, come [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md), e [[!UICONTROL Il Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) sono disponibili.

Real-Time CDP attualmente supporta più di 60 destinazioni in modalità nativa nel [catalogo](/help/destinations/catalog/overview.md), oltre 20 di cui sono destinazioni pubblicitarie o social che supportano la corrispondenza del pubblico di prime parti.

## Passaggi successivi

Dopo aver letto questa pagina, ora disponi di una prima serie di considerazioni da elaborare quando inizi la tua evoluzione da Audience Manager a Real-Time CDP.
