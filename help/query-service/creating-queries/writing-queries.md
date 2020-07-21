---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Scrittura di query
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---


# Guida generale per l&#39;esecuzione delle query in [!DNL Query Service]

In questo documento sono riportati dettagli importanti da conoscere durante la scrittura di query in  Adobe Experience Platform [!DNL Query Service].

Per informazioni dettagliate sulla sintassi SQL utilizzata in [!DNL Query Service], consultate la documentazione [sulla sintassi](../sql/syntax.md)SQL.

## Modelli di esecuzione delle query

 Adobe Experience Platform [!DNL Query Service] dispone di due modelli di esecuzione delle query: interattivo e non interattivo. L&#39;esecuzione interattiva viene utilizzata per lo sviluppo di query e la generazione di report in strumenti di business intelligence, mentre quella non interattiva viene utilizzata per processi e query operative più grandi come parte di un flusso di lavoro di elaborazione dati.

### Esecuzione di query interattive

Le query possono essere eseguite in modo interattivo inviandole tramite l&#39; [!DNL Query Service] interfaccia utente o [tramite un client](../clients/overview.md)connesso. Quando si esegue [!DNL Query Service] attraverso un client connesso, una sessione attiva viene eseguita tra il client e [!DNL Query Service] fino a quando la query inviata non viene restituita o non scade.

L&#39;esecuzione della query interattiva presenta le seguenti limitazioni:

| Parametro | Limitazione |
| --------- | ---------- |
| Timeout query | 10 minuti |
| Numero massimo di righe restituite | 50.000 |
| Numero massimo di query simultanee | 5 |

>[!NOTE]
>
>Per ignorare il limite massimo di righe, includi `LIMIT 0` nella query. È ancora valido il timeout della query di 10 minuti.

Per impostazione predefinita, i risultati delle query interattive vengono restituiti al client e **non** sono persistenti. Per mantenere i risultati come dataset in [!DNL Experience Platform], la query deve utilizzare la `CREATE TABLE AS SELECT` sintassi.

### Esecuzione query non interattiva

Le query inviate tramite l&#39; [!DNL Query Service] API vengono eseguite in modo non interattivo. L’esecuzione non interattiva indica che [!DNL Query Service] riceve la chiamata API ed esegue la query nell’ordine in cui viene ricevuta. Le query non interattive generano sempre un nuovo dataset [!DNL Experience Platform] per ricevere i risultati, oppure l&#39;inserimento di nuove righe in un dataset esistente.

## Accesso a un campo specifico all&#39;interno di un oggetto

Per accedere a un campo all’interno di un oggetto della query, è possibile utilizzare la notazione del punto (`.`) o la notazione tra parentesi (`[]`). La seguente istruzione SQL utilizza la notazione del punto per scorrere l&#39; `endUserIds` oggetto verso il basso fino all&#39; `mcid` oggetto.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nome della tabella di analisi. |

L&#39;istruzione SQL seguente utilizza la notazione tra parentesi quadre per scorrere l&#39; `endUserIds` oggetto verso il basso fino all&#39; `mcid` oggetto.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nome della tabella di analisi. |

>[!NOTE]
>
>Poiché ogni tipo di notazione restituisce gli stessi risultati, quello che si sceglie di utilizzare dipende dalle preferenze.

Entrambe le query di esempio sopra restituiscono un oggetto appiattito, anziché un singolo valore:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

L&#39; `endUserIds._experience.mcid` oggetto restituito contiene i valori corrispondenti per i seguenti parametri:

- `id`
- `namespace`
- `primary`

Quando la colonna è dichiarata solo verso il basso, restituisce l&#39;intero oggetto come una stringa. Per visualizzare solo l’ID, utilizza:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Quando utilizzare virgolette singole, virgolette doppie e virgolette

Questa sezione spiega quando utilizzare virgolette singole, virgolette doppie e virgolette nelle query.

### Virgolette singole

Le virgolette singole (`'`) vengono utilizzate per creare stringhe di testo. Ad esempio, può essere utilizzato nell&#39; `SELECT` istruzione per restituire un valore di testo statico nel risultato e nella `WHERE` clausola per valutare il contenuto di una colonna.

La seguente query dichiara un valore di testo statico (`'datasetA'`) per una colonna:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

La seguente query utilizza una stringa (`'homepage'`) tra virgolette singole nella clausola WHERE per restituire gli eventi per una pagina specifica.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### Doppie virgolette

Le virgolette doppie (`"`) vengono utilizzate per dichiarare un identificatore con spazi.

La seguente query utilizza virgolette doppie per restituire valori da colonne specificate quando una colonna contiene uno spazio nel relativo identificatore:

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>Le virgolette doppie **non possono** essere utilizzate con l&#39;accesso al campo di notazione del punto.

### virgolette posteriori

Le virgolette posteriori `` ` `` vengono utilizzate per l&#39;escape dei nomi di colonna riservati **solo** quando si utilizza la sintassi della notazione del punto. Ad esempio, poiché `order` è una parola riservata in SQL, è necessario utilizzare le virgolette per accedere al campo `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Le virgolette posteriori sono utilizzate anche per accedere a un campo che inizia con un numero. Ad esempio, per accedere al campo `30_day_value`, è necessario utilizzare la notazione delle virgolette.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Le virgolette posteriori **non** sono necessarie se si utilizza la notazione tra parentesi.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Passaggi successivi

Leggendo questo documento, sono state introdotte alcune considerazioni importanti durante la scrittura di query tramite [!DNL Query Service]. Per ulteriori informazioni sull&#39;utilizzo della sintassi SQL per scrivere le proprie query, consultare la documentazione [sulla sintassi](../sql/syntax.md)SQL.