---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica di Servizio catalogo
topic: overview
translation-type: tm+mt
source-git-commit: 1fce86193bc1660d0f16408ed1b9217368549f6c
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 5%

---


# Panoramica di Servizio catalogo

Catalog Service è il sistema di record per la posizione dei dati e la linea di demarcazione all’interno di Adobe Experience Platform. Anche se tutti i dati acquisiti in Experience Platform sono memorizzati nel Data Lake come file e directory, Catalog contiene i metadati e la descrizione di tali file e directory a scopo di ricerca e monitoraggio.

In breve, Catalog funge da archivio di metadati o &quot;catalogo&quot; in cui potete trovare informazioni sui vostri dati all&#39;interno di Experience Platform. Potete usare Catalog per rispondere alle seguenti domande:

* Dove si trovano i miei dati?
* In quale fase di elaborazione si trovano questi dati?
* Quali sistemi o processi hanno agito sui miei dati?
* Quanti dati sono stati elaborati correttamente?
* Quali errori si sono verificati durante l&#39;elaborazione?

Catalog fornisce un RESTful API che consente di gestire i metadati della piattaforma a livello di programmazione utilizzando le operazioni CRUD di base. Per ulteriori informazioni, consulta la guida [per gli sviluppatori del](api/getting-started.md) catalogo.

## Servizi Catalogo ed Experience Platform

Le risorse monitorate dal servizio Catalog vengono utilizzate da più servizi della piattaforma Experience. Per sfruttare al massimo le funzionalità di Catalog, si consiglia di acquisire familiarità con questi servizi e con come interagiscono con Catalog.

### Sistema XDM (Experience Data Model)

Il sistema XDM (Experience Data Model) è il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente. Experience Platform sfrutta gli schemi XDM per descrivere la struttura dei dati in modo coerente e riutilizzabile.

Quando i dati vengono trasferiti in Piattaforma, la struttura di tali dati viene mappata su uno schema XDM e memorizzata all&#39;interno del Data Lake come parte di un **dataset**. I metadati per ogni set di dati vengono tracciati dal servizio Catalog, che include un riferimento allo schema XDM a cui è conforme il set di dati.

Per ulteriori informazioni generali sul sistema XDM, vedere la panoramica [del sistema](../xdm/home.md)XDM.

### Ingestione dati

Experience Platform acquisisce i dati da più origini e i record persistono come insiemi di dati all&#39;interno del Data Lake. Catalog tiene traccia dei metadati per questi set di dati, indipendentemente dalla loro origine o dal metodo di assimilazione.

Quando si utilizza il metodo di caricamento batch, Catalog tiene traccia anche dei metadati aggiuntivi per i file **batch** . I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Catalog tiene traccia dei metadati per questi file batch, nonché dei set di dati in cui sono persistenti dopo l’assimilazione. I metadati batch includono informazioni sul numero di record acquisiti con successo, nonché eventuali record con errore e messaggi di errore associati.

Per ulteriori informazioni, consulta la panoramica [sull’assimilazione dei](../ingestion/home.md) dati.

## Oggetti del catalogo

Come descritto nella sezione precedente, Catalog tiene traccia dei metadati per diversi tipi di risorse e operazioni che vengono utilizzate da altri servizi della piattaforma. Catalog mantiene un proprio archivio di &quot;oggetti&quot; che racchiude questi metadati. Gli oggetti catalogo sono rappresentazioni interrogabili dei dati della piattaforma che consentono di eseguire ricerche, monitorare ed etichettare i dati senza dover accedere ai dati stessi.

La tabella seguente delinea i diversi tipi di oggetti supportati da Catalog:

| Oggetto | Endpoint API | Definizione |
|---|---|---|
| Account | `/accounts` | Durante la creazione di connessioni di origine, è necessario fornire le credenziali di autenticazione. Un account rappresenta una raccolta di credenziali di autenticazione utilizzate per creare una connessione di un tipo specifico. Ciascuna connessione dispone di un set di parametri univoci persistenti in Catalog e protetti in un insieme di credenziali delle chiavi di Azure. |
| Batch | `/batches` | I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Un oggetto batch in Catalog illustra le metriche di assimilazione del batch (ad esempio il numero di record elaborati o le dimensioni su disco) e può includere anche collegamenti a set di dati, viste e altre risorse interessate dall&#39;operazione batch. |
| Connessione | `/connections` | Una connessione è una singola istanza di un connettore di origine, univoca per la propria organizzazione e configurata utilizzando le credenziali di autenticazione appropriate per il tipo di connettore. |
| Connettore | `/connectors` | I connettori definiscono il modo in cui le connessioni di origine devono raccogliere dati da altre applicazioni Adobe (come Adobe Analytics e Adobe Audience Manager), da origini di archiviazione cloud di terze parti (come Azure Blob, Amazon S3, server FTP e server SFTP) e da sistemi CRM di terze parti (come Microsoft Dynamics e Salesforce). |
| Set di dati | `/dataSets` | Un dataset è un costrutto di storage e gestione utilizzato per la raccolta di dati (in genere una tabella) che contiene uno schema (colonne) e campi (righe). Per ulteriori informazioni, vedere la panoramica [dei](./datasets/overview.md) set di dati. |
| File di set di dati | `/datasetFiles` | I file di set di dati rappresentano blocchi di dati salvati sulla piattaforma. Come record di file letterali, questi sono i punti in cui è possibile trovare la dimensione del file, il numero di record in cui contiene e un riferimento al batch in cui è stato assimilato il file. |

## Passaggi successivi

Questo documento fornisce un&#39;introduzione a Catalog Service e spiega come funziona all&#39;interno dell&#39;ambito più ampio di Experience Platform. Consultate la guida [per gli sviluppatori del](api/getting-started.md) catalogo per i passaggi sull&#39;interazione con i diversi endpoint di tale API del catalogo. Si consiglia inoltre di fare riferimento alla guida sul [filtro dei dati](api/filter-data.md) catalogo per seguire le procedure ottimali per limitare i dati restituiti nelle risposte API.