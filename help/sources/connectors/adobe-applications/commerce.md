---
title: Connettore Source di Adobe Commerce
description: Scopri come utilizzare l’origine Adobe Commerce per dare Experience Platform ai dati di e-commerce.
last-substantial-update: 2023-12-13T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: 506f33e03dea5d5879808bccb82948209714926a
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Adobe Commerce

Adobe Commerce è una piattaforma di e-commerce agile B2B e B2C che consente a commercianti e marchi di accelerare i ricavi attraverso esperienze di e-commerce digitale incentrate sul cliente in spazi online e fisici.

Adobe Experience Platform Sources supporta l&#39;integrazione di Adobe Commerce per consentire ai commercianti di inviare i dati di vetrina e di back office all&#39;Edge Network Experience Platform, in modo che altri prodotti Adobe Experience Cloud come Adobe Analytics e Adobe Target possano utilizzare i dati di [!DNL Commerce].

* **Eventi Storefront**: acquisisce le interazioni dell&#39;acquirente come `View Page`, `View Product` e `Add to Cart`. Per i commercianti B2B, gli eventi storefront acquisiscono anche [elenchi di richieste](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>).
* **Eventi back office**: acquisisce informazioni sullo stato di un ordine, ad esempio se è stato effettuato, annullato, rimborsato, spedito o completato.

>[!NOTE]
>
>I dati acquisiti in Adobe Commerce non includono informazioni personali (PII, personally identifiable information). Tutti gli identificatori utente, come gli ID cookie e gli indirizzi IP, sono rigorosamente anonimi.

## Prerequisiti

Per collegare Adobe Commerce ad Experience Platform, è necessario disporre dei seguenti elementi:

* Adobe Commerce 2.4.3 o versione successiva.
* Un Adobe ID valido e un ID organizzazione.
* Accesso all&#39;estensione [Adobe Client Data Layer](../../../tags/extensions/client/client-data-layer/overview.md). Questa estensione è necessaria per raccogliere i dati dell’evento storefront.
* Diritti ad altri prodotti Adobe DX.

## Passaggi di onboarding

Per integrare completamente l’account sorgente di Adobe Commerce, segui i passaggi descritti di seguito insieme alla relativa documentazione.

* [Installa  [!DNL Data Connection] l&#39;estensione](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) per Adobe Commerce. È possibile scaricare l&#39;estensione del connettore da [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* Dopo aver installato correttamente l&#39;estensione del connettore, accedi al tuo account Adobe in Experience Cloud e [conferma l&#39;ID organizzazione](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Questo ID è associato alla società di Experience Cloud con provisioning. È formattato come stringa alfanumerica composta da 24 caratteri e include un `@AdobeOrg` obbligatorio.
* Quindi, crea o aggiorna lo schema Experience Data Model (XDM) con i gruppi di campi specifici di Commerce. Per i passaggi dettagliati su come aggiungere gruppi di campi specifici di Commerce allo schema XDM, consulta la guida su [aggiunta di gruppi di campi a uno schema XDM](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html).
* Una volta configurato lo schema, devi creare un set di dati basato sul nuovo schema. Questo set di dati conterrà i dati [!DNL Commerce] inviati. Per i passaggi dettagliati sulla creazione di un set di dati per i dati [!DNL Commerce], leggere la guida sull&#39;[invio di dati all&#39;Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* Quindi, crea un flusso di dati e seleziona lo schema XDM che contiene i gruppi di campi specifici di Commerce. Per ulteriori informazioni sugli stream di dati, leggere la [panoramica sugli stream di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html).
* Quindi è necessario connettere l&#39;istanza di Adobe Commerce al [Connettore servizi Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). Questo consente di distribuire l’istanza Commerce come SaaS (Software as a Service).
* Una volta completate tutte le configurazioni di cui sopra, è ora possibile connettersi ad Experience Platform configurando sia Commerce Services Connector che l&#39;estensione [!DNL Data Connection] utilizzando [!DNL Commerce Admin]. Per ulteriori informazioni su questo passaggio finale, consulta la guida su [connessione dei dati di Commerce all&#39;Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).
