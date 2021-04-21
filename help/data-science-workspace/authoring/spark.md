---
keywords: Experience Platform;home;argomenti popolari;accesso ai dati;scintilla sdk;api di accesso ai dati;ricetta di scintilla;scintilla di lettura;scintilla di scrittura
solution: Experience Platform
title: Accesso ai dati con Spark in Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Il seguente documento contiene esempi su come accedere ai dati utilizzando Spark per l’utilizzo in Data Science Workspace.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Accesso ai dati tramite Spark in Data Science Workspace

Il seguente documento contiene esempi su come accedere ai dati utilizzando Spark per l’utilizzo in Data Science Workspace. Per informazioni sull&#39;accesso ai dati tramite i notebook JupyterLab, visita la documentazione [JupyterLab data access](../jupyterlab/access-notebook-data.md) .

## Introduzione

L&#39;utilizzo di [!DNL Spark] richiede ottimizzazioni delle prestazioni che devono essere aggiunte a `SparkSession`. Inoltre, puoi impostare `configProperties` in modo che in seguito sia possibile leggere e scrivere nei set di dati.

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

Utilizzando Spark è possibile accedere a due modalità di lettura: interattivo e batch.

La modalità interattiva crea una connessione Java Database Connectivity (JDBC) a [!DNL Query Service] e ottiene risultati tramite un JDBC `ResultSet` regolare che viene convertito automaticamente in un `DataFrame`. Questa modalità funziona in modo simile al metodo incorporato [!DNL Spark] `spark.read.jdbc()`. Questa modalità è destinata solo ai set di dati di piccole dimensioni. Se il set di dati supera i 5 milioni di righe, è consigliabile passare alla modalità batch.

La modalità batch utilizza il comando COPY di [!DNL Query Service] per generare set di risultati Parquet in una posizione condivisa. Questi file Parquet possono quindi essere ulteriormente elaborati.

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

Analogamente, un esempio di lettura di un set di dati in modalità batch può essere visto di seguito:

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

### clausola DISTINCT

La clausola DISTINCT consente di recuperare tutti i valori distinti a livello di riga/colonna, rimuovendo tutti i valori duplicati dalla risposta.

Di seguito è riportato un esempio di utilizzo della funzione `distinct()` :

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### clausola WHERE

L&#39;SDK [!DNL Spark] consente due metodi di filtraggio: Utilizzo di un&#39;espressione SQL o filtrando tra le condizioni.

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

La clausola ORDER BY consente di ordinare i risultati ricevuti in base a una colonna specifica in un ordine specifico (crescente o decrescente). Nell’SDK [!DNL Spark], questo viene fatto utilizzando la funzione `sort()` .

Di seguito è riportato un esempio di utilizzo della funzione `sort()` :

```scala
df = df.sort($"column1", $"column2".desc)
```

### Clausola LIMIT

La clausola LIMIT ti consente di limitare il numero di record ricevuti dal set di dati.

Di seguito è riportato un esempio di utilizzo della funzione `limit()` :

```scala
df = df.limit(100)
```

## Scrittura in un set di dati

Utilizzando la mappatura `configProperties`, puoi scrivere in un set di dati in un Experience Platform utilizzando `QSOption`.

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

Adobe Experience Platform Data Science Workspace fornisce un esempio di ricetta Scala (Spark) che utilizza gli esempi di codice riportati sopra per leggere e scrivere i dati. Per ulteriori informazioni su come utilizzare Spark per accedere ai dati, consulta l’ [Archivio Scala GitHub di Data Science Workspace](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
