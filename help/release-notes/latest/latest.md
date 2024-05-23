---
title: Note sulla versione di Adobe Experience Platform - Maggio 2024
description: Note sulla versione di Adobe Experience Platform di maggio 2024.
source-git-commit: e02892a2cbf5f65a1b9a0eec49722896bd061084
workflow-type: tm+mt
source-wordcount: '1596'
ht-degree: 20%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: mercoledì 21 maggio 2024**

>[!TIP]
>
>Il [Documentazione API di Experienci Platform](https://developer.adobe.com/experience-platform-apis/) è ora interattivo. Esplora gli endpoint API direttamente dalle pagine della documentazione per ottenere un feedback immediato e velocizzare l’implementazione tecnica. [Ulteriori informazioni](#interactive-api-documentation) sulle nuove funzionalità.

Aggiornamenti alle funzioni esistenti in Experienci Platform:

- [Servizio catalogo](#catalog-service)
- [Dashboard](#dashboards)
- [Governance dei dati](#governance)
- [Destinazioni](#destinations)
- [Servizio query](#query-service)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

Altri aggiornamenti in Adobe Experience Platform:

- [Aggiornamenti alla documentazione](#documentation-updates)

## Servizio catalogo {#catalog-service}

Catalog Service è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Mentre tutti i dati acquisiti in Experienci Platform vengono memorizzati nel data lake come file e directory, Catalog contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca e monitoraggio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Azioni in blocco | L’inventario dei set di dati ora supporta azioni in blocco. Semplifica i processi di gestione dei dati e assicurati la gestione efficiente dei set di dati con azioni in blocco. Utilizza le azioni in blocco per risparmiare tempo eseguendo più azioni contemporaneamente su numerosi set di dati.  Le azioni in blocco includono [Sposta nella cartella](../../catalog/datasets/user-guide.md#move-to-folders), [Modifica tag](../../catalog/datasets/user-guide.md#manage-tags), e [Elimina](../../catalog/datasets/user-guide.md#delete) set di dati. <br> ![Azioni in blocco nell’area di lavoro dell’interfaccia utente Set di dati.](../2024/assets/may/bulk-actions.png "Azioni in blocco nell’area di lavoro dell’interfaccia utente Set di dati."){width="100" zoomable="yes"} <br> Per ulteriori informazioni su questa funzione, leggere [Guida all’interfaccia utente dei set di dati](../../catalog/datasets/user-guide.md#bulk-actions). |

{style="table-layout:auto"}

## Dashboard {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Approfondimenti personalizzabili per reporting esteso dell’app | Senza soluzione di continuità [transizione dell&#39;output dell&#39;analisi SQL in formati visivi comprensibili e facili da usare](../../dashboards/data-distiller/customizable-insights/overview.md). Utilizza query SQL personalizzate per una manipolazione precisa dei dati e la creazione di grafici dinamici da diversi set di dati strutturati. È possibile utilizzare la modalità query pro per eseguire analisi complesse con SQL e quindi condividere questa analisi con utenti non tecnici tramite grafici nel dashboard personalizzato o esportarli in file CSV. |

{style="table-layout:auto"}

## Governance dei dati {#governance}

La governance dei dati di Adobe Experience Platform è una serie di strategie e tecnologie utilizzate per gestire i dati della clientela e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave in [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo degli accessi ai dati per le azioni di marketing.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto mTLS per destinazioni API HTTP e azioni personalizzate Adobe Journey Optimizer | Rafforzare la fiducia dei clienti con le misure di sicurezza rafforzate del protocollo Mutual Transport Layer Security (mTLS). Il [Experience Platform di destinazione API HTTP](../../destinations/catalog/streaming/http-destination.md#mtls-protocol-support) e [Azioni personalizzate Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) ora supporta il protocollo mTLS per l’invio di dati agli endpoint configurati. Per attivare mTLS non è necessaria alcuna configurazione aggiuntiva nella destinazione dell’azione personalizzata o dell’API HTTP. Questo processo si verifica automaticamente quando viene rilevato un endpoint abilitato per mTLS. È possibile [scarica il certificato pubblico di Adobe Journey Optimizer qui](../../landing/governance-privacy-security/encryption.md#download-certificates) e [Certificato pubblico del servizio destinazioni qui](../../landing/governance-privacy-security/encryption.md#download-certificates).<br>Consulta la [Experience Platform di documentazione sulla crittografia dei dati](../../landing/governance-privacy-security/encryption.md#mtls-protocol-support) per ulteriori informazioni sui protocolli di connessione di rete durante l&#39;esportazione di dati in sistemi di terze parti. |

{style="table-layout:auto"}

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Riordina i campi di mappatura per le destinazioni batch | Ora puoi modificare l’ordine delle colonne nelle esportazioni CSV trascinando e rilasciando i campi di mappatura nella sezione [passaggio di mappatura](../../destinations/ui/activate-batch-profile-destinations.md#mapping). L’ordine dei campi mappati nell’interfaccia utente si riflette nell’ordine delle colonne nel file CSV esportato, dall’alto verso il basso, con la riga in alto che corrisponde alla colonna più a sinistra nel file CSV. <br> ![Visualizzazione della modalità di riordinamento delle mappature.](../2024/assets/may/reorder-mappings.gif "Visualizzazione della modalità di riordinamento delle mappature."){width="100" zoomable="yes"} |
| Programmi di esportazione predefiniti preselezionati per le destinazioni batch | Experienci Platform ora imposta automaticamente una pianificazione predefinita per ogni esportazione di file. Consulta la documentazione su [programmazione delle esportazioni del pubblico](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) per informazioni su come modificare la pianificazione predefinita. |
| Modificare più pianificazioni di attivazione del pubblico per le destinazioni batch | Ora puoi modificare la pianificazione di attivazione per più tipi di pubblico esportati in destinazione batch (basata su file) dalla sezione **[!UICONTROL Dati di attivazione]** scheda di [pagina dei dettagli della destinazione](../../destinations/ui/destination-details-page.md#bulk-edit-schedule). <br> ![Visualizzare come selezionare più tipi di pubblico e modificare la pianificazione dell’esportazione dei file.](../2024/assets/may/bulk-edit-schedule.gif "Visualizzare come selezionare più tipi di pubblico e modificare la pianificazione dell’esportazione dei file."){width="100" zoomable="yes"} |
| Esportare più tipi di pubblico on-demand in destinazioni batch | Ora puoi selezionare ed esportare più tipi di pubblico in destinazioni batch, tramite [esportazione di file on-demand](../../destinations/ui/export-file-now.md) funzionalità. |

{style="table-layout:auto"}

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Servizio query {#query-service}

Il Servizio query consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform.[!DNL Data Lake] Puoi unire qualsiasi set di dati da [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’acquisizione in Real-time Customer Profile.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Editor legacy obsoleto | L’editor legacy è obsoleto e non è più accessibile per l’utilizzo. Al suo posto, puoi utilizzare [funzioni avanzate dell’editor di query](../../query-service/ui/user-guide.md#query-authoring) per scrivere, convalidare ed eseguire le query. |
| Ritardo esecuzione query | Tieni sotto controllo le ore di calcolo impostando avvisi per eventuali ritardi nell’esecuzione delle query. È possibile scegliere di ricevere avvisi se lo stato di una query non cambia dopo un determinato periodo di tempo. È sufficiente impostare il tempo di ritardo desiderato nell’interfaccia utente di Platform per rimanere informati sull’avanzamento della query. Per informazioni su come impostare questo avviso nell’interfaccia utente, consulta [documentazione pianificazioni query](../../query-service/ui/query-schedules.md#alerts-for-query-status) o [guida alle azioni di query in linea](../../query-service/ui/monitor-queries.md#query-run-delay). |
| Inventario semplificato dei registri di query | È ora possibile migliorare l’efficienza nella risoluzione dei problemi e nel monitoraggio delle attività grazie a [interfaccia utente semplificata dei registri di query](../../query-service/ui/query-logs.md#filter-logs): <ul><li> Per impostazione predefinita, l’interfaccia utente di Platform ora esclude tutte le &quot;Query di sistema&quot; dalla scheda dei registri. </li><li> Visualizzare le query di sistema deselezionando **Escludere le query di sistema**. </li></ul> <br> ![Scheda Registri nell’area di lavoro dell’interfaccia utente Query.](../2024/assets/may/query-log.png "Scheda Registri nell’area di lavoro dell’interfaccia utente Query."){width="100" zoomable="yes"} <br> Utilizza l’interfaccia utente semplificata dei registri di query per una visualizzazione più dettagliata che consente di identificare e analizzare rapidamente i registri rilevanti. |
| Selettore database | Utilizza il nuovo menu a discesa del selettore del database per [accesso comodo alle visualizzazioni dati di Customer Journey Analytics da Power BI o Tableau](../../query-service/ui/credentials.md#connect-to-customer-journey-analytics). Ora puoi selezionare il database desiderato direttamente dall’interfaccia utente di Platform per un’integrazione più semplice degli strumenti di business intelligence. <br> ![Scheda Credenziali nell’area di lavoro dell’interfaccia utente Query.](../2024/assets/may/database-selector.png "Scheda Credenziali nell’area di lavoro dell’interfaccia utente Query."){width="100" zoomable="yes"} <br> |

{style="table-layout:auto"}

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] consente di segmentare i dati memorizzati in [!DNL Experience Platform] che si riferiscono ai singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in tipi di pubblico. Puoi creare tipi di pubblico tramite definizioni di segmenti o altre origini dai tuoi dati di [!DNL Real-Time Customer Profile]. Questi tipi di pubblico sono configurati e gestiti centralmente in [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione Adobe.

**Funzione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Importare tipi di pubblico generati esternamente | L’importazione di tipi di pubblico generati esternamente ora richiede l’autorizzazione &quot;Import audience&quot; (Importa pubblico). Per ulteriori informazioni sulle autorizzazioni, consulta [guida all’interfaccia utente per le autorizzazioni](../../access-control/home.md#permissions). |

{style="table-layout:auto"}

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experienci Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Autenticazione credenziali client OAuth2 per [!DNL Salesforce] sorgente | È ora possibile utilizzare le credenziali client OAuth2 per autenticare [!DNL Salesforce] account su Experience Platform. Leggi le [!DNL Salesforce] sorgente [Guida API](../../sources/tutorials/api/create/crm/salesforce.md) e [Guida all’interfaccia utente](../../sources/tutorials/ui/create/crm/salesforce.md) per ulteriori informazioni. |
| Supporto per un flusso di dati di esempio per [!DNL Marketo Engage] sorgente | Il [!DNL Marketo Engage] l’origine ora supporta i flussi di dati di esempio. Abilita la configurazione del flusso di dati di esempio per limitare il tasso di acquisizione, quindi prova le funzioni di Experience Platform senza dover acquisire grandi quantità di dati. Per ulteriori informazioni, consulta la guida su [creazione di un flusso di dati per [!DNL Marketo Engage] nell’interfaccia utente](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |
| Aggiornamenti all’elenco consentiti dell’indirizzo IP | A seconda della posizione, è necessario aggiungere un set di nuovi indirizzi IP all’elenco consentiti per utilizzare correttamente le origini di streaming. Per un elenco completo dei nuovi indirizzi IP, leggi [Guida all’elenco consentiti dell’indirizzo IP](../../sources/ip-address-allow-list.md). |

{style="table-layout:auto"}

**Documentazione nuova o aggiornata**

| Documentazione aggiornata | Descrizione |
| --- | --- |
| Aggiornamenti alla documentazione per [!DNL Google PubSub] | Il [!DNL Google PubSub] la documentazione di origine è stata aggiornata con una guida completa ai prerequisiti. Utilizza la nuova sezione prerequisiti per scoprire come creare l’account di servizio, concedere autorizzazioni a livello di argomento o di abbonamento e impostare configurazioni per ottimizzare l’utilizzo di [!DNL Google PubSub] sorgente. Leggi le [[!DNL Google PubSub] panoramica](../../sources/connectors/cloud-storage/google-pubsub.md) per ulteriori informazioni. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, leggere [panoramica sulle origini](../../sources/home.md).

## Aggiornamenti alla documentazione {#documentation-updates}

### Documentazione API di Experience Platform interattivo {#interactive-api-documentation}

Il [Documentazione API di Experienci Platform](https://developer.adobe.com/experience-platform-apis/) è ora interattivo. Tutte le pagine di riferimento API ora dispongono di un **Prova** .funzionalità che puoi utilizzare per testare le chiamate API direttamente sulla pagina del sito web della documentazione. [Ottieni le credenziali di autenticazione richieste](/help/landing/api-authentication.md) e inizia a utilizzare la funzionalità per esplorare gli endpoint API.

Utilizza questa nuova funzionalità per esplorare le richieste e le risposte dagli endpoint API, per ottenere feedback immediati e velocizzare l’implementazione tecnica. Ad esempio, visita il [API del servizio Identity](https://developer.adobe.com/experience-platform-apis/references/identity-service/) o [API del registro dello schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) endpoint per esplorare il nuovo **Prova** nella barra a destra.

![Registrazione schermata che mostra una chiamata API effettuata direttamente dal sito web della documentazione.](../2024/assets/may/api-playground-demo.gif)

>[!CAUTION]
>
>Tieni presente che utilizzando la funzionalità API interattiva nelle pagine della documentazione, stai effettuando chiamate API reali agli endpoint. Tieni presente questo aspetto durante la sperimentazione con le sandbox di produzione.

### Approfondimenti personalizzati e coinvolgimento {#personalized-insights-engagement}

Una nuova pagina di documentazione del caso d’uso end-to-end per [evoluzione del valore una tantum rispetto al valore a vita](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md) è ora live. Leggi questa documentazione per scoprire come utilizzare Real-Time CDP e Adobe Journey Optimizer per convertire i visitatori sporadici nelle tue proprietà web ai clienti fedeli.
