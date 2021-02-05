---
keywords: ' Experience Platform;guida per gli sviluppatori;SDK;creazione di modelli;Area di lavoro di analisi dati;argomenti comuni;test'
solution: Experience Platform
title: Model Authoring SDK
topic: Overview
description: L’SDK per l’authoring dei modelli consente di sviluppare ricette di apprendimento automatico personalizzate e pipeline di funzionalità utilizzabili in Adobe Experience Platform Data Science Workspace, fornendo modelli implementabili in PySpark e Spark (Scala).
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 1%

---


# Model Authoring SDK

L’SDK per l’authoring dei modelli consente di sviluppare ricette di apprendimento automatico personalizzate e pipeline delle funzioni che possono essere utilizzate in [!DNL Adobe Experience Platform] Data Science Workspace, fornendo modelli implementabili in [!DNL PySpark] e [!DNL Spark (Scala)].

Questo documento fornisce informazioni sulle varie classi rilevate nell’SDK per l’authoring dei modelli.

## DataLoader {#dataloader}

La classe DataLoader racchiude qualsiasi elemento correlato al recupero, al filtraggio e alla restituzione di dati di input non elaborati. Esempi di dati di input includono quelli per la formazione, il punteggio o la progettazione di funzionalità. I caricatori di dati estendono la classe astratta `DataLoader` e devono sostituire il metodo astratto `load`.

**PySpark**

Nella tabella seguente sono descritti i metodi astratti di una classe PySpark Data Loader:

<table>
    <thead>
        <tr>
            <th>Metodo e descrizione</th>
            <th>Parametri</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(self, configProperties, spark)</code></p>
                <p>Carica e restituisce i dati della piattaforma come dati Pandas DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Riferimento autonomo</li>
                    <li><code>configProperties</code>: Mappa delle proprietà di configurazione</li>
                    <li><code>spark</code>: Spark session</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

Nella tabella seguente sono descritti i metodi astratti di una classe [!DNL Spark] Data Loader:

<table>
    <thead>
        <tr>
            <th>Metodo e descrizione</th>
            <th>Parametri</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(configProperties, sparkSession)</code></p>
                <p>Carica e restituisce i dati della piattaforma come DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Mappa delle proprietà di configurazione</li>
                    <li><code>sparkSession</code>: Spark session</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Carica dati da un set di dati [!DNL Platform] {#load-data-from-a-platform-dataset}

L&#39;esempio seguente recupera i dati [!DNL Platform] per ID e restituisce un DataFrame, dove l&#39;ID dataset (`datasetId`) è una proprietà definita nel file di configurazione.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load_dataset(config_properties, spark, task_id):

        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
        PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

        # prepare variables
        service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        dataset_id = str(config_properties.get(task_id))

        # validate variables
        for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session

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

        # return as DataFrame
        return pd
```

**Spark (Scala)**

```scala
// Spark

package com.adobe.platform.ml

import java.time.LocalDateTime

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.ml.feature.StringIndexer
import org.apache.spark.sql.expressions.Window
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.{StructType, TimestampType}
import org.apache.spark.sql.{DataFrame, SparkSession}
import org.apache.spark.sql.Column

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
    final val PLATFORM_SDK_PQS_INTERACTIVE: String = "interactive"
    final val PLATFORM_SDK_PQS_BATCH: String = "batch"

    /**
    *
    * @param configProperties - Configuration Properties map
    * @param sparkSession     - SparkSession
    * @return                 - DataFrame which is loaded for training
    */


  def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {

    require(configProperties != null)
    require(sparkSession != null)

    // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

    val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, PLATFORM_SDK_PQS_INTERACTIVE)
      .option(QSOption.datasetId, dataSetId)
      .load()
    df.show()
    df
    }
}
```

## DataSaver {#datasaver}

La classe DataSaver racchiude qualsiasi elemento correlato alla memorizzazione dei dati di output, inclusi quelli derivanti dal punteggio o dalla progettazione di funzionalità. I salvatori di dati estendono la classe astratta `DataSaver` e devono sostituire il metodo astratto `save`.

**PySpark**

Nella tabella seguente sono descritti i metodi astratti di una classe [!DNL PySpark] Data Saver:

<table>
    <thead>
        <tr>
            <th>Metodo e descrizione</th>
            <th>Parametri</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(self, configProperties, dataframe)</code></p>
                <p>Ricevi i dati di output come DataFrame e li memorizza in un dataset della piattaforma</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Riferimento autonomo</li>
                    <li><code>configProperties</code>: Mappa delle proprietà di configurazione</li>
                    <li><code>dataframe</code>: Dati da memorizzare sotto forma di DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Nella tabella seguente sono descritti i metodi astratti di una classe [!DNL Spark] Data Saver:

<table>
    <thead>
        <tr>
            <th>Metodo e descrizione</th>
            <th>Parametri</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(configProperties, dataFrame)</code></p>
                <p>Ricevi i dati di output come DataFrame e li memorizza in un dataset della piattaforma</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Mappa delle proprietà di configurazione</li>
                    <li><code>dataFrame</code>: Dati da memorizzare sotto forma di DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Salva i dati in un set di dati [!DNL Platform] {#save-data-to-a-platform-dataset}

Per memorizzare i dati in un dataset [!DNL Platform], le proprietà devono essere fornite o definite nel file di configurazione:

- Un ID di set di dati [!DNL Platform] valido a cui memorizzare i dati
- L&#39;ID tenant appartenente alla tua organizzazione

Gli esempi seguenti memorizzano i dati (`prediction`) in un dataset [!DNL Platform], dove l&#39;ID dataset (`datasetId`) e l&#39;ID tenant (`tenantId`) sono proprietà definite all&#39;interno del file di configurazione.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
from .helper import *


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, config_properties, prediction):

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if config_properties is None:
            raise ValueError("config_properties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")
        
        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"

        # prepare variables
        scored_dataset_id = str(config_properties.get("scoringResultsDataSetId"))
        tenant_id = str(config_properties.get("tenant_id"))
        timestamp = "2019-01-01 00:00:00"

        service_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
       for arg in ['service_token', 'user_token', 'org_id', 'scored_dataset_id', 'api_key', 'tenant_id']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)
        
        scored_df = prediction.withColumn("date", col("date").cast(StringType()))
        scored_df = scored_df.withColumn(tenant_id, struct(col("date"), col("store"), col("prediction")))
        scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        scored_df = scored_df.withColumn("_id", lit("empty"))
        scored_df = scored_df.withColumn("eventType", lit("empty")

        # store data into dataset

        query_options = get_query_options(sparkContext)

        scored_df.select(tenant_id, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE) \
            .option(query_options.userToken(), user_token) \
            .option(query_options.serviceToken(), service_token) \
            .option(query_options.imsOrg(), org_id) \
            .option(query_options.apiKey(), api_key) \
            .option(query_options.datasetId(), scored_dataset_id) \
            .save()
```

**Spark (Scala)**

```scala
// Spark

package com.adobe.platform.ml

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */

class ScoringDataSaver extends DataSaver {

  final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
  final val PLATFORM_SDK_PQS_BATCH: String = "batch"

  /**
    * Method that saves the scoring data into a dataframe
    * @param configProperties  - Configuration Properties map
    * @param dataFrame         - Dataframe with the scoring results
    */
    
  override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

    require(configProperties != null)
    require(dataFrame != null)

    val predictionColumn = configProperties.get(Constants.PREDICTION_COL).getOrElse(Constants.DEFAULT_PREDICTION)
    val sparkSession = dataFrame.sparkSession

    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val tenantId:String = configProperties.get("tenantId").getOrElse("")
    val timestamp:String = "2019-01-01 00:00:00"

    val scoringResultsDataSetId: String = configProperties.get("scoringResultsDataSetId").getOrElse("")
    import sparkSession.implicits._

    var df = dataFrame.withColumn("date", $"date".cast("String"))

    var scored_df  = df.withColumn(tenantId, struct(df("date"), df("store"), df(predictionColumn)))
    scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
    scored_df = scored_df.withColumn("_id", lit("empty"))
    scored_df = scored_df.withColumn("eventType", lit("empty"))

    scored_df.select(tenantId, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .save()
    }
}
```

## DatasetTransformer {#datasettransformer}

La classe DatasetTransformer modifica e trasforma la struttura di un dataset. Il componente [!DNL Sensei Machine Learning Runtime] non richiede la definizione di questo componente ed è implementato in base ai requisiti dell&#39;utente.

Per quanto riguarda una tubazione di feature, i trasformatori di set di dati possono essere utilizzati in modo collaborativo con una fabbrica di tubazioni di feature per preparare i dati per la progettazione di feature.

**PySpark**

Nella tabella seguente sono descritti i metodi di classe di una classe di trasformatore di set di dati PySpark:

<table>
    <thead>
        <tr>
            <th>Metodo e descrizione</th>
            <th>Parametri</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>transform(self, configProperties, dataset)</code></p>
                <p>Assume un dataset come input e genera un nuovo dataset derivato</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Riferimento autonomo</li>
                    <li><code>configProperties</code>: Mappa delle proprietà di configurazione</li>
                    <li><code>dataset</code>: Il set di dati di input per la trasformazione</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Nella tabella seguente sono descritti i metodi astratti di una classe di trasformatore di set di dati [!DNL Spark]:

<table>
    <thead>
        <tr>
            <th>Metodo e descrizione</th>
            <th>Parametri</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>transform(configProperties, dataset)</code></p>
                <p>Assume un dataset come input e genera un nuovo dataset derivato</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Mappa delle proprietà di configurazione</li>
                    <li><code>dataset</code>: Il set di dati di input per la trasformazione</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

La classe FeaturePipelineFactory contiene algoritmi di estrazione delle feature e definisce le fasi di una feature Pipeline dall&#39;inizio alla fine.

**PySpark**

Nella tabella seguente sono descritti i metodi di classe di una FeaturePipelineFactory di PySpark:

<table>
    <thead>
        <tr>
            <th>Metodo e descrizione</th>
            <th>Parametri</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>create_pipeline(self, configProperties)</code></p>
                <p>Creare e restituire una pipeline Spark che contiene una serie di trasformatori Spark</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Riferimento autonomo</li>
                    <li><code>configProperties</code>: Mappa delle proprietà di configurazione</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Recuperare e restituire la mappa param dalle proprietà di configurazione</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Riferimento autonomo</li>
                    <li><code>configProperties</code>: Proprietà di configurazione</li>
                    <li><code>sparkSession</code>: Spark session</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Nella tabella seguente sono descritti i metodi di classe di una [!DNL Spark] FeaturePipelineFactory:

<table>
    <thead>
        <tr>
            <th>Metodo e descrizione</th>
            <th>Parametri</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>createPipeline(configProperties)</code></p>
                <p>Creare e restituire una tubazione contenente una serie di trasformatori</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Mappa delle proprietà di configurazione</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>Recuperare e restituire la mappa param dalle proprietà di configurazione</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Proprietà di configurazione</li>
                    <li><code>sparkSession</code>: Spark session</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

La classe PipelineFactory racchiude metodi e definizioni per la formazione e il punteggio dei modelli, in cui la logica e gli algoritmi di formazione sono definiti sotto forma di [!DNL Spark] Pipeline.

**PySpark**

Nella tabella seguente sono descritti i metodi di classe di una PipelineFactory di PySpark:

<table>
    <thead>
        <tr>
            <th>Metodo e descrizione</th>
            <th>Parametri</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>apply(self, configProperties)</code></p>
                <p>Creare e restituire una pipeline Spark che contiene la logica e l'algoritmo per la formazione e il punteggio dei modelli</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Riferimento autonomo</li>
                    <li><code>configProperties</code>: Proprietà di configurazione</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>train(self, configProperties, dataframe)</code></p>
                <p>Restituisce una pipeline personalizzata che contiene la logica e l'algoritmo per l'addestramento di un modello. Questo metodo non è richiesto se viene utilizzata una pipeline Spark</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Riferimento autonomo</li>
                    <li><code>configProperties</code>: Proprietà di configurazione</li>
                    <li><code>dataframe</code>: Set di dati delle funzioni per l'input di formazione</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>score(self, configProperties, dataframe, model)</code></p>
                <p>Punteggio utilizzando il modello preparato e restituire i risultati</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Riferimento autonomo</li>
                    <li><code>configProperties</code>: Proprietà di configurazione</li>
                    <li><code>dataframe</code>: Set di dati di input per il punteggio</li>
                    <li><code>model</code>: Un modello qualificato utilizzato per il punteggio</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Recuperare e restituire la mappa param dalle proprietà di configurazione</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Riferimento autonomo</li>
                    <li><code>configProperties</code>: Proprietà di configurazione</li>
                    <li><code>sparkSession</code>: Spark session</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Nella tabella seguente sono descritti i metodi di classe di una [!DNL Spark] PipelineFactory:

<table>
    <thead>
        <tr>
            <th>Metodo e descrizione</th>
            <th>Parametri</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>apply(configProperties)</code></p>
                <p>Creare e restituire una pipeline che contiene la logica e l'algoritmo per la formazione e il punteggio dei modelli</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Proprietà di configurazione</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>Recuperare e restituire la mappa param dalle proprietà di configurazione</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Proprietà di configurazione</li>
                    <li><code>sparkSession</code>: Spark session</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEperatore {#mlevaluator}

La classe MLEvalue fornisce metodi per definire le metriche di valutazione e determinare i set di dati di formazione e test.

**PySpark**

Nella tabella seguente sono descritti i metodi di classe di un oggetto PySpark MLEvalue:

<table>
    <thead>
        <tr>
            <th>Metodo e descrizione</th>
            <th>Parametri</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>split(self, configProperties, dataframe)</code></p>
                <p>Suddivide il set di dati di input in sottoinsiemi di formazione e test</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Riferimento autonomo</li>
                    <li><code>configProperties</code>: Proprietà di configurazione</li>
                    <li><code>dataframe</code>: Set di dati di input da dividere</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Valuta un modello preparato e restituisce i risultati della valutazione</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Riferimento autonomo</li>
                    <li><code>dataframe</code>: Un DataFrame costituito da dati di formazione e test</li>
                    <li><code>model</code>: Un modello preparato</li>
                    <li><code>configProperties</code>: Proprietà di configurazione</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Nella tabella seguente sono descritti i metodi di classe di un [!DNL Spark] MLEvalue:

<table>
    <thead>
        <tr>
            <th>Metodo e descrizione</th>
            <th>Parametri</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>split(configProperties, data)</code></p>
                <p>Suddivide il set di dati di input in sottoinsiemi di formazione e test</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Proprietà di configurazione</li>
                    <li><code>data</code>: Set di dati di input da dividere</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>evaluate(configProperties, model, data)</code></p>
                <p>Valuta un modello preparato e restituisce i risultati della valutazione</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Proprietà di configurazione</li>
                    <li><code>model</code>: Un modello preparato</li>
                    <li><code>data</code>: Un DataFrame costituito da dati di formazione e test</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>