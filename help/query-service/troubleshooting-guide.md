---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;guida alla risoluzione dei problemi;FAQ;risoluzione dei problemi;
solution: Experience Platform
title: Guida alla risoluzione dei problemi del servizio query
topic-legacy: troubleshooting
description: Questo documento contiene domande comuni e risposte relative al servizio query. Gli argomenti includono l'esportazione di dati, strumenti di terze parti ed errori PSQL.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 25953a5a1f5b32de7d150dbef700ad06ce6014df
workflow-type: tm+mt
source-wordcount: '3522'
ht-degree: 1%

---

# [!DNL Query Service] guida alla risoluzione dei problemi

Questo documento fornisce le risposte alle domande più frequenti sul servizio Query e fornisce un elenco di codici di errore visualizzati di frequente durante l’utilizzo del servizio Query. Per domande e risoluzione dei problemi relativi ad altri servizi in Adobe Experience Platform, fai riferimento alla [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

Il seguente elenco di risposte alle domande frequenti è suddiviso nelle seguenti categorie:

- [Generale](#general)
- [Esportazione dei dati](#exporting-data)
- [Strumenti di terze parti](#third-party-tools)
- [Errori API PostgreSQL](#postgresql-api-errors)
- [Errori API REST](#rest-api-errors)

## Domande generali sul servizio Query {#general}

Questa sezione include informazioni su prestazioni, limiti e processi.

### Posso disattivare la funzione di completamento automatico nell’editor del servizio query?

++ + N. risposta La disattivazione della funzione di completamento automatico non è attualmente supportata dall&#39;editor.
+++

### Perché a volte l’Editor query diventa lento quando scrivo una query?

+++Risposta Una possibile causa è la funzione di completamento automatico. La funzione elabora alcuni comandi di metadati che possono rallentare occasionalmente l’editor durante la modifica delle query.
+++

### Posso utilizzare Postman per l’API del servizio query?

+++Risposta Sì, puoi visualizzare e interagire con tutti i servizi API di Adobe utilizzando Postman (un’applicazione gratuita di terze parti). Guarda il [Guida alla configurazione del postman](https://video.tv.adobe.com/v/28832) istruzioni dettagliate su come impostare un progetto in Adobe Developer Console e acquisire tutte le credenziali necessarie per l’utilizzo con Postman. Consulta la documentazione ufficiale per [indicazioni sull’avvio, l’esecuzione e la condivisione delle raccolte Postman](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### Esiste un limite al numero massimo di righe restituite da una query tramite l’interfaccia utente?

+++Risposta Sì, Query Service applica internamente un limite di 50.000 righe a meno che non venga specificato un limite esplicito all’esterno. Consulta le linee guida [esecuzione di query interattive](./best-practices/writing-queries.md#interactive-query-execution) per ulteriori dettagli.
+++

### Esiste un limite di dimensione dei dati per l&#39;output risultante da una query?

++ + N. risposta Non esiste un limite alla dimensione dei dati, ma esiste un limite di timeout della query di 10 minuti da una sessione interattiva. Se la query viene eseguita come CTAS batch, non è applicabile un timeout di 10 minuti. Consulta le linee guida [esecuzione di query interattive](./best-practices/writing-queries.md#interactive-query-execution) per ulteriori dettagli.
+++

### Come posso ignorare il limite del numero di righe di output da una query SELECT?

+++Risposta Per ignorare il limite di righe di output, applicare &quot;LIMIT 0&quot; nella query. Esempio:

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### Come posso evitare che le mie query scadano in 10 minuti?

+++Risposta Si consiglia una o più delle seguenti soluzioni in caso di timeout delle query.

- [Convertire la query in una query CTAS](./sql/syntax.md#create-table-as-select) e pianificare l&#39;esecuzione. La pianificazione di un&#39;esecuzione può essere eseguita [tramite l’interfaccia utente](./ui/user-guide.md#scheduled-queries) o [API](./api/scheduled-queries.md#create).
- Esegui la query su un blocco dati più piccolo applicando ulteriori [condizioni di filtro](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [Esegui il comando EXPLAIN](./sql/syntax.md#explain) per raccogliere ulteriori dettagli.
- Esamina le statistiche dei dati all’interno del set di dati.
- Convertire la query in un modulo semplificato ed eseguirla nuovamente utilizzando [dichiarazioni preparate](./sql/prepared-statements.md).
+++

### Se vengono eseguite più query contemporaneamente, si verifica un problema o un impatto sulle prestazioni del servizio query?

++ + N. risposta Query Service ha una funzionalità di scalabilità automatica che garantisce che le query simultanee non abbiano alcun impatto significativo sulle prestazioni del servizio.
+++

### Come si trova un nome di colonna da un set di dati gerarchico?

+++Risposta I passaggi seguenti descrivono come visualizzare una visualizzazione a tabella di un set di dati tramite l’interfaccia utente, inclusi tutti i campi e le colonne nidificati in un modulo appiattito.

- Dopo aver effettuato l’accesso all’Experience Platform, seleziona **[!UICONTROL Set di dati]** nella navigazione a sinistra dell’interfaccia utente per passare a [!UICONTROL Set di dati] dashboard.
- Set di dati [!UICONTROL Sfoglia] viene visualizzata la scheda . Puoi usare la barra di ricerca per perfezionare le opzioni disponibili. Seleziona un set di dati dall’elenco visualizzato.

![Un set di dati evidenziato nell’interfaccia utente di Platform.](./images/troubleshooting/dataset-selection.png)

- La [!UICONTROL Attività set di dati] viene visualizzata la schermata . Seleziona [!UICONTROL Anteprima set di dati] per aprire una finestra di dialogo dello schema XDM e una visualizzazione tabulare dei dati appiattiti dal set di dati selezionato. Maggiori dettagli sono disponibili nella sezione [visualizzare in anteprima la documentazione del set di dati](../catalog/datasets/user-guide.md#preview-a-dataset)

![Lo schema XDM e la visualizzazione tabulare dei dati appiattiti.](./images/troubleshooting/dataset-preview.png)

- Seleziona un campo qualsiasi dallo schema per visualizzarne il contenuto in una colonna appiattita. Il nome della colonna viene visualizzato sopra il relativo contenuto sul lato destro della pagina. È necessario copiare questo nome da utilizzare per eseguire query su questo set di dati.

![Il nome della colonna di un set di dati nidificato evidenziato nell’interfaccia utente.](./images/troubleshooting/column-name.png)

Consulta la documentazione per maggiori informazioni [come utilizzare le strutture dati nidificate](./best-practices/nested-data-structures.md) utilizzando l’editor delle query o un client di terze parti.
+++

### Come velocizzare una query su un set di dati che contiene array?

+++Risposta Per migliorare le prestazioni delle query sui set di dati contenenti array, è necessario [esplodere la matrice](https://spark.apache.org/docs/latest/api/sql/index.html#explode) come [Query CTAS](./sql/syntax.md#create-table-as-select) in fase di esecuzione, quindi esploralo ulteriormente per le opportunità di migliorare il tempo di elaborazione.
+++

### Perché la mia query CTAS viene ancora elaborata dopo molte ore solo per un numero limitato di righe?

+++Risposta Se la query richiede molto tempo su un set di dati molto piccolo, contatta l’assistenza clienti.

È possibile che una query sia bloccata durante l’elaborazione per diversi motivi. Per determinare la causa esatta è necessaria un&#39;analisi approfondita caso per caso. [Contattare l&#39;assistenza clienti di Adobe](#customer-support) a questo processo.
+++

### Come posso contattare l&#39;assistenza clienti Adobe? {#customer-support}

+++Risposta
[Elenco completo dei numeri di telefono dell&#39;assistenza clienti Adobi](https://helpx.adobe.com/ca/contact/phone.html) è disponibile nella pagina della guida di Adobe. In alternativa, puoi trovare la guida online completando i seguenti passaggi:

- Passa a [https://www.adobe.com/](https://www.adobe.com/) nel browser web.
- Sul lato destro della barra di navigazione superiore, seleziona **[!UICONTROL Accesso]**.

![Adobe del sito web con accesso evidenziato.](./images/troubleshooting/adobe-sign-in.png)

- Utilizza il tuo Adobe ID e la password registrati con la tua licenza di Adobe.
- Seleziona **[!UICONTROL Aiuto e supporto]** dalla barra di navigazione superiore.

![Menu a discesa della barra di navigazione superiore con aiuto e supporto evidenziato.](./images/troubleshooting/help-and-support.png)

Viene visualizzato un banner a discesa contenente un [!UICONTROL Aiuto e supporto] sezione . Seleziona **[!UICONTROL Contattaci]** per aprire Adobe Customer Care Virtual Assistant o selezionare **[!UICONTROL Supporto aziendale]** per un aiuto dedicato alle grandi organizzazioni.
+++

### Come si implementa una serie sequenziale di processi senza eseguire i processi successivi se il processo precedente non viene completato correttamente?

+++Risposta La funzione blocco anonimo consente di catena di una o più istruzioni SQL eseguite in sequenza. Essi consentono inoltre la possibilità di gestire le eccezioni.

Consulta la sezione [documentazione relativa al blocco anonimo](./best-practices/anonymous-block.md) per ulteriori dettagli.
+++

### Come si implementa l’attribuzione personalizzata in Query Service?

+++Risposta Esistono due modi per implementare l’attribuzione personalizzata:

1. Utilizza una combinazione di [Funzioni definite dall&#39;Adobe](./sql/adobe-defined-functions.md) per identificare se le esigenze del caso d’uso sono soddisfatte.
1. Se il suggerimento precedente non soddisfa il caso d’uso, è necessario utilizzare una combinazione di [funzioni della finestra](./sql/adobe-defined-functions.md#window-functions). Le funzioni finestra visualizzano tutti gli eventi in una sequenza. Consentono inoltre di rivedere i dati storici e possono essere utilizzati in qualsiasi combinazione.
+++

### Posso modellare le mie query in modo da poterle facilmente riutilizzare?

+++Risposta Sì, è possibile modellare le query utilizzando le istruzioni preparate. Le istruzioni preparate possono ottimizzare le prestazioni ed evitare di ripetere ripetutamente l’analisi di una query. Consulta la sezione [documentazione preparata delle dichiarazioni](./sql/prepared-statements.md) per ulteriori dettagli.
+++

### Come posso recuperare i registri degli errori per una query? {#error-logs}

+++Risposta Per recuperare i registri degli errori per una query specifica, è innanzitutto necessario utilizzare l’API del servizio query per recuperare i dettagli del registro delle query. La risposta HTTP contiene gli ID della query necessari per indagare un errore di query.

Utilizzare il comando GET per recuperare più query. Le informazioni su come effettuare una chiamata all’API sono disponibili nella sezione [documentazione di esempio sulle chiamate API](./api/queries.md#sample-api-calls).

Dalla risposta, identifica la query da esaminare ed effettua un’altra richiesta di GET utilizzando la relativa `id` valore. Le istruzioni complete sono disponibili nella sezione [recuperare una query per documentazione ID](./api/queries.md#retrieve-a-query-by-id).

Una risposta corretta restituisce lo stato HTTP 200 e contiene il `errors` array. La risposta è stata abbreviata per brevità.

```json
{
    "isInsertInto": false,
    "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
    "clientId": "8c2455819a624534bb665c43c3759877",
    "state": "SUCCESS",
    "rowCount": 0,
    "errors": [{
      'code': '58000', 
      'message': 'Batch query execution gets : [failed reason ErrorCode: 58000 Batch query execution gets : [Analysis error encountered. Reason: [sessionId: f055dc73-1fbd-4c9c-8645-efa609da0a7b Function [varchar] not defined.]]]', 
      'errorType': 'USER_ERROR'
      }],
    "isCTAS": false,
    "version": 1,
    "id": "343388b0-e0dd-4227-a75b-7fc945ef408a",
}
```

La [Documentazione di riferimento API del servizio query](https://www.adobe.io/experience-platform-apis/references/query-service/) fornisce ulteriori informazioni su tutti gli endpoint disponibili.
+++

### Che cosa significa &quot;Errore di convalida dello schema&quot;?

+++Risposta Il messaggio &quot;Errore di convalida dello schema&quot; indica che il sistema non è in grado di individuare un campo all&#39;interno dello schema. Leggere il documento sulle best practice per [organizzazione delle risorse dati in Query Service](./best-practices/organize-data-assets.md) seguito da [Crea tabella come selezione della documentazione](./sql/syntax.md#create-table-as-select).

L&#39;esempio seguente illustra l&#39;utilizzo di una sintassi CTAS e di un tipo di dati struct:

```sql
CREATE TABLE table_name WITH (SCHEMA='schema_name')

AS SELECT '1' as _id,

 STRUCT

  ('2021-02-17T15:39:29.0Z' AS taskActualCompletionDate,

    '2020-09-09T21:21:16.0Z' AS taskActualStartDate,

    'Consulting' AS taskdescription,

    '5f6527c10011e09b89666c52d9a8c564' AS taskguide,

    'Stakeholder Consulting Engagement' AS taskname, 

    '2020-09-09T15:00:00.0Z' AS taskPlannedStartDate,

    '2021-02-15T11:00:00.0Z' AS taskPlannedCompletionDate

  ) AS _workfront ;
```

+++

### Come posso elaborare rapidamente i nuovi dati che entrano nel sistema ogni giorno?

+++Risposta [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) può essere utilizzato per leggere in modo incrementale i dati su una tabella basata su un ID snapshot. Questa funzione è ideale per l&#39;utilizzo con [carico incrementale](./best-practices/incremental-load.md) pattern di progettazione che elabora solo le informazioni nel set di dati creato o modificato dall’ultima esecuzione del caricamento. Di conseguenza, aumenta l’efficienza dell’elaborazione e può essere utilizzata sia con l’elaborazione in streaming che con quella in batch.
+++

### Perché c&#39;è una differenza tra i numeri mostrati nell&#39;interfaccia utente del profilo e i numeri calcolati dal set di dati di esportazione del profilo?

+++Risposta I numeri visualizzati nel dashboard del profilo sono accurati a partire dall&#39;ultima istantanea. I numeri generati nella tabella di esportazione del profilo dipendono interamente dalla query di esportazione. Di conseguenza, l’esecuzione di query sul numero di profili idonei per un particolare segmento è una causa comune di questa discrepanza.

>[!NOTE]
>
>La query include i dati storici, mentre l’interfaccia utente visualizza solo i dati di profilo correnti.

+++

### Perché la mia query ha restituito un sottoinsieme vuoto e cosa devo fare?

+++Risposta La causa più probabile è che la query è troppo limitata nell&#39;ambito. È necessario rimuovere sistematicamente una sezione del `WHERE` fino a quando non si iniziano a vedere alcuni dati.

Puoi anche confermare che il set di dati contiene dati utilizzando una piccola query come:

```sql
SELECT count(1) FROM myTableName
```

+++

### Posso campionare i miei dati?

+++Risposta Questa funzione è attualmente in corso di elaborazione. I dettagli saranno disponibili in [note sulla versione](../release-notes/latest/latest.md) e tramite le finestre di dialogo dell’interfaccia utente di Platform una volta che la funzione è pronta per il rilascio.
+++

### Quali funzioni helper sono supportate da Query Service?

+++Risposta Query Service fornisce diverse funzioni integrate di supporto SQL per estendere le funzionalità SQL. Consulta il documento per un elenco completo delle [Funzioni SQL supportate da Query Service](./sql/spark-sql-functions.md).
+++

### Cosa devo fare se la query pianificata non riesce?

+++Risposta prima, controlla i registri per scoprire i dettagli dell’errore. La sezione Domande frequenti su [ricerca di errori nei registri](#error-logs) fornisce ulteriori informazioni su come eseguire questa operazione.

È inoltre necessario consultare la documentazione per informazioni su come eseguire [query pianificate nell’interfaccia utente](./ui/user-guide.md#scheduled-queries) e [API](./api/scheduled-queries.md).

Di seguito è riportato un elenco di considerazioni per le query pianificate quando si utilizza il [!DNL Query Editor]. Non si applicano al [!DNL Query Service] API:<br/>È possibile aggiungere una pianificazione solo a una query già creata, salvata ed eseguita.<br/>You **impossibile** aggiungi una pianificazione a una query con parametri.<br/>Query pianificate **impossibile** contiene un blocco anonimo.<br/>È possibile pianificare solo **uno** modello di query utilizzando l’interfaccia utente. Se desideri aggiungere ulteriori pianificazioni a un modello di query, dovrai utilizzare l’API . Se una pianificazione è già stata aggiunta utilizzando l’API , non potrai aggiungere altre pianificazioni utilizzando l’interfaccia utente .
+++

### Cosa significa l’errore &quot;Limite di sessione raggiunto&quot;?

+++Risposta &quot;Limite sessione raggiunto&quot; significa che è stato raggiunto il numero massimo di sessioni del servizio query consentite per la tua organizzazione. Connettiti all’amministratore Adobe Experience Platform della tua organizzazione.
+++

### In che modo il registro query gestisce le query relative a un set di dati eliminato?

+++Risposta Query Service non elimina mai la cronologia delle query. Ciò significa che qualsiasi query che fa riferimento a un set di dati eliminato restituirà &quot;Nessun set di dati valido&quot; come risultato.
+++

### Come posso ottenere solo i metadati per una query?

+++Risposta È possibile eseguire una query che restituisce zero righe per ottenere solo i metadati nella risposta. Questa query di esempio restituisce solo i metadati della tabella specificata.

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### Come posso iterare rapidamente una query CTAS (Crea tabella come selezione) senza materializzarla?

+++Risposta È possibile creare tabelle temporanee per eseguire rapidamente l&#39;iterazione e la sperimentazione su una query prima di materializzarla per l&#39;utilizzo. È inoltre possibile utilizzare tabelle temporanee per convalidare il funzionamento di una query.

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

+++

### Come posso cambiare il fuso orario in e da una marca temporale UTC?

+++Risposta Adobe Experience Platform persiste i dati nel formato timestamp UTC (Coordinated Universal Time). Un esempio del formato UTC è `2021-12-22T19:52:05Z`

Query Service supporta funzioni SQL integrate per convertire una data marca temporale in e dal formato UTC. Entrambi i `to_utc_timestamp()` e `from_utc_timestamp()` i metodi richiedono due parametri: marca temporale e fuso orario.

| Parametro | Descrizione |
|-----------|---------------|
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

#### Converti dalla marca temporale UTC

La `from_utc_timestamp()` interpreta i parametri indicati **dalla marca temporale del fuso orario locale** e fornisce la marca temporale equivalente della regione desiderata in formato UTC. Nell’esempio seguente, l’ora è 2:40 nel fuso orario locale dell’utente. Il fuso orario di Seoul passato come variabile è nove ore prima del fuso orario locale.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

La query restituisce una marca temporale in formato UTC per il fuso orario passato come parametro. Il risultato è nove ore prima del fuso orario in cui è stata eseguita la query.

```
8/31/2021, 11:40 PM
```

### Come posso filtrare i dati della serie temporale?

+++Risposta Quando esegui una query con dati della serie temporale, utilizza il filtro della marca temporale ogni volta che è possibile per un’analisi più accurata.

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

+++

### Come si utilizza correttamente il `CAST` per convertire i timestamp nelle query SQL?

+++Risposta quando si utilizza il `CAST` per convertire una marca temporale, è necessario includere sia la data **e** tempo.

Ad esempio, se manca il componente tempo , come illustrato di seguito, si verifica un errore:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

L&#39;uso corretto del `CAST` l’operatore è mostrato di seguito:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### È necessario utilizzare i caratteri jolly, ad esempio * per ottenere tutte le righe dai set di dati?

+++Risposta Non è possibile utilizzare i caratteri jolly per ottenere tutti i dati dalle righe, in quanto Query Service deve essere trattato come un **columnar-store** piuttosto che un sistema di archiviazione tradizionale basato su righe.
+++

### Dovrei utilizzare `NOT IN` nella query SQL?

+++Risposta `NOT IN` viene spesso utilizzato per recuperare righe che non si trovano in un&#39;altra tabella o istruzione SQL. Questo operatore può rallentare le prestazioni e può restituire risultati imprevisti se le colonne confrontate accettano `NOT NULL`oppure hai un gran numero di documenti.

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

+++

## Esportazione dei dati {#exporting-data}

Questa sezione fornisce informazioni sull’esportazione di dati e limiti.

### Esiste un modo per estrarre i dati da Query Service dopo l’elaborazione delle query e salvare i risultati in un file CSV? {#export-csv}

++ + Risposta Sì. I dati possono essere estratti da Query Service e c&#39;è anche l&#39;opzione per memorizzare i risultati in formato CSV tramite un comando SQL.

Esistono due modi per salvare i risultati di una query quando si utilizza un client PSQL. È possibile utilizzare `COPY TO` creare un&#39;istruzione utilizzando il formato seguente:

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[Orientamenti sull&#39;uso `COPY TO` command](./sql/syntax.md#copy) può essere trovato nella documentazione di riferimento della sintassi SQL.
+++

### Posso estrarre il contenuto del set di dati finale che è stato acquisito tramite le query CTAS (supponendo che si tratti di quantità maggiori di dati come Terabytes)?

++ + N. risposta Al momento non è disponibile alcuna funzione per l’estrazione dei dati acquisiti.
+++

## Strumenti di terze parti {#third-party-tools}

Questa sezione include informazioni sull&#39;utilizzo di strumenti di terze parti come PSQL e Power BI.

### Posso collegare Query Service a uno strumento di terze parti?

+++Risposta Sì, è possibile collegare più client desktop di terze parti a Query Service. Consulta la documentazione per [informazioni complete sui client disponibili e su come collegarli al servizio Query](./clients/overview.md).
+++

### Esiste un modo per collegare Query Service una volta per un utilizzo continuo con uno strumento di terze parti?

+++Risposta Sì, i client desktop di terze parti possono essere collegati a Query Service tramite una configurazione unica di credenziali non in scadenza. Le credenziali non in scadenza possono essere generate da un utente autorizzato e le riceveranno in un file JSON scaricato sul computer locale. Completo [istruzioni su come creare e scaricare credenziali non in scadenza](./ui/credentials.md#non-expiring-credentials) si trova nella documentazione.
+++

### Che tipo di editor SQL di terze parti posso collegare a Query Service Editor?

+++Risposta Qualsiasi editor SQL di terze parti PSQL o [!DNL Postgres] È possibile collegare l’editor del servizio query al client. Consulta la documentazione per [connessione dei client a Query Service](./clients/overview.md) per un elenco delle istruzioni disponibili.
+++

### Posso collegare lo strumento Power BI a Query Service?

+++Risposta Sì, è possibile collegare Power BI a Query Service. Consulta la documentazione per [istruzioni sulla connessione dell’app desktop Power BI al servizio query](./clients/power-bi.md).
+++

### Perché il caricamento delle dashboard richiede molto tempo quando sono connesse al servizio query?

+++Risposta Quando il sistema è connesso a Query Service, è connesso a un motore di elaborazione interattivo o batch. Questo può comportare tempi di caricamento più lunghi per riflettere i dati elaborati.

Se desideri migliorare i tempi di risposta per le dashboard, implementa un server di Business Intelligence (BI) come livello di memorizzazione in cache tra gli strumenti Query Service e BI. In genere, la maggior parte degli strumenti BI presenta un’offerta aggiuntiva per un server.

Lo scopo di aggiungere il livello del server cache è quello di memorizzare in cache i dati da Query Service e utilizzare lo stesso per le dashboard per velocizzare la risposta. Ciò è possibile in quanto i risultati per le query eseguite vengono memorizzati nella cache del server BI ogni giorno. Il server di caching distribuisce quindi questi risultati per qualsiasi utente con la stessa query per ridurre la latenza. Fare riferimento alla documentazione dell&#39;utilità o dello strumento di terze parti utilizzato per i chiarimenti su questa configurazione.
+++

### È possibile accedere a Query Service utilizzando lo strumento di connessione pgAdmin?

+++Risposta No, la connettività pgAdmin non è supportata. A [elenco dei client di terze parti disponibili e istruzioni su come collegarli a Query Service](./clients/overview.md) si trova nella documentazione.
+++

## Errori API PostgreSQL {#postgresql-api-errors}

Nella tabella seguente sono riportati i codici di errore PSQL e le relative possibili cause.

| Codice di errore | Stato connessione | Descrizione | Possibile causa |
|------------|---------------------------|-------------|----------------|
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

### Perché ho ricevuto un codice di errore 58000 quando si utilizza il metodo history_meta() sulla mia tabella?

+++Risposta `history_meta()` viene utilizzato per accedere a uno snapshot da un set di dati. In precedenza, se si eseguiva una query su un set di dati vuoto in Azure Data Lake Storage (ADLS), si riceveva un codice di errore 58000 che indica che il set di dati non esiste. Di seguito è riportato un esempio del vecchio errore di sistema.

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

Errore. Nessun valore restituito per la query. Questo comportamento è stato corretto per restituire il seguente messaggio:

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## Errori API REST {#rest-api-errors}

La tabella seguente fornisce i codici di errore HTTP e le relative possibili cause.

| Codice di stato HTTP | Descrizione | Possibili cause |
|------------------|-----------------------|----------------------------|
| 400 | Richiesta errata | Query non valida |
| 401 | Autenticazione non riuscita | Token di autenticazione non valido |
| 500 | Errore interno del server | Errore interno del sistema |
