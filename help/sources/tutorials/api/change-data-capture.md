---
title: Abilitare Change Data Capture per le connessioni di origine nell’API
description: Scopri come abilitare l’acquisizione dei dati di modifica per le connessioni di origine nell’API
source-git-commit: d8b4557424e1f29dfdd8893932aef914226dd60d
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Abilitare Change Data Capture per le connessioni di origine nell’API

Change data capture (Cambia acquisizione dati) nelle origini Adobe Experience Platform è una funzionalità che puoi utilizzare per mantenere la sincronizzazione dei dati in tempo reale tra i sistemi di origine e di destinazione.

Al momento, Experience Platform supporta **copia dati incrementale**, che garantisce che i record appena creati o aggiornati nel sistema di origine vengano periodicamente copiati nei set di dati acquisiti. Questo processo si basa sull&#39;utilizzo della **colonna timestamp**, ad esempio `LastModified`, per tenere traccia delle modifiche e acquisire **solo i dati appena inseriti o aggiornati**. Tuttavia, questo metodo non tiene conto dei record eliminati, il che può causare incoerenze nei dati nel tempo.

Con l’acquisizione dei dati di modifica, un dato flusso acquisisce e applica tutte le modifiche, inclusi inserimenti, aggiornamenti ed eliminazioni. Allo stesso modo, i set di dati di Experience Platform rimangono completamente sincronizzati con il sistema di origine.

È possibile utilizzare l&#39;acquisizione dati di modifica per le origini seguenti:

## [!DNL Amazon S3]

Verificare che `_change_request_type` sia presente nel file [!DNL Amazon S3] che si intende acquisire in Experience Platform. Inoltre, è necessario assicurarsi che i seguenti valori validi siano inclusi nel file:

* `u`: per inserimenti e aggiornamenti
* `d`: per eliminazioni.

Se `_change_request_type` non è presente nel file, verrà utilizzato il valore predefinito di `u`.

Per i passaggi su come abilitare l&#39;acquisizione dei dati di modifica per la connessione di origine [!DNL Amazon S3], leggere la seguente documentazione:

* [Crea una [!DNL Amazon S3] connessione di base](../api/create/cloud-storage/s3.md).
* [Creare una connessione di origine per un&#39;archiviazione cloud](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Blob]

Verificare che `_change_request_type` sia presente nel file [!DNL Azure Blob] che si intende acquisire in Experience Platform. Inoltre, è necessario assicurarsi che i seguenti valori validi siano inclusi nel file:

* `u`: per inserimenti e aggiornamenti
* `d`: per eliminazioni.

Se `_change_request_type` non è presente nel file, verrà utilizzato il valore predefinito di `u`.

Per i passaggi su come abilitare l&#39;acquisizione dei dati di modifica per la connessione di origine [!DNL Azure Blob], leggere la seguente documentazione:

* [Crea una [!DNL Azure Blob] connessione di base](../api/create/cloud-storage/blob.md).
* [Creare una connessione di origine per un&#39;archiviazione cloud](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Databricks]

È necessario abilitare **cambiare feed dati** nella tabella [!DNL Azure Databricks] per utilizzare l&#39;acquisizione dati di modifica nella connessione di origine.

Utilizzare i comandi seguenti per abilitare esplicitamente l&#39;opzione di modifica del feed dati in [!DNL Azure Databricks]

**Nuova tabella**

Per applicare il feed di dati di modifica a una nuova tabella, è necessario impostare la proprietà della tabella `delta.enableChangeDataFeed` su `TRUE` nel comando `CREATE TABLE`.

```sql
CREATE TABLE student (id INT, name STRING, age INT) TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Tabella esistente**

Per applicare il feed di dati di modifica a una tabella esistente, è necessario impostare la proprietà della tabella `delta.enableChangeDataFeed` su `TRUE` nel comando `ALTER TABLE`.

```sql
ALTER TABLE myDeltaTable SET TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Tutte le nuove tabelle**

Per applicare il feed dati di modifica a tutte le nuove tabelle, è necessario impostare le proprietà predefinite su `TRUE`.

```sql
set spark.databricks.delta.properties.defaults.enableChangeDataFeed = true;
```

Per ulteriori informazioni, leggere la [[!DNL Azure Databricks] guida sull&#39;abilitazione del feed di dati di modifica](https://docs.databricks.com/aws/en/delta/delta-change-data-feed#enable-change-data-feed).

Per i passaggi su come abilitare l&#39;acquisizione dei dati di modifica per la connessione di origine [!DNL Azure Databricks], leggere la seguente documentazione:

* [Crea una [!DNL Azure Databricks] connessione di base](../api/create/databases/databricks.md).
* [Creare una connessione di origine per un database](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Data Landing Zone]

È necessario abilitare **cambiare feed dati** nella tabella [!DNL Data Landing Zone] per utilizzare l&#39;acquisizione dati di modifica nella connessione di origine.

Utilizzare i comandi seguenti per abilitare esplicitamente l&#39;opzione di modifica del feed dati in [!DNL Data Landing Zone].

Per i passaggi su come abilitare l&#39;acquisizione dei dati di modifica per la connessione di origine [!DNL Data Landing Zone], leggere la seguente documentazione:

* [Crea una [!DNL Data Landing Zone] connessione di base](../api/create/cloud-storage/data-landing-zone.md).
* [Creare una connessione di origine per un&#39;archiviazione cloud](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Google BigQuery]

Per utilizzare l&#39;acquisizione dati di modifica nella connessione di origine [!DNL Google BigQuery]. Passare alla pagina [!DNL Google BigQuery] nella console [!DNL Google Cloud] e impostare `enable_change_history` su `TRUE`. Questa proprietà abilita la cronologia delle modifiche per la tabella dati.

Per ulteriori informazioni, leggere la guida sulle [istruzioni del linguaggio di definizione dei dati in [!DNL GoogleSQL]](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Per i passaggi su come abilitare l&#39;acquisizione dei dati di modifica per la connessione di origine [!DNL Google BigQuery], leggere la seguente documentazione:

* [Crea una [!DNL Google BigQuery] connessione di base](../api/create/databases/bigquery.md).
* [Creare una connessione di origine per un database](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Google Cloud Storage]

Verificare che `_change_request_type` sia presente nel file [!DNL Google Cloud Storage] che si intende acquisire in Experience Platform. Inoltre, è necessario assicurarsi che i seguenti valori validi siano inclusi nel file:

* `u`: per inserimenti e aggiornamenti
* `d`: per eliminazioni.

Se `_change_request_type` non è presente nel file, verrà utilizzato il valore predefinito di `u`.

Per i passaggi su come abilitare l&#39;acquisizione dei dati di modifica per la connessione di origine [!DNL Google Cloud Storage], leggere la seguente documentazione:

* [Crea una [!DNL Google Cloud Storage] connessione di base](../api/create/cloud-storage/google.md).
* [Creare una connessione di origine per un&#39;archiviazione cloud](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL SFTP]

Verificare che `_change_request_type` sia presente nel file [!DNL SFTP] che si intende acquisire in Experience Platform. Inoltre, è necessario assicurarsi che i seguenti valori validi siano inclusi nel file:

* `u`: per inserimenti e aggiornamenti
* `d`: per eliminazioni.

Se `_change_request_type` non è presente nel file, verrà utilizzato il valore predefinito di `u`.

Per i passaggi su come abilitare l&#39;acquisizione dei dati di modifica per la connessione di origine [!DNL SFTP], leggere la seguente documentazione:

* [Crea una [!DNL SFTP] connessione di base](../api/create/cloud-storage/sftp.md).
* [Creare una connessione di origine per un&#39;archiviazione cloud](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL Snowflake]

Devi abilitare il **rilevamento delle modifiche** nelle tabelle [!DNL Snowflake] per utilizzare l&#39;acquisizione dei dati di modifica nelle connessioni di origine.

In [!DNL Snowflake], abilitare il rilevamento delle modifiche utilizzando `ALTER TABLE` e impostando `CHANGE_TRACKING` su `TRUE`.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Per ulteriori informazioni, leggere la [[!DNL Snowflake] guida sull&#39;utilizzo della clausola changes](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Per i passaggi su come abilitare l&#39;acquisizione dei dati di modifica per la connessione di origine [!DNL Snowflake], leggere la seguente documentazione:

* [Crea una [!DNL Snowflake] connessione di base](../api/create/databases/snowflake.md).
* [Creare una connessione di origine per un database](../api/collect/database-nosql.md#create-a-source-connection).

