---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Applicazioni Privacy Service e Experience Cloud
topic-legacy: overview
description: Questo documento fornisce un riferimento su come configurare diverse applicazioni Experience Cloud per le operazioni relative alla privacy.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 19%

---

# [!DNL Privacy Service] e  [!DNL Experience Cloud] applicazioni

Adobe Experience Platform [!DNL Privacy Service] è progettato per supportare le richieste di privacy per diverse applicazioni Adobe Experience Cloud. Ogni applicazione supporta valori di prodotto e ID diversi per identificare le persone interessate.

Questo documento funge da riferimento per la documentazione dell&#39;applicazione [!DNL Experience Cloud] che illustra come configurare tale applicazione per le operazioni relative alla privacy. Ciò include la formattazione e l’etichetta dei dati. Si tratta di due categorie di domande:

* [Applicazioni integrate con Privacy Service](#integrated): Applicazioni in grado di inviare richieste di accesso, cancellazione o rinuncia a  [!DNL Privacy Service].
* [Applicazioni](#self-serve) self-service: Applicazioni che devono gestire internamente le proprie richieste di privacy e non possono comunicare  [!DNL Privacy Service] direttamente con .

Per informazioni su come formattare le richieste di accesso a dati personali e quali valori sono supportati per tali richieste, consulta la documentazione relativa alle applicazioni [!DNL Experience Cloud] .

## Applicazioni integrate con [!DNL Privacy Service] {#integrated}

Di seguito è riportato un elenco delle applicazioni [!DNL Experience Cloud] integrate con [!DNL Privacy Service], incluse le funzionalità [!DNL Privacy Service] con cui sono compatibili, e sono presenti collegamenti alla documentazione per ulteriori informazioni.

| Applicazione | Accedere/eliminare | Rinuncia alla vendita | Documentazione e considerazioni |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | . | . | <ul><li>[Accedere/eliminare la documentazione relativa al RGPD](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Accedere/eliminare la documentazione relativa al CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentazione di rifiuto del CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | . | . | <ul><li>[Accedere/eliminare la documentazione](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] gestisce le richieste di rinuncia utilizzando le variabili di reporting  [sulla privacy](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | . | . | <ul><li>[Accedere/eliminare la documentazione](https://docs.adobe.com/content/help/it-IT/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentazione di rinuncia](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | . | . | <ul><li>[Accedere/eliminare la documentazione](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=it)</li><li>[Documentazione di rinuncia](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe Attributi del cliente (CRS) | . | N/D | <ul><li>[Accedere/eliminare la documentazione relativa al RGPD](https://docs.adobe.com/content/help/it-IT/core-services/interface/customer-attributes/gdpr.html)</li><li>[Accedere/eliminare la documentazione relativa al CCPA](https://docs.adobe.com/content/help/it-IT/core-services/interface/customer-attributes/ccpa.html)</li><li>Gli attributi del cliente non sono in grado di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |
| Adobe Experience Platform | . | . | <ul><li>[Accedere/eliminare la documentazione per Data Lake](../catalog/privacy.md)</li><li>[Accedere/eliminare la documentazione per il profilo cliente in tempo reale](../profile/privacy.md)</li><li>[!DNL Experience Platform] rispetta le richieste di  [rinuncia per i segmenti](../segmentation/honoring-opt-outs.md) di pubblico.</li></ul> |
| Autenticazione Adobe Primetime | . | N/D | <ul><li>[Accedere/eliminare la documentazione](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] non dispone della capacità di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |
| Adobe Target | . | N/D | <ul><li>[Accedere/eliminare la documentazione](https://docs.adobe.com/content/help/it-IT/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] non dispone della capacità di trasferire i dati, pertanto le richieste di rinuncia alla vendita non sono applicabili.</li></ul> |


## Applicazioni self-service {#self-serve}

Di seguito è riportato un elenco delle applicazioni [!DNL Experience Cloud] non integrate con [!DNL Privacy Service] che devono gestire internamente i propri problemi di privacy. Vengono forniti collegamenti alla documentazione di ogni applicazione, oltre a descrizioni del contenuto della documentazione.

| Applicazione | Descrizione della documentazione |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | Panoramica delle funzionalità RGPD per Adobe Campaign Classic. |
| [Adobe Dynamic Tag Manager](https://docs.adobe.com/content/help/it-IT/dtm/using/tools/opt-in.html) | Procedura per impedire l’attivazione dei tag di Adobe fino all’acquisizione del consenso. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Panoramica sulla gestione delle richieste RGPD da parte di un amministratore della privacy dei clienti o AEM amministratore. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Passaggi per effettuare le richieste di accesso e di cancellazione RGPD utilizzando Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Come gli sviluppatori possono utilizzare le estensioni e il generatore di regole per definire soluzioni di gestione dei consensi e delle rinunce. |
