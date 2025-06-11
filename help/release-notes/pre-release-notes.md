---
title: Note pre-release di Experience Platform
description: Un’anteprima delle ultime note sulla versione di Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: c34c41d384fbc4f309dffa8bba97a0f6f3468efc
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 42%

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

**Data di rilascio: giovedì 18 giugno 2025**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Controllo degli accessi](#access-control)
- [Gestione avanzata del ciclo di vita dei dati](#advanced-data-lifecycle-management)
- [Dashboard](#dashboards)
- [Governance dei dati](#data-governance)
- [Destinazioni](#destinations)
- [Composizione di pubblico federato](#fac)
- [Privacy Service](#privacy-service)
- [Query Service](#query-service)
- [Sandbox](#sandboxes)
- [Origini](#sources)

## Controllo degli accessi {#access-control}

Experience Platform sfrutta i profili di prodotto [Adobe Admin Console](https://adminconsole.adobe.com) per collegare gli utenti con autorizzazioni e sandbox. Le autorizzazioni controllano l’accesso a diverse funzionalità di Experience Platform, tra cui la modellazione di dati, la gestione dei profili e l’amministrazione della sandbox.

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Esporta autorizzazione per i dati del dashboard | Le opzioni **[!UICONTROL Scarica CSV]** e **[!UICONTROL Invia come messaggio e-mail]** nei dashboard ora richiedono l&#39;autorizzazione **[!UICONTROL Esporta dati dashboard]**. Questa autorizzazione garantisce che solo gli utenti autorizzati possano esportare dati insight tabulati, supportando regole di governance e criteri di controllo dell’accesso ai dati più rigidi. |

Per ulteriori informazioni, vedere la [panoramica sul controllo degli accessi](../access-control/home.md).

## Gestione avanzata del ciclo di vita dei dati {#advanced-data-lifecycle-management}

Experience Platform offre una suite di funzionalità di igiene dei dati che ti consentono di gestire i dati archiviati tramite l’eliminazione programmatica di record e set di dati del consumatore. Utilizzando l’area di lavoro del ciclo di vita dei dati nell’interfaccia utente o tramite chiamate all’API di igiene dei dati, puoi gestire in modo efficace gli archivi di dati. Usa queste funzionaità per garantire che le informazioni vengano utilizzate come previsto, che vengano aggiornate quando è necessario correggere dati scorretti e che vengano eliminate quando i criteri organizzativi lo ritengono necessario.

**Nuova documentazione**

| Nuova documentazione | Descrizione |
| --- | --- |
| Record Elimina disponibilità generale | Ora puoi eliminare singoli record in base ai campi di identità utilizzando l’interfaccia utente o l’API. Questa funzione consente di ridurre lo storage, applicare la governance e migliorare l’igiene dei dati consentendo le eliminazioni da un singolo set di dati o tra tutti i set di dati. Si applicano limiti di volume e requisiti di adesione. |

Per ulteriori informazioni, leggi la [panoramica sulla gestione avanzata del ciclo di vita dei dati](../hygiene/home.md).

## Dashboard {#dashboards}

Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Opzione Invia come esportazione e-mail | Ora puoi esportare fino a 10.000 record dai dashboard in modalità Query Pro selezionando **[!UICONTROL Invia come e-mail]** dal menu **[!UICONTROL Visualizza altro]**. Questa opzione invia in modo sicuro un collegamento per il download all’e-mail associata ad Adobe per esportazioni più grandi. |

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../dashboards/home.md).

## Governance dei dati {#data-governance}

La governance dei dati di Adobe Experience Platform è una serie di strategie e tecnologie utilizzate per gestire i dati della clientela e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave all’interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo degli accessi ai dati per le azioni di marketing.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Inserire nell&#39;elenco Consentiti Configurazione di avvisi CMK di Azure e IP | Ora puoi inserire nell&#39;elenco Consentiti l’indirizzo IP statico di Adobe nell’Insieme di credenziali delle chiavi di Azure per garantire l’accesso continuo quando sono abilitate le restrizioni di rete. Questo aiuta a evitare interruzioni dei servizi Platform dovute a restrizioni nell’accesso alle chiavi. |
| Avvisi e risoluzioni di configurazione CMK | Experience Platform ora attiva gli avvisi quando i servizi Adobe perdono l’accesso all’insieme di credenziali delle chiavi di Azure (ad esempio, a causa di voci di elenco Consentiti IP rimosse o di chiavi disabilitate). Una nuova guida ti aiuta a comprendere ogni avviso e ad intraprendere azioni correttive. |

Per ulteriori informazioni, consulta la [panoramica sulla governance dei dati](../data-governance/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| --- | --- |
| Segmenti utente Algolia | La destinazione Segmenti utente Algolia consente ai professionisti del marketing di distribuire personalizzazioni coerenti tra i siti dalla home page alla ricerca. Crea tipi di pubblico avanzati da più origini di dati e condividili tra vari canali per migliorare le strategie di targeting e la personalizzazione delle campagne. |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Informazioni sulla scadenza dell&#39;account LinkedIn | Le informazioni sulla scadenza dell&#39;account per le destinazioni di LinkedIn sono ora disponibili direttamente nelle visualizzazioni [!UICONTROL Sfoglia] e [!UICONTROL Account]. In precedenza, queste informazioni erano disponibili solo nella documentazione. Questo miglioramento fornisce una migliore visibilità sullo stato di autenticazione e sulla gestione delle credenziali di LinkedIn. |
| Google Customer Match + DV360 disponibilità generale e miglioramento | La destinazione Google Customer Match + DV360 è ora disponibile per tutti gli utenti di Experience Platform. La documentazione ora include istruzioni dettagliate per il collegamento dell’account tra gli account pubblicitari di Adobe e Google. |
| Supporto della crittografia di destinazione DLZ (Data Landing Zone) | È stato aggiunto il supporto per la crittografia della destinazione Data Landing Zone. È ora possibile allegare chiavi pubbliche in formato RSA per aggiungere la crittografia ai file esportati. |
| Monitoraggio a livello di pubblico per le destinazioni aziendali | Il monitoraggio a livello di pubblico è ora disponibile per le seguenti destinazioni Enterprise: [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [[!DNL HTTP API]](/help/destinations/catalog/streaming/http-destination.md), [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [Panoramica sulle destinazioni](../destinations/home.md).

## Composizione di pubblico federato {#fac}

La composizione di pubblico federato consente alle aziende di comporre i dati per un migliore utilizzo in vari casi d’uso. Con questo nuovo approccio, in qualità di utente di Adobe Real-Time Customer Data Platform e/o di Adobe Journey Optimizer, puoi federare i set di dati direttamente dal data warehouse esistente per creare e arricchire i tipi di pubblico e gli attributi di Adobe Experience Platform in un unico sistema.

| Nuova funzionalità | Descrizione |
| ----------- | ----------- |
| Funzionalità di preparazione HIPAA | La Federated Audience Composition è ora compatibile con HIPAA. Per ulteriori informazioni sulle misure di privacy e sicurezza di Federated Audience Composition, leggi [privacy e sicurezza in Panoramica di Federated Audience Composition](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/start/privacy-security). Per ulteriori informazioni sulla conformità HIPAA per i prodotti Experience Platform in generale, leggere la [Panoramica su prodotti e servizi HIPAA e Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Per ulteriori informazioni, consulta la [documentazione sulla composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Nuove normative legali e organizzative danno agli utenti il diritto di accedere ai propri dati personali o di cancellarli dagli archivi dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente per aiutarti a gestire le richieste di dati dalla clientela. Con [!DNL Privacy Service] puoi inviare richieste di accesso e cancellare dati della clientela personali o privati dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Supporto per le leggi sulla privacy in Tennessee e Minnesota | Privacy Service ora supporta il Tennessee Information Protection Act (`tipa_tn_usa`) e il Minnesota Consumer Data Privacy Act (`mcdpa_mn_usa`). Puoi elaborare le richieste di accesso ed eliminazione in conformità a queste nuove normative a livello di stato. Per ulteriori dettagli, consulta la [Panoramica sulle normative](https://experienceleague.adobe.com/it/docs/experience-platform/privacy/regulations/overview). |

Per ulteriori informazioni sul servizio, consulta la [panoramica di Privacy Service](../privacy-service/home.md).

## Query Service {#query-service}

Eseguire query sui dati nel data lake di Adobe Experience Platform utilizzando SQL standard con Query Service. Combina facilmente i set di dati e generane di nuovi dai risultati delle query per abilitare i rapporti, i flussi di lavoro della scienza dei dati o facilitare l’acquisizione nel profilo cliente in tempo reale.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Funzioni statistiche avanzate | **Intersezione di sketch theta**: nuova funzione per calcolare le intersezioni dei set utilizzando gli schizzi theta per operazioni di conteggio e impostazione valori univoci approssimativi. **Istogrammi KLL**: sono state migliorate le funzionalità degli istogrammi utilizzando schizzi KLL (Kth small, L large, Elementi grandi) per la stima quantile e l&#39;analisi della distribuzione. Queste funzioni sono disponibili per i clienti di Data Distiller. |
| Libreria modelli SQL | È ora disponibile una libreria completa di modelli SQL per i casi d’uso comuni. Questa funzione accelera lo sviluppo delle query fornendo modelli di best practice per pattern di analisi frequenti, consentendo ai clienti di Data Distiller di implementare analisi complesse in modo più efficiente. |

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Esempio di modellazione RFM | È stato aggiunto un esempio completo di modellazione Recency, Frequency, Monetary (RFM) per i clienti Data Distiller. Include documentazione dettagliata e guide all’implementazione per la segmentazione del cliente e l’analisi del valore utilizzando le tecniche RFM. |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Query Service], consulta la [[!DNL Query Service] panoramica](../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Migrazione degli aggiornamenti della configurazione degli oggetti | Dopo la replica iniziale, è ora possibile eseguire la migrazione degli aggiornamenti della configurazione di oggetti iterativi tra sandbox. Questo miglioramento supporta i flussi di lavoro di sviluppo in cui le configurazioni devono essere aggiornate e propagate tra gli ambienti senza ricreare l’intera configurazione sandbox. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle sandbox, consulta la [panoramica sulle sandbox](../sandboxes/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per il nuovo tipo di autenticazione per [!DNL Azure Synapse Analytics] | [!DNL Azure Synapse Analytics] supporterà ora anche l&#39;autenticazione dell&#39;entità servizio, oltre all&#39;autenticazione della stringa di connessione esistente. |

**Aggiornamenti importanti per l&#39;autenticazione**

| Aggiornamento | Descrizione |
| --- | --- |
| [!DNL Salesforce] Autenticazione di base obsoleta | L’autenticazione di base per Salesforce CRM e Salesforce Service Cloud diventerà obsoleta entro gennaio 2026. I clienti devono effettuare la migrazione all’autenticazione OAuth 2.0 per mantenere la connettività. Questa modifica interessa entrambi i connettori di origine e garantisce una maggiore sicurezza e conformità agli standard di autenticazione di Salesforce. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [Panoramica sulle origini](../sources/home.md).
