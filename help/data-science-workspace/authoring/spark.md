---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api;spark recipe;read spark;write spark
solution: Experience Platform
title: Accesso ai dati con Spark
topic: tutorial
type: Tutorial
description: Il seguente documento contiene esempi su come accedere ai dati utilizzando Spark per l’utilizzo in Data Science Workspace.
translation-type: tm+mt
source-git-commit: fcb4088ecac76d10b0cb69b04ad55167f5cdac3e
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Accesso ai dati con Spark

Il seguente documento contiene esempi su come accedere ai dati utilizzando Spark per l’utilizzo in Data Science Workspace. Per informazioni sull&#39;accesso ai dati utilizzando i notebook JupyterLab, consulta la documentazione sull&#39;accesso [ai dati dei notebook](../jupyterlab/access-notebook-data.md) JupyterLab.

## Introduzione

L&#39;utilizzo [!DNL Spark] richiede ottimizzazioni delle prestazioni che devono essere aggiunte al `SparkSession`. È inoltre possibile impostare `configProperties` per la lettura e la scrittura successive nei set di dati.

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
            val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## Lettura di un dataset

Con Spark è possibile accedere a due modalità di lettura: interattivo e batch.

La modalità interattiva crea una connessione Java Database Connectivity (JDBC) a [!DNL Query Service] e ottiene risultati tramite un JDBC regolare `ResultSet` che viene automaticamente convertito in un `DataFrame`. Questa modalità funziona in modo simile al [!DNL Spark] metodo incorporato `spark.read.jdbc()`. Questa modalità è valida solo per i set di dati di piccole dimensioni. Se il set di dati supera i 5 milioni di righe, si consiglia di passare alla modalità batch.

La modalità batch utilizza [!DNL Query Service]il comando COPY per generare set di risultati Parquet in una posizione condivisa. Questi file Parquet possono essere elaborati ulteriormente.

Di seguito è riportato un esempio di lettura di un dataset in modalità interattiva:

```scala
  // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
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
      .option(QSOption.serviceToken, serviceToken)
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

Di seguito è riportato un esempio di utilizzo della `distinct()` funzione:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### Clausola WHERE

L’ [!DNL Spark] SDK consente due metodi per filtrare: Utilizzo di un&#39;espressione SQL o filtraggio attraverso le condizioni.

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

La clausola ORDER BY consente di ordinare i risultati ricevuti in base a una colonna specificata in un ordine specifico (crescente o decrescente). Nell’ [!DNL Spark] SDK, questa operazione viene eseguita utilizzando la `sort()` funzione.

Di seguito è riportato un esempio di utilizzo della `sort()` funzione:

```scala
df = df.sort($"column1", $"column2".desc)
```

### Clausola LIMIT

La clausola LIMIT consente di limitare il numero di record ricevuti dal set di dati.

Di seguito è riportato un esempio di utilizzo della `limit()` funzione:

```scala
df = df.limit(100)
```

## Scrittura in un dataset

Utilizzando la `configProperties` mappatura, potete scrivere in un dataset in  Experience Platform utilizzando `QSOption`.

```scala
val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## Passaggi successivi

Adobe Experience Platform Data Science Workspace fornisce un esempio di ricetta Scala (Spark) che utilizza gli esempi di codice riportati sopra per leggere e scrivere i dati. Per ulteriori informazioni sull&#39;utilizzo di Spark per l&#39;accesso ai dati, consulta il repository [Scala GitHub di](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala)Data Science Workspace.