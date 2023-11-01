---
title: Note sulla versione di Adobe Experience Platform, novembre 2020
description: Note sulla versione di novembre 2020 per Adobe Experience Platform.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2179'
ht-degree: 11%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 11 novembre 2020**

Nuove funzioni di Adobe Experience Platform:

- [Migrazione di Adobe Experience Platform Data Lake](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Aggiornamenti alle funzioni esistenti:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] Servizio](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Migrazione di Adobe Experience Platform Data Lake {#migration}

Durante la migrazione del Data Lake da Adobe da Gen1 a Gen2, gli utenti saranno in grado di leggere dal Data Lake, ma saranno interessate tutte le funzionalità che scrivono nel Data Lake. L’Adobe contatterà gli amministratori di sistema per discutere in dettaglio l’impatto della migrazione e confermare le date e le ore di migrazione per organizzazioni specifiche.

Per ulteriori informazioni, leggere [Guida alla migrazione di Data Lake](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] sfrutta [Adobe Admin Console](https://adminconsole.adobe.com) profili di prodotto per collegare gli utenti con autorizzazioni e sandbox. Le autorizzazioni controllano l’accesso a diverse funzionalità di Platform, tra cui la modellazione di dati, la gestione dei profili e l’amministrazione delle sandbox.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Autorizzazioni | In [!DNL Admin Console], la scheda all’interno di una [!DNL Platform] profilo di prodotto consente di personalizzare quale [!DNL Platform] Le funzionalità di sono disponibili per gli utenti associati a tale profilo. Le categorie di autorizzazioni disponibili includono: **[!UICONTROL Modellazione dati]**, **[!UICONTROL Gestione dati]**, **[!UICONTROL Gestione profilo]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Monitoraggio dei dati]**, **[!UICONTROL Amministrazione sandbox]**, **[!UICONTROL Destinazioni]**, **[!UICONTROL Acquisizione dei dati]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Servizio query]**, e **[!UICONTROL Governance dei dati]**. |
| Accesso alle sandbox | Il **[!UICONTROL Autorizzazioni]** all’interno di una [!DNL Platform] il profilo di prodotto può concedere agli utenti l’accesso a specifiche sandbox. Consulta la sezione su [sandbox](#sandboxes) per ulteriori informazioni. |

Per ulteriori informazioni, vedere [panoramica sul controllo degli accessi](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] è un servizio applicativo integrato con [!DNL Experience Platform]. Consente di sfruttare [!DNL Platform] per offrire ai clienti l’offerta e l’esperienza migliore al momento giusto, in tutti i punti di contatto.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Libreria di offerte centralizzata | L’interfaccia in cui puoi creare e gestire i diversi elementi che compongono le offerte e definirne regole e vincoli. |
| Motore di decisione dell’offerta | Il motore delle decisioni per le offerte sfrutta [!DNL Platform] dati e [!DNL Real-Time Customer Profiles], insieme alla Libreria di offerte, per selezionare il momento giusto, i clienti e i canali a cui verranno consegnate le offerte. |

Per ulteriori informazioni, vedere [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=it) documentazione.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] è stata creata per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per rispondere a questa esigenza, [!DNL Experience Platform] fornisce sandbox che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Sandbox di produzione | [!DNL Experience Platform] fornisce una singola sandbox di produzione, che non può essere eliminata o reimpostata. Il numero totale di sandbox disponibili, di produzione e non di produzione, è determinato dalla licenza acquisita. |
| Sandbox non di produzione | È possibile creare più sandbox non di produzione per un singolo [!DNL Platform] che consente di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sulla sandbox di produzione. |
| Commutatore sandbox | In [!DNL Experience Platform] interfaccia utente, il selettore sandbox nell’angolo in alto a sinistra dello schermo consente di passare dalle sandbox disponibili attraverso un menu a discesa. Il selettore sandbox fornisce anche una funzione di ricerca che consente di filtrare tra le sandbox disponibili. |
| `x-sandbox-name` intestazione | Tutte le chiamate a [!DNL Experience Platform] Le API ora devono includere la nuova `x-sandbox-name` , il cui valore fa riferimento all&#39; `name` dell’ambiente sandbox in cui si svolgerà l’operazione. |

Per ulteriori informazioni, vedere [panoramica sulle sandbox](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Operazioni iterative | [!DNL Data Prep] Mapper ora supporta l&#39;esecuzione di operazioni iterative su una gerarchia. |
| Funzione mappatore | [!DNL Data Prep] Mapper ora ha la possibilità di **non** copia un attributo dall’origine nell’XDM di destinazione. |

Per ulteriori informazioni, vedere [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per creare informazioni approfondite dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di effettuare previsioni utilizzando i contenuti e le risorse di dati delle soluzioni Adobe. Uno dei modi in cui Data Science Workspace esegue questa operazione è tramite l’utilizzo di [!DNL JupyterLab]. [!DNL JupyterLab] è un’interfaccia utente basata su web per [[!DNL Project Jupyter]](https://jupyter.org/) ed è strettamente integrato con Adobe Experience Platform. Fornisce un ambiente di sviluppo interattivo con cui i data scientist possono lavorare [!DNL Jupyter] blocchi appunti, codice e dati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| [!DNL JupyterLab] Modello per la generazione di ricette | Aggiornamento dell’utilizzo e delle versioni dei requisiti da notebook a ricetta. [!DNL Python] L’immagine base di runtime ML è stata aggiornata per l’utilizzo [!DNL Python] 3.6.7 e a [!DNL Conda] esclusivamente l&#39;ambiente. |

Per ulteriori informazioni, leggere il documento [creazione di una ricetta con Jupyter Notebooks](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] Servizio {#destinations}

In entrata [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| Braze | Braze è una piattaforma completa per il coinvolgimento dei clienti che offre esperienze pertinenti e memorabili tra i clienti e i marchi che amano. |
| Microsoft Bing | La destinazione Microsoft Bing consente di eseguire campagne digitali di retargeting e targeting del pubblico in Microsoft Display Advertising. |
| Il Trade Desk | Trade Desk è una piattaforma self-service per consentire agli acquirenti di annunci di eseguire campagne digitali di retargeting e targeting del pubblico tra sorgenti di visualizzazione, video e inventario mobile. |

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Dettagli della destinazione Aggiornamenti UX | Il flusso di lavoro di destinazione di Real-Time CDP ora include il monitoraggio in linea che consente di vedere quali attivazioni batch sono state completate correttamente. Questa funzione consentirà agli utenti di risolvere i problemi direttamente nel flusso di lavoro per le destinazioni batch tramite avvisi e un dashboard di monitoraggio per tenere traccia degli errori nella pipeline di elaborazione. |
| Crittografia file | Per le destinazioni basate su file, gli utenti possono ora aggiungere la crittografia ai file esportati. |
| Pianificazione file | Per entrambe le destinazioni di archiviazione cloud e basata su e-mail, gli utenti possono creare un’esportazione una tantum o istantanee giornaliere. |
| Campi obbligatori | Gli utenti possono contrassegnare i campi come obbligatori, assicurandosi che vengano esportati solo i campi che contengono il campo obbligatorio. |

Per ulteriori informazioni, vedere [Panoramica sulle destinazioni](../../destinations/home.md).

## Intelligent Services {#intelligent-services}

I servizi intelligenti consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi di utilizzo dell’esperienza del cliente. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un’azienda utilizzando configurazioni a livello aziendale senza la necessità di competenze in materia di data science.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Set di dati di Consumer Experience Events (CEE) | La creazione di un set di dati CEE ora supporta l’aggiunta di campi di identità al set di dati con l’Editor schema. Attribution AI e IA per l’analisi dei clienti utilizzano l’identità primaria per la combinazione di eventi. |

Per ulteriori informazioni, leggere la sezione relativa a [aggiunta di campi di identità a un set di dati](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) nella guida alla preparazione dei dati di Intelligent Services.

### IA per l’attribuzione

Attribution AI, parte di Intelligent Services è un servizio di attribuzione algoritmica multicanale che calcola l’influenza e l’impatto incrementale delle interazioni dei clienti rispetto a risultati specifici.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Collegamento origine dati | Il collegamento all’origine del set di dati originale può essere visualizzato e spostato dalla barra a destra di un’istanza del servizio selezionata. |
| Modifica nome istanza | Ora puoi modificare il nome di un’istanza Attribution AI esistente. |
| Clona istanza | Copia la configurazione dell&#39;istanza del servizio attualmente selezionata e consente di apportare modifiche. |
| Modificare i parametri di configurazione dell&#39;istanza | Ora puoi modificare la configurazione di un’istanza Attribution AI esistente se non ha ancora iniziato il punteggio. |
| Punteggio unico | Ora puoi attivare il punteggio del modello ad hoc nelle istanze Attribution AI. |
| Colonne pass-through | Ora puoi configurare colonne aggiuntive da aggiungere ai file di punteggio di output non elaborati per aggiungere ulteriori dimensioni alle viste strumenti BI. |
| Attivazione e disattivazione dell’istanza | Ora puoi attivare e disattivare l’apprendimento del modello pianificato e il punteggio delle istanze di Attribution AI. |
| Tracciamento diritti | Puoi trovare la quantità totale di approfondimenti di attribuzione utilizzati dal tuo account nel contenitore crea istanza. |
| Suddivisione dei punti di contatto per posizione | Un nuovo grafico di approfondimenti che fornisce un’analisi dei punti di contatto in base alle posizioni del percorso di conversione. |
| Percorsi di conversione principali | Un nuovo grafico di approfondimenti si trova nella scheda Analisi del percorso. Il grafico contiene un elenco dei primi cinque percorsi di conversione che mostrano la sequenza dei punti di contatto del canale di marketing che hanno portato al maggior numero di conversioni. |
| Efficacia dei punti di contatto | Fornisce informazioni approfondite sulle tre variabili più importanti in base alle quali il modello misura l’efficacia dei punti di contatto. Le variabili sono il rapporto tra percorsi positivi e negativi toccati, l’efficienza del punto di contatto e il volume del punto di contatto. |

Per ulteriori informazioni, leggere [Panoramica di Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### IA per l’analisi dei clienti

IA per l’analisi dei clienti, parte di Intelligent Services offre agli esperti marketing la possibilità di generare previsioni sui clienti a livello individuale con spiegazioni. Con l’aiuto di fattori di influenza, IA per l’analisi dei clienti può dirti cosa potrebbe fare un cliente e perché. Inoltre, gli esperti marketing possono trarre vantaggio dalle previsioni e dalle informazioni di IA per l’analisi dei clienti per personalizzare le customer experience fornendo le offerte e i messaggi più appropriati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Collegamento origine dati | Il collegamento all’origine del set di dati originale può essere visualizzato e spostato dalla barra a destra di un’istanza del servizio selezionata. |
| Modifica nome istanza | Puoi modificare il nome di un’istanza di Customer AI esistente. |
| Modificare i parametri di configurazione dell&#39;istanza | Ora puoi modificare la configurazione di un’istanza di IA per l’analisi dei clienti esistente se non ha ancora avviato un punteggio. |
| Clona istanza | Copia la configurazione dell&#39;istanza del servizio attualmente selezionata e consente di apportare modifiche. |
| Tracciamento diritti | Puoi trovare la quantità totale di profili valutati da IA per l’analisi dei clienti per il tuo account nel contenitore crea istanza. |
| Obiettivo di previsione | La flessibilità nella creazione di un obiettivo di previsione è stata aumentata con nuove opzioni per prevedere se qualcosa &quot;si verificherà&quot; o &quot;non si verificherà&quot;. Inoltre, sono state aggiunte le opzioni per prevedere se &quot;tutti&quot; gli eventi si verificano o se &quot;uno qualsiasi&quot; degli eventi si verifica quando vengono utilizzati più eventi. |
| Espansione del fattore di influenza | I bucket dei fattori influenti principali della propensione ora contengono drill-down. I drill-down rappresentano un riepilogo più dettagliato dei valori per ciascuno dei principali fattori influenti all’interno di un bucket di propensione. |

Per ulteriori informazioni, leggere [Panoramica di Customer AI](../../intelligent-services/customer-ai/overview.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Flusso di lavoro dei criteri di unione aggiornato | Platform ha aggiornato la configurazione dei criteri di unione a un nuovo flusso di lavoro graduale. Questo flusso di lavoro consente agli utenti di riunire frammenti di dati da più set di dati profilo e di impostare la priorità del modo in cui i dati vengono uniti in tali set di dati, al fine di creare una visualizzazione completa di ogni singolo utente. Gli utenti possono unire i singoli set di dati profilo XDM selezionati selezionando il metodo di unione appropriato (Timestamp ordinato o Precedenza set di dati) e aggiungendo i set di dati ExperienceEvent ai set di dati profilo. |
| Visualizzazione schema di unione | Nell’interfaccia utente di Experienci Platform, gli utenti possono trovare più facilmente le informazioni relative a tutti gli schemi e i set di dati che contribuiscono allo schema di unione, nonché gli attributi chiave della superficie, come i campi di identità e relazione. Questi aggiornamenti migliorano la possibilità di risolvere i problemi e di verificare che i profili siano configurati correttamente, che le identità siano unite correttamente e che i dati siano stati acquisiti correttamente. |

Per ulteriori informazioni su Real-Time Customer Profile, inclusi tutorial e best practice per l’utilizzo di [!DNL Profile] dati, leggi i [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove sorgenti**

| Funzione | Descrizione |
| ------- | ----------- |
| [!DNL Shopify] | Ora puoi connetterti [!DNL Shopify] a [!DNL Experience Platform] utilizzando [!DNL Flow Service] o l&#39;interfaccia utente. Consulta la [Panoramica del connettore Shopify](../../sources/connectors/ecommerce/shopify.md) per ulteriori informazioni. |

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiorna informazioni di connessione | È ora possibile aggiornare nomi, descrizioni e credenziali delle connessioni batch esistenti utilizzando [!DNL Flow Service] e l&#39;interfaccia utente. Per ulteriori informazioni, consulta l’esercitazione su [aggiornamento delle connessioni tramite l’API del servizio Flusso](../../sources/tutorials/api/update.md) e [modifica dei dettagli account tramite l’interfaccia utente di](../../sources/tutorials/ui/monitor.md). |
| Eliminare le connessioni | Le connessioni batch che contengono errori o che sono diventate superflue ora possono essere eliminate utilizzando [!DNL Flow Service] e l&#39;interfaccia utente. Per ulteriori informazioni, consulta l’esercitazione su [eliminazione di connessioni tramite l’API del servizio Flusso](../../sources/tutorials/api/delete.md) e [eliminazione di account tramite l’interfaccia utente](../../sources/tutorials/ui/delete-accounts.md). |
| Mappatura gerarchica | Durante il processo di acquisizione dei dati, è possibile visualizzare in anteprima un file di origine gerarchico, ad esempio JSON o Parquet. Guarda il tutorial su [configurazione di un flusso di dati per i connettori di archiviazione cloud nell’interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) per ulteriori informazioni. |
| Supporto API per la mappatura nelle origini di streaming | Ora puoi utilizzare le API per eseguire funzioni di mappatura con le origini di streaming. |
| Supporto API per delimitatori personalizzati per origini di archiviazione cloud | Ora puoi raccogliere file non delimitati da CSV utilizzando origini di archiviazione cloud. È possibile utilizzare qualsiasi delimitatore a colonna singola, ad esempio una tabulazione, una virgola, una barra verticale, un punto e virgola o un hash, per raccogliere file flat in qualsiasi formato. |
| Supporto sandbox per il connettore Adobe Audience Manager | Il connettore di Audience Manager è ora in grado di riconoscere la sandbox. Gli utenti possono abilitare il connettore per instradare i set di dati di Audience Manager alla sandbox di loro scelta (comprese le sandbox non di produzione). La configurazione è limitata a una sandbox per organizzazione. |
| Miglioramenti UX | L’acquisizione basata su file è ora accessibile tramite il catalogo delle origini. |

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).
