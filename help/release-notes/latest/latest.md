---
title: Note sulla versione di Adobe Experience Platform - Aprile 2026
description: Note sulla versione di aprile 2026 per Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 9ebf498257378f4c5002276a84f104cf2d337601
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 22%

---

# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/latest)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: 28 aprile 2026**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Servizio Query Service](#query-service)
- [Real-Time CDP](#rtcdp)
- [Sandbox](#sandboxes)
- [Origini](#sources)

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Visualizzare i dettagli della build | Ora puoi accedere alle build e ai dettagli della build da una libreria o da un ambiente per visualizzare la build attualmente live e ispezionarne il contenuto (estensioni, elementi dati e regole). Per ulteriori informazioni, vedere [Panoramica delle build](../../tags/ui/publishing/builds.md#build-details). |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [Panoramica sulla raccolta dati](../../tags/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con le piattaforme di destinazione. Utilizza le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} [Corrispondenza cliente Microsoft Ads](../../destinations/catalog/advertising/microsoft-ads-customer-match.md) | Abbina i clienti per indirizzo e-mail e interagisci nuovamente con loro in [!DNL Microsoft Advertising Network], inclusi gli annunci Search&amp;Audience. Collega il tuo account [!DNL Microsoft Advertising] a Real-Time CDP per automatizzare la creazione e la gestione degli elenchi di corrispondenze dei clienti direttamente da Experience Platform. Per ottenere l’accesso, contatta il tuo account manager Adobe. |
| [!BADGE Beta]{type=Informative} [Modifica pubblico personalizzato](../../destinations/catalog/advertising/reddit-custom-audience.md) | Invia tipi di pubblico da Experience Platform a [!DNL Reddit Ads]. Connetti il tuo account [!DNL Reddit], mappa le identità e attiva i tipi di pubblico per raggiungere le persone che esplorano attivamente i loro interessi su [!DNL Reddit]. |
| [Amazon Ads v2](../../destinations/catalog/advertising/amazon-ads-v2.md) | Utilizza la scheda [!DNL Amazon Ads v2] per tutte le nuove connessioni [!DNL Amazon Ads]. [!DNL Amazon Ads v2] si connette a [!DNL Ads Data Manager], che fornisce supporto per tipi di identità espansi, campi relativi all&#39;indirizzo e condivisione di dati tra i prodotti [!DNL Amazon Ads], migliorando il targeting e le percentuali di corrispondenza del pubblico. Il connettore [!DNL Amazon Ads] esistente nel catalogo è stato rinominato in [(Legacy) [!DNL Amazon Ads]](../../destinations/catalog/advertising/amazon-ads.md). Se disponi di una connessione legacy esistente, questa continua a funzionare senza le modifiche necessarie. |
| [[!DNL Rokt]](../../destinations/catalog/advertising/rokt.md) | Utilizza [!DNL Rokt] per connettere il pubblico di Experience Platform a decisioni in tempo reale basate sull&#39;intelligenza artificiale, migliorando le prestazioni della campagna tramite targeting, eliminazione e personalizzazione più precisi. |
| [Connessione Pubblico Acxiom](../../destinations/catalog/advertising/acxiom-audience-connection.md) | La destinazione [!DNL Acxiom Audience Connection] è ora generalmente disponibile. Utilizzalo per migliorare i tipi di pubblico con la tecnologia [!DNL Acxiom's Real ID] e attivali in [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], [!DNL Cox], [!DNL Facebook], [!DNL Amazon], [!DNL Pinterest], [!DNL Vizio], [!DNL LG Ads], [!DNL Spectrum] e [!DNL Viant]. |
| [Connessione pubblico Acxiom Real ID](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | La destinazione [!DNL Acxiom Real ID Audience Connection] è ora generalmente disponibile. Utilizzalo per attivare i tipi di pubblico utilizzando [!DNL Acxiom's Real ID] come chiave di corrispondenza in [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], [!DNL Cox], [!DNL Facebook], [!DNL Amazon], [!DNL Pinterest], [!DNL Vizio], [!DNL LG Ads], [!DNL Spectrum] e [!DNL Viant]. |

{style="table-layout:auto"}

**Correzioni e miglioramenti**

| Correggi | Descrizione |
| --- | --- |
| Nuova colonna `TS` per [destinazioni Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) | La destinazione [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) ora include una colonna timestamp `TS` nella tabella condivisa, che indica quando è stato eseguito l&#39;ultimo aggiornamento di ogni riga. Questo aggiornamento verrà introdotto entro la fine di aprile. |
| Monitoraggio del supporto per [destinazioni Personalization](../../destinations/catalog/personalization/custom-personalization.md) personalizzate | Il [flusso di dati esegue la pagina](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) ora mostra le metriche per [destinazioni Personalization](../../destinations/catalog/personalization/custom-personalization.md) personalizzate. In precedenza, queste metriche non erano disponibili per questo tipo di destinazione. Utilizzali per verificare che il pubblico si stia attivando come previsto e per diagnosticare i problemi. <br> ![Il flusso di dati esegue le metriche visualizzate per una destinazione Personalization personalizzata, mostrando le identità attivate, escluse e non riuscite.](../2026/assets/april/dataflow-run-custom-personalization.png "Il flusso di dati esegue le metriche per le destinazioni Personalization personalizzate."){zoomable="yes"} |
| Conteggi dei profili nel passaggio di revisione del flusso di lavoro di attivazione | Il passaggio di revisione del flusso di lavoro di attivazione ora mostra i conteggi dei profili per i tipi di pubblico già attivati. Vengono visualizzati anche i conteggi dei profili per [destinazioni di streaming](../../destinations/ui/activate-segment-streaming-destinations.md), non solo [destinazioni batch](../../destinations/ui/activate-batch-profile-destinations.md). <br> ![I conteggi dei profili visualizzati nel passaggio di revisione del flusso di lavoro di attivazione per i tipi di pubblico già attivati e in streaming.](../2026/assets/april/profile-count-review.png "Conteggi profili nel passaggio di revisione del flusso di lavoro di attivazione."){zoomable="yes"} |
| Visibilità scadenza token [!DNL Pinterest] | Nella destinazione [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md) viene ora visualizzata la data di scadenza del token, in modo da poter vedere quando è necessaria la riautenticazione. [!DNL Pinterest] token scadono ogni 30 giorni. Alla scadenza di un token, le esportazioni di dati cessano di funzionare. Per evitare interruzioni, [aggiorna le credenziali di autenticazione](../../destinations/catalog/advertising/pinterest.md#refresh-authentication-credentials) prima della scadenza del token. |
| Il file di esportazione è ora disabilitato per le pianificazioni scadute | Quando la pianificazione del pubblico è scaduta, **[!UICONTROL Export file now]** è disabilitato prima di tentare di utilizzarlo e una descrizione del comando ne spiega il motivo. In precedenza, la selezione dell’azione generava un errore. <br> ![L&#39;azione Esporta file ora è disabilitata con una descrizione comando che spiega perché l&#39;azione non è disponibile.](../2026/assets/april/export-file-now-disabled.png "Azione Esporta file ora disabilitata."){zoomable="yes"} |
| Correzione della visibilità delle colonne nel flusso di lavoro di attivazione | È stato risolto un problema a causa del quale la modifica delle colonne visibili in una tabella influiva in modo errato su altre tabelle nel flusso di lavoro di attivazione. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti All’Utilizzo E All’Individuazione Dei Gruppi Di Campi | Visualizza gli schemi che utilizzano un gruppo di campi e accedi ai metadati, come classi compatibili, attributi obbligatori ed etichette di governance, direttamente nell’interfaccia utente. Puoi anche filtrare i gruppi di campi in base alla compatibilità tra classi e ai tag di settore per individuare in modo più efficiente le risorse rilevanti e valutare l’impatto prima di apportare modifiche. Per ulteriori dettagli, consulta la [guida Esplora gruppi di campi](../../xdm/ui/explore.md#explore-field-groups.md). |

Per ulteriori informazioni, consulta la [panoramica su XDM](../../xdm/home.md).

## Servizio Query Service {#query-service}

Utilizzare Query Service per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake] con SQL standard. Unisci qualsiasi set di dati da [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o nell&#39;acquisizione in Real-Time Customer Profile.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Gestione delle sessioni di Query Service | Visualizzare e terminare le sessioni attive di Query Service dalla scheda [!UICONTROL Admin] per monitorare l&#39;utilizzo e la capacità della sessione inattiva. In questo modo gli amministratori possono mantenere flussi di lavoro affidabili per Data Distiller recuperando la capacità dalle sessioni inattive. Per ulteriori dettagli, consulta la [Guida alle sessioni di Gestione servizio query](../../query-service/ui/session-management.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [Panoramica di Query Service](../../query-service/home.md).

## Real-Time CDP {#rtcdp}

Real-Time CDP fornisce profili cliente unificati e actionable acquisendo, elaborando e attivando i dati su più canali in tempo reale. Con Real-Time CDP, le organizzazioni possono collegare origini di dati esistenti, creare e attivare tipi di pubblico avanzati e garantire l’attivazione conforme alla privacy tra le destinazioni, il tutto dall’interno di Experience Platform. In questo modo esperti di marketing, analisti e team IT possono offrire esperienze altamente personalizzate e tempestive ai clienti attraverso campagne di marketing dirette e multicanale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Real-Time CDP MCP (Beta) | Utilizza [Real-Time CDP MCP](../../rtcdp/rtcdp-mcp.md) per inserire Real-Time CDP negli agenti di intelligenza artificiale e nei client compatibili con MCP, consentendo di interagire direttamente con gli strumenti di Real-Time CDP tramite l&#39;esperienza LLM nativa. Collegando un client compatibile con MCP (ad esempio Claude, ChatGPT, Claude Code, Codex, Cursor o VS Code) all’endpoint fornito dal rappresentante Adobe, puoi utilizzare il linguaggio naturale per controllare il pubblico, la configurazione della destinazione e la cronologia delle esecuzioni di attivazione, senza scrivere chiamate REST API di Experience Platform o navigare in più flussi di lavoro dell’interfaccia utente. Dopo aver completato l’accesso a Adobe basato su browser, potrai accedere in sola lettura a diversi strumenti, tra cui: <ul><li>Cerca tipi di pubblico esistenti</li><li>Anteprima iscrizione pubblico</li><li>Elenca tipi di destinazione</li><li>Elenca account configurati</li><li>Elenco delle destinazioni configurate</li><li>Elencare connessioni Source</li><li>Elenca connessioni di destinazione</li><li>Controlla esecuzioni di attivazione</li></ul>. Ogni richiesta richiede `imsOrgId` e `sandboxName` parametri per garantire che le azioni abbiano l&#39;ambito della tua organizzazione e sandbox. **Nota**: le operazioni di scrittura non sono supportate in questa versione di Beta. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [panoramica di Real-Time CDP](../../rtcdp/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Express Copy | Utilizza la funzione Copia rapida per copiare gli oggetti in una sandbox di destinazione in un&#39;unica azione dall&#39;[interfaccia utente strumenti sandbox](/help/sandboxes/ui/sandbox-tooling.md#express-copy). Gli oggetti dipendenti vengono rilevati automaticamente e vengono creati nella sandbox di destinazione o riutilizzati quando esistono già. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [panoramica sulle sandbox](../../sandboxes/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Origini nuove o aggiornate**

| Origine | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.One] | L&#39;[[!DNL Talon.One] origine](../../sources/connectors/loyalty/talon-one.md) per Experience Platform è ora disponibile sia in modalità batch che in modalità streaming. Utilizza [[!DNL Talon.One Batch Source Connector]](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) per acquisire periodicamente sessioni chiuse e transazioni fedeltà cronologiche e l&#39;origine [[!DNL Talon.One Streaming Events]](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) per portare [!DNL Talon.One] eventi in Experience Platform quasi in tempo reale. Insieme, semplificano il caricamento e l&#39;attivazione dei dati fedeltà [!DNL Talon.One] in Real-Time CDP, Adobe Journey Optimizer e Offer Decisioning. |
| Supporto del filtro a livello di riga per [!DNL Salesforce] tramite SOQL | È ora possibile applicare [!DNL Salesforce] filtri SOQL (Object Query Language) direttamente nelle connessioni di origine [!DNL Salesforce], consentendo di limitare i dati a livello di riga prima che vengano acquisiti in Experience Platform. Utilizza la funzionalità per: <ul><li>Definisci le condizioni di stile della clausola WHERE SOQL sugli oggetti Salesforce (ad esempio, solo lead con E-mail != null o opportunità in fasi specifiche)</li><li>Limita l’acquisizione alle sole righe che soddisfano i tuoi criteri, riducendo gli spostamenti di dati, l’archiviazione e l’elaborazione a valle non necessari</li><li>Allinea più strettamente l’acquisizione di Experience Platform con le tue regole di accesso e conformità dei dati CRM, controllando quali record vengono introdotti in Experience Platform all’origine</li></ul>. Per ulteriori informazioni, leggere la guida sul filtro a livello di riga [&#x200B; per le origini](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).

<!--

| Data Distiller Accelerators | Run and schedule Adobe-managed, parameterized SQL templates in the Query Service UI to perform common analyses without writing SQL. This helps you standardize analytics workflows and reuse trusted query logic across your organization. See the [Data Distiller accelerators guide](../../query-service/ui/accelerators.md) for more details. |

| Automatic dataflow disabling | Sources ingestion dataflows that fail continuously for 30 days are automatically disabled, helping to surface unhealthy dataflows and reduce repeated failed runs. |

--->