---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;guida alla risoluzione dei problemi;faq;risoluzione dei problemi;
solution: Experience Platform
title: Domande frequenti
description: Questo documento contiene domande e risposte comuni relative a Query Service. Gli argomenti includono esportazione di dati, strumenti di terze parti ed errori PSQL.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '4425'
ht-degree: 0%

---

# Domande frequenti

Questo documento fornisce le risposte alle domande più frequenti su Query Service e fornisce un elenco dei codici di errore più comuni durante l’utilizzo di Query Service. Per domande e risoluzione dei problemi relativi ad altri servizi in Adobe Experience Platform, consulta [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

Il seguente elenco di risposte alle domande frequenti è suddiviso nelle seguenti categorie:

- [Generale](#general)
- [Esportazione dei dati](#exporting-data)
- [Strumenti di terze parti](#third-party-tools)
- [Errori API PostgreSQL](#postgresql-api-errors)
- [Errori REST API](#rest-api-errors)

## Domande generali su Query Service {#general}

Questa sezione include informazioni su prestazioni, limiti e processi.

### È possibile disattivare la funzione di completamento automatico nell’editor di Query Service?

+++Risposta n. La disattivazione della funzione di completamento automatico non è attualmente supportata dall’editor.
+++

### Perché l&#39;editor di query a volte diventa lento quando si digita una query?

+++Risposta Una possibile causa è la funzione di completamento automatico. La funzione elabora alcuni comandi di metadati che possono occasionalmente rallentare l’editor durante la modifica delle query.
+++

### Posso utilizzare [!DNL Postman] per l’API Query Service?

+++Risposta Sì, puoi visualizzare e interagire con tutti i servizi API di Adobe utilizzando [!DNL Postman] (applicazione gratuita di terze parti). Osserva [[!DNL Postman] guida alla configurazione](https://video.tv.adobe.com/v/28832) per istruzioni dettagliate su come impostare un progetto in Adobe Developer Console e acquisire tutte le credenziali necessarie per l’utilizzo con [!DNL Postman]. Consulta la documentazione ufficiale per [istruzioni su avvio, esecuzione e condivisione [!DNL Postman] raccolte](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### Esiste un limite al numero massimo di righe restituite da una query tramite l’interfaccia utente?

+++Risposta Sì, Query Service applica internamente un limite di 50.000 righe, a meno che non venga specificato esternamente un limite esplicito. Consulta la guida su [esecuzione di query interattive](./best-practices/writing-queries.md#interactive-query-execution) per ulteriori dettagli.
+++

### È possibile utilizzare le query per aggiornare le righe?

+++Risposta Nelle query batch, l’aggiornamento di una riga all’interno del set di dati non è supportato.
+++

### Esiste un limite di dimensione dei dati per l’output risultante da una query?

+++Risposta n. Non vi è alcun limite alla dimensione dei dati, ma esiste un limite di timeout della query di 10 minuti da una sessione interattiva. Se la query viene eseguita come CTAS batch, non è applicabile un timeout di 10 minuti. Consulta la guida su [esecuzione di query interattive](./best-practices/writing-queries.md#interactive-query-execution) per ulteriori dettagli.
+++

### Come si aggira il limite del numero di righe di output da una query SELECT?

+++Risposta Per ignorare il limite di righe di output, applicare &quot;LIMIT 0&quot; nella query. Ad esempio:

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### Come posso evitare che le query scadano in 10 minuti?

+++Risposta Una o più delle seguenti soluzioni sono consigliate in caso di timeout delle query.

- [Convertire la query in una query CTAS](./sql/syntax.md#create-table-as-select) e pianifica l’esecuzione. La pianificazione di un’esecuzione può essere eseguita [tramite l’interfaccia utente](./ui/user-guide.md#scheduled-queries) o [API](./api/scheduled-queries.md#create).
- Eseguire la query su un blocco di dati più piccolo applicando ulteriori [condizioni del filtro](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [Esegui il comando EXPLAIN](./sql/syntax.md#explain) per raccogliere ulteriori dettagli.
- Esamina le statistiche dei dati all’interno del set di dati.
- Converti la query in una forma semplificata ed esegui di nuovo utilizzando [istruzioni preparate](./sql/prepared-statements.md).
+++

### Se vengono eseguite più query contemporaneamente, si verificano problemi o un impatto sulle prestazioni di Query Service?

+++Risposta n. Query Service dispone di una funzionalità di scalabilità automatica che garantisce che le query simultanee non abbiano alcun impatto rilevante sulle prestazioni del servizio.
+++

### È possibile utilizzare parole chiave riservate come nome di colonna?

+++Risposta Esistono alcune parole chiave riservate che non possono essere utilizzate come nome di colonna, ad esempio, `ORDER`, `GROUP BY`, `WHERE`, `DISTINCT`. Se desideri utilizzare queste parole chiave, devi eseguire l’escape di queste colonne.
+++

### Come si trova un nome di colonna da un set di dati gerarchico?

+++Risposta Nei passaggi seguenti viene descritto come visualizzare una visualizzazione tabulare di un set di dati tramite l’interfaccia utente, inclusi tutti i campi e le colonne nidificati in un modulo appiattito.

- Dopo aver effettuato l’accesso a Experienci Platform, seleziona **[!UICONTROL Set di dati]** nel menu di navigazione a sinistra dell’interfaccia utente per passare a [!UICONTROL Set di dati] dashboard.
- I set di dati [!UICONTROL Sfoglia] viene visualizzata la scheda. Puoi utilizzare la barra di ricerca per perfezionare le opzioni disponibili. Seleziona un set di dati dall’elenco visualizzato.

![Il dashboard Set di dati nell’interfaccia utente di Platform, con la barra di ricerca e un set di dati evidenziati.](./images/troubleshooting/dataset-selection.png)

- Il [!UICONTROL Attività set di dati] viene visualizzata la schermata. Seleziona **[!UICONTROL Anteprima set di dati]** per aprire una finestra di dialogo dello schema XDM e della vista a tabella dei dati appiattiti dal set di dati selezionato. Ulteriori dettagli sono disponibili nella sezione [visualizzare in anteprima la documentazione di un set di dati](../catalog/datasets/user-guide.md#preview-a-dataset)

![Scheda Attività set di dati del dashboard Set di dati con Anteprima set di dati evidenziata.](./images/troubleshooting/dataset-preview.png)

- Seleziona un campo dello schema per visualizzarne il contenuto in una colonna appiattita. Il nome della colonna viene visualizzato sopra il suo contenuto sul lato destro della pagina. È necessario copiare questo nome da utilizzare per eseguire query su questo set di dati.

![Lo schema XDM e la vista a tabella dei dati appiattiti. Il nome della colonna di un set di dati nidificato viene evidenziato nell’interfaccia utente.](./images/troubleshooting/column-name.png)

Consulta la documentazione per istruzioni complete su [come utilizzare le strutture di dati nidificate](./key-concepts/nested-data-structures.md) utilizzando Query Editor o un client di terze parti.
+++

### Come velocizzare una query su un set di dati contenente array?

+++Risposta Per migliorare le prestazioni delle query su set di dati contenenti array, è necessario [esplodere l’array](https://spark.apache.org/docs/latest/api/sql/index.html#explode) as a [Query CTAS](./sql/syntax.md#create-table-as-select) in fase di esecuzione, quindi esplorala ulteriormente per scoprire le opportunità di migliorare il tempo di elaborazione.
+++

### Perché la query CTAS viene ancora elaborata dopo molte ore solo per un numero limitato di righe?

+++Risposta Se la query ha richiesto molto tempo su un set di dati molto piccolo, contatta l’assistenza clienti.

Un’interrogazione può essere bloccata durante l’elaborazione per diversi motivi. Per determinare la causa esatta è necessaria un’analisi approfondita caso per caso. [Contatta l’assistenza clienti Adobe](#customer-support) ad essere questo processo.
+++

### Come posso contattare l’assistenza clienti Adobe? {#customer-support}

+++Risposta
[Un elenco completo dei numeri di telefono dell’assistenza clienti Adobe](https://helpx.adobe.com/ca/contact/phone.html) è disponibile nella guida di Adobe. In alternativa, è possibile trovare la guida online completando i passaggi seguenti:

- Accedi a [https://www.adobe.com/](https://www.adobe.com/it/) nel browser.
- Sul lato destro della barra di navigazione superiore, seleziona **[!UICONTROL Accedi]**.

![Il sito web di Adobe con l’opzione Accedi evidenziata.](./images/troubleshooting/adobe-sign-in.png)

- Utilizza l’Adobe ID e la password registrati con la tua licenza di Adobe.
- Seleziona **[!UICONTROL Guida e supporto]** dalla barra di navigazione superiore.

![Menu a discesa della barra di navigazione superiore con Guida e supporto tecnico, Supporto Enterprise e Contattaci evidenziati.](./images/troubleshooting/help-and-support.png)

Viene visualizzato un banner a discesa contenente [!UICONTROL Guida e supporto] sezione. Seleziona **[!UICONTROL Contattaci]** per aprire l’Assistente virtuale dell’Assistenza clienti di Adobe, oppure seleziona **[!UICONTROL Supporto Enterprise]** per assistenza dedicata alle grandi organizzazioni.
+++

### Come si implementa una serie sequenziale di job senza eseguire i job successivi se il job precedente non viene completato correttamente?

+++Risposta La funzione di blocco anonimo consente di concatenare una o più istruzioni SQL eseguite in sequenza. Consentono inoltre di gestire le eccezioni.

Consulta la [documentazione di blocco anonimo](./key-concepts/anonymous-block.md) per ulteriori dettagli.
+++

### Come si implementa l’attribuzione personalizzata in Query Service?

+++Risposta Esistono due modi per implementare l’attribuzione personalizzata:

1. Utilizza una combinazione di [Funzioni definite da Adobe](./sql/adobe-defined-functions.md) per identificare se le esigenze del caso d’uso sono soddisfatte.
1. Se il suggerimento precedente non soddisfa il tuo caso d’uso, utilizza una combinazione di [funzioni finestra](./sql/adobe-defined-functions.md#window-functions). Le funzioni di finestra esaminano tutti gli eventi in una sequenza. Consentono inoltre di rivedere i dati storici e possono essere utilizzati in qualsiasi combinazione.
+++

### Posso modellare le mie query in modo da poterle riutilizzare facilmente?

+++Risposta Sì, è possibile modellare le query tramite l&#39;utilizzo di istruzioni preparate. Le istruzioni preparate possono ottimizzare le prestazioni ed evitare di rianalizzare ripetutamente una query. Consulta la [documentazione delle dichiarazioni preparate](./sql/prepared-statements.md) per ulteriori dettagli.
+++

### Come si recuperano i registri di errore per una query? {#error-logs}

+++Risposta Per recuperare i log degli errori per una query specifica, è necessario innanzitutto utilizzare l&#39;API Query Service per recuperare i dettagli del log delle query. La risposta HTTP contiene gli ID query necessari per individuare un errore di query.

Utilizzare il comando GET per recuperare più query. Le informazioni su come effettuare una chiamata all&#39;API sono disponibili nella sezione [Esempio di documentazione sulle chiamate API](./api/queries.md#sample-api-calls).

Dalla risposta, identifica la query da esaminare e invia un’altra richiesta di GET utilizzando il relativo `id` valore. Le istruzioni complete sono reperibili nella sezione [recuperare una query per documentazione ID](./api/queries.md#retrieve-a-query-by-id).

Una risposta corretta restituisce lo stato HTTP 200 e contiene `errors` array. La risposta è stata ridotta per brevità.

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

Il [Documentazione di riferimento API di Query Service](https://www.adobe.io/experience-platform-apis/references/query-service/) fornisce ulteriori informazioni su tutti gli endpoint disponibili.
+++

### Cosa significa &quot;Errore durante la convalida dello schema&quot;?

+++Risposta Il messaggio &quot;Errore durante la convalida dello schema&quot; indica che il sistema non è in grado di individuare un campo all&#39;interno dello schema. È necessario leggere il documento sulle best practice per [organizzazione delle risorse dati in Query Service](./best-practices/organize-data-assets.md) seguito da [Documentazione di Crea tabella come selezione](./sql/syntax.md#create-table-as-select).

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

+++Rispondi [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) può essere utilizzata per leggere in modo incrementale i dati su una tabella basata su un ID snapshot. Questa funzione è ideale per l&#39;utilizzo con [carico incrementale](./key-concepts/incremental-load.md) modello di progettazione che elabora solo le informazioni nel set di dati creato o modificato dopo l’ultima esecuzione del caricamento. Di conseguenza, aumenta l’efficienza di elaborazione e può essere utilizzato sia con l’elaborazione dei dati in streaming che in batch.
+++

### Perché esiste una differenza tra i numeri visualizzati nell’interfaccia utente del profilo e i numeri calcolati dal set di dati di esportazione del profilo?

+++Risposta I numeri visualizzati nel dashboard dei profili sono accurati all&#39;ultima istantanea. I numeri generati nella tabella di esportazione del profilo dipendono interamente dalla query di esportazione. Di conseguenza, l’esecuzione di query sul numero di profili idonei per un determinato pubblico è una causa comune di questa discrepanza.

>[!NOTE]
>
>La query include dati storici, mentre l’interfaccia utente visualizza solo i dati di profilo correnti.

+++

### Perché la query ha restituito un sottoinsieme vuoto e cosa devo fare?

+++Risposta La causa più probabile è che l&#39;ambito della query è troppo limitato. È necessario rimuovere sistematicamente una sezione del `WHERE` finché non si iniziano a visualizzare alcuni dati.

Puoi anche verificare che il set di dati contenga dati utilizzando una piccola query come:

```sql
SELECT count(1) FROM myTableName
```

+++

### Posso campionare i miei dati?

+++Risposta Questa funzione è attualmente in corso di elaborazione. I dettagli saranno resi disponibili in [note sulla versione](../release-notes/latest/latest.md) e nelle finestre di dialogo dell’interfaccia utente di Platform quando la funzione è pronta per il rilascio.
+++

### Quali funzioni di assistenza sono supportate da Query Service?

+++Answer Query Service fornisce diverse funzioni di assistenza SQL integrate per estendere le funzionalità SQL. Consulta il documento per un elenco completo [Funzioni SQL supportate da Query Service](./sql/spark-sql-functions.md).
+++

### Sono tutti nativi [!DNL Spark SQL] funzioni supportate o utenti limitati solo al wrapper [!DNL Spark SQL] le funzioni fornite da Adobe?

+++Risposta non ancora disponibile, non tutte open-source [!DNL Spark SQL] Le funzioni sono state testate sui dati del data lake. Una volta testate e confermate, verranno aggiunte all’elenco delle supportate. Fare riferimento al [elenco di supportate [!DNL Spark SQL] funzioni](./sql/spark-sql-functions.md) per verificare la presenza di una funzione specifica.
+++

### Gli utenti possono definire le proprie funzioni definite dall&#39;utente (FDU) che possono essere utilizzate in altre query?

+++Risposta A causa di considerazioni sulla sicurezza dei dati, la definizione personalizzata di FDU non è consentita.
+++

### Cosa devo fare se la query pianificata non riesce?

+++Rispondi prima, controlla i registri per individuare i dettagli dell’errore. La sezione delle domande frequenti su [ricerca di errori nei registri](#error-logs) fornisce ulteriori informazioni su come eseguire questa operazione.

Consulta anche la documentazione per istruzioni su come eseguire [query pianificate nell’interfaccia utente](./ui/user-guide.md#scheduled-queries) e attraverso [l’API](./api/scheduled-queries.md).

Tieni presente che quando utilizzi [!DNL Query Editor] è possibile aggiungere una pianificazione solo a una query già creata e salvata. Questo non si applica al [!DNL Query Service] API.
+++

### Cosa significa l’errore &quot;Limite di sessione raggiunto&quot;?

+++La risposta &quot;Limite sessione raggiunto&quot; indica che è stato raggiunto il numero massimo di sessioni di Query Service consentite per la tua organizzazione. Stabilisci una connessione con l’amministratore Adobe Experience Platform della tua organizzazione.
+++

### In che modo il registro delle query gestisce le query relative a un set di dati eliminato?

+++Answer Query Service non elimina mai la cronologia delle query. Ciò significa che eventuali query che fanno riferimento a un set di dati eliminato restituirebbero come risultato &quot;Nessun set di dati valido&quot;.
+++

### Come posso ottenere solo i metadati per una query?

+++Risposta È possibile eseguire una query che restituisce zero righe per ottenere solo i metadati nella risposta. Questa query di esempio restituisce solo i metadati per la tabella specificata.

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### Come è possibile eseguire rapidamente l&#39;iterazione su una query CTAS (Create Table As Select) senza materializzarla?

+++Risposta È possibile creare tabelle temporanee per eseguire rapidamente l&#39;iterazione e la sperimentazione di una query prima di materializzarla per l&#39;utilizzo. È inoltre possibile utilizzare tabelle temporanee per verificare se una query funziona.

Ad esempio, puoi creare una tabella temporanea:

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

È quindi possibile utilizzare la tabella temporanea nel modo seguente:

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

### Come si modifica il fuso orario in e da un timestamp UTC?

+++Il Adobe Experience Platform delle risposte mantiene i dati nel formato timestamp UTC (Coordinated Universal Time). Un esempio del formato UTC è `2021-12-22T19:52:05Z`

Query Service supporta funzioni SQL incorporate per convertire un determinato timestamp in e dal formato UTC. Entrambe `to_utc_timestamp()` e `from_utc_timestamp()` i metodi richiedono due parametri: timestamp e timezone.

| Parametro | Descrizione |
|-----------|---------------|
| Marca temporale | Il timestamp può essere scritto in formato UTC o semplice `{year-month-day}` formato. Se non viene specificata un&#39;ora, il valore predefinito è la mezzanotte del mattino del giorno specificato. |
| Fuso orario | Il fuso orario è scritto in un `{continent/city})` formato. Deve essere uno dei codici di fuso orario riconosciuti presenti nella [database TZ di dominio pubblico](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### Converti in timestamp UTC

Il `to_utc_timestamp()` il metodo interpreta i parametri specificati e li converte **alla marca temporale del fuso orario locale** in formato UTC. Ad esempio, il fuso orario a Seul, Corea del Sud, è UTC/GMT +9 ore. Specificando un timestamp di sola data, il metodo utilizza il valore predefinito mezzanotte del mattino. La marca temporale e il fuso orario vengono convertiti in formato UTC dall’ora dell’area geografica a una marca temporale UTC dell’area locale.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

La query restituisce un timestamp nell’ora locale dell’utente. In questo caso sono le 15 del giorno prima, mentre Seoul è avanti di nove ore.

```
2021-08-30 15:00:00
```

Altro esempio: se la marca temporale specificata è `2021-07-14 12:40:00.0` per `Asia/Seoul` fuso orario, il timestamp UTC restituito sarebbe `2021-07-14 03:40:00.0`

L’output della console fornito nell’interfaccia utente di Query Service è un formato più leggibile:

```
8/30/2021, 3:00 PM
```

#### Converti dal timestamp UTC

Il `from_utc_timestamp()` il metodo interpreta i parametri specificati **dalla marca temporale del fuso orario locale** e fornisce la marca temporale equivalente della regione desiderata in formato UTC. Nell’esempio seguente, l’ora è le 14:40 nel fuso orario locale dell’utente. Il fuso orario di Seoul superato come variabile è di nove ore davanti al fuso orario locale.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

La query restituisce una marca temporale in formato UTC per il fuso orario passato come parametro. Il risultato è nove ore prima del fuso orario in cui è stata eseguita la query.

```
8/31/2021, 11:40 PM
```

### Come posso filtrare i dati delle serie temporali?

+++Risposta Quando si esegue una query con dati di serie temporali, è necessario utilizzare il filtro timestamp quando possibile per un’analisi più accurata.

>[!NOTE]
>
> La stringa della data **deve** essere nel formato `yyyy-mm-ddTHH24:MM:SS`.

Di seguito è riportato un esempio di utilizzo del filtro timestamp:

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

+++

### Come si utilizza correttamente il `CAST` per convertire i timestamp in query SQL?

+++Risposta quando si utilizza `CAST` per convertire una marca temporale, è necessario includere sia la data **e** tempo.

Ad esempio, la mancanza del componente tempo, come mostrato di seguito, genera un errore:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

L&#39;utilizzo corretto del `CAST` L&#39;operatore è mostrato di seguito:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### È necessario utilizzare caratteri jolly, ad esempio *, per ottenere tutte le righe dai set di dati?

+++Risposta Non è possibile utilizzare i caratteri jolly per ottenere tutti i dati dalle righe, in quanto Query Service deve essere considerato come un **columnar-store** anziché utilizzare un sistema tradizionale basato su file.
+++

### Devo utilizzare `NOT IN` nella query SQL?

+++Rispondi `NOT IN` L&#39;operatore viene spesso utilizzato per recuperare le righe non trovate in un&#39;altra tabella o istruzione SQL. Questo operatore può rallentare le prestazioni e può restituire risultati imprevisti se le colonne confrontate accettano `NOT NULL`o un numero elevato di record.

Invece di utilizzare `NOT IN`, è possibile utilizzare `NOT EXISTS` o `LEFT OUTER JOIN`.

Ad esempio, se sono state create le seguenti tabelle:

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Se utilizzi il `NOT EXISTS` , è possibile eseguire la replica utilizzando `NOT IN` mediante la seguente query:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

In alternativa, se utilizzi il `LEFT OUTER JOIN` , è possibile eseguire la replica utilizzando `NOT IN` mediante la seguente query:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### È possibile creare un set di dati utilizzando una query CTAS con un doppio nome di sottolineatura come quelli visualizzati nell’interfaccia utente? Ad esempio: `test_table_001`.

+++Risposta n., si tratta di una limitazione intenzionale in un Experience Platform che si applica a tutti i servizi Adobe, incluso Query Service. Un nome con due trattini bassi è accettabile come nome di schema e set di dati, ma il nome della tabella per il set di dati può contenere solo un singolo trattino basso.
+++

### Quante query simultanee è possibile eseguire alla volta?

+++Risposta Non esiste alcun limite di concorrenza per le query in quanto le query batch vengono eseguite come processi back-end. Tuttavia, è stato impostato un limite di timeout per le query di 24 ore.
+++

### Esiste un dashboard attività in cui è possibile visualizzare le attività e lo stato delle query?

+++Risposta Sono disponibili funzionalità di monitoraggio e di avviso per verificare le attività e gli stati delle query. Consulta la [Integrazione del registro di controllo di Query Service](./data-governance/audit-log-guide.md) e [registri di query](./ui/overview.md#log) documenti per ulteriori informazioni.
+++

### Esiste un modo per eseguire il rollback degli aggiornamenti? Ad esempio, in caso di errore o se alcuni calcoli devono essere riconfigurati durante la scrittura di dati in Platform, come deve essere gestito lo scenario?

+++Risposta Al momento, non sono supportati rollback o aggiornamenti di questo tipo.
+++

### Come si ottimizzano le query in Adobe Experience Platform?

+++Risposta Il sistema non dispone di indici in quanto non si tratta di un database ma dispone di altre ottimizzazioni associate all&#39;archivio dati. Per ottimizzare le query sono disponibili le seguenti opzioni:

- Un filtro basato sul tempo per i dati della serie temporale.
- Push-down ottimizzato per il tipo di dati struct.
- Ottimizzazione del push-down dei costi e della memoria per array e tipi di dati delle mappe.
- Elaborazione incrementale mediante snapshot.
- Un formato di dati persistente.
+++

### Gli accessi possono essere limitati ad alcuni aspetti di Query Service o si tratta di una soluzione &quot;tutto o niente&quot;?

+++Answer Query Service è una soluzione completa o nulla. Impossibile fornire l&#39;accesso parziale.
+++

### È possibile limitare i dati utilizzabili da Query Service o accedere semplicemente all’intero data lake di Adobe Experience Platform?

+++Risposta Sì, è possibile limitare la query ai set di dati con accesso in sola lettura.
+++

### Quali altre opzioni sono disponibili per limitare i dati a cui può accedere Query Service?

+++Risposta Esistono tre approcci per limitare l’accesso. Essi sono i seguenti:

- Utilizza le istruzioni SELECT only e concedi ai set di dati l’accesso in sola lettura. Inoltre, assegna l’autorizzazione per gestire le query.
- Utilizza le istruzioni SELECT/INSERT/CREATE e concedi l’accesso in scrittura ai set di dati. Inoltre, assegna l’autorizzazione di gestione della query.
- Utilizza un account di integrazione con i suggerimenti precedenti e assegna l’autorizzazione per l’integrazione della query.

+++

### Una volta che i dati sono stati restituiti da Query Service, vengono eseguiti alcuni controlli da parte di Platform per verificare che non siano stati restituiti dati protetti?

- Query Service supporta il controllo degli accessi basato su attributi. Puoi limitare l’accesso ai dati a livello di colonna/foglia e/o di struttura. Per ulteriori informazioni sul controllo degli accessi basato su attributi, consulta la documentazione.

### È possibile specificare una modalità SSL per la connessione a un client di terze parti? È possibile, ad esempio, utilizzare &quot;verify-full&quot; con Power BI?

+++Risposta Sì, sono supportate le modalità SSL. Consulta la [Documentazione sulle modalità SSL](./clients/ssl-modes.md) suddividendo le diverse modalità SSL disponibili e il livello di protezione che offrono.
+++

### Usiamo TLS 1.2 per tutte le connessioni dai client Power BI al servizio di query?

+++Risposta Sì. I dati in transito sono sempre conformi a HTTPS. La versione attualmente supportata è TLS1.2.
+++

### Una connessione effettuata sulla porta 80 utilizza ancora https?

+++Risposta Sì, una connessione effettuata sulla porta 80 utilizza ancora SSL. È inoltre possibile utilizzare la porta 5432.
+++

### Posso controllare l’accesso a set di dati e colonne specifici per una particolare connessione? Come si configura?

+++Risposta Sì, se configurato, viene applicato il controllo degli accessi basato su attributi. Consulta la [panoramica sul controllo degli accessi basato su attributi](../access-control/abac/overview.md) per ulteriori informazioni.
+++

### Query Service supporta il comando &quot;INSERT OVERWRITE INTO&quot;?

+++Risposta no, Query Service non supporta il comando &quot;INSERT OVERWRITE INTO&quot;.
+++

### Con quale frequenza vengono aggiornati i dati di utilizzo nel dashboard utilizzo licenze per le ore di calcolo di Data Distiller?

+++Risposta La dashboard sull&#39;utilizzo delle licenze per le ore del computer Data Distiller viene aggiornata quattro volte al giorno, ogni sei ore.
+++

### È possibile utilizzare il comando CREATE VIEW senza accedere a Data Distiller?

+++Risposta Sì, è possibile utilizzare `CREATE VIEW` senza accesso a Data Distiller. Questo comando fornisce una vista logica dei dati ma non li riscrive nel data lake.
+++

### È possibile utilizzare blocchi anonimi in DbVisualizer?

+++Risposta Sì. Tuttavia, alcuni client di terze parti, come DbVisualizer, potrebbero richiedere un identificatore separato prima e dopo un blocco SQL per indicare che una parte di uno script deve essere gestita come una singola istruzione. Ulteriori dettagli sono disponibili nella sezione [documentazione di blocco anonimo](./key-concepts/anonymous-block.md) o in [la documentazione ufficiale di DbVisualizer](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsinganSQLDialect).
+++

## Esportazione dei dati {#exporting-data}

Questa sezione fornisce informazioni sull’esportazione di dati e sui limiti.

### Esiste un modo per estrarre i dati da Query Service dopo l’elaborazione delle query e salvare i risultati in un file CSV? {#export-csv}

+++Risposta Sì. I dati possono essere estratti da Query Service ed è inoltre possibile memorizzare i risultati in formato CSV tramite un comando SQL.

Esistono due modi per salvare i risultati di una query quando si utilizza un client PSQL. È possibile utilizzare `COPY TO` o creare un&#39;istruzione utilizzando il seguente formato:

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[Linee guida sull&#39;uso del `COPY TO` comando](./sql/syntax.md#copy) possono essere trovate nella documentazione di riferimento della sintassi SQL.
+++

### Posso estrarre il contenuto del set di dati finale che è stato acquisito tramite query CTAS (supponendo che si tratti di quantità di dati più grandi, come Terabyte)?

+++Risposta n. Al momento non è disponibile alcuna funzione per l’estrazione dei dati acquisiti.
+++

### Perché il connettore dati di Analytics non restituisce dati?

+++Risposta Una causa comune per questo problema è la query di dati di serie temporali senza un filtro temporale. Ad esempio:

```sql
SELECT * FROM prod_table LIMIT 1;
```

Deve essere scritto come:

```sql
SELECT * FROM prod_table
WHERE
timestamp >= to_timestamp('2022-07-22')
and timestamp < to_timestamp('2022-07-23');
```

+++

## Strumenti di terze parti {#third-party-tools}

Questa sezione include informazioni sull’utilizzo di strumenti di terze parti come PSQL e Power BI.

### È possibile collegare Query Service a uno strumento di terze parti?

+++Risposta Sì, è possibile collegare più client desktop di terze parti a Query Service. Consulta la documentazione per [informazioni complete sui client disponibili e su come collegarli a Query Service](./clients/overview.md).
+++

### Esiste un modo per connettere Query Service una volta per un utilizzo continuo con uno strumento di terze parti?

+++Risposta Sì, i client desktop di terze parti possono essere collegati a Query Service tramite l’impostazione una tantum di credenziali senza scadenza. Le credenziali senza scadenza possono essere generate da un utente autorizzato e ricevute in un file JSON che viene scaricato automaticamente nel computer locale. Completo [istruzioni su come creare e scaricare credenziali senza scadenza](./ui/credentials.md#non-expiring-credentials) sono disponibili nella documentazione.
+++

### Perché le mie credenziali senza scadenza non funzionano?

+++Risposta Il valore per le credenziali senza scadenza è costituito dagli argomenti concatenati del `technicalAccountID` e `credential` preso dal file JSON di configurazione. Il valore della password è il seguente: `{{technicalAccountId}:{credential}}`.
Consulta la documentazione per ulteriori informazioni su come [connettersi ai client esterni con le credenziali](./ui/credentials.md#using-credentials-to-connect-to-external-clients).
+++

### Che tipo di editor SQL di terze parti è possibile connettere a Query Service Editor?

+++Rispondi a qualsiasi editor SQL di terze parti che sia PSQL o [!DNL Postgres] è possibile connettersi all’editor di Query Service con la compatibilità del client. Consulta la documentazione per [connessione dei client a Query Service](./clients/overview.md) per un elenco delle istruzioni disponibili.
+++

### È possibile collegare lo strumento Power BI a Query Service?

+++Risposta Sì, è possibile collegare Power BI a Query Service. Consulta la documentazione per [istruzioni per la connessione dell’app desktop Power BI a Query Service](./clients/power-bi.md).
+++

### Perché il caricamento delle dashboard richiede molto tempo quando si è connessi a Query Service?

+++Risposta Quando il sistema è connesso a Query Service, è connesso a un motore di elaborazione batch o interattivo. Questo può comportare tempi di caricamento più lunghi per riflettere i dati elaborati.

Se desideri migliorare i tempi di risposta per i dashboard, devi implementare un server di Business Intelligence (BI) come livello di caching tra gli strumenti Query Service e BI. In genere, la maggior parte degli strumenti di business intelligence dispone di un&#39;offerta aggiuntiva per un server.

Lo scopo dell’aggiunta del livello del server di cache è quello di memorizzare in cache i dati da Query Service e utilizzarli ugualmente per i dashboard per velocizzare la risposta. Ciò è possibile in quanto i risultati per le query eseguite verrebbero memorizzati nella cache del server di business intelligence ogni giorno. Il server di caching fornisce quindi questi risultati a tutti gli utenti con la stessa query per ridurre la latenza. Per ulteriori informazioni su questa configurazione, consulta la documentazione dell’utility o dello strumento di terze parti in uso.
+++

### È possibile accedere a Query Service utilizzando lo strumento di connessione pgAdmin?

+++Risposta n.: la connettività pgAdmin non è supportata. A [elenco dei client di terze parti disponibili e istruzioni su come collegarli a Query Service](./clients/overview.md) sono disponibili nella documentazione.
+++

## Errori API PostgreSQL {#postgresql-api-errors}

Nella tabella seguente sono riportati i codici di errore PSQL e le possibili cause.

| Codice errore | Stato della connessione | Descrizione | Possibile causa |
|------------|---------------------------|-------------|----------------|
| **08P01** | N/D | Tipo di messaggio non supportato | Tipo di messaggio non supportato |
| **28P01** | Avvio - Autenticazione | Password non valida | Token di autenticazione non valido |
| **28000** | Avvio - Autenticazione | Tipo di autorizzazione non valido | Tipo di autorizzazione non valido. Deve essere `AuthenticationCleartextPassword`. |
| **42P12** | Avvio - Autenticazione | Nessuna tabella trovata | Nessuna tabella trovata per l&#39;utilizzo |
| **42601** | Query | Errore di sintassi | Errore di comando o sintassi non valida |
| **42P01** | Query | Tabella non trovata | Impossibile trovare la tabella specificata nella query |
| **42P07** | Query | Tabella esistente | Esiste già una tabella con lo stesso nome (CREATE TABLE) |
| **53400** | Query | Il limite supera il valore massimo | L&#39;utente ha specificato una clausola LIMIT superiore a 100.000 |
| **53400** | Query | Timeout rendiconto | Il rendiconto live inviato ha richiesto più di 10 minuti |
| **58000** | Query | Errore di sistema | Guasto del sistema interno |
| **0A000** | Query/Comando | Non supportati | La funzionalità nella query o nel comando non è supportata |
| **42501** | DROP TABLE Query | Eliminazione della tabella non creata da Query Service | La tabella che viene eliminata non è stata creata da Query Service utilizzando `CREATE TABLE` dichiarazione |
| **42501** | DROP TABLE Query | Tabella non creata dall&#39;utente autenticato | La tabella in fase di eliminazione non è stata creata dall&#39;utente attualmente connesso |
| **42P01** | DROP TABLE Query | Tabella non trovata | Impossibile trovare la tabella specificata nella query |
| **42P12** | DROP TABLE Query | Nessuna tabella trovata per `dbName`: controlla la `dbName` | Nessuna tabella trovata nel database corrente |

### Perché è stato ricevuto un codice di errore 58000 quando si utilizza il metodo history_meta() nella tabella?

+++Rispondi `history_meta()` viene utilizzato per accedere a uno snapshot da un set di dati. In precedenza, se si eseguiva una query su un set di dati vuoto in Azure Data Lake Storage (ADLS), veniva visualizzato un codice di errore 58000 che indicava che il set di dati non esiste. Di seguito è riportato un esempio del precedente errore di sistema.

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

Questo errore si è verificato perché non è stato restituito alcun valore per la query. Questo comportamento è stato corretto per restituire il seguente messaggio:

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## Errori REST API {#rest-api-errors}

Nella tabella seguente sono riportati i codici di errore HTTP e le possibili cause.

| Codice di stato HTTP | Descrizione | Possibili cause |
|------------------|-----------------------|----------------------------|
| 400 | Richiesta non valida | Query non valida o non valida |
| 401 | Autenticazione non riuscita | Token di autenticazione non valido |
| 500 | Errore interno del server | Guasto del sistema interno |
