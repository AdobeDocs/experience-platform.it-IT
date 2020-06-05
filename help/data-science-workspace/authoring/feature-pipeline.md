---
keywords: Experience Platform;Tutorial;Feature Pipeline;Data Science Workspace;popular topics
solution: Experience Platform
title: Creare una tubazione di feature
topic: Tutorial
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# Creare una tubazione di feature

[!DNL Adobe Experience Platform] consente di creare e creare tubazioni di feature personalizzate per eseguire la progettazione di feature in scala tramite il runtime Sensei Machine Learning Framework (di seguito &quot;Runtime&quot;).

Questo documento descrive le varie classi rilevate in una pipeline delle feature e fornisce un&#39;esercitazione dettagliata per la creazione di una pipeline delle feature personalizzata mediante l&#39;SDK [per l&#39;authoring dei](./sdk.md) modelli in PySpark e Spark.

## Classi pipeline delle feature

Nella tabella seguente sono descritte le principali classi astratte che è necessario estendere per creare una pipeline delle feature:

| Classe astratta | Descrizione |
| -------------- | ----------- |
| DataLoader | Una classe DataLoader fornisce l&#39;implementazione per il recupero dei dati di input. |
| DatasetTransformer | Una classe DatasetTransformer fornisce implementazioni per trasformare il dataset di input. È possibile scegliere di non fornire una classe DatasetTransformer e implementare la logica di progettazione delle funzionalità all&#39;interno della classe FeaturePipelineFactory. |
| FeaturePipelineFactory | Una classe FeaturePipelineFactory crea una tubazione Spark costituita da una serie di trasformatori Spark per eseguire la progettazione di funzionalità. È possibile scegliere di non fornire una classe FeaturePipelineFactory e implementare la logica di progettazione delle funzionalità all&#39;interno della classe DatasetTransformer. |
| DataSaver | Una classe DataSaver fornisce la logica per l&#39;archiviazione di un set di dati di una funzione. |

Quando viene avviato un processo di pipeline delle feature, il Runtime eseguirà prima il DataLoader per caricare i dati di input come DataFrame, quindi modificherà il DataFrame eseguendo DatasetTransformer o FeaturePipelineFactory o entrambi. Infine, il set di dati della funzionalità risultante viene memorizzato tramite DataSaver.

Il seguente diagramma di flusso mostra l&#39;ordine di esecuzione del runtime:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Implementare le classi di Feature Pipeline {#implement-your-feature-pipeline-classes}

Le sezioni seguenti forniscono dettagli ed esempi sull&#39;implementazione delle classi necessarie per una tubazione di feature.

### Definire le variabili nel file JSON di configurazione {#define-variables-in-the-configuration-json-file}

Il file JSON di configurazione è costituito da coppie chiave-valore ed è destinato all&#39;utente a specificare eventuali variabili da definire successivamente durante il runtime. Queste coppie chiave-valore possono definire proprietà quali la posizione del set di dati di input, l&#39;ID del set di dati di output, l&#39;ID tenant, le intestazioni di colonna e così via.

L&#39;esempio seguente illustra le coppie chiave-valore rilevate all&#39;interno di un file di configurazione. Espandete l’esempio per visualizzare i dettagli:


**esempio JSON di configurazione**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "datasetId",
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



Potete accedere alla configurazione JSON tramite qualsiasi metodo di classe definito `configProperties` come parametro. Ad esempio:

**PySpark**

```python
input_dataset_id = str(configProperties.get("datasetId"))
```

**Spark**

```scala
val input_dataset_id: String = configProperties.get("datasetId")
```


### Preparare i dati di input con DataLoader {#prepare-the-input-data-with-dataloader}

DataLoader è responsabile del recupero e del filtraggio dei dati di input. L&#39;implementazione di DataLoader deve estendere la classe astratta `DataLoader` e ignorare il metodo abstract `load`.

L&#39;esempio seguente recupera un set di dati della piattaforma per ID e lo restituisce come DataFrame, dove l&#39;ID del set di dati (`datasetId`) è una proprietà definita nel file di configurazione. Espandete ciascun esempio per visualizzare i dettagli:


**Esempio di PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    def load(self, configProperties, spark):

        # preliminary checks
        if configProperties is None :
            raise ValueError("configProperties parameter is null")
        if spark is None:
            raise ValueError("spark parameter is null")

        # prepare variables
        dataset_id = str(
            configProperties.get("datasetId"))
        service_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['dataset_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session
        df = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return df
```




**Spark, esempio**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

class MyDataLoader extends DataLoader {
    override def load(configProperties: ConfigProperties, sparkSession: SparkSession): DataFrame = {

        // preliminary checks
        require(configProperties != null)
        require(sparkSession != null)

        // prepare variables
        val dataSetId: String = configProperties
            .get("datasetId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(dataSetId, serviceToken, userToken, orgId, apiKey).foreach(
            value => required(value != "")
        )

        // load dataset through Spark session
        var df = sparkSession.read.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .load(dataSetId)
        
        // return as DataFrame
        df
    }
}
```



### Trasforma un set di dati con DatasetTransformer {#transform-a-dataset-with-datasettransformer}

Un oggetto DatasetTransformer fornisce la logica necessaria per trasformare un DataFrame di input e restituisce un nuovo DataFrame derivato. Questa classe può essere implementata in modo collaborativo con FeaturePipelineFactory, può essere utilizzata come unico componente di ingegneria delle funzioni, oppure è possibile scegliere di non implementare questa classe.

L&#39;esempio seguente estende la classe DatasetTransformer. Espandete ciascun esempio per visualizzare i dettagli:


**Esempio di PySpark**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer

class MyDatasetTransformer(DatasetTransformer):

    def transform(self, configProperties, dataset):
        transformed = dataset

        '''
        Transformations
        '''

        # return new DataFrame
        return transformed
```




**Spark, esempio**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DatasetTransformer

class MyDatasetTransformer extends DatasetTransformer {

    override def transform(configProperties: ConfigProperties, dataset: Dataset[_]): Dataset[_] = {
        val transformed = dataset

        /*
        transformations
        */
        
        // return new DataFrame
        transformed
    }
}
```



### Caratteristiche tecniche dei dati con FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

FeaturePipelineFactory consente di implementare la logica di progettazione delle funzionalità definendo e concatenando una serie di trasformatori Spark attraverso una tubazione Spark. Questa classe può essere implementata per lavorare in collaborazione con un DataSetTransformer, come unico componente di ingegneria delle funzionalità, oppure è possibile scegliere di non implementare questa classe.

L&#39;esempio seguente estende la classe FeaturePipelieFactory e implementa una serie di trasformatori Spark come più fasi in una tubazione Spark. Espandete ciascun esempio per visualizzare i dettagli:


**Esempio di PySpark**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.feature import HashingTF, Tokenizer
from sdk.feature_pipeline_factory import FeaturePipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def create_pipeline(self, configProperties):

        # Spark Transformers
        tokenizer = Tokenizer(inputCol="lower_text", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")

        # Chain together Spark Transformers as Spark Pipeline Stages
        pipeline = Pipeline(stages=[tokenizer, hashingTF])

        # return a Spark Pipeline
        return pipeline

    def get_param_map(self, configProperties, sparkSession):
        pass
```




**Spark, esempio**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.FeaturePipelineFactory
import org.apache.spark.ml.feature.{HashingTF, Tokenizer}
import org.apache.spark.ml.Pipeline
import org.apache.spark.ml.param.ParamMap
import org.apache.spark.sql.SparkSession

class MyFeaturePipelineFactory(uid:String) extends FeaturePipelineFactory(uid) {
    def this() = this("MyFeaturePipeline")

    override def createPipeline(configProperties: ConfigProperties): Pipeline = {
        
        // Spark Transformers
        val tokenizer = new Tokenizer()
            .setInputCol("lower_text")
            .setOutputCol("words")
        val hashingTF = new HashingTF()
            .setInputCol(tokenizer.getOutputCol())
            .setOutputCol("features")

        // Chain together Spark Transformers as Spark Pipeline Stages
        val pipeline = new Pipeline()
            .setStages(Array(tokenizer, hashingTF))
        
        // return a Spark Pipeline
        pipeline
    }

    override def getParamMap(configProperties: ConfigProperties, sparkSession: SparkSession): ParamMap = {
        val map = new ParamMap()
        map
    }
}
```



### Memorizzazione del set di dati della funzionalità con DataSaver {#store-your-feature-dataset-with-datasaver}

DataSaver è responsabile della memorizzazione dei set di dati delle funzionalità risultanti in una posizione di archiviazione. L&#39;implementazione di DataSaver deve estendere la classe astratta `DataSaver` e ignorare il metodo abstract `save`.

L&#39;esempio seguente estende la classe DataSaver che memorizza i dati in un dataset della piattaforma per ID, dove l&#39;ID del set di dati (`featureDatasetId`) e l&#39;ID tenant (`tenantId`) sono proprietà definite nel file di configurazione. Espandete ciascun esempio per visualizzare i dettagli:


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




**Spark, esempio**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

class MyDataSaver extends DataSaver {
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("featureDatasetId").getOrElse("")
        val tenant_id:String = configProperties
            .get("tenantId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(output_dataset_id, tenant_id, serviceToken, userToken, orgId, apiKey).foreach(
            value => require(value != "")
        )

        // create and prepare DataFrame with valid columns
        import sparkSession.implicits._

        var output_df  = dataFrame.withColumn("date", $"date".cast("String"))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        // store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp").write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

### Specificare i nomi delle classi implementate nel file dell&#39;applicazione {#specify-your-implemented-class-names-in-the-application-file}

Una volta definite e implementate le classi di Feature Pipeline, è necessario specificare i nomi delle classi nel file dell&#39;applicazione.

Gli esempi seguenti specificano i nomi di classe implementati. Espandete l’esempio per visualizzare i dettagli:


**Esempio di PySpark**

```yaml
# application.yaml

# Name of the implementation of DataLoader abstract class
feature.dataLoader: MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer: MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.pipeline.class: MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver: MyDataSaver
```




**Spark, esempio**

```properties
# application.properties

# Name of the implementation of DataLoader abstract class
feature.pipeline.class=MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer=MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.dataLoader=MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver=MyDataSaver
```



## Creare l&#39;artefatto binario {#build-the-binary-artifact}

Ora che le classi di Feature Pipeline sono state implementate, potete generarle e compilarle in un artefatto binario che potrà essere utilizzato per creare una Feature Pipeline tramite chiamate API.

**PySpark**

Per creare una pipeline delle feature PySpark, eseguite lo script `setup.py` Python presente nella directory principale dell’SDK per l’authoring dei modelli.

>[!NOTE] La creazione di una tubazione di feature PySpark richiede l&#39;installazione di Python 3 nel computer.

```shell
python3 setup.py bdist_egg
```

La creazione corretta della feature Pipeline genera un `.egg` artefatto nella `/dist` directory, che viene utilizzato per creare una feature Pipeline.

**Spark**

Per creare una pipeline delle feature di Spark, eseguite il seguente comando della console nella directory principale dell’SDK per l’authoring dei modelli:

>[!NOTE] La creazione di una pipeline delle feature di Spark richiede l&#39;installazione di Scala e sbt nel computer.

```shell
mvn clean install
```

La creazione corretta della feature Pipeline genera un `.jar` artefatto nella `/dist` directory. Questo artefatto viene utilizzato per creare una feature Pipeline.

## Creazione di un motore di pipeline delle funzioni tramite l&#39;API {#create-a-feature-pipeline-engine-using-the-api}

Dopo aver creato la pipeline delle feature e aver creato l&#39;artefatto binario, è possibile [creare un motore di tubazione delle feature utilizzando l&#39;API](../api/engines.md#create-a-feature-pipeline-engine-using-binary-artifacts)Sensei Machine Learning. La creazione corretta di un motore di tubazione delle feature fornisce un ID motore come parte del corpo della risposta. Accertatevi di salvare questo valore prima di continuare con i passaggi successivi.

## Passaggi successivi {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the Feature Pipeline Engine. Update this document once those tutorials are available)

Leggendo questo documento, hai creato una pipeline di feature utilizzando l’SDK per l’authoring dei modelli, creato un artefatto binario e utilizzato l’artefatto per creare un motore di pipeline delle feature tramite una chiamata API. È ora possibile [creare un modello](../api/mlinstances.md#create-an-mlinstance) di pipeline delle feature utilizzando il motore appena creato e iniziare a trasformare i set di dati ed estrarre le feature di dati su scala.