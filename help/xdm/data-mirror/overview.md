---
keywords: Experience Platform;mirroring dati;schema relazionale;cambiare acquisizione dati;sincronizzazione database;chiave primaria;relazioni;;data mirror;relational schema;change data capture;database sync;primary key;relations
solution: Experience Platform
title: Panoramica di Data Mirror
description: Scopri come Data Mirror consente l’acquisizione delle modifiche a livello di riga dai database esterni in Adobe Experience Platform utilizzando schemi relazionali con univocità, relazioni e controllo delle versioni applicate.
badge: Disponibilità limitata
exl-id: bb92c77a-6c7a-47df-885a-794cf55811dd
source-git-commit: 57981d2e4306b2245ce0c1cdd9f696065c508a1d
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 0%

---

# Panoramica di Data Mirror

>[!AVAILABILITY]
>
>Data Mirror e gli schemi relazionali sono disponibili per i titolari di licenze di **Campagne orchestrate** Adobe Journey Optimizer. Sono disponibili anche come **versione limitata** per gli utenti di Customer Journey Analytics, a seconda della licenza e dell&#39;abilitazione della funzione. Contatta il tuo rappresentante Adobe per accedere.

>[!NOTE]
>
>Nelle versioni precedenti della documentazione di Adobe Experience Platform, gli schemi relazionali erano precedentemente denominati schemi basati su modelli. La funzionalità rimane invariata.

Data Mirror è una funzionalità di Adobe Experience Platform che consente l’acquisizione delle modifiche a livello di riga dai database esterni nel data lake utilizzando schemi relazionali. Mantiene le relazioni tra i dati, applica l’univocità e supporta il controllo delle versioni senza richiedere processi ETL (Extract, Transform, Load) a monte.

Utilizzare Data Mirror per sincronizzare inserimenti, aggiornamenti ed eliminazioni (dati mutabili) da sistemi esterni come [!DNL Snowflake], [!DNL Databricks] o [!DNL BigQuery] direttamente in Experience Platform. In questo modo è possibile preservare la struttura del modello di database esistente e l’integrità dei dati durante l’inserimento dei dati in Platform.

## Funzionalità e vantaggi

Data Mirror offre le seguenti funzionalità essenziali per la sincronizzazione del database:

* **Applicazione della chiave primaria**: assicura l&#39;univocità all&#39;interno dei set di dati e impedisce la duplicazione dei record durante l&#39;acquisizione.
* **Acquisizione delle modifiche a livello di riga**: supporta le modifiche granulari dei dati, inclusi gli upsert e le eliminazioni, con controllo di precisione.
* **Relazioni schema**: abilita le relazioni chiave primaria ed esterna tra i set di dati tramite descrittori.
* **Gestione eventi fuori servizio**: elabora gli eventi di modifica utilizzando i descrittori di versione e marca temporale, anche quando non sono in sequenza.
* **Integrazione warehouse diretta**: si connette con data warehouse cloud supportati per sincronizzare le modifiche quasi in tempo reale.

Utilizza Data Mirror per acquisire le modifiche direttamente dai sistemi di origine, applicare l’integrità dello schema e rendere i dati disponibili per le attività di analisi, orchestrazione del percorso e flussi di lavoro di conformità. Data Mirror elimina i complessi processi ETL a monte e accelera l&#39;implementazione consentendo il mirroring diretto dei modelli di database esistenti.

Pianifica i requisiti di eliminazione e igiene dei dati durante l’implementazione di schemi relazionali con Data Mirror. Tutte le applicazioni devono considerare in che modo le eliminazioni influiscono sui set di dati correlati, sui flussi di lavoro di conformità e sui processi a valle prima della distribuzione.

## Prerequisiti {#prerequisites}

Prima di iniziare, è necessario comprendere i seguenti componenti di Experience Platform e verificare che l’ambiente soddisfi i requisiti tecnici e strutturali:

* [Creare schemi nell&#39;interfaccia utente di Experience Platform](../ui/resources/schemas.md) o [API](../api/schemas.md)
* [Configurare le connessioni di origine cloud](../../sources/home.md#cloud-storage)
* [Applica concetti di acquisizione dati di modifica](../../sources/tutorials/api/change-data-capture.md) (upsert, deletes)
* Distinguere tra [standard](../schema/composition.md) e [schemi relazionali](../schema/relational.md)
* [Definire le relazioni strutturali con i descrittori](../api/descriptors.md)

### Requisiti di implementazione

L’istanza di Platform e i dati di origine devono soddisfare requisiti specifici affinché Data Mirror funzioni correttamente. Data Mirror richiede **schemi relazionali**, che sono strutture di dati flessibili con vincoli imposti.

Includi **chiave primaria e descrittore di versione** in tutti gli schemi. Se utilizzi uno schema di serie temporali, è necessario anche un descrittore **timestamp**.

Il database esterno deve supportare l&#39;acquisizione dei dati di modifica o fornire metadati che identifichino inserimenti, aggiornamenti ed eliminazioni. I dati di Source devono includere **identificatori univoci**, un singolo campo o una chiave primaria composita e **informazioni sulla versione** in modo che il sistema possa applicare gli aggiornamenti nell&#39;ordine corretto.

Per rilevare le eliminazioni, aggiungere una colonna `_change_request_type` che specifichi se ogni record è un upsert o un&#39;eliminazione.

## Implementare Data Mirror {#implementation-workflow}

A differenza degli approcci di acquisizione standard, Data Mirror mantiene la struttura del modello di database all’interno del data lake di Experience Platform. Questa coerenza della struttura dati elimina la necessità di pre-elaborazione esterna. Di seguito è riportato un flusso di lavoro di alto livello per l’implementazione di Data Mirror. Scegli il metodo di implementazione in base al flusso di lavoro del team e al sistema di origine.

### Definire la struttura dello schema

Crea [schemi relazionali](../schema/relational.md) con i descrittori richiesti (metadati che definiscono il comportamento e i vincoli dello schema). Scegli un metodo che si adatti al flusso di lavoro del team, sia tramite l’interfaccia utente che direttamente tramite l’API.

* **Approccio dell&#39;interfaccia utente**: [Creare schemi relazionali nell&#39;Editor schema](../ui/resources/schemas.md#create-relational-schema)
* **Approccio API**: [Creare schemi tramite API Registro schemi](../api/schemas.md#create-relational-schema)

### Mappare le relazioni e definire la gestione dei dati

Definisci le connessioni tra i set di dati utilizzando i descrittori di relazione. Gestisci le relazioni e mantieni la qualità dei dati nei diversi set di dati. Queste attività garantiscono join coerenti e supportano la conformità ai requisiti di igiene dei dati.

* **Relazioni schema**: [Definire le relazioni tra i set di dati utilizzando i descrittori](../api/descriptors.md)
* **Igiene dei record**: [Gestisci eliminazioni record di precisione per set di dati basati su schemi relazionali](../../hygiene/ui/record-delete.md#relational-record-delete)

### Configurare la connessione sorgente

Seleziona un metodo di acquisizione in base al sistema di origine e al caso d’uso. Ogni opzione supporta diversi livelli di automazione, trasformazione e scalabilità.

* [**Configurare le connessioni di origine cloud**](../../sources/home.md#cloud-storage)
* **Acquisizione SQL**: utilizza Data Distiller per scrivere in set di dati relazionali
* [**Caricamento file**](../ui/resources/schemas.md#upload-ddl-file): carica i file manualmente per l&#39;acquisizione in batch o occasionale

### Abilita acquisizione Change Data Capture

Imposta le connessioni di Change Data Capture con i data warehouse cloud supportati. Acquisisci le modifiche a livello di riga mantenendo l’univocità e applicando gli aggiornamenti nell’ordine corretto.

* **Modifica acquisizione dati**: [Abilita modifica acquisizione dati nelle connessioni di origine](../../sources/tutorials/api/change-data-capture.md)

## Casi d’uso comuni {#use-cases}

Esamina i casi d’uso comuni elencati di seguito in cui Data Mirror supporta la sincronizzazione precisa dei dati e la conservazione delle relazioni. Ogni scenario mostra come Data Mirror supporta le esigenze aziendali comuni in termini di analisi, orchestrazione e conformità.

### Modellazione dati relazionali

Utilizzare [schemi relazionali](../schema/relational.md) in Data Mirror per rappresentare entità, inserire, aggiornare ed eliminare elementi a livello di riga e mantenere le relazioni chiave primaria ed esterna esistenti nelle origini dati. Questo approccio porta i principi di modellazione dei dati relazionali in Experience Platform e garantisce la coerenza strutturale tra i diversi set di dati.

### Sincronizzazione da magazzino a lago

Esegui il mirroring dei dati dell’evento, dei registri di interazione con il cliente, degli eventi delle campagne e dei dati ausiliari dai data warehouse cloud supportati in Experience Platform. Questo supporta l’idoneità della campagna, la precisione del targeting e la sequenza dei messaggi. Journey Optimizer e Real-Time CDP B2B si basano su questo per una logica di orchestrazione quasi in tempo reale.

### Integrazione con Customer Journey Analytics

Sincronizza gli eventi della serie temporale come clic sul web, visualizzazioni di prodotti, acquisti e interazioni di supporto da sistemi come call center o registri di chat. Una cronologia completa delle modifiche supporta un’analisi accurata delle tendenze e una segmentazione comportamentale. Experience Platform Data Mirror for Customer Journey Analytics lo utilizza per riflettere gli upsert e le eliminazioni dai sistemi di origine.

### Modellazione delle relazioni B2B

Mantenere relazioni quali le gerarchie account-contatto, abbonamento-account o contatto-area. Questi supportano la segmentazione, il punteggio di lead, il tracciamento delle opportunità e la coordinazione multicanale. A differenza dell’acquisizione standard che appiattisce le relazioni, Data Mirror le mantiene in modalità nativa utilizzando i descrittori per una modellazione più accurata.

### Gestione abbonamenti

Tieni traccia di eventi quali rinnovi, annullamenti, aggiornamenti, downgrade e modifiche del piano con la cronologia completa delle versioni. Questo supporta campagne di conservazione, previsione di abbandono e segmentazione basata sul ciclo di vita. La cronologia completa consente approfondimenti comportamentali e un targeting preciso.

### Operazioni di igiene dei dati

Utilizza l’acquisizione dei dati di modifica per consentire eliminazioni precise a livello di record per conformità (ad esempio, settori regolamentati) e flussi di lavoro di pulizia. Data Mirror applica le eliminazioni in modo preciso, conservando al contempo i dati correlati tra i set di dati connessi.

## Considerazioni importanti {#considerations}

Esamina queste considerazioni chiave per garantire che l’implementazione sia allineata ai comportamenti di schema, ai metodi di acquisizione e ai modelli di relazione supportati. Una corretta pianificazione consente di evitare problemi di integrazione e garantisce una modellazione accurata dei dati.

### Requisiti per la cancellazione dei dati e l’igiene

Tutte le applicazioni che utilizzano schemi relazionali e Data Mirror devono comprendere le implicazioni relative all’eliminazione dei dati. Gli schemi relazionali consentono eliminazioni precise a livello di record che possono influire sui dati correlati tra i set di dati connessi. Queste funzionalità di eliminazione influiscono sull’integrità dei dati, sulla conformità e sul comportamento delle applicazioni a valle, indipendentemente dal caso d’uso specifico. Rivedi [requisiti di igiene dei dati per i set di dati basati su schemi relazionali](../../hygiene/ui/record-delete.md#relational-record-delete) e pianifica gli scenari di eliminazione prima dell&#39;implementazione.

### Selezione del comportamento dello schema

Per impostazione predefinita, gli schemi relazionali presentano il comportamento **record**, che acquisisce lo stato dell&#39;entità (clienti, account, ecc.). Se hai bisogno di **comportamento della serie temporale** per il tracciamento degli eventi, devi configurarlo esplicitamente.

### Confronto dei metodi di acquisizione

Utilizzare questa tabella di confronto per scegliere il metodo di acquisizione più adatto alle proprie esigenze di dati, che si tratti di sincronizzazione in tempo reale, trasformazione basata su SQL o caricamento manuale di file.

| Metodo di acquisizione | Caso d’uso |
| ----------------------- | -------------------------------------------------------------- |
| **Cambia acquisizione dati** | Sincronizzazione in tempo reale da warehouse cloud supportati |
| **Distiller dati** | Flussi di lavoro di acquisizione e trasformazione basati su SQL |
| **Caricamento file** | Acquisizione in batch/manuale quando l’integrazione sorgente non è disponibile |

### Limitazioni delle relazioni

Data Mirror supporta **relazioni uno-a-uno** e **molti-a-uno** tramite descrittori. **Le relazioni molti-a-molti** richiedono una modellazione aggiuntiva e non sono supportate direttamente.

## Passaggi successivi

Dopo aver esaminato questa panoramica, dovresti essere in grado di determinare se Data Mirror si adatta al tuo caso d’uso e comprendere i requisiti per l’implementazione. Per iniziare:

1. **Gli architetti di dati** devono valutare il modello di dati per assicurarsi che supporti le chiavi primarie, il controllo delle versioni e le funzionalità di rilevamento delle modifiche.
2. **Le parti interessate** devono confermare che la licenza include il supporto per schemi relazionali e le edizioni Experience Platform richieste.
3. **I progettisti di schemi** devono pianificare la struttura dello schema per identificare i descrittori richiesti, le relazioni tra i campi e le esigenze di governance dei dati.
4. **I team di implementazione** devono scegliere un metodo di acquisizione basato sui sistemi di origine, sui requisiti in tempo reale e sui flussi di lavoro operativi.

Per informazioni dettagliate sull&#39;implementazione, consulta la [documentazione sugli schemi relazionali](../schema/relational.md).
