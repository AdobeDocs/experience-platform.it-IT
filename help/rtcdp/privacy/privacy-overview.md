---
keywords: governance dei dati rtcdp;governance dei dati rtcdp;governance dei dati del profilo del cliente in tempo reale;privacy rtcdp;rtcdp privacy
title: Privacy in Real-time Customer Data Platform
description: Adobe Real-time Customer Data Platform ti consente di semplificare il processo per mantenere le operazioni sui dati conformi alle normative sulla privacy.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Privacy in Real-time Customer Data Platform

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) aiuta gli esperti di marketing a unire i dati provenienti da più sistemi aziendali, consentendo loro di identificare, comprendere e coinvolgere meglio i loro clienti. Adobe considera la privacy dei dati dei consumatori come un principio fondamentale di progettazione e fornisce vari controlli per aiutare gli esperti di marketing a gestire la privacy dei dati dei loro clienti.

La maggioranza dei [!DNL Real-Time CDP] Le funzionalità sono fornite da Adobe Experience Platform. Questo documento fornisce informazioni sulle varie tecnologie per il miglioramento della privacy supportate da [!DNL Real-Time CDP], con collegamenti a [!DNL Experience Platform] documentazione per ulteriori informazioni.

## Soddisfare le richieste di accesso e cancellazione dei clienti

Norme legali sulla privacy come [!DNL General Data Protection Regulation] (RGPD) e [!DNL California Consumer Privacy Act] (CCPA) offre ai clienti il diritto di richiedere l’accesso o la cancellazione dei dati personali raccolti da loro. Da [!DNL Real-Time CDP] leva finanziaria [!DNL Experience Platform] le funzionalità di raccolta e archiviazione dei dati, le richieste dei clienti di accesso e cancellazione dei propri dati personali devono essere gestite entro [!DNL Platform]. Vedi la panoramica su [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) per ulteriori informazioni.

>[!IMPORTANT]
>
> Le richieste di privacy inviate tramite Adobe Experience Platform Privacy Service per Adobe Marketo Engage si applicano solo ai clienti B2B Real-Time CDP.

## Funzionalità di rinuncia

[!DNL Real-Time CDP] consente ai clienti di rinunciare all’inclusione dei propri dati personali nei casi di utilizzo della segmentazione. Le preferenze di rinuncia dei clienti vengono acquisite e memorizzate da [!DNL Real-Time Customer Profile], e può essere applicato escludendo gli utenti che hanno rinunciato a un segmento utilizzando la logica booleana (&quot;AND NOT&quot;) nel predicato del segmento.

Visualizza il documento in [soddisfare le richieste di rinuncia](../../segmentation/consents.md) per ulteriori informazioni, consulta la documentazione sul servizio di segmentazione di Adobe Experience Platform .

## Supporto IAB TCF 2.0

[!DNL Real-Time CDP] è basato su Adobe Experience Platform, che fa parte della registrazione [elenco fornitori](https://iabeurope.eu/vendor-list-tcf-v2-0/) per [!DNL Transparency & Consent Framework (TCF)], come indicato dal [!DNL Interactive Advertising Bureau (IAB)]. In conformità ai requisiti di TCF 2.0, Platform ti consente di raccogliere dati dettagliati sul consenso dei clienti e integrarli nei profili dei clienti memorizzati. Questi dati di consenso possono quindi essere fatti in modo da determinare se alcuni profili sono inclusi nei segmenti di pubblico esportati, a seconda del loro caso d’uso.

Vedi la panoramica su [Supporto IAB TCF 2.0 in Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) per ulteriori informazioni.

## Passaggi successivi

Questo documento fornisce una breve introduzione alle funzionalità per la privacy di [!DNL Real-Time CDP]. Per ulteriori informazioni su ciascuna funzione, consulta la documentazione collegata a in questa guida.
