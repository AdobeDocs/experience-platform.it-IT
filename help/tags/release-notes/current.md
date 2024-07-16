---
title: Note sulla versione per Tag ed Inoltro eventi
description: Le ultime note sulla versione relative ai tag e all’inoltro di eventi in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 7%

---

# Note sulla versione per tag e inoltro di eventi

>[!IMPORTANT]
>
>In questa pagina non verranno più forniti i tag e le note sulla versione per l’inoltro degli eventi. Per informazioni dettagliate sui tag e sugli aggiornamenti per l&#39;inoltro degli eventi, consulta le ultime [note sulla versione di Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection).

## 26 aprile 2023

* **Segreto JWT OAuth**: il [Segreto JWT OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) consente ai clienti di utilizzare i token Adobe e Google Service per supportare le interazioni server-to-server nell&#39;inoltro degli eventi.

È stata rilasciata la seguente nuova estensione:

* Estensione **[!DNL Pinterest Conversions API]**: l&#39;estensione di inoltro degli eventi [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=it) consente di sfruttare i dati acquisiti nell&#39;Edge Network di Adobe Experience Platform e di inviarli a [!DNL Pinterest] sotto forma di eventi lato server utilizzando [!DNL Pinterest Conversions API].

## 29 marzo 2023

**Flussi di lavoro rapidi (Beta)**

Accedi ai nuovi flussi di lavoro di avvio rapido nella “Guida introduttiva” dalla schermata iniziale della Raccolta dati. I seguenti flussi di lavoro sono ora disponibili per i clienti come Beta pubblico.
* **[Meta Conversions API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**: i clienti di Inoltro eventi possono raccogliere e inoltrare rapidamente i dati dell&#39;evento dal lato server a Meta per le conversioni degli annunci in pochi semplici passaggi.
* **[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)**: i clienti possono implementare rapidamente Mobile SDK e convalidare gli eventi mobili di base in pochi semplici passaggi.

Sono state rilasciate nuove estensioni:

* Estensione **[!DNL Braze]per l&#39;inoltro degli eventi**: l&#39;estensione [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=it) per l&#39;inoltro degli eventi consente di sfruttare i dati acquisiti nell&#39;Edge Network di Adobe Experience Platform e inviarli a [!DNL Braze] sotto forma di eventi lato server utilizzando le API User Track di [!DNL Braze].
* Estensione di inoltro eventi **[Epsilon Events API]**: l&#39;estensione [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=it) consente di sfruttare l&#39;inoltro eventi per acquisire informazioni sull&#39;evento nell&#39;Edge Network Adobe Experience Platform e inviarle a [!DNL Epsilon] utilizzando l&#39;API eventi [!DNL Epsilon].
* Estensione **[!DNL Mixpanel]per l&#39;inoltro degli eventi**: l&#39;estensione [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=it) consente di sfruttare l&#39;inoltro degli eventi per acquisire informazioni sugli eventi nell&#39;Edge Network di Adobe Experience Platform e inviarle a [!DNL Mixpanel] utilizzando l&#39;API Track Events.

## 25 gennaio 2023

* **Nuova schermata iniziale**: la pagina principale dell&#39;interfaccia utente di Data Collection è stata aggiornata per includere informazioni utili sull&#39;onboarding e collegamenti per ottimizzare la produttività. Ciò include:
   1. Documentazione e flussi di lavoro consigliati per iniziare
   1. Proprietà, regole ed elementi dati recenti
   1. Estensioni popolari
   1. Nuovi aggiornamenti delle estensioni con una funzione di installazione rapida
* **Invia dati a [!DNL Google Ads] tramite l&#39;inoltro eventi**: è ora possibile utilizzare l&#39;estensione [[!DNL Google Ads Enhanced Conversions] API](../extensions/server/google-ads-enhanced-conversions/overview.md) per l&#39;inoltro degli eventi, in combinazione con [segreti Google Oauth 2](../ui/event-forwarding/secrets.md#google-oauth2), per inviare in modo sicuro i dati lato server a [!DNL Google Ads] in tempo reale.

## giovedì 23 novembre 2022

* Estensione **[!DNL AWS]per l&#39;inoltro eventi**: è ora possibile inviare dati a [!DNL Amazon Web Services] ([!DNL AWS]) utilizzando un&#39;estensione [inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni, vedere [[!DNL AWS] panoramica dell&#39;estensione](../../tags/extensions/server/aws/overview.md).
* Estensione **[!DNL Google Ads Enhanced Conversions]per l&#39;inoltro eventi**: è ora possibile inviare dati di conversione a [!DNL Google Ads] utilizzando un&#39;estensione [inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni, vedere [[!DNL Google Ads Enhanced Conversions] panoramica dell&#39;estensione](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md).
* Estensione **[!DNL Microsoft Azure]per l&#39;inoltro eventi**: è ora possibile inviare dati a [!DNL Microsoft Azure] utilizzando un&#39;estensione [inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni, vedere [[!DNL Microsoft Azure] panoramica dell&#39;estensione](../../tags/extensions/server/azure/overview.md).

## 26 ottobre 2022

* **Gestione dei dati sensibili per i flussi di dati**: i flussi di dati ora sfruttano diverse tecnologie Platform per gestire in modo appropriato i dati sensibili in base a normative quali l&#39;Health Insurance Portability and Accountability Act (HIPAA). Per ulteriori informazioni, consulta la sezione sulla gestione di [dati sensibili nei flussi di dati](../../datastreams/overview.md#sensitive).
* Estensione **[!DNL Splunk]per l&#39;inoltro eventi**: è ora possibile inviare dati a [!DNL Splunk] utilizzando un&#39;estensione [inoltro eventi](../ui/event-forwarding/overview.md). Per ulteriori informazioni, vedere [[!DNL Splunk] panoramica dell&#39;estensione](../extensions/server/splunk/overview.md).
* Estensione **[!DNL Zendesk]per l&#39;inoltro eventi**: è ora possibile inviare dati a [!DNL Zendesk] utilizzando un&#39;estensione [inoltro eventi](../ui/event-forwarding/overview.md). Per ulteriori informazioni, vedere [[!DNL Zendesk] panoramica dell&#39;estensione](../extensions/server/zendesk/overview.md).

## 28 settembre 2022

* **Integrazione con navigazione a sinistra di Adobe Experience Platform**: tutte le funzionalità che in precedenza erano esclusive dell&#39;interfaccia utente di Data Collection (inclusi tag e inoltro eventi) sono ora disponibili anche tramite la navigazione a sinistra nell&#39;interfaccia utente di Experience Platform, nella categoria **[!UICONTROL Raccolta dati]**. Questo elimina la necessità di passare da un’interfaccia utente all’altra quando si lavora con le funzionalità di raccolta dati in Platform.
* **Attribuzione utente in tag e inoltro eventi**: quando si elencano le proprietà disponibili in tag e inoltro eventi, ogni proprietà elencata ora viene visualizzata quando è stato aggiornato l&#39;ultima volta e da chi.
* **[[!DNL Snap Conversions API] estensione](https://exchange.adobe.com/apps/ec/108550) per l&#39;inoltro degli eventi**: è ora possibile inviare dati a [!DNL Snapchat Conversions API] utilizzando un&#39;estensione [inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni su come autenticare e utilizzare l&#39;API, consulta la [[!DNL Snapchat Marketing API] documentazione](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 luglio 2022

* L’accesso ai tag e alle funzionalità di inoltro degli eventi viene ora gestito tramite Adobe Admin Console nella scheda di Adobe Experience Platform Data Collection. Per ulteriori informazioni, consulta la guida sulle [autorizzazioni per la raccolta dati](../../collection/permissions.md).
* Il supporto per Internet Explorer 10 e 11 è stato [obsoleto](../ie-deprecation.md).

## 22 giugno 2022

Sono state rilasciate nuove estensioni:

* [Estensione tag di Google Data Layer](../extensions/client/google-data-layer/overview.md): consente di utilizzare un livello dati di Google nell&#39;implementazione dei tag.
* [Estensione inoltro eventi per conversioni avanzate di Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): consente di migliorare le conversioni di Google Ads in tempo reale.
* [Estensione di inoltro eventi Mailchimp](../extensions/server/mailchimp/overview.md): invia eventi all&#39;API di marketing Mailchimp che può attivare le e-mail per campagne di marketing, percorsi o transazioni Mailchimp.