---
title: Connettore sorgente Adobe Commerce
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

Adobe Experience Platform Sources supporta l’integrazione di Adobe Commerce per consentire ai commercianti di inviare i dati di vetrina e di back office ad Experienci Platform Edge Network, in modo che altri prodotti Adobe Experience Cloud come Adobe Analytics e Adobe Target possano utilizzare [!DNL Commerce] dati.

* **Eventi vetrina**: acquisisce le interazioni dell’acquirente come `View Page`, `View Product`, e `Add to Cart`. Per gli esercenti B2B, gli eventi storefront acquisiscono anche [elenchi richieste di acquisto](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>).
* **Eventi back office**: acquisisce informazioni sullo stato di un ordine, ad esempio se è stato effettuato, annullato, rimborsato, spedito o completato.

>[!NOTE]
>
>I dati acquisiti in Adobe Commerce non includono informazioni personali (PII, personally identifiable information). Tutti gli identificatori utente, come gli ID cookie e gli indirizzi IP, sono rigorosamente anonimi.

## Prerequisiti

Per collegare Adobe Commerce ad Experienci Platform, è necessario disporre dei seguenti elementi:

* Adobe Commerce 2.4.3 o versione successiva.
* Un Adobe ID valido e un ID organizzazione.
* Accesso al [Estensione Adobe Client Data Layer](../../../tags/extensions/client/client-data-layer/overview.md). Questa estensione è necessaria per raccogliere i dati dell’evento storefront.
* Diritti ad altri prodotti Adobe DX.

## Passaggi di onboarding

Per integrare completamente l’account sorgente di Adobe Commerce, segui i passaggi descritti di seguito insieme alla relativa documentazione.

* [Installare [!DNL Data Connection] estensione](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) per Adobe Commerce. Puoi scaricare l’estensione del connettore da [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* Dopo aver installato correttamente l’estensione del connettore, accedi al tuo account di Adobe in Experience Cloud e [conferma il tuo ID organizzazione](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Questo ID è associato alla società di Experience Cloud con provisioning. È formattato come stringa alfanumerica composta da 24 caratteri e include una stringa `@AdobeOrg`.
* Quindi, crea o aggiorna lo schema Experience Data Model (XDM) con i gruppi di campi specifici di Commerce. Per i passaggi dettagliati su come aggiungere gruppi di campi specifici di Commerce allo schema XDM, consulta la guida su [aggiunta di gruppi di campi a uno schema XDM](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html).
* Una volta configurato lo schema, devi creare un set di dati basato sul nuovo schema. Questo set di dati conterrà quindi [!DNL Commerce] dati inviati. Per passaggi dettagliati su come creare un set di dati per [!DNL Commerce] , leggi la guida su [invio di dati all’Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* Quindi, crea un flusso di dati e seleziona lo schema XDM che contiene i gruppi di campi specifici di Commerce. Per ulteriori informazioni sugli stream di dati, consulta [panoramica sugli stream di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html).
* Quindi, devi collegare la tua istanza di Adobe Commerce al [Connettore Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). Questo consente di distribuire l’istanza Commerce come SaaS (Software as a Service).
* Una volta completate tutte le configurazioni di cui sopra, è ora possibile connettersi ad Experienci Platform configurando sia Commerce Services Connector che [!DNL Data Connection] tramite il [!DNL Commerce Admin]. Per ulteriori informazioni su questo passaggio finale, consulta la guida [connessione dei dati di Commerce all’Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).
