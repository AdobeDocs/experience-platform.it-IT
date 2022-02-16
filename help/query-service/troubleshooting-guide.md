---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;guida alla risoluzione dei problemi;FAQ;risoluzione dei problemi;
solution: Experience Platform
title: Guida alla risoluzione dei problemi del servizio query
topic-legacy: troubleshooting
description: Questo documento contiene informazioni sui codici di errore comuni riscontrati e sulle possibili cause.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 03cd013e35872bcc30c68508d9418cb888d9e260
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 3%

---

# [!DNL Query Service] guida alla risoluzione dei problemi

Questo documento fornisce le risposte alle domande più frequenti sul servizio Query e fornisce un elenco di codici di errore visualizzati di frequente durante l’utilizzo del servizio Query. Per domande e risoluzione dei problemi relativi ad altri servizi in Adobe Experience Platform, fai riferimento alla [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

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

### Come posso cambiare il fuso orario in e da una marca temporale UTC?

Adobe Experience Platform persiste i dati nel formato di marca temporale UTC (Coordinated Universal Time). Un esempio del formato UTC è `2021-12-22T19:52:05Z`

Query Service supporta funzioni SQL integrate per convertire una data marca temporale in e dal formato UTC. Entrambi i `to_utc_timestamp()` e `from_utc_timestamp()` i metodi richiedono due parametri: marca temporale e fuso orario.

| Parametro | Descrizione |
|---|---|
| Marca temporale | La marca temporale può essere scritta in formato UTC o in formato semplice `{year-month-day}` formato. Se non viene fornito alcun orario, il valore predefinito è mezzanotte della mattina del giorno specificato. |
| Fuso orario | Il fuso orario viene scritto in un `{continent/city})` formato. Deve essere uno dei codici di fuso orario riconosciuti come trovato nella [database TZ di dominio pubblico](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### Converti in timestamp UTC

La `to_utc_timestamp()` interpreta i parametri specificati e li converte **alla marca temporale del fuso orario locale** in formato UTC. Ad esempio, il fuso orario a Seoul, Corea del Sud, è UTC/GMT +9 ore. Fornendo una marca temporale di sola data, il metodo utilizza un valore predefinito di mezzanotte della mattina. La marca temporale e il fuso orario vengono convertiti in formato UTC dall’ora di tale regione a una marca temporale UTC della propria area locale.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

La query restituisce una marca temporale nell’ora locale dell’utente. In questo caso, alle 15.00 del giorno precedente, mentre Seoul è in attesa di 9 ore.

```
2021-08-30 15:00:00
```

Un altro esempio, se la marca temporale è stata `2021-07-14 12:40:00.0` per `Asia/Seoul` fuso orario, la marca temporale UTC restituita sarà `2021-07-14 03:40:00.0`

L’output della console fornito nell’interfaccia utente del servizio query è un formato più leggibile dall’utente:

```
8/30/2021, 3:00 PM
```

### Converti dalla marca temporale UTC

La `from_utc_timestamp()` interpreta i parametri indicati **dalla marca temporale del fuso orario locale** e fornisce la marca temporale equivalente della regione desiderata in formato UTC. Nell’esempio seguente, l’ora è 2:40 nel fuso orario locale dell’utente. Il fuso orario di Seoul passato come variabile è nove ore prima del fuso orario locale.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

La query restituisce una marca temporale in formato UTC per il fuso orario passato come parametro. Il risultato è nove ore prima del fuso orario in cui è stata eseguita la query.

```
8/31/2021, 11:40 PM
```

### Come posso filtrare i dati della serie temporale?

Quando esegui una query con dati della serie temporale, utilizza il filtro della marca temporale quando possibile per un’analisi più accurata.

>[!NOTE]
>
> Stringa data **deve** nel formato `yyyy-mm-ddTHH24:MM:SS`.

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

Non è possibile utilizzare i caratteri jolly per ottenere tutti i dati dalle righe, in quanto Query Service deve essere trattato come **columnar-store** piuttosto che un sistema di archiviazione tradizionale basato su righe.

### Dovrei utilizzare `NOT IN` nella query SQL?

La `NOT IN` viene spesso utilizzato per recuperare righe che non si trovano in un&#39;altra tabella o istruzione SQL. Questo operatore può rallentare le prestazioni e può restituire risultati imprevisti se le colonne confrontate accettano `NOT NULL`oppure hai un gran numero di documenti.

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

Se utilizzi `NOT EXISTS` è possibile replicare utilizzando `NOT IN` utilizzando la seguente query:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

In alternativa, se utilizzi il `LEFT OUTER JOIN` è possibile replicare utilizzando `NOT IN` utilizzando la seguente query:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

### Qual è l’utilizzo corretto del `OR` e `UNION` operatori?

### Come si utilizza correttamente il `CAST` per convertire i timestamp nelle query SQL?

Quando utilizzi `CAST` per convertire una marca temporale, è necessario includere sia la data **e** tempo.

Ad esempio, se manca il componente tempo , come illustrato di seguito, si verifica un errore:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

Un uso corretto del `CAST` l’operatore è mostrato di seguito:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

### Come posso scaricare i risultati della query come file CSV?

Questa non è una funzione che Query Service offre direttamente. Tuttavia, se [!DNL PostgreSQL] il client utilizzato per connettersi al server di database ha la funzionalità , la risposta di una query SELECT può essere scritta e scaricata come file CSV. Fare riferimento alla documentazione dell&#39;utilità o dello strumento di terze parti utilizzato per i chiarimenti su questo processo.

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
| **42501** | Query DI TABELLA A DISCESA | Tabella di eliminazione non creata dal servizio query | La tabella da eliminare non è stata creata dal servizio query utilizzando `CREATE TABLE` dichiarazione |
| **42501** | Query DI TABELLA A DISCESA | Tabella non creata dall&#39;utente autenticato | La tabella da eliminare non è stata creata dall&#39;utente attualmente connesso |
| **42P01** | Query DI TABELLA A DISCESA | Tabella non trovata | Impossibile trovare la tabella specificata nella query |
| **42P12** | Query DI TABELLA A DISCESA | Nessuna tabella trovata per `dbName`: controlla `dbName` | Impossibile trovare tabelle nel database corrente |
