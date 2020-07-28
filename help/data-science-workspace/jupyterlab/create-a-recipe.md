---
keywords: Experience Platform;JupyterLab;recipe;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Creare una ricetta utilizzando i notebook Jupyter
topic: Tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2273'
ht-degree: 0%

---


# Creare una ricetta utilizzando i notebook Jupyter

Questa esercitazione si sovrappone a due sezioni principali. Innanzitutto, creerete un modello di machine learning utilizzando un modello all&#39;interno [!DNL JupyterLab Notebook]. Successivamente, verrà eseguito il flusso di lavoro di ricetta del blocco appunti [!DNL JupyterLab] per creare una ricetta all&#39;interno [!DNL Data Science Workspace].

## Concetti introdotti:

- **Ricette:** Una ricetta è  termine  Adobe per una specifica di modello ed è un contenitore di primo livello che rappresenta uno specifico machine learning, un algoritmo AI o un insieme di algoritmi, una logica di elaborazione e una configurazione necessarie per creare ed eseguire un modello qualificato e quindi aiutare a risolvere problemi aziendali specifici.
- **Modello:** Un modello è un&#39;istanza di una ricetta di machine learning che viene formata utilizzando dati storici e configurazioni per risolvere un caso d&#39;uso aziendale.
- **Formazione:** La formazione è il processo di apprendimento di schemi e approfondimenti da dati etichettati.
- **Punteggio:** Il punteggio è il processo di generazione di informazioni dai dati utilizzando un modello qualificato.

## Introduzione all&#39;ambiente [!DNL JupyterLab] notebook

È possibile creare una ricetta da zero all&#39;interno [!DNL Data Science Workspace]. Per iniziare, andate a [Adobe Experience Platform](https://platform.adobe.com) e fate clic sulla **[!UICONTROL Notebooks]** scheda a sinistra. Per creare un nuovo blocco appunti, selezionate il modello di Generatore di ricette dal pannello [!DNL JupyterLab Launcher].

Il [!UICONTROL Recipe Builder] notebook consente di eseguire corsi di formazione e punteggio all&#39;interno del notebook. Questo vi offre la flessibilità di apportare modifiche ai loro `train()` e `score()` metodi tra l&#39;esecuzione di esperimenti sui dati di formazione e punteggio. Una volta soddisfatti i risultati della formazione e del punteggio, è possibile creare una ricetta da utilizzare nell&#39; [!DNL Data Science Workspace] utilizzo del notebook per utilizzare le funzionalità di ricetta integrate nel notebook Recipe Builder.

>[!NOTE]
>
>
>Il notebook Recipe Builder supporta l&#39;utilizzo di tutti i formati di file, ma al momento la funzionalità Crea ricetta supporta solo [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe-builder.png)

Quando si fa clic sul blocco appunti di Recipe Builder dall&#39;avvio, il blocco appunti viene aperto nella scheda. Il modello utilizzato nel blocco appunti è la Ricetta di previsione delle vendite al dettaglio Python che si trova anche in [questo archivio pubblico](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

Nella barra degli strumenti sono disponibili tre azioni aggiuntive: - **[!UICONTROL Train]**, **[!UICONTROL Score]** e **[!UICONTROL Create Recipe]**. Queste icone verranno visualizzate solo nel [!UICONTROL Recipe Builder] blocco appunti. Ulteriori informazioni su queste azioni verranno discusse [nella sezione](#training-and-scoring) Formazione e punteggio dopo la creazione della Ricetta nel blocco appunti.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Apportare modifiche ai file di ricette

Per apportare modifiche ai file di ricetta, andate alla cella in Jupyter corrispondente al percorso del file. Ad esempio, se desiderate apportare modifiche a `evaluator.py`, cercate `%%writefile demo-recipe/evaluator.py`.

Iniziare a apportare le modifiche necessarie alla cella e, al termine, eseguire semplicemente la cella. Il `%%writefile filename.py` comando scriverà il contenuto della cella sul `filename.py`. Sarà necessario eseguire manualmente la cella per ogni file con modifiche.

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

### File dei requisiti {#requirements-file}

Il file dei requisiti viene utilizzato per dichiarare librerie aggiuntive da utilizzare nella ricetta. È possibile specificare il numero di versione in presenza di una dipendenza. Per ulteriori librerie, visitate https://anaconda.org. L&#39;elenco delle librerie principali già in uso include:

```JSON
python=3.5.2
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>
>Le librerie o versioni specifiche aggiunte potrebbero essere incompatibili con le librerie elencate sopra.

### File di configurazione {#configuration-files}

I file di configurazione `training.conf` e `scoring.conf`vengono utilizzati per specificare i set di dati da utilizzare per la formazione e il punteggio, nonché per aggiungere parametri ipertestuali. Sono disponibili configurazioni separate per la formazione e il punteggio.

Gli utenti devono compilare le seguenti variabili prima di eseguire formazione e punteggio:
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

Per trovare il set di dati e gli ID dello schema, andate alla scheda Dati all&#39;interno dei blocchi appunti nella barra di navigazione a sinistra (sotto l&#39;icona della cartella).

![](../images/jupyterlab/create-recipe/datasets.png)

Le stesse informazioni si trovano in [Adobe Experience Platform](https://platform.adobe.com/) nelle schede **[Schema](https://platform.adobe.com/schema)**e**[Set](https://platform.adobe.com/dataset/overview)** dati.

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

In questo passaggio viene utilizzato il [frame di dati](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)panda. I dati possono essere caricati da file [!DNL Adobe Experience Platform] utilizzando l&#39; [!DNL Platform] SDK (`platform_sdk`) o da origini esterne utilizzando i panda `read_csv()` o `read_json()` le funzioni.

- [!DNL Platform SDK](#platform-sdk)
- [Fonti esterne](#external-sources)

>[!NOTE]
>
>
>Nel blocco appunti di Recipe Builder, i dati vengono caricati tramite il `platform_sdk` caricatore dati.

### [!DNL Platform] SDK {#platform-sdk}

Per un&#39;esercitazione dettagliata sull&#39;utilizzo del `platform_sdk` caricatore dati, visita la guida [all&#39;SDK per](../authoring/platform-sdk.md)Platform. Questa esercitazione fornisce informazioni sull&#39;autenticazione della build, sulla lettura di base dei dati e sulla scrittura di base dei dati.

### Fonti esterne {#external-sources}

In questa sezione viene illustrato come importare un file JSON o CSV in un oggetto panda. La documentazione ufficiale della biblioteca pandas è disponibile qui:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Innanzitutto, ecco un esempio di importazione di un file CSV. L’ `data` argomento è il percorso del file CSV. Questa variabile è stata importata dalla `configProperties` nella sezione [](#configuration-files)precedente.

```PYTHON
df = pd.read_csv(data)
```

Potete anche importare da un file JSON. L’ `data` argomento è il percorso del file CSV. Questa variabile è stata importata dalla `configProperties` nella sezione [](#configuration-files)precedente.

```PYTHON
df = pd.read_json(data)
```

Ora i dati si trovano nell&#39;oggetto dataframe e possono essere analizzati e modificati nella sezione [](#data-preparation-and-feature-engineering)successiva.

### Dall&#39;SDK per l&#39;accesso ai dati (obsoleto)

>[!CAUTION]
>
>
> `data_access_sdk_python` non è più consigliato. Consulta [Converti codice di accesso ai dati in Platform SDK](../authoring/platform-sdk.md) per una guida sull&#39;utilizzo del `platform_sdk` caricatore di dati.

Gli utenti possono caricare i dati utilizzando l&#39;SDK per l&#39;accesso ai dati. La libreria può essere importata nella parte superiore della pagina includendo la riga:

`from data_access_sdk_python.reader import DataSetReader`

Quindi utilizziamo il `load()` metodo per acquisire il set di dati di formazione dal `trainingDataSetId` set nel nostro file di configurazione (`recipe.conf`).

```PYTHON
prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

df = prodreader.load(data_set_id=configProperties['trainingDataSetId'],
                     ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

>[!NOTE]
>
>
>Come indicato nella sezione [File di](#configuration-files)configurazione, i seguenti parametri di configurazione vengono impostati automaticamente quando si accede ai dati da [!DNL Experience Platform]:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Ora che hai i tuoi dati, puoi iniziare con la preparazione dei dati e la progettazione di funzionalità.

### Preparazione dei dati e progettazione di funzionalità {#data-preparation-and-feature-engineering}

Una volta caricati i dati, questi vengono sottoposti a preparazione e quindi suddivisi nei `train` set di dati e `val` nei set di dati. Di seguito è riportato un esempio di codice:

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
- aggiunta `week` e `year` colonne
- converti `storeType` in una variabile indicatore
- convertire `isHoliday` in variabile numerica
- offset `weeklySales` per ottenere valore di vendita futuro e passato
- suddividere i dati, per data, in `train` e `val` set di dati

Innanzitutto, `week` vengono create `year` colonne e la `date` colonna originale viene convertita in [!DNL Python] datetime [](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html). I valori relativi a settimana e anno sono estratti dall&#39;oggetto datetime.

Successivamente `storeType` viene convertita in tre colonne che rappresentano i tre diversi tipi di store (`A`, `B`e `C`). Ciascuno di essi conterrà un valore booleano per indicare che `storeType` è vero. La `storeType` colonna verrà eliminata.

Analogamente, `weeklySales` imposta il valore `isHoliday` booleano su una rappresentazione numerica, uno o zero.

Questi dati sono suddivisi tra `train` set di dati e `val` set di dati.

La `load()` funzione deve completare con il `train` `val` set di dati e il set di dati come output.

### Caricatore dati punteggio {#scoring-data-loader}

La procedura per caricare i dati per il punteggio è simile ai dati di formazione di caricamento nella `split()` funzione. Utilizziamo l’SDK per l’accesso ai dati per caricare i dati dal `scoringDataSetId` `recipe.conf` file trovato.

```PYTHON
def load(configProperties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                               user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                               service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    df = prodreader.load(data_set_id=configProperties['scoringDataSetId'],
                         ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

Dopo il caricamento dei dati, la preparazione dei dati e la progettazione delle funzioni vengono eseguite.

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
df.date = pd.to_datetime(df.date)
df['week'] = df.date.dt.week
df['year'] = df.date.dt.year

df = pd.concat([df, pd.get_dummies(df['storeType'])], axis=1)
df.drop('storeType', axis=1, inplace=True)
df['isHoliday'] = df['isHoliday'].astype(int)

df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
df.dropna(0, inplace=True)

df = df.set_index(df.date)
df.drop('date', axis=1, inplace=True)

print("Scoring Data Load Finish")

return df
```

Poiché lo scopo del nostro modello è prevedere le vendite settimanali future, sarà necessario creare un set di dati di punteggio utilizzato per valutare le prestazioni della previsione del modello.

Questo notebook Recipe Builder lo fa compensando la nostra vendita settimanale 7 giorni in avanti. Notate che esistono misure per 45 punti vendita a settimana in modo da poter spostare i `weeklySales` valori 45 set di dati in avanti in una nuova colonna denominata `weeklySalesAhead`.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

Allo stesso modo, potete creare una colonna `weeklySalesLag` spostando indietro di 45. In questo modo è anche possibile calcolare la differenza nelle vendite settimanali e memorizzarle in colonna `weeklySalesDiff`.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

Poiché si sta effettuando l&#39;offset dei `weeklySales` punti dati 45 in avanti e 45 in indietro per creare nuove colonne, i primi e gli ultimi 45 punti dati avranno valori NaN. È possibile rimuovere questi punti dal nostro dataset utilizzando la `df.dropna()` funzione che rimuove tutte le righe che hanno valori NaN.

```PYTHON
df.dropna(0, inplace=True)
```

La `load()` funzione nel caricatore dei dati di punteggio deve essere completa con il set di dati di punteggio come output.

### File pipeline {#pipeline-file}

Il `pipeline.py` file include logica per la formazione e il punteggio.

### Formazione {#training}

Lo scopo della formazione è quello di creare un modello utilizzando le funzioni e le etichette presenti nel dataset di formazione.

>[!NOTE]
>
> 
>_Le funzioni_ fanno riferimento alla variabile di input utilizzata dal modello di apprendimento automatico per prevedere le _etichette_.

La `train()` funzione deve includere il modello di addestramento e restituire il modello addestrato. Alcuni esempi di diversi modelli sono disponibili nella documentazione [della guida](https://scikit-learn.org/stable/user_guide.html)scikit-learn utente.

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

A seconda dell&#39;applicazione, la `GradientBoostingRegressor()` funzione avrà argomenti. `xTrainingDataset` devono contenere le funzioni utilizzate per la formazione, mentre `yTrainingDataset` devono contenere le etichette.

### Punteggio {#scoring}

La `score()` funzione deve contenere l&#39;algoritmo di valutazione e restituire una misura per indicare l&#39;efficacia del modello. La `score()` funzione utilizza le etichette del set di dati di punteggio e il modello addestrato per generare un insieme di funzioni previste. Questi valori predetti vengono quindi confrontati con le funzioni effettive nel dataset di valutazione. In questo esempio, la `score()` funzione utilizza il modello preparato per prevedere le feature utilizzando le etichette del set di dati di punteggio. Vengono restituite le funzioni previste.

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

Il `evaluator.py` file contiene la logica per la valutazione della ricetta formata e per la suddivisione dei dati di formazione. Nell’esempio di vendita al dettaglio, verrà inclusa la logica per il caricamento e la preparazione dei dati di formazione. Passeremo alle due sezioni seguenti.

### Dividere il set di dati {#split-the-dataset}

La fase di preparazione dei dati per la formazione richiede la suddivisione del set di dati per la formazione e il test. Questi `val` dati saranno utilizzati in modo implicito per valutare il modello dopo che sarà stato addestrato. Questo processo è separato dal punteggio.

Questa sezione mostra la `split()` funzione che prima caricherà i dati nel blocco appunti, quindi pulirà i dati rimuovendo colonne non correlate nel set di dati. Da qui, sarà possibile eseguire l&#39;ingegneria delle caratteristiche, che è il processo per creare ulteriori caratteristiche rilevanti dalle caratteristiche grezze esistenti nei dati. Di seguito è riportato un esempio di questo processo con una spiegazione.

La `split()` funzione è mostrata di seguito. Il dataframe fornito nell&#39;argomento sarà suddiviso nelle `train` variabili e `val` le variabili da restituire.

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### Valutare il modello preparato {#evaluate-the-trained-model}

La `evaluate()` funzione viene eseguita dopo che il modello è stato addestrato e restituirà una metrica per indicare il successo del modello. La `evaluate()` funzione utilizza le etichette del set di dati di prova e il modello Traine per prevedere un insieme di funzioni. Questi valori predetti vengono quindi confrontati con le funzioni effettive nel set di dati di test. Gli algoritmi comuni di punteggio includono:
- [Errore medio percentuale assoluta (MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [Errore medio assoluto (MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [Errore radice quadrato (RMSE)](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


La `evaluate()` funzione nell&#39;esempio di vendita al dettaglio è indicata di seguito:

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

Tenere presente che la funzione restituisce un `metric` oggetto contenente un array di metriche di valutazione. Tali metriche verranno utilizzate per valutare le prestazioni del modello preparato.

### File Data Saver {#data-saver-file}

Il `datasaver.py` file contiene la `save()` funzione per salvare la previsione durante il test del punteggio. La `save()` funzione prenderà la previsione e utilizzando [!DNL Experience Platform Catalog] le API, scriverà i dati al `scoringResultsDataSetId` specificato nel `scoring.conf` file.

L&#39;esempio utilizzato nella ricetta di esempio per le vendite al dettaglio è riportato di seguito. Prendete nota dell&#39;utilizzo della `DataSetWriter` libreria per scrivere dati in Platform:

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

Dopo aver apportato le modifiche al blocco appunti e aver scelto di addestrare la ricetta, potete fare clic sui pulsanti associati nella parte superiore della barra per creare una sequenza di formazione nella cella. Facendo clic sul pulsante, nel blocco appunti (sotto la `evaluator.py` cella) viene visualizzato un registro di comandi e output dello script di formazione. Conda prima installa tutte le dipendenze, quindi la formazione viene avviata.

È necessario eseguire la formazione almeno una volta prima di poter eseguire il punteggio. Facendo clic sul **[!UICONTROL Run Scoring]** pulsante si ottiene un punteggio sul modello preparato generato durante l&#39;addestramento. Lo script di punteggio verrà visualizzato sotto `datasaver.py`.

Per il debug, se si desidera visualizzare l&#39;output nascosto, aggiungere `debug` alla fine della cella di output e rieseguirla.

## Creare una ricetta {#create-recipe}

Dopo aver modificato la ricetta e aver ottenuto l’output di formazione/punteggio, è possibile creare una ricetta dal blocco appunti premendo **[!UICONTROL Create Recipe]** nella navigazione in alto a destra.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Dopo aver premuto il pulsante, viene richiesto di immettere un nome per la ricetta. Questo nome rappresenta la ricetta effettiva creata in [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Una volta premuto **[!UICONTROL Ok]** sarà possibile passare alla nuova ricetta sul [Adobe Experience Platform](https://platform.adobe.com/). Puoi fare clic sul **[!UICONTROL View Recipes]** pulsante per portarti alla **[!UICONTROL Recipes]** scheda sotto **[!UICONTROL ML Models]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

Una volta completato il processo, la ricetta avrà un aspetto simile al seguente:

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
> - Non eliminare alcuna cella del file
> - Non modificare la `%%writefile` riga nella parte superiore delle celle del file
> - Non creare allo stesso tempo ricette in diversi notebook


## Passaggi successivi {#next-steps}

Completando questa esercitazione hai imparato a creare un modello di machine learning nel notebook Recipe Builder. Hai anche imparato a utilizzare il blocco appunti per definire il flusso di lavoro all&#39;interno del blocco appunti per creare una ricetta all&#39;interno [!DNL Data Science Workspace].

Per continuare a imparare a lavorare con le risorse all&#39;interno [!DNL Data Science Workspace], visita il menu a discesa [!DNL Data Science Workspace] ricette e modelli.

## Risorse aggiuntive {#additional-resources}

Il seguente video è stato progettato per consentire agli utenti di comprendere meglio come creare e implementare modelli.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)


