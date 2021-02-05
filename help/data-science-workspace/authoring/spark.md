---
keywords: ' Experience Platform;casa;argomenti popolari;accesso ai dati;scintilla sdk;accesso ai dati api;ricetta scintilla;scintilla di lettura;scintilla di scrittura'
solution: Experience Platform
title: Accesso ai dati tramite Spark in Data Science Workspace
topic: tutorial
type: Tutorial
description: Il seguente documento contiene esempi su come accedere ai dati utilizzando Spark per l’utilizzo in Data Science Workspace.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Accesso ai dati tramite Spark in Data Science Workspace

Il seguente documento contiene esempi su come accedere ai dati utilizzando Spark per l’utilizzo in Data Science Workspace. Per informazioni sull&#39;accesso ai dati utilizzando i notebook JupyterLab, consultare la [documentazione relativa all&#39;accesso ai dati dei notebook JupyterLab](../jupyterlab/access-notebook-data.md).

## Introduzione

L&#39;utilizzo di [!DNL Spark] richiede ottimizzazioni delle prestazioni che devono essere aggiunte alla `SparkSession`. Inoltre, è possibile impostare `configProperties` in modo che sia possibile leggere e scrivere nei set di dati in un secondo momento.

```scala
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.{DataFrame, SparkSession}

Class Helper {

 /**
   *
   * @param configProperties - Configuration Properties map
   * @param sparkSession     - SparkSession
   * @return                 - DataFrame which is loaded for training
   */

   def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {
            // Read the configs
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## Lettura di un dataset

Con Spark è possibile accedere a due modalità di lettura: interattivo e batch.

La modalità interattiva crea una connessione JDBC (Java Database Connectivity) a [!DNL Query Service] e ottiene risultati tramite un JDBC `ResultSet` regolare che viene automaticamente convertito in un `DataFrame`. Questa modalità funziona in modo simile al metodo incorporato [!DNL Spark] `spark.read.jdbc()`. Questa modalità è valida solo per i set di dati di piccole dimensioni. Se il set di dati supera i 5 milioni di righe, si consiglia di passare alla modalità batch.

La modalità batch utilizza il comando COPY di [!DNL Query Service] per generare i set di risultati di Parquet in una posizione condivisa. Questi file Parquet possono essere elaborati ulteriormente.

Di seguito è riportato un esempio di lettura di un dataset in modalità interattiva:

```scala
  // Read the configs
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "interactive")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
  }
```

Analogamente, un esempio di lettura di un set di dati in modalità batch è riportato di seguito:

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### SELEZIONARE le colonne dal dataset

```scala
df = df.select("column-a", "column-b").show()
```

### Clausola DISTINCT

La clausola DISTINCT consente di recuperare tutti i valori distinti a livello di riga/colonna, rimuovendo tutti i valori duplicati dalla risposta.

Di seguito è riportato un esempio di utilizzo della funzione `distinct()`:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### Clausola WHERE

L&#39;SDK [!DNL Spark] consente due metodi per filtrare: Utilizzo di un&#39;espressione SQL o filtraggio attraverso le condizioni.

Di seguito è riportato un esempio di utilizzo di queste funzioni di filtro:

#### Espressione SQL

```scala
df.where("age > 15")
```

#### Condizioni di filtro

```scala
df.where("age" > 15 || "name" = "Steve")
```

### Clausola ORDER BY

La clausola ORDER BY consente di ordinare i risultati ricevuti in base a una colonna specificata in un ordine specifico (crescente o decrescente). Nell&#39;SDK [!DNL Spark], questo viene fatto utilizzando la funzione `sort()`.

Di seguito è riportato un esempio di utilizzo della funzione `sort()`:

```scala
df = df.sort($"column1", $"column2".desc)
```

### Clausola LIMIT

La clausola LIMIT consente di limitare il numero di record ricevuti dal set di dati.

Di seguito è riportato un esempio di utilizzo della funzione `limit()`:

```scala
df = df.limit(100)
```

## Scrittura in un dataset

Utilizzando la mappatura `configProperties`, è possibile scrivere in un dataset in  Experience Platform utilizzando `QSOption`.

```scala
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## Passaggi successivi

Adobe Experience Platform Data Science Workspace fornisce un esempio di ricetta Scala (Spark) che utilizza gli esempi di codice riportati sopra per leggere e scrivere i dati. Per ulteriori informazioni sull&#39;utilizzo di Spark per l&#39;accesso ai dati, consultare il [Data Science Workspace Scala GitHub Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).