---
title: Note pre-release di Experience Platform
description: Un’anteprima delle ultime note sulla versione di Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: b8c257ad9ab4e7ee085687f6c03cf55d7fb83ef0
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 34%

---

# Note preliminari su Adobe Experience Platform

>[!IMPORTANT]
>
>Questo documento è destinato ad essere **anteprima** delle note sulla versione per il mese corrente. Gli elementi da rilasciare sono soggetti a modifiche e possono essere aggiunti o rimossi nella versione finale.

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/latest)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: febbraio 2026**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Avvisi](#alerts)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Servizio Query Service](#query-service)
- [Origini](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator consente di creare e distribuire agenti basati sull’intelligenza artificiale in grado di automatizzare i flussi di lavoro e interagire con i clienti su più canali.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Agente di onboarding dei dati | Utilizza Data Onboarding Agent per configurare le connessioni di origine, convalidare la qualità dei dati, applicare l’arricchimento semantico, rivedere e convalidare gli schemi ed eseguire l’acquisizione dei dati. Segui i flussi di lavoro passo per passo sia per i flussi B2C che per i flussi B2B, rivedi gli output previsti e risolvi i problemi comuni. |
| Agente Data Distiller | Utilizzare Data Distiller Agent per creare processi SQL dal linguaggio naturale, ottimizzare le prestazioni SQL, ripristinare gli errori SQL, pianificare e gestire processi SQL e monitorare lo stato dei processi. Per iniziare, controlla le protezioni, le autorizzazioni necessarie e le linee guida per la risoluzione dei problemi. |
| Agente di raccolta dati | Utilizza l’agente di raccolta dati per ottenere indicazioni contestuali per configurazioni di raccolta dati complesse e per esplorare la derivazione, le dipendenze e le relazioni tra gli oggetti di raccolta dati tramite approfondimenti sulla conversazione. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [documentazione di Agent Orchestrator](https://experienceleague.adobe.com/it/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Avvisi {#alerts}

Experience Platform consente di iscriverti agli avvisi basati su eventi per varie attività di Experience Platform. È possibile abbonarsi a diverse regole di avviso tramite la scheda [!UICONTROL Alerts] nell&#39;interfaccia utente di Experience Platform e scegliere di ricevere messaggi di avviso all&#39;interno dell&#39;interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Integrazione di [!DNL Slack] per gli avvisi rivolti al cliente | È ora possibile inviare avvisi rivolti al cliente a [!DNL Slack]. Segui il tutorial per configurare l&#39;integrazione di [!DNL Slack] e ricevere notifiche di avviso direttamente nell&#39;area di lavoro di [!DNL Slack]. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [[!DNL Observability Insights] panoramica](../observability/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform Data Collection fornisce un set di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli all’Edge Network di Adobe Experience Platform e ad altre destinazioni.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Gestione estensione tag per piattaforma Adobe | Utilizza la nuova funzionalità di gestione delle estensioni per caricare, creare pacchetti e rilasciare le estensioni della tua organizzazione per la distribuzione pubblica, privata e di sviluppo. Nella vista aziendale di livello superiore, puoi trovare estensioni private condivise insieme alle estensioni di tua proprietà. Questa funzione supporta le estensioni web, edge e mobili. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [documentazione sulla raccolta dati](https://experienceleague.adobe.com/en/docs/experience-platform/collection/home).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| Batch [!DNL Snowflake] generalmente disponibile | La destinazione del batch [!DNL Snowflake] è stata spostata nella disponibilità generale. Ora puoi visualizzare la colonna ID del criterio di unione nei dati esportati insieme alle colonne esistenti, ad esempio marca temporale, attributi di mappatura e iscrizione al pubblico. |
| Supporto della crittografia AES256 per [destinazioni Amazon S3](../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) | Ora puoi configurare la crittografia AES256 per le esportazioni Amazon S3. Scegli tra due opzioni: <ul><li>**[!UICONTROL Default]**: Experience Platform crittografa i dati inattivi con l&#39;algoritmo di crittografia predefinito impostato sul bucket.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform aggiunge l&#39;intestazione `s3:x-amz-server-side-encryption": "AES256` all&#39;esportazione e crittografa i dati inattivi con l&#39;algoritmo AES256 quando arriva in S3. **Questa opzione ha la precedenza su qualsiasi algoritmo di crittografia predefinito configurato nel bucket S3**.</li></ul> |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Organizzazione e ricerca dell’inventario degli schemi | La pagina di navigazione dello schema ora include funzioni avanzate di ricerca e filtro, azioni in linea e supporto di tag e cartelle definiti dall’utente. Questi aggiornamenti semplificano la ricerca, l’organizzazione e la gestione degli schemi nelle sandbox, riducendo al contempo il lavoro di navigazione e manutenzione manuale. |

Per ulteriori informazioni, consulta la [[!DNL XDM] panoramica](../xdm/home.md).

## Query Service {#query-service}

Il servizio Query Service consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal [!DNL Data Lake] e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire nel profilo cliente in tempo reale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Allineamento della data annuale di reimpostazione del calcolo di Data Distiller (versione limitata) | Le ore di calcolo annuali di Data Distiller ora vengono reimpostate alla data dell’anniversario del contratto con Data Distiller, in base al momento in cui la licenza è stata acquistata o rinnovata. In questo modo i rapporti sull’utilizzo delle licenze vengono allineati ai termini del contratto e possono risultare in un adeguamento una tantum ai valori di utilizzo correnti. |
| Gestione delle sessioni di Data Distiller (versione limitata) | In qualità di amministratore autorizzato, puoi visualizzare e gestire sessioni attive di Query Service e Data Distiller all’interno della tua organizzazione e sandbox tramite l’interfaccia utente di. Utilizza la gestione delle sessioni per identificare le sessioni inattive e terminarle per liberare capacità. Le protezioni integrate impediscono di terminare le sessioni con query attive. La funzione registra tutte le azioni di rimozione per il controllo e avvisa gli utenti interessati. Per accedere a questa funzionalità è necessaria l&#39;autorizzazione **Gestisci sessioni query**. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [Panoramica di Query Service](../query-service/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Origini nuove o aggiornate**

| Origine | Descrizione |
| --- | --- |
| Supporto di Unity Catalog nel connettore di origine [!DNL Databricks] | Il connettore di origine [!DNL Databricks] ora supporta Unity Catalog. Leggi la documentazione aggiornata di [[!DNL Databricks]](../sources/connectors/databases/databricks.md) per scoprire come utilizzare Unity Catalog quando configuri la connessione di origine. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../sources/home.md).
