---
keywords: Experience Platform;home;argomenti popolari;accesso ai dati;sdk di spark;api di accesso ai dati;ricetta di spark;spark di lettura;spark di scrittura
solution: Experience Platform
title: Accesso ai dati con Spark in Data Science Workspace
type: Tutorial
description: Il seguente documento contiene esempi su come accedere ai dati utilizzando Spark per l’utilizzo in Data Science Workspace.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Accesso ai dati con Spark in Data Science Workspace

Il seguente documento contiene esempi su come accedere ai dati utilizzando Spark per l’utilizzo in Data Science Workspace. Per informazioni sull’accesso ai dati tramite i notebook JupyterLab, visita il [Accesso ai dati dei notebook JupyterLab](../jupyterlab/access-notebook-data.md) documentazione.

## Introduzione

Utilizzo di [!DNL Spark] richiede ottimizzazioni delle prestazioni che devono essere aggiunte al `SparkSession`. Inoltre, puoi anche impostare `configProperties` per poter poi essere letti e scritti nei set di dati.

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

Durante l’utilizzo di Spark è possibile accedere a due modalità di lettura: interattiva e batch.

La modalità interattiva crea una connessione JDBC (Java Database Connectivity) a [!DNL Query Service] e ottiene risultati tramite un JDBC regolare `ResultSet` che viene tradotto automaticamente in una `DataFrame`. Questa modalità funziona in modo simile al [!DNL Spark] metodo `spark.read.jdbc()`. Questa modalità è destinata solo ai set di dati di piccole dimensioni. Se il set di dati supera i 5 milioni di righe, si consiglia di passare alla modalità batch.

La modalità batch utilizza [!DNL Query Service]comando COPY di per generare set di risultati Parquet in una posizione condivisa. Questi file di Parquet possono quindi essere ulteriormente elaborati.

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

Un esempio di utilizzo di `distinct()` di seguito:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### clausola WHERE

Il [!DNL Spark] SDK consente due metodi per filtrare: utilizzando un’espressione SQL o filtrando attraverso le condizioni.

Di seguito è riportato un esempio di utilizzo di queste funzioni di filtro:

#### Espressione SQL

```scala
df.where("age > 15")
```

#### Condizioni di filtro

```scala
df.where("age" > 15 || "name" = "Steve")
```

### clausola ORDER BY

La clausola ORDER BY consente di ordinare i risultati ricevuti in base a una colonna specificata in un ordine specifico (crescente o decrescente). In [!DNL Spark] SDK, questo viene effettuato utilizzando `sort()` funzione.

Un esempio di utilizzo di `sort()` di seguito:

```scala
df = df.sort($"column1", $"column2".desc)
```

### clausola LIMIT

La clausola LIMIT consente di limitare il numero di record ricevuti dal set di dati.

Un esempio di utilizzo di `limit()` di seguito:

```scala
df = df.limit(100)
```

## Scrittura in un set di dati

Utilizzo di `configProperties` mappatura, puoi scrivere su un set di dati in Experience Platform utilizzando `QSOption`.

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

Adobe Experience Platform Data Science Workspace fornisce un esempio di ricetta Scala (Spark) che utilizza gli esempi di codice precedenti per leggere e scrivere dati. Per ulteriori informazioni su come utilizzare Spark per accedere ai dati, consulta la sezione [Archivio GitHub Scala di Data Science Workspace](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
