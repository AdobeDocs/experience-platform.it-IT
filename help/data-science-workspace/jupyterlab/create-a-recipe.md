---
keywords: ' Experience Platform;JupyterLab;ricetta;notebook;Data Science Workspace;argomenti più comuni;creare ricetta'
solution: Experience Platform
title: Creazione di una ricetta tramite Jupyter Notebooks
topic: tutorial
type: Tutorial
description: Questa esercitazione si sovrappone a due sezioni principali. Innanzitutto, si crea un modello di machine learning utilizzando un modello all'interno di JupyterLab Notebook. Successivamente, si eserciterà il notebook per il flusso di lavoro delle ricette in JupyterLab per creare una ricetta all'interno di Data Science Workspace.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '2343'
ht-degree: 0%

---


# Creazione di una ricetta tramite Jupyter Notebooks

Questa esercitazione si sovrappone a due sezioni principali. Innanzitutto, creerete un modello di machine learning utilizzando un modello all&#39;interno di [!DNL JupyterLab Notebook]. Successivamente, verrà eseguito il flusso di lavoro di ricetta del blocco appunti all&#39;interno di [!DNL JupyterLab] per creare una ricetta all&#39;interno di [!DNL Data Science Workspace].

## Concetti introdotti:

- **Ricette:** Una ricetta è  termine  Adobe per una specifica di modello ed è un contenitore di primo livello che rappresenta uno specifico machine learning, un algoritmo AI o un insieme di algoritmi, logica di elaborazione e configurazione necessari per creare ed eseguire un modello qualificato e quindi aiutare a risolvere problemi aziendali specifici.
- **Modello:** Un modello è un&#39;istanza di una ricetta di machine learning che viene formata utilizzando dati storici e configurazioni per risolvere un caso d&#39;uso aziendale.
- **Formazione:** Formazione è il processo di apprendimento di schemi e approfondimenti da dati etichettati.
- **Punteggio:** Punteggio è il processo di generazione di approfondimenti dai dati utilizzando un modello qualificato.

## Introduzione all&#39;ambiente [!DNL JupyterLab] notebook

La creazione di una ricetta da zero può essere effettuata all&#39;interno di [!DNL Data Science Workspace]. Per iniziare, passare a [Adobe Experience Platform](https://platform.adobe.com) e fare clic sulla scheda **[!UICONTROL Notebooks]** a sinistra. Per creare un nuovo blocco appunti, selezionate il modello di Generatore di ricette dal [!DNL JupyterLab Launcher].

Il notebook [!UICONTROL Recipe Builder] consente di eseguire attività di formazione e punteggio all&#39;interno del notebook. Questo offre la flessibilità di apportare modifiche ai metodi `train()` e `score()` tra l&#39;esecuzione di esperimenti sui dati di formazione e valutazione. Una volta soddisfatti i risultati della formazione e del punteggio, è possibile creare una ricetta da utilizzare in [!DNL Data Science Workspace] utilizzando il notebook per la funzionalità di ricetta integrata nel notebook Recipe Builder.

>[!NOTE]
>
>Il notebook Recipe Builder supporta l&#39;utilizzo di tutti i formati di file, ma attualmente la funzionalità Crea ricetta supporta solo [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder.png)

Quando si fa clic sul blocco appunti di Recipe Builder dall&#39;avvio, il blocco appunti viene aperto nella scheda. Il modello utilizzato nel blocco appunti è la Ricetta di previsione delle vendite al dettaglio Python che si trova anche in [questo repository pubblico](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

Nella barra degli strumenti sono disponibili tre azioni aggiuntive: **[!UICONTROL Train]**, **[!UICONTROL Score]** e **[!UICONTROL Create Recipe]**. Queste icone vengono visualizzate solo nel blocco appunti [!UICONTROL Recipe Builder]. Ulteriori informazioni su queste azioni verranno fornite nella sezione [formazione e punteggio](#training-and-scoring) dopo la creazione della Ricetta nel blocco appunti.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Apportare modifiche ai file di ricette

Per apportare modifiche ai file di ricetta, andate alla cella in Jupyter corrispondente al percorso del file. Ad esempio, se desiderate apportare modifiche a `evaluator.py`, cercate `%%writefile demo-recipe/evaluator.py`.

Iniziare a apportare le modifiche necessarie alla cella e, al termine, eseguire semplicemente la cella. Il comando `%%writefile filename.py` scriverà il contenuto della cella in `filename.py`. Sarà necessario eseguire manualmente la cella per ogni file con modifiche.

>[!NOTE]
>
>Se necessario, eseguire le celle manualmente.

## Introduzione al notebook Recipe Builder

Ora che si conoscono le basi per l&#39;ambiente [!DNL JupyterLab] notebook, è possibile iniziare a guardare i file che compongono una ricetta modello di apprendimento automatico. I file di cui parleremo sono mostrati qui:

- [File dei requisiti](#requirements-file)
- [File di configurazione](#configuration-files)
- [Caricatore dati formazione](#training-data-loader)
- [Caricatore dati punteggio](#scoring-data-loader)
- [File pipeline](#pipeline-file)
- [File di valutazione](#evaluator-file)
- [File Data Saver](#data-saver-file)

### File di requisiti {#requirements-file}

Il file dei requisiti viene utilizzato per dichiarare librerie aggiuntive da utilizzare nella ricetta. È possibile specificare il numero di versione in presenza di una dipendenza. Per cercare ulteriori librerie, visitare [anaconda.org](https://anaconda.org). Per informazioni su come formattare il file dei requisiti, visitare [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). L&#39;elenco delle librerie principali già in uso include:

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>Le librerie o versioni specifiche aggiunte potrebbero essere incompatibili con le librerie elencate sopra. Inoltre, se scegliete di creare manualmente un file di ambiente, il campo `name` non può essere ignorato.

### File di configurazione {#configuration-files}

I file di configurazione `training.conf` e `scoring.conf` vengono utilizzati per specificare i set di dati da utilizzare per la formazione e il punteggio, nonché per aggiungere parametri ipertestuali. Sono disponibili configurazioni separate per la formazione e il punteggio.

Gli utenti devono compilare le seguenti variabili prima di eseguire formazione e punteggio:
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

Per trovare il set di dati e gli ID dello schema, andate alla scheda Dati all&#39;interno dei blocchi appunti nella barra di navigazione a sinistra (sotto l&#39;icona della cartella).

![](../images/jupyterlab/create-recipe/datasets.png)

Le stesse informazioni si trovano nelle schede [Adobe Experience Platform](https://platform.adobe.com/) **[Schema](https://platform.adobe.com/schema)** e **[Dataset](https://platform.adobe.com/dataset/overview)**.

Per impostazione predefinita, quando si accede ai dati vengono impostati i seguenti parametri di configurazione:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Caricatore dati formazione {#training-data-loader}

Lo scopo di Training Data Loader è di creare un&#39;istanza dei dati utilizzati per creare il modello di apprendimento automatico. In genere, il caricatore dati formazione esegue due attività:
- Carica dati da [!DNL Platform]
- Preparazione dei dati e progettazione di funzionalità

Nelle due sezioni seguenti verranno analizzati il caricamento dei dati e la preparazione dei dati.

### Caricamento dei dati {#loading-data}

Questo passaggio utilizza il [panda dataframe](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). I dati possono essere caricati da file in [!DNL Adobe Experience Platform] utilizzando l&#39;SDK [!DNL Platform] (`platform_sdk`) oppure da origini esterne utilizzando le funzioni panda `read_csv()` o `read_json()`.

- [[!DNL Platform SDK]](#platform-sdk)
- [Fonti esterne](#external-sources)

>[!NOTE]
>
>Nel notebook Recipe Builder, i dati vengono caricati tramite il caricatore di dati `platform_sdk`.

### [!DNL Platform] SDK {#platform-sdk}

Per un&#39;esercitazione dettagliata sull&#39;utilizzo del caricatore di dati `platform_sdk`, visitare la [Guida SDK della piattaforma](../authoring/platform-sdk.md). Questa esercitazione fornisce informazioni sull&#39;autenticazione della build, sulla lettura di base dei dati e sulla scrittura di base dei dati.

### Origini esterne {#external-sources}

In questa sezione viene illustrato come importare un file JSON o CSV in un oggetto panda. La documentazione ufficiale della biblioteca pandas è disponibile qui:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Innanzitutto, ecco un esempio di importazione di un file CSV. L&#39;argomento `data` rappresenta il percorso del file CSV. Questa variabile è stata importata dalla `configProperties` nella [sezione precedente](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

Potete anche importare da un file JSON. L&#39;argomento `data` rappresenta il percorso del file CSV. Questa variabile è stata importata dalla `configProperties` nella [sezione precedente](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

Ora i dati si trovano nell&#39;oggetto dataframe e possono essere analizzati e modificati nella sezione [successiva](#data-preparation-and-feature-engineering).

### Da SDK piattaforma

Puoi caricare i dati tramite l’SDK della piattaforma. La libreria può essere importata nella parte superiore della pagina includendo la riga:

`from platform_sdk.dataset_reader import DatasetReader`

Quindi utilizziamo il metodo `load()` per acquisire il dataset di formazione dal `trainingDataSetId` come impostato nel file di configurazione (`recipe.conf`).

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
>Come indicato nella sezione [File di configurazione](#configuration-files), i seguenti parametri di configurazione vengono impostati automaticamente quando si accede ai dati da  Experience Platform utilizzando `client_context`:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Ora che hai i tuoi dati, puoi iniziare con la preparazione dei dati e la progettazione di funzionalità.

### Preparazione dei dati e progettazione delle funzionalità {#data-preparation-and-feature-engineering}

Una volta caricati i dati, questi vengono sottoposti a preparazione e quindi suddivisi nei set di dati `train` e `val`. Di seguito è riportato un esempio di codice:

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

In questo esempio, al set di dati originale vengono eseguite cinque operazioni:
- aggiungere le colonne `week` e `year`
- convertire `storeType` in una variabile indicatore
- convertire `isHoliday` in una variabile numerica
- offset `weeklySales` per ottenere il valore delle vendite future e passate
- suddividere i dati, per data, in base al `train` e `val` dataset

Innanzitutto, vengono create le colonne `week` e `year` e la colonna `date` originale viene convertita in [!DNL Python] [datetime](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html). I valori relativi a settimana e anno sono estratti dall&#39;oggetto datetime.

Successivamente, `storeType` viene convertito in tre colonne che rappresentano i tre diversi tipi di store (`A`, `B` e `C`). Ciascuno di essi conterrà un valore booleano per indicare che `storeType` è true. La colonna `storeType` verrà eliminata.

Analogamente, `weeklySales` modifica il valore booleano `isHoliday` in una rappresentazione numerica, uno o zero.

Questi dati sono suddivisi tra `train` e `val` dataset.

La funzione `load()` deve essere completa con il dataset `train` e `val` come output.

### Caricatore dati punteggio {#scoring-data-loader}

La procedura per caricare i dati per il punteggio è simile ai dati di formazione di caricamento nella funzione `split()`. L&#39;SDK di accesso ai dati viene utilizzato per caricare i dati dal `scoringDataSetId` presente nel nostro file `recipe.conf`.

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

Dopo il caricamento dei dati, la preparazione dei dati e la progettazione delle funzioni vengono eseguite.

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

Poiché lo scopo del nostro modello è prevedere le vendite settimanali future, sarà necessario creare un set di dati di punteggio utilizzato per valutare le prestazioni della previsione del modello.

Questo notebook Recipe Builder lo fa compensando la nostra vendita settimanale 7 giorni in avanti. Tenere presente che esistono misure per 45 punti vendita a settimana, per cui è possibile spostare in avanti i valori `weeklySales` 45 set di dati in una nuova colonna denominata `weeklySalesAhead`.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

Allo stesso modo, potete creare una colonna `weeklySalesLag` spostando indietro di 45. In questo modo è anche possibile calcolare la differenza nelle vendite settimanali e memorizzarle nella colonna `weeklySalesDiff`.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

Poiché si esegue l&#39;offset dei `weeklySales` datapoint 45 dataset in avanti e 45 dataset all&#39;indietro per creare nuove colonne, i primi e gli ultimi 45 punti dati avranno valori NaN. È possibile rimuovere questi punti dal nostro dataset utilizzando la funzione `df.dropna()` che rimuove tutte le righe che hanno valori NaN.

```PYTHON
df.dropna(0, inplace=True)
```

La funzione `load()` nel loader dei dati di punteggio deve essere completata con il dataset di valutazione come output.

### File pipeline {#pipeline-file}

Il file `pipeline.py` include logica per la formazione e il punteggio.

### Formazione {#training}

Lo scopo della formazione è quello di creare un modello utilizzando le funzioni e le etichette presenti nel dataset di formazione.

>[!NOTE]
> 
>Le funzioni fanno riferimento alla variabile di input utilizzata dal modello di apprendimento automatico per prevedere le etichette.

La funzione `train()` deve includere il modello di formazione e restituire il modello addestrato. Alcuni esempi di diversi modelli sono disponibili nella [documentazione della guida utente di ](https://scikit-learn.org/stable/user_guide.html).

Dopo aver scelto il modello di formazione, inserirete il set di dati x e y della formazione nel modello e la funzione restituirà il modello preparato. Esempio che mostra quanto segue:

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

Tenere presente che, a seconda dell&#39;applicazione, la funzione `GradientBoostingRegressor()` contiene argomenti. `xTrainingDataset` devono contenere le funzioni utilizzate per la formazione e  `yTrainingDataset` contenere le etichette.

### Punteggio {#scoring}

La funzione `score()` deve contenere l&#39;algoritmo di valutazione e restituire una misura per indicare il successo del modello. La funzione `score()` utilizza le etichette del set di dati di punteggio e il modello addestrato per generare una serie di funzioni previste. Questi valori predetti vengono quindi confrontati con le funzioni effettive nel dataset di valutazione. In questo esempio, la funzione `score()` utilizza il modello addestrato per prevedere le caratteristiche utilizzando le etichette del set di dati di punteggio. Vengono restituite le funzioni previste.

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

Il file `evaluator.py` contiene la logica per la valutazione della ricetta formata e per la suddivisione dei dati di formazione. Nell’esempio di vendita al dettaglio, verrà inclusa la logica per il caricamento e la preparazione dei dati di formazione. Passeremo alle due sezioni seguenti.

### Dividi il set di dati {#split-the-dataset}

La fase di preparazione dei dati per la formazione richiede la suddivisione del set di dati per la formazione e il test. Questi dati `val` verranno utilizzati in modo implicito per valutare il modello dopo che è stato addestrato. Questo processo è separato dal punteggio.

In questa sezione viene mostrata la funzione `split()` che prima caricherà i dati nel blocco appunti, quindi pulirà i dati rimuovendo colonne non correlate nel set di dati. Da qui, sarà possibile eseguire l&#39;ingegneria delle caratteristiche, che è il processo per creare ulteriori caratteristiche rilevanti dalle caratteristiche grezze esistenti nei dati. Di seguito è riportato un esempio di questo processo con una spiegazione.

La funzione `split()` è illustrata di seguito. Il dataframe fornito nell&#39;argomento sarà suddiviso nelle variabili `train` e `val` da restituire.

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

La funzione `evaluate()` viene eseguita dopo che il modello è stato preparato e restituirà una metrica per indicare l&#39;efficacia del modello. La funzione `evaluate()` utilizza le etichette del set di dati di prova e il modello Traine per prevedere un insieme di funzioni. Questi valori predetti vengono quindi confrontati con le funzioni effettive nel set di dati di test. Gli algoritmi comuni di punteggio includono:
- [Errore medio percentuale assoluta (MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [Errore medio assoluto (MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [Errore radice quadrato (RMSE)](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


La funzione `evaluate()` nell&#39;esempio di vendita al dettaglio è indicata di seguito:

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

Tenere presente che la funzione restituisce un oggetto `metric` contenente un array di metriche di valutazione. Tali metriche verranno utilizzate per valutare le prestazioni del modello preparato.

### File Data Saver {#data-saver-file}

Il file `datasaver.py` contiene la funzione `save()` per salvare la previsione durante il test del punteggio. La funzione `save()` prenderà la previsione e utilizzando [!DNL Experience Platform Catalog] API, scriverà i dati nella `scoringResultsDataSetId` specificata nel file `scoring.conf`.

L&#39;esempio utilizzato nella ricetta di esempio per le vendite al dettaglio è riportato di seguito. Prendete nota dell&#39;utilizzo della libreria `DataSetWriter` per scrivere dati in Platform:

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

## Formazione e punteggio {#training-and-scoring}

Dopo aver apportato le modifiche al blocco appunti e aver scelto di addestrare la ricetta, potete fare clic sui pulsanti associati nella parte superiore della barra per creare una sequenza di formazione nella cella. Quando si fa clic sul pulsante, nel blocco appunti (sotto la cella `evaluator.py`) viene visualizzato un registro di comandi e output dello script di formazione. Conda prima installa tutte le dipendenze, quindi la formazione viene avviata.

È necessario eseguire la formazione almeno una volta prima di poter eseguire il punteggio. Facendo clic sul pulsante **[!UICONTROL Run Scoring]** si ottiene un punteggio sul modello preparato generato durante l&#39;addestramento. Lo script di punteggio verrà visualizzato in `datasaver.py`.

Per il debug, se si desidera visualizzare l&#39;output nascosto, aggiungere `debug` alla fine della cella di output e rieseguirla.

## Creare la ricetta {#create-recipe}

Dopo aver modificato la ricetta e aver ottenuto l&#39;output di formazione/punteggio, è possibile creare una ricetta dal blocco appunti premendo **[!UICONTROL Create Recipe]** nella navigazione in alto a destra.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Dopo aver premuto il pulsante, viene richiesto di immettere un nome per la ricetta. Questo nome rappresenta la ricetta effettiva creata in [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Una volta premuto **[!UICONTROL Ok]** sarà possibile passare alla nuova ricetta su [Adobe Experience Platform](https://platform.adobe.com/). È possibile fare clic sul pulsante **[!UICONTROL View Recipes]** per passare alla scheda **[!UICONTROL Recipes]** in **[!UICONTROL ML Models]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

Una volta completato il processo, la ricetta avrà un aspetto simile al seguente:

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
>
> - Non eliminare alcuna cella del file
> - Non modificare la riga `%%writefile` nella parte superiore delle celle del file
> - Non creare allo stesso tempo ricette in diversi notebook


## Passaggi successivi {#next-steps}

Completando questa esercitazione hai imparato a creare un modello di machine learning nel notebook Recipe Builder. Hai anche imparato a utilizzare il blocco appunti per creare un flusso di lavoro di ricetta all&#39;interno del blocco appunti per creare una ricetta all&#39;interno di [!DNL Data Science Workspace].

Per continuare a imparare a utilizzare le risorse all&#39;interno di [!DNL Data Science Workspace], visita il menu a discesa [!DNL Data Science Workspace] ricette e modelli.

## Risorse aggiuntive {#additional-resources}

Il seguente video è stato progettato per consentire agli utenti di comprendere meglio come creare e implementare modelli.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)


