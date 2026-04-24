---
title: Blocco anonimo in Query Service
description: Il blocco anonimo è una sintassi SQL supportata da Adobe Experience Platform Query Service che consente di eseguire in modo efficiente una sequenza di query
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: f2d81f05c8c19c6f28849fc4dbe9bfa26be64645
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Blocco anonimo in Query Service

Adobe Experience Platform Query Service supporta blocchi anonimi. La funzione di blocco anonimo consente di concatenare una o più istruzioni SQL eseguite in sequenza. Consentono inoltre di gestire le eccezioni.

La funzione di blocco anonimo rappresenta un modo efficiente per eseguire una sequenza di operazioni o query. La catena di query all’interno del blocco può essere salvata come modello e pianificata per l’esecuzione in un determinato momento o intervallo. Queste query possono essere utilizzate per scrivere e accodare dati per creare un nuovo set di dati e vengono in genere utilizzate nei casi in cui si dispone di una dipendenza.

La tabella fornisce un raggruppamento delle sezioni principali del blocco: esecuzione e gestione delle eccezioni. Le sezioni sono definite dalle parole chiave `BEGIN`, `END` e `EXCEPTION`.

| sezione | descrizione |
|---|---|
| esecuzione | Una sezione eseguibile inizia con la parola chiave `BEGIN` e termina con la parola chiave `END`. Qualsiasi set di istruzioni incluso nelle parole chiave `BEGIN` e `END` verrà eseguito in sequenza e garantisce che le query successive non vengano eseguite fino al completamento della query precedente nella sequenza. |
| gestione delle eccezioni | La sezione facoltativa per la gestione delle eccezioni inizia con la parola chiave `EXCEPTION`. Contiene il codice per intercettare e gestire le eccezioni in caso di errore di una qualsiasi delle istruzioni SQL nella sezione di esecuzione. Se una delle query ha esito negativo, l’intero blocco viene interrotto. |

È opportuno notare che un blocco è un’istruzione eseguibile e può pertanto essere nidificato all’interno di altri blocchi.

>[!NOTE]
>
> Si consiglia vivamente di testare le query su set di dati più piccoli e di assicurarsi che funzionino come previsto. Se una query presenta un errore di sintassi, verrà generata l’eccezione e l’intero blocco verrà interrotto. Dopo aver verificato l’integrità delle query, puoi iniziare a concatenarle. In questo modo il blocco funziona come previsto prima di metterlo in funzione.

## Sample anonymous block queries

The following query shows an example of chaining SQL statements. See the [SQL syntax in Query Service](../sql/syntax.md) document for more information on any of the SQL syntax used.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHERS THEN SET @ret = SELECT 'ERROR';
END
$$;
```

In the example below, `SET` persists the result of a `SELECT` query in the specified local variable. The variable is scoped to the anonymous block.

The snapshot ID is stored as a local variable (`@current_sid`). It is then used in the next query to return results based on the SNAPSHOT from the same dataset/table. For more [information on the snapshot clause](../sql/syntax.md#SNAPSHOT-clause) see the SQL syntax documentation.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Anonymous block with third-party clients {#third-party-clients}

Certain third-party clients may require a separate identifier before and after an SQL block to indicate that a part of the script should be handled as a single statement. If you receive an error message when using Query Service with a third-party client, you should refer to the documentation of the third-party client regarding the use of an SQL block.

For example, **DbVisualizer** requires that the delimiter must be the only text on the line. In DbVisualizer, the default value for the Begin Identifier is `--/` and for the End Identifier it is `/`. An example of an anonymous block in DbVisualizer is seen below:

```SQL
--/
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
    EXCEPTION WHEN OTHERS THEN SET @ret = SELECT 'ERROR';
END
$$;
/
```

For DbVisualizer in particular, there is also an option in the UI to &quot;[!DNL Execute the complete buffer as one SQL statement]&quot;. See the [DbVisualizer documentation](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsingExecuteBuffer) for more information.

## Passaggi successivi

By reading this document, you now have a clear understanding of anonymous blocks and how they are structured. Please read the [query execution guide](../best-practices/writing-queries.md) for more information on writing queries.

You should also read about [how anonymous blocks are used with the incremental load design pattern](./incremental-load.md) to increase query efficiency.
