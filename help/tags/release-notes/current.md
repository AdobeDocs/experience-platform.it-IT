---
title: Note sulla versione per tag e inoltro eventi
description: Le più recenti note sulla versione relative ai tag e all’inoltro di eventi in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: ht
source-wordcount: '771'
ht-degree: 100%

---

# Note sulla versione per tag e inoltro eventi

>[!IMPORTANT]
>
>In questa pagina non verranno più fornite le note sulla versione per i tag e per l’inoltro di eventi. Per informazioni dettagliate sugli aggiornamenti per i tag e l’inoltro degli eventi, consulta le ultime [note sulla versione di Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=it#data-collection).

## 26 aprile 2023

* **Segreto JWT OAuth**: il [segreto JWT OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=it) consente alla clientela di utilizzare i token di servizio Adobe e Google per supportare le interazioni da server a server nell’inoltro eventi.

È stata rilasciata la nuova estensione seguente:

* Estensione **[!DNL Pinterest Conversions API]**: l’estensione [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=it) per l’inoltro degli eventi consente di sfruttare i dati acquisiti nella rete Edge di Adobe Experience Platform e di inviarli a [!DNL Pinterest] sotto forma di eventi lato server utilizzando [!DNL Pinterest Conversions API].

## 29 marzo 2023

**Flussi di lavoro con avvio rapido (Beta)**

Accedi ai nuovi flussi di lavoro di avvio rapido nell’area introduttiva dalla schermata iniziale della Raccolta dati. I seguenti flussi di lavoro sono ora disponibili per la clientela come Beta pubblico.
* **[API di conversione metadati](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=it#quick-start)**: l’inoltro eventi consente alla clientela di raccogliere e inoltrare rapidamente i dati di evento lato server a Meta per le conversioni di annunci in alcuni semplici passaggi.
* **[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)**: è possibile implementare rapidamente Mobile SDK e convalidare gli eventi mobili di base in pochi semplici passaggi.

Sono state rilasciate nuove estensioni:

* Estensione **[!DNL Braze]per l’inoltro eventi**: l’estensione [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=it) per l’inoltro degli eventi consente di sfruttare i dati acquisiti nella rete Edge Network di Adobe Experience Platform e di inviarli a [!DNL Braze] sotto forma di eventi lato server utilizzando le API User Track di [!DNL Braze].
* Estensione **[Epsilon Events API] per l’inoltro degli eventi**: l’estensione [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=it) consente di sfruttare l’inoltro degli eventi per acquisire informazioni sugli eventi nella rete Edge di Adobe Experience Platform e inviarle a [!DNL Epsilon] utilizzando [!DNL Epsilon] Event API.
* Estensione **[!DNL Mixpanel]per l’inoltro eventi**: l’estensione [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=it) consente di sfruttare l’inoltro degli eventi per acquisire informazioni sugli eventi nella rete Edge Network di Adobe Experience Platform e inviarle a [!DNL Mixpanel] utilizzando l’API degli eventi di tracciamento.

## 25 gennaio 2023

* **Nuova schermata Home**: la pagina Home dell’interfaccia utente della Raccolta dati è stata aggiornata per includere informazioni utili sull’onboarding e collegamenti per ottimizzare la produttività. Ciò include:
   1. Documentazione e flussi di lavoro consigliati per iniziare
   1. Proprietà, regole ed elementi dati recenti
   1. Estensioni popolari
   1. Nuovi aggiornamenti delle estensioni con una funzione di installazione rapida
* **Invia dati a [!DNL Google Ads] utilizzando l’inoltro eventi**: ora puoi utilizzare l’estensione [[!DNL Google Ads Enhanced Conversions] API](../extensions/server/google-ads-enhanced-conversions/overview.md) per l’inoltro degli eventi, in combinazione con i [segreti OAuth 2 di Google](../ui/event-forwarding/secrets.md#google-oauth2), per inviare in modo sicuro i dati lato server a [!DNL Google Ads] in tempo reale.

## 23 novembre 2022

* Estensione **[!DNL AWS]per l’inoltro eventi**: è ora possibile inviare dati a [!DNL Amazon Web Services] ([!DNL AWS]) utilizzando un’estensione di [inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni, consulta [[!DNL AWS] - Panoramica dell’estensione](../../tags/extensions/server/aws/overview.md).
* Estensione **[!DNL Google Ads Enhanced Conversions]per l’inoltro eventi**: è ora possibile inviare dati di conversione a [!DNL Google Ads] utilizzando un’estensione per l’[inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni, consulta [[!DNL Google Ads Enhanced Conversions] - Panoramica dell’estensione](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md).
* Estensione **[!DNL Microsoft Azure]per l’inoltro eventi**: è ora possibile inviare dati a [!DNL Microsoft Azure] utilizzando un’estensione per l’[inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni, consulta [[!DNL Microsoft Azure] - Panoramica dell’estensione](../../tags/extensions/server/azure/overview.md).

## 26 ottobre 2022

* **Gestione dei dati sensibili per gli stream di dati**: gli stream di dati ora sfruttano diverse tecnologie Platform per gestire in modo appropriato i dati sensibili in base a normative quali l’Health Insurance Portability and Accountability Act (HIPAA). Per ulteriori informazioni, consulta la sezione sulla [gesstione dei dati sensibili negli stream di dati](../../datastreams/overview.md#sensitive).
* Estensione **[!DNL Splunk]per l’inoltro eventi**: è ora possibile inviare dati a [!DNL Splunk] utilizzando un’estensione per l’[inoltro eventi](../ui/event-forwarding/overview.md). Per ulteriori informazioni, consulta [[!DNL Splunk] - Panoramica dell’estensione](../extensions/server/splunk/overview.md).
* Estensione **[!DNL Zendesk]per l’inoltro eventi**: è ora possibile inviare dati a [!DNL Zendesk] utilizzando un’estensione [inoltro eventi](../ui/event-forwarding/overview.md). Per ulteriori informazioni, consulta la [[!DNL Zendesk] panoramica delle estensioni](../extensions/server/zendesk/overview.md).

## 28 settembre 2022

* **Integrazione con barra di navigazione a sinistra di Adobe Experience Platform**: tutte le funzionalità che in precedenza erano esclusive dell’interfaccia utente della raccolta dati (inclusi tag e inoltro eventi) sono ora disponibili anche tramite la barra di navigazione a sinistra nell’interfaccia utente di Experience Platform, nella categoria **[!UICONTROL Raccolta dati]**. Questo elimina la necessità di passare da un’interfaccia utente all’altra quando si utilizzano le funzionalità di raccolta dati in Platform.
* **Attribuzione utente in tag e inoltro eventi**: quando si elencano le proprietà disponibili in tag e inoltro eventi, per ogni proprietà elencata viene visualizzato l’ultimo aggiornamento e chi l’ha effettuato.
* **[[!DNL Snap Conversions API] estensione](https://exchange.adobe.com/apps/ec/108550) per l’inoltro eventi**: è ora possibile inviare dati a [!DNL Snapchat Conversions API] utilizzando un’estensione [inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni su come autenticarsi e utilizzare l’API, consulta la [[!DNL Snapchat Marketing API] documentazione](https://marketingapi.snapchat.com/docs/conversion.html?lang=it).

## 27 luglio 2022

* L’accesso alle funzionalità per tag e inoltro eventi viene ora gestito tramite Adobe Admin Console nella scheda Raccolta dati di Adobe Experience Platform. Per ulteriori informazioni, consulta la guida sulle [autorizzazioni della raccolta dati](../../collection/permissions.md).
* Il supporto per Internet Explorer 10 e 11 è [obsoleto](../ie-deprecation.md).

## 22 giugno 2022

Sono state rilasciate nuove estensioni:

* [Estensione del tag di livello dati di Google](../extensions/client/google-data-layer/overview.md): consente di utilizzare un livello dati di Google nell’implementazione dei tag.
* [Estensione inoltro eventi per conversioni avanzate di Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html?lang=it): consente di migliorare le conversioni di Google Ads in tempo reale.
* [Estensione di inoltro eventi Mailchimp](../extensions/server/mailchimp/overview.md): invia eventi all’API di marketing Mailchimp che può attivare le e-mail per campagne di marketing, percorsi o transazioni Mailchimp.