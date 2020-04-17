---
title: Privacy nel profilo dei dati del cliente in tempo reale
seo-title: Privacy nel profilo dei dati del cliente in tempo reale
description: Il profilo dati cliente in tempo reale consente di semplificare il processo di mantenimento delle operazioni sui dati conformi alle normative sulla privacy.
seo-description: Il profilo dati cliente in tempo reale consente di semplificare il processo di mantenimento delle operazioni sui dati conformi alle normative sulla privacy.
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Privacy in CDP in tempo reale

Real-time Customer Data Platform (CDP in tempo reale) consente agli esperti di marketing di unire i dati provenienti da più sistemi aziendali, consentendogli di identificare, comprendere e coinvolgere meglio i clienti. Adobe considera la privacy dei dati dei consumatori come un principio fondamentale di progettazione e fornisce vari controlli per aiutare gli esperti di marketing a gestire la privacy dei dati dei loro clienti.

La maggior parte delle funzionalità CDP in tempo reale è fornita da Adobe Experience Platform. Questo documento fornisce informazioni sulle diverse tecnologie per il miglioramento della privacy supportate da CDP in tempo reale, con collegamenti alla documentazione della piattaforma Experience per ulteriori informazioni.

## Servizio Privacy

Il servizio Adobe Experience Platform per la privacy consente di semplificare il processo di mantenimento delle operazioni relative ai dati conformi alle normative sulla privacy, come il Regolamento generale sulla protezione dei dati (General Data Protection Regulation, GDPR) e il California Consumer Privacy Act (CCPA). Poiché CDP in tempo reale sfrutta le funzionalità della piattaforma Experience per la raccolta e lo storage dei dati, le richieste di accesso ed eliminazione per GDPR e CCPA devono essere gestite all&#39;interno della piattaforma. Per un&#39;introduzione più dettagliata del servizio, consulta il documento di panoramica [del servizio](../../privacy-service/home.md) sulla privacy.

Esistono due metodi per inviare le singole richieste di dati GDPR e CCPA per accedere ed eliminare i dati dei clienti:

* Utilizzate l&#39;interfaccia utente [del servizio](https://gdprui.cloud.adobe.io/) Privacy per creare e monitorare le richieste di accesso ed eliminazione all&#39;interno di un&#39;area di lavoro visiva. Per istruzioni dettagliate, consulta l’esercitazione [sull’interfaccia utente del servizio](../../privacy-service/ui/overview.md) Privacy.
* Utilizzate l&#39;API [del servizio](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) Privacy per gestire le richieste di accesso ed eliminazione con le chiamate RESTful API. Per istruzioni dettagliate, consulta l’esercitazione [API](../../privacy-service/api/getting-started.md) Privacy Service.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Passaggi successivi

Questo documento fornisce una breve introduzione alle funzionalità Privacy di CDP in tempo reale. Per informazioni più dettagliate sulle procedure ottimali e sui passaggi per l&#39;invio delle richieste di accesso/eliminazione, consulta la documentazione [del Servizio](../../privacy-service/home.md)per la privacy.