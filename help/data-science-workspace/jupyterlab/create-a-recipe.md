---
keywords: Experience Platform;JupyterLab;ricetta;notebook;Data Science Workspace;argomenti popolari;creare ricetta
solution: Experience Platform
title: Creare una ricetta utilizzando i notebook Jupyter
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione si articola su due sezioni principali. Innanzitutto, creerai un modello di apprendimento automatico utilizzando un modello all'interno di JupyterLab Notebook. Successivamente, si eserciterà il notebook per creare un flusso di lavoro di ricetta all'interno di JupyterLab per creare una ricetta all'interno di Data Science Workspace.
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---

# Creare una ricetta utilizzando Jupyter Notebooks

Questa esercitazione si articola su due sezioni principali. Innanzitutto, creerai un modello di apprendimento automatico utilizzando un modello all&#39;interno di [!DNL JupyterLab Notebook]. Successivamente, si eserciterà il blocco appunti per creare un flusso di lavoro all&#39;interno di [!DNL JupyterLab] per creare una ricetta all&#39;interno di [!DNL Data Science Workspace].

## Concetti presentati:

- **Ricette:** una ricetta è un termine di Adobe per una specifica di modello ed è un contenitore di primo livello che rappresenta uno specifico apprendimento automatico, un algoritmo AI o un insieme di algoritmi, logica di elaborazione e configurazione necessari per creare ed eseguire un modello addestrato e quindi contribuire a risolvere problemi di business specifici.
- **Modello:** un modello è un&#39;istanza di una ricetta di apprendimento automatico formata utilizzando dati storici e configurazioni per risolvere un caso d&#39;uso aziendale.
- **Formazione:** la formazione è il processo di apprendimento di schemi e insights dai dati etichettati.
- **Punteggio:** il punteggio è il processo di generazione di informazioni dai dati che utilizza un modello addestrato.

## Guida introduttiva all&#39;ambiente [!DNL JupyterLab] per notebook

La creazione di una ricetta da zero può essere effettuata all&#39;interno di [!DNL Data Science Workspace]. Per iniziare, passa a [Adobe Experience Platform](https://platform.adobe.com) e fai clic sulla scheda **[!UICONTROL Notebooks]** a sinistra. Crea un nuovo blocco appunti selezionando il modello Ricetta Builder dal [!DNL JupyterLab Launcher].

Il notebook [!UICONTROL Recipe Builder] consente di eseguire attività di formazione e valutazione all&#39;interno del notebook. Questo ti offre la flessibilità di apportare modifiche ai metodi `train()` e `score()` tra l’esecuzione di esperimenti sui dati di formazione e valutazione. Una volta soddisfatti i risultati della formazione e del punteggio, è possibile creare una ricetta da utilizzare in [!DNL Data Science Workspace] utilizzando il blocco appunti per creare le funzionalità integrate nel blocco appunti di Recipe Builder.

>[!NOTE]
>
>Il blocco appunti di Recipe Builder supporta l&#39;utilizzo di tutti i formati di file, ma al momento la funzionalità Create Recipe supporta solo [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder.png)

Quando si fa clic sul blocco appunti del generatore di ricette dal modulo di avvio, il blocco appunti viene aperto nella scheda . Il modello utilizzato nel blocco appunti è la Ricetta di previsione vendite al dettaglio Python che si trova anche in [questo archivio pubblico](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

Nella barra degli strumenti sono disponibili tre azioni aggiuntive: **[!UICONTROL Train]**, **[!UICONTROL Score]** e **[!UICONTROL Create Recipe]**. Queste icone vengono visualizzate solo nel blocco appunti [!UICONTROL Recipe Builder]. Per ulteriori informazioni su queste azioni, consulta la sezione [Formazione e valutazione](#training-and-scoring) dopo la creazione della composizione nel blocco appunti.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Apportare modifiche ai file di ricetta

Per apportare modifiche ai file di ricetta, passa alla cella in Jupyter corrispondente al percorso del file. Ad esempio, se desideri apportare modifiche a `evaluator.py`, cerca `%%writefile demo-recipe/evaluator.py`.

Iniziare a apportare le modifiche necessarie alla cella e, al termine, eseguire semplicemente la cella. Il comando `%%writefile filename.py` scriverà il contenuto della cella in `filename.py`. Sarà necessario eseguire manualmente la cella per ogni file con modifiche.

>[!NOTE]
>
>Se necessario, eseguire le celle manualmente.

## Guida introduttiva al blocco appunti di Recipe Builder

Ora che si conoscono le basi dell&#39;ambiente [!DNL JupyterLab] per notebook, è possibile iniziare a esaminare i file che compongono una ricetta modello di apprendimento automatico. I file di cui parleremo sono mostrati qui:

- [File dei requisiti](#requirements-file)
- [File di configurazione](#configuration-files)
- [Caricatore dati di formazione](#training-data-loader)
- [Caricatore dati di valutazione](#scoring-data-loader)
- [File di tubazione](#pipeline-file)
- [File valutatore](#evaluator-file)
- [File di Data Saver](#data-saver-file)

### File dei requisiti {#requirements-file}

Il file dei requisiti viene utilizzato per dichiarare librerie aggiuntive da utilizzare nella ricetta. Se esiste una dipendenza, è possibile specificare il numero di versione. Per cercare librerie aggiuntive, visita [anaconda.org](https://anaconda.org). Per informazioni su come formattare il file dei requisiti, visita [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). L’elenco delle librerie principali già in uso include:

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>Le librerie o le versioni specifiche aggiunte potrebbero essere incompatibili con le librerie di cui sopra. Inoltre, se scegli di creare manualmente un file di ambiente, il campo `name` non può essere ignorato.

### File di configurazione {#configuration-files}

I file di configurazione `training.conf` e `scoring.conf` vengono utilizzati per specificare i set di dati da utilizzare per la formazione e il punteggio, nonché per aggiungere parametri ipertestuali. Sono disponibili configurazioni separate per la formazione e il punteggio.

Gli utenti devono compilare le seguenti variabili prima di eseguire la formazione e il punteggio:
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

Per trovare il set di dati e gli ID dello schema, vai alla scheda dati ![scheda dati](../images/jupyterlab/create-recipe/dataset-tab.png) all’interno dei blocchi appunti nella barra di navigazione a sinistra (sotto l’icona della cartella).

![](../images/jupyterlab/create-recipe/dataset_tab.png)

Le stesse informazioni si trovano nelle schede [Adobe Experience Platform](https://platform.adobe.com/) **[Schema](https://platform.adobe.com/schema)** e **[Set di dati](https://platform.adobe.com/dataset/overview)**.

Per impostazione predefinita, quando accedi ai dati vengono impostati i seguenti parametri di configurazione:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Caricatore dati di formazione {#training-data-loader}

Lo scopo di Training Data Loader è quello di creare un&#39;istanza dei dati utilizzati per creare il modello di apprendimento automatico. In genere, esistono due attività che il caricatore dati di formazione eseguirà:
- Carica dati da [!DNL Platform]
- Preparazione dei dati e ingegneria delle funzioni

Le due sezioni seguenti esamineranno il caricamento dei dati e la preparazione dei dati.

### Caricamento dei dati {#loading-data}

Questo passaggio utilizza il [dataframe panda](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). I dati possono essere caricati da file in [!DNL Adobe Experience Platform] utilizzando l&#39;SDK [!DNL Platform] (`platform_sdk`) o da fonti esterne utilizzando le funzioni `read_csv()` o `read_json()`.

- [[!DNL Platform SDK]](#platform-sdk)
- [Origini esterne](#external-sources)

>[!NOTE]
>
>Nel blocco appunti del Generatore di ricette, i dati vengono caricati tramite il caricatore di dati `platform_sdk`.

### [!DNL Platform] SDK {#platform-sdk}

Per un&#39;esercitazione approfondita sull&#39;utilizzo del caricatore dati `platform_sdk`, visita la [guida SDK della piattaforma](../authoring/platform-sdk.md). Questa esercitazione fornisce informazioni sull’autenticazione della build, sulla lettura di base dei dati e sulla scrittura di base dei dati.

### Origini esterne {#external-sources}

Questa sezione mostra come importare un file JSON o CSV in un oggetto panda. La documentazione ufficiale della biblioteca dei panda si trova qui:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Innanzitutto, ecco un esempio di importazione di un file CSV. L’argomento `data` rappresenta il percorso del file CSV. Questa variabile è stata importata da `configProperties` nella sezione [precedente](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

Puoi anche importare da un file JSON. L’argomento `data` rappresenta il percorso del file CSV. Questa variabile è stata importata da `configProperties` nella sezione [precedente](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

Ora i dati si trovano nell&#39;oggetto dataframe e possono essere analizzati e manipolati nella sezione [successiva](#data-preparation-and-feature-engineering).

### Dall’SDK di Platform

Puoi caricare i dati utilizzando l’SDK di Platform. La libreria può essere importata nella parte superiore della pagina includendo la riga :

`from platform_sdk.dataset_reader import DatasetReader`

Quindi utilizziamo il metodo `load()` per recuperare il set di dati di formazione dal `trainingDataSetId` come impostato nel file di configurazione (`recipe.conf`).

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    
    dataset_reader = DatasetReader(client_context, config_properties['trainingDataSetId'])
    
    timeframe = config_properties.get("timeframe")
    tenant_id = config_properties.get("tenant_id")
```

>[!NOTE]
>
>Come indicato nella sezione [File di configurazione](#configuration-files), i seguenti parametri di configurazione vengono impostati automaticamente quando si accede ai dati da un Experience Platform utilizzando `client_context`:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Ora che disponi dei tuoi dati, puoi iniziare con la preparazione dei dati e l&#39;ingegneria delle funzioni.

### Preparazione dei dati e ingegneria delle funzioni {#data-preparation-and-feature-engineering}

Una volta caricati i dati, questi vengono preparati e quindi suddivisi nei set di dati `train` e `val`. Di seguito è riportato un codice di esempio:

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
dataframe.date = pd.to_datetime(dataframe.date)
dataframe['week'] = dataframe.date.dt.week
dataframe['year'] = dataframe.date.dt.year

dataframe = pd.concat([dataframe, pd.get_dummies(dataframe['storeType'])], axis=1)
dataframe.drop('storeType', axis=1, inplace=True)
dataframe['isHoliday'] = dataframe['isHoliday'].astype(int)

dataframe['weeklySalesAhead'] = dataframe.shift(-45)['weeklySales']
dataframe['weeklySalesLag'] = dataframe.shift(45)['weeklySales']
dataframe['weeklySalesDiff'] = (dataframe['weeklySales'] - dataframe['weeklySalesLag']) / dataframe['weeklySalesLag']
dataframe.dropna(0, inplace=True)

dataframe = dataframe.set_index(dataframe.date)
dataframe.drop('date', axis=1, inplace=True) 
```

In questo esempio, vengono eseguite cinque operazioni sul set di dati originale:
- aggiungere colonne `week` e `year`
- convertire `storeType` in una variabile indicatore
- convertire `isHoliday` in una variabile numerica
- offset `weeklySales` per ottenere il valore delle vendite future e passate
- suddividere i dati, per data, in `train` e `val` set di dati

Innanzitutto, vengono create le colonne `week` e `year` e la colonna `date` originale viene convertita in [!DNL Python] [datetime](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html). I valori settimana e anno vengono estratti dall’oggetto datetime .

Successivamente, `storeType` viene convertito in tre colonne che rappresentano i tre diversi tipi di archivio, (`A`, `B` e `C`). Ciascuna contiene un valore booleano per indicare che `storeType` è true. La colonna `storeType` verrà eliminata.

Analogamente, `weeklySales` cambia il valore booleano `isHoliday` in una rappresentazione numerica, uno o zero.

Questi dati sono suddivisi tra `train` e `val` set di dati.

La funzione `load()` deve essere completata con il set di dati `train` e `val` come output.

### Caricatore dati di punteggio {#scoring-data-loader}

La procedura per caricare i dati per il punteggio è simile a quella per il caricamento dei dati di formazione nella funzione `split()` . Usiamo l&#39;SDK per l&#39;accesso ai dati per caricare i dati dal `scoringDataSetId` presente nel nostro file `recipe.conf`.

```PYTHON
def load(config_properties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    client_context = get_client_context(config_properties)

    dataset_reader = DatasetReader(client_context, config_properties['scoringDataSetId'])
    timeframe = config_properties.get("timeframe")
    tenant_id = config_properties.get("tenant_id")
```

Dopo aver caricato i dati, viene eseguita la preparazione dei dati e l’ingegneria delle funzioni.

```PYTHON
    #########################################
    # Data Preparation/Feature Engineering
    #########################################
    if '_id' in dataframe.columns:
        #Rename columns to strip tenantId
        dataframe = dataframe.rename(columns = lambda x : str(x)[str(x).find('.')+1:])
        #Drop id, eventType and timestamp
        dataframe.drop(['_id', 'eventType', 'timestamp'], axis=1, inplace=True)

    dataframe.date = pd.to_datetime(dataframe.date)
    dataframe['week'] = dataframe.date.dt.week
    dataframe['year'] = dataframe.date.dt.year

    dataframe = pd.concat([dataframe, pd.get_dummies(dataframe['storeType'])], axis=1)
    dataframe.drop('storeType', axis=1, inplace=True)
    dataframe['isHoliday'] = dataframe['isHoliday'].astype(int)

    dataframe['weeklySalesAhead'] = dataframe.shift(-45)['weeklySales']
    dataframe['weeklySalesLag'] = dataframe.shift(45)['weeklySales']
    dataframe['weeklySalesDiff'] = (dataframe['weeklySales'] - dataframe['weeklySalesLag']) / dataframe['weeklySalesLag']
    dataframe.dropna(0, inplace=True)

    dataframe = dataframe.set_index(dataframe.date)
    dataframe.drop('date', axis=1, inplace=True)

    print("Scoring Data Load Finish")

    return dataframe
```

Poiché lo scopo del nostro modello è quello di prevedere le vendite settimanali future, dovrai creare un set di dati di valutazione utilizzato per valutare le prestazioni della previsione del modello.

Questo notebook Recipe Builder lo fa compensando la nostra vendita settimanale 7 giorni in avanti. Tieni presente che esistono misure per 45 archivi ogni settimana in modo da poter spostare i valori `weeklySales` 45 set di dati in avanti in una nuova colonna denominata `weeklySalesAhead`.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

Allo stesso modo, è possibile creare una colonna `weeklySalesLag` spostando indietro di 45. Utilizzando questo strumento è inoltre possibile calcolare la differenza nelle vendite settimanali e memorizzarle nella colonna `weeklySalesDiff`.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

Poiché si sta eseguendo l’offset dei `weeklySales` punti dati 45 in avanti e 45 in indietro per creare nuove colonne, i primi e gli ultimi 45 punti dati avranno valori NaN. Puoi rimuovere questi punti dal nostro set di dati utilizzando la funzione `df.dropna()` che rimuove tutte le righe con valori NaN.

```PYTHON
df.dropna(0, inplace=True)
```

La funzione `load()` nel caricatore dati di punteggio deve essere completata con il set di dati di punteggio come output.

### File della pipeline {#pipeline-file}

Il file `pipeline.py` include logica per la formazione e il punteggio.

### Formazione {#training}

Lo scopo della formazione è quello di creare un modello utilizzando caratteristiche ed etichette nel set di dati di formazione.

>[!NOTE]
> 
>Le feature si riferiscono alla variabile di input utilizzata dal modello di apprendimento automatico per prevedere le etichette.

La funzione `train()` deve includere il modello di addestramento e restituire il modello addestrato. Alcuni esempi di modelli diversi sono disponibili nella documentazione della guida utente [scikit-learn](https://scikit-learn.org/stable/user_guide.html) .

Dopo aver scelto il tuo modello di formazione, inserirai il tuo set di dati x e y di formazione al modello e la funzione restituirà il modello addestrato. Un esempio che mostra questo è il seguente:

```PYTHON
def train(configProperties, data):

    print("Train Start")

    #########################################
    # Extract fields from configProperties
    #########################################
    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])


    #########################################
    # Fit model
    #########################################
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values

    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)

    model.fit(X_train, y_train)

    print("Train Complete")

    return model
```

A seconda dell’applicazione, la funzione `GradientBoostingRegressor()` contiene argomenti. `xTrainingDataset` deve contenere le funzioni utilizzate per la formazione, mentre  `yTrainingDataset` deve contenere le etichette.

### Punteggio {#scoring}

La funzione `score()` deve contenere l&#39;algoritmo di punteggio e restituire una misurazione per indicare il successo del modello. La funzione `score()` utilizza le etichette del set di dati di punteggio e il modello addestrato per generare un set di funzioni previste. Questi valori previsti vengono quindi confrontati con le funzioni effettive nel set di dati di punteggio. In questo esempio, la funzione `score()` utilizza il modello addestrato per prevedere le funzioni utilizzando le etichette del set di dati di punteggio. Vengono restituite le funzionalità previste.

```PYTHON
def score(configProperties, data, model):

    print("Score Start")

    X_test = data.drop('weeklySalesAhead', axis=1).values
    y_test = data['weeklySalesAhead'].values
    y_pred = model.predict(X_test)

    data['prediction'] = y_pred
    data = data[['store', 'prediction']].reset_index()
    data['date'] = data['date'].astype(str)

    print("Score Complete")

    return data
```

### File di valutazione {#evaluator-file}

Il file `evaluator.py` contiene una logica che indica come valutare la ricetta formata e come suddividere i dati di formazione. Nell’esempio di vendita al dettaglio, sarà inclusa la logica per il caricamento e la preparazione dei dati di formazione. Passiamo ora alle due sezioni seguenti.

### Dividi il set di dati {#split-the-dataset}

La fase di preparazione dei dati per la formazione richiede la suddivisione del set di dati da utilizzare per la formazione e il test. Questi dati `val` verranno utilizzati in modo implicito per valutare il modello dopo che è stato addestrato. Questo processo è separato dal punteggio.

In questa sezione viene mostrata la funzione `split()` che prima carica i dati nel blocco appunti, quindi pulisce i dati rimuovendo le colonne non collegate nel set di dati. Da lì, sarà possibile eseguire l&#39;ingegneria delle funzioni, che è il processo per creare ulteriori caratteristiche rilevanti dalle caratteristiche grezze esistenti nei dati. Un esempio di questo processo può essere visto di seguito insieme a una spiegazione.

La funzione `split()` è mostrata di seguito. Il dataframe fornito nell&#39;argomento verrà suddiviso nelle variabili `train` e `val` da restituire.

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### Valutare il modello addestrato {#evaluate-the-trained-model}

La funzione `evaluate()` viene eseguita dopo aver eseguito il training del modello e restituirà una metrica per indicare il successo del modello. La funzione `evaluate()` utilizza le etichette dei set di dati di prova e il modello Trained per prevedere un set di funzioni. Questi valori previsti vengono quindi confrontati con le funzioni effettive nel set di dati di test. Gli algoritmi di punteggio comuni includono:
- [Errore percentuale assoluta media (MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [Errore medio assoluto (MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [Errore quadrato medio radice (RMSE)](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


La funzione `evaluate()` nell&#39;esempio di vendita al dettaglio è mostrata di seguito:

```PYTHON
def evaluate(self, data=[], model={}, configProperties={}):
    print ("Evaluation evaluate triggered")
    val = data.drop('weeklySalesAhead', axis=1)
    y_pred = model.predict(val)
    y_actual = data['weeklySalesAhead'].values
    mape = np.mean(np.abs((y_actual - y_pred) / y_actual))
    mae = np.mean(np.abs(y_actual - y_pred))
    rmse = np.sqrt(np.mean((y_actual - y_pred) ** 2))

    metric = [{"name": "MAPE", "value": mape, "valueType": "double"},
                {"name": "MAE", "value": mae, "valueType": "double"},
                {"name": "RMSE", "value": rmse, "valueType": "double"}]

    return metric
```

La funzione restituisce un oggetto `metric` contenente una matrice di metriche di valutazione. Queste metriche verranno utilizzate per valutare le prestazioni del modello addestrato.

### File di Data Saver {#data-saver-file}

Il file `datasaver.py` contiene la funzione `save()` per salvare la previsione durante il test del punteggio. La funzione `save()` acquisirà la previsione e utilizzerà le API [!DNL Experience Platform Catalog], scriverà i dati nel `scoringResultsDataSetId` specificato nel file `scoring.conf`.

L&#39;esempio utilizzato nella ricetta di esempio per le vendite al dettaglio è riportato qui. Nota l’utilizzo della libreria `DataSetWriter` per scrivere dati in Platform:

```PYTHON
from data_access_sdk_python.writer import DataSetWriter

def save(configProperties, prediction):
    print("Datasaver Start")
    print("Setting up Writer")

    catalog_url = "https://platform.adobe.io/data/foundation/catalog"
    ingestion_url = "https://platform.adobe.io/data/foundation/import"

    writer = DataSetWriter(catalog_url=catalog_url,
                           ingestion_url=ingestion_url,
                           client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    print("Writer Configured")

    writer.write(data_set_id=configProperties['scoringResultsDataSetId'],
                 dataframe=prediction,
                 ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])

    print("Write Done")
    print("Datasaver Finish")
    print(prediction)
```

## Formazione e valutazione {#training-and-scoring}

Una volta apportate le modifiche al blocco appunti e desiderate addestrare la ricetta, potete fare clic sui pulsanti associati nella parte superiore della barra per creare un percorso di formazione nella cella. Facendo clic sul pulsante, nel blocco appunti (sotto la cella `evaluator.py`) viene visualizzato un registro di comandi e output dello script di formazione. Conda prima installa tutte le dipendenze, poi viene avviato il training.

Tieni presente che è necessario eseguire il corso di formazione almeno una volta prima di poter eseguire il punteggio. Facendo clic sul pulsante **[!UICONTROL Run Scoring]** si otterrà un punteggio sul modello addestrato generato durante l&#39;addestramento. Lo script di punteggio verrà visualizzato in `datasaver.py`.

A scopo di debug, se desideri visualizzare l’output nascosto, aggiungi `debug` alla fine della cella di output e rieseguiscila.

## Crea ricetta {#create-recipe}

Dopo aver modificato la ricetta e aver ottenuto l&#39;output di formazione/punteggio, è possibile creare una ricetta dal blocco appunti premendo **[!UICONTROL Create Recipe]** nella navigazione in alto a destra.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Dopo aver premuto il pulsante, viene richiesto di inserire un nome di ricetta. Questo nome rappresenta la ricetta effettiva creata su [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Una volta premuto **[!UICONTROL Ok]** sarà possibile passare alla nuova ricetta su [Adobe Experience Platform](https://platform.adobe.com/). Puoi fare clic sul pulsante **[!UICONTROL View Recipes]** per passare alla scheda **[!UICONTROL Recipes]** in **[!UICONTROL ML Models]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

Una volta completato il processo, la ricetta avrà un aspetto simile al seguente:

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
>
> - Non eliminare nessuna delle celle del file
> - Non modificare la riga `%%writefile` nella parte superiore delle celle del file
> - Non creare ricette contemporaneamente in diversi notebook


## Passaggi successivi {#next-steps}

Completando questa esercitazione, hai imparato a creare un modello di apprendimento automatico nel notebook Ricipe Builder. Hai anche imparato a utilizzare il blocco appunti per creare un flusso di lavoro di ricetta all&#39;interno del blocco appunti per creare una ricetta all&#39;interno di [!DNL Data Science Workspace].

Per continuare a imparare a lavorare con le risorse all’interno di [!DNL Data Science Workspace], visita il menu a discesa [!DNL Data Science Workspace] ricette e modelli .

## Risorse aggiuntive {#additional-resources}

Il video seguente è progettato per aiutarti a comprendere come creare e distribuire modelli.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)
