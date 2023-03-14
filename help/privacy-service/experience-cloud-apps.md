---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Applicazioni Privacy Service e Experience Cloud
description: Questo documento fornisce un riferimento su come configurare diverse applicazioni Experience Cloud per le operazioni relative alla privacy.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 12%

---

# [!DNL Privacy Service] e [!DNL Experience Cloud] applicazioni

Adobe Experience Platform [!DNL Privacy Service] è stato creato per supportare le richieste di accesso a dati personali per diverse applicazioni Adobe Experience Cloud. Ogni applicazione supporta diversi valori e ID di prodotto per identificare le persone interessate.

Questo documento funge da riferimento per [!DNL Experience Cloud] documentazione dell’applicazione che illustra come configurare l’applicazione per le operazioni relative alla privacy. Questo include come formattare ed etichettare i dati. Sono contemplate due categorie di domande:

* [Applicazioni integrate con Privacy Service](#integrated): applicazioni in grado di inviare richieste di accesso, eliminazione o rinuncia a [!DNL Privacy Service].
* [Applicazioni self-service](#self-serve): applicazioni che devono gestire internamente le richieste di privacy e non possono comunicare con [!DNL Privacy Service] direttamente.

Consulta la documentazione di per [!DNL Experience Cloud] applicazioni per scoprire come formattare le richieste di accesso a dati personali e quali valori sono supportati per tali richieste.

## Applicazioni integrate con [!DNL Privacy Service] {#integrated}

Di seguito è riportato un elenco [!DNL Experience Cloud] applicazioni integrate con [!DNL Privacy Service], incluso [!DNL Privacy Service] le funzionalità con cui sono compatibili, i loro protocolli per l’elaborazione delle richieste di eliminazione e i collegamenti alla documentazione per ulteriori informazioni.

>[!NOTE]
>
>Tutti i prodotti integrati rispondono alle richieste di privacy entro 30 giorni o meno.

| Applicazione | Accesso/eliminazione | Rinuncia alla vendita | Comportamento eliminazione | Documentazione e altre considerazioni |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | L’ID cookie o l’ID dispositivo dell’interessato viene eliminato dal sistema, insieme a tutti i dati relativi a costi, clic e ricavi associati al cookie. | <ul><li>[Accesso/eliminazione della documentazione relativa al RGPD](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Documentazione di accesso/eliminazione per CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentazione relativa alla rinuncia al CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Se `analyticsDeleteMethod` viene omesso o impostato su `anonymize` quando si effettua la richiesta di accesso a dati personali, tutti i dati a cui fa riferimento la raccolta specificata di ID utente vengono resi anonimi. Se `analyticsDeleteMethod` è impostato su `purge`, tutti i dati vengono rimossi completamente. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=it)</li><li>[!DNL Analytics] gestisce le richieste di rinuncia utilizzando [variabili di reporting sulla privacy](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/consent-variables.html?lang=it)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Tutte le caratteristiche e i segmenti associati all’identificatore Audience Manager incluso nella richiesta vengono eliminati. Inoltre, i rispettivi identificatori dell’individuo sono esclusi da un’ulteriore raccolta di dati e le rispettive mappature ID sono rimosse. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentazione sulla rinuncia](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | I dati memorizzati dell’interessato vengono eliminati dal sistema. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=it)</li><li>[Documentazione sulla rinuncia](../segmentation/consents.md)</li></ul> |
| Attributi del cliente di Adobe (CRS) | ✓ | N/D | Gli attributi dell’interessato vengono eliminati dal sistema. | <ul><li>[Accesso/eliminazione della documentazione relativa al RGPD](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html?lang=it)</li><li>[Documentazione di accesso/eliminazione per CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html?lang=it)</li><li>La funzionalità Attributi del cliente non è in grado di trasferire dati, pertanto le richieste di rifiuto non sono applicabili.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Quando Experience Platform riceve una richiesta di eliminazione da Privacy Service, Platform invia una conferma a Privacy Service che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l’eliminazione. I record vengono quindi rimossi dal Data Lake o dall’archivio profili una volta completato il processo di privacy. Prima del completamento del processo, i dati vengono eliminati in modo preliminare e non sono quindi accessibili da alcun servizio Platform. | <ul><li>[Documentazione di accesso/eliminazione per Data Lake](../catalog/privacy.md)</li><li>[Documentazione di accesso/eliminazione per il servizio Identity](../identity-service/privacy.md)</li><li>[Documentazione di accesso/eliminazione per Real-Time Customer Profile](../profile/privacy.md)</li><li>[!DNL Experience Platform] onori [richieste di rinuncia per segmenti di pubblico](../segmentation/consents.md).</li></ul> |
| Autenticazione Adobe Primetime | ✓ | N/D | I dati memorizzati dell’interessato vengono eliminati dal sistema. | <ul><li>[Accedere/eliminare la documentazione](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] non è in grado di trasferire dati, pertanto le richieste di rifiuto della vendita non sono applicabili.</li></ul> |
| Adobe Target | ✓ | N/D | Tutti i dati associati all’ID della persona interessata vengono eliminati dal suo profilo visitatore. I dati aggregati o anonimi che non identificano l’individuo o che non sono altrimenti correlati (come i dati sul contenuto) non si applicano alle richieste di cancellazione. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=it)</li><li>[!DNL Target] non è in grado di trasferire dati, pertanto le richieste di rifiuto della vendita non sono applicabili.</li></ul> |
| Marketo Engage | ✓ | N/D | I dati memorizzati dell’interessato vengono eliminati dal sistema. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] non è in grado di trasferire dati, pertanto le richieste di rifiuto della vendita non sono applicabili.</li></ul> |

{style="table-layout:auto"}

## Applicazioni self-service {#self-serve}

Di seguito è riportato un elenco [!DNL Experience Cloud] applicazioni che non sono integrate con [!DNL Privacy Service] e devono gestire internamente i loro problemi di privacy. Vengono forniti collegamenti alla documentazione di ogni applicazione, insieme alle descrizioni del contenuto della documentazione.

| Applicazione | Descrizione della documentazione |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=it) | Panoramica delle funzionalità RGPD per Adobe Campaign Classic. |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | Panoramica di come un amministratore della privacy del cliente o un amministratore AEM può gestire le richieste RGPD. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Passaggi per effettuare richieste di accesso e cancellazione relative al RGPD tramite Livefyre. |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Assicurati che le installazioni del tuo Magento Commerce siano conformi ai requisiti delle normative sulla privacy specifiche. |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | Scopri come le normative sulla privacy si applicano a Marketo. |
| [Tag in Adobe Experience Platform](../tags/ui/client-side/consent.md) | Come gli sviluppatori possono utilizzare le estensioni e il generatore di regole per definire soluzioni di gestione dei consensi e delle rinunce. |
| [Workfront](https://www.workfront.com/privacy-notice) | Scopri come Workfront raccoglie dati personali e come un interessato può inviare una richiesta di accesso a dati personali tramite un modulo. |

{style="table-layout:auto"}
