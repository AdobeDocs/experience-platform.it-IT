---
keywords: Experience Platform;Tutorial;feature pipeline;Data Science Workspace;popular topic
title: Creare una pipeline di feature utilizzando l’SDK per l’authoring del modello
type: Tutorial
description: Adobe Experience Platform consente di creare e creare pipeline di funzioni personalizzate per eseguire attività di progettazione delle funzioni su larga scala tramite Sensei Machine Learning Framework Runtime. Questo documento descrive le varie classi presenti in una pipeline di funzioni e fornisce un tutorial dettagliato per la creazione di una pipeline di funzioni personalizzata tramite l’SDK per l’authoring dei modelli in PySpark.
exl-id: c2c821d5-7bfb-4667-ace9-9566e6754f98
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 0%

---

# Creare una pipeline di feature utilizzando l&#39;SDK per la creazione del modello (Model Authoring)

>[!IMPORTANT]
>
> Le pipeline delle funzioni sono attualmente disponibili solo tramite API.

Adobe Experience Platform consente di creare e creare pipeline di funzioni personalizzate per eseguire attività di progettazione delle funzioni su larga scala tramite Sensei Machine Learning Framework Runtime (di seguito denominato &quot;Runtime&quot;).

Questo documento descrive le varie classi presenti in una pipeline di funzioni e fornisce un tutorial dettagliato per la creazione di una pipeline di funzioni personalizzata utilizzando [SDK per authoring modelli](./sdk.md) a PySpark.

Durante l’esecuzione di una pipeline di funzioni si verifica il seguente flusso di lavoro:

1. La ricetta carica il set di dati in una pipeline.
2. La trasformazione delle funzionalità viene eseguita sul set di dati e viene riscritta in Adobe Experience Platform.
3. I dati trasformati vengono caricati per l’apprendimento.
4. La tubazione della feature definisce gli stadi con il Regressore di incremento della sfumatura come modello scelto.
5. La pipeline viene utilizzata per adattarsi ai dati di addestramento e viene creato il modello addestrato.
6. Il modello viene trasformato con il set di dati di punteggio.
7. Le colonne interessanti dell’output vengono quindi selezionate e salvate nuovamente in [!DNL Experience Platform] con i dati associati.

## Introduzione

Per eseguire una composizione in qualsiasi organizzazione, è necessario quanto segue:
- Un set di dati di input.
- Lo schema del set di dati.
- Schema trasformato e set di dati vuoto basato su tale schema.
- Uno schema di output e un set di dati vuoto basato su tale schema.

Tutti i set di dati sopra indicati devono essere caricati in [!DNL Platform] UI. Per configurare questa impostazione, utilizza l’ fornito dall’ Adobe [script bootstrap](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap).

## Classi di pipeline delle funzioni

La tabella seguente descrive le principali classi astratte che è necessario estendere per creare una pipeline di funzioni:

| Classe astratta | Descrizione |
| -------------- | ----------- |
| DataLoader | Una classe DataLoader fornisce l&#39;implementazione per il recupero dei dati di input. |
| DatasetTransformer | Una classe DatasetTransformer fornisce implementazioni per trasformare il set di dati di input. È possibile scegliere di non fornire una classe DatasetTransformer e implementare la logica di ingegneria delle caratteristiche all&#39;interno della classe FeaturePipelineFactory. |
| FeaturePipelineFactory | Una classe FeaturePipelineFactory crea una pipeline Spark composta da una serie di trasformatori Spark per eseguire l&#39;ingegneria delle feature. È possibile scegliere di non fornire una classe FeaturePipelineFactory e implementare la logica di ingegneria delle caratteristiche all&#39;interno della classe DatasetTransformer. |
| DataSaver | Una classe DataSaver fornisce la logica per l&#39;archiviazione di un set di dati di funzionalità. |

Quando viene avviato un processo Pipeline di funzionalità, il runtime esegue prima DataLoader per caricare i dati di input come DataFrame e quindi modifica il DataFrame eseguendo DatasetTransformer, FeaturePipelineFactory o entrambi. Infine, il set di dati della feature risultante viene memorizzato tramite DataSaver.

Il seguente diagramma mostra l’ordine di esecuzione del runtime:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Implementare le classi della pipeline delle funzioni {#implement-your-feature-pipeline-classes}

Le sezioni seguenti forniscono dettagli ed esempi sull’implementazione delle classi richieste per una pipeline di funzioni.

### Definire le variabili nel file JSON di configurazione {#define-variables-in-the-configuration-json-file}

Il file JSON di configurazione è costituito da coppie chiave-valore ed è concepito per specificare eventuali variabili da definire successivamente durante il runtime. Queste coppie chiave-valore possono definire proprietà quali la posizione del set di dati di input, l’ID del set di dati di output, l’ID tenant, le intestazioni di colonna e così via.

L’esempio seguente illustra le coppie chiave-valore presenti all’interno di un file di configurazione:

**Esempio JSON di configurazione**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "dataset_id",
                "value": "000"
            },
            {
                "key": "featureDatasetId",
                "value": "111"
            },
            {
                "key": "tenantId",
                "value": "_tenantid"
            }
        ]
    }
]
```

Puoi accedere alla configurazione JSON tramite qualsiasi metodo di classe che definisce `config_properties` come parametro. Ad esempio:

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

Consulta la [pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) fornito da Data Science Workspace per un esempio di configurazione più approfondito.

### Preparare i dati di input con DataLoader {#prepare-the-input-data-with-dataloader}

DataLoader è responsabile del recupero e del filtraggio dei dati di input. L’implementazione di DataLoader deve estendere la classe astratta `DataLoader` e sovrascrivi il metodo astratto `load`.

L’esempio seguente recupera un [!DNL Platform] e lo restituisce come DataFrame, dove l’ID del set di dati (`dataset_id`) è una proprietà definita nel file di configurazione.

**Esempio di PySpark**

```python
# PySpark

from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
import logging

class MyDataLoader(DataLoader):
    def load_dataset(config_properties, spark, tenant_id, dataset_id):
    PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
    PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

    service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
    user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
    org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
    api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

    dataset_id = str(config_properties.get(dataset_id))

    for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
        if eval(arg) == 'None':
            raise ValueError("%s is empty" % arg)

    query_options = get_query_options(spark.sparkContext)

    pd = spark.read.format(PLATFORM_SDK_PQS_PACKAGE) \
        .option(query_options.userToken(), user_token) \
        .option(query_options.serviceToken(), service_token) \
        .option(query_options.imsOrg(), org_id) \
        .option(query_options.apiKey(), api_key) \
        .option(query_options.mode(), PLATFORM_SDK_PQS_INTERACTIVE) \
        .option(query_options.datasetId(), dataset_id) \
        .load()
    pd.show()

    # Get the distinct values of the dataframe
    pd = pd.distinct()

    # Flatten the data
    if tenant_id in pd.columns:
        pd = pd.select(col(tenant_id + ".*"))

    return pd
```

### Trasformare un set di dati con DatasetTransformer {#transform-a-dataset-with-datasettransformer}

DatasetTransformer fornisce la logica per la trasformazione di un DataFrame di input e restituisce un nuovo DataFrame derivato. Questa classe può essere implementata per funzionare in modo cooperativo con FeaturePipelineFactory, per lavorare come unico componente di ingegneria delle feature oppure per non implementarla.

Nell&#39;esempio seguente viene estesa la classe DatasetTransformer:

**Esempio di PySpark**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer
from pyspark.ml.feature import StringIndexer
from pyspark.sql.types import IntegerType
from pyspark.sql.functions import unix_timestamp, from_unixtime, to_date, lit, lag, udf, date_format, lower, col, split, explode
from pyspark.sql import Window
from .helper import setupLogger

class MyDatasetTransformer(DatasetTransformer):
    logger = setupLogger(__name__)

    def transform(self, config_properties, dataset):
        tenant_id = str(config_properties.get("tenantId"))

        # Flatten the data
        if tenant_id in dataset.columns:
            self.logger.info("Flatten the data before transformation")
            dataset = dataset.select(col(tenant_id + ".*"))
            dataset.show()

        # Convert isHoliday boolean value to Int
        # Rename the column to holiday and drop isHoliday
        pd = dataset.withColumn("holiday", col("isHoliday").cast(IntegerType())).drop("isHoliday")
        pd.show()

        # Get the week and year from date
        pd = pd.withColumn("week", date_format(to_date("date", "MM/dd/yy"), "w").cast(IntegerType()))
        pd = pd.withColumn("year", date_format(to_date("date", "MM/dd/yy"), "Y").cast(IntegerType()))

        # Convert the date to TimestampType
        pd = pd.withColumn("date", to_date(unix_timestamp(pd["date"], "MM/dd/yy").cast("timestamp")))

        # Convert categorical data
        indexer = StringIndexer(inputCol="storeType", outputCol="storeTypeIndex")
        pd = indexer.fit(pd).transform(pd)

        # Get the WeeklySalesAhead and WeeklySalesLag column values
        window = Window.orderBy("date").partitionBy("store")
        pd = pd.withColumn("weeklySalesLag", lag("weeklySales", 1).over(window)).na.drop(subset=["weeklySalesLag"])
        pd = pd.withColumn("weeklySalesAhead", lag("weeklySales", -1).over(window)).na.drop(subset=["weeklySalesAhead"])
        pd = pd.withColumn("weeklySalesScaled", lag("weeklySalesAhead", -1).over(window)).na.drop(subset=["weeklySalesScaled"])
        pd = pd.withColumn("weeklySalesDiff", (pd['weeklySales'] - pd['weeklySalesLag'])/pd['weeklySalesLag'])

        pd = pd.na.drop()
        self.logger.debug("Transformed dataset count is %s " % pd.count())

        # return transformed dataframe
        return pd
```

### Funzioni dati del tecnico con FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

FeaturePipelineFactory consente di implementare la logica di ingegneria delle feature definendo e concatenando una serie di trasformatori Spark attraverso una pipeline Spark. Questa classe può essere implementata per lavorare in modo cooperativo con un DatasetTransformer, lavorare come unico componente di ingegneria delle caratteristiche oppure è possibile scegliere di non implementare questa classe.

L&#39;esempio che segue estende la classe FeaturePipelineFactory:

**Esempio di PySpark**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.regression import GBTRegressor
from pyspark.ml.feature import VectorAssembler

import numpy as np

from sdk.pipeline_factory import PipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def apply(self, config_properties):
        if config_properties is None:
            raise ValueError("config_properties parameter is null")

        tenant_id = str(config_properties.get("tenantId"))
        input_features = str(config_properties.get("ACP_DSW_INPUT_FEATURES"))

        if input_features is None:
            raise ValueError("input_features parameter is null")
        if input_features.startswith(tenant_id):
            input_features = input_features.replace(tenant_id + ".", "")

        learning_rate = float(config_properties.get("learning_rate"))
        n_estimators = int(config_properties.get("n_estimators"))
        max_depth = int(config_properties.get("max_depth"))

        feature_list = list(input_features.split(","))
        feature_list.remove("date")
        feature_list.remove("storeType")

        cols = np.array(feature_list)

        # Gradient-boosted tree estimator
        gbt = GBTRegressor(featuresCol='features', labelCol='weeklySalesAhead', predictionCol='prediction',
                       maxDepth=max_depth, maxBins=n_estimators, stepSize=learning_rate)

        # Assemble the fields to a vector
        assembler = VectorAssembler(inputCols=cols, outputCol="features")

        # Construct the pipeline
        pipeline = Pipeline(stages=[assembler, gbt])

        return pipeline

    def train(self, config_properties, dataframe):
        pass

    def score(self, config_properties, dataframe, model):
        pass

    def getParamMap(self, config_properties, sparkSession):
        return None
```

### Memorizzare il set di dati della funzione con DataSaver {#store-your-feature-dataset-with-datasaver}

DataSaver è responsabile dell&#39;archiviazione dei set di dati delle funzionalità risultanti in una posizione di archiviazione. L&#39;implementazione di DataSaver deve estendere la classe astratta `DataSaver` e sovrascrivi il metodo astratto `save`.

Nell&#39;esempio seguente viene estesa la classe DataSaver che memorizza i dati in una [!DNL Platform] set di dati per ID, dove l’ID del set di dati (`featureDatasetId`) e ID tenant (`tenantId`) sono proprietà definite nella configurazione.

**Esempio di PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct


class MyDataSaver(DataSaver):
    def save(self, configProperties, data_feature):

        # Spark context
        sparkContext = data_features._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if data_features is None:
            raise ValueError("data_features parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("featureDatasetId"))
        tenant_id = str(
            configProperties.get("tenantId"))
        service_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['output_dataset_id', 'tenant_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # create and prepare DataFrame with valid columns
        output_df = data_features.withColumn("date", col("date").cast(StringType()))
        output_df = output_df.withColumn(tenant_id, struct(col("date"), col("store"), col("features")))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        # store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp") \
            .write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```


### Specificare i nomi di classe implementati nel file dell&#39;applicazione {#specify-your-implemented-class-names-in-the-application-file}

Una volta definite e implementate le classi della pipeline delle funzionalità, è necessario specificare i nomi delle classi nel file YAML dell&#39;applicazione.

Negli esempi seguenti vengono specificati i nomi di classe implementati:

**Esempio di PySpark**

```yaml
#Name of the class which contains implementation to get the input data.
feature.dataLoader: InputDataLoaderForFeaturePipeline

#Name of the class which contains implementation to get the transformed data.
feature.dataset.transformer: MyDatasetTransformer

#Name of the class which contains implementation to save the transformed data.
feature.dataSaver: DatasetSaverForTransformedData

#Name of the class which contains implementation to get the training data
training.dataLoader: TrainingDataLoader

#Name of the class which contains pipeline. It should implement PipelineFactory.scala
pipeline.class: TrainPipeline

#Name of the class which contains implementation for evaluation metrics.
evaluator: Evaluator
evaluateModel: True

#Name of the class which contains implementation to get the scoring data.
scoring.dataLoader: ScoringDataLoader

#Name of the class which contains implementation to save the scoring data.
scoring.dataSaver: MyDatasetSaver
```

## Creare il motore della pipeline delle funzioni utilizzando l’API {#create-feature-pipeline-engine-api}

Dopo aver creato la pipeline delle funzioni, è necessario creare un’immagine Docker per effettuare una chiamata agli endpoint della pipeline delle funzioni nella [!DNL Sensei Machine Learning] API. Per effettuare una chiamata agli endpoint della pipeline della funzione è necessario un URL dell’immagine Docker.

>[!TIP]
>
>Se non disponi di un URL Docker, visita il [Creare pacchetti di file di origine in una ricetta](../models-recipes/package-source-files-recipe.md) tutorial per una procedura dettagliata sulla creazione di un URL host Docker.

Facoltativamente, puoi anche utilizzare la seguente raccolta Postman per facilitare il completamento del flusso di lavoro API della pipeline delle funzioni:

https://www.postman.com/collections/c5fc0d1d5805a5ddd41a

### Creare un motore di feature pipeline {#create-engine-api}

Una volta individuata la posizione dell’immagine Docker, puoi [creare un motore di feature pipeline](../api/engines.md#feature-pipeline-docker) utilizzando [!DNL Sensei Machine Learning] tramite l’esecuzione di un POST per `/engines`. La creazione corretta di un motore di feature pipeline ti fornisce un identificatore univoco del motore (`id`). Prima di continuare, assicurati di salvare questo valore.

### Creare un&#39;istanza MLI {#create-mlinstance}

Utilizzo del nuovo `engineID`, è necessario [creare un MLIstance](../api/mlinstances.md#create-an-mlinstance) effettuando una richiesta POST al `/mlInstance` endpoint. In caso di esito positivo, la risposta restituisce un payload contenente i dettagli della nuova istanza MLInstance creata, incluso il relativo identificatore univoco (`id`) utilizzato nella chiamata API successiva.

### Creare un esperimento {#create-experiment}

Quindi, devi [creare un esperimento](../api/experiments.md#create-an-experiment). Per creare un esperimento è necessario disporre dell’identificatore univoco MLIstance (`id`) e invia una richiesta POST al `/experiment` endpoint. In caso di esito positivo, la risposta restituisce un payload contenente i dettagli dell’esperimento appena creato, compreso il relativo identificatore univoco (`id`) utilizzato nella chiamata API successiva.

### Specificare l&#39;attività Esperimento esecuzione feature pipeline {#specify-feature-pipeline-task}

Dopo aver creato un esperimento, devi modificarne la modalità in `featurePipeline`. Per cambiare la modalità, aggiungi un POST aggiuntivo a [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) con il `EXPERIMENT_ID` e nel corpo inviano `{ "mode":"featurePipeline"}` per specificare un&#39;esecuzione dell&#39;esperimento della tubazione di feature.

Una volta completato, invia una richiesta GET a `/experiments/{EXPERIMENT_ID}` a [recuperare lo stato dell’esperimento](../api/experiments.md#retrieve-specific) e attendi il completamento dell’aggiornamento dello stato dell’esperimento.

### Specifica l’attività di apprendimento Esecuzione esperimento {#training}

Quindi, devi [specifica l’attività di esecuzione dell’addestramento](../api/experiments.md#experiment-training-scoring). Imposta come POST `experiments/{EXPERIMENT_ID}/runs` e nel corpo impostare la modalità su `train` e invia un array di attività che contengono i parametri di apprendimento. Una risposta corretta restituisce un payload contenente i dettagli dell’esperimento richiesto.

Una volta completato, invia una richiesta GET a `/experiments/{EXPERIMENT_ID}` a [recuperare lo stato dell’esperimento](../api/experiments.md#retrieve-specific) e attendi il completamento dell’aggiornamento dello stato dell’esperimento.

### Specificare l&#39;attività Esperimento esecuzione punteggio {#scoring}

>[!NOTE]
>
> Per completare questo passaggio, devi avere almeno un’esecuzione di formazione di successo associata al tuo esperimento.

Dopo un’esecuzione di apprendimento corretta, è necessario: [specificare l&#39;attività di esecuzione del punteggio](../api/experiments.md#experiment-training-scoring). Imposta come POST `experiments/{EXPERIMENT_ID}/runs` e nel corpo imposta il `mode` attribuire a &quot;score&quot;. Viene avviata l’esecuzione dell’esperimento di punteggio.

Una volta completato, invia una richiesta GET a `/experiments/{EXPERIMENT_ID}` a [recuperare lo stato dell’esperimento](../api/experiments.md#retrieve-specific) e attendi il completamento dell’aggiornamento dello stato dell’esperimento.

Una volta completato il punteggio, la pipeline delle funzioni dovrebbe essere operativa.

## Passaggi successivi {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

Una volta letto questo documento, hai creato una pipeline di funzioni utilizzando l’SDK di authoring del modello, creato un’immagine Docker e utilizzato l’URL dell’immagine Docker per creare un modello di pipeline di funzioni utilizzando [!DNL Sensei Machine Learning] API. Ora puoi continuare a trasformare i set di dati ed estrarre le funzioni di dati su larga scala utilizzando [[!DNL Sensei Machine Learning API]](../api/getting-started.md).
