---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Secure Spark Data Access SDK
topic: tutorial
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 1%

---


# Secure [!DNL Spark Data Access] SDK

Secure [!DNL Spark][!DNL Data Access] SDK è un kit di sviluppo software che consente di leggere e scrivere set di dati da  Adobe Experience Platform.

## Introduzione

Per poter accedere ai valori per effettuare chiamate all’SDK di protezione, devi completare l’esercitazione [di autenticazione](../../tutorials/authentication.md) [!DNL Spark][!DNL Data Access] :

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. L’utilizzo dell’ [!DNL Spark] SDK richiede il nome e l’ID della sandbox in cui avrà luogo l’operazione:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

## Configurazione dell&#39;ambiente

L&#39; [!DNL Spark] SDK prevede che tu fornisca le credenziali nelle variabili di ambiente o nelle opzioni Origine dati.

| Variable | Valore |
| -------- | ----- | 
| `SERVICE_TOKEN` | Token di autorizzazione del servizio. |
| `SERVICE_API_KEY` | La chiave API del servizio. In genere corrisponde all&#39;ID client IMS. |
| `ORG_ID` | Il valore `{IMS_ORG}` ID. |
| `USER_TOKEN` | Il vostro `{ACCESS_TOKEN}` valore. |

Altri parametri di configurazione includono:

| Variable | Valore |
| -------- | ----- |
| `ENVIRONMENT_NAME` | Ambiente a cui si sta tentando di connettersi. Può trattarsi di &quot;dev&quot;, &quot;stage&quot; o &quot;prod&quot;. |
| `SANDBOX_NAME` | Nome della sandbox a cui ci si sta connettendo. |

In alternativa, oltre a `ENVIRONMENT_NAME`, puoi impostare una qualsiasi delle variabili di ambiente sopra riportate all&#39;interno `QSOption`, come illustrato nell&#39;esempio seguente:

```scala
val df = spark.read
    .format("com.adobe.platform.query")
    .option(QSOption.userToken, userToken) // same as env var USER_TOKEN
    .option(QSOption.imsOrg, "69A7534C5808063C0A494234@AdobeOrg") // same as env var ORG_ID
    .option(QSOption.apiKey, "acp_foundation_queryService") // same as env var SERVICE_API_KEY
    .option("mode", "interactive")
    .option("query", "SELECT * FROM csv10000row_xcm_001 LIMIT 10")
    .load()
```

## Installazione

L’utilizzo dell’ [!DNL Spark] SDK richiede ottimizzazioni delle prestazioni che devono essere aggiunte al `SparkSession`. È possibile applicarli utilizzando uno dei seguenti metodi:

Applicatelo direttamente alla SparkSession corrente:

```scala
import com.adobe.platform.query.QSOptimizations
QSOptimizations.apply(spark)
```

Impostare la seguente conf prima o durante la creazione di SparkSession:

```scala
spark.sql.extensions = com.adobe.platform.query.QSSparkSessionExtensions
```

## Lettura di un dataset

L’ [!DNL Spark] SDK supporta due modalità di lettura: interattivo e batch.

La modalità interattiva crea una connessione Java Database Connectivity (JDBC) a [!DNL Query Service] e ottiene risultati tramite un JDBC regolare `ResultSet` che viene automaticamente convertito in un `DataFrame`. Questa modalità funziona in modo simile al [!DNL Spark] metodo incorporato `spark.read.jdbc()`. Questa modalità è destinata solo ai set di dati di piccole dimensioni e richiede solo un token utente per l&#39;autenticazione.

La modalità batch utilizza [!DNL Query Service]il comando COPY per generare set di risultati Parquet in una posizione condivisa. Questi file Parquet possono essere elaborati ulteriormente. Questa modalità richiede sia un token utente che un token di servizio con l&#39; `acp.foundation.catalog.credentials` ambito.

Di seguito è riportato un esempio di lettura di un dataset in modalità interattiva:

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "interactive")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

Analogamente, un esempio di lettura di un set di dati in modalità batch è riportato di seguito:

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "batch")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
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

La clausola LIMIT consente agli utenti di limitare il numero di record ricevuti dall&#39;insieme di dati.

Di seguito è riportato un esempio di utilizzo della `limit()` funzione:

```scala
df = df.limit(100)
```

## Scrittura in un dataset

L&#39; [!DNL Spark] SDK supporta la scrittura di set di dati. Gli utenti dovranno innanzitutto recuperare un dataset precedente per scrivere in un nuovo dataset.

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", userToken)
      .option("ims-org", "{IMS_ORG}")
      .option("api-key", "{API_KEY}")
      .option("mode", "interactive")
      .option("dataset-id", "{DATASET_ID}")
      .load()

    df.write
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", "{IMS_ORG_ID})
      .option("api-key", "{API_KEY}")
      .option("create-dataset", "{DATASET_ID}")
      .save()
```
