---
keywords: Experience Platform;JupyterLab;ricetta;blocchi appunti;Data Science Workspace;argomenti popolari;creare ricetta
solution: Experience Platform
title: Creare un modello utilizzando JupyterLab Notebooks
type: Tutorial
description: Questo tutorial illustra i passaggi necessari per creare una ricetta utilizzando il modello per la generazione di formule dei notebook JupyterLab.
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 0%

---

# Creare un modello utilizzando JupyterLab Notebooks

Questo tutorial illustra i passaggi necessari per creare un modello utilizzando il modello per la generazione di formule dei notebook JupyterLab.

## Concetti introdotti:

- **Ricette:** Una ricetta è il termine Adobe per una specifica di modello ed è un contenitore di livello superiore che rappresenta un apprendimento automatico specifico, un algoritmo di intelligenza artificiale o un insieme di algoritmi, una logica di elaborazione e una configurazione necessarie per generare ed eseguire un modello addestrato.
- **Modello:** Un modello è un’istanza di una ricetta di apprendimento automatico che viene addestrata utilizzando dati e configurazioni storici per risolvere un caso d’uso aziendale.
- **Formazione:** La formazione è il processo di apprendimento dei pattern e delle informazioni dai dati etichettati.
- **Punteggio** Il punteggio è il processo di generazione di informazioni dai dati utilizzando un modello addestrato.

## Scarica le risorse richieste {#assets}

Prima di procedere con questa esercitazione, è necessario creare gli schemi e i set di dati richiesti. Visita il tutorial per [creazione di schemi e set di dati del modello di propensione Luma](../models-recipes/create-luma-data.md) per scaricare le risorse richieste e impostare i prerequisiti.

## Introduzione a [!DNL JupyterLab] ambiente notebook

La creazione di una ricetta da zero può essere eseguita in [!DNL Data Science Workspace]. Per iniziare, passa a [Adobe Experience Platform](https://platform.adobe.com) e seleziona la **[!UICONTROL Notebook]** a sinistra. Per creare un nuovo blocco appunti, selezionare il modello di Generatore di ricette dal [!DNL JupyterLab Launcher].

Il [!UICONTROL Generatore di ricette] notebook consente di eseguire esecuzioni di formazione e punteggio all&#39;interno del notebook. Questo offre la flessibilità di apportare modifiche alle `train()` e `score()` metodi tra l’esecuzione di esperimenti sull’addestramento e i dati di punteggio. Una volta soddisfatti dei risultati di formazione e punteggio, puoi creare una ricetta e pubblicarla ulteriormente come modello utilizzando la ricetta per modellare la funzionalità.

>[!NOTE]
>
>Il [!UICONTROL Generatore di ricette] il notebook supporta l’utilizzo di tutti i formati di file, ma al momento la funzionalità crea ricetta supporta solo [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder-new.png)

Quando selezioni il [!UICONTROL Generatore di ricette] dal modulo di avvio, il blocco appunti viene aperto in una nuova scheda.

Nella nuova scheda del blocco appunti nella parte superiore, viene caricata una barra degli strumenti contenente tre azioni aggiuntive: **[!UICONTROL Addestra]**, **[!UICONTROL Punteggio]**, e **[!UICONTROL Crea ricetta]**. Queste icone vengono visualizzate solo nel [!UICONTROL Generatore di ricette] notebook. Vengono fornite ulteriori informazioni su queste azioni [nella sezione formazione e punteggio](#training-and-scoring) dopo aver creato la ricetta nel blocco appunti.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Introduzione a [!UICONTROL Generatore di ricette] notebook

Nella cartella delle risorse fornita è presente un modello di propensione Luma `propensity_model.ipynb`. Utilizzando l’opzione carica notebook in JupyterLab, carica il modello fornito e apri il notebook.

![carica blocco appunti](../images/jupyterlab/create-recipe/upload_notebook.png)

Il resto di questo tutorial riguarda i seguenti file predefiniti nel notebook del modello di propensione:

- [File dei requisiti](#requirements-file)
- [File di configurazione](#configuration-files)
- [Caricatore dati di formazione](#training-data-loader)
- [Caricatore dati punteggio](#scoring-data-loader)
- [File di pipeline](#pipeline-file)
- [File valutatore](#evaluator-file)
- [File di Data Saver](#data-saver-file)

Il seguente tutorial video spiega il notebook con modello di propensione Luma:

>[!VIDEO](https://video.tv.adobe.com/v/333570)

### File dei requisiti {#requirements-file}

Il file dei requisiti viene utilizzato per dichiarare librerie aggiuntive da utilizzare nel modello. Se esiste una dipendenza, puoi specificare il numero di versione. Per cercare altre librerie, visita [anaconda.org](https://anaconda.org). Per informazioni su come formattare il file dei requisiti, visitare [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). L’elenco delle librerie principali già in uso include:

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>Le librerie o le versioni specifiche aggiunte potrebbero essere incompatibili con le librerie di cui sopra. Inoltre, se scegli di creare manualmente un file di ambiente, il `name` il campo non può essere sostituito.

Per il notebook con propensione Luma, non è necessario aggiornare i requisiti.

### File di configurazione {#configuration-files}

I file di configurazione, `training.conf` e `scoring.conf`, vengono utilizzati per specificare i set di dati da utilizzare per l’apprendimento e il punteggio, nonché per aggiungere iperparametri. Esistono configurazioni separate per l’apprendimento e il punteggio.

Affinché un modello possa eseguire l’apprendimento, devi fornire `trainingDataSetId`, `ACP_DSW_TRAINING_XDM_SCHEMA`, e `tenantId`. Inoltre, per il punteggio, devi fornire `scoringDataSetId`, `tenantId`, e `scoringResultsDataSetId `.

Per trovare il set di dati e gli ID dello schema, passa alla scheda dati ![Scheda Dati](../images/jupyterlab/create-recipe/dataset-tab.png) all&#39;interno di blocchi appunti sulla barra di spostamento a sinistra (sotto l&#39;icona della cartella ). È necessario fornire tre ID di set di dati diversi. Il `scoringResultsDataSetId` viene utilizzato per memorizzare i risultati del punteggio del modello e deve essere un set di dati vuoto. Questi set di dati sono stati creati in precedenza in [Risorse richieste](#assets) passaggio.

![](../images/jupyterlab/create-recipe/dataset_tab.png)

Le stesse informazioni sono disponibili su [Adobe Experience Platform](https://platform.adobe.com/) sotto **[Schema](https://platform.adobe.com/schema)** e **[Set di dati](https://platform.adobe.com/dataset/overview)** schede.

Al termine del concorso, la configurazione di apprendimento e punteggio dovrà essere simile alla schermata seguente:

![configurazione](../images/jupyterlab/create-recipe/config.png)

Per impostazione predefinita, quando si addestrano e si assegnano punteggi ai dati vengono impostati i seguenti parametri di configurazione:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Informazioni su Training Data Loader {#training-data-loader}

Lo scopo del caricatore dati di formazione è quello di creare un’istanza dei dati utilizzati per creare il modello di apprendimento automatico. In genere, il caricatore di dati di formazione esegue due attività:

- Caricamento dati da [!DNL Platform]
- Preparazione dei dati e progettazione delle funzioni

Nelle due sezioni seguenti verranno descritti i passaggi necessari per caricare i dati e preparare i dati.

### Caricamento dei dati {#loading-data}

Questo passaggio utilizza [dataframe panda](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). I dati possono essere caricati dai file in [!DNL Adobe Experience Platform] utilizzando [!DNL Platform] SDK (`platform_sdk`) o da fonti esterne che utilizzano i panda&#39; `read_csv()` o `read_json()` funzioni.

- [[!DNL Platform SDK]](#platform-sdk)
- [Sorgenti esterne](#external-sources)

>[!NOTE]
>
>Nel blocco appunti di Recipe Builder, i dati vengono caricati tramite `platform_sdk` caricatore di dati.

### [!DNL Platform] SDK {#platform-sdk}

Per un tutorial approfondito sull’utilizzo di `platform_sdk` caricatore di dati, visita il [Guida all’SDK di Platform](../authoring/platform-sdk.md). Questo tutorial fornisce informazioni sull’autenticazione della build, sulla lettura di base dei dati e sulla scrittura di base dei dati.

### Sorgenti esterne {#external-sources}

Questa sezione mostra come importare un file JSON o CSV in un oggetto panda. La documentazione ufficiale della libreria dei panda è disponibile qui:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Innanzitutto, ecco un esempio di importazione di un file CSV. Il `data` è il percorso del file CSV. Questa variabile è stata importata da `configProperties` nel [sezione precedente](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

Puoi anche importare da un file JSON. Il `data` è il percorso del file CSV. Questa variabile è stata importata da `configProperties` nel [sezione precedente](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

Ora i dati si trovano nell’oggetto dataframe e possono essere analizzati e manipolati nel [sezione successiva](#data-preparation-and-feature-engineering).

## File caricatore dati addestramento

In questo esempio, i dati vengono caricati utilizzando l’SDK di Platform. La libreria può essere importata nella parte superiore della pagina includendo la riga:

`from platform_sdk.dataset_reader import DatasetReader`

È quindi possibile utilizzare `load()` metodo per acquisire il set di dati di formazione da `trainingDataSetId` come impostato nella configurazione (`recipe.conf`).

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    dataset_reader = DatasetReader(client_context, dataset_id=config_properties['trainingDataSetId'])
```

>[!NOTE]
>
>Come indicato nella [Sezione File di configurazione](#configuration-files), i seguenti parametri di configurazione sono impostati quando si accede ai dati da Experience Platform utilizzando `client_context = get_client_context(config_properties)`:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Ora che disponi dei tuoi dati, puoi iniziare con la preparazione dei dati e la progettazione delle funzionalità.

### Preparazione dei dati e progettazione delle funzioni {#data-preparation-and-feature-engineering}

Dopo il caricamento dei dati, è necessario pulirli e prepararli. In questo esempio, l’obiettivo del modello è prevedere se un cliente ordinerà o meno un prodotto. Poiché il modello non considera prodotti specifici, non è necessario `productListItems` e quindi la colonna viene eliminata. Vengono quindi eliminate colonne aggiuntive che contengono un solo valore o due valori in una singola colonna. Durante l’apprendimento di un modello, è importante conservare solo dati utili che ti aiutino a prevedere il tuo obiettivo.

![esempio di preparazione dati](../images/jupyterlab/create-recipe/data_prep.png)

Una volta eliminati i dati non necessari, puoi iniziare la progettazione delle funzionalità. I dati demo utilizzati per questo esempio non contengono informazioni sulla sessione. In genere, è necessario disporre di dati sulle sessioni correnti e passate per un determinato cliente. A causa della mancanza di informazioni sulla sessione, questo esempio imita le sessioni attuali e precedenti tramite la demarcazione del percorso.

![demarcazione percorso](../images/jupyterlab/create-recipe/journey_demarcation.png)

Una volta completata la delimitazione, i dati vengono etichettati e viene creato un percorso.

![etichettare i dati](../images/jupyterlab/create-recipe/label_data.png)

Successivamente, le feature vengono create e suddivise in passato e presente. Vengono quindi eliminate tutte le colonne non necessarie, lasciando ai clienti Luma sia i percorsi passati che quelli correnti. Questi percorsi contengono informazioni quali se un cliente ha acquistato un articolo e il percorso che ha utilizzato prima dell’acquisto.

![corso di formazione finale](../images/jupyterlab/create-recipe/final_journey.png)

## Caricatore dati punteggio {#scoring-data-loader}

La procedura per caricare i dati per il punteggio è simile al caricamento dei dati di apprendimento. Osservando attentamente il codice, puoi notare che tutto è uguale, tranne che per `scoringDataSetId` nel `dataset_reader`. Questo perché la stessa origine dati Luma viene utilizzata sia per l’apprendimento che per il punteggio.

Nel caso in cui si desideri utilizzare file di dati diversi per l’apprendimento e il punteggio, il caricatore di dati per l’apprendimento e il punteggio è separato. Questo ti consente di eseguire una pre-elaborazione aggiuntiva, ad esempio la mappatura dei dati di apprendimento ai dati di punteggio, se necessario.

## File di pipeline {#pipeline-file}

Il `pipeline.py` Il file include la logica per l’apprendimento e il punteggio.

Lo scopo dell’apprendimento è quello di creare un modello utilizzando le funzioni e le etichette nel set di dati di apprendimento. Dopo aver scelto il modello di apprendimento, devi adattare il set di dati di apprendimento x e y al modello e la funzione restituisce il modello addestrato.

>[!NOTE]
> 
>Le funzioni si riferiscono alla variabile di input utilizzata dal modello di apprendimento automatico per prevedere le etichette.

![def train](../images/jupyterlab/create-recipe/def_train.png)

Il `score()` La funzione deve contenere l’algoritmo di punteggio e restituire una misurazione per indicare il successo del modello. Il `score()` La funzione utilizza le etichette dei set di dati di punteggio e il modello addestrato per generare un set di funzioni previste. Questi valori previsti vengono quindi confrontati con le funzioni effettive nel set di dati di punteggio. In questo esempio, la proprietà `score()` la funzione utilizza il modello addestrato per prevedere le feature utilizzando le etichette del set di dati di punteggio. Vengono restituite le funzioni previste.

![def score](../images/jupyterlab/create-recipe/def_score.png)

## File valutatore {#evaluator-file}

Il `evaluator.py` Il file contiene informazioni logiche su come valutare la ricetta formata e su come suddividere i dati di formazione.

### Dividere il set di dati {#split-the-dataset}

La fase di preparazione dei dati per l’addestramento richiede la suddivisione del set di dati da utilizzare per l’addestramento e il test. Questo `val` I dati vengono utilizzati implicitamente per valutare il modello dopo che è stato addestrato. Questo processo è separato dal punteggio.

Questa sezione mostra `split()` funzione che carica i dati nel blocco appunti, quindi pulisce i dati rimuovendo colonne non correlate nel set di dati. Da qui è possibile eseguire la progettazione delle feature, ovvero il processo per creare ulteriori feature rilevanti dalle feature raw esistenti nei dati.

![Funzione split](../images/jupyterlab/create-recipe/split.png)

### Valuta il modello addestrato {#evaluate-the-trained-model}

Il `evaluate()` La funzione viene eseguita dopo che il modello è stato addestrato e restituisce una metrica per indicare il successo del modello. Il `evaluate()` La funzione utilizza le etichette dei set di dati di test e il modello addestrato per prevedere un set di feature. Questi valori previsti vengono quindi confrontati con le funzioni effettive nel set di dati di test. In questo esempio le metriche utilizzate sono `precision`, `recall`, `f1`, e `accuracy`. La funzione restituisce un valore `metric` oggetto contenente un array di metriche di valutazione. Queste metriche vengono utilizzate per valutare le prestazioni del modello addestrato.

![valutare](../images/jupyterlab/create-recipe/evaluate.png)

Aggiunta `print(metric)` ti consente di visualizzare i risultati della metrica.

![risultati delle metriche](../images/jupyterlab/create-recipe/evaluate_metric.png)

## File di Data Saver {#data-saver-file}

Il `datasaver.py` il file contiene `save()` e viene utilizzato per salvare la previsione durante il test del punteggio. Il `save()` prende le tue previsioni e utilizza [!DNL Experience Platform Catalog] API, scrive i dati in `scoringResultsDataSetId` hai specificato in `scoring.conf` file. È possibile

![Risparmio dati](../images/jupyterlab/create-recipe/data_saver.png)

## Formazione e valutazione {#training-and-scoring}

Una volta apportate le modifiche al blocco appunti e si desidera addestrare la composizione, è possibile selezionare i pulsanti associati nella parte superiore della barra per creare un&#39;esecuzione di addestramento nella cella. Quando si seleziona il pulsante, nel blocco appunti viene visualizzato un registro di comandi e output dello script di addestramento (sotto `evaluator.py` ). Conda installa prima tutte le dipendenze, quindi viene avviato l’addestramento.

È necessario eseguire l’apprendimento almeno una volta prima di poter eseguire il punteggio. Selezione del **[!UICONTROL Esegui punteggio]** Pulsante assegnerà un punteggio al modello addestrato generato durante l’addestramento. Lo script di punteggio viene visualizzato in `datasaver.py`.

A scopo di debug, se desideri visualizzare l’output nascosto, aggiungi `debug` alla fine della cella di output ed eseguirla nuovamente.

![treno e punteggio](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Creare una ricetta {#create-recipe}

Una volta completata la modifica della ricetta e soddisfatti dell’output di formazione/punteggio, puoi creare una ricetta dal blocco appunti selezionando **[!UICONTROL Crea ricetta]** in alto a destra.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Dopo aver selezionato **[!UICONTROL Crea ricetta]**, viene richiesto di immettere un nome per la ricetta. Questo nome rappresenta la ricetta effettiva creata il [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Dopo aver selezionato **[!UICONTROL Ok]**, inizia il processo di creazione della ricetta. Questa operazione può richiedere del tempo e al posto del pulsante Crea composizione viene visualizzata una barra di avanzamento. Al termine, puoi selezionare **[!UICONTROL Visualizza ricette]** per passare al **[!UICONTROL Ricette]** scheda in **[!UICONTROL Modelli ML]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

>[!CAUTION]
>
> - Non eliminare nessuna delle celle del file
> - Non modificare `%%writefile` riga nella parte superiore delle celle del file
> - Non creare ricette in diversi notebook contemporaneamente


## Passaggi successivi {#next-steps}

Completando questa esercitazione, hai imparato a creare un modello di apprendimento automatico in [!UICONTROL Generatore di ricette] notebook. Hai anche imparato a sfruttare il blocco appunti per il flusso di lavoro della ricetta.

Per continuare a imparare a utilizzare le risorse in [!DNL Data Science Workspace], visitare il sito [!DNL Data Science Workspace] elenco a discesa ricette e modelli.