---
keywords: governance dei dati rtcdp;governance dei dati rtcdp;governance dei dati dei profili dei dati dei clienti in tempo reale;privacy rtcdp;rtcdp privacy
title: Privacy nel profilo dei dati del cliente in tempo reale
seo-title: Privacy nel profilo dei dati del cliente in tempo reale
description: Il profilo dati cliente in tempo reale consente di semplificare il processo di mantenimento delle operazioni sui dati conformi alle normative sulla privacy.
seo-description: Il profilo dati cliente in tempo reale consente di semplificare il processo di mantenimento delle operazioni sui dati conformi alle normative sulla privacy.
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# Privacy in [!DNL Real-time CDP]

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) aiuta gli esperti di marketing a mettere insieme i dati provenienti da più sistemi aziendali, consentendo loro di identificare, comprendere e coinvolgere meglio i clienti.  Adobe considera la privacy dei dati dei consumatori come un principio fondamentale di progettazione e fornisce vari controlli per aiutare gli addetti al marketing a gestire la privacy dei dati dei loro clienti.

La maggior parte delle funzionalità [!DNL Real-time CDP] è fornita da Adobe Experience Platform. Questo documento fornisce informazioni sulle diverse tecnologie per il miglioramento della privacy supportate da [!DNL Real-time CDP], con collegamenti alla documentazione [!DNL Experience Platform] per ulteriori informazioni.

## Come soddisfare le richieste di accesso ed eliminazione dei clienti

Le normative sulla privacy legali, come il [!DNL General Data Protection Regulation] (GDPR) e il [!DNL California Consumer Privacy Act] (CCPA), danno ai clienti il diritto di richiedere l&#39;accesso o la cancellazione dei dati personali raccolti. Poiché [!DNL Real-time CDP] sfrutta le funzionalità [!DNL Experience Platform] per la raccolta e l&#39;archiviazione dei dati, le richieste dei clienti di accedere ed eliminare i propri dati personali devono essere gestite entro [!DNL Platform]. Per ulteriori informazioni, vedere la panoramica su [ Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Funzionalità di rifiuto

[!DNL Real-time CDP] consente ai clienti di scegliere di non includere i propri dati personali nei casi di utilizzo della segmentazione. Le preferenze di rifiuto dei clienti vengono acquisite e memorizzate da [!DNL Real-time Customer Profile] e possono essere applicate escludendo gli utenti che hanno rinunciato a un segmento utilizzando la logica booleana (&quot;AND NOT&quot;) nel predicato del segmento.

Per ulteriori informazioni, consulta il documento [sulle richieste di rifiuto](../../segmentation/honoring-opt-outs.md) nella documentazione di Adobe Experience Platform Segmentation Service.

## Supporto IAB TCF 2.0

[!DNL Real-time CDP] è basato su Adobe Experience Platform, che fa parte dell&#39; [elenco ](https://iabeurope.eu/vendor-list-tcf-v2-0/) dei fornitori registrati per il  [!DNL Transparency & Consent Framework (TCF)], come indicato dal  [!DNL Interactive Advertising Bureau (IAB)]. In conformità ai requisiti di TCF 2.0, la piattaforma consente di raccogliere dati dettagliati sul consenso dei clienti e integrarli nei profili dei clienti archiviati. Questi dati di consenso possono quindi essere presi in considerazione per stabilire se alcuni profili sono inclusi nei segmenti di pubblico esportati, a seconda del loro caso di utilizzo.

Per ulteriori informazioni, vedere la panoramica sul supporto di [IAB TCF 2.0 in  Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md).

## Passaggi successivi

Questo documento fornisce una breve introduzione alle funzionalità per la privacy di [!DNL Real-time CDP]. Per ulteriori informazioni su ciascuna funzione, consulta la documentazione collegata in questa guida.