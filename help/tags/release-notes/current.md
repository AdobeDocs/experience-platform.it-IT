---
title: Note sulla versione per tag e inoltro eventi
description: Le ultime note di rilascio relative ai tag e all’inoltro di eventi in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 6%

---

# Note sulla versione per tag e inoltro eventi

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
