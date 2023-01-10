---
keywords: Experience Platform;home;argomenti popolari;accesso ai dati;scintilla sdk;api di accesso ai dati;ricetta di scintilla;scintilla di lettura;scintilla di scrittura
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

# Accesso ai dati tramite Spark in Data Science Workspace

Il seguente documento contiene esempi su come accedere ai dati utilizzando Spark per l’utilizzo in Data Science Workspace. Per informazioni sull&#39;accesso ai dati tramite i notebook JupyterLab, visita [Accesso ai dati dei notebook JupyterLab](../jupyterlab/access-notebook-data.md) documentazione.

## Introduzione

Utilizzo [!DNL Spark] richiede ottimizzazioni delle prestazioni che devono essere aggiunte al `SparkSession`. È inoltre possibile configurare `configProperties` per leggere e scrivere in un secondo momento nei set di dati.

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

La modalità interattiva crea una connessione JDBC (Java Database Connectivity) a [!DNL Query Service] e ottiene risultati attraverso un normale JDBC `ResultSet` che viene automaticamente tradotto in un `DataFrame`. Questa modalità funziona in modo simile a quella incorporata [!DNL Spark] metodo `spark.read.jdbc()`. Questa modalità è destinata solo ai set di dati di piccole dimensioni. Se il set di dati supera i 5 milioni di righe, è consigliabile passare alla modalità batch.

La modalità batch utilizza [!DNL Query Service]Comando COPY per generare set di risultati Parquet in una posizione condivisa. Questi file Parquet possono quindi essere ulteriormente elaborati.

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

Un esempio di utilizzo del `distinct()` funzionalità di seguito:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### clausola WHERE

La [!DNL Spark] L’SDK consente due metodi di filtraggio: Utilizzo di un&#39;espressione SQL o filtrando tra le condizioni.

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

La clausola ORDER BY consente di ordinare i risultati ricevuti in base a una colonna specifica in un ordine specifico (crescente o decrescente). In [!DNL Spark] SDK, viene eseguito utilizzando `sort()` funzione .

Un esempio di utilizzo del `sort()` funzionalità di seguito:

```scala
df = df.sort($"column1", $"column2".desc)
```

### Clausola LIMIT

La clausola LIMIT ti consente di limitare il numero di record ricevuti dal set di dati.

Un esempio di utilizzo del `limit()` funzionalità di seguito:

```scala
df = df.limit(100)
```

## Scrittura in un set di dati

Utilizzo della `configProperties` mappatura, puoi scrivere in un set di dati in Experience Platform utilizzando `QSOption`.

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

Adobe Experience Platform Data Science Workspace fornisce un esempio di ricetta Scala (Spark) che utilizza gli esempi di codice riportati sopra per leggere e scrivere i dati. Per ulteriori informazioni su come utilizzare Spark per accedere ai dati, consulta la [Archivio GitHub Scala di Data Science Workspace](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
