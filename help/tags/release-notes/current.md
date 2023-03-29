---
title: Note sulla versione per tag e inoltro eventi
description: Le ultime note sulla versione relative ai tag e all’inoltro di eventi in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: f2f2f9abc50f2016e41fd23bfbb66553fadf6fce
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 4%

---

# Note sulla versione per tag e inoltro eventi

## 29 marzo 2023

**Flussi di lavoro rapidi (beta)**

Accedi ai nuovi flussi di lavoro di avvio rapido in &quot;Guida introduttiva&quot; dalla schermata iniziale Raccolta dati. I seguenti flussi di lavoro sono ora disponibili per i clienti come versione beta pubblica.
* **[API per le metaconversioni](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start)**: I clienti di Event Forwarding possono raccogliere e inoltrare rapidamente i dati degli eventi, lato server a Meta per le conversioni di annunci in pochi semplici passaggi.
* **[SDK per dispositivi mobili](https://developer.adobe.com/client-sdks/documentation/)**: I clienti possono implementare rapidamente l’SDK di Mobile e convalidare gli eventi mobile di base in pochi semplici passaggi.

Sono state rilasciate nuove estensioni:

* **[!DNL Braze]estensione di inoltro eventi**: La [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) l’estensione di inoltro eventi consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e inviarli a [!DNL Braze] sotto forma di eventi lato server che utilizzano [!DNL Braze] API di tracciamento utente.
* **[!DNL Mixpanel]estensione di inoltro eventi**: La [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) l’estensione ti consente di sfruttare l’inoltro eventi per acquisire informazioni sull’evento in Adobe Experience Platform Edge Network e di inviarle a Mixpanel utilizzando l’API Track Events.

## 25 gennaio 2023

* **Nuova schermata principale**: La home page dell’interfaccia utente di raccolta dati è stata aggiornata con informazioni utili sull’onboarding e collegamenti per semplificare la produttività. Ciò include:
   1. Documentazione e flussi di lavoro consigliati per iniziare
   1. Proprietà, regole ed elementi dati recenti
   1. Estensioni popolari
   1. Nuovi aggiornamenti di estensione con una funzione di installazione rapida
* **Invia dati a [!DNL Google Ads] utilizzo dell&#39;inoltro eventi**: Ora puoi utilizzare la [[!DNL Google Ads Enhanced Conversions] Estensione API](../extensions/server/google-ads-enhanced-conversions/overview.md) per l&#39;inoltro di eventi, combinato con [Google Oauth 2 segreti](../ui/event-forwarding/secrets.md#google-oauth2), per inviare in modo sicuro i dati lato server a [!DNL Google Ads] in tempo reale.

## 23 novembre 2022

* **[!DNL AWS]estensione per l&#39;inoltro eventi**: Ora puoi inviare dati a [!DNL Amazon Web Services] ([!DNL AWS]) utilizzando un [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la sezione [[!DNL AWS] panoramica dell&#39;estensione](../../tags/extensions/server/aws/overview.md) per ulteriori informazioni.
* **[!DNL Google Ads Enhanced Conversions]estensione per l&#39;inoltro eventi**: Ora puoi inviare i dati di conversione a [!DNL Google Ads] utilizzando [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la sezione [[!DNL Google Ads Enhanced Conversions] panoramica dell&#39;estensione](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) per ulteriori informazioni.
* **[!DNL Microsoft Azure]estensione per l&#39;inoltro eventi**: Ora puoi inviare dati a [!DNL Microsoft Azure] utilizzando [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la sezione [[!DNL Microsoft Azure] panoramica dell&#39;estensione](../../tags/extensions/server/azure/overview.md) per ulteriori informazioni.

## 26 ottobre 2022

* **Gestione sensibile dei dati per i datastreams**: I Datastreams ora sfruttano diverse tecnologie Platform per gestire in modo appropriato i dati sensibili come imposto da regolamenti come l&#39;Health Insurance Portability and Accountability Act (HIPAA). Vedi la sezione su [gestione dei dati sensibili nei flussi di dati](../../edge/datastreams/overview.md#sensitive) per ulteriori informazioni.
* **[!DNL Splunk]estensione per l&#39;inoltro eventi**: Ora puoi inviare dati a [!DNL Splunk] utilizzando [inoltro eventi](../ui/event-forwarding/overview.md) estensione. Consulta la sezione [[!DNL Splunk] panoramica dell&#39;estensione](../extensions/server/splunk/overview.md) per ulteriori informazioni.
* **[!DNL Zendesk]estensione per l&#39;inoltro eventi**: Ora puoi inviare dati a [!DNL Zendesk] utilizzando [inoltro eventi](../ui/event-forwarding/overview.md) estensione. Consulta la sezione [[!DNL Zendesk] panoramica dell&#39;estensione](../extensions/server/zendesk/overview.md) per ulteriori informazioni.

## 28 settembre 2022

* **Integrazione con il menu di navigazione a sinistra di Adobe Experience Platform**: Tutte le funzionalità precedentemente esclusive dell’interfaccia utente di raccolta dati (inclusi tag e inoltro eventi) sono ora disponibili anche nella navigazione a sinistra nell’interfaccia utente di Experience Platform, nella categoria **[!UICONTROL Raccolta dati]**. Questo elimina la necessità di passare da un’interfaccia utente all’altra quando si lavora con le funzionalità di raccolta dati in Platform.
* **Attribuzione utente in tag e inoltro evento**: Nell’elenco delle proprietà disponibili nei tag e nell’inoltro di eventi, ogni proprietà elencata viene visualizzata quando è stata aggiornata per l’ultima volta e da chi.
* **[[!DNL Snap Conversions API] estensione](https://exchange.adobe.com/apps/ec/108550) per l&#39;inoltro di eventi**: Ora puoi inviare dati a [!DNL Snapchat Conversions API] utilizzando [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Per ulteriori informazioni su come autenticare e utilizzare l’API, consulta [[!DNL Snapchat Marketing API] documentazione](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 luglio 2022

* L’accesso ai tag e alle funzionalità di inoltro eventi ora è gestito tramite Adobe Admin Console nella scheda per la raccolta dati di Adobe Experience Platform. Consulta la guida su [autorizzazioni per la raccolta dati](../../collection/permissions.md) per ulteriori informazioni.
* Il supporto per Internet Explorer 10 e 11 è stato [obsoleto](../ie-deprecation.md).

## 22 giugno 2022

Sono state rilasciate nuove estensioni:

* [Estensione tag Google Data Layer](../extensions/client/google-data-layer/overview.md): Consente di utilizzare un livello dati Google nell’implementazione dei tag.
* [Estensione di inoltro evento Conversioni migliorate di Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Consente di migliorare le conversioni di Google Ads in tempo reale.
* [Estensione inoltro evento Mailchimp](../extensions/server/mailchimp/overview.md): Invia eventi all’API marketing Mailchimp che può attivare le e-mail per campagne di marketing, percorsi o transazioni Mailchimp.