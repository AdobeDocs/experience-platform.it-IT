---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Applicazioni Privacy Service e Experience Cloud '
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 20%

---


# [!DNL Privacy Service] e [!DNL Experience Cloud] applicazioni

 Adobe Experience Platform [!DNL Privacy Service] è progettato per supportare le richieste di privacy per diverse applicazioni Adobe Experience Cloud. Ogni applicazione supporta valori di prodotto e ID diversi per identificare gli interessati di dati.

Questo documento funge da riferimento per la documentazione [!DNL Experience Cloud] dell’applicazione che illustra come configurare tale applicazione per le operazioni relative alla privacy. Ciò include la formattazione e l&#39;etichetta dei dati. Sono previste due categorie di domande:

* [Applicazioni integrate con Privacy Service](#integrated): Applicazioni in grado di inviare richieste di accesso, eliminare o rifiutare [!DNL Privacy Service].
* [Applicazioni](#self-serve)self-service: Applicazioni che devono gestire internamente le proprie richieste di privacy e non possono comunicare [!DNL Privacy Service] direttamente.

Per informazioni su come formattare le richieste di privacy, consulta la documentazione relativa [!DNL Experience Cloud] alle applicazioni e quali valori sono supportati per tali richieste.

## Applicazioni integrate con [!DNL Privacy Service] {#integrated}

Di seguito è riportato un elenco di [!DNL Experience Cloud] applicazioni integrate con [!DNL Privacy Service], con le [!DNL Privacy Service] funzionalità compatibili e collegamenti alla documentazione per ulteriori informazioni.

| Applicazione | Accesso/eliminazione | Rifiuto della vendita | Documentazione e considerazioni |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Accedere/eliminare la documentazione](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>[!DNL Advertising Cloud] sfrutta le capacità globali di rinuncia offerte dal Centro per la privacy di Adobe. Per ulteriori informazioni, consulta la guida [su come effettuare richieste](https://docs.adobe.com/content/help/it-IT/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) di privacy per i dati.</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Accedere/eliminare la documentazione](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] gestisce le richieste di rifiuto utilizzando le variabili di reporting della [privacy](https://docs.adobe.com/content/help/it-IT/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Accedere/eliminare la documentazione](https://docs.adobe.com/content/help/it-IT/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentazione per il rifiuto](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Accedere/eliminare la documentazione](https://docs.campaign.adobe.com/doc/standard/getting_started/en/ACS_GDPR.html)</li><li>[Documentazione per il rifiuto](../segmentation/honoring-opt-outs.md)</li></ul> |
| Attributi del cliente Adobe (CRS) | ✓ | N/D | <ul><li>[Accedere/eliminare la documentazione per il GDPR](https://docs.adobe.com/content/help/it-IT/core-services/interface/customer-attributes/gdpr.html)</li><li>[Accedere/eliminare la documentazione per l&#39;applicazione CCPA](https://docs.adobe.com/content/help/it-IT/core-services/interface/customer-attributes/ccpa.html)</li><li>Gli attributi del cliente non sono in grado di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Accedere/eliminare la documentazione per il Data Lake](../catalog/privacy.md)</li><li>[Accedere/eliminare la documentazione per il profilo cliente in tempo reale](../profile/privacy.md)</li><li>[!DNL Experience Platform] rispetta le richieste di [rifiuto per i segmenti](../segmentation/honoring-opt-outs.md)di pubblico.</li></ul> |
| Autenticazione Adobe Primetime | ✓ | N/D | <ul><li>[Accedere/eliminare la documentazione](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] non è in grado di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |
| Adobe Target | ✓ | N/D | <ul><li>[Accedere/eliminare la documentazione](https://docs.adobe.com/content/help/it-IT/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] non è in grado di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |


## Applicazioni self-service {#self-serve}

Di seguito è riportato un elenco di [!DNL Experience Cloud] applicazioni che non sono integrate con [!DNL Privacy Service] e che devono gestire internamente le proprie preoccupazioni in materia di privacy. Vengono forniti collegamenti alla documentazione di ogni applicazione, con descrizioni dei contenuti della documentazione.

| Applicazione | Descrizione della documentazione |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | Panoramica delle funzionalità GDPR per  Adobe Campaign Classic. |
| [Adobe Dynamic Tag Manager](https://docs.adobe.com/content/help/it-IT/dtm/using/tools/opt-in.html) | Passaggi per impedire che i tag Adobe vengano attivati fino all’acquisizione del consenso. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Panoramica di come un amministratore della privacy cliente o AEM possono gestire le richieste GDPR. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Passaggi per l’accesso GDPR e l’eliminazione di richieste tramite Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Come gli sviluppatori possono utilizzare le estensioni e il generatore di regole per definire soluzioni di gestione dei consensi e delle rinunce. |
