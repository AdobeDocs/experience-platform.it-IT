---
title: Note sulla versione di Adobe Experience Platform di novembre 2024
description: Note sulla versione di Adobe Experience Platform di novembre 2024.
exl-id: e3969f8b-70b2-40f8-bb9b-5be6e3d8f722
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 96%

---

# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>La nuova [documentazione di prodotto dell’Assistente IA](../../ai-assistant/landing.md) è ora disponibile. Utilizza questa pagina come hub per tutte le risorse relative all’Assistente IA.

**Data di rilascio: 26 novembre 2024**

Aggiornamenti alle funzioni e alla documentazione esistenti in Adobe Experience Platform:

- [Assistente IA](#ai-assistant)
- [Destinazioni](#destinations)
- [Query Service](#query-service)
- [Sandbox](#sandboxes)
- [Aggiornamenti della documentazione](#documentation-updates)
   - [Documentazione API di Experience Platform interattiva](#interactive-experience-platform-api-documentation)
   - [Nuovo indice su Experience League](#new-table-of-contents-on-experience-league)
   - [Nuova pagina di destinazione dell’Assistente IA](#new-ai-assistant-landing-page)

## Assistente IA {#ai-assistant}

L’Assistente IA in Adobe Experience Platform è un’esperienza di conversazione che puoi utilizzare per accelerare i flussi di lavoro nelle applicazioni Adobe. È possibile utilizzare l’Assistente IA per accrescere la conoscenza del prodotto, risolvere i problemi o eseguire ricerche nelle informazioni e trovare approfondimenti operativi. L’Assistente IA supporta Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Alpha]{type=Informative} Monitorare modifiche significative e prevedere la crescita del pubblico | Utilizza l’Assistente IA per monitorare le modifiche significative e fornire previsioni sulla crescita del pubblico e le dimensioni del set di dati. Puoi quindi utilizzare queste informazioni per garantire l’integrità dei dati del pubblico e offrire proiezioni future a supporto di decisioni basate sui dati. Per ulteriori informazioni, consulta la guida su come [monitorare le modifiche significative e prevedere la crescita del pubblico](../../ai-assistant/new-features/audience-forecasting.md). |
| [!BADGE Alpha]{type=Informative} Stima del linguaggio naturale | Utilizza le capacità di stima del linguaggio naturale dell’Assistente IA per stimare le dimensioni del pubblico e prevederne le propensioni basandoti su semplici domande conversazionali. Per ulteriori informazioni, consulta la guida sull’[utilizzo della stima del linguaggio naturale con l’Assistente IA](../../ai-assistant/new-features/natural-language.md). |

{style="table-layout:auto"}

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| --- | --- |
| [Magnite Streaming in tempo reale](/help/destinations/catalog/advertising/magnite-streaming.md) | Esporta tipi di pubblico per l’attivazione, il targeting o la soppressione nella piattaforma Magnite Streaming. Affinché i tipi di pubblico possano essere esportati correttamente in Magnite, è necessario utilizzare sia le destinazioni in tempo reale che quelle batch. |
| [Magnite Streaming batch](/help/destinations/catalog/advertising/magnite-batch.md) | Esporta tipi di pubblico per l’attivazione, il targeting o la soppressione nella piattaforma Magnite Streaming. Affinché i tipi di pubblico possano essere esportati correttamente in Magnite, è necessario utilizzare sia le destinazioni in tempo reale che quelle batch. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| --- | --- |
| [Cerca attributi di profilo in tempo reale su Edge](/help/destinations/ui/activate-edge-profile-lookup.md) | Scopri come cercare gli attributi del profilo Edge in tempo reale per fornire esperienze di personalizzazione o comunicare le regole decisionali tramite le applicazioni a valle, utilizzando la destinazione Personalizzazione personalizzata e l’API Edge Network. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggi la [panoramica sulle destinazioni](../../destinations/home.md).

## Query Service {#query-service}

Eseguire query sui dati nel data lake di Adobe Experience Platform utilizzando SQL standard con Query Service. Combina facilmente i set di dati e generane nuovi dai risultati delle query per alimentare il reporting, i flussi di lavoro data science o facilitare l’acquisizione nel profilo cliente in tempo reale. Ad esempio, puoi unire i dati di transazione della clientela con i dati comportamentali per identificare tipi di pubblico ad alto valore per campagne di marketing mirate.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| API di autorizzazione Dater Distiller | Gestisci e applica restrizioni di accesso basate sull’IP per le sandbox di Query Service, per migliorare la sicurezza dei dati e garantire la conformità ai criteri organizzativi. Consulta la [Guida all’API di autorizzazione Data Distiller](../../query-service/auth-api/overview.md) per ulteriori informazioni sulle capacità e funzioni principali oppure la [documentazione di OpenAPI](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) per informazioni complete che includono dettagli sull’endpoint, gli elenchi dei parametri, gli esempi di richiesta/risposta e le funzionalità di test. |

Per ulteriori informazioni su [!DNL Query Service], consulta la [[!DNL Query Service] panoramica](../../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per soddisfare questa esigenza, Experience Platform fornisce ambienti sandbox che permettono di suddividere una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Condivisione pacchetto con l’API di strumenti di sandbox | Utilizza due nuovi endpoint API, [`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) e [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages), per gestire la condivisione dei pacchetti tra organizzazioni, ad esempio le approvazioni di richiesta, la visibilità del pacchetto e l’importazione di pacchetti, utilizzando l’API di strumenti sandbox. |

Per ulteriori informazioni sulle sandbox, consulta la [panoramica sulle sandbox](../../sandboxes/home.md).

## Aggiornamenti della documentazione {#documentation-updates}

### Documentazione API di Experience Platform interattiva {#interactive-api-documentation}

La [documentazione di Experience Platform API](https://developer.adobe.com/experience-platform-apis/) è ora completamente interattiva e consente di autenticare ed esplorare le API direttamente nella pagina della documentazione di riferimento API. Ora puoi passare alla pagina di documentazione di riferimento API desiderata, creare o ottenere le credenziali di autenticazione API, incollarle nel blocco **[!UICONTROL Prova]** ed eseguire la chiamata. Tutto su una sola pagina. [Ulteriori informazioni](/help/landing/api-authentication.md#get-credentials-functionality) sulla nuova funzionalità.

### Nuovo indice su Experience League {#new-table-of-contents-on-experience-league}

L’indice delle pagine di documentazione di Experience League è stato aggiornato per fornire ai lettori una migliore esperienza, includendo un filtro per parole chiave che consente di individuare la pagina esatta di cui si ha bisogno, la possibilità di espandere tutte le pagine e altro ancora. <br> ![Nuova esperienza dell’indice, inclusi il filtro per parole chiave e la possibilità di espandere tutte le pagine.](../2024/assets/november/new-toc-experience.gif "Nuova esperienza dell’indice, inclusi il filtro per parole chiave e la possibilità di espandere tutte le pagine."){width="250" align="center" zoomable="yes"}

### Nuova pagina di destinazione dell’Assistente IA {#new-ai-assistant-landing-page}

Utilizza la nuova pagina [documentazione di prodotto dell’ Assistente IA](../../ai-assistant/landing.md) come hub per tutti gli elementi dell’Assistente IA. Consulta la documentazione del prodotto per tutorial video, documentazione tecnica, casi d’uso e collegamenti ai post del blog sull’Assistente IA.
