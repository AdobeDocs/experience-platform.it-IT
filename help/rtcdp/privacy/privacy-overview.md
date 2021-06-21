---
keywords: governance dei dati rtcdp;governance dei dati rtcdp;governance dei dati del profilo dei dati del cliente in tempo reale;privacy rtcdp;rtcdp privacy
title: Privacy in Real-time Customer Data Platform
seo-title: Privacy in Real-time Customer Data Platform
description: Real-time Customer Data Platform ti consente di semplificare il processo di mantenimento delle operazioni sui dati conformi alle normative sulla privacy.
seo-description: Real-time Customer Data Platform ti consente di semplificare il processo di mantenimento delle operazioni sui dati conformi alle normative sulla privacy.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: f193787ac27e30c69d25418656ae9c59c89622dc
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Privacy in Real-time Customer Data Platform

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) aiuta gli esperti di marketing a unire i dati di più sistemi aziendali, consentendo loro di identificare, comprendere e coinvolgere meglio i loro clienti. Adobe considera la privacy dei dati dei consumatori come un principio fondamentale di progettazione e fornisce vari controlli per aiutare gli esperti di marketing a gestire la privacy dei dati dei loro clienti.

La maggior parte delle funzionalità [!DNL Real-time CDP] è basata su Adobe Experience Platform. Questo documento fornisce informazioni sulle varie tecnologie per il miglioramento della privacy supportate da [!DNL Real-time CDP], con collegamenti alla documentazione [!DNL Experience Platform] per ulteriori informazioni.

## Soddisfare le richieste di accesso e cancellazione dei clienti

Le normative legali sulla privacy, come il [!DNL General Data Protection Regulation] (RGPD) e il [!DNL California Consumer Privacy Act] (CCPA), danno ai clienti il diritto di richiedere l&#39;accesso ai dati personali raccolti da loro o la loro cancellazione. Poiché [!DNL Real-time CDP] sfrutta le funzionalità di raccolta e archiviazione dei dati, le richieste dei clienti di accedere e cancellare i propri dati personali devono essere gestite all&#39;interno di [!DNL Platform]. [!DNL Experience Platform] Per ulteriori informazioni, consulta la panoramica su [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) .

## Funzionalità di rinuncia

[!DNL Real-time CDP] consente ai clienti di rinunciare all’inclusione dei propri dati personali nei casi di utilizzo della segmentazione. Le preferenze di rinuncia dei clienti vengono acquisite e memorizzate da [!DNL Real-time Customer Profile] e possono essere applicate escludendo gli utenti che hanno rinunciato a un segmento utilizzando la logica booleana (&quot;AND NOT&quot;) nel predicato del segmento.

Per ulteriori informazioni, consulta il documento [Rispetto delle richieste di rinuncia](../../segmentation/consents.md) nella documentazione del servizio di segmentazione di Adobe Experience Platform .

## Supporto IAB TCF 2.0

[!DNL Real-time CDP] è basato su Adobe Experience Platform, che fa parte dell’ [elenco dei fornitori registrati ](https://iabeurope.eu/vendor-list-tcf-v2-0/) per  [!DNL Transparency & Consent Framework (TCF)], come descritto da  [!DNL Interactive Advertising Bureau (IAB)]. In conformità ai requisiti di TCF 2.0, Platform ti consente di raccogliere dati dettagliati sul consenso dei clienti e integrarli nei profili dei clienti memorizzati. Questi dati di consenso possono quindi essere fatti in modo da determinare se alcuni profili sono inclusi nei segmenti di pubblico esportati, a seconda del loro caso d’uso.

Per ulteriori informazioni, consulta la panoramica sul supporto di [IAB TCF 2.0 in Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) .

## Passaggi successivi

Questo documento fornisce una breve introduzione alle funzionalità per la privacy di [!DNL Real-time CDP]. Per ulteriori informazioni su ciascuna funzione, consulta la documentazione collegata a in questa guida.
