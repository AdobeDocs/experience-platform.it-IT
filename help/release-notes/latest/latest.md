---
title: Note sulla versione di Adobe Experience Platform - Aprile 2025
description: Note sulla versione di Adobe Experience Platform di aprile 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6558046e9708267cd0ceda36e7c0bdba6b2f758a
workflow-type: ht
source-wordcount: '2192'
ht-degree: 100%

---

# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: 29 aprile 2025**

Aggiornamenti alle funzioni e alla documentazione esistenti di Adobe Experience Platform:

- [Experience League](#experience-league)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Experience Data Model](#xdm)
- [Identity Service](#identity)
- [Query Service](#query-service)
- [Profilo cliente in tempo reale](#profile)
- [Sandbox](#sandboxes)
- [Origini](#sources)
- [Playbook di casi d’uso](#use-case-playbooks)

## Experience League {#experience-league}

Experience League è una piattaforma di apprendimento completa progettata per aiutarti ad acquisire ulteriori competenze con i prodotti Adobe. Offre una varietà di risorse, tra cui: corsi, documentazione, pagine della community, eventi e accesso alle certificazioni.

| Funzione | Descrizione |
| --- | --- |
| Pagina Home personalizzata | Accedi e personalizza la tua pagina Home su [Experience League](https://experienceleague.adobe.com/it/home#). Accedi con le credenziali Adobe, quindi seleziona **[!UICONTROL Experience League]** dal menu principale e inizia a ottimizzare la tua esperienza di apprendimento: <ul><li>**Segnalibri**: utilizza la funzione [!UICONTROL Segnalibri] per salvare e raccogliere le tue risorse preferite in un’unica posizione. Puoi salvare una vasta gamma di contenuti, tra cui playlist, articoli e tutorial.</li><li>**Personalizza l’apprendimento**: per migliorare la tua esperienza di apprendimento, aggiorna il tuo profilo Experience League indicando i ruoli, i settori, i prodotti e il livello di esperienza che meglio corrispondono alle tue esigenze.</li><li>**Consigli**: visualizza i contenuti di apprendimento consigliati in base alle tue attività più recenti.</li><li>**Visualizzato di recente**: utilizza la sezione [!UICONTROL Visualizzato di recente] per tornare rapidamente ai contenuti visualizzati di recente, ad esempio documentazione e video.</li><li>**Risorse di apprendimento**: utilizza il pannello [!UICONTROL Tutte le risorse di apprendimento] per accedere a tutorial, documentazione, community, eventi e certificazioni.</li><li>**Novità**: visualizza la sezione [!UICONTROL Novità] per uno stream dei contenuti più recenti in Experience League.</li><li>**Guarda eventi passati on-demand**: guarda le registrazioni di precedenti eventi in live streaming su prodotti, casi d’uso e tutorial, accessibili dalla sezione [!UICONTROL Guarda eventi passati on-demand].</li></ul><br> ![Pagina Home personalizzata su Experience League.](../2025/assets/april/personalized-home-page.png "Pagina Home personalizzata su Experience League."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Estensione [!DNL Adform] | L’estensione [!DNL Adform] lato server consente ai brand di eseguire facilmente il retargeting del pubblico all’esterno del sito utilizzando identificatori ECID. Questa estensione lato server non dipende da cookie di terze parti o da ID alternativi dei cookie. Inoltre, poiché questa operazione viene eseguita interamente lato server, non sono necessari pixel aggiuntivi o altre modifiche lato client. Per ulteriori informazioni, consulta [Panoramica dell’estensione Adform](/help/tags/extensions/server/adform/overview.md). |
| Estensione API per eventi web [!DNL Amazon] | L’estensione API per conversioni [!DNL Amazon] consente all’inserzionista di condividere interazioni con il sito web direttamente con [!DNL Amazon], per una migliore attribuzione, affidabilità dei dati e ottimizzazione delle campagne. Questa estensione supporta l’inoltro degli eventi, che consente di inviare eventi di conversione come acquisti, aggiunte al carrello e altri ancora, garantendo inoltre la deduplica corretta per dati di reporting accurati. Per ulteriori informazioni, consulta la [Panoramica dell’estensione Amazon](/help/tags/extensions/server/amazon/overview.md). |

{style="table-layout:auto"}

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| --- | --- |
| [Marketo Engage Person Sync](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe ha aggiornato la destinazione [!DNL Marketo Engage Person Sync] per risolvere un problema che si verificava se erano presenti più e-mail nella mappa delle identità. |
| [(V2) Connessione Pega CDH Realtime Audience](/help/destinations/catalog/personalization/pega-v2.md) | Utilizza la destinazione [!DNL (V2) Pega Customer Decision Hub Realtime Audience] in Adobe Experience Platform per inviare a Pega Customer Decision Hub gli attributi del profilo e i dati sull’iscrizione del pubblico, per prendere decisioni sulle prossime azioni migliori, quando nel tuo account Pega sono configurate più applicazioni Pega Customer Decision Hub. |

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| --- | --- |
| Opzioni di pianificazione **Settimanale** e **Mensile** per esportazioni di file completi | Ora puoi pianificare l’esportazione di file completi per un pubblico di persone o potenziali clienti su base settimanale o mensile, per l’attivazione in destinazioni basate su file in archiviazione cloud. [Ulteriori informazioni](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) sulle opzioni di pianificazione. |

{style="table-layout:auto"}

**Correzioni, miglioramenti e altri annunci** {#destinations-fixes-and-enhancements}

- **L’applicazione di una data di fine per l’esportazione dei set di dati è stata posticipata al 1° settembre 2025**\
  Con la [versione di settembre 2024](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality), Adobe aveva annunciato che il 1° maggio 2025 sarebbe divenuta la data di fine predefinita per tutti i flussi di dati di esportazione di set di dati creati *prima di tale versione*. Adobe sta ora estendendo questa scadenza dell’imposizione al **1° settembre 2025** per concedere ai clienti più tempo per aggiornare le proprie pianificazioni. Per informazioni su come modificare la data di fine di un flusso di dati di esportazione di set di dati, consulta la sezione sulla pianificazione nel [tutorial su come esportare un set di dati](../../destinations/ui/export-datasets.md#schedule-dataset-export).

- **È stata migliorata la gestione dei trasferimenti SFTP non riusciti per LiveRamp Onboarding**\
  Adobe ha implementato una correzione per un problema che interessa le esportazioni di file nella destinazione [LiveRamp Onboarding ](/help/destinations/catalog/advertising/liveramp-onboarding.md) tramite SFTP. A volte, i trasferimenti di file non riuscivano a causa di problemi transitori lato server e i file temporanei da tentativi non riusciti rimanevano sul server. Questi file non eliminabili bloccavano i tentativi successivi, in quanto Adobe non disponeva dell’autorizzazione per sovrascriverli.\
  Con questa correzione, se con un nuovo tentativo non è possibile eliminare il file temporaneo, Adobe genera un nuovo file con suffisso `attempt2` affinché il nuovo tentativo possa essere completato correttamente.

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Componenti XDM aggiornati**

| Funzione | Descrizione |
| --- | --- |
| I campi stringa ricevono un valore minimo di uno | Per impostazione predefinita, ai nuovi campi stringa viene assegnata una lunghezza minima pari a uno. I valori nulli per i campi non obbligatori sono ancora accettabili. Per ulteriori informazioni sulle best practice, consulta la guida sulle [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md#data-integrity-tips) |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Experience Platform, consulta la [panoramica del sistema XDM](../../xdm/home.md).

## Identity Service {#identity}

Utilizza Identity Service di Adobe Experience Platform per creare una panoramica completa della clientela e del relativo comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali ed efficaci in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Disponibilità limitata]{type=Informative} [!DNL Identity Graph Linking Rules] Le regole di collegamento del grafo identità sono ora accessibili a tutta la clientela nelle sandbox di sviluppo. <ul><li>**Requisiti per l’attivazione**: la funzione rimarrà inattiva finché non avrai configurato e salvato [!DNL Identity Settings]. Senza questa configurazione, il sistema continuerà a funzionare normalmente, senza cambiamenti di comportamento.</li><li>**Note importanti**: durante questa fase di disponibilità limitata, la segmentazione Edge può produrre risultati imprevisti di appartenenza al segmento. Tuttavia, la segmentazione in streaming e in batch funzionerà come previsto.</li><li>**Passaggi successivi**: per informazioni su come abilitare questa funzione nelle sandbox di produzione, contatta il team Adobe Account.</li></ul> |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [[!DNL Identity Graph Linking Rules] documentazione](../../identity-service/identity-graph-linking-rules/overview.md).

## Query Service {#query-service}

Eseguire query sui dati nel data lake di Adobe Experience Platform utilizzando SQL standard con Query Service. Combina facilmente i set di dati e generane nuovi dai risultati delle query per alimentare il reporting, i flussi di lavoro data science o facilitare l’acquisizione nel profilo cliente in tempo reale. Ad esempio, puoi unire i dati di transazione della clientela con i dati comportamentali per identificare tipi di pubblico ad alto valore per campagne di marketing mirate.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Sovrascrittura SQL per tipi di pubblico | Aggiorna l’appartenenza al pubblico sovrascrivendo i profili esistenti con i risultati di una nuova query SQL. Questo consente di gestire in modo più efficiente i tipi di pubblico dinamici, rimuovendo i record obsoleti e inserendo quelli aggiornati in un’unica operazione. Per ulteriori informazioni, consulta la [guida dell’estensione SQL per tipi di pubblico](../../query-service/data-distiller-audiences/overview.md#replace-audience). |
| Scaricare e copiare i risultati delle query | [Scarica i risultati delle query direttamente dall’editor di query](../../query-service/ui/overview.md#download-query-results) come file CSV, XLSX o JSON, oppure [copia i risultati negli Appunti](../../query-service/ui/overview.md#copy-results) come valori delimitati da virgole (CSV) per utilizzarli rapidamente in applicazioni per fogli di calcolo come Excel. Questi miglioramenti semplificano l’analisi offline, il reporting e i flussi di lavoro di convalida dei dati. |
| Visualizzare i risultati delle query a schermo intero | [Visualizza in anteprima i risultati delle query in una finestra di dialogo a schermo intero](../../query-service/ui/overview.md#view-results) per migliorare la leggibilità, analizzare facilmente set di dati di grandi dimensioni e selezionare le righe da copiare. La visualizzazione a schermo intero offre un layout a griglia ridimensionabile che consente di controllare tabelle di grandi dimensioni e un output dettagliato in modo più efficiente. |
| Selezione avanzata delle colonne nella modellazione predittiva | Seleziona colonne specifiche e applica alias utilizzando la sintassi `model_predict` estesa. Recupera i risultati predittivi intermedi, ad esempio i vettori di caratteristiche e i punteggi di probabilità. La selezione avanzata richiede l’attivazione di un flag di funzione. Per esempi di sintassi e dettagli sul flag di funzione, consulta la [documentazione sul ciclo di vita del modello](../../query-service/advanced-statistics/models.md#select-specific-output-fields). |
| Salvare gli output di modellazione predittiva utilizzando CREATE TABLE e INSERIT INTO | [Per salvare gli output di modellazione predittiva selezionati come nuove tabelle, utilizza CREATE TABLE AS SELECT; per inserirli in tabelle esistenti, utilizza INSERT INTO SELECT](../../query-service/advanced-statistics/models.md#predict). Se è abilitata la selezione avanzata delle colonne, i risultati intermedi come i vettori di caratteristiche e le probabilità possono anche essere salvati insieme alle previsioni finali. Per esempi di utilizzo, consulta la [documentazione sulla sintassi SQL](../../query-service/sql/syntax.md#create-table-as-select). |

Per ulteriori informazioni su [!DNL Query Service], consulta la [[!DNL Query Service] panoramica](../../query-service/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati clienti in una visualizzazione unificata che offre un account utilizzabile e dotato di marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Scadenza dati profilo identificato da pseudonimo | Gestisci la scadenza dei dati di profili identificati da pseudonimo nella dashboard Profilo. Per ulteriori informazioni su questa funzione e sui profili identificati da pseudonimi, consulta la [Guida alla scadenza dei dati del profilo identificato da pseudonimo](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sul profilo cliente in tempo reale, leggi la [panoramica sul profilo](../../profile/home.md)

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per rispondere a questa esigenza, Experience Platform fornisce sandbox che permettono di suddividere una singola istanza di Experience Platform in ambienti virtuali separati, utili per lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto ampliato per il plug-in degli strumenti sandbox | Ora puoi copiare le azioni personalizzate come oggetto dipendente durante la duplicazione di oggetti Percorso negli strumenti sandbox. Inoltre, puoi selezionare le azioni esistenti da riutilizzare nella sandbox di destinazione. Possono anche essere aggiunte a un pacchetto in modo indipendente. Per informazioni complete sugli oggetti Adobe Journey Optimizer supportati, leggi la guida sugli [strumenti della sandbox](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle sandbox, consulta la [panoramica sulle sandbox](../../sandboxes/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Nuove origini**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | L’origine [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md) è ora disponibile. Utilizza questa origine per portare in Experience Platform i dati di affinità dei profili utente [!DNL Algolia]. Puoi quindi utilizzare questi dati per migliorare il coinvolgimento degli utenti, i tassi di conversione e l’esperienza complessiva del cliente, fornendo soluzioni di ricerca ad alte prestazioni per siti web, piattaforme e-commerce e applicazioni. Per ulteriori informazioni, consulta la guida su come [acquisire [!DNL Algolia User Profiles]  i dati in Experience Platform](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md). |
| [!BADGE Beta]{type=Informative} Supporto API per [!DNL Azure Databricks] | L’origine [!DNL Azure Databricks] è ora disponibile nell’API. Utilizza l’API [!DNL Flow Service] per connettere il tuo account [!DNL Databricks] e portare in Experience Platform i dati [!DNL Databricks]. Per ulteriori informazioni, consulta la documentazione su [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md). |

{style="table-layout:auto"}

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Sono stati aggiornati i campi XDM per acquisire in Experience Platform i dati di contenuti in streaming. | Il nuovo gruppo di campi XDM `mediaReporting` è ora disponibile per acquisire in Experience Platform i dati di contenuti in streaming tramite l’origine Adobe Analytics. Questo campo sostituisce il campo `media.mediaTimed`.</br> <br>Durante un periodo di transizione di tre mesi, resterà disponibile l’acquisizione dei dati mediante i campi `media.mediaTimed`. Tuttavia, alla fine di luglio 2025, i campi `media.mediaTimed` diventeranno obsoleti e non saranno più visibili nell’interfaccia utente dello schema di Experience Platform e i dati verranno inviati solo mediante i campi `mediaReporting`.</br><br>Se hai implementato l’origine Analytics per raccogliere in Platform i dati di contenuti in streaming prima del 22 aprile 2025, devi migrare le configurazioni esistenti per inviare i dati utilizzando il nuovo gruppo di campi. Tale migrazione deve essere completata entro la fine di luglio 2025. Per assistenza sulla migrazione, contatta il team Adobe Account . |
| Nuovi tipi di autenticazione per [!DNL MariaDB] e [!DNL PostgreSQL] | Ora puoi utilizzare l’autenticazione di base per autenticare le origini [!DNL MariaDB] e [!DNL PostgreSQL] in Experience Platform. Per ulteriori informazioni, consulta la documentazione seguente: <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| Supporto per filtro a livello di riga per [!DNL Amazon Redshift] | Puoi utilizzare le funzionalità di filtro a livello di riga per i dati [!DNL Amazon Redshift] in Experience Platform. Per ulteriori informazioni, consulta la guida su come [filtrare i dati a livello di riga per le origini nell’API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).

## Playbook di casi d’uso {#use-case-playbooks}

I playbook di casi d’uso sono stati originariamente progettati come supporto per superare eventuali difficoltà quando si inizia a utilizzare Real-Time Customer Data Platform o Adobe Journey Optimizer. Con la loro continua evoluzione, ora consentono di affrontare rapidamente casi d’uso chiave per le attività di marketing e forniscono spunti e risorse predefinite per le fasi di test e passaggio alla produzione.

I playbook di casi d’uso sono passati da uno strumento di esplorazione a un framework di collaborazione. Ora ti aiutano a creare, gestire e condividere i tuoi playbook tra organizzazioni diverse.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} Authoring e condivisione dei playbook | Un nuovo framework per l’authoring di playbook consente di creare, gestire e condividere i playbook di casi d’uso. Questo include il supporto per l’acquisizione dei metadati chiave, la modifica delle mappe dei percorsi e l’associazione delle risorse tecniche pertinenti. Puoi condividere i playbook tra organizzazioni diverse per standardizzare gli approcci di marketing e promuovere la coerenza. |

{style="table-layout:auto"}

Per scoprire come creare e condividere i tuoi playbook, leggi il documento [Authoring e condivisione dei playbook](/help/use-case-playbooks/playbooks/author.md).

Per ulteriori informazioni, leggi la [Panoramica sui playbook di casi d’uso](/help/use-case-playbooks/playbooks/overview.md): descrive le funzionalità e lo scopo dei playbook, e fornisce una dimostrazione completa, che illustra come creare istanze e importare in altri ambienti sandbox le risorse generate.
