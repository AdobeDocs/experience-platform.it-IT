---
keywords: Experience Platform;home;argomenti popolari;servizio catalogo;catalogo;Catalog Service;posizione dati;gestione dei dati;gestione dati;lineage;derivazione;catalogo;abilitare set di dati
solution: Experience Platform
title: Panoramica di Catalog Service
topic-legacy: overview
description: Catalog Service è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Mentre tutti i dati acquisiti in Experience Platform vengono memorizzati nel data lake come file e directory, il servizio Catalog contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca e monitoraggio.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: ht
source-wordcount: '805'
ht-degree: 100%

---

# Panoramica di [!DNL Catalog Service]

[!DNL Catalog Service] è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Mentre tutti i dati acquisiti in [!DNL Experience Platform] vengono memorizzati nel [!DNL Data Lake] come file e directory, [!DNL Catalog] contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca e monitoraggio.

In sintesi, [!DNL Catalog] funge da archivio o “catalogo” di metadati in cui è possibile trovare informazioni sui dati all’interno di [!DNL Experience Platform]. È possibile utilizzare [!DNL Catalog] per rispondere alle seguenti domande:

* Dove si trovano i miei dati?
* In quale fase di elaborazione sono i dati?
* Quali sistemi o processi hanno agito in base ai dati?
* Quanti dati sono stati elaborati correttamente?
* Quali errori si sono verificati durante l’elaborazione?

[!DNL Catalog] fornisce un’API RESTful che consente di gestire in modo programmatico i metadati di [!DNL Platform] mediante operazioni CRUD di base. Per ulteriori informazioni, consulta la [guida per sviluppatori di Catalog](api/getting-started.md).

## Servizi [!DNL Catalog] e [!DNL Experience Platform]

Le risorse di cui [!DNL Catalog Service] tiene traccia vengono utilizzate da diversi servizi di [!DNL Experience Platform]. Per sfruttare al massimo le capacità di [!DNL Catalog's], si consiglia di acquisire familiarità con questi servizi e con il modo in cui interagiscono con [!DNL Catalog].

### Sistema [!DNL Experience Data Model] (XDM) 

Il sistema [!DNL Experience Data Model] (XDM) è il framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull’esperienza del cliente. [!DNL Experience Platform] sfrutta gli schemi XDM per descrivere la struttura dei dati in modo coerente e riutilizzabile.

Quando i dati vengono acquisiti in [!DNL Platform], la struttura di tali dati viene mappata su uno schema XDM e memorizzata all’interno del [!DNL Data Lake] come parte di un set di dati. I metadati per ogni set di dati vengono tracciati da [!DNL Catalog Service], che include un riferimento allo schema XDM a cui è conforme il set di dati.

Per ulteriori informazioni generali sul sistema XDM, consulta la [panoramica del sistema XDM](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] acquisisce dati da più origini e salva i record in modo permanente come set di dati all’interno di [!DNL Data Lake]. [!DNL Catalog] tiene traccia dei metadati per questi set di dati, indipendentemente dalla loro origine o dal loro metodo di acquisizione.

Quando si utilizza il metodo di acquisizione batch, [!DNL Catalog] tiene traccia anche di metadati aggiuntivi per i file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. [!DNL Catalog] tiene traccia dei metadati per i file batch, nonché dei set di dati in cui vengono salvati in modo permanente dopo l’acquisizione. I metadati batch includono informazioni sul numero di record correttamente acquisiti, nonché su eventuali record con errore e sui relativi messaggi di errore.

Per ulteriori informazioni, consulta la [panoramica sull’acquisizione dei dati](../ingestion/home.md).

## Oggetti [!DNL Catalog]

Come descritto nella sezione precedente, [!DNL Catalog] tiene traccia dei metadati per diversi tipi di risorse e operazioni utilizzate da altri servizi [!DNL Platform]. [!DNL Catalog] mantiene il proprio archivio di “oggetti” che incapsulano questi metadati. Gli oggetti [!DNL Catalog] sono rappresentazioni disponibili per query dei dati [!DNL Platform], che consentono di cercare, monitorare ed etichettare i dati senza necessità di accedere ai dati stessi.

La tabella seguente illustra i diversi tipi di oggetti supportati da [!DNL Catalog]:

| Oggetto | Endpoint API | Definizione |
|---|---|---|
| Account | `/accounts` | Durante la creazione delle connessioni di origini, è necessario fornire le credenziali di autenticazione. Un account rappresenta una raccolta di credenziali di autenticazione utilizzate per creare una connessione di un tipo specifico. Ogni connessione dispone di un set di parametri univoci che vengono salvati in modo permanente da [!DNL Catalog] e protetti in un [!DNL Azure Key Vault]. |
| Batch | `/batches` | I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Un oggetto batch in [!DNL Catalog] delinea le metriche di acquisizione del batch (ad esempio il numero di record elaborati o la dimensione su disco) e può includere anche collegamenti a set di dati, viste e altre risorse interessate dall’operazione batch. |
| Connessione | `/connections` | Una connessione è una singola istanza di un connettore di origine, specifica per la tua organizzazione e configurata utilizzando le credenziali di autenticazione appropriate per il tipo di connettore. |
| Connettore  | `/connectors` | I connettori definiscono il modo in cui le connessioni di origini devono raccogliere dati da altre applicazioni di Adobe (come Adobe Analytics e Adobe Audience Manager), da origini di archiviazione cloud di terze parti (ad esempio [!DNL Azure Blob], [!DNL Amazon S3], server FTP e server SFTP) e sistemi CRM di terze parti (come [!DNL Microsoft Dynamics] e [!DNL Salesforce]). |
| Set di dati | `/dataSets` | Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). Per ulteriori informazioni, consulta la [panoramica dei set di dati](./datasets/overview.md). |
| File di set di dati | `/datasetFiles` | I file di set di dati rappresentano blocchi di dati salvati in [!DNL Platform]. Come record di file letterali, è qui che si possono trovare la dimensione del file, il numero di record che contiene e un riferimento al batch con cui è stato acquisito il file. |

## Passaggi successivi

Questo documento fornisce un’introduzione a [!DNL Catalog Service] e come funziona all&#39;interno dell’ambito di applicazione più ampio di [!DNL Experience Platform]. Consulta la [[!DNL Catalog] guida per sviluppatori](api/getting-started.md) per informazioni su come interagire con i diversi endpoint dell’API di [!DNL Catalog]. È consigliabile consultare anche la guida sul [filtraggio dei dati Catalog](api/filter-data.md) e seguire le best practice per limitare i dati restituiti nelle risposte API.
