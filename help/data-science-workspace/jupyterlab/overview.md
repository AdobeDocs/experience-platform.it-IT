---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Guida utente di JupyterLab
topic: Overview
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '3349'
ht-degree: 5%

---


# Guida utente di JupyterLab

JupyterLab è un&#39;interfaccia utente basata sul Web per <a href="https://jupyter.org/" target="_blank">Project Jupyter</a> ed è strettamente integrata in [!DNL Adobe Experience Platform]. Fornisce un ambiente di sviluppo interattivo che consente agli scienziati dei dati di lavorare con notebook, codice e dati Jupyter.

Questo documento fornisce una panoramica di JupyterLab e delle sue funzioni, oltre alle istruzioni per eseguire azioni comuni.

## JupyterLab sulla piattaforma Experience

L&#39;integrazione JupyterLab della Experience Platform è accompagnata da modifiche architettoniche, considerazioni di progettazione, estensioni personalizzate dei notebook, librerie preinstallate e un&#39;interfaccia a tema Adobe.

L&#39;elenco seguente illustra alcune delle funzioni esclusive di JupyterLab sulla piattaforma:

| Funzione | Descrizione |
| --- | --- |
| **Kernel** | I kernel forniscono ai notebook e ad altri front-end JupyterLab la possibilità di eseguire e analizzare il codice in diversi linguaggi di programmazione. Experience Platform fornisce ulteriori kernel per supportare lo sviluppo in Python, R, PySpark e Spark. Per ulteriori dettagli, consulta la sezione [kernel](#kernels) . |
| **Accesso ai dati** | Accedete ai set di dati esistenti direttamente da JupyterLab con il supporto completo per le funzionalità di lettura e scrittura. |
| **Integrazione del servizio piattaforma** | Le integrazioni integrate consentono di utilizzare altri servizi della piattaforma direttamente da JupyterLab. Un elenco completo delle integrazioni supportate è disponibile nella sezione [Integrazione con altri servizi](#service-integration)della piattaforma. |
| **Autenticazione** | Oltre al modello <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">di sicurezza integrato di</a>JupyterLab, ogni interazione tra l&#39;applicazione e la piattaforma Experience Platform, inclusa la comunicazione tra i servizi della piattaforma, viene crittografata e autenticata tramite <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Librerie di Sviluppo** | In Experience Platform, JupyterLab offre librerie preinstallate per Python, R e PySpark. Consultate l&#39; [appendice](#supported-libraries) per un elenco completo delle librerie supportate. |
| **Controller libreria** | Se le librerie preinstallate non sono adatte alle vostre esigenze, è possibile installare librerie aggiuntive per Python e R e memorizzare temporaneamente in contenitori isolati per mantenere l&#39;integrità della Piattaforma e proteggere i dati. Per ulteriori dettagli, consulta la sezione [kernel](#kernels) . |

>[!NOTE] Le librerie aggiuntive sono disponibili solo per la sessione in cui sono state installate. È necessario reinstallare tutte le librerie aggiuntive necessarie all&#39;avvio delle nuove sessioni.

## Integrazione con altri servizi della piattaforma {#service-integration}

Standardizzazione e interoperabilità sono concetti chiave della piattaforma Experience. L&#39;integrazione di JupyterLab sulla piattaforma come IDE integrato consente di interagire con altri servizi della piattaforma, consentendoti di utilizzare la piattaforma al massimo potenziale. I seguenti servizi della piattaforma sono disponibili in JupyterLab:

* **Servizio catalogo:** Accesso ed esplorazione di set di dati con funzionalità di lettura e scrittura.
* **Servizio query:** Accesso ed esplorazione di dataset utilizzando SQL, fornendo costi generali di accesso ai dati inferiori quando si tratta di grandi quantità di dati.
* **Sensei ML Framework:** Sviluppo di modelli con la capacità di formare e valutare i dati, nonché creazione di ricette con un solo clic.

>[!NOTE] Alcune integrazioni dei servizi della piattaforma su JupyterLab sono limitate a specifici kernel. Per ulteriori informazioni, consulta la sezione sui [kernel](#kernels) .

## Funzioni principali e operazioni comuni

Le informazioni sulle caratteristiche chiave di JupyterLab e le istruzioni sulle operazioni comuni sono fornite nelle sezioni seguenti:

* [Access JupyterLab](#access-jupyterlab)
* [Interfaccia JupyterLab](#jupyterlab-interface)
* [Celle di codice](#code-cells)
* [Kernel](#kernels)
* [Sessioni kernel](#kernel-sessions)
* [Risorsa di esecuzione PySpark/Spark](#execution-resource)
* [Launcher](#launcher)

### Access JupyterLab {#access-jupyterlab}

In [Adobe Experience Platform](https://platform.adobe.com), seleziona **Notebook** dalla colonna di navigazione a sinistra. Lasciare un po&#39; di tempo per l&#39;inizializzazione completa di JupyterLab.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### Interfaccia JupyterLab {#jupyterlab-interface}

L&#39;interfaccia JupyterLab è composta da una barra dei menu, una barra laterale sinistra comprimibile e l&#39;area di lavoro principale contenente schede di documenti e attività.

**Barra dei menu**

Nella barra dei menu nella parte superiore dell&#39;interfaccia sono disponibili menu di livello principale che mostrano le azioni disponibili in JupyterLab con le relative scelte rapide da tastiera:

* **File:** Azioni relative a file e directory
* **Modifica:** Azioni relative alla modifica di documenti e altre attività
* **Visualizza:** Azioni che modificano l’aspetto di JupyterLab
* **Esegui:** Azioni per l’esecuzione di codice in diverse attività, ad esempio blocchi appunti e console di codice
* **Kernel:** Azioni per la gestione dei kernel
* **Schede:** Elenco di documenti e attività aperti
* **Impostazioni:** Impostazioni comuni e un editor di impostazioni avanzato
* **Aiuto:** Elenco dei collegamenti della guida di JupyterLab e del kernel

**Barra laterale sinistra**

La barra laterale sinistra contiene schede selezionabili che consentono di accedere alle seguenti funzioni:

* **Browser file:** Elenco dei documenti e delle directory del blocco appunti salvati
* **Esploratore dati:** Sfogliare, accedere ed esplorare dataset e schemi
* **Canali e terminali in esecuzione:** Un elenco di sessioni attive del kernel e del terminale con la possibilità di terminare
* **Comandi:** Un elenco di comandi utili
* **Controllo celle:** Editor di celle che consente di accedere a strumenti e metadati utili per impostare un blocco appunti a scopo di presentazione
* **schede:** Un elenco di schede aperte

Fate clic su una scheda per visualizzarne le caratteristiche, oppure fate clic su una scheda espansa per comprimere la barra laterale sinistra come illustrato di seguito:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Area di lavoro principale**

L&#39;area di lavoro principale di JupyterLab consente di disporre documenti e altre attività in pannelli di schede che possono essere ridimensionati o suddivisi in due parti. Trascinare una scheda al centro di un pannello di tabulazione per migrare la scheda. Per dividere un pannello, trascinate una scheda a sinistra, a destra, in alto o in basso nel pannello:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Celle di codice {#code-cells}

Le celle di codice sono il contenuto principale dei blocchi appunti. Contengono codice sorgente nella lingua del kernel associato al notebook e l&#39;output come risultato dell&#39;esecuzione della cella di codice. Viene visualizzato un conteggio di esecuzione a destra di ogni cella di codice che rappresenta il relativo ordine di esecuzione.

![](../images/jupyterlab/user-guide/code_cell.png)

Di seguito sono descritte le azioni comuni delle celle:

* **Aggiungere una cella:** Fare clic sul simbolo più (**+**) dal menu del blocco appunti per aggiungere una cella vuota. Le nuove celle vengono posizionate sotto la cella con la quale è in corso l&#39;interazione oppure alla fine del blocco appunti, se non è attiva alcuna cella particolare.

* **Spostare una cella:** Posizionare il cursore a destra della cella che si desidera spostare, quindi fare clic e trascinare la cella in una nuova posizione. Inoltre, lo spostamento di una cella da un blocco appunti a un altro replica la cella con il relativo contenuto.

* **Eseguire una cella:** Fare clic sul corpo della cella che si desidera eseguire, quindi fare clic sull&#39;icona di **riproduzione** (**▶**) dal menu del blocco appunti. Un asterisco (**\***) viene visualizzato nel contatore di esecuzione della cella quando il kernel sta elaborando l&#39;esecuzione e viene sostituito con un numero intero al termine.

* **Eliminare una cella:** Fare clic sul corpo della cella che si desidera eliminare, quindi fare clic sull&#39;icona **forbici** .

### Kernel {#kernels}

I kernel per notebook sono i motori informatici specifici per la lingua per l&#39;elaborazione delle celle per notebook. Oltre a Python, JupyterLab offre supporto linguistico aggiuntivo in R, PySpark e Spark. Quando si apre un documento del blocco appunti, viene avviato il kernel associato. Quando viene eseguita una cella del blocco appunti, il kernel esegue il calcolo e produce risultati che possono richiedere notevoli risorse di CPU e di memoria. Tenere presente che la memoria allocata non viene liberata fino alla chiusura del kernel.

>[!IMPORTANT] JupyterLab Launcher aggiornato da Spark 2.3 a Spark 2.4. I kernel Spark e PySpark non sono più supportati nei notebook Spark 2.4.

Alcune caratteristiche e funzionalità sono limitate a specifici kernel come descritto nella tabella seguente:

| Kernel | Supporto per l&#39;installazione della libreria | Integrazioni di piattaforme |
| :----: | :--------------------------: | :-------------------- |
| **Python** | Sì | <ul><li>Sensei ML Framework</li><li>Servizio catalogo</li><li>Servizio query</li></ul> |
| **R** | Sì | <ul><li>Sensei ML Framework</li><li>Servizio catalogo</li></ul> |
| **PySpark - obsoleto** | No | <ul><li>Sensei ML Framework</li><li>Servizio catalogo</li></ul> |
| **Spark - obsoleto** | No | <ul><li>Sensei ML Framework</li><li>Servizio catalogo</li></ul> |
| **Scala** | No | <ul><li>Sensei ML Framework</li><li>Servizio catalogo</li></ul> |

### Sessioni kernel {#kernel-sessions}

Ogni blocco appunti o attività attiva su JupyterLab utilizza una sessione del kernel. Tutte le sessioni attive si trovano espandendo la scheda Terminali **in esecuzione e kernel** dalla barra laterale sinistra. Il tipo e lo stato del kernel di un notebook possono essere identificati osservando l&#39;interfaccia superiore destra del notebook. Nel diagramma seguente, il kernel associato al notebook è **Python 3** e lo stato corrente è rappresentato da un cerchio grigio a destra. Un cerchio vuoto implica un kernel inattivo e un cerchio pieno implica un kernel occupato.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Se il kernel è spento o inattivo per un periodo prolungato, allora **nessun kernel!** con un cerchio pieno viene visualizzato. Attivate un kernel facendo clic sullo stato del kernel e selezionando il tipo di kernel appropriato come mostrato di seguito:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Risorsa di esecuzione PySpark/Spark {#execution-resource}

>[!IMPORTANT]
>Con la transizione da Spark 2.3 a Spark 2.4, entrambi i kernel Spark e PySpark sono obsoleti.
>
>I nuovi notebook PySpark 3 (Spark 2.4) utilizzano il kernel Python3. Consulta la guida sulla conversione di [Pyspark 3 (Spark 2.3) in PySpark 3 (Spark 2.4)](../recipe-notebook-migration.md) per un&#39;esercitazione approfondita sull&#39;aggiornamento dei notebook esistenti.
>
>I nuovi notebook Spark dovrebbero utilizzare il kernel Scala. Consulta la guida sulla conversione da [Spark 2.3 a Scala (Spark 2.4)](../recipe-notebook-migration.md) per un&#39;esercitazione approfondita sull&#39;aggiornamento dei notebook esistenti.

I kernel PySpark e Spark consentono di configurare le risorse del cluster Spark all&#39;interno del notebook PySpark o Spark utilizzando il comando di configurazione (`%%configure`) e fornendo un elenco di configurazioni. Idealmente, queste configurazioni vengono definite prima dell&#39;inizializzazione dell&#39;applicazione Spark. La modifica delle configurazioni mentre l&#39;applicazione Spark è attiva richiede un flag di forza aggiuntivo dopo il comando (`%%configure -f`), che riavvierà l&#39;applicazione per applicare le modifiche, come illustrato di seguito:

>[!CAUTION]
>Con i notebook PySpark 3 (Spark 2.4) e Scala (Spark 2.4), non `%%` è più supportato lo scintillio. Non è più possibile utilizzare le operazioni seguenti:
* `%%help`
* `%%info`
* `%%cleanup`
* `%%delete`
* `%%configure`
* `%%local`

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

Tutte le proprietà configurabili sono elencate nella tabella seguente:

| Proprietà | Descrizione | Tipo |
| :------- | :---------- | :-----:|
| tipo | Il tipo di sessione (richiesto) | `session kind`_ |
| proxyUser | L&#39;utente da rappresentare che eseguirà la sessione (ad esempio, bob) | string |
| barattoli | File da inserire nella Java `classpath` | elenco di percorsi |
| pyFiles | I file da inserire nel pannello `PYTHONPATH` | elenco di percorsi |
| files | File da inserire nella directory di lavoro dell&#39;esecutore | elenco di percorsi |
| driverMemory | Memoria per driver in megabyte o gigabyte (ad esempio 1000M, 2G) | string |
| driverCores | Numero di core utilizzati dal driver (solo modalità YARN) | int |
| esecutoreMemory | Memoria per esecutore in megabyte o gigabyte (ad esempio 1000M, 2G) | string |
| esecutoreCores | Numero di core utilizzati dall&#39;esecutore | int |
| numExecutor | Numero di esecutori (solo in modalità YARN) | int |
| archives | Archivi da non comprimere nella directory di lavoro dell&#39;esecutore (solo in modalità YARN) | elenco di percorsi |
| queue | La coda YARN a cui inviare (solo in modalità YARN) | string |
| nome | Nome della domanda | string |
| conf | Spark, proprietà di configurazione | Mappa di key=val |

### Launcher {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Il modulo *Launcher* personalizzato offre utili modelli per notebook per i kernel supportati, che consentono di avviare rapidamente l&#39;attività, tra cui:

| Modello | Descrizione |
| --- | --- |
| Vuoto | Un file di blocco appunti vuoto. |
| Starter | Un blocco appunti precompilato che illustra l&#39;esplorazione dei dati utilizzando dati di esempio. |
| Vendite al dettaglio | Un blocco appunti precompilato con ricetta <a href="https://adobe.ly/2wOgO3L" target="_blank">vendite</a> al dettaglio utilizzando dati di esempio. |
| Generatore di ricette | Modello per notebook per la creazione di una ricetta in JupyterLab. È precompilato con codice e commenti che mostrano e descrivono il processo di creazione delle ricette. Per informazioni dettagliate, fare riferimento al <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">notebook per l&#39;esercitazione</a> sulle ricette. |
| Servizio query | Un blocco appunti precompilato che illustra l&#39;utilizzo di Query Service direttamente in JupyterLab con flussi di lavoro di esempio forniti che analizzano i dati in scala. |
| Eventi XDM | Un blocco appunti precompilato che illustra l&#39;esplorazione dei dati relativi ai dati degli eventi di post-valore, con particolare attenzione alle funzioni comuni all&#39;intera struttura di dati. |
| Query XDM | Un blocco appunti precompilato che illustra le query aziendali di esempio sui dati dell&#39;evento esperienza. |
| Aggregazione | Un notebook precompilato che illustra i flussi di lavoro campione per aggregare grandi quantità di dati in blocchi più piccoli e gestibili. |
| Clustering | Un blocco appunti precompilato che illustra il processo di modellazione end-to-end dell&#39;apprendimento automatico utilizzando gli algoritmi di clustering. |

Alcuni modelli per notebook sono limitati a determinati kernel. La disponibilità del modello per ciascun kernel è mappata nella seguente tabella:

<table>
    <tr>
        <td></td>
        <th><strong>Vuoto</strong></th>
        <th><strong>Starter</strong></th>
        <th><strong>Vendite al dettaglio</strong></th>
        <th><strong>Generatore di ricette</strong></th>
        <th><strong>Servizio query</strong></th>
        <th><strong>Eventi XDM</strong></th>
        <th><strong>Query XDM</strong></th>
        <th><strong>Aggregazione</strong></th>
        <th><strong>Clustering</strong></th>
    </tr>
    <tr>
        <th><strong>Python</strong></th>
        <td >sì</td>
        <td >sì</td>
        <td >sì</td>
        <td >sì</td>
        <td >sì</td>
        <td >sì</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >sì</td>
        <td >sì</td>
        <td >sì</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
    <tr>
        <th  ><strong>PySpark 3 (Spark 2.3 - obsoleto)</strong></th>
        <td >sì</td>
        <td >sì</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >sì</td>
        <td >sì</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>Spark (Spark 2.3 - obsoleto)</strong></th>
        <td >sì</td>
        <td >sì</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >sì</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3 (Spark 2.4)</strong></th>
        <td >no</td>
        <td >sì</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >sì</td>
        <td >sì</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>Scala</strong></th>
        <td >sì</td>
        <td >sì</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >sì</td>
    </tr>
</table>

Per aprire un nuovo *avvio*, fai clic su **File > Nuovo avvio**. In alternativa, espandete il browser **** File dalla barra laterale sinistra e fate clic sul simbolo più (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Accesso ai dati della piattaforma tramite i notebook

Ogni kernel supportato fornisce funzionalità integrate che consentono di leggere i dati della piattaforma da un dataset all&#39;interno di un blocco appunti. Tuttavia, il supporto per l&#39;impaginazione dei dati è limitato ai notebook Python e R.

### Leggi da un set di dati in Python/R

I notebook Python e R consentono di impaginare i dati quando si accede ai set di dati. Di seguito è illustrato il codice di esempio per leggere i dati con e senza impaginazione.

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### Lettura da un set di dati in Python/R senza impaginazione

L&#39;esecuzione del codice seguente consente di leggere l&#39;intero set di dati. Se l&#39;esecuzione ha esito positivo, i dati verranno salvati come fotogramma dati Pandas a cui fa riferimento la variabile `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

* `{DATASET_ID}`: L&#39;identità univoca del dataset a cui accedere

#### Leggi da un set di dati in Python/R con impaginazione

L&#39;esecuzione del codice seguente consente di leggere i dati dal set di dati specificato. La paginazione si ottiene limitando e compensando i dati attraverso le funzioni `limit()` e `offset()` rispettivamente. I dati limitati si riferiscono al numero massimo di punti dati da leggere, mentre l&#39;offset fa riferimento al numero di punti dati da ignorare prima della lettura dei dati. Se l&#39;operazione di lettura viene eseguita correttamente, i dati verranno salvati come fotogramma dati Pandas a cui fa riferimento la variabile `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$limit(100L)$offset(10L)$read() 
```

* `{DATASET_ID}`: L&#39;identità univoca del dataset a cui accedere

### Leggi da un set di dati in PySpark/Spark/Scala

>[!IMPORTANT]
>Con la transizione da Spark 2.3 a Spark 2.4, entrambi i kernel Spark e PySpark sono obsoleti.
>
>I nuovi notebook PySpark 3 (Spark 2.4) utilizzano il kernel Python3. Per convertire il codice Spark 2.3 esistente, consultate la guida alla conversione da [Pyspark 3 (Spark 2.3) a PySpark 3 (Spark 2.4)](../recipe-notebook-migration.md) . I nuovi notebook devono seguire l&#39;esempio [PySpark 3 (Spark 2.4)](#pyspark2.4) riportato di seguito.
>
>I nuovi notebook Spark dovrebbero utilizzare il kernel Scala. Per convertire il codice Spark 2.3 esistente, consultate la guida alla conversione da [Spark 2.3 a Scala (Spark 2.4)](../recipe-notebook-migration.md) . I nuovi notebook devono seguire l&#39;esempio [Scala (Spark 2.4)](#spark2.4) riportato di seguito.

Con un blocco appunti PySpark o Spark attivo aperto, espandere la scheda **Esplora** dati dalla barra laterale sinistra e fare doppio clic su **Set** dati per visualizzare un elenco dei set di dati disponibili. Fare clic con il pulsante destro del mouse sull&#39;elenco di set di dati a cui si desidera accedere e scegliere **Esplora dati nel blocco appunti**. Vengono generate le seguenti celle di codice:

#### PySpark (Spark 2.3 - obsoleto)

```python
# PySpark 3 (Spark 2.3 - deprecated)

pd0 = spark.read.format("com.adobe.platform.dataset").\
    option('orgId', "YOUR_IMS_ORG_ID@AdobeOrg").\
    load("{DATASET_ID}")
pd0.describe()
pd0.show(10, False)
```

#### PySpark (Spark 2.4) {#pyspark2.4}

Con l&#39;introduzione di Spark 2.4, [`%dataset`](#magic) la magia personalizzata è in dotazione.

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Spark (Spark 2.3 - obsoleto)

```scala
// Spark (Spark 2.3 - deprecated)

import com.adobe.platform.dataset.DataSetOptions
val dataFrame = spark.read.
    format("com.adobe.platform.dataset").
    option(DataSetOptions.orgId, "YOUR_IMS_ORG_ID@AdobeOrg").
    load("{DATASET_ID}")
dataFrame.printSchema()
dataFrame.show()
```

#### Scala (Spark 2.4) {#spark2.4}

```scala
// Scala (Spark 2.4)

// initialize the session
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()

val dataFrame = spark.read.format("com.adobe.platform.query")
    .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
    .option("ims-org", sys.env("IMS_ORG_ID"))
    .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
    .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
    .option("mode", "batch")
    .option("dataset-id", "{DATASET_ID}")
    .load()
dataFrame.printSchema()
dataFrame.show()
```

>[!TIP]
>In Scala è possibile utilizzare `sys.env()` per dichiarare e restituire un valore dall&#39;interno `option`.

### Utilizzo di %dataset Magic nei notebook PySpark 3 (Spark 2.4) {#magic}

Con l&#39;introduzione di Spark 2.4, `%dataset` la magia personalizzata viene fornita per l&#39;uso nei nuovi notebook PySpark 3 (Spark 2.4) (kernel Python 3).

**Utilizzo**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Descrizione**

Un comando magico personalizzato di Data Science Workspace per la lettura o la scrittura di un set di dati da un notebook Python (kernel Python 3).

* **{action}**: Tipo di azione da eseguire sul set di dati. Sono disponibili due azioni: &quot;read&quot; o &quot;write&quot;.
* **—datasetId {id}**: Utilizzato per fornire l&#39;ID del set di dati da leggere o scrivere. Questo è un argomento obbligatorio.
* **—dataFrame {df}**: Il dataframe panda. Questo è un argomento obbligatorio.
   * Quando l&#39;azione è &quot;read&quot;, {df} è la variabile in cui sono disponibili i risultati dell&#39;operazione di lettura del dataset.
   * Quando l&#39;azione è &quot;scrivi&quot;, il dataframe {df} viene scritto nel dataset.
* **—mode (facoltativo)**: I parametri consentiti sono &quot;batch&quot; e &quot;interattivo&quot;. Per impostazione predefinita, la modalità è impostata su &quot;interattivo&quot;. Si consiglia di utilizzare la modalità &quot;batch&quot; durante la lettura di grandi quantità di dati.

**Esempi**

* **Leggi l&#39;esempio**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **Esempio** di scrittura: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### Dati query con il servizio query in Python

JupyterLab sulla piattaforma consente di utilizzare SQL in un notebook Python per accedere ai dati tramite il servizio <a href="https://www.adobe.com/go/query-service-home-en" target="_blank">query</a>Adobe Experience Platform. L&#39;accesso ai dati tramite Query Service può essere utile per gestire insiemi di dati di grandi dimensioni a causa dei suoi tempi di esecuzione superiori. Tenere presente che l&#39;esecuzione di query sui dati tramite il servizio Query ha un limite di tempo di elaborazione di dieci minuti.

Prima di utilizzare Query Service in JupyterLab, verificare di disporre di una conoscenza approfondita della sintassi <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">SQL di</a>Query Service.

La query dei dati tramite il servizio Query richiede di fornire il nome del set di dati di destinazione. È possibile generare le celle di codice necessarie individuando il set di dati desiderato utilizzando **Data Explorer**. Fare clic con il pulsante destro del mouse sull&#39;elenco dei set di dati e scegliere Dati **query nel blocco appunti** per generare le due celle di codice seguenti nel blocco appunti:


Per utilizzare il servizio Query in JupyterLab, è innanzitutto necessario creare una connessione tra il notebook Python in funzione e il servizio Query. Questo può essere ottenuto eseguendo la prima cella generata.

```python
qs_connect()
```

Nella seconda cella generata, la prima riga deve essere definita prima della query SQL. Per impostazione predefinita, la cella generata definisce una variabile opzionale (`df0`) che salva i risultati della query come fotogramma dati Pandas. <br>L&#39; `-c QS_CONNECTION` argomento è obbligatorio e indica al kernel di eseguire la query SQL su Query Service. Per un elenco degli argomenti aggiuntivi, vedere l’ [appendice](#optional-sql-flags-for-query-service) .

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Alle variabili Python è possibile fare riferimento direttamente all&#39;interno di una query SQL utilizzando la sintassi in formato stringa e racchiudendo le variabili tra parentesi graffe (`{}`), come illustrato nell&#39;esempio seguente:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtrare i dati ExperienceEvent in Python/R

Per accedere e filtrare un set di dati ExperienceEvent in un blocco appunti Python o R, è necessario fornire l&#39;ID del set di dati (`{DATASET_ID}`) insieme alle regole del filtro che definiscono un intervallo di tempo specifico utilizzando operatori logici. Quando viene definito un intervallo di tempo, qualsiasi impaginazione specificata viene ignorata e viene considerato l&#39;intero set di dati.

Di seguito è riportato un elenco di operatori di filtraggio:

* `eq()`: Uguale a
* `gt()`: Maggiore di
* `ge()`: Maggiore o uguale a
* `lt()`: Minore di
* `le()`: Minore o uguale a
* `And()`: Operatore logico AND
* `Or()`: Operatore OR logico

Le celle seguenti filtrano un set di dati ExperienceEvent in dati esistenti esclusivamente tra il 1 gennaio 2019 e la fine del 31 dicembre 2019.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

### Filtrare i dati ExperienceEvent in PySpark/Spark

>[!IMPORTANT]
>Con la transizione da Spark 2.3 a Spark 2.4, entrambi i kernel Spark e PySpark sono obsoleti.
>
>I nuovi notebook PySpark 3 (Spark 2.4) utilizzano il kernel Python3. Consulta la guida sulla conversione di [Pyspark 3 (Spark 2.3) in PySpark 3 (Spark 2.4)](../recipe-notebook-migration.md) per ulteriori informazioni sulla conversione del codice esistente. Se state creando un nuovo blocco appunti PySpark, utilizzate l&#39;esempio [PySpark 3 (scintilla 2.4)](#pyspark3-spark2.4) per filtrare i dati ExperienceEvent.
>
>I nuovi notebook Spark dovrebbero utilizzare il kernel Scala. Consulta la guida sulla conversione di [Spark 2.3 in Scala (Spark 2.4)](../recipe-notebook-migration.md) per ulteriori informazioni sulla conversione del codice esistente. Se state creando un nuovo blocco appunti Spark, utilizzate l&#39;esempio [Scala (scintilla 2.4)](#scala-spark) per filtrare i dati ExperienceEvent.

Per accedere e filtrare un set di dati ExperienceEvent in un blocco appunti PySpark o Spark è necessario fornire l&#39;identità del set di dati (`{DATASET_ID}`), l&#39;identità IMS della propria organizzazione e le regole del filtro che definiscono un intervallo di tempo specifico. Un intervallo di tempo di filtro è definito utilizzando la funzione `spark.sql()`, dove il parametro della funzione è una stringa di query SQL.

Le celle seguenti filtrano un set di dati ExperienceEvent in dati esistenti esclusivamente tra il 1 gennaio 2019 e la fine del 31 dicembre 2019.

#### PySpark 3 (Spark 2.3 - obsoleto)

```python
# PySpark 3 (Spark 2.3 - deprecated)

pd = spark.read.format("com.adobe.platform.dataset").\
    option("orgId", "YOUR_IMS_ORG_ID@AdobeOrg").\
    load("{DATASET_ID}")

pd.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
```

#### PySpark 3 (Spark 2.4) {#pyspark3-spark2.4}

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

#### Spark (Spark 2.3 - obsoleto)

```scala
// Spark (Spark 2.3 - deprecated)

import com.adobe.platform.dataset.DataSetOptions
val dataFrame = spark.read.
    format("com.adobe.platform.dataset").
    option(DataSetOptions.orgId, "YOUR_IMS_ORG_ID@AdobeOrg").
    load("{DATASET_ID}")

dataFrame.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
```

#### Scala (Spark 2.4) {#scala-spark}

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

>[!TIP]
>In Scala è possibile utilizzare `sys.env()` per dichiarare e restituire un valore dall&#39;interno `option`. Questo elimina la necessità di definire le variabili se sai che verranno utilizzate solo una volta. L&#39;esempio seguente prende `val userToken` spunto dall&#39;esempio precedente e lo dichiara in linea `option` come alternativa:
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

## Librerie supportate {#supported-libraries}

### Python / R

| Libreria | Versione |
| :------ | :------ |
| notebook | 6.0.0 |
| requests | 2.22.0 |
| plotly | 4.0.0 |
| folium | 0.10.0 |
| ipywidgets | 7.5.1 |
| bokeh | 1.3.1 |
| gensim | 3.7.3 |
| ipyparallelo | 0.5.2 |
| jq | 1.6 |
| cheras | 2.2.4 |
| nltk | 3.2.5 |
| panda | 0.22.0 |
| pandasql | 0.7.3 |
| cuscino | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0.21.3 |
| sciolto | 1.3.0 |
| grassa | 1.3.0 |
| marinaio | 0.9.0 |
| statsmodels | 0.10.1 |
| elastico | 5.1.0.17 |
| ggplot | 0.11.5 |
| py xgipplo | 0.90 |
| opencv | 3.4.1 |
| pyspark | 2.4.3 |
| torcia | 1.0.1 |
| wxpitone | 4.0.6 |
| colorante | 0.3.0 |
| geopandas | 0.5.1 |
| pirata | 2.1.0 |
| sagomato | 1.6.4 |
| rpy2 | 2.9.4 |
| r-Essentials | 3.6 |
| aruli | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-gtopics | 4.2.0 |
| r-gvis | 0.4.4 |
| r-igrafo | 1.2.4.1 |
| giri | 3.0 |
| ri-manipolare | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| r-sopravvivenza | 2.44_1.1 |
| r-zoo | 1.8_6 |
| r-stringdist | 0.9.5.2 |
| quadrante r | 1.5_7 |
| r-rjson | 0.2.20 |
| r-previsione | 8.7 |
| r-rsolnp | 1.16 |
| reticolare | 1.12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| raccordo | 0.84 |
| r-fnn | 1.1.3 |
| r-lubridato | 1.7.4 |
| r-randomForest | 4.6_14 |
| r-tidyverse | 1.2.1 |
| r-tree | 1.0_39 |
| pymongo | 3.8.0 |
| freccia | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| parquet | 0.3.2 |
| pitone | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| graphviz | 2.40.1 |
| pitone-grafviz | 0.11.1 |
| stoccaggio di azzurro | 0.36.0 |
| jupyterlab | 1.0.4 |
| pandas_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| beffa | 3.0.5 |
| ipympl | 0.3.3 |
| fonts-anacond | 1,0 |
| psycopg2 | 2.8.3 |
| naso | 1.3.7 |
| autovwidget | 0.12.9 |
| altair | 3.1.0 |
| vega_datasets | 0.7.0 |
| cartiere | 1.0.1 |
| sql_magic | 0.0.4 |
| iso3166 | 1,0 |
| nbimporter | 0.3.1 |

### PySpark

| Libreria | Versione |
| :------ | :------ |
| requests | 2.18.4 |
| gensim | 2.3.0 |
| cheras | 2.0.6 |
| nltk | 3.2.4 |
| panda | 0.20.1 |
| pandasql | 0.7.3 |
| cuscino | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| sciolto | 0.19.1 |
| grassa | 1.3.3 |
| statsmodels | 0.8.0 |
| elastico | 4.0.30.44 |
| py xgipplo | 0.60 |
| opencv | 3.1.0 |
| freccia | 0.8.0 |
| boto3 | 1.5.18 |
| azure-storage-blob | 1.4.0 |
| pitone | 3.6.7 |
| mkl-rt | 11.1 |

## Flag SQL facoltativi per il servizio query {#optional-sql-flags-for-query-service}

Nella tabella seguente sono illustrati i flag SQL facoltativi utilizzabili per il servizio di query.

| **Flag** | **Descrizione** |
| --- | --- |
| `-h`, `--help` | Visualizza il messaggio della Guida e esci. |
| `-n`, `--notify` | Attiva/disattiva l&#39;opzione per la notifica dei risultati della query. |
| `-a`, `--async` | L&#39;utilizzo di questo flag consente di eseguire la query in modo asincrono e di liberare il kernel durante l&#39;esecuzione della query. Prestate attenzione quando assegnate i risultati della query alle variabili, in quanto potrebbe essere undefined se la query non è completa. |
| `-d`, `--display` | L&#39;utilizzo di questo flag impedisce la visualizzazione dei risultati. |

