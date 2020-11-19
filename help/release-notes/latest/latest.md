---
title: 'Note sulla versione di Adobe Experience Platform '
description: ' Experience Platform note sulla versione 11 novembre 2020'
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 6cf9c88f6dc751a4cc877670a89cc99d1efb1b2a
workflow-type: tm+mt
source-wordcount: '2157'
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

Mentre  Adobe sta migrando il Data Lake da Gen1 a Gen2, gli utenti saranno in grado di leggere dal Data Lake, ma tutte le capacità che scrivono nel Data Lake saranno influenzate.  Adobe contatterà gli amministratori di sistema per discutere in dettaglio l&#39;impatto della migrazione e per confermare le date e le ore di migrazione per specifiche organizzazioni IMS.

Per ulteriori informazioni, consulta la guida [alla migrazione a](../../landing/adls2-gen2-migration.md)Data Lake.

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] sfrutta i profili di prodotto [Adobe Admin Console](https://adminconsole.adobe.com) per collegare gli utenti con autorizzazioni e sandbox. Le autorizzazioni controllano l&#39;accesso a diverse funzionalità della piattaforma, tra cui la modellazione dei dati, la gestione dei profili e l&#39;amministrazione della sandbox.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Autorizzazioni | In [!DNL Admin Console], la scheda all&#39;interno di un profilo di [!DNL Platform] prodotto consente di personalizzare [!DNL Platform] le funzionalità disponibili per gli utenti collegati a tale profilo. Le categorie di autorizzazioni disponibili includono: **[!UICONTROL Data Modeling]**, **[!UICONTROL Data Management]**, **[!UICONTROL Profile Management]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Data Monitoring]**, **[!UICONTROL Sandbox Administration]**, **[!UICONTROL Destinations]**, **[!UICONTROL Data Ingestion]**, **[!UICONTROL Data Science Workspace]**, e **[!UICONTROL Query Service]****[!UICONTROL Data Governance]**. |
| Accesso alle sandbox | La **[!UICONTROL Permissions]** scheda all&#39;interno di un profilo di [!DNL Platform] prodotto può consentire agli utenti l&#39;accesso a sandbox specifiche. Per ulteriori informazioni, consultate la sezione sulle [sandbox](#sandboxes) di seguito. |

Per ulteriori informazioni, consulta la panoramica [sul controllo](../../access-control/home.md)degli accessi.

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] è un servizio applicazione integrato con [!DNL Experience Platform]. Consente di sfruttare [!DNL Platform] per offrire ai clienti la migliore offerta ed esperienza su tutti i punti di contatto al momento giusto.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Libreria di offerte centralizzata | Interfaccia in cui creare e gestire i diversi elementi che compongono le offerte e definire le relative regole e vincoli. |
| Modulo di decisione offerta | Il modulo decisionale Offer sfrutta [!DNL Platform] i dati e [!DNL Real-time Customer Profiles], insieme alla libreria Offer, per selezionare il momento giusto, i clienti e i canali a cui verranno consegnate le offerte. |

Per ulteriori informazioni, consulta la [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=en) documentazione.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] è progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e all&#39;implementazione di tali applicazioni, garantendo al contempo la conformità operativa. Per rispondere a questa esigenza, [!DNL Experience Platform] fornisce sandbox che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per aiutare a sviluppare e sviluppare applicazioni di esperienza digitale.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Sandbox produzione | [!DNL Experience Platform] fornisce una singola sandbox di produzione, che non può essere eliminata o reimpostata. Il numero totale di sandbox disponibili, produzione e non produzione, è determinato dalla licenza acquisita. |
| Sandbox non di produzione | È possibile creare più sandbox non di produzione per una singola [!DNL Platform] istanza, per testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sul sandbox di produzione. |
| Switcher sandbox | Nell&#39;interfaccia [!DNL Experience Platform] utente, lo switcher sandbox nell&#39;angolo superiore sinistro dello schermo consente di passare dalle sandbox disponibili a un menu a discesa. Lo switcher sandbox offre anche una funzione di ricerca che consente di filtrare attraverso le sandbox disponibili. |
| `x-sandbox-name` header | Tutte le chiamate alle [!DNL Experience Platform] API ora devono includere la nuova `x-sandbox-name` intestazione, il cui valore fa riferimento all&#39; `name` attributo della sandbox in cui avrà luogo l&#39;operazione. |

Per ulteriori informazioni, consultate la panoramica sulle [sandbox](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente agli sviluppatori di dati di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Operazioni iterative | [!DNL Data Prep] Mapper ora supporta l&#39;esecuzione di operazioni ripetitive su una gerarchia. |
| Funzione Mapper | [!DNL Data Prep] Mapper ora ha la capacità di **non** copiare un attributo dall&#39;origine all&#39;XDM di destinazione. |

Per ulteriori informazioni, consultate la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per creare approfondimenti dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di fare previsioni utilizzando i contenuti e le risorse dati nelle soluzioni  Adobe. Uno dei modi in cui Data Science Workspace ottiene questo risultato è attraverso l&#39;uso di [!DNL JupyterLab]. [!DNL JupyterLab] è un&#39;interfaccia utente basata sul Web per [[!DNL Project Jupyter]](https://jupyter.org/) ed è strettamente integrata in Adobe Experience Platform. Fornisce un ambiente di sviluppo interattivo per l&#39;utilizzo di [!DNL Jupyter] blocchi appunti, codice e dati da parte degli esperti di analisi dei dati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| [!DNL JupyterLab] Modello di Generatore di ricette | Aggiornamento dei requisiti di utilizzo e delle versioni del notebook. [!DNL Python] L&#39;immagine di base del runtime ML è stata aggiornata per utilizzare esclusivamente [!DNL Python] 3.6.7 e un [!DNL Conda] ambiente. |

Per ulteriori informazioni, leggete il documento sulla [creazione di una ricetta utilizzando i notebook](../../data-science-workspace/jupyterlab/create-a-recipe.md)Jupyter.

## [!DNL Destinations] Servizio {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni pre-costruite con piattaforme di destinazione che attivano i dati a tali partner in modo semplice.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| Braccio | Braze è una piattaforma completa di coinvolgimento dei clienti che offre esperienze rilevanti e memorabili tra i clienti e i marchi che amano. |
| Microsoft Bing | La destinazione Microsoft Bing consente di eseguire il retargeting e campagne digitali mirate per l&#39;audience in Microsoft Display Advertising. |
| Il banco commerciale | Il Trade Desk è una piattaforma self-service per gli acquirenti di annunci che esegue retargeting e campagne digitali mirate per il pubblico attraverso fonti di visualizzazione, video e inventario mobile. |

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Dettagli di destinazione Aggiornamenti UX | Il flusso di lavoro di destinazione del CDP in tempo reale ora include il monitoraggio in linea per vedere quali attivazioni batch hanno avuto successo. Questa funzione consente agli utenti di risolvere i problemi direttamente nel flusso di lavoro per le destinazioni batch tramite avvisi e una dashboard di monitoraggio per monitorare gli errori nella pipeline di elaborazione. |
| Cifratura file | Per le destinazioni basate su file, gli utenti ora possono aggiungere la cifratura ai propri file esportati. |
| Pianificazione file | Per le destinazioni di archiviazione cloud e basate su e-mail, gli utenti possono creare un&#39;esportazione una tantum o istantanee giornaliere. |
| Campi obbligatori | Gli utenti possono contrassegnare i campi come obbligatori, assicurando che vengano esportati solo i campi contenenti il campo obbligatorio. |

Per ulteriori informazioni, consulta la panoramica [](../../rtcdp/destinations/destinations-overview.md)Destinazioni.

## Intelligent Services {#intelligent-services}

I servizi intelligenti consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell&#39;intelligenza artificiale e dell&#39;apprendimento automatico nei casi di utilizzo dell&#39;esperienza cliente. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un&#39;azienda utilizzando configurazioni a livello di business, senza bisogno di conoscenze scientifiche.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Set di dati degli eventi di esperienza del consumatore (CEE) | La creazione di un set di dati CEE ora supporta l&#39;aggiunta di campi di identità al set di dati con l&#39;Editor schema.  Attribution AI e AI cliente utilizzano l&#39;identità principale per combinare gli eventi. |

Per ulteriori informazioni, consulta la sezione sull’ [aggiunta di campi di identità a un dataset](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) nella guida alla preparazione dei dati dei servizi intelligenti.

### Attribution AI 

 Attribution AI, come parte di Intelligent Services è un servizio di attribuzione algoritmica multicanale che calcola l&#39;influenza e l&#39;impatto incrementale delle interazioni dei clienti rispetto a determinati risultati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Collegamento origine dati | Il collegamento all&#39;origine del set di dati originale può essere visualizzato e navigato dalla barra laterale destra di un&#39;istanza di servizio selezionata. |
| Modifica nome istanza | È ora possibile modificare il nome di un&#39;istanza di Attribution AI  esistente. |
| Clona istanza | Copia l’impostazione dell’istanza di servizio attualmente selezionata e consente di apportare modifiche. |
| Modificare i parametri di configurazione dell&#39;istanza | È ora possibile modificare la configurazione di un&#39;istanza di Attribution AI  esistente se non ha ancora iniziato il punteggio. |
| Un punteggio finale | Ora è possibile attivare il punteggio del modello ad hoc nelle Attribution AI . |
| Passa alle colonne | È ora possibile configurare ulteriori colonne che verranno aggiunte ai file di valutazione dell&#39;output non elaborato per aggiungere ulteriori dimensioni alle visualizzazioni degli strumenti BI. |
| Attivazione e disattivazione dell’istanza | È ora possibile attivare e disattivare la formazione e il punteggio pianificati per i modelli delle Attribution AI . |
| Tracciamento adesione | Puoi trovare la quantità totale di approfondimenti di attribuzione utilizzati dal tuo account nel contenitore delle istanze di creazione. |
| Suddivisione punti di contatto per posizione | Un nuovo grafico di approfondimenti che fornisce un&#39;analisi dei punti di contatto per le posizioni dei percorsi di conversione. |
| Percorsi di conversione principali | Un nuovo grafico delle informazioni nella scheda Analisi percorso. Il grafico contiene un elenco dei primi cinque percorsi di conversione con la sequenza di punti di contatto dei canali di marketing che hanno portato al maggior numero di conversioni. |
| Efficienza punto di contatto | Fornisce informazioni approfondite sulle tre variabili più importanti per cui il modello misura l’efficacia dei punti di contatto. Le variabili sono rapporto tra percorsi positivi e negativi, efficienza dei punti di contatto e volume dei punti di contatto. |

Per ulteriori informazioni, leggere la [panoramica](../../intelligent-services/attribution-ai/overview.md)delle Attribution AI.

### AI cliente

L&#39;AI del cliente, come parte di Intelligent Services, fornisce ai professionisti del marketing la possibilità di generare previsioni sui clienti a livello individuale con spiegazioni. Con l&#39;aiuto di fattori influenti, l&#39;intelligenza artificiale del cliente può dirvi cosa è probabile fare e perché. Inoltre, gli esperti di marketing possono trarre vantaggio dalle previsioni e dalle informazioni dell&#39;AI cliente per personalizzare l&#39;esperienza dei clienti, servendo le offerte e i messaggi più appropriati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Collegamento origine dati | Il collegamento all&#39;origine del set di dati originale può essere visualizzato e navigato dalla barra laterale destra di un&#39;istanza di servizio selezionata. |
| Modifica nome istanza | Puoi modificare il nome di un&#39;istanza AI cliente esistente. |
| Modificare i parametri di configurazione dell&#39;istanza | Ora puoi modificare la configurazione di un&#39;istanza dell&#39;AI cliente esistente se non ha ancora iniziato un punteggio. |
| Clona istanza | Copia l’impostazione dell’istanza di servizio attualmente selezionata e consente di apportare modifiche. |
| Tracciamento adesione | Puoi trovare la quantità totale di profili assegnati dal Customer AI per il tuo account nel contenitore di istanza di creazione. |
| Obiettivo di previsione | La flessibilità nella creazione di un obiettivo di previsione è stata aumentata con nuove opzioni per prevedere se qualcosa &quot;si verificherà&quot; o &quot;non si verificherà&quot;. Inoltre, sono state aggiunte le opzioni per prevedere se &quot;tutti&quot; gli eventi accadono o &quot;uno qualsiasi&quot; quando vengono utilizzati più eventi. |
| Perdita dei fattori influenti | I periodi fissi dei fattori influenti principali di tendenza ora contengono i drill-down. Le analisi approfondite sono un riepilogo di livello più approfondito dei valori per ciascuno dei fattori più influenti all&#39;interno di un intervallo di propensione. |

Per ulteriori informazioni, consulta la panoramica [dell&#39;intelligenza artificiale](../../intelligent-services/customer-ai/overview.md)del cliente.

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti per i clienti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con il profilo cliente in tempo reale, puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati da più canali, inclusi dati online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Flusso di lavoro dei criteri di unione aggiornati | La piattaforma ha aggiornato la configurazione del criterio di unione a un nuovo flusso di lavoro graduale. Questo flusso di lavoro consente agli utenti di riunire i frammenti di dati provenienti da più set di dati Profilo e impostare la priorità per l&#39;unione dei dati tra tali set di dati, al fine di creare una visualizzazione completa di ciascun singolo. Gli utenti possono unire i set di dati XDM singoli profili selezionati selezionando il metodo di unione appropriato (timestamp ordinato o Precedenza DataSet) e aggiungendo i set di dati ExperienceEvent ai set di dati Profilo. |
| Visualizzazione schema unione | Nell&#39;interfaccia utente del Experience Platform di , gli utenti possono trovare più facilmente informazioni su tutti gli schemi e i set di dati che contribuiscono allo schema unione, nonché attributi di chiave di superficie quali i campi di identità e relazione. Questi aggiornamenti migliorano la capacità di risolvere eventuali problemi e convalidare la corretta configurazione dei profili, la corretta unione delle identità e l’acquisizione dei dati. |

Per ulteriori informazioni sul profilo cliente in tempo reale, comprese esercitazioni e best practice per lavorare con [!DNL Profile] i dati, consulta la panoramica [sul profilo cliente in tempo](../../profile/home.md)reale.

## [!DNL Sources] {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne e di strutturarli, etichettarli e ottimizzarli utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove origini**

| Funzione | Descrizione |
| ------- | ----------- |
| [!DNL Shopify] | È ora possibile connettersi [!DNL Shopify] a [!DNL Experience Platform] utilizzando l&#39; [!DNL Flow Service] API o l&#39;interfaccia utente. Per ulteriori informazioni, vedere la panoramica [del connettore](../../sources/connectors/ecommerce/shopify.md) Shopify. |

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento delle informazioni di connessione | Ora puoi aggiornare i nomi, le descrizioni e le credenziali delle connessioni batch esistenti utilizzando l&#39; [!DNL Flow Service] API e l&#39;interfaccia utente. Per ulteriori informazioni, consulta l’esercitazione sull’ [aggiornamento delle connessioni tramite l’API](../../sources/tutorials/api/update.md) del servizio di flusso e sulla [modifica dei dettagli dell’account tramite l’interfaccia utente](../../sources/tutorials/ui/monitor.md). |
| Elimina connessioni | Le connessioni batch che contengono errori o che non sono più necessarie ora possono essere eliminate utilizzando l&#39; [!DNL Flow Service] API e l&#39;interfaccia utente. Per ulteriori informazioni, consultate l&#39;esercitazione sull&#39; [eliminazione di connessioni tramite l&#39;API](../../sources/tutorials/api/delete.md) del servizio di flusso e sull&#39; [eliminazione di account tramite l&#39;interfaccia utente](../../sources/tutorials/ui/delete-accounts.md). |
| Mappatura gerarchica | Durante il processo di assimilazione dei dati è possibile visualizzare l&#39;anteprima di un file di origine gerarchico, ad esempio JSON o Parquet. Per ulteriori informazioni, consulta l’esercitazione sulla [configurazione di un flusso di dati per i connettori di archiviazione cloud nell’interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) . |
| Supporto API per la mappatura nelle origini di streaming | Ora puoi utilizzare le API per eseguire funzioni di mappatura con le origini di streaming. |
| Supporto API per delimitatori personalizzati per le origini di archiviazione cloud | Ora potete raccogliere file non delimitati da CSV utilizzando le origini di archiviazione cloud. Potete utilizzare un carattere di delimitazione di colonna singolo, ad esempio tabulazione, virgola, tubazione, punto e virgola o hash per raccogliere file semplici in qualsiasi formato. |
| Supporto sandbox per connettore Adobe Audience Manager | Il connettore del Audience Manager  ora è in grado di riconoscere la sandbox. Gli utenti possono abilitare il connettore per indirizzare  set di dati di Audience Manager alla sandbox di loro scelta (comprese le sandbox non di produzione). La configurazione è limitata a una sandbox per organizzazione IMS. |
| Miglioramenti UX | L&#39;assimilazione basata su file ora è accessibile tramite il catalogo delle origini. |

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).