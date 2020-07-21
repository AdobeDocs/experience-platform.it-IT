---
title: Privacy nel profilo dei dati del cliente in tempo reale
seo-title: Privacy nel profilo dei dati del cliente in tempo reale
description: Il profilo dati cliente in tempo reale consente di semplificare il processo di mantenimento delle operazioni sui dati conformi alle normative sulla privacy.
seo-description: Il profilo dati cliente in tempo reale consente di semplificare il processo di mantenimento delle operazioni sui dati conformi alle normative sulla privacy.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Privacy in CDP in tempo reale

[!DNL Real-time Customer Data Platform] (CDP in tempo reale) aiuta gli esperti di marketing a unire i dati provenienti da più sistemi aziendali, consentendo loro di identificare, comprendere e coinvolgere meglio i clienti. Adobe considera la privacy dei dati dei consumatori come un principio fondamentale di progettazione e fornisce vari controlli per aiutare gli esperti di marketing a gestire la privacy dei dati dei loro clienti.

La maggior parte delle funzionalità CDP in tempo reale è fornita da  Adobe Experience Platform. Questo documento fornisce informazioni sulle diverse tecnologie per il miglioramento della privacy supportate da CDP in tempo reale, con collegamenti alla [!DNL Experience Platform] documentazione per ulteriori informazioni.

## [!DNL Privacy Service]

 Adobe Experience Platform [!DNL Privacy Service] consente di semplificare il processo di mantenimento delle operazioni relative ai dati conformi alle normative sulla privacy, quali [!DNL General Data Protection Regulation] (GDPR) e [!DNL California Consumer Privacy Act] (CCPA). Poiché il CDP in tempo reale sfrutta [!DNL Experience Platform] le capacità di raccolta e archiviazione dei dati, le richieste di accesso ed eliminazione per il GDPR e il CCPA devono essere gestite all&#39;interno [!DNL Platform]. Consultate il documento di panoramica [di](../../privacy-service/home.md) Privacy Service per un&#39;introduzione più dettagliata del servizio.

Esistono due metodi per inviare le singole richieste di dati GDPR e CCPA per accedere ed eliminare i dati dei clienti:

* Utilizzate l&#39;icona [!DNL Privacy Service UI](https://gdprui.cloud.adobe.io/) per creare e monitorare le richieste di accesso ed eliminazione all&#39;interno di un&#39;area di lavoro visiva. Per istruzioni dettagliate, consulta l’esercitazione [sull’interfaccia utente di](../../privacy-service/ui/overview.md) Privacy Service.
* Utilizzate l&#39;API [!DNL Privacy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) per gestire le richieste di accesso ed eliminazione con le chiamate RESTful API. Per istruzioni dettagliate, vedete l&#39;esercitazione [API di](../../privacy-service/api/getting-started.md) Privacy Service.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Passaggi successivi

Questo documento fornisce una breve introduzione alle funzionalità Privacy di CDP in tempo reale. Per informazioni dettagliate sulle procedure ottimali e i passaggi per l&#39;invio delle richieste di accesso/eliminazione, consultare la documentazione [](../../privacy-service/home.md)Privacy Service.