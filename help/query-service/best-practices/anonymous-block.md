---
title: Esempio di query di blocchi anonimi
description: 'Il blocco anonimo è una sintassi SQL supportata da Adobe Experience Platform Query Service, che consente di eseguire in modo efficiente una sequenza di query '
source-git-commit: dffa03d9ab8e26e2c99a359ae000022d6d469572
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Query di esempio per blocco Anonymous

Adobe Experience Platform Query Service supporta blocchi anonimi. La funzione blocco anonimo consente di catena di una o più istruzioni SQL eseguite in sequenza. Essi consentono inoltre la possibilità di gestire le eccezioni.

La funzione blocco anonimo è un modo efficiente per eseguire una sequenza di operazioni o query. La catena di query all’interno del blocco può essere salvata come modello e pianificata per l’esecuzione in un determinato momento o intervallo. Queste query possono essere utilizzate per scrivere e aggiungere dati per creare un nuovo set di dati e in genere vengono utilizzate quando si dispone di una dipendenza.

La tabella fornisce una suddivisione delle sezioni principali del blocco: esecuzione e gestione delle eccezioni. Le sezioni sono definite dalle parole chiave `BEGIN`, `END` e `EXCEPTION`.

| pagina | descrizione |
|---|---|
| esecuzione | Una sezione eseguibile inizia con la parola chiave `BEGIN` e termina con la parola chiave `END`. Qualsiasi set di istruzioni incluse nelle parole chiave `BEGIN` e `END` verrà eseguito in sequenza e assicura che le query successive non vengano eseguite fino al completamento della query precedente nella sequenza. |
| trattamento delle eccezioni | La sezione opzionale relativa alla gestione delle eccezioni inizia con la parola chiave `EXCEPTION`. Contiene il codice per rilevare e gestire le eccezioni in caso di errore di una qualsiasi delle istruzioni SQL nella sezione di esecuzione. Se una delle query non riesce, l&#39;intero blocco viene interrotto. |

Vale la pena notare che un blocco è un&#39;istruzione eseguibile e può quindi essere nidificato all&#39;interno di altri blocchi.

>[!NOTE]
>
> Si consiglia vivamente di sottoporre a test le query su set di dati più piccoli e assicurarsi che funzionino come previsto. Se una query ha un errore di sintassi, l&#39;eccezione verrà lanciata e l&#39;intero blocco verrà interrotto. Dopo aver verificato l’integrità delle query, è possibile iniziare a catena. In questo modo il blocco funziona come previsto prima di attivarlo.

## Query di blocco anonime di esempio

La seguente query mostra un esempio di concatenamento di istruzioni SQL. Per ulteriori informazioni sulla sintassi SQL utilizzata, vedere la sintassi [SQL nel documento Query Service](../sql/syntax.md) .

```SQL
$$BEGIN
     
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
     
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
     
END$$;
```

<!-- The block below uses `SET` to persist the result of a select query with a variable. It is used in the anonymous block to store the response from a query as a local variable for use with the `SNAPSHOT` feature. -->

Nell’esempio seguente, `SET` persiste il risultato di una query `SELECT` nella variabile locale specificata. La variabile viene limitata al blocco anonimo.

L&#39;ID dello snapshot viene memorizzato come variabile locale (`@current_sid`). Viene quindi utilizzato nella query successiva per restituire i risultati in base allo SNAPSHOT dello stesso set di dati/tabella.

Uno snapshot di database è una visualizzazione statica di sola lettura di un database SQL Server. Per ulteriori [informazioni sulla clausola snapshot](../sql/syntax.md#SNAPSHOT-clause), vedere la documentazione relativa alla sintassi SQL.

```SQL
$$BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                                     
END$$;
```

## Passaggi successivi

Leggendo questo documento, si ha ora una chiara comprensione dei blocchi anonimi e come sono strutturati. [Per ulteriori informazioni sull’esecuzione](./writing-queries.md) della query, consulta la guida sull’esecuzione della query in Query Service.

Per ulteriori esempi di query utilizzabili all’interno di Query Service, consulta le guide sulle query di esempio di [Adobe Analytics](./adobe-analytics.md), [query di esempio di Adobe Target](./adobe-target.md) o [query di esempio di ExperienceEvent](./experience-event-queries.md).
