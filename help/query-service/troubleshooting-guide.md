---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;guida alla risoluzione dei problemi;FAQ;risoluzione dei problemi;
solution: Experience Platform
title: Guida alla risoluzione dei problemi del servizio query
topic-legacy: troubleshooting
description: Questo documento contiene informazioni sui codici di errore comuni riscontrati e sulle possibili cause.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 42288ae7db6fb19bc0a0ee8e4ecfa50b7d63d017
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 4%

---

# [!DNL Query Service] guida alla risoluzione dei problemi

Questo documento fornisce le risposte alle domande più frequenti sul servizio Query e fornisce un elenco di codici di errore visualizzati di frequente durante l’utilizzo del servizio Query. Per domande e risoluzione dei problemi relativi ad altri servizi in Adobe Experience Platform, consulta la [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

## Domande frequenti

Di seguito è riportato un elenco delle risposte alle domande più frequenti sul servizio query.

### Come posso ottenere solo i metadati per una query?

Per ottenere solo i metadati di una query, è possibile eseguire una query che restituisce zero righe, come segue:

```sql
SELECT * FROM <table> WHERE 1=0
```

Questa query restituisce solo i metadati della tabella specificata.

### Come posso iterare rapidamente una query CTAS (Crea tabella come selezione) senza materializzarla?

È possibile creare tabelle temporanee per eseguire rapidamente l’iterazione e l’esperimento su una query prima di materializzarla per l’utilizzo. È inoltre possibile utilizzare tabelle temporanee per convalidare il funzionamento di una query.

Ad esempio, puoi creare una tabella temporanea:

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

Quindi puoi utilizzare la tabella temporanea come segue:

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

### Come posso filtrare i dati della serie temporale?

Quando esegui una query con dati della serie temporale, utilizza il filtro della marca temporale quando possibile per un’analisi più accurata.

>[!NOTE]
>
> La stringa data **deve essere nel formato**.`yyyy-mm-ddTHH24:MM:SS`

Di seguito è riportato un esempio di utilizzo del filtro timestamp :

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

### È necessario utilizzare i caratteri jolly, ad esempio * per ottenere tutte le righe dai set di dati?

Non è possibile utilizzare i caratteri jolly per ottenere tutti i dati dalle righe, in quanto Query Service deve essere trattato come un **columnar-store** anziché come sistema di archiviazione tradizionale basato su righe.

### È necessario utilizzare `NOT IN` nella query SQL?

L&#39;operatore `NOT IN` viene spesso utilizzato per recuperare righe che non si trovano in un&#39;altra tabella o istruzione SQL. Questo operatore può rallentare le prestazioni e può restituire risultati imprevisti se le colonne confrontate accettano `NOT NULL` o se si dispone di un numero elevato di record.

Invece di utilizzare `NOT IN`, puoi utilizzare `NOT EXISTS` o `LEFT OUTER JOIN`.

Ad esempio, se sono state create le tabelle seguenti:

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Se utilizzi l’operatore `NOT EXISTS` , puoi replicare utilizzando l’operatore `NOT IN` utilizzando la seguente query:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

In alternativa, se utilizzi l’operatore `LEFT OUTER JOIN` , puoi replicare utilizzando l’operatore `NOT IN` utilizzando la seguente query:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

### Qual è l’utilizzo corretto degli operatori `OR` e `UNION`?

### Come posso utilizzare correttamente l&#39;operatore `CAST` per convertire i timestamp nelle query SQL?

Quando utilizzi l’operatore `CAST` per convertire una marca temporale, devi includere sia la data **che l’ora**.

Ad esempio, se manca il componente tempo , come illustrato di seguito, si verifica un errore:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

Di seguito viene illustrato l’utilizzo corretto dell’operatore `CAST`:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

## Errori API REST

| Codice di stato HTTP | Descrizione | Possibili cause |
| ---------------- | ----------- | --------------- |
| 400 | Richiesta errata | Query non valida |
| 401 | Autenticazione non riuscita | Token di autenticazione non valido |
| 500 | Errore interno del server | Errore interno del sistema |

## Errori API PostgreSQL

| Codice di errore | Stato connessione | Descrizione | Possibile causa |
| ---------- | ---------------- | ----------- | -------------- |
| **08P01** | N/D | Tipo di messaggio non supportato | Tipo di messaggio non supportato |
| **28P01** | Avvio - autenticazione | Password non valida | Token di autenticazione non valido |
| **28000** | Avvio - autenticazione | Tipo di autorizzazione non valido | Tipo di autorizzazione non valido. Deve essere `AuthenticationCleartextPassword`. |
| **42P12** | Avvio - autenticazione | Nessuna tabella trovata | Non sono state trovate tabelle da utilizzare |
| **42601** | Query | Errore di sintassi | Errore di comando o sintassi non valido |
| **42P01** | Query | Tabella non trovata | Impossibile trovare la tabella specificata nella query |
| **42P07** | Query | La tabella esiste | Esiste già una tabella con lo stesso nome (CREATE TABLE) |
| **53400** | Query | LIMITE supera il valore massimo | L&#39;utente ha specificato una clausola LIMIT superiore a 100.000 |
| **53400** | Query | Timeout dell&#39;istruzione | La dichiarazione in diretta ha richiesto più di 10 minuti al massimo |
| **58000** | Query | Errore di sistema | Errore interno del sistema |
| **0A000** | Query/Comando | Non supportati | Funzionalità/funzionalità nella query/comando non supportata |
| **42501** | Query DI TABELLA A DISCESA | Tabella di eliminazione non creata dal servizio query | La tabella che viene eliminata non è stata creata dal servizio query utilizzando l’istruzione `CREATE TABLE` |
| **42501** | Query DI TABELLA A DISCESA | Tabella non creata dall&#39;utente autenticato | La tabella da eliminare non è stata creata dall&#39;utente attualmente connesso |
| **42P01** | Query DI TABELLA A DISCESA | Tabella non trovata | Impossibile trovare la tabella specificata nella query |
| **42P12** | Query DI TABELLA A DISCESA | Nessuna tabella trovata per `dbName`: controlla il`dbName` | Impossibile trovare tabelle nel database corrente |
