---
title: Abilitare Change Data Capture per le connessioni di origine nell’API
description: Scopri come abilitare l’acquisizione dei dati di modifica per le connessioni di origine nell’API
exl-id: 362f3811-7d1e-4f16-b45f-ce04f03798aa
source-git-commit: bd28d5be932823b8bf9c98280f97694ff221d76d
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 0%

---

# Abilitare Change Data Capture per le connessioni di origine nell’API

>[!AVAILABILITY]
>
>È ora possibile utilizzare l&#39;acquisizione dei dati di modifica per le origini [!DNL Amazon S3] e [!DNL Data Landing Zone] durante l&#39;esecuzione di Adobe Experience Platform su Amazon Web Services (AWS) durante la connessione a un data center VA6. Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../landing/multi-cloud.md).

Utilizza l’acquisizione dei dati di modifica nelle origini Adobe Experience Platform per mantenere sincronizzati i sistemi di origine e di destinazione quasi in tempo reale.

Experience Platform attualmente supporta **copia dati incrementale**, che trasferisce periodicamente i record appena creati o aggiornati dal sistema di origine ai set di dati acquisiti. Questo metodo si basa su una **colonna timestamp** per tenere traccia delle modifiche, ma non rileva le eliminazioni, il che può causare incongruenze nei dati nel tempo.

Cambia invece acquisisce ed applica inserti, aggiornamenti ed eliminazioni quasi in tempo reale. Questo monitoraggio completo delle modifiche assicura che i set di dati rimangano completamente allineati al sistema di origine e fornisce una cronologia completa delle modifiche, oltre a ciò che supporta la copia incrementale. Tuttavia, le operazioni di eliminazione richiedono una considerazione particolare in quanto influiscono su tutte le applicazioni che utilizzano i set di dati di destinazione.

La modifica dell&#39;acquisizione dati in Experience Platform richiede **[Data Mirror](../../../xdm/data-mirror/overview.md)** con [schemi relazionali](../../../xdm/schema/relational.md). È possibile fornire i dati di modifica a Data Mirror in due modi:

* **[Rilevamento delle modifiche manuale](#file-based-sources)**: includi una colonna `_change_request_type` nel set di dati per le origini che non generano in modo nativo record di acquisizione dati di modifica
* **[Esportazioni native di acquisizione dati di modifica](#database-sources)**: utilizza i record di acquisizione dati di modifica esportati direttamente dal sistema di origine

Entrambi gli approcci richiedono Data Mirror con schemi relazionali per preservare le relazioni e applicare l’univocità.

## Data Mirror con schemi relazionali

>[!AVAILABILITY]
>
>Data Mirror e gli schemi relazionali sono disponibili per i titolari di licenze di **Campagne orchestrate** Adobe Journey Optimizer. Sono disponibili anche come **versione limitata** per gli utenti di Customer Journey Analytics, a seconda della licenza e dell&#39;abilitazione della funzione. Contatta il tuo rappresentante Adobe per accedere.

>[!NOTE]
>
>**Utenti di campagne orchestrate**: utilizza le funzionalità di Data Mirror descritte in questo documento per lavorare con i dati dei clienti mantenendo l&#39;integrità referenziale. Anche se l&#39;origine non utilizza la formattazione di acquisizione dati di modifica, Data Mirror supporta funzioni relazionali quali l&#39;imposizione della chiave primaria, gli aggiornamenti a livello di record e le relazioni tra schemi. Queste funzioni garantiscono una modellazione dei dati coerente e affidabile tra i set di dati connessi.

Data Mirror utilizza gli schemi relazionali per estendere l’acquisizione dei dati sulle modifiche e abilitare funzionalità avanzate di sincronizzazione del database. Per una panoramica di Data Mirror, vedere [Panoramica di Data Mirror](../../../xdm/data-mirror/overview.md).

Gli schemi relazionali estendono Experience Platform per applicare l’univocità della chiave primaria, tenere traccia delle modifiche a livello di riga e definire relazioni a livello di schema. Con l’acquisizione dei dati di modifica, vengono applicati inserti, aggiornamenti ed eliminazioni direttamente nel data lake, riducendo la necessità di estrarre, trasformare, caricare (ETL) o riconciliazione manuale.

Per ulteriori informazioni, vedere [Panoramica sugli schemi relazionali](../../../xdm/schema/relational.md).

### Requisiti dello schema relazionale per l’acquisizione dei dati di modifica

Prima di utilizzare uno schema relazionale con Change Data Capture, configura i seguenti identificatori:

* Identificare in modo univoco ogni record con una chiave primaria.
* Applica gli aggiornamenti in sequenza utilizzando un identificatore di versione.
* Per gli schemi di serie temporali, aggiungi un identificatore di marca temporale.

### Gestione colonne di controllo {#control-column-handling}

Utilizzare la colonna `_change_request_type` per specificare la modalità di elaborazione di ogni riga:

* `u` — upsert (impostazione predefinita se la colonna è assente)
* `d` — elimina

Questa colonna viene valutata solo durante l’acquisizione e non viene memorizzata o mappata su campi XDM.

### Flusso di lavoro {#workflow}

Per abilitare l&#39;acquisizione dei dati di modifica con uno schema relazionale:

1. Creare uno schema relazionale.
2. Aggiungi i descrittori richiesti:
   * [Descrittore della chiave primaria](../../../xdm/api/descriptors.md#primary-key-descriptor)
   * [Descrittore versione](../../../xdm/api/descriptors.md#version-descriptor)
   * [Descrittore marca temporale](../../../xdm/api/descriptors.md#timestamp-descriptor) (solo serie temporali)
3. Crea un set di dati dallo schema e abilita l’acquisizione dei dati di modifica.
4. Solo per l’acquisizione basata su file: se devi specificare esplicitamente le operazioni di eliminazione, aggiungi la colonna `_change_request_type` ai file di origine. Le configurazioni di esportazione CDC gestiscono automaticamente questa situazione per le origini del database.
5. Completa l’impostazione della connessione di origine per abilitare l’acquisizione.

>[!NOTE]
>
>La colonna `_change_request_type` è necessaria solo per le origini basate su file (Amazon S3, Azure Blob, Google Cloud Storage, SFTP) quando si desidera controllare in modo esplicito il comportamento di modifica a livello di riga. Per le origini di database con funzionalità CDC native, le operazioni di modifica vengono gestite automaticamente tramite le configurazioni di esportazione CDC. Per impostazione predefinita, l’acquisizione basata su file prevede l’esecuzione di operazioni upsert. È sufficiente aggiungere questa colonna per specificare le operazioni di eliminazione nei caricamenti di file.

>[!IMPORTANT]
>
>**È richiesta la pianificazione dell&#39;eliminazione dei dati**. Tutte le applicazioni che utilizzano schemi relazionali devono comprendere le implicazioni relative all’eliminazione prima di implementare l’acquisizione dei dati di modifica. Pianifica in che modo le eliminazioni influiranno sui set di dati correlati, sui requisiti di conformità e sui processi a valle. Consulta [considerazioni sull&#39;igiene dei dati](../../../hygiene/ui/record-delete.md#relational-record-delete) per maggiori informazioni.

## Fornitura di dati di modifica per origini basate su file {#file-based-sources}

>[!IMPORTANT]
>
>L&#39;acquisizione dei dati di modifica basata su file richiede Data Mirror con schemi relazionali. Prima di seguire i passaggi di formattazione dei file riportati di seguito, assicurati di aver completato il [flusso di lavoro di installazione di Data Mirror](#workflow) descritto in precedenza in questo documento. I passaggi seguenti descrivono come formattare i file di dati per includere le informazioni di rilevamento delle modifiche che verranno elaborate da Data Mirror.

Per le origini basate su file ([!DNL Amazon S3], [!DNL Azure Blob], [!DNL Google Cloud Storage] e [!DNL SFTP]), includere una colonna `_change_request_type` nei file.

Utilizza i valori `_change_request_type` definiti nella sezione precedente [Gestione colonna di controllo](#control-column-handling).

>[!IMPORTANT]
>
>Solo per **origini basate su file**, alcune applicazioni potrebbero richiedere una colonna `_change_request_type` con `u` (upsert) o `d` (delete) per convalidare le funzionalità di rilevamento delle modifiche. Ad esempio, la funzionalità **Campagne orchestrate** di Adobe Journey Optimizer richiede questa colonna per abilitare l&#39;interruttore &quot;Campagna orchestrata&quot; e consentire la selezione del set di dati per il targeting. I requisiti di convalida specifici dell’applicazione possono variare.

Segui i passaggi specifici per l’origine riportati di seguito.

### Origini archiviazione cloud {#cloud-storage-sources}

Abilita l’acquisizione dei dati di modifica per le origini di archiviazione cloud seguendo questi passaggi:

1. Creare una connessione di base per l&#39;origine:

   | Origine | Guida alla connessione di base |
   |---|---|
   | [!DNL Amazon S3] | [Crea una [!DNL Amazon S3] connessione di base](../api/create/cloud-storage/s3.md) |
   | [!DNL Azure Blob] | [Crea una [!DNL Azure Blob] connessione di base](../api/create/cloud-storage/blob.md) |
   | [!DNL Google Cloud Storage] | [Crea una [!DNL Google Cloud Storage] connessione di base](../api/create/cloud-storage/google.md) |
   | [!DNL SFTP] | [Crea una [!DNL SFTP] connessione di base](../api/create/cloud-storage/sftp.md) |

2. [Creare una connessione di origine per un&#39;archiviazione cloud](../api/collect/cloud-storage.md#create-a-source-connection).

Tutte le origini di archiviazione cloud utilizzano lo stesso formato di colonna `_change_request_type` descritto nella sezione [Origini basate su file](#file-based-sources) precedente.

## Origini del database {#database-sources}

### [!DNL Azure Databricks]

Per utilizzare Change Data Capture con [!DNL Azure Databricks], è necessario abilitare **change Data Feed** nelle tabelle di origine e configurare Data Mirror con schemi relazionali in Experience Platform.

Utilizzare i seguenti comandi per abilitare il feed di dati di modifica nelle tabelle:

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

### [!DNL Data Landing Zone]

Per utilizzare Change Data Capture con [!DNL Data Landing Zone], è necessario abilitare **change Data Feed** nelle tabelle di origine e configurare Data Mirror con schemi relazionali in Experience Platform.

Per i passaggi su come abilitare l&#39;acquisizione dei dati di modifica per la connessione di origine [!DNL Data Landing Zone], leggere la seguente documentazione:

* [Crea una [!DNL Data Landing Zone] connessione di base](../api/create/cloud-storage/data-landing-zone.md).
* [Creare una connessione di origine per un&#39;archiviazione cloud](../api/collect/cloud-storage.md#create-a-source-connection).

### [!DNL Google BigQuery]

Per utilizzare Change Data Capture con [!DNL Google BigQuery], è necessario abilitare la cronologia delle modifiche nelle tabelle di origine e configurare Data Mirror con schemi relazionali in Experience Platform.

Per abilitare la cronologia delle modifiche nella connessione di origine [!DNL Google BigQuery], passare alla pagina [!DNL Google BigQuery] nella console [!DNL Google Cloud] e impostare `enable_change_history` su `TRUE`. Questa proprietà abilita la cronologia delle modifiche per la tabella dati.

Per ulteriori informazioni, leggere la guida sulle [istruzioni del linguaggio di definizione dei dati in [!DNL GoogleSQL]](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Per i passaggi su come abilitare l&#39;acquisizione dei dati di modifica per la connessione di origine [!DNL Google BigQuery], leggere la seguente documentazione:

* [Crea una [!DNL Google BigQuery] connessione di base](../api/create/databases/bigquery.md).
* [Creare una connessione di origine per un database](../api/collect/database-nosql.md#create-a-source-connection).

### [!DNL Snowflake]

Per utilizzare Change Data Capture con [!DNL Snowflake], è necessario abilitare **rilevamento modifiche** nelle tabelle di origine e configurare Data Mirror con schemi relazionali in Experience Platform.

In [!DNL Snowflake], abilitare il rilevamento delle modifiche utilizzando `ALTER TABLE` e impostando `CHANGE_TRACKING` su `TRUE`.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Per ulteriori informazioni, leggere la [[!DNL Snowflake] guida sull&#39;utilizzo della clausola changes](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Per i passaggi su come abilitare l&#39;acquisizione dei dati di modifica per la connessione di origine [!DNL Snowflake], leggere la seguente documentazione:

* [Crea una [!DNL Snowflake] connessione di base](../api/create/databases/snowflake.md).
* [Creare una connessione di origine per un database](../api/collect/database-nosql.md#create-a-source-connection).
