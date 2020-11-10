---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: Privacy nel profilo dei dati del cliente in tempo reale
seo-title: Privacy nel profilo dei dati del cliente in tempo reale
description: Il profilo dati cliente in tempo reale consente di semplificare il processo di mantenimento delle operazioni sui dati conformi alle normative sulla privacy.
seo-description: Il profilo dati cliente in tempo reale consente di semplificare il processo di mantenimento delle operazioni sui dati conformi alle normative sulla privacy.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Privacy in [!DNL Real-time CDP]

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) aiuta gli esperti di marketing a mettere insieme i dati provenienti da più sistemi aziendali, consentendo loro di identificare, comprendere e coinvolgere meglio i clienti.  Adobe considera la privacy dei dati dei consumatori come un principio fondamentale di progettazione e fornisce vari controlli per aiutare gli addetti al marketing a gestire la privacy dei dati dei loro clienti.

La maggior parte delle [!DNL Real-time CDP] funzionalità è fornita da Adobe Experience Platform. Questo documento fornisce informazioni sulle varie tecnologie per il miglioramento della privacy supportate da [!DNL Real-time CDP], con collegamenti alla [!DNL Experience Platform] documentazione per ulteriori informazioni.

## Come soddisfare le richieste di accesso ed eliminazione dei clienti

Le normative sulla privacy legali, come il [!DNL General Data Protection Regulation] (GDPR) e il [!DNL California Consumer Privacy Act] (CCPA), danno ai clienti il diritto di richiedere l&#39;accesso o la cancellazione dei dati personali raccolti. Poiché [!DNL Real-time CDP] sfrutta [!DNL Experience Platform] le capacità di raccolta e archiviazione dei dati, le richieste dei clienti di accedere ed eliminare i loro dati personali devono essere gestite entro [!DNL Platform]. Per ulteriori informazioni, consulta la panoramica su [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) .

## Funzionalità di rifiuto

[!DNL Real-time CDP] consente ai clienti di scegliere di non includere i propri dati personali nei casi di utilizzo della segmentazione. Le preferenze di rifiuto dei clienti vengono acquisite e memorizzate da [!DNL Real-time Customer Profile]e possono essere applicate escludendo gli utenti che hanno rinunciato da un segmento utilizzando la logica booleana (&quot;AND NOT&quot;) nel predicato del segmento.

Per ulteriori informazioni, consulta il documento sul [rispetto delle richieste](../../segmentation/honoring-opt-outs.md) di rifiuto nella documentazione di Adobe Experience Platform Segmentation Service.

## Supporto IAB TCF 2.0

[!DNL Real-time CDP] fa parte dell&#39;elenco [di](https://iabeurope.eu/vendor-list-tcf-v2-0/) fornitori registrati per il [!DNL Transparency & Consent Framework (TCF)], come indicato dall&#39; [!DNL Interactive Advertising Bureau] (IAB). In conformità ai requisiti di TCF 2.0, [!DNL Real-time CDP] puoi raccogliere dati dettagliati sul consenso dei clienti e integrarli nei profili dei clienti archiviati. Questi dati di consenso possono quindi essere presi in considerazione per stabilire se alcuni profili sono inclusi nei segmenti di pubblico esportati, a seconda del loro caso di utilizzo.

Per ulteriori informazioni, consulta la panoramica sul supporto [IAB TCF 2.0 in [!DNL Real-time CDP]](./iab/overview.md) .

## Passaggi successivi

Questo documento ha fornito una breve introduzione alle capacità di privacy di [!DNL Real-time CDP]. Per ulteriori informazioni su ciascuna funzione, consulta la documentazione collegata in questa guida.