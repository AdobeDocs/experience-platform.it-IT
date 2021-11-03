---
audience: user
user-guide-title: Guida alle destinazioni
user-guide-description: Attiva i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.
description: Questo documento elenca il sommario delle destinazioni Adobe Experience Platform
feature: Destinations
source-git-commit: 6221fd920d297fe6982fba8d61db5fc242ce5a25
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 9%

---


# Destinazioni {#destinations}

* [Destinazioni - Panoramica](./home.md)
* [Tipi di destinazione e categorie](./destination-types.md)
* Esercitazioni API {#api}
   * [Connettiti alle destinazioni di streaming e attiva i dati utilizzando l’API del servizio di flusso](./api/streaming-destinations.md)
   * [Connettiti alle destinazioni di marketing e-mail e attiva i dati utilizzando l’API del servizio di flusso](./api/email-marketing.md)
   * [(Beta) Attiva i segmenti nelle destinazioni batch tramite API di attivazione ad hoc](./api/ad-hoc-activation-api.md)
* Guide dell&#39;interfaccia {#ui}
   * [Area di lavoro Destinazioni](./ui/destinations-workspace.md)
   * [Crea una nuova connessione di destinazione](./ui/connect-destination.md)
   * Attivare i dati del pubblico nelle destinazioni{#activate}
      * [Panoramica di Activation](./ui/activation-overview.md)
      * [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](./ui/activate-segment-streaming-destinations.md)
      * [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo in streaming](./ui/activate-streaming-profile-destinations.md)
      * [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](./ui/activate-batch-profile-destinations.md)
      * [Attivare i dati del pubblico nelle destinazioni di richiesta del profilo (Beta)](./ui/activate-profile-request-destinations.md)
   * [Visualizza dettagli destinazione](./ui/destination-details-page.md)
   * [Aggiorna account di destinazione](./ui/update-accounts.md)
   * [Modifica flussi di attivazione](./ui/edit-activation.md)
   * [Eliminare le destinazioni](./ui/delete-destinations.md)
   * [Monitorare i flussi di dati](./ui/monitor-dataflows.md)
* Catalogo delle destinazioni {#catalog}
   * [Panoramica del catalogo delle destinazioni](./catalog/overview.md)
   * [ Connessione HTTP (Alpha)](./catalog/http-destination.md)
   * Destinazioni di Adobe{#adobe}
      * [Panoramica sulle destinazioni di Adobe](./catalog/adobe/overview.md)
      * [Connessione al Marketo Engage (Beta)](./catalog/adobe/marketo-engage.md)
      * [Experience Platform di condivisione dei segmenti](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * Destinazioni pubblicitarie{#advertising}
      * [Panoramica sulle destinazioni pubblicitarie](./catalog/advertising/overview.md)
      * [Estensione Adobe Advertising Cloud](./catalog/advertising/adobe-advertising-cloud.md)
      * [Estensione Tag di conversione Awin Advertiser](./catalog/advertising/awin-conversiontag.md)
      * [Estensione Awin Advertiser Mastertag](./catalog/advertising/awin-mastertag.md)
      * [Estensione Bing Ads Universal Event Tracking (UET)](./catalog/advertising/bing-ads.md)
      * [Estensione ramo](./catalog/advertising/branch.md)
      * [Estensione DoubleClick Floodlight (Beta)](./catalog/advertising/doubleclick-floodlight.md)
      * [Estensione facebook Pixel](./catalog/advertising/facebook-pixel.md)
      * [Estensione Flashtalk OneTag](./catalog/advertising/flashtalking.md)
      * [Connessione Google Ads](./catalog/advertising/google-ads-destination.md)
      * [Estensione Google Ads](./catalog/advertising/google-ads-extension.md)
      * [Connessione Google Ad Manager](./catalog/advertising/google-ad-manager.md)
      * [Connessione Customer Match di Google](./catalog/advertising/google-customer-match.md)
      * [Connessione Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
      * [Estensione tag Google](./catalog/advertising/gtag-advertising.md)
      * [Estensione linkedIn Insight Tag](./catalog/advertising/linkedin.md)
      * [Connessione Microsoft Bing](./catalog/advertising/bing.md)
      * [Estensione pinterest Conversion Tracking](./catalog/advertising/pinterest-extension.md)
      * [Connessione all’elenco dei clienti pinterest](./catalog/advertising/pinterest.md)
      * [Il collegamento del Trade Desk](./catalog/advertising/tradedesk.md)
      * [Estensione tag twitter Universal Website](./catalog/advertising/twitter-uwt.md)
      * [Connessione Yahoo/Verizon DataX](./catalog/advertising/datax.md)
   * Destinazioni di Analytics {#analytics}
      * [Panoramica sulle destinazioni di Analytics](./catalog/analytics/overview.md)
      * [Estensione di tracciamento dei siti web di Adobe](./catalog/analytics/adform.md)
      * [Estensione Adobe Analytics](./catalog/analytics/adobe-analytics.md)
      * [Estensione Adobe Media Analytics for Audio and Video](./catalog/analytics/adobe-video-analytics.md)
      * [Estensione Clicktale](./catalog/analytics/clicktale.md)
      * [Estensione Contentsquare](./catalog/analytics/contentsquare.md)
      * [Estensione Decibel](./catalog/analytics/decibel.md)
      * [Estensione Demandbase](./catalog/analytics/demandbase.md)
      * [Estensione DialogTech](./catalog/analytics/dialogtech.md)
      * [Estensione Google Global Site Tag](./catalog/analytics/gtag-analytics.md)
      * [Estensione Google Universal Analytics](./catalog/analytics/google-universal-analytics.md)
      * [Estensione JW Player Analytics (Beta)](./catalog/analytics/jw-player-analytics.md)
      * [Estensione Nielsen BSDK](./catalog/analytics/nielsen-bsdk.md)
      * [Estensione Nielsen IMA Handler](./catalog/analytics/nielsen-ima.md)
      * [Estensione Nielsen VideoJS Player Handler](./catalog/analytics/nielsen-videojs.md)
      * [Estensione Parse.ly Analytics](./catalog/analytics/parsely.md)
      * [Estensione quantistica](./catalog/analytics/quantum-metric.md)
      * [Estensione SessionCam](./catalog/analytics/sessioncam.md)
      * [Estensione TMMData](./catalog/analytics/tmmdata.md)
      * [Estensione Yext Conversion Tracking](./catalog/analytics/yext.md)
   * Destinazioni di archiviazione cloud {#cloud-storage}
      * [Panoramica delle destinazioni di archiviazione cloud](./catalog/cloud-storage/overview.md)
      * [(Beta) Connessione Amazon Kinesis](./catalog/cloud-storage/amazon-kinesis.md)
      * [Connessione Amazon S3](./catalog/cloud-storage/amazon-s3.md)
      * [Connessione BLOB di Azure](./catalog/cloud-storage/azure-blob.md)
      * [(Beta) Connessione ad Azure Event Hubs](./catalog/cloud-storage/azure-event-hubs.md)
      * [Connessione SFTP](./catalog/cloud-storage/sftp.md)
      * [ELENCO CONSENTITI di indirizzo IP](./catalog/cloud-storage/ip-address-allow-list.md)
   * Destinazioni della piattaforma di gestione dati {#data-management}
      * [Panoramica sulle destinazioni della Data Management Platform (DMP)](./catalog/data-management/overview.md)
      * [Estensione Audience Manager DIL](./catalog/data-management/aam-dil-extension.md)
   * Destinazioni e-mail {#email}
      * [Estensione Bizible](./catalog/email/bizible.md)
      * [Estensione Marketo](./catalog/email/marketo.md)
      * [Estensione Marketo Munchkin](./catalog/email/marketo-munchkin.md)
      * [Estensione PebblePost](./catalog/email/pebblepost.md)
   * Destinazioni di marketing e-mail {#email-marketing}
      * [Panoramica sulle destinazioni di e-mail marketing](./catalog/email-marketing/overview.md)
      * [Connessione Adobe Campaign](./catalog/email-marketing/adobe-campaign.md)
      * [Oracle collegamento Eloqua](./catalog/email-marketing/oracle-eloqua.md)
      * [Oracle connessione Responsys](./catalog/email-marketing/oracle-responsys.md)
      * [Collegamento Marketing Cloud Salesforce](./catalog/email-marketing/salesforce-marketing-cloud.md)
   * Assegnare tag alle estensioni {#launch-extensions}
      * [Panoramica dell’estensione tag](./catalog/launch-extensions/overview.md)
   * Destinazioni di coinvolgimento mobile {#mobile-engagement}
      * [Panoramica delle destinazioni di coinvolgimento mobile](./catalog/mobile-engagement/overview.md)
      * [Collegamento Attributi del volo](./catalog/mobile-engagement/airship-attributes.md)
      * [Collegamento dei tag dell&#39;aeroporto](./catalog/mobile-engagement/airship-tags.md)
      * [Collegamento del freno](./catalog/mobile-engagement/braze.md)
   * Destinazioni di personalizzazione {#personalization}
      * [Panoramica sulle destinazioni di personalizzazione](./catalog/personalization/overview.md)
      * [Connessione Adobe Target (Beta)](./catalog/personalization/adobe-target-connection.md)
      * [Estensione Adobe Target](./catalog/personalization/adobe-target.md)
      * [Estensione Adobe Target v2](./catalog/personalization/adobe-target-v2.md)
      * [Estensione dei raggi anabbaglianti](./catalog/personalization/beemray.md)
      * [Connessione di personalizzazione personalizzata (Beta)](./catalog/personalization/custom-personalization.md)
      * [Estensione D&amp;B Visitor Intelligence](./catalog/personalization/dnb.md)
      * [Estensione del servizio Experience Cloud ID](./catalog/personalization/adobe-ecid.md)
      * [Estensione del guadagno](./catalog/personalization/gainsight.md)
      * [Estensione KickFire](./catalog/personalization/kickfire.md)
      * [Estensione Marketo Web Personalization](./catalog/personalization/marketo-web-personalization.md)
   * Destinazioni social{#social}
      * [Panoramica delle destinazioni social](./catalog/social/overview.md)
      * [Estensione Adobe Livefyre](./catalog/social/adobe-livefyre.md)
      * [Connessione facebook](./catalog/social/facebook.md)
      * [Connessione linkedIn Matched Audiences](./catalog/social/linkedin.md)
      * [[!DNL Twitter Custom Audiences] connection](./catalog/social/twitter.md)
   * Destinazioni del sondaggio {#survey}
      * [Panoramica sulle destinazioni del sondaggio](./catalog/survey/overview.md)
      * [Destinazione dell&#39;estensione Foresee](./catalog/survey/foresee.md)
      * [Estensione InMoment](./catalog/survey/inmoment.md)
      * [Estensione Qualtrics Website Feedback](./catalog/survey/qualtrics.md)
      * [Estensione QuestionPro Intercept Survey](./catalog/survey/web-intercept-surveys.md)
   * Voce delle destinazioni dei clienti {#voice}
      * [Panoramica sulla voce delle destinazioni del cliente](./catalog/voice/overview.md)
      * [Conferma estensione Digital Feedback](./catalog/voice/confirmit-digital-feedback.md)
      * [Estensione Invoca Tags](./catalog/voice/invoca.md)
      * [Estensione Medallia](./catalog/voice/medallia.md)
      * [Estensione casella in entrata Talk URL](./catalog/voice/talkurl.md)
* SDK di destinazione {#destination-sdk}
   * [Panoramica](./destination-sdk/overview.md)
   * [Prerequisiti per l’integrazione](./destination-sdk/integration-prerequisites.md)
   * [Introduzione](./destination-sdk/getting-started.md)
   * Funzionalità SDK per la destinazione {#functionality}
      * [Opzioni di configurazione](./destination-sdk/configuration-options.md)
      * [Configurazione della destinazione](./destination-sdk/destination-configuration.md)
      * [Specifiche del server e del modello](./destination-sdk/server-and-template-configuration.md)
      * [Formato del messaggio](./destination-sdk/message-format.md)
      * [Gestione dei metadati del pubblico](./destination-sdk/audience-metadata-management.md)
      * Autenticazione {#authentication}
         * [Configurazione dell’autenticazione](./destination-sdk/authentication-configuration.md)
         * [Autenticazione OAuth 2](./destination-sdk/oauth2-authentication.md)
      * Strumenti per sviluppatori {#developer-tools}
         * [Creare e testare un modello di trasformazione dei messaggi](./destination-sdk/create-template.md)
         * [Verifica la configurazione di destinazione](./destination-sdk/test-destination.md)
   * Operazioni API {#api}
      * [Riferimento API per l’SDK di destinazione (Authoring delle destinazioni)](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * [Operazioni API per gli endpoint delle destinazioni](./destination-sdk/destination-configuration-api.md)
      * [Operazioni API endpoint server di destinazione](./destination-sdk/destination-server-api.md)
      * [Operazioni API per l’endpoint dei metadati del pubblico](./destination-sdk/audience-metadata-api.md)
      * [Operazioni API per l’endpoint delle credenziali](./destination-sdk/credentials-configuration-api.md)
      * [Pubblicazione delle operazioni API dell’endpoint](./destination-sdk/destination-publish-api.md)
      * Riferimento per gli strumenti per sviluppatori {#developer-tools-reference}
         * [Ottieni operazioni API con modelli di esempio](./destination-sdk/sample-template-api.md)
         * [Operazioni API per i modelli di rendering](./destination-sdk/render-template-api.md)
         * [Operazioni API per il test di destinazione](./destination-sdk/destination-testing-api.md)
         * [Operazioni API per la generazione di profili di esempio](./destination-sdk/sample-profile-generation-api.md)
   * Guide {#guides}
      * [Usa SDK di destinazione per configurare una destinazione in streaming](./destination-sdk/configure-destination-instructions.md)
   * Documentare la destinazione {#document-destination}
      * [Documentare la destinazione in Adobe Experience Platform](./destination-sdk/docs-framework/documentation-instructions.md)
      * [Utilizza l’interfaccia web GitHub per creare una pagina di documentazione di destinazione](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [Utilizza un editor di testo nel tuo ambiente locale per creare una pagina di documentazione di destinazione](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [Modello self-service della documentazione](./destination-sdk/docs-framework/self-service-template.md)
* [Domande frequenti](./destinations-faq.md)
* [Note sulla versione di Platform](https://www.adobe.com/go/platform-release-notes-en)
