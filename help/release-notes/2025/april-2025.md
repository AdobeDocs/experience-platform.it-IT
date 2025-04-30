---
title: Note sulla versione di Adobe Experience Platform - Aprile 2025
description: Note sulla versione di Adobe Experience Platform di aprile 2025.
exl-id: a3b1e2e8-d780-4e23-b323-37e1a631f716
source-git-commit: 65e0f0f98006f55bc08ccf24499841413def7a16
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 26%

---

# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: mercoledì 29 aprile 2025**

Aggiornamenti alle funzioni e alla documentazione esistenti di Adobe Experience Platform:

- [Experience League](#experience-league)
- [Destinazioni](#destinations)
- [Experience Data Model](#xdm)
- [Identity Service](#identity)
- [Query Service](#query-service)
- [Profilo cliente in tempo reale](#profile)
- [Origini](#sources)
- [Playbook di casi d’uso](#use-case-playbooks)

## Experience League {#experience-league}

Experience League è una piattaforma di apprendimento completa progettata per aiutarti a migliorare le tue competenze con i prodotti Adobe. Offre una varietà di risorse, tra cui: corsi, documentazione, pagine della community, eventi e accesso alle certificazioni.

| Funzione | Descrizione |
| --- | --- |
| Home page personalizzata | Accedi e personalizza la tua home page personalizzata in [Experience League](https://experienceleague.adobe.com/en/home#). Accedi con le tue credenziali Adobe, quindi seleziona **[!UICONTROL Experience League]** dal menu principale per iniziare a ottimizzare la tua esperienza di apprendimento: <ul><li>**Segnalibri**: utilizza la funzionalità [!UICONTROL Segnalibri] per salvare e raccogliere le risorse preferite in un&#39;unica posizione. È possibile salvare una vasta gamma di contenuti, tra cui playlist, articoli e tutorial.</li><li>**Personalizza il tuo apprendimento**: migliora la tua esperienza di apprendimento aggiornando il tuo profilo Experience League con i ruoli, i settori, i prodotti e il livello di esperienza più adatti alle tue esigenze.</li><li>**Consigli**: visualizza i contenuti di apprendimento consigliati in base all&#39;attività recente.</li><li>**Visualizzato di recente**: utilizza la sezione [!UICONTROL Visualizzato di recente] per tornare rapidamente al contenuto visualizzato di recente, ad esempio documentazione e video.</li><li>**Risorse di apprendimento**: utilizza il pannello [!UICONTROL Tutte le risorse di apprendimento] per accedere a tutorial, documentazione, community, eventi e certificazioni.</li><li>**Novità**: visualizza la sezione [!UICONTROL Novità] per un flusso dei contenuti più recenti su Experience League.</li><li>**Guarda gli eventi passati on-demand**: guarda i flussi live registrati in precedenza su faretti di prodotto, casi d&#39;uso e tutorial con la sezione [!UICONTROL Guarda gli eventi passati on-demand].</li></ul><br> ![Home page personalizzata su Experience League.](../2025/assets/april/personalized-home-page.png "Home page personalizzata in Experience League."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| --- | --- |
| [Sincronizzazione persona Marketo Engage](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe ha aggiornato la destinazione [!DNL Marketo Engage Person Sync] per risolvere un problema che interessava i clienti quando erano presenti più e-mail nella mappa delle identità. |
| [(V2) Connessione pubblico in tempo reale Pega CDH](/help/destinations/catalog/personalization/pega-v2.md) | Utilizza la destinazione [!DNL (V2) Pega Customer Decision Hub Realtime Audience] in Adobe Experience Platform per inviare gli attributi del profilo e i dati sull&#39;iscrizione del pubblico a Pega Customer Decision Hub per prendere decisioni ottimali, quando nel tuo account Pega sono configurate più applicazioni Pega Customer Decision Hub. |

**Funzionalità nuova o aggiornata** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| --- | --- |
| Opzioni di pianificazione **Settimanale** e **Mensile** per esportazioni di file complete | È ora possibile pianificare l’esportazione di file completi per utenti e potenziali tipi di pubblico su base settimanale o mensile quando si attivano destinazioni basate su file nell’archiviazione cloud. [Ulteriori informazioni](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) sulle opzioni di pianificazione. |

{style="table-layout:auto"}

**Correzioni, miglioramenti e altri annunci** {#destinations-fixes-and-enhancements}

- **L&#39;applicazione delle date di fine dell&#39;esportazione del set di dati è stata posticipata al 1° settembre 2025**\
  Come parte della versione [di settembre 2024](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality), Adobe ha impostato una data di fine predefinita del 1° maggio 2025 per tutti i flussi di dati di esportazione del set di dati creati *prima di tale versione*. Adobe sta ora estendendo questa scadenza di imposizione al **1 settembre 2025** per fornire ai clienti più tempo per aggiornare le pianificazioni. Per informazioni su come modificare la data di fine di un flusso di dati per l&#39;esportazione di un set di dati, fare riferimento alla sezione di pianificazione dell&#39;esercitazione [esporta set di dati](../../destinations/ui/export-datasets.md#schedule-dataset-export).

- **È stata migliorata la gestione dei trasferimenti SFTP non riusciti per l&#39;onboarding di LiveRamp**\
  Adobe ha implementato una correzione per un problema che influisce sulle esportazioni di file nella destinazione [Onboarding LiveRamp](/help/destinations/catalog/advertising/liveramp-onboarding.md) tramite SFTP. A volte, i trasferimenti di file non sono riusciti a causa di problemi transitori lato server e i file temporanei da tentativi non riusciti sono rimasti sul server. Questi file non eliminabili hanno bloccato i tentativi successivi, in quanto Adobe non disponeva dell’autorizzazione per sovrascriverli.\
  Con la correzione, se un nuovo tentativo non riesce a eliminare il file temporaneo, Adobe genererà un nuovo file con suffisso aggiunto ,`attempt2`, per garantire che il nuovo tentativo venga completato correttamente.

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Componenti XDM aggiornati**

| Funzione | Descrizione |
| --- | --- |
| I campi stringa ricevono un valore minimo di uno | Per impostazione predefinita, ai nuovi campi stringa viene assegnata una lunghezza minima pari a uno. I valori Null per i campi non obbligatori sono ancora accettabili. Per ulteriori informazioni sulle best practice, consulta la guida sulle [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md#data-integrity-tips) |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Experience Platform, consulta la [panoramica del sistema XDM](../../xdm/home.md).

## Identity Service {#identity}

Utilizza Identity Service di Adobe Experience Platform per creare una panoramica completa della clientela e del relativo comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali ed efficaci in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Disponibilità limitata]{type=Informative} [!DNL Identity Graph Linking Rules] | Le regole di collegamento del grafico identità ora sono a disponibilità limitata e sono accessibili a tutti i clienti nelle sandbox di sviluppo. <ul><li>**Requisiti per l&#39;attivazione**: la funzionalità rimarrà inattiva finché non avrai configurato e salvato [!DNL Identity Settings]. Senza questa configurazione, il sistema continuerà a funzionare normalmente, senza cambiamenti di comportamento.</li><li>**Note importanti**: durante questa fase di disponibilità limitata, la segmentazione di Edge può produrre risultati imprevisti di iscrizione al segmento. Tuttavia, lo streaming e la segmentazione batch funzioneranno come previsto.</li><li>**Passaggi successivi**: per informazioni su come abilitare questa funzione nelle sandbox di produzione, contatta il team del tuo account di Adobe.</li></ul> |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [[!DNL Identity Graph Linking Rules] documentazione](../../identity-service/identity-graph-linking-rules/overview.md).

## Query Service {#query-service}

Eseguire query sui dati nel data lake di Adobe Experience Platform utilizzando SQL standard con Query Service. Combina facilmente i set di dati e generane nuovi dai risultati delle query per alimentare il reporting, i flussi di lavoro data science o facilitare l’acquisizione nel profilo cliente in tempo reale. Ad esempio, puoi unire i dati di transazione della clientela con i dati comportamentali per identificare tipi di pubblico ad alto valore per campagne di marketing mirate.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Sovrascrittura del pubblico SQL | Aggiorna l’iscrizione al pubblico sovrascrivendo i profili esistenti con i risultati di una nuova query SQL. Questo consente di gestire in modo più efficiente i tipi di pubblico dinamici rimuovendo i record obsoleti e inserendo quelli aggiornati in un’unica operazione. Per ulteriori informazioni, vedere la [Guida dell&#39;estensione del pubblico SQL](../../query-service/data-distiller-audiences/overview.md#replace-audience). |
| Scaricare e copiare i risultati della query | [Scarica i risultati della query direttamente dall&#39;editor query](../../query-service/ui/overview.md#download-query-results) come file CSV, XLSX o JSON oppure [copia i risultati negli Appunti](../../query-service/ui/overview.md#copy-results) come valori delimitati da virgole (CSV) per un utilizzo rapido in applicazioni per fogli di calcolo come Excel. Questi miglioramenti semplificano l’analisi offline, il reporting e i flussi di lavoro di convalida dei dati. |
| Visualizzare i risultati della query a schermo intero | [La query di anteprima genera una finestra di dialogo a schermo intero](../../query-service/ui/overview.md#view-results) per migliorare la leggibilità, analizzare facilmente set di dati di grandi dimensioni e selezionare le righe da copiare. La visualizzazione a schermo intero offre un layout a griglia ridimensionabile che consente di esaminare tabelle di grandi dimensioni e output dettagliato in modo più efficiente. |
| Selezione migliorata delle colonne nella previsione del modello | Selezionare colonne specifiche e applicare alias utilizzando la sintassi estesa `model_predict`. Recupera i risultati di previsione intermedi, ad esempio i vettori di funzionalità e i punteggi di probabilità. La selezione avanzata richiede l&#39;attivazione di un flag di funzione. Per esempi di sintassi e dettagli sui flag di funzionalità, consulta la [documentazione sul ciclo di vita del modello](../../query-service/advanced-statistics/models.md#select-specific-output-fields). |
| Salvare gli output di previsione del modello utilizzando CREATE TABLE e INSERT INTO | [Salvare gli output di previsione selezionati in nuove tabelle utilizzando CREATE TABLE AS SELECT o inserire nelle tabelle esistenti utilizzando INSERT INTO SELECT](../../query-service/advanced-statistics/models.md#predict). Se è abilitata la selezione avanzata delle colonne, i risultati intermedi come i vettori delle funzioni e le probabilità possono anche essere mantenuti insieme alle previsioni finali. Per esempi di utilizzo, consultare la [documentazione relativa alla sintassi SQL](../../query-service/sql/syntax.md#create-table-as-select). |

Per ulteriori informazioni su [!DNL Query Service], consulta la [[!DNL Query Service] panoramica](../../query-service/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati clienti in una visualizzazione unificata che offre un account utilizzabile e dotato di marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Scadenza dei dati del profilo pseudonimo | Gestisci la scadenza dei dati del profilo pseudonimo nel dashboard Profilo. Per ulteriori informazioni su questa funzione e sui profili identificati da pseudonimi, consulta la [Guida alla scadenza dei dati del profilo identificato da pseudonimo](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sul profilo cliente in tempo reale, leggi la [panoramica sul profilo](../../profile/home.md)

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Nuove origini**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | L&#39;origine [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md) è ora disponibile. Usa questa origine per portare i dati di affinità dei profili utente di [!DNL Algolia] ad Experience Platform. Puoi quindi utilizzare questi dati per migliorare il coinvolgimento degli utenti, i tassi di conversione e l’esperienza complessiva del cliente, fornendo soluzioni di ricerca ad alte prestazioni per siti web, piattaforme di e-commerce e applicazioni. Per ulteriori informazioni, consulta la guida su come [acquisire [!DNL Algolia User Profiles] dati in Experience Platform](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md). |
| Supporto API di [!BADGE Beta]{type=Informative} per [!DNL Azure Databricks] | L&#39;origine [!DNL Azure Databricks] è ora disponibile nell&#39;API. Utilizza l&#39;API [!DNL Flow Service] per connettere il tuo account [!DNL Databricks] e portare i tuoi dati di [!DNL Databricks] in Experience Platform. Per ulteriori informazioni leggere la documentazione su [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md). |

{style="table-layout:auto"}

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Sono stati aggiornati i campi XDM per l’acquisizione di dati Streaming Media in Experience Platform. | Il nuovo gruppo di campi XDM `mediaReporting` è ora disponibile per l&#39;acquisizione di dati Streaming Media in Experience Platform tramite l&#39;origine Adobe Analytics. Questo campo sostituisce il campo `media.mediaTimed`.</br> <br>Durante un periodo transitorio di tre mesi, l&#39;acquisizione dei dati nei campi `media.mediaTimed` continuerà. Tuttavia, alla fine di luglio 2025, i campi `media.mediaTimed` diventeranno completamente obsoleti e non saranno più visibili nell&#39;interfaccia utente dello schema di Experience Platform e i dati verranno inviati solo utilizzando i campi `mediaReporting`.</br><br>Se hai implementato l’origine Analytics per raccogliere i dati di Streaming Media in Platform prima del 22 aprile 2025, devi migrare le configurazioni esistenti per inviare i dati utilizzando il nuovo gruppo di campi. Questa migrazione deve essere completata entro la fine di luglio 2025. Contatta il team del tuo account Adobe per il supporto alla migrazione. |
| Nuovi tipi di autenticazione per [!DNL MariaDB] e [!DNL PostgreSQL] | È ora possibile utilizzare l&#39;autenticazione di base per autenticare le origini [!DNL MariaDB] e [!DNL PostgreSQL] in Experience Platform. Per ulteriori informazioni, consulta la seguente documentazione: <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| Supporto del filtro a livello di riga per [!DNL Amazon Redshift] | È possibile utilizzare funzionalità di filtro a livello di riga per i dati di [!DNL Amazon Redshift] in Experience Platform. Per ulteriori informazioni, leggere la guida su [filtrare i dati a livello di riga per le origini nell&#39;API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).

## Playbook di casi d’uso {#use-case-playbooks}

Use Case Playbooks were originally designed to help overcome challenges when getting started with Real-Time Customer Data Platform or Adobe Journey Optimizer. They continue to evolve, and now enable you to jumpstart key marketing use cases and provide inspiration and pre-built assets to test and move into production.

Use Case Playbooks have transitioned from a discovery tool into a collaborative framework. Ora ti aiutano a creare, gestire e condividere i tuoi playbook tra organizzazioni diverse.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} Author and share your own playbooks | Un nuovo Playbook Authoring Framework consente di creare, gestire e condividere playbook personalizzati per casi d’uso. Ciò include il supporto per l’acquisizione dei metadati chiave, la modifica delle mappe del percorso e l’associazione delle risorse tecniche pertinenti. Puoi condividere i playbook tra organizzazioni per standardizzare gli approcci di marketing e mantenere la coerenza. |

{style="table-layout:auto"}

Per scoprire come creare e condividere i tuoi playbook, leggi il documento [Autore e condividi i tuoi playbook](/help/use-case-playbooks/playbooks/author.md).

Per ulteriori informazioni, consulta la [Panoramica sui playbook di casi d&#39;uso](/help/use-case-playbooks/playbooks/overview.md), che fornisce una panoramica delle funzionalità dei playbook, del loro scopo e una dimostrazione end-to-end, tra cui come creare istanze e importare risorse generate in altri ambienti sandbox.