---
title: Note sulla versione per Tag ed Inoltro eventi
description: Le ultime note sulla versione relative ai tag e all’inoltro di eventi in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 12%

---

# Note sulla versione per tag e inoltro di eventi

>[!IMPORTANT]
>
>In questa pagina non verranno più forniti i tag e le note sulla versione per l’inoltro degli eventi. Si prega di fare riferimento al più recente [Note sulla versione di Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection) per tag dettagliati e aggiornamenti sull’inoltro degli eventi.

## 26 aprile 2023

* **Segreto JWT OAuth**: Il [Segreto JWT OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) consente ai clienti di utilizzare i token di servizio Adobe e Google per supportare le interazioni server-to-server nell’inoltro degli eventi.

È stata rilasciata la seguente nuova estensione:

* **[!DNL Pinterest Conversions API]estensione**: Il [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=it) l’estensione per l’inoltro degli eventi consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e di inviarli a [!DNL Pinterest] sotto forma di eventi lato server che utilizzano [!DNL Pinterest Conversions API].

## 29 marzo 2023

**Flussi di lavoro Quick Stark (Beta)**

Accedi ai nuovi flussi di lavoro di avvio rapido nella “Guida introduttiva” dalla schermata iniziale della Raccolta dati. I seguenti flussi di lavoro sono ora disponibili per i clienti come versione beta pubblica.
* **[API di metaconversione](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**: i clienti di Inoltro eventi possono raccogliere e inoltrare rapidamente i dati dell’evento dal lato server a Meta per le conversioni di annunci in pochi e semplici passaggi.
* **[SDK per dispositivi mobili](https://developer.adobe.com/client-sdks/documentation/)**: i clienti possono implementare rapidamente l’SDK di Mobile e convalidare gli eventi mobili di base in pochi semplici passaggi.

Sono state rilasciate nuove estensioni:

* **[!DNL Braze]estensione di inoltro eventi**: Il [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=it) l’estensione per l’inoltro degli eventi consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e di inviarli a [!DNL Braze] sotto forma di eventi lato server che utilizzano [!DNL Braze] API User Track.
* **[API eventi Epsilon] estensione di inoltro eventi**: Il [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=it) consente di sfruttare l’inoltro degli eventi per acquisire informazioni sugli eventi in Adobe Experience Platform Edge Network e inviarle a [!DNL Epsilon] utilizzando [!DNL Epsilon] API evento.
* **[!DNL Mixpanel]estensione di inoltro eventi**: Il [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=it) consente di sfruttare l’inoltro degli eventi per acquisire informazioni sugli eventi in Adobe Experience Platform Edge Network e inviarle a [!DNL Mixpanel] utilizzando l’API Track Events.

## 25 gennaio 2023

* **Nuova schermata iniziale**: la pagina principale dell’interfaccia utente di Data Collection è stata aggiornata per includere informazioni utili sull’onboarding e collegamenti per ottimizzare la produttività. Ciò include:
   1. Documentazione e flussi di lavoro consigliati per iniziare
   1. Proprietà, regole ed elementi dati recenti
   1. Estensioni popolari
   1. Nuovi aggiornamenti delle estensioni con una funzione di installazione rapida
* **Invia dati a [!DNL Google Ads] utilizzo dell’inoltro degli eventi**: ora è possibile utilizzare [[!DNL Google Ads Enhanced Conversions] Estensione API](../extensions/server/google-ads-enhanced-conversions/overview.md) per l’inoltro di eventi, in combinazione con [Segreti Google Oauth 2](../ui/event-forwarding/secrets.md#google-oauth2), per inviare in modo sicuro i dati lato server a [!DNL Google Ads] in tempo reale.

## 23 novembre 2022

* **[!DNL AWS]estensione per l’inoltro di eventi**: ora è possibile inviare dati a [!DNL Amazon Web Services] ([!DNL AWS]) utilizzando un [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la [[!DNL AWS] panoramica dell’estensione](../../tags/extensions/server/aws/overview.md) per ulteriori informazioni.
* **[!DNL Google Ads Enhanced Conversions]estensione per l’inoltro di eventi**: ora puoi inviare dati di conversione a [!DNL Google Ads] utilizzando un [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la [[!DNL Google Ads Enhanced Conversions] panoramica dell’estensione](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) per ulteriori informazioni.
* **[!DNL Microsoft Azure]estensione per l’inoltro di eventi**: ora è possibile inviare dati a [!DNL Microsoft Azure] utilizzando un [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la [[!DNL Microsoft Azure] panoramica dell’estensione](../../tags/extensions/server/azure/overview.md) per ulteriori informazioni.

## 26 ottobre 2022

* **Gestione dei dati sensibili per gli stream di dati**: i flussi di dati sfruttano ora diverse tecnologie Platform per gestire in modo appropriato i dati sensibili in conformità a normative quali l’Health Insurance Portability and Accountability Act (HIPAA). Consulta la sezione su [gestione dei dati sensibili nei flussi di dati](../../datastreams/overview.md#sensitive) per ulteriori informazioni.
* **[!DNL Splunk]estensione per l’inoltro di eventi**: ora è possibile inviare dati a [!DNL Splunk] utilizzando un [inoltro eventi](../ui/event-forwarding/overview.md) estensione. Consulta la [[!DNL Splunk] panoramica dell’estensione](../extensions/server/splunk/overview.md) per ulteriori informazioni.
* **[!DNL Zendesk]estensione per l’inoltro di eventi**: ora è possibile inviare dati a [!DNL Zendesk] utilizzando un [inoltro eventi](../ui/event-forwarding/overview.md) estensione. Consulta la [[!DNL Zendesk] panoramica dell’estensione](../extensions/server/zendesk/overview.md) per ulteriori informazioni.

## 28 settembre 2022

* **Integrazione navigazione sinistra Adobe Experience Platform**: tutte le funzionalità che in precedenza erano esclusive dell’interfaccia utente di Data Collection (inclusi tag e inoltro eventi) ora sono disponibili anche tramite la navigazione a sinistra nell’interfaccia utente di Experienci Platform, nella categoria **[!UICONTROL Raccolta dati]**. Questo elimina la necessità di passare da un’interfaccia utente all’altra quando si lavora con le funzionalità di raccolta dati in Platform.
* **Attribuzione degli utenti nei tag e nell’inoltro degli eventi**: quando elenchi le proprietà disponibili nei tag e nell’inoltro degli eventi, ogni proprietà elencata ora mostra quando è stata aggiornata l’ultima volta e da chi.
* **[[!DNL Snap Conversions API] estensione](https://exchange.adobe.com/apps/ec/108550) per l’inoltro di eventi**: ora è possibile inviare dati a [!DNL Snapchat Conversions API] utilizzando un [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Per ulteriori informazioni su come autenticare e utilizzare l’API, consulta [[!DNL Snapchat Marketing API] documentazione](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 luglio 2022

* L’accesso ai tag e alle funzionalità di inoltro degli eventi viene ora gestito tramite Adobe Admin Console nella scheda di Adobe Experience Platform Data Collection. Consulta la guida su [autorizzazioni raccolta dati](../../collection/permissions.md) per ulteriori informazioni.
* Il supporto per Internet Explorer 10 e 11 è stato [obsoleto](../ie-deprecation.md).

## 22 giugno 2022

Sono state rilasciate nuove estensioni:

* [Estensione tag Google Data Layer](../extensions/client/google-data-layer/overview.md): consente di utilizzare un livello dati di Google nell’implementazione dei tag.
* [Estensione di inoltro eventi per conversioni avanzate di Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): consente di migliorare le conversioni di Google Ads in tempo reale.
* [Estensione di inoltro eventi Mailchimp](../extensions/server/mailchimp/overview.md): invia eventi all’API di marketing Mailchimp che può attivare le e-mail per campagne di marketing, percorsi o transazioni Mailchimp.