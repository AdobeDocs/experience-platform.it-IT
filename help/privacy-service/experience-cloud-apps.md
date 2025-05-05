---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Applicazioni Privacy Service e Experience Cloud
description: Questo documento fornisce un riferimento su come configurare diverse applicazioni Experience Cloud per le operazioni relative alla privacy.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 10%

---

# [!DNL Privacy Service] e [!DNL Experience Cloud] applicazioni

Adobe Experience Platform [!DNL Privacy Service] è stato creato per supportare le richieste di accesso a dati personali per diverse applicazioni Adobe Experience Cloud. Ogni applicazione supporta diversi valori e ID di prodotto per identificare le persone interessate.

Questo documento funge da riferimento per la documentazione dell&#39;applicazione [!DNL Experience Cloud] che illustra come configurare l&#39;applicazione per le operazioni relative alla privacy. Questo include come formattare ed etichettare i dati. Sono contemplate due categorie di domande:

* [Applicazioni integrate con Privacy Service](#integrated): applicazioni in grado di inviare richieste di accesso, eliminazione o rinuncia a [!DNL Privacy Service].
* [Applicazioni self-service](#self-serve): applicazioni che devono gestire internamente le richieste di privacy e non possono comunicare direttamente con [!DNL Privacy Service].

Per informazioni su come formattare le richieste di accesso a dati personali e sui valori supportati per tali richieste, consultare la documentazione delle applicazioni [!DNL Experience Cloud].

## Applicazioni integrate con [!DNL Privacy Service] {#integrated}

Di seguito è riportato un elenco delle applicazioni [!DNL Experience Cloud] integrate con [!DNL Privacy Service], incluse le funzionalità [!DNL Privacy Service] con cui sono compatibili, i relativi protocolli per l&#39;elaborazione delle richieste di eliminazione e i collegamenti alla documentazione per ulteriori informazioni.

>[!NOTE]
>
>Tutti i prodotti integrati rispondono alle richieste di privacy entro 30 giorni o meno.

| Applicazione | Accesso/eliminazione | Rinuncia alla vendita | Comportamento eliminazione | Documentazione e altre considerazioni |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | L’ID cookie o l’ID dispositivo dell’interessato viene eliminato dal sistema, insieme a tutti i dati relativi a costi, clic e ricavi associati al cookie. | <ul><li>[Documentazione di accesso/eliminazione per RGPD](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html?lang=it)</li><li>[Documentazione di accesso/eliminazione per CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html?lang=it)</li><li>[Documentazione di Opt-out-of-sale per CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html?lang=it)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics fornisce strumenti per etichettare i dati in base alla loro sensibilità e alle restrizioni contrattuali. Le etichette sono un passaggio importante per:<ol><li>Identificazione degli interessati.</li><li>Determinazione dei dati da restituire come parte di una richiesta di accesso.</li><li>Identificazione dei campi dati che devono essere eliminati come parte di una richiesta di eliminazione.</li></ol> | <ul><li>[Flusso di lavoro per la privacy](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html?lang=it)</li><li>[Etichettatura Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html?lang=it)</li><li>[Rinuncia ad Analytics](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html?lang=it)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Tutte le caratteristiche e i segmenti associati all’identificatore Audience Manager incluso nella richiesta vengono eliminati. Inoltre, i rispettivi identificatori dell’individuo sono esclusi da un’ulteriore raccolta di dati e le rispettive mappature ID sono rimosse. | <ul><li>Documentazione di [Access](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html?lang=it#access-data) / [delete](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html?lang=it#delete-data)</li><li>[Documentazione per la rinuncia](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html?lang=it#opt-out-calls)</li><li>[Richieste di rinuncia](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html?lang=it#opt-out-requests)</li></ul> |
| Adobe Campaign Classic | ✓ | ✓ | I dati memorizzati dell’interessato vengono eliminati dal sistema. | <ul><li>[Gestione della privacy](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=it)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | I dati memorizzati dell’interessato vengono eliminati dal sistema. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/it/docs/campaign-standard/using/getting-started/privacy/privacy-management#right-access-forgotten)</li><li>[Documentazione per la rinuncia](https://experienceleague.adobe.com/it/docs/campaign-standard/using/profiles-and-audiences/understanding-opt-in-and-opt-out-processes/about-opt-in-and-opt-out-in-campaign)</li></ul> |
| Attributi del cliente di Adobe (CRS) | ✓ | N/D | Gli attributi dell’interessato vengono eliminati dal sistema. | <ul><li>[Documentazione di accesso/eliminazione per RGPD](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html?lang=it)</li><li>[Documentazione di accesso/eliminazione per CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html?lang=it)</li><li>La funzionalità Attributi del cliente non è in grado di trasferire dati, pertanto le richieste di rifiuto non sono applicabili.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Quando Experience Platform riceve una richiesta di eliminazione da Privacy Service, Experience Platform invia una conferma a Privacy Service che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l’eliminazione. I record vengono quindi rimossi dal Data Lake o dall’archivio profili una volta completato il processo di privacy. Prima del completamento del processo, i dati vengono eliminati in modo preliminare e non sono quindi accessibili da alcun servizio Experience Platform. | <ul><li>[Documentazione di accesso/eliminazione per Data Lake](../catalog/privacy.md)</li><li>[Accesso/eliminazione della documentazione per Identity Service](../identity-service/privacy.md)</li><li>[Accesso/eliminazione della documentazione per Real-Time Customer Profile](../profile/privacy.md)</li><li>[!DNL Experience Platform] rispetta [richieste di rinuncia per segmenti di pubblico](../segmentation/tutorials/consents.md).</li></ul> |
| Adobe Journey Optimizer | ✓ | N/D | I dati memorizzati dell’interessato vengono eliminati dal sistema. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/privacy/requests)</li></ul> |
| Autenticazione Adobe Pass | ✓ | N/D | I dati memorizzati dell’interessato vengono eliminati dal sistema. | <ul><li>[Accedere/eliminare la documentazione](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Il passaggio non è in grado di trasferire dati, pertanto le richieste di rifiuto non sono applicabili.</li></ul> |
| Adobe Target | ✓ | N/D | Tutti i dati associati all’ID della persona interessata vengono eliminati dal suo profilo visitatore. I dati aggregati o anonimi che non identificano l’individuo o che non sono altrimenti correlati (come i dati sul contenuto) non si applicano alle richieste di cancellazione. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=it)</li><li>[!DNL Target] non è in grado di trasferire dati, pertanto le richieste di rifiuto non sono applicabili.</li></ul> |
| Commerce (Personalization) | ✓ | N/D | Privacy Service elimina i dati [!DNL Commerce] memorizzati nei servizi SaaS di Commerce a scopo di marketing, il che significa che i profili e gli ordini delle persone interessate non vengono più inviati alle applicazioni di marketing Adobe per l&#39;utilizzo in campagne e percorsi di clienti. Tuttavia, Privacy Service non elimina i dati nell&#39;applicazione [!DNL Commerce], poiché potrebbero essere ancora necessari per le esigenze transazionali dei commercianti. I commercianti sono responsabili di qualsiasi richiesta di eliminazione/accesso ai dati nell&#39;applicazione [!DNL Commerce]. | <ul><li>[Accesso/eliminazione della documentazione per Commerce](https://experienceleague.adobe.com/it/docs/commerce-merchant-services/data-connection/handle-privacy-request)</li></ul> |
| Marketo Engage | ✓ | N/D | I dati memorizzati dell’interessato vengono eliminati dal sistema. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html?lang=it)</li><li>[!DNL Marketo] non è in grado di trasferire dati, pertanto le richieste di rifiuto non sono applicabili.</li></ul> |

{style="table-layout:auto"}

## Applicazioni self-service {#self-serve}

Di seguito è riportato un elenco di applicazioni [!DNL Experience Cloud] che non sono integrate con [!DNL Privacy Service] e devono gestire internamente i propri problemi di privacy. Vengono forniti collegamenti alla documentazione di ogni applicazione, insieme alle descrizioni del contenuto della documentazione.

| Applicazione | Descrizione della documentazione |
| ------- | ----------- |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html?lang=it) | Panoramica su come un amministratore della privacy dei clienti o un amministratore AEM può gestire le richieste RGPD. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html?lang=it) | Passaggi per effettuare richieste di accesso e cancellazione relative al RGPD tramite Livefyre. |
| [Adobe Commerce](https://experienceleague.adobe.com/it/docs/commerce-operations/security-and-compliance/overview) | Assicurati che le tue installazioni di Adobe Commerce siano conformi ai requisiti di specifiche normative sulla privacy. |
| [Tag in Adobe Experience Platform](../tags/ui/client-side/consent.md) | Come gli sviluppatori possono utilizzare le estensioni e il generatore di regole per definire soluzioni di gestione dei consensi e delle rinunce. |
| [Workfront](https://www.workfront.com/privacy-notice) | Scopri come Workfront raccoglie dati personali e come un interessato può inviare una richiesta di accesso a dati personali tramite un modulo. |

{style="table-layout:auto"}
