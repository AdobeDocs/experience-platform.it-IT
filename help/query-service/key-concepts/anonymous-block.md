---
title: Blocco anonimo in Query Service
description: Il blocco anonimo è una sintassi SQL supportata da Adobe Experience Platform Query Service che consente di eseguire in modo efficiente una sequenza di query
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 65eeeb1df1d512c4cd6c67892905a63cc1cc4fc5
workflow-type: tm+mt
source-wordcount: '603'
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

## Query di blocco anonime di esempio

Nella query seguente viene illustrato un esempio di concatenamento di istruzioni SQL. Per ulteriori informazioni sulla sintassi SQL utilizzata, vedere il documento [Sintassi SQL in Query Service](../sql/syntax.md).

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

Nell&#39;esempio seguente, `SET` mantiene il risultato di una query `SELECT` nella variabile locale specificata. La variabile ha l’ambito del blocco anonimo.

L&#39;ID snapshot è archiviato come variabile locale (`@current_sid`). Viene quindi utilizzato nella query successiva per restituire risultati basati sullo SNAPSHOT dello stesso set di dati/tabella. Per ulteriori [informazioni sulla clausola snapshot](../sql/syntax.md#SNAPSHOT-clause), vedere la documentazione relativa alla sintassi SQL.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Blocco anonimo con client di terze parti {#third-party-clients}

Alcuni client di terze parti possono richiedere un identificatore separato prima e dopo un blocco SQL per indicare che una parte dello script deve essere gestita come una singola istruzione. Se viene visualizzato un messaggio di errore quando si utilizza Query Service con un client di terze parti, è necessario fare riferimento alla documentazione del client di terze parti relativa all&#39;utilizzo di un blocco SQL.

Ad esempio, **DbVisualizer** richiede che il delimitatore sia l&#39;unico testo sulla riga. In DbVisualizer il valore predefinito per l&#39;identificatore iniziale è `--/` e per l&#39;identificatore finale è `/`. Di seguito è riportato un esempio di blocco anonimo in DbVisualizer:

```SQL
--/
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
/
```

Nell&#39;interfaccia utente di DbVisualizer, in particolare, è inoltre disponibile un&#39;opzione per &quot;[!DNL Execute the complete buffer as one SQL statement]&quot;. Per ulteriori informazioni, consulta la [documentazione di DbVisualizer](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsingExecuteBuffer).

## Passaggi successivi

Una volta letto questo documento, avrai una chiara comprensione dei blocchi anonimi e della loro struttura. Per ulteriori informazioni sulla scrittura delle query, leggere la [guida all&#39;esecuzione delle query](../best-practices/writing-queries.md).

Per aumentare l&#39;efficienza delle query, è inoltre necessario leggere le [modalità di utilizzo dei blocchi anonimi con il modello di struttura del caricamento incrementale](./incremental-load.md).
