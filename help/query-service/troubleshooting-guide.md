---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;guida alla risoluzione dei problemi;FAQ;risoluzione dei problemi;
solution: Experience Platform
title: Guida alla risoluzione dei problemi del servizio query
topic-legacy: troubleshooting
description: Questo documento contiene informazioni sui codici di errore comuni riscontrati e sulle possibili cause.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: e3557fe75680153f051b8a864ad8f6aca5f743ee
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

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
WHERE timestamp >= To_timestamp('2021-01-21 12:00:00')
AND timestamp < To_timestamp('2021-01-21 13:00:00')
LIMIT 100;
```

### Come posso filtrare i dati della serie temporale?

Quando esegui una query con dati della serie temporale, utilizza il filtro della marca temporale quando possibile per un’analisi più accurata.

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

## Errori API REST

| Codice di stato HTTP | Descrizione | Possibili cause |
| ---------------- | ----------- | --------------- |
| 400 | Richiesta errata | Query non valida |
| 401 | Autenticazione non riuscita | Token di autenticazione non valido |
| 500 | Errore interno del server | Errore interno del sistema |

## Errori API PostgreSQL

| Codice di errore e stato di connessione | Descrizione | Possibile causa |
| ------------------------------- | ----------- | -------------- |
| **Start-up 28P01**  - autenticazione | Password non valida | Token di autenticazione non valido |
| **Start-up 28000**  - autenticazione | Tipo di autorizzazione non valido | Tipo di autorizzazione non valido. Deve essere `AuthenticationCleartextPassword`. |
| **42P12** Start-up - autenticazione | Nessuna tabella trovata | Non sono state trovate tabelle da utilizzare |
| **Query 42601**  | Errore di sintassi | Errore di comando o sintassi non valido |
| **Query 58000**  | Errore di sistema | Errore interno del sistema |
| **Query 42P01**  | Tabella non trovata | Impossibile trovare la tabella specificata nella query |
| **Query 42P07**  | La tabella esiste | La tabella esiste già con lo stesso nome (CREATE TABLE) |
| **Query 53400**  | LIMITE supera il valore massimo | L&#39;utente ha specificato una clausola LIMIT superiore a 100.000 |
| **Query 53400**  | Timeout dell&#39;istruzione | La dichiarazione in diretta ha richiesto più di 10 minuti al massimo |
| **08P01** N/D | Tipo di messaggio non supportato | Tipo di messaggio non supportato |
