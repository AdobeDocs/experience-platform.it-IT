---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Applicazioni Privacy Service e Experience Cloud
topic-legacy: overview
description: Questo documento fornisce un riferimento su come configurare diverse applicazioni Experience Cloud per le operazioni relative alla privacy.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: f0dc33dcd4803f157e411d8baf3b2d2f96cea5e1
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 15%

---

# [!DNL Privacy Service] e [!DNL Experience Cloud] applicazioni

Adobe Experience Platform [!DNL Privacy Service] è progettato per supportare le richieste di privacy per diverse applicazioni Adobe Experience Cloud. Ogni applicazione supporta valori di prodotto e ID diversi per identificare le persone interessate.

Questo documento funge da riferimento per [!DNL Experience Cloud] documentazione dell&#39;applicazione che descrive come configurare tale applicazione per le operazioni relative alla privacy. Ciò include la formattazione e l’etichetta dei dati. Si tratta di due categorie di domande:

* [Applicazioni integrate con Privacy Service](#integrated): Applicazioni in grado di inviare richieste di accesso, cancellazione o rinuncia a [!DNL Privacy Service].
* [Applicazioni self-service](#self-serve): Applicazioni che devono gestire internamente le proprie richieste di privacy e non possono comunicare con [!DNL Privacy Service] direttamente.

Consulta la documentazione per [!DNL Experience Cloud] per informazioni su come formattare le richieste di privacy e quali valori sono supportati per tali richieste.

## Applicazioni integrate con [!DNL Privacy Service] {#integrated}

Di seguito è riportato un elenco di [!DNL Experience Cloud] applicazioni integrate con [!DNL Privacy Service], compreso il [!DNL Privacy Service] funzionalità compatibili con e collegamenti alla documentazione per ulteriori informazioni.

| Applicazione | Accedere/eliminare | Rinuncia alla vendita | Documentazione e considerazioni |
| --- | :---: | :---: | --- |
| Adobe Advertising Cloud | ✓ | . | <ul><li>[Accedere/eliminare la documentazione relativa al RGPD](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Accedere/eliminare la documentazione relativa al CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentazione di rifiuto del CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | . | . | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=it)</li><li>[!DNL Analytics] gestisce le richieste di rinuncia utilizzando [variabili per la generazione di rapporti sulla privacy](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | . | . | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentazione di rinuncia](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | . | . | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=it)</li><li>[Documentazione di rinuncia](../segmentation/consents.md)</li></ul> |
| Adobe Attributi del cliente (CRS) | . | N/D | <ul><li>[Accedere/eliminare la documentazione relativa al RGPD](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[Accedere/eliminare la documentazione relativa al CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>Gli attributi del cliente non sono in grado di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |
| Adobe Experience Platform | . | . | <ul><li>[Accedere/eliminare la documentazione per Data Lake](../catalog/privacy.md)</li><li>[Accedere/eliminare la documentazione relativa al servizio Identity](../identity-service/privacy.md)</li><li>[Accedere/eliminare la documentazione per il profilo cliente in tempo reale](../profile/privacy.md)</li><li>[!DNL Experience Platform] onori [richieste di rinuncia per segmenti di pubblico](../segmentation/consents.md).</li></ul> |
| Autenticazione Adobe Primetime | . | N/D | <ul><li>[Accedere/eliminare la documentazione](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] non dispone della capacità di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |
| Adobe Target | . | N/D | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=it)</li><li>[!DNL Target] non dispone della capacità di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Applicazioni self-service {#self-serve}

Di seguito è riportato un elenco di [!DNL Experience Cloud] applicazioni non integrate con [!DNL Privacy Service] e devono gestire internamente le loro preoccupazioni in materia di privacy. Vengono forniti collegamenti alla documentazione di ogni applicazione, oltre a descrizioni del contenuto della documentazione.

| Applicazione | Descrizione della documentazione |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=it) | Panoramica delle funzionalità RGPD per Adobe Campaign Classic. |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | Panoramica sulla gestione delle richieste RGPD da parte di un amministratore della privacy dei clienti o AEM amministratore. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Passaggi per effettuare le richieste di accesso e di cancellazione RGPD utilizzando Livefyre. |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Assicurati che le installazioni del tuo Magento Commerce siano conformi ai requisiti delle normative sulla privacy specifiche. |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | Scopri come le normative sulla privacy si applicano a Marketo. |
| [Tag in Adobe Experience Platform](../tags/ui/client-side/consent.md) | Come gli sviluppatori possono utilizzare le estensioni e il generatore di regole per definire soluzioni di gestione dei consensi e delle rinunce. |
| [Workfront](https://www.workfront.com/privacy-notice) | Scopri in che modo Workfront raccoglie i dati personali e in che modo un interessato può inviare una richiesta di accesso a dati personali tramite un modulo. |

{style=&quot;table-layout:auto&quot;}
