---
title: Blocco anonimo in Query Service
description: Il blocco anonimo è una sintassi SQL supportata da Adobe Experience Platform Query Service che consente di eseguire in modo efficiente una sequenza di query
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Blocco anonimo in Query Service

Adobe Experience Platform Query Service supporta blocchi anonimi. La funzione di blocco anonimo consente di concatenare una o più istruzioni SQL eseguite in sequenza. Consentono inoltre di gestire le eccezioni.

La funzione di blocco anonimo rappresenta un modo efficiente per eseguire una sequenza di operazioni o query. La catena di query all’interno del blocco può essere salvata come modello e pianificata per l’esecuzione in un determinato momento o intervallo. Queste query possono essere utilizzate per scrivere e accodare dati per creare un nuovo set di dati e vengono in genere utilizzate nei casi in cui si dispone di una dipendenza.

>[!IMPORTANT]
>
>La pianificazione delle query tramite blocchi anonimi è attualmente possibile solo tramite [!DNL Query Service] API. Consulta la documentazione per [istruzioni complete sulla pianificazione delle query tramite l’API](../api/scheduled-queries.md).

La tabella fornisce un raggruppamento delle sezioni principali del blocco: esecuzione e gestione delle eccezioni. Le sezioni sono definite dalle parole chiave `BEGIN`, `END`, e `EXCEPTION`.

| pagina | descrizione |
|---|---|
| esecuzione | Una sezione eseguibile inizia con la parola chiave `BEGIN` e termina con la parola chiave `END`. Qualsiasi insieme di istruzioni incluso nel `BEGIN` e `END` le parole chiave vengono eseguite in sequenza e garantiscono che le query successive non vengano eseguite fino al completamento della query precedente nella sequenza. |
| gestione delle eccezioni | La sezione facoltativa per la gestione delle eccezioni inizia con la parola chiave `EXCEPTION`. Contiene il codice per intercettare e gestire le eccezioni in caso di errore di una qualsiasi delle istruzioni SQL nella sezione di esecuzione. Se una delle query ha esito negativo, l’intero blocco viene interrotto. |

È opportuno notare che un blocco è un’istruzione eseguibile e può pertanto essere nidificato all’interno di altri blocchi.

>[!NOTE]
>
> Si consiglia vivamente di testare le query su set di dati più piccoli e di assicurarsi che funzionino come previsto. Se una query presenta un errore di sintassi, verrà generata l’eccezione e l’intero blocco verrà interrotto. Dopo aver verificato l’integrità delle query, puoi iniziare a concatenarle. In questo modo il blocco funziona come previsto prima di metterlo in funzione.

## Query di blocco anonime di esempio

Nella query seguente viene illustrato un esempio di concatenamento di istruzioni SQL. Consulta la [Sintassi SQL in Query Service](../sql/syntax.md) per ulteriori informazioni sulla sintassi SQL utilizzata.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

Nell’esempio seguente, `SET` persiste il risultato di un `SELECT` query nella variabile locale specificata. La variabile ha l’ambito del blocco anonimo.

L&#39;ID snapshot viene memorizzato come variabile locale (`@current_sid`). Viene quindi utilizzato nella query successiva per restituire risultati basati sullo SNAPSHOT dello stesso set di dati/tabella.

Uno snapshot di database è una visualizzazione statica di sola lettura di un database di SQL Server. Per ulteriori informazioni [informazioni sulla clausola snapshot](../sql/syntax.md#SNAPSHOT-clause) consulta la documentazione sulla sintassi SQL.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Passaggi successivi

Una volta letto questo documento, avrai una chiara comprensione dei blocchi anonimi e della loro struttura. [Per ulteriori informazioni sull’esecuzione delle query](../best-practices/writing-queries.md), leggi la guida sull’esecuzione delle query in Query Service.

Leggi anche informazioni su [utilizzo del blocco anonimo con il modello di progettazione del caricamento incrementale](./incremental-load.md) per aumentare l’efficienza delle query.
