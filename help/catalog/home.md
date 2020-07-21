---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica di Servizio catalogo
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 6%

---


# [!DNL Catalog Service]panoramica

[!DNL Catalog Service] è il sistema di record per la posizione dei dati e la linea all&#39;interno  Adobe Experience Platform. Anche se tutti i dati in cui [!DNL Experience Platform] viene effettuato il caricamento vengono memorizzati [!DNL Data Lake] come file e directory, [!DNL Catalog] contiene i metadati e la descrizione di tali file e directory a scopo di ricerca e monitoraggio.

In poche parole, [!DNL Catalog] funge da archivio di metadati o &quot;[!UICONTROL catalog]&quot; per trovare informazioni sui dati all&#39;interno [!DNL Experience Platform]. Potete usare [!DNL Catalog] per rispondere alle seguenti domande:

* Dove si trovano i miei dati?
* In quale fase di elaborazione si trovano questi dati?
* Quali sistemi o processi hanno agito sui miei dati?
* Quanti dati sono stati elaborati correttamente?
* Quali errori si sono verificati durante l&#39;elaborazione?

[!DNL Catalog] fornisce un RESTful API che consente di gestire [!DNL Platform] i metadati a livello di programmazione utilizzando le operazioni CRUD di base. Per ulteriori informazioni, consulta la guida [per gli sviluppatori del](api/getting-started.md) catalogo.

## [!DNL Catalog] e [!DNL Experience Platform] servizi

Le risorse che [!DNL Catalog Service] tengono traccia vengono utilizzate da più [!DNL Experience Platform] servizi. Per sfruttare al massimo [!DNL Catalog's] le funzionalità, si consiglia di acquisire familiarità con questi servizi e con come interagiscono con [!DNL Catalog].

### [!DNL Experience Data Model] Sistema (XDM)

[!DNL Experience Data Model] (XDM) Il sistema è il framework standardizzato tramite il quale [!DNL Platform] vengono organizzati i dati sull&#39;esperienza del cliente. [!DNL Experience Platform] sfrutta gli schemi XDM per descrivere la struttura dei dati in modo coerente e riutilizzabile.

Quando i dati vengono assimilati in [!DNL Platform], la struttura di tali dati viene mappata su uno schema XDM e memorizzata all&#39;interno del [!DNL Data Lake] set di **dati**. I metadati per ogni dataset vengono tracciati da [!DNL Catalog Service], che include un riferimento allo schema XDM a cui è conforme il dataset.

Per ulteriori informazioni generali sul sistema XDM, vedere la panoramica [del sistema](../xdm/home.md)XDM.

### [!DNL Data Ingestion]

[!DNL Experience Platform] acquisisce i dati da più origini e persiste come insiemi di dati all&#39;interno dell&#39; [!DNL Data Lake]. [!DNL Catalog] tiene traccia dei metadati per questi set di dati, indipendentemente dalla loro origine o dal metodo di assimilazione.

Quando si utilizza il metodo di assimilazione batch, [!DNL Catalog] vengono inoltre tracciati i metadati aggiuntivi per i file **batch** . I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. [!DNL Catalog] tiene traccia dei metadati per questi file batch, nonché dei set di dati in cui sono persistenti dopo l’assimilazione. I metadati batch includono informazioni sul numero di record acquisiti con successo, nonché eventuali record con errore e messaggi di errore associati.

Per ulteriori informazioni, consulta la panoramica [sull’assimilazione dei](../ingestion/home.md) dati.

## [!DNL Catalog] objects

Come descritto nella sezione precedente, [!DNL Catalog] tiene traccia dei metadati relativi a diversi tipi di risorse e operazioni utilizzate da altri [!DNL Platform] servizi. [!DNL Catalog] mantiene un proprio archivio di &quot;oggetti&quot; che racchiudono questi metadati. [!DNL Catalog] gli oggetti sono rappresentazioni di [!DNL Platform] dati interrogabili che consentono di eseguire ricerche, monitorare ed etichettare i dati senza dover accedere ai dati stessi.

La tabella seguente delinea i diversi tipi di oggetti supportati da [!DNL Catalog]:

| Oggetto | Endpoint API | Definizione |
|---|---|---|
| Account | `/accounts` | Durante la creazione di connessioni di origine, è necessario fornire le credenziali di autenticazione. Un account rappresenta una raccolta di credenziali di autenticazione utilizzate per creare una connessione di un tipo specifico. Ogni connessione ha un insieme di parametri univoci che sono persistenti da [!DNL Catalog] e protetti in un [!DNL Azure Key Vault]. |
| Batch | `/batches` | I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Un oggetto batch in [!DNL Catalog] descrive le metriche di assimilazione del batch (come il numero di record elaborati o le dimensioni su disco) e può includere anche collegamenti a set di dati, viste e altre risorse interessate dall&#39;operazione batch. |
| Connessione | `/connections` | Una connessione è una singola istanza di un connettore di origine, univoca per la propria organizzazione e configurata utilizzando le credenziali di autenticazione appropriate per il tipo di connettore. |
| Connettore | `/connectors` | I connettori definiscono il modo in cui le connessioni di origine devono raccogliere dati da altre applicazioni Adobe (come Adobe  Analytics e  Adobe Audience Manager), da origini di archiviazione cloud di terze parti (come [!DNL Azure Blob], server [!DNL Amazon S3], server FTP e server SFTP) e da sistemi CRM di terze parti (come [!DNL Microsoft Dynamics] e [!DNL Salesforce]). |
| Set di dati | `/dataSets` | Un dataset è un costrutto di storage e gestione utilizzato per la raccolta di dati (in genere una tabella) che contiene uno schema (colonne) e campi (righe). Per ulteriori informazioni, vedere la panoramica [dei](./datasets/overview.md) set di dati. |
| File di set di dati | `/datasetFiles` | I file di set di dati rappresentano blocchi di dati salvati in [!DNL Platform]. Come record di file letterali, questi sono i punti in cui è possibile trovare la dimensione del file, il numero di record in cui contiene e un riferimento al batch in cui è stato assimilato il file. |

## Passaggi successivi

Questo documento ha fornito un&#39;introduzione a [!DNL Catalog Service] e come funziona all&#39;interno dell&#39;ambito maggiore di [!DNL Experience Platform]. Consultate la guida [per gli sviluppatori del](api/getting-started.md) catalogo per i passaggi sull&#39;interazione con i diversi endpoint di tale [!DNL Catalog] API. Si consiglia inoltre di fare riferimento alla guida sul [filtro dei dati](api/filter-data.md) catalogo per seguire le procedure ottimali per limitare i dati restituiti nelle risposte API.