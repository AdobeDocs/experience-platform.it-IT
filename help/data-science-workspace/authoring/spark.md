---
keywords: Experience Platform; casa; argomenti popolari; accesso dei dati; SDK Spark; API accesso dati; ricetta scintilla; leggere scintilla; Scrivi Spark
solution: Experience Platform
title: Accesso ai dati tramite Spark in Data Science Area di lavoro
type: Tutorial
description: Il documento seguente contiene esempi su come accesso dati usando Spark per l'utilizzo in Data Science Area di lavoro.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Accesso ai dati tramite Spark in Data Science Area di lavoro

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto.
>
>Questa documentazione è destinata ai clienti esistenti che dispongono di diritti precedenti su Data Science Workspace.

Il seguente documento contiene esempi su come accedere ai dati utilizzando Spark per l’utilizzo in Data Science Workspace. Per informazioni sull&#39;accesso ai dati tramite i notebook JupyterLab, consulta la documentazione sull&#39;[accesso ai dati dei notebook JupyterLab](../jupyterlab/access-notebook-data.md).

## Guida introduttuva

L&#39;utilizzo di [!DNL Spark] richiede ottimizzazioni delle prestazioni che devono essere aggiunte a `SparkSession`. Inoltre, è possibile configurare `configProperties` per una fase successiva in modo che possa essere letto e scritto nei set di dati.

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

## Lettura di un set di dati

Durante l&#39;utilizzo di Spark hai accesso a due modalità di lettura: interattiva e batch.

La modalità interattiva crea una connessione [!DNL Query Service] JDBC (Java Database Connectivity) e ottiene risultati tramite un normale JDBC `ResultSet` che viene automaticamente convertito in un `DataFrame`file . Questa modalità funziona in modo simile al metodo `spark.read.jdbc()`incorporato[!DNL Spark]. Questa modalità è destinata solo a set di dati di piccole dimensioni. Se il set di dati supera i 5 milioni di righe, si consiglia di passare alla modalità batch.

La modalità batch utilizza il comando COPY di [!DNL Query Service] per generare set di risultati Parquet in una posizione condivisa. Questi file di Parquet possono quindi essere ulteriormente elaborati.

Di seguito è riportato un esempio di lettura di un set di dati in modalità interattiva:

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

Analogamente, di seguito è riportato un esempio di lettura di un set di dati in modalità batch:

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

### SELEZIONA colonne dal set di dati

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

L&#39;SDK [!DNL Spark] consente due metodi per filtrare: utilizzando un&#39;espressione SQL o filtrando le condizioni.

Di seguito è riportato un esempio dell&#39;utilizzo di queste funzioni di filtro:

#### Espressione SQL

```scala
df.where("age > 15")
```

#### Condizioni di filtro

```scala
df.where("age" > 15 || "name" = "Steve")
```

### clausola ORDER BY

La clausola ORDER BY consente di ordinare i risultati ricevuti in base a una colonna specificata in un ordine specifico (crescente o decrescente). Nell&#39;SDK [!DNL Spark], questo avviene utilizzando la funzione `sort()`.

Di seguito è riportato un esempio di utilizzo della funzione `sort()`:

```scala
df = df.sort($"column1", $"column2".desc)
```

### clausola LIMIT

La clausola LIMIT consente di limitare il numero di record ricevuti dal set di dati.

Di seguito è riportato un esempio di utilizzo della funzione `limit()`:

```scala
df = df.limit(100)
```

## Scrittura su un dataset

Utilizzando la `configProperties` mappatura, è possibile scrivere in un dataset in Experience Platform utilizzando `QSOption`.

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

Adobe Experience Platform Data Science Workspace fornisce un esempio di ricetta Scala (Spark) che utilizza gli esempi di codice precedenti per leggere e scrivere dati. Per ulteriori informazioni su come utilizzare Spark per accedere ai dati, consulta la [Archivio GitHub Scala di Data Science Workspace](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
