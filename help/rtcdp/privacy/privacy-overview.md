---
keywords: governance dei dati rtcdp;rtcdp governance dei dati;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: Privacy in Real-time Customer Data Platform
description: Adobe Real-time Customer Data Platform consente di semplificare il processo di conformità delle operazioni sui dati alle normative sulla privacy.
feature: Get Started, Privacy
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: 2a0ebe1e92ea21ff45051096d5a6969839c2f947
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Privacy in Real-time Customer Data Platform

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) aiuta gli addetti al marketing a unire dati provenienti da più sistemi aziendali, consentendo loro di identificare, comprendere e coinvolgere meglio i clienti. Adobe considera la privacy dei dati dei consumatori un principio fondamentale della progettazione e fornisce vari controlli per aiutare gli esperti di marketing a gestire la privacy dei dati dei loro clienti.

La maggior parte dei [!DNL Real-Time CDP] sono fornite da Adobe Experience Platform. Questo documento fornisce informazioni sulle varie tecnologie di miglioramento della privacy supportate da [!DNL Real-Time CDP], con collegamenti a [!DNL Experience Platform] per ulteriori informazioni.

## Rispetto delle richieste di accesso e di cancellazione dei clienti

Normative legali sulla privacy come [!DNL General Data Protection Regulation] (RGPD) e [!DNL California Consumer Privacy Act] (CCPA) conferisci ai clienti il diritto di richiedere l’accesso o la cancellazione dei dati personali che raccogli da loro. Da [!DNL Real-Time CDP] sfrutta [!DNL Experience Platform] le funzionalità di raccolta e archiviazione dei dati, le richieste dei clienti di accedere e cancellare i propri dati personali devono essere gestite entro [!DNL Platform]. Consulta la panoramica su [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) per ulteriori informazioni.

>[!IMPORTANT]
>
> Le richieste di accesso ai dati personali inviate tramite Adobe Experience Platform Privacy Service per Adobe Marketo Engage si applicano solo ai clienti Real-Time CDP B2B.

## Funzionalità di rinuncia

[!DNL Real-Time CDP] consente ai clienti di rinunciare all’inclusione dei propri dati personali nei casi di utilizzo della segmentazione. Le preferenze di rinuncia dei clienti vengono acquisite e memorizzate da [!DNL Real-Time Customer Profile], e possono essere applicati escludendo gli utenti che hanno rinunciato a un segmento utilizzando la logica booleana (&quot;AND NOT&quot;) nel predicato del segmento.

Vedi il documento su [rispetto delle richieste di rinuncia](../../segmentation/consents.md) per ulteriori informazioni, consulta la documentazione sul servizio di segmentazione di Adobe Experience Platform.

## Supporto IAB TCF 2.0

[!DNL Real-Time CDP] è basato su Adobe Experience Platform, che fa parte di [elenco fornitori](https://iabeurope.eu/vendor-list-tcf/) per [!DNL Transparency & Consent Framework (TCF)], come indicato dalla [!DNL Interactive Advertising Bureau (IAB)]. In conformità ai requisiti TCF 2.0, Platform consente di raccogliere dati dettagliati sul consenso del cliente e di integrarli nei profili cliente memorizzati. Questi dati sul consenso possono quindi essere presi in considerazione per determinare se alcuni profili sono inclusi nei segmenti di pubblico esportati, a seconda del loro caso d’uso.

Consulta la panoramica su [Supporto IAB TCF 2.0 in Experienci Platform](../../landing/governance-privacy-security/consent/iab/overview.md) per ulteriori informazioni.

## Passaggi successivi

Questo documento fornisce una breve introduzione alle funzionalità di privacy di [!DNL Real-Time CDP]. Per ulteriori informazioni su ciascuna funzione, consulta la documentazione accessibile dai collegamenti presenti in questa guida.
