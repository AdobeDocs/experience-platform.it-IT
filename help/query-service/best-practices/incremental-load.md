---
title: Query di caricamento incrementale di esempio
description: La funzione di caricamento incrementale utilizza sia le funzioni di blocco anonimo che quelle di snapshot per fornire una soluzione in tempo quasi reale per lo spostamento dei dati dal data lake al data warehouse, ignorando al contempo la corrispondenza dei dati.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: e5a79db157524d014c9a07d2bf5907a5544e7b77
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---

# Query di caricamento dati incrementali di esempio

Il modello di progettazione del carico incrementale è una soluzione per la gestione dei dati. Il pattern elabora solo le informazioni nel set di dati che sono state create o modificate dopo l’ultima esecuzione del caricamento.

Il caricamento incrementale utilizza varie funzioni fornite da Adobe Experience Platform Query Service, come blocchi anonimi e istantanee. Questo pattern di progettazione aumenta l’efficienza di elaborazione in quanto vengono saltati tutti i dati già elaborati dall’origine. Può essere utilizzato sia con l’elaborazione in streaming che con quella in batch.

Questo documento fornisce una serie di istruzioni per creare un pattern di progettazione per l’elaborazione incrementale. Questi passaggi possono essere utilizzati come modello per creare query di caricamento dati incrementali personalizzate.

## Introduzione

Gli esempi SQL presenti in questo documento richiedono una comprensione delle funzionalità di blocco anonimo e snapshot. Si consiglia di leggere il [query di blocco anonime di esempio](./anonymous-block.md) la documentazione e [clausola snapshot](../sql/syntax.md#snapshot-clause) documentazione.

Per informazioni su qualsiasi terminologia utilizzata in questa guida, consulta [Guida alla sintassi SQL](../sql/syntax.md).

## Caricamento dati incrementale

I passaggi seguenti mostrano come creare e caricare in modo incrementale i dati utilizzando le istantanee e la funzione blocco anonimo. Il pattern di progettazione può essere utilizzato come modello per la propria sequenza di query.

1 Crea un `checkpoint_log` per tenere traccia dello snapshot più recente utilizzato per elaborare correttamente i dati. La tabella di tracciamento (`checkpoint_log` in questo esempio) deve prima essere inizializzato a `null` per elaborare in modo incrementale un set di dati.

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

2 Popolare `checkpoint_log` tabella con un record vuoto per il set di dati che richiede l’elaborazione incrementale. `DIM_TABLE_ABC` è il set di dati da elaborare nell’esempio seguente. In occasione della prima trasformazione `DIM_TABLE_ABC`, `last_snapshot_id` viene inizializzato come `null`. Questo consente di elaborare l’intero set di dati la prima volta e in modo incrementale successivamente.

```SQL
INSERT INTO
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
       cast(NULL AS string) last_snapshot_id,
       CURRENT_TIMESTAMP process_timestamp;
```

3 Inizializzazione successiva `DIM_TABLE_ABC_Incremental` per contenere l&#39;output elaborato da `DIM_TABLE_ABC`. Il blocco anonimo nel **obbligatorio** la sezione di esecuzione dell&#39;esempio SQL seguente, come descritto nei passaggi da uno a quattro, viene eseguita in sequenza per elaborare i dati in modo incrementale.

1. Imposta la `from_snapshot_id` che indica da dove inizia l’elaborazione. La `from_snapshot_id` nell&#39;esempio viene interrogato dal `checkpoint_log` tabella per l&#39;uso con `DIM_TABLE_ABC`. All&#39;esecuzione iniziale, l&#39;ID dello snapshot sarà `null` significa che l’intero set di dati verrà elaborato.
2. Imposta la `to_snapshot_id` come ID snapshot corrente della tabella di origine (`DIM_TABLE_ABC`). Nell’esempio, questa viene eseguita dalla tabella di metadati della tabella di origine.
3. Utilizza la `CREATE` parola chiave da creare `DIM_TABLE_ABC_Incremenal` come tabella di destinazione. La tabella di destinazione persiste i dati elaborati dal set di dati di origine (`DIM_TABLE_ABC`). Ciò consente di elaborare i dati dalla tabella di origine tra `from_snapshot_id` e `to_snapshot_id`, da aggiungere in modo incrementale alla tabella di destinazione.
4. Aggiorna `checkpoint_log` con `to_snapshot_id` per i dati di origine che `DIM_TABLE_ABC` elaborazione completata.
5. Se una delle query eseguite in sequenza del blocco anonimo non riesce, la **facoltativo** viene eseguita la sezione delle eccezioni. Questo restituisce un errore e termina il processo.

>[!NOTE]
>
>La `history_meta('source table name')` è un metodo comodo utilizzato per accedere allo snapshot disponibile in un set di dati.

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

4 Utilizza la logica di caricamento dati incrementale nell’esempio di blocco anonimo seguente per consentire l’elaborazione e l’aggiunta regolare di nuovi dati dal set di dati di origine (dal timestamp più recente) alla tabella di destinazione a cadenza regolare. Nell’esempio, i dati vengono modificati in `DIM_TABLE_ABC` viene elaborato e aggiunto a `DIM_TABLE_ABC_incremental`.

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

Questa logica può essere applicata a qualsiasi tabella per eseguire carichi incrementali.

## Istantanee scadute

>[!IMPORTANT]
>
>I metadati snapshot scadono dopo **due** giorni. Uno snapshot scaduto invalida la logica dello script fornito in precedenza.

Per risolvere il problema di un ID snapshot scaduto, inserire il seguente comando all&#39;inizio del blocco anonimo. La seguente riga di codice sostituisce il `@from_snapshot_id` con il più presto disponibile `snapshot_id` da metadati.

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

L’intero blocco di codice si presenta come segue:

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

Leggendo questo documento, dovresti avere una migliore comprensione di come utilizzare le funzioni di blocco anonimo e snapshot per eseguire carichi incrementali e puoi applicare questa logica alle tue query specifiche. Per informazioni generali sull’esecuzione delle query, leggere il [guida sull’esecuzione delle query in Query Service](./writing-queries.md).
