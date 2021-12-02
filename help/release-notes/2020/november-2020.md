---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di Experience Platform 11 novembre 2020
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: 38c493e6306e493f4ef5caf90509bda6f4d80023
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 3%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 11 novembre 2020**

Nuove funzioni in Adobe Experience Platform:

- [Migrazione Adobe Experience Platform Data Lake](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Aggiornamenti alle funzioni esistenti:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] Servizio](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Migrazione Adobe Experience Platform Data Lake {#migration}

Durante la migrazione del Data Lake da Gen1 a Gen2, gli utenti saranno in grado di leggere dal Data Lake, ma tutte le funzionalità che scrivono nel Data Lake saranno influenzate. Ad Adobe, gli amministratori di sistema contatteranno per discutere in dettaglio l’impatto della migrazione e per confermare le date e le ore di migrazione per specifiche organizzazioni IMS.

Per ulteriori informazioni, leggere il [Guida alla migrazione a Data Lake](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] leva finanziaria [Adobe Admin Console](https://adminconsole.adobe.com) profili di prodotto per collegare gli utenti con autorizzazioni e sandbox. Le autorizzazioni controllano l’accesso a una varietà di funzionalità di Platform, tra cui la modellazione dei dati, la gestione dei profili e l’amministrazione di sandbox.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Autorizzazioni | In [!DNL Admin Console], la scheda all’interno di un [!DNL Platform] il profilo di prodotto ti consente di personalizzare quali [!DNL Platform] sono disponibili per gli utenti collegati a tale profilo. Le categorie di autorizzazioni disponibili includono: **[!UICONTROL Modellazione dati]**, **[!UICONTROL Gestione dati]**, **[!UICONTROL Gestione dei profili]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Monitoraggio dei dati]**, **[!UICONTROL Amministrazione delle sandbox]**, **[!UICONTROL Destinazioni]**, **[!UICONTROL Acquisizione dei dati]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Servizio query]** e **[!UICONTROL Governance dei dati]**. |
| Accesso alle sandbox | La **[!UICONTROL Autorizzazioni]** in una scheda [!DNL Platform] il profilo di prodotto può concedere agli utenti l’accesso a sandbox specifiche. Vedi la sezione su [sandbox](#sandboxes) qui sotto per ulteriori informazioni. |

Per ulteriori informazioni, consulta la sezione [panoramica sul controllo degli accessi](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] è un servizio applicativo integrato con [!DNL Experience Platform]. Ti consente di sfruttare [!DNL Platform] per offrire ai clienti la migliore offerta ed esperienza possibile in tutti i punti di contatto al momento giusto.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Libreria di offerte centralizzata | Interfaccia in cui puoi creare e gestire i diversi elementi che compongono le offerte e definirne regole e vincoli. |
| Motore di decisione dell’offerta | Il motore di decisione dell’offerta sfrutta [!DNL Platform] dati e [!DNL Real-time Customer Profiles], insieme alla Libreria offerte, per selezionare l’ora esatta, i clienti e i canali a cui verranno distribuite le offerte. |

Per ulteriori informazioni, consulta la sezione [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=it) documentazione.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] è progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e alla distribuzione di queste applicazioni, garantendo al contempo la conformità operativa. Per far fronte a questa necessità, [!DNL Experience Platform] fornisce sandbox che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Sandbox di produzione | [!DNL Experience Platform] fornisce una singola sandbox di produzione che non può essere eliminata o reimpostata. Il numero totale di sandbox disponibili, produzione e non produzione, è determinato dalla licenza acquisita. |
| Sandbox non di produzione | È possibile creare più sandbox non di produzione per un singolo [!DNL Platform] , che consente di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sulla sandbox di produzione. |
| Switcher sandbox | In [!DNL Experience Platform] l’interfaccia utente, il commutatore sandbox nell’angolo in alto a sinistra dello schermo consente di passare da una sandbox all’altra tramite un menu a discesa. Il commutatore sandbox fornisce anche una funzione di ricerca che consente di filtrare tra le sandbox disponibili. |
| `x-sandbox-name` header | Tutte le chiamate a [!DNL Experience Platform] Ora le API devono includere i nuovi `x-sandbox-name` intestazione, il cui valore fa riferimento a `name` attributo della sandbox in cui avrà luogo l’operazione. |

Per ulteriori informazioni, consulta la sezione [panoramica sulle sandbox](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Operazioni iterative | [!DNL Data Prep] Mapper ora supporta l&#39;esecuzione di operazioni iterative su una gerarchia. |
| Funzione Mapper | [!DNL Data Prep] Mapper ora ha la capacità di **not** copia un attributo dall&#39;origine all&#39;XDM di destinazione. |

Per ulteriori informazioni, consulta la sezione [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per creare informazioni dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di fare previsioni utilizzando i contenuti e le risorse di dati nelle soluzioni Adobe. Uno dei modi in cui Data Science Workspace ottiene questo risultato è attraverso l&#39;uso di [!DNL JupyterLab]. [!DNL JupyterLab] è un&#39;interfaccia utente basata sul Web per [[!DNL Project Jupyter]](https://jupyter.org/) ed è strettamente integrato in Adobe Experience Platform. Offre agli scienziati dei dati un ambiente di sviluppo interattivo con cui lavorare [!DNL Jupyter] blocchi appunti, codice e dati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| [!DNL JupyterLab] Modello di Generatore di ricette | Aggiornamento delle versioni e dell&#39;utilizzo del notebook per le ricette. [!DNL Python] L&#39;immagine di base di ML Runtime è stata aggiornata per utilizzare [!DNL Python] 3.6.7 e a [!DNL Conda] ambiente esclusivamente. |

Per ulteriori informazioni, leggere il documento su [creazione di una ricetta utilizzando Jupyter Notebooks](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] Servizio {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| Braccio | Braze è una piattaforma completa di coinvolgimento dei clienti che offre esperienze rilevanti e memorabili tra i clienti e i marchi che amano. |
| Microsoft Bing | La destinazione Microsoft Bing consente di eseguire campagne digitali di retargeting e mirate per il pubblico in Microsoft Display Advertising. |
| Il banco commerciale | Il Trade Desk è una piattaforma self-service per gli acquirenti di annunci che esegue il retargeting e campagne digitali mirate per il pubblico tra le varie fonti di visualizzazione, video e inventario mobile. |

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamenti UX dettagli destinazione | Il flusso di lavoro di destinazione di Real-time CDP ora include il monitoraggio in linea per vedere quali attivazioni batch hanno avuto successo. Questa funzione consente agli utenti di risolvere i problemi direttamente nel flusso di lavoro per le destinazioni batch tramite avvisi e un dashboard di monitoraggio per tenere traccia degli errori nella pipeline di elaborazione. |
| Crittografia file | Per le destinazioni basate su file, gli utenti possono ora aggiungere la crittografia ai file esportati. |
| Pianificazione dei file | Per le destinazioni di archiviazione cloud e basate su e-mail, gli utenti possono creare un’esportazione una tantum o istantanee giornaliere. |
| Campi obbligatori | Gli utenti possono contrassegnare i campi come obbligatori, garantendo l’esportazione solo dei campi contenenti il campo obbligatorio. |

Per ulteriori informazioni, consulta la sezione [Panoramica sulle destinazioni](../../destinations/home.md).

## Intelligent Services {#intelligent-services}

I servizi intelligenti consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi d’uso della customer experience. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un&#39;azienda utilizzando configurazioni a livello di business senza la necessità di conoscenze scientifiche dei dati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Set di dati di Consumer Experience Events (CEE) | La creazione di un set di dati CEE supporta ora l’aggiunta di campi di identità al set di dati con l’Editor schema. Attribution AI e Customer AI utilizzano l’identità principale per combinare gli eventi. |

Per ulteriori informazioni, consulta la sezione su [aggiunta di campi di identità a un set di dati](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) nella guida alla preparazione dei dati di Intelligent Services .

### Attribution AI

Nell’ambito di Intelligent Services, Attribution AI è un servizio di attribuzione algoritmica multicanale che calcola l’influenza e l’impatto incrementale delle interazioni dei clienti rispetto a risultati specifici.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Collegamento alla sorgente dati | Il collegamento all’origine del set di dati originale può essere visualizzato e navigato dalla barra a destra di un’istanza di servizio selezionata. |
| Modifica nome istanza | Ora puoi modificare il nome di un’istanza di Attribution AI esistente. |
| Clona istanza | Copia la configurazione dell&#39;istanza del servizio attualmente selezionata e consente le modifiche. |
| Modificare i parametri di configurazione dell’istanza | Ora puoi modificare la configurazione di un’istanza di Attribution AI esistente se non ha ancora iniziato il punteggio. |
| Punteggio unico | Ora puoi attivare il punteggio del modello ad hoc nelle istanze di Attribution AI. |
| Passare alle colonne | È ora possibile configurare colonne aggiuntive che verranno aggiunte ai file di punteggio di output non elaborati per aggiungere dimensioni aggiuntive alle visualizzazioni degli strumenti BI. |
| Attivazione e disattivazione delle istanze | Ora puoi attivare e disattivare la formazione e il punteggio pianificati dei modelli di Attribution AI. |
| Tracciamento dei diritti | Puoi trovare la quantità totale di approfondimenti di attribuzione utilizzati dal tuo account nel contenitore di istanze di creazione. |
| Suddivisione per posizione dei punti di contatto | Un nuovo grafico di informazioni che fornisce un’analisi dei punti di contatto in base alle posizioni dei percorsi di conversione. |
| Percorsi di conversione principali | Un nuovo grafico di insights si trova nella scheda Analisi percorso . Il grafico contiene un elenco dei primi cinque percorsi di conversione che mostrano la sequenza di punti di contatto dei canali di marketing che hanno portato al maggior numero di conversioni. |
| Efficienza dei punti di contatto | Fornisce informazioni approfondite sulle tre variabili più importanti per le quali il modello misura l’efficacia dei punti di contatto. Le variabili sono il rapporto tra percorsi positivi e negativi toccati, l’efficienza dei punti di contatto e il volume dei punti di contatto. |

Per ulteriori informazioni, leggere il [Panoramica di Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Customer AI

Customer AI, come parte di Intelligent Services, fornisce agli addetti al marketing il potere di generare previsioni sui clienti a livello individuale con spiegazioni. Con l’aiuto di fattori influenti, Customer AI può dirvi cosa è probabile che faccia un cliente e perché. Inoltre, gli esperti di marketing possono trarre vantaggio dalle previsioni e dalle informazioni di Customer AI per personalizzare le esperienze dei clienti servendo le offerte e i messaggi più appropriati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Collegamento alla sorgente dati | Il collegamento all’origine del set di dati originale può essere visualizzato e navigato dalla barra a destra di un’istanza di servizio selezionata. |
| Modifica nome istanza | Puoi modificare il nome di un’istanza di Customer AI esistente. |
| Modificare i parametri di configurazione dell’istanza | Ora puoi modificare la configurazione di un’istanza di Customer AI esistente se non ha ancora avviato un punteggio. |
| Clona istanza | Copia la configurazione dell&#39;istanza del servizio attualmente selezionata e consente le modifiche. |
| Tracciamento dei diritti | Puoi trovare la quantità totale di profili valutati da Customer AI per il tuo account nel contenitore di istanze di creazione. |
| Obiettivo di previsione | La flessibilità nella creazione di un obiettivo di previsione è stata aumentata con nuove opzioni per prevedere se qualcosa &quot;si verificherà&quot; o &quot;non si verificherà&quot;. Inoltre, sono state aggiunte le opzioni per prevedere se &quot;tutti&quot; gli eventi si verificano o &quot;uno qualsiasi&quot; gli eventi che si verificano quando vengono utilizzati più eventi. |
| Drilldown dei fattori influenti | I blocchi di fattori influenti principali della tendenza ora contengono drill-down. I drill-down sono un riepilogo di livello più approfondito dei valori per ciascuno dei fattori influenti principali all’interno di un bucket di propensione. |

Per ulteriori informazioni, leggere il [Panoramica di Customer AI](../../intelligent-services/customer-ai/overview.md).

## Real-time Customer Profile {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account actionable e timestamp di ogni interazione con il cliente.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Flusso di lavoro dei criteri di unione aggiornato | Platform ha aggiornato la configurazione dei criteri di unione a un nuovo flusso di lavoro graduale. Questo flusso di lavoro consente agli utenti di unire frammenti di dati provenienti da più set di dati Profilo e impostare la priorità per il modo in cui i dati vengono uniti in tali set di dati al fine di creare una visualizzazione completa di ogni singolo utente. Gli utenti possono unire i set di dati di profilo individuali XDM selezionati selezionando il metodo di unione appropriato (timestamp ordered or Dataset) e aggiungendo i set di dati ExperienceEvent ai set di dati di profilo. |
| Visualizzazione schema unione | Nell’interfaccia utente di Experience Platform, gli utenti possono trovare più facilmente informazioni su tutti gli schemi e i set di dati che contribuiscono allo schema dell’unione, nonché attributi chiave di superficie come i campi di identità e relazione. Questi aggiornamenti migliorano la possibilità di risolvere e convalidare la corretta configurazione dei profili, la corretta unione delle identità e il corretto inserimento dei dati. |

Per ulteriori informazioni sul profilo cliente in tempo reale, compresi tutorial e best practice per l’utilizzo di [!DNL Profile] dati, leggere [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove fonti**

| Funzione | Descrizione |
| ------- | ----------- |
| [!DNL Shopify] | È ora possibile connettersi [!DNL Shopify] a [!DNL Experience Platform] utilizzando [!DNL Flow Service] API o interfaccia utente. Consulta la sezione [Panoramica del connettore Shopid](../../sources/connectors/ecommerce/shopify.md) per ulteriori informazioni. |

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiorna informazioni sulla connessione | È ora possibile aggiornare i nomi, le descrizioni e le credenziali delle connessioni batch esistenti utilizzando [!DNL Flow Service] API e interfaccia utente. Per ulteriori informazioni, consulta l’esercitazione su [aggiornamento delle connessioni tramite l’API del servizio di flusso](../../sources/tutorials/api/update.md) e [modifica dei dettagli dell’account tramite l’interfaccia utente](../../sources/tutorials/ui/monitor.md). |
| Eliminare le connessioni | Le connessioni batch che contengono errori o che sono diventate superflue ora possono essere eliminate utilizzando [!DNL Flow Service] API e interfaccia utente. Per ulteriori informazioni, consulta l’esercitazione su [eliminazione di connessioni tramite l’API del servizio di flusso](../../sources/tutorials/api/delete.md) e [eliminazione di account tramite l’interfaccia utente](../../sources/tutorials/ui/delete-accounts.md). |
| Mappatura gerarchica | È possibile visualizzare in anteprima un file di origine gerarchico, ad esempio JSON o Parquet, durante il processo di acquisizione dei dati. Visualizza l’esercitazione su [configurazione di un flusso di dati per i connettori di archiviazione cloud nell’interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) per ulteriori informazioni. |
| Supporto API per la mappatura nelle origini streaming | È ora possibile utilizzare le API per eseguire funzioni di mappatura con origini streaming. |
| Supporto API per delimitatori personalizzati per le origini di archiviazione cloud | Ora puoi raccogliere file non delimitati da CSV utilizzando le origini di archiviazione cloud. È possibile utilizzare qualsiasi carattere di delimitazione a una singola colonna, ad esempio tabulazione, virgola, barra verticale, punto e virgola o hash, per raccogliere file flat in qualsiasi formato. |
| Supporto sandbox per il connettore Adobe Audience Manager | Il connettore di Audience Manager ora è in grado di riconoscere la sandbox. Gli utenti possono abilitare il connettore per indirizzare i set di dati di Audience Manager alla sandbox di loro scelta (incluse le sandbox non di produzione). La configurazione è limitata a una sandbox per organizzazione IMS. |
| Miglioramenti UX | L’acquisizione basata su file è ora accessibile tramite il catalogo origini. |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
