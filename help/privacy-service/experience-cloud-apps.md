---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Applicazioni Privacy Service e Experience Cloud
description: Questo documento fornisce un riferimento su come configurare diverse applicazioni Experience Cloud per le operazioni relative alla privacy.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 4a078a09da131260fa44b64cd5f707482afdce04
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 10%

---

# [!DNL Privacy Service] e [!DNL Experience Cloud] applicazioni

Adobe Experience Platform [!DNL Privacy Service] è progettato per supportare le richieste di privacy per diverse applicazioni Adobe Experience Cloud. Ogni applicazione supporta valori di prodotto e ID diversi per identificare le persone interessate.

Questo documento funge da riferimento per [!DNL Experience Cloud] documentazione dell&#39;applicazione che descrive come configurare tale applicazione per le operazioni relative alla privacy. Ciò include la formattazione e l’etichetta dei dati. Si tratta di due categorie di domande:

* [Applicazioni integrate con Privacy Service](#integrated): Applicazioni in grado di inviare richieste di accesso, cancellazione o rinuncia a [!DNL Privacy Service].
* [Applicazioni self-service](#self-serve): Applicazioni che devono gestire internamente le proprie richieste di privacy e non possono comunicare con [!DNL Privacy Service] direttamente.

Consulta la documentazione per [!DNL Experience Cloud] per informazioni su come formattare le richieste di privacy e quali valori sono supportati per tali richieste.

## Applicazioni integrate con [!DNL Privacy Service] {#integrated}

Di seguito è riportato un elenco di [!DNL Experience Cloud] applicazioni integrate con [!DNL Privacy Service], compreso il [!DNL Privacy Service] funzionalità compatibili con , protocolli per l’elaborazione delle richieste di cancellazione e collegamenti alla documentazione per ulteriori informazioni.

>[!NOTE]
>
>Tutti i prodotti integrati rispondono alle richieste di privacy entro 30 giorni o meno.

| Applicazione | Accedere/eliminare | Rinuncia alla vendita | Elimina comportamento | Documentazione e altre considerazioni |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | L’ID cookie o l’ID dispositivo della persona interessata viene eliminato dal sistema, insieme a tutti i dati relativi a costi, clic e ricavi associati al cookie. | <ul><li>[Accedere/eliminare la documentazione relativa al RGPD](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Accedere/eliminare la documentazione relativa al CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentazione di rifiuto del CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics fornisce strumenti per l’etichettatura dei dati in base alla loro sensibilità e alle restrizioni contrattuali. Le etichette sono un passo importante per:<ol><li>Identificazione degli interessati.</li><li>Determinazione dei dati da restituire come parte di una richiesta di accesso.</li><li>Identificazione dei campi di dati che devono essere eliminati come parte di una richiesta di eliminazione.</li></ol> | <ul><li>[Flusso di lavoro sulla privacy](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)</li><li>[Etichette di Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Tutte le caratteristiche e i segmenti associati all’identificatore di Audience Manager incluso nella richiesta vengono eliminati. Inoltre, i rispettivi identificatori per il singolo utente vengono esclusi dall’ulteriore raccolta di dati e le rispettive mappature ID vengono rimosse. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentazione di rinuncia](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | I dati archiviati della persona interessata vengono eliminati dal sistema. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=it)</li><li>[Documentazione di rinuncia](../segmentation/consents.md)</li></ul> |
| Adobe Attributi del cliente (CRS) | ✓ | N/D | Gli attributi della persona interessata vengono eliminati dal sistema. | <ul><li>[Accedere/eliminare la documentazione relativa al RGPD](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html?lang=it)</li><li>[Accedere/eliminare la documentazione relativa al CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html?lang=it)</li><li>Gli attributi del cliente non sono in grado di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Quando Experience Platform riceve una richiesta di cancellazione da Privacy Service, Platform invia una conferma ad Privacy Service che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l’eliminazione. I record vengono quindi rimossi dall’archivio Data Lake o Profilo una volta che il processo di privacy è stato completato. Prima del completamento del processo, i dati vengono eliminati tramite soft e non sono quindi accessibili da alcun servizio Platform. | <ul><li>[Accedere/eliminare la documentazione per Data Lake](../catalog/privacy.md)</li><li>[Accedere/eliminare la documentazione relativa al servizio Identity](../identity-service/privacy.md)</li><li>[Accedere/eliminare la documentazione per il profilo cliente in tempo reale](../profile/privacy.md)</li><li>[!DNL Experience Platform] onori [richieste di rinuncia per segmenti di pubblico](../segmentation/consents.md).</li></ul> |
| Autenticazione Adobe Primetime | ✓ | N/D | I dati archiviati della persona interessata vengono eliminati dal sistema. | <ul><li>[Accedere/eliminare la documentazione](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] non dispone della capacità di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |
| Adobe Target | ✓ | N/D | Tutti i dati associati all’ID della persona interessata vengono eliminati dal relativo profilo visitatore. I dati aggregati o anonimi che non identificano l’individuo o che non sono altrimenti correlati (come i dati sul contenuto) non si applicano alle richieste di cancellazione. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=it)</li><li>[!DNL Target] non dispone della capacità di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |
| Marketo Engage | ✓ | N/D | I dati archiviati della persona interessata vengono eliminati dal sistema. | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] non dispone della capacità di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |

{style="table-layout:auto"}

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

{style="table-layout:auto"}
