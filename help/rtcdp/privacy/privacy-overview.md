---
keywords: governance dei dati rtcdp;rtcdp governance dei dati;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: Privacy in Real-time Customer Data Platform
description: Adobe Real-time Customer Data Platform consente di semplificare il processo di conformità delle operazioni sui dati alle normative sulla privacy.
feature: Get Started, Privacy
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Privacy in Real-time Customer Data Platform

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) consente ai professionisti del marketing di unire dati provenienti da più sistemi aziendali, consentendo loro di identificare, comprendere e coinvolgere meglio i propri clienti. Adobe considera la privacy dei dati dei consumatori un principio fondamentale della progettazione e fornisce vari controlli per aiutare gli esperti di marketing a gestire la privacy dei dati dei loro clienti.

La maggior parte delle funzionalità di [!DNL Real-Time CDP] sono basate su Adobe Experience Platform. In questo documento vengono fornite informazioni sulle varie tecnologie per il miglioramento della privacy supportate da [!DNL Real-Time CDP], con collegamenti alla documentazione di [!DNL Experience Platform] per ulteriori informazioni.

## Rispetto delle richieste di accesso e di cancellazione dei clienti

Le normative legali sulla privacy, come il [!DNL General Data Protection Regulation] (RGPD) e il [!DNL California Consumer Privacy Act] (CCPA), consentono ai clienti di richiedere l&#39;accesso o l&#39;eliminazione dei dati personali raccolti. Poiché [!DNL Real-Time CDP] sfrutta le funzionalità di [!DNL Experience Platform] per la raccolta e l&#39;archiviazione dei dati, le richieste dei clienti di accedere ed eliminare i propri dati personali devono essere gestite entro [!DNL Platform]. Per ulteriori informazioni, consulta la panoramica su [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

>[!IMPORTANT]
>
> Le richieste di accesso ai dati personali inviate tramite Adobe Experience Platform Privacy Service per Adobe Marketo Engage si applicano solo ai clienti Real-Time CDP B2B.

## Funzionalità di rinuncia

[!DNL Real-Time CDP] consente ai clienti di non includere i propri dati personali nei casi di utilizzo della segmentazione. Le preferenze di rinuncia dei clienti vengono acquisite e memorizzate da [!DNL Real-Time Customer Profile] e possono essere applicate escludendo gli utenti che hanno rinunciato a un pubblico utilizzando la logica booleana (&quot;AND NOT&quot;) nel predicato del segmento.

Per ulteriori informazioni, consulta il documento su [risposta alle richieste di rinuncia](../../segmentation/consents.md) nella documentazione del servizio di segmentazione di Adobe Experience Platform.

## Supporto IAB TCF 2.0

[!DNL Real-Time CDP] è basato su Adobe Experience Platform, che fa parte dell&#39;[elenco fornitori](https://iabeurope.eu/vendor-list-tcf/) registrato per [!DNL Transparency & Consent Framework (TCF)], come indicato da [!DNL Interactive Advertising Bureau (IAB)]. In conformità ai requisiti TCF 2.0, Platform consente di raccogliere dati dettagliati sul consenso del cliente e di integrarli nei profili cliente memorizzati. Questi dati sul consenso possono quindi essere presi in considerazione per stabilire se alcuni profili sono inclusi nei tipi di pubblico esportati, a seconda del loro caso d’uso.

Per ulteriori informazioni, vedere la panoramica sul supporto di [IAB TCF 2.0 nell&#39;Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md).

## Passaggi successivi

Questo documento fornisce una breve introduzione alle funzionalità di [!DNL Real-Time CDP] relative alla privacy. Per ulteriori informazioni su ciascuna funzione, consulta la documentazione accessibile dai collegamenti presenti in questa guida.
