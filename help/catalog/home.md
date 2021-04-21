---
keywords: Experience Platform;home;argomenti popolari;servizio catalogo;catalogo;servizio catalogo;posizione dati;posizione dati;gestione dati;gestione dati;linea;linea;derivazione;catalogo;abilita set di dati
solution: Experience Platform
title: Panoramica del servizio catalogo
topic-legacy: overview
description: Servizio catalogo è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Mentre tutti i dati acquisiti in Experience Platform vengono memorizzati nel Data Lake come file e directory, Catalog contiene i metadati e la descrizione di tali file e directory a scopo di ricerca e monitoraggio.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# [!DNL Catalog Service]panoramica

[!DNL Catalog Service] è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Mentre tutti i dati acquisiti in [!DNL Experience Platform] vengono memorizzati in [!DNL Data Lake] come file e directory, [!DNL Catalog] contiene i metadati e la descrizione di tali file e directory a scopo di ricerca e monitoraggio.

In poche parole, [!DNL Catalog] funge da archivio di metadati o &quot;catalogo&quot;, dove è possibile trovare informazioni sui dati all&#39;interno di [!DNL Experience Platform]. Puoi utilizzare [!DNL Catalog] per rispondere alle seguenti domande:

* Dove si trovano i miei dati?
* In quale fase del trattamento si trovano questi dati?
* Quali sistemi o processi hanno agito sui miei dati?
* Quanti dati sono stati elaborati correttamente?
* Quali errori si sono verificati durante l&#39;elaborazione?

[!DNL Catalog] fornisce un’API RESTful che consente di gestire programmaticamente  [!DNL Platform] i metadati utilizzando le operazioni CRUD di base. Per ulteriori informazioni, consulta la [Guida per gli sviluppatori del catalogo](api/getting-started.md) .

## [!DNL Catalog] e  [!DNL Experience Platform] servizi

Le risorse che [!DNL Catalog Service] traccia vengono utilizzate da più servizi [!DNL Experience Platform]. Per sfruttare al massimo le funzionalità di [!DNL Catalog's], ti consigliamo di acquisire familiarità con questi servizi e con il modo in cui interagiscono con [!DNL Catalog].

### [!DNL Experience Data Model] Sistema (XDM)

[!DNL Experience Data Model] (XDM) System è il framework standardizzato tramite il quale  [!DNL Platform] organizza i dati sulla customer experience. [!DNL Experience Platform] sfrutta gli schemi XDM per descrivere la struttura dei dati in modo coerente e riutilizzabile.

Quando i dati vengono acquisiti in [!DNL Platform], la struttura di tali dati viene mappata su uno schema XDM e memorizzata all&#39;interno di [!DNL Data Lake] come parte di un set di dati. I metadati per ogni set di dati sono tracciati da [!DNL Catalog Service], che include un riferimento allo schema XDM a cui è conforme il set di dati.

Per informazioni generali sul sistema XDM, vedere la [Panoramica del sistema XDM](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] acquisisce dati da più sorgenti e persiste record come set di dati all’interno di  [!DNL Data Lake]. [!DNL Catalog] tiene traccia dei metadati per questi set di dati, indipendentemente dalla loro origine o dal loro metodo di acquisizione.

Quando si utilizza il metodo di acquisizione batch, [!DNL Catalog] tiene traccia anche dei metadati aggiuntivi per i file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. [!DNL Catalog] tiene traccia dei metadati per questi file batch, nonché dei set di dati in cui vengono mantenuti dopo l’acquisizione. I metadati batch includono informazioni sul numero di record correttamente acquisiti, nonché su eventuali record con errore e relativi messaggi di errore.

Per ulteriori informazioni, consulta la [panoramica sull’acquisizione dei dati](../ingestion/home.md) .

## [!DNL Catalog] oggetti

Come descritto nella sezione precedente, [!DNL Catalog] tiene traccia dei metadati per diversi tipi di risorse e operazioni utilizzate da altri servizi [!DNL Platform]. [!DNL Catalog] mantiene il proprio archivio di &quot;oggetti&quot; che incapsulano questi metadati. [!DNL Catalog] Gli oggetti sono rappresentazioni di  [!DNL Platform] dati interrogabili che consentono di eseguire ricerche, monitorare ed etichettare i dati senza dover accedere ai dati stessi.

La tabella seguente illustra i diversi tipi di oggetti supportati da [!DNL Catalog]:

| Oggetto | Endpoint API | Definizione |
|---|---|---|
| Account | `/accounts` | Durante la creazione delle connessioni di origine, è necessario fornire le credenziali di autenticazione. Un account rappresenta una raccolta di credenziali di autenticazione utilizzate per creare una connessione di un tipo specifico. Ogni connessione dispone di un set di parametri univoci che vengono mantenuti da [!DNL Catalog] e protetti in un [!DNL Azure Key Vault]. |
| Batch | `/batches` | I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Un oggetto batch in [!DNL Catalog] delinea le metriche di acquisizione del batch (come il numero di record elaborati o le dimensioni su disco) e può includere anche collegamenti a set di dati, viste e altre risorse interessate dall&#39;operazione batch. |
| Connessione | `/connections` | Una connessione è una singola istanza di un connettore di origine, univoca per la tua organizzazione e configurata utilizzando le credenziali di autenticazione appropriate per il tipo di connettore. |
| Connettore | `/connectors` | I connettori definiscono il modo in cui le connessioni di origine devono raccogliere dati da altre applicazioni di Adobe (come Adobe Analytics e Adobe Audience Manager), da sorgenti di archiviazione cloud di terze parti (come [!DNL Azure Blob], [!DNL Amazon S3], server FTP e server SFTP) e da sistemi CRM di terze parti (come [!DNL Microsoft Dynamics] e [!DNL Salesforce]). |
| Set di dati | `/dataSets` | Un set di dati è un costrutto di archiviazione e gestione utilizzato per la raccolta di dati (in genere una tabella) che contiene uno schema (colonne) e campi (righe). Per ulteriori informazioni, consulta la [panoramica dei set di dati](./datasets/overview.md) . |
| File set di dati | `/datasetFiles` | I file del set di dati rappresentano blocchi di dati salvati in [!DNL Platform]. Come record di file letterali, questi sono i punti in cui è possibile trovare le dimensioni del file, il numero di record in esso contenuti e un riferimento al batch che ha acquisito il file. |

## Passaggi successivi

Questo documento fornisce un&#39;introduzione a [!DNL Catalog Service] e il suo funzionamento all&#39;interno dell&#39;ambito maggiore di [!DNL Experience Platform]. Consulta la [[!DNL Catalog] guida per sviluppatori](api/getting-started.md) per i passaggi sull&#39;interazione con i diversi endpoint di tale [!DNL Catalog] API. È consigliabile consultare anche la guida sul [filtraggio dei dati del catalogo](api/filter-data.md) per seguire le best practice per limitare i dati restituiti nelle risposte API.
