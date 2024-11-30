---
title: Note sulla versione di Adobe Experience Platform, novembre 2024
description: Note sulla versione di novembre 2024 per Adobe Experience Platform.
exl-id: e3969f8b-70b2-40f8-bb9b-5be6e3d8f722
source-git-commit: f71fc1d4ad51af52046caeee289546e05967d5bd
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 29%

---

# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>È ora disponibile la nuova documentazione di [AI Assistant](../../ai-assistant/landing.md). Utilizza questa pagina come hub per tutte le risorse relative all’Assistente di intelligenza artificiale.

**Data di rilascio: 26 novembre 2024**

Aggiornamenti alle funzioni e alla documentazione esistenti in Adobe Experience Platform:

- [Assistente IA](#ai-assistant)
- [Destinazioni](#destinations)
- [Servizio query](#query-service)
- [Sandbox](#sandboxes)
- [Aggiornamenti della documentazione](#documentation-updates)
   - [Documentazione API di Experience Platform interattiva](#interactive-experience-platform-api-documentation)
   - [Nuovo sommario su Experience League](#new-table-of-contents-on-experience-league)
   - [Nuova pagina di destinazione dell’Assistente AI](#new-ai-assistant-landing-page)

## Assistente IA {#ai-assistant}

L’Assistente IA in Adobe Experience Platform è un’esperienza di conversazione che puoi utilizzare per accelerare i flussi di lavoro nelle applicazioni Adobe. È possibile utilizzare l’Assistente IA per accrescere la conoscenza del prodotto, risolvere i problemi o eseguire ricerche nelle informazioni e trovare approfondimenti operativi. L’Assistente IA supporta Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Alpha]{type=Informativo} Monitora le modifiche significative e la crescita prevista del pubblico | Utilizza AI Assistant per monitorare modifiche significative e fornire previsioni di crescita per il pubblico e le dimensioni dei set di dati. Potrai quindi utilizzare queste informazioni per garantire l’integrità dei dati sul pubblico e offrire proiezioni lungimiranti per supportare processi decisionali basati sui dati. Per ulteriori informazioni, consulta la guida su [monitoraggio di cambiamenti significativi e previsione della crescita del pubblico](../../ai-assistant/new-features/audience-forecasting.md). |
| [!BADGE Alpha]{type=Informativo} Stima linguaggio naturale | Utilizza le funzionalità di stima del linguaggio naturale di AI Assistant per stimare le dimensioni del pubblico e prevedere le tendenze del pubblico in base a domande semplici e conversazionali. Per ulteriori informazioni, leggere la guida su [utilizzo della stima del linguaggio naturale con l&#39;Assistente AI](../../ai-assistant/new-features/natural-language.md). |

{style="table-layout:auto"}

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| --- | --- |
| [Streaming Magnite In Tempo Reale](/help/destinations/catalog/advertising/magnite-streaming.md) | Esporta tipi di pubblico per l’attivazione, il targeting o l’eliminazione nella piattaforma Magnite Streaming. Tieni presente che, affinché i tipi di pubblico possano essere esportati correttamente in Magnite, devi utilizzare sia le destinazioni in tempo reale che quelle batch. |
| [Batch di streaming Magnite](/help/destinations/catalog/advertising/magnite-batch.md) | Esporta tipi di pubblico per l’attivazione, il targeting o l’eliminazione nella piattaforma Magnite Streaming. Tieni presente che, affinché i tipi di pubblico possano essere esportati correttamente in Magnite, devi utilizzare sia le destinazioni in tempo reale che quelle batch. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| --- | --- |
| [Cerca attributi profilo in tempo reale sul perimetro](/help/destinations/ui/activate-edge-profile-lookup.md) | Scopri come cercare gli attributi del profilo edge in tempo reale per fornire esperienze di personalizzazione o informare le regole decisionali tramite le applicazioni a valle, utilizzando la destinazione Personalization personalizzata e l’API Edge Network. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggi la [panoramica sulle destinazioni](../../destinations/home.md).

## Query Service {#query-service}

Eseguire query sui dati nel data lake di Adobe Experience Platform utilizzando SQL standard con Query Service. Combina facilmente i set di dati e generane di nuovi dai risultati delle query per abilitare i rapporti, i flussi di lavoro della scienza dei dati o facilitare l’acquisizione nel profilo cliente in tempo reale. Ad esempio, puoi unire i dati delle transazioni dei clienti con i dati comportamentali per identificare tipi di pubblico di alto valore per campagne di marketing mirate.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Dater Distiller Authorization API | Gestisci e applica restrizioni di accesso basate su IP per le sandbox di Query Service, per migliorare la sicurezza dei dati e garantire la conformità con le policy organizzative. Consulta la [Guida all&#39;API di autorizzazione di Data Distiller](../../query-service/auth-api/overview.md) per ulteriori informazioni sulle sue funzionalità chiave o la [documentazione di OpenAPI](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) per informazioni complete, inclusi i dettagli dell&#39;endpoint, gli elenchi di parametri, gli esempi di richieste/risposte e le funzionalità di test. |

Per ulteriori informazioni su [!DNL Query Service], vedere la [[!DNL Query Service] panoramica](../../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per rispondere a questa esigenza, Experience Platform fornisce ambienti sandbox che permettono di suddividere una singola istanza di Platform in ambienti virtuali separati, utili per le attività di sviluppo e evoluzione delle applicazioni di esperienza digitale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Condivisione di pacchetti con l’API di strumenti sandbox | Utilizzare due nuovi endpoint API, [`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) e [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages) per gestire la condivisione dei pacchetti tra organizzazioni, ad esempio le approvazioni delle richieste, la visibilità dei pacchetti e l&#39;importazione di pacchetti, utilizzando l&#39;API di strumenti sandbox. |

Per ulteriori informazioni sulle sandbox, consulta la [panoramica sulle sandbox](../../sandboxes/home.md).

## Aggiornamenti della documentazione {#documentation-updates}

### Documentazione API di Experience Platform interattiva {#interactive-api-documentation}

La [documentazione di Experience Platform API](https://developer.adobe.com/experience-platform-apis/) è ora completamente interattiva e consente di autenticare ed esplorare le API direttamente nella pagina della documentazione di riferimento API. Ora puoi passare alla pagina di documentazione di riferimento API desiderata, creare o ottenere le credenziali di autenticazione API, incollarle nel blocco **[!UICONTROL Prova]** ed eseguire la chiamata. Tutto su una sola pagina. [Ulteriori informazioni](/help/landing/api-authentication.md#get-credentials-functionality) sulla funzionalità.

### Nuovo sommario su Experience League {#new-table-of-contents-on-experience-league}

Il sommario nelle pagine della documentazione di Experience League è stato migliorato per fornire ai lettori un’esperienza migliore, con un filtro per parole chiave che consente di scoprire la pagina esatta necessaria, la possibilità di espandere tutte le pagine e altro ancora. <br> ![Nuova esperienza del sommario, inclusi il filtro per parole chiave e la possibilità di espandere tutte le pagine.](../2024/assets/november/new-toc-experience.gif "Nuova esperienza del sommario, inclusi il filtro per parole chiave e la possibilità di espandere tutte le pagine."){width="250" align="center" zoomable="yes"}

### Nuova pagina di destinazione dell’Assistente AI {#new-ai-assistant-landing-page}

Utilizza la nuova pagina [Documentazione del prodotto dell&#39;Assistente AI](../../ai-assistant/landing.md) come hub per tutti gli elementi dell&#39;Assistente AI. Consulta la documentazione del prodotto per tutorial video, documentazione tecnica, casi d’uso e collegamenti a post di blog su AI Assistant.
