---
title: Note sulla versione di Adobe Experience Platform di novembre 2020
description: Note sulla versione di Adobe Experience Platform di novembre 2020.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2178'
ht-degree: 10%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 11 novembre 2020**

Nuove funzioni di Adobe Experience Platform:

- [Migrazione di Adobe Experience Platform Data Lake](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Aggiornamenti alle funzioni esistenti:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [Servizio [!DNL Destinations]](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Migrazione di Adobe Experience Platform Data Lake {#migration}

Durante la migrazione del Data Lake da Adobe a Gen1, gli utenti potranno leggere da Data Lake, ma saranno interessate tutte le funzionalità che scrivono nel Data Lake. Adobe contatterà gli amministratori di sistema per discutere in dettaglio l’impatto della migrazione e confermare le date e gli orari della migrazione per organizzazioni specifiche.

Per ulteriori informazioni, leggere la [Guida alla migrazione di Data Lake](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] sfrutta i profili di prodotto [Adobe Admin Console](https://adminconsole.adobe.com) per collegare gli utenti con autorizzazioni e sandbox. Le autorizzazioni controllano l’accesso a diverse funzionalità di Experience Platform, tra cui la modellazione di dati, la gestione dei profili e l’amministrazione della sandbox.

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Autorizzazioni | In [!DNL Admin Console], la scheda all&#39;interno di un profilo di prodotto [!DNL Experience Platform] ti consente di personalizzare quali funzionalità [!DNL Experience Platform] sono disponibili per gli utenti associati a tale profilo. Le categorie di autorizzazioni disponibili includono: **[!UICONTROL Modellazione dati]**, **[!UICONTROL Gestione dati]**, **[!UICONTROL Gestione profili]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Monitoraggio dati]**, **[!UICONTROL Amministrazione sandbox]**, **[!UICONTROL Destinazioni]**, **[!UICONTROL Acquisizione dati]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Query Service]** e **[!UICONTROL Governance dati]**. |
| Accesso alle sandbox | La scheda **[!UICONTROL Autorizzazioni]** all&#39;interno di un profilo di prodotto [!DNL Experience Platform] può concedere agli utenti l&#39;accesso a sandbox specifiche. Per ulteriori informazioni, consulta la sezione sulle [sandbox](#sandboxes). |

Per ulteriori informazioni, vedere la [panoramica sul controllo degli accessi](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] è un servizio applicativo integrato con [!DNL Experience Platform]. Consente di sfruttare [!DNL Experience Platform] per offrire ai clienti l&#39;offerta e l&#39;esperienza migliore al momento giusto, in tutti i punti di contatto.

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Libreria di offerte centralizzata | L’interfaccia in cui puoi creare e gestire i diversi elementi che compongono le offerte e definirne regole e vincoli. |
| Motore di decisione dell’offerta | Il motore delle decisioni per le offerte sfrutta i dati [!DNL Experience Platform] e [!DNL Real-Time Customer Profiles], insieme alla Libreria di offerte, per selezionare il momento giusto, i clienti e i canali a cui verranno consegnate le offerte. |

Per ulteriori informazioni, vedere la documentazione di [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=it).

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] è stato creato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per soddisfare questa esigenza, [!DNL Experience Platform] fornisce sandbox che suddividono una singola istanza di [!DNL Experience Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Sandbox di produzione | [!DNL Experience Platform] fornisce una singola sandbox di produzione, che non può essere eliminata o reimpostata. Il numero totale di sandbox disponibili, di produzione e non di produzione, è determinato dalla licenza acquisita. |
| Sandbox non di produzione | È possibile creare più sandbox non di produzione per una singola istanza [!DNL Experience Platform], consentendo di testare le funzionalità, eseguire esperimenti e creare configurazioni personalizzate senza influire sulla sandbox di produzione. |
| Commutatore sandbox | Nell&#39;interfaccia utente di [!DNL Experience Platform], il commutatore sandbox nell&#39;angolo in alto a sinistra dello schermo consente di passare dalle sandbox disponibili tramite un menu a discesa. Il selettore sandbox fornisce anche una funzione di ricerca che consente di filtrare tra le sandbox disponibili. |
| Intestazione `x-sandbox-name` | Tutte le chiamate alle API [!DNL Experience Platform] ora devono includere la nuova intestazione `x-sandbox-name`, il cui valore fa riferimento all&#39;attributo `name` della sandbox in cui si svolgerà l&#39;operazione. |

Per ulteriori informazioni, consulta la [panoramica delle sandbox](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Operazioni iterative | [!DNL Data Prep] Mapper ora supporta l&#39;esecuzione di operazioni iterative su una gerarchia. |
| Funzione mappatore | [!DNL Data Prep] Mapper ora può **non** copiare un attributo dall&#39;origine all&#39;XDM di destinazione. |

Per ulteriori informazioni, vedere la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per creare informazioni dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di effettuare previsioni utilizzando i contenuti e le risorse di dati delle soluzioni Adobe. Uno dei modi in cui Data Science Workspace esegue questa operazione è tramite l&#39;utilizzo di [!DNL JupyterLab]. [!DNL JupyterLab] è un&#39;interfaccia utente basata sul Web per [[!DNL Project Jupyter]](https://jupyter.org/) ed è strettamente integrata in Adobe Experience Platform. Fornisce un ambiente di sviluppo interattivo per consentire ai data scientist di lavorare con [!DNL Jupyter] notebook, codice e dati.

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| [!DNL JupyterLab] modello di Generatore di ricette | Aggiornamento dell’utilizzo e delle versioni dei requisiti da notebook a ricetta. L&#39;immagine di base di runtime [!DNL Python] ML è stata aggiornata per utilizzare [!DNL Python] 3.6.7 e un ambiente [!DNL Conda] in modo esclusivo. |

Per ulteriori informazioni, consulta il documento su [creazione di una ricetta tramite Jupyter Notebooks](../../data-science-workspace/jupyterlab/create-a-model.md).

## Servizio [!DNL Destinations] {#destinations}

In [Real-Time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| Braze | Braze è una piattaforma completa per il coinvolgimento dei clienti che offre esperienze pertinenti e memorabili tra i clienti e i marchi che amano. |
| Microsoft Bing | La destinazione Microsoft Bing consente di eseguire il retargeting e campagne digitali mirate al pubblico in Microsoft Display Advertising. |
| The Trade Desk | Trade Desk è una piattaforma self-service per consentire agli acquirenti di annunci di eseguire campagne digitali di retargeting e targeting del pubblico tra sorgenti di visualizzazione, video e inventario mobile. |

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Dettagli della destinazione Aggiornamenti UX | Il flusso di lavoro di destinazione di Real-Time CDP ora include il monitoraggio in linea che consente di vedere quali attivazioni batch sono state completate correttamente. Questa funzione consentirà agli utenti di risolvere i problemi direttamente nel flusso di lavoro per le destinazioni batch tramite avvisi e un dashboard di monitoraggio per tenere traccia degli errori nella pipeline di elaborazione. |
| Crittografia file | Per le destinazioni basate su file, gli utenti possono ora aggiungere la crittografia ai file esportati. |
| Pianificazione file | Per entrambe le destinazioni di archiviazione cloud e basata su e-mail, gli utenti possono creare un’esportazione una tantum o istantanee giornaliere. |
| Campi obbligatori | Gli utenti possono contrassegnare i campi come obbligatori, assicurandosi che vengano esportati solo i campi che contengono il campo obbligatorio. |

Per ulteriori informazioni, consulta la [Panoramica sulle destinazioni](../../destinations/home.md).

## Intelligent Services {#intelligent-services}

I servizi intelligenti consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi di utilizzo dell’esperienza del cliente. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un’azienda utilizzando configurazioni a livello aziendale senza la necessità di competenze in materia di data science.

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Set di dati di Consumer Experience Events (CEE) | La creazione di un set di dati CEE ora supporta l’aggiunta di campi di identità al set di dati con l’Editor schema. IA per l’attribuzione e IA per l’analisi dei clienti utilizzano l’identità primaria per la combinazione di eventi. |

Per ulteriori informazioni, leggere la sezione relativa all&#39;[aggiunta di campi di identità a un set di dati](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) nella guida alla preparazione dei dati di Intelligent Services.

### IA per l’attribuzione

IA per l’attribuzione, parte di Intelligent Services è un servizio di attribuzione algoritmica multicanale che calcola l’influenza e l’impatto incrementale delle interazioni dei clienti rispetto a risultati specifici.

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Collegamento origine dati | Il collegamento all’origine del set di dati originale può essere visualizzato e spostato dalla barra a destra di un’istanza del servizio selezionata. |
| Modifica nome istanza | Ora puoi modificare il nome di un’istanza di IA per l’attribuzione esistente. |
| Clona istanza | Copia la configurazione dell&#39;istanza del servizio attualmente selezionata e consente di apportare modifiche. |
| Modificare i parametri di configurazione dell&#39;istanza | Ora puoi modificare la configurazione di un’istanza di IA per l’attribuzione esistente se non ha ancora iniziato il punteggio. |
| Punteggio unico | Ora puoi attivare il punteggio del modello ad hoc nelle istanze di IA per l’attribuzione. |
| Colonne pass-through | Ora puoi configurare colonne aggiuntive da aggiungere ai file di punteggio di output non elaborati per aggiungere ulteriori dimensioni alle viste strumenti BI. |
| Attivazione e disattivazione dell’istanza | Ora puoi attivare e disattivare l’apprendimento del modello pianificato e il punteggio delle istanze di IA per l’attribuzione. |
| Tracciamento diritti | Puoi trovare la quantità totale di approfondimenti di attribuzione utilizzati dal tuo account nel contenitore crea istanza. |
| Suddivisione dei punti di contatto per posizione | Un nuovo grafico di approfondimenti che fornisce un’analisi dei punti di contatto in base alle posizioni del percorso di conversione. |
| Percorsi di conversione principali | Un nuovo grafico di approfondimenti si trova nella scheda Analisi del percorso. Il grafico contiene un elenco dei primi cinque percorsi di conversione che mostrano la sequenza dei punti di contatto del canale di marketing che hanno portato al maggior numero di conversioni. |
| Efficacia dei punti di contatto | Fornisce informazioni approfondite sulle tre variabili più importanti in base alle quali il modello misura l’efficacia dei punti di contatto. Le variabili sono il rapporto tra percorsi positivi e negativi toccati, l’efficienza del punto di contatto e il volume del punto di contatto. |

Per ulteriori informazioni, leggere la [Panoramica di IA per l&#39;attribuzione](../../intelligent-services/attribution-ai/overview.md).

### IA per l’analisi dei clienti

IA per l’analisi dei clienti, parte di Intelligent Services offre agli esperti marketing la possibilità di generare previsioni sui clienti a livello individuale con spiegazioni. Con l’aiuto di fattori influenti, IA per l’analisi dei clienti può dirti cosa potrebbe fare un cliente e perché. Inoltre, gli esperti di marketing possono trarre vantaggio dalle previsioni e dalle informazioni di Customer AI per personalizzare le esperienze dei clienti fornendo le offerte e i messaggi più appropriati.

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Collegamento origine dati | Il collegamento all’origine del set di dati originale può essere visualizzato e spostato dalla barra a destra di un’istanza del servizio selezionata. |
| Modifica nome istanza | Puoi modificare il nome di un’istanza di Customer AI esistente. |
| Modificare i parametri di configurazione dell&#39;istanza | Ora puoi modificare la configurazione di un’istanza di IA per l’analisi dei clienti esistente se non ha ancora avviato un punteggio. |
| Clona istanza | Copia la configurazione dell&#39;istanza del servizio attualmente selezionata e consente di apportare modifiche. |
| Tracciamento diritti | Puoi trovare la quantità totale di profili valutati da IA per l’analisi dei clienti per il tuo account nel contenitore crea istanza. |
| Obiettivo di previsione | La flessibilità nella creazione di un obiettivo di previsione è stata aumentata con nuove opzioni per prevedere se qualcosa &quot;si verificherà&quot; o &quot;non si verificherà&quot;. Inoltre, sono state aggiunte le opzioni per prevedere se &quot;tutti&quot; gli eventi si verificano o se &quot;uno qualsiasi&quot; degli eventi si verifica quando vengono utilizzati più eventi. |
| Espansione del fattore di influenza | I bucket dei fattori influenti principali della propensione ora contengono drill-down. I drill-down rappresentano un riepilogo più dettagliato dei valori per ciascuno dei principali fattori influenti all’interno di un bucket di propensione. |

Per ulteriori informazioni, leggere la [Panoramica di Customer AI](../../intelligent-services/customer-ai/overview.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati disparati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Flusso di lavoro dei criteri di unione aggiornato | Experience Platform ha aggiornato la configurazione dei criteri di unione a un nuovo flusso di lavoro graduale. Questo flusso di lavoro consente agli utenti di riunire frammenti di dati da più set di dati profilo e di impostare la priorità del modo in cui i dati vengono uniti in tali set di dati, al fine di creare una visualizzazione completa di ogni singolo utente. Gli utenti possono unire i singoli set di dati profilo XDM selezionati selezionando il metodo di unione appropriato (Timestamp ordinato o Precedenza set di dati) e aggiungendo i set di dati ExperienceEvent ai set di dati profilo. |
| Visualizzazione schema di unione | Nell’interfaccia utente di Experience Platform, gli utenti possono trovare più facilmente le informazioni relative a tutti gli schemi e i set di dati che contribuiscono allo schema di unione, nonché gli attributi chiave della superficie, come i campi di identità e relazione. Questi aggiornamenti migliorano la possibilità di risolvere i problemi e di verificare che i profili siano configurati correttamente, che le identità siano unite correttamente e che i dati siano stati acquisiti correttamente. |

Per ulteriori informazioni su Real-Time Customer Profile, inclusi tutorial e best practice per l&#39;utilizzo dei dati di [!DNL Profile], leggere la [Panoramica sul profilo cliente in tempo reale](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo consentire di strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Experience Platform]. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema di gestione delle relazioni con i clienti.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di configurare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove origini**

| Funzione | Descrizione |
| ------- | ----------- |
| [!DNL Shopify] | È ora possibile connettere [!DNL Shopify] a [!DNL Experience Platform] utilizzando l&#39;API [!DNL Flow Service] o l&#39;interfaccia utente. Per ulteriori informazioni, vedere [Panoramica del connettore Shopify](../../sources/connectors/ecommerce/shopify.md). |

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiorna informazioni di connessione | È ora possibile aggiornare i nomi, le descrizioni e le credenziali delle connessioni batch esistenti utilizzando l&#39;API [!DNL Flow Service] e l&#39;interfaccia utente. Per ulteriori informazioni, vedere l&#39;esercitazione su [aggiornamento delle connessioni tramite l&#39;API del servizio Flusso](../../sources/tutorials/api/update.md) e [modifica dei dettagli dell&#39;account tramite l&#39;interfaccia utente](../../sources/tutorials/ui/monitor.md). |
| Elimina connessioni | È ora possibile eliminare le connessioni batch che contengono errori o che non sono più necessarie utilizzando l&#39;API [!DNL Flow Service] e l&#39;interfaccia utente. Per ulteriori informazioni, vedere l&#39;esercitazione su [eliminazione di connessioni tramite l&#39;API del servizio Flusso](../../sources/tutorials/api/delete.md) e [eliminazione di account tramite l&#39;interfaccia utente](../../sources/tutorials/ui/delete-accounts.md). |
| Mappatura gerarchica | Durante il processo di acquisizione dei dati, è possibile visualizzare in anteprima un file di origine gerarchico, ad esempio JSON o Parquet. Per ulteriori informazioni, consulta l&#39;esercitazione su [configurazione di un flusso di dati per i connettori di archiviazione cloud nell&#39;interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |
| Supporto API per la mappatura nelle origini di streaming | Ora puoi utilizzare le API per eseguire funzioni di mappatura con le origini di streaming. |
| Supporto API per delimitatori personalizzati per origini di archiviazione cloud | Ora puoi raccogliere file non delimitati da CSV utilizzando origini di archiviazione cloud. È possibile utilizzare qualsiasi delimitatore a colonna singola, ad esempio una tabulazione, una virgola, una barra verticale, un punto e virgola o un hash, per raccogliere file flat in qualsiasi formato. |
| Supporto sandbox per il connettore Adobe Audience Manager | Il connettore Audience Manager ora supporta la sandbox. Gli utenti possono abilitare il connettore per indirizzare i set di dati di Audience Manager alla sandbox di loro scelta (comprese le sandbox non di produzione). La configurazione è limitata a una sandbox per organizzazione. |
| Miglioramenti UX | L’acquisizione basata su file è ora accessibile tramite il catalogo delle origini. |

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
