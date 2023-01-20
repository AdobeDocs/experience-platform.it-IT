---
title: Blocco anonimo nel servizio query
description: Il blocco anonimo è una sintassi SQL supportata da Adobe Experience Platform Query Service, che consente di eseguire in modo efficiente una sequenza di query
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Blocco anonimo nel servizio query

Adobe Experience Platform Query Service supporta blocchi anonimi. La funzione blocco anonimo consente di catena di una o più istruzioni SQL eseguite in sequenza. Essi consentono inoltre la possibilità di gestire le eccezioni.

La funzione blocco anonimo è un modo efficiente per eseguire una sequenza di operazioni o query. La catena di query all’interno del blocco può essere salvata come modello e pianificata per l’esecuzione in un determinato momento o intervallo. Queste query possono essere utilizzate per scrivere e aggiungere dati per creare un nuovo set di dati e in genere vengono utilizzate quando si dispone di una dipendenza.

>[!IMPORTANT]
>
>La pianificazione delle query tramite blocchi anonimi è attualmente possibile solo tramite [!DNL Query Service] API. Consulta la documentazione per [istruzioni complete sulla pianificazione delle query tramite API](../api/scheduled-queries.md).

La tabella fornisce una suddivisione delle sezioni principali del blocco: esecuzione e gestione delle eccezioni. Le sezioni sono definite dalle parole chiave `BEGIN`, `END`e `EXCEPTION`.

| pagina | descrizione |
|---|---|
| esecuzione | Una sezione eseguibile inizia con la parola chiave `BEGIN` e termina con la parola chiave `END`. Qualsiasi insieme di istruzioni incluse nella `BEGIN` e `END` le parole chiave vengono eseguite in sequenza e garantiscono che le query successive non vengano eseguite fino al completamento della query precedente nella sequenza. |
| trattamento delle eccezioni | La sezione opzionale di gestione delle eccezioni inizia con la parola chiave `EXCEPTION`. Contiene il codice per rilevare e gestire le eccezioni in caso di errore di una qualsiasi delle istruzioni SQL nella sezione di esecuzione. Se una delle query non riesce, l&#39;intero blocco viene interrotto. |

Vale la pena notare che un blocco è un&#39;istruzione eseguibile e può quindi essere nidificato all&#39;interno di altri blocchi.

>[!NOTE]
>
> Si consiglia vivamente di sottoporre a test le query su set di dati più piccoli e assicurarsi che funzionino come previsto. Se una query ha un errore di sintassi, l&#39;eccezione verrà lanciata e l&#39;intero blocco verrà interrotto. Dopo aver verificato l’integrità delle query, è possibile iniziare a catena. In questo modo il blocco funziona come previsto prima di attivarlo.

## Query di blocco anonime di esempio

La seguente query mostra un esempio di concatenamento di istruzioni SQL. Consulta la sezione [Sintassi SQL in Query Service](../sql/syntax.md) per ulteriori informazioni sulla sintassi SQL utilizzata.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

Nell’esempio seguente: `SET` persiste il risultato di un `SELECT` nella variabile locale specificata. La variabile viene limitata al blocco anonimo.

L&#39;ID dello snapshot viene memorizzato come variabile locale (`@current_sid`). Viene quindi utilizzato nella query successiva per restituire i risultati in base allo SNAPSHOT dello stesso set di dati/tabella.

Uno snapshot di database è una visualizzazione statica di sola lettura di un database SQL Server. Per ulteriori informazioni [informazioni sulla clausola snapshot](../sql/syntax.md#SNAPSHOT-clause) consultare la documentazione relativa alla sintassi SQL.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Passaggi successivi

Leggendo questo documento, si ha ora una chiara comprensione dei blocchi anonimi e come sono strutturati. [Per ulteriori informazioni sull’esecuzione delle query](../best-practices/writing-queries.md), leggi la guida sull’esecuzione della query in Query Service.

È inoltre necessario leggere [come viene utilizzato il blocco anonimo con il modello di progettazione del carico incrementale](./incremental-load.md) per aumentare l’efficienza delle query.
