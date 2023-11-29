---
title: Carico incrementale in Query Service
description: La funzione di caricamento incrementale utilizza sia le funzioni di blocco anonimo che di istantanea per fornire una soluzione quasi in tempo reale per spostare i dati dal data lake al data warehouse ignorando i dati corrispondenti.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Carico incrementale in Query Service

Il modello di progettazione del carico incrementale è una soluzione per la gestione dei dati. Il modello elabora solo le informazioni nel set di dati che è stato creato o modificato dopo l’ultima esecuzione del caricamento.

Il caricamento incrementale utilizza varie funzioni fornite da Adobe Experience Platform Query Service, ad esempio blocchi anonimi e snapshot. Questo modello di progettazione aumenta l’efficienza di elaborazione quando tutti i dati già elaborati dall’origine vengono ignorati. Può essere utilizzato sia con l’elaborazione dei dati in streaming che in batch.

Questo documento fornisce una serie di istruzioni per creare un modello di progettazione per l’elaborazione incrementale. Questi passaggi possono essere utilizzati come modello per creare query di caricamento dati incrementali personalizzate.

## Introduzione

Gli esempi SQL illustrati in questo documento richiedono una conoscenza approfondita delle funzionalità di blocco anonimo e snapshot. Si consiglia di leggere il [query di blocco anonime di esempio](./anonymous-block.md) e anche la [clausola snapshot](../sql/syntax.md#snapshot-clause) documentazione.

Per informazioni su qualsiasi terminologia utilizzata in questa guida, consulta la [Guida alla sintassi SQL](../sql/syntax.md).

## Caricamento incrementale dei dati

I passaggi seguenti mostrano come creare e caricare i dati in modo incrementale utilizzando gli snapshot e la funzione di blocco anonimo. Il modello struttura può essere utilizzato come modello per la propria sequenza di query.

1. Creare un `checkpoint_log` tabella per tenere traccia dello snapshot più recente utilizzato per elaborare correttamente i dati. Tabella di tracciamento (`checkpoint_log` in questo esempio) deve prima essere inizializzato in `null` per elaborare in modo incrementale un set di dati.

   ```SQL
   DROP TABLE IF EXISTS checkpoint_log;
   CREATE TABLE  checkpoint_log AS
   SELECT
      cast(NULL AS string) process_name,
      cast(NULL AS string) process_status,
      cast(NULL AS string) last_snapshot_id,
      cast(NULL AS TIMESTAMP) process_timestamp
      WHERE false;
   ```

1. Popolare il `checkpoint_log` con un record vuoto per il set di dati che richiede l’elaborazione incrementale. `DIM_TABLE_ABC` è il set di dati da elaborare nell’esempio seguente. Alla prima trasformazione `DIM_TABLE_ABC`, il `last_snapshot_id` è inizializzato come `null`. Questo consente di elaborare l’intero set di dati la prima volta e in modo incrementale in seguito.

   ```SQL
   INSERT INTO
      checkpoint_log
      SELECT
         'DIM_TABLE_ABC' process_name,
         'SUCCESSFUL' process_status,
         cast(NULL AS string) last_snapshot_id,
         CURRENT_TIMESTAMP process_timestamp;
   ```

1. Quindi, inizializza `DIM_TABLE_ABC_Incremental` per contenere l&#39;output elaborato da `DIM_TABLE_ABC`. Blocco anonimo in **obbligatorio** La sezione di esecuzione dell&#39;esempio SQL seguente, come descritto nei passaggi da uno a quattro, viene eseguita in sequenza per elaborare i dati in modo incrementale.

   1. Imposta il `from_snapshot_id` che indica da dove inizia l’elaborazione. Il `from_snapshot_id` nell’esempio viene interrogato da `checkpoint_log` tabella da utilizzare con `DIM_TABLE_ABC`. Nell&#39;esecuzione iniziale, l&#39;ID snapshot sarà `null` ciò significa che verrà elaborato l’intero set di dati.
   1. Imposta il `to_snapshot_id` come ID snapshot corrente della tabella di origine (`DIM_TABLE_ABC`). Nell’esempio, questa viene eseguita dalla tabella dei metadati della tabella di origine.
   1. Utilizza il `CREATE` parola chiave da creare `DIM_TABLE_ABC_Incremenal` come tabella di destinazione. La tabella di destinazione salva in modo permanente i dati elaborati dal set di dati di origine (`DIM_TABLE_ABC`). In questo modo i dati elaborati dalla tabella di origine tra `from_snapshot_id` e `to_snapshot_id`, da aggiungere in modo incrementale alla tabella di destinazione.
   1. Aggiornare il `checkpoint_log` tabella con `to_snapshot_id` per i dati di origine che `DIM_TABLE_ABC` elaborato correttamente.
   1. Se una delle query eseguite in sequenza del blocco anonimo ha esito negativo, il **facoltativo** viene eseguita la sezione delle eccezioni. Questo restituisce un errore e termina il processo.

   >[!NOTE]
   >
   >Il `history_meta('source table name')` è un metodo pratico utilizzato per accedere alle istantanee disponibili in un set di dati.

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       CREATE TABLE DIM_TABLE_ABC_Incremental AS
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id ;
   
   INSERT INTO
      checkpoint_log
      SELECT
          'DIM_TABLE_ABC' process_name,
          'SUCCESSFUL' process_status,
         cast( @to_snapshot_id AS string) last_snapshot_id,
         cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
   
   EXCEPTION
     WHEN OTHER THEN
       SELECT 'ERROR';
   END 
   $$;
   ```

1. Utilizza la logica di caricamento dati incrementale nell’esempio di blocco anonimo seguente per consentire a tutti i nuovi dati dal set di dati di origine (dal timestamp più recente) di essere elaborati e aggiunti alla tabella di destinazione a una cadenza regolare. Nell’esempio, i dati diventano `DIM_TABLE_ABC` verrà elaborato e aggiunto a `DIM_TABLE_ABC_incremental`.

   >[!NOTE]
   >
   > `_ID` è la chiave primaria in entrambi `DIM_TABLE_ABC_Incremental` e `SELECT history_meta('DIM_TABLE_ABC')`.

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a join
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       INSERT INTO DIM_TABLE_ABC_Incremental
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
   
   INSERT INTO
      checkpoint_log
      SELECT
          'DIM_TABLE_ABC' process_name,
          'SUCCESSFUL' process_status,
         cast( @to_snapshot_id AS string) last_snapshot_id,
         cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
   
   EXCEPTION
     WHEN OTHER THEN
       SELECT 'ERROR';
   END
   $$;
   ```

Questa logica può essere applicata a qualsiasi tabella per eseguire caricamenti incrementali.

## Snapshot scaduti

>[!IMPORTANT]
>
>Scadenza metadati snapshot dopo **due** giorni. Uno snapshot scaduto invalida la logica dello script fornito in precedenza.

Per risolvere il problema di un ID di snapshot scaduto, inserisci il seguente comando all’inizio del blocco anonimo. La seguente riga di codice sostituisce la `@from_snapshot_id` con la prima versione disponibile `snapshot_id` dai metadati.

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

L’aspetto dell’intero blocco di codice è il seguente:

```SQL
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
 
Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```

## Passaggi successivi

Una volta letto questo documento, sarai in grado di comprendere meglio come utilizzare le funzioni di blocco e istantanea anonime per eseguire caricamenti incrementali e di applicare questa logica alle tue query specifiche. Per informazioni generali sull’esecuzione delle query, consulta la sezione [guida all’esecuzione delle query in Query Service](../best-practices/writing-queries.md).
