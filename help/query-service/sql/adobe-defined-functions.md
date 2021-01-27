---
keywords: Experience Platform;home;popular topics;query service;Query service;adobe defined functions;sql;
solution: Experience Platform
title: ' funzioni definite dal Adobe'
topic: functions
description: Questo documento fornisce informazioni sulle funzioni definite dal Adobe  disponibili in Servizio query.
translation-type: tm+mt
source-git-commit: e15229601d35d1155fc9a8ab9296f8c41811ebf9
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 2%

---


#  funzioni definite dal Adobe

 funzioni definite dal Adobe, di seguito denominate ADF, sono funzioni preconfigurate in Adobe Experience Platform Query Service che consentono di eseguire le attività aziendali comuni sui dati [!DNL Experience Event]. Tra questi rientrano funzioni per [Sessionization](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) e [Attribution](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html) come quelle di  Adobe Analytics.

Questo documento fornisce informazioni  funzioni definite dal Adobe disponibili in [!DNL Query Service].

## Funzioni della finestra {#window-functions}

La maggior parte della logica di business richiede la raccolta dei punti di contatto per un cliente e l&#39;ordine per tempo. Questo supporto è fornito da [!DNL Spark] SQL sotto forma di funzioni finestra. Le funzioni finestra fanno parte di SQL standard e sono supportate da molti altri motori SQL.

Una funzione finestra aggiorna un&#39;aggregazione e restituisce un singolo elemento per ogni riga del sottoinsieme ordinato. La funzione di aggregazione di base è `SUM()`. `SUM()` prende le righe e le dà un totale. Se invece si applica `SUM()` a una finestra, trasformandola in una funzione finestra, si riceve una somma cumulativa con ogni riga.

La maggior parte degli assistenti [!DNL Spark] SQL sono funzioni finestra che aggiornano ogni riga nella finestra, con l&#39;aggiunta dello stato di tale riga.

**Sintassi query**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `{PARTITION}` | Un sottogruppo di righe basato su una colonna o su un campo disponibile. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | Colonna o campo disponibile utilizzato per ordinare il sottoinsieme o le righe. | `ORDER BY timestamp` |
| `{FRAME}` | Un sottogruppo delle righe in una partizione. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionizzazione

Quando si lavora con dati [!DNL Experience Event] provenienti da un sito Web, un&#39;applicazione mobile, un sistema di risposta vocale interattivo o qualsiasi altro canale di interazione con i clienti, è utile raggruppare gli eventi intorno a un periodo di attività correlato. In genere, l&#39;attività è guidata da un intento specifico, come la ricerca di un prodotto, il pagamento di una fattura, il controllo del saldo del conto, la compilazione di un&#39;applicazione e così via.

Questo raggruppamento, o sessionizzazione dei dati, consente di associare gli eventi per scoprire un contesto più ampio sull&#39;esperienza del cliente.

Per ulteriori informazioni sulla sessione in  Adobe Analytics, consultate la documentazione relativa alle [sessioni basate sul contesto](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html.

**Sintassi query**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo timestamp trovato nel set di dati. |
| `{EXPIRATION_IN_SECONDS}` | Il numero di secondi necessari tra gli eventi per qualificare la fine della sessione corrente e l&#39;inizio di una nuova sessione. |

Una spiegazione dei parametri all&#39;interno della funzione `OVER()` si trova nella sezione [funzioni finestra](#window-functions).

**Query di esempio**

```sql
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp,
  SESS_TIMEOUT(timestamp, 60 * 30)
    OVER (PARTITION BY endUserIds._experience.mcid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS session
FROM experience_events
ORDER BY id, timestamp ASC
LIMIT 10
```

**Risultati**

```console
                id                |       timestamp       |      session       
----------------------------------+-----------------------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | (40,1,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | (55,1,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | (1361821,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | (54,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | (49,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | (33,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | (31,2,false,5)
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `session`. La colonna `session` è composta dai seguenti componenti:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parametri | Descrizione |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | La differenza di tempo, in secondi, tra il record corrente e il record precedente. |
| `{NUM}` | Un numero di sessione univoco, a partire da 1, per la chiave definita in `PARTITION BY` della funzione finestra. |
| `{IS_NEW}` | Valore booleano utilizzato per identificare se un record è il primo di una sessione. |
| `{DEPTH}` | Profondità del record corrente all&#39;interno della sessione. |

### SESS_START_IF

Questa query restituisce lo stato della sessione per la riga corrente, in base alla marca temporale corrente e all&#39;espressione data, e avvia una nuova sessione con la riga corrente.

**Sintassi query**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo timestamp trovato nel set di dati. |
| `{TEST_EXPRESSION}` | Espressione con cui si desidera controllare i campi dei dati. Ad esempio, `application.launches > 0`. |

Una spiegazione dei parametri all&#39;interno della funzione `OVER()` si trova nella sezione [funzioni finestra](#window-functions).

**Query di esempio**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.launches.value > 0, true, false) AS isLaunch,
    SESS_START_IF(timestamp, application.launches.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Risultati**

```console
                id                |       timestamp       | isLaunch |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | true     | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | false    | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | true     | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `session`. La colonna `session` è composta dai seguenti componenti:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parametri | Descrizione |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | La differenza di tempo, in secondi, tra il record corrente e il record precedente. |
| `{NUM}` | Un numero di sessione univoco, a partire da 1, per la chiave definita in `PARTITION BY` della funzione finestra. |
| `{IS_NEW}` | Valore booleano utilizzato per identificare se un record è il primo di una sessione. |
| `{DEPTH}` | Profondità del record corrente all&#39;interno della sessione. |

### SESS_END_IF

Questa query restituisce lo stato della sessione per la riga corrente, in base alla marca temporale corrente e all&#39;espressione data, termina la sessione corrente e inizia una nuova sessione nella riga successiva.

**Sintassi query**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo timestamp trovato nel set di dati. |
| `{TEST_EXPRESSION}` | Espressione con cui si desidera controllare i campi dei dati. Ad esempio, `application.launches > 0`. |

Una spiegazione dei parametri all&#39;interno della funzione `OVER()` si trova nella sezione [funzioni finestra](#window-functions).

**Query di esempio**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.applicationCloses.value > 0 OR application.crashes.value > 0, true, false) AS isExit,
    SESS_END_IF(timestamp, application.applicationCloses.value > 0 OR application.crashes.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Risultati**

```console
                id                |       timestamp       | isExit   |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | false    | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | true     | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | false    | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `session`. La colonna `session` è composta dai seguenti componenti:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parametri | Descrizione |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | La differenza di tempo, in secondi, tra il record corrente e il record precedente. |
| `{NUM}` | Un numero di sessione univoco, a partire da 1, per la chiave definita in `PARTITION BY` della funzione finestra. |
| `{IS_NEW}` | Valore booleano utilizzato per identificare se un record è il primo di una sessione. |
| `{DEPTH}` | Profondità del record corrente all&#39;interno della sessione. |

## Attribution

Associare le azioni dei clienti al successo è una parte importante della comprensione dei fattori che influenzano le esperienze dei clienti. I seguenti file ADF supportano l’attribuzione di tipo primo tocco e ultimo tocco con diverse impostazioni di scadenza.

Per ulteriori informazioni sull&#39;attribuzione in  Adobe Analytics, vedere la [ Attribution IQ panoramica](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html) nella [!DNL Analytics] Guida del pannello Attribuzione.

### Attribuzione primo tocco

Questa query restituisce il valore di attribuzione del primo tocco e i dettagli per un singolo canale nel set di dati [!DNL Experience Event] di destinazione. La query restituisce un oggetto `struct` con il primo valore di tocco, marca temporale e attribuzione per ogni riga restituita per il canale selezionato.

Questa query è utile per visualizzare quale interazione ha portato a una serie di azioni da parte del cliente. Nell&#39;esempio riportato di seguito, il codice di tracciamento iniziale (`em:946426`) nei dati [!DNL Experience Event] è attribuito al 100% (`1.0`) della responsabilità per le azioni del cliente, in quanto si è trattato della prima interazione.

**Sintassi query**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo timestamp trovato nel set di dati. |
| `{CHANNEL_NAME}` | Etichetta per l&#39;oggetto restituito. |
| `{CHANNEL_VALUE}` | Colonna o campo che rappresenta il canale di destinazione per la query. |

Una spiegazione dei parametri all&#39;interno di `OVER()` si trova nella sezione [funzioni finestra](#window-functions).

**Query di esempio**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH(timestamp, 'Paid First', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
LIMIT 10
```

**Risultati**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:06:12.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:02.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:55.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:08:44.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:10.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:43.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:53:02.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:12.0 | sms:70175    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:57.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2019-01-02 19:41:38.0 | em:526702    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `first_touch`. La colonna `first_touch` è composta dai seguenti componenti:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, immesso come etichetta nell&#39;ADF. |
| `{VALUE}` | Il valore di `{CHANNEL_VALUE}` che è il primo tocco in [!DNL Experience Event] |
| `{TIMESTAMP}` | Il timestamp del [!DNL Experience Event] in cui si è verificato il primo tocco. |
| `{FRACTION}` | Attribuzione del primo tocco, espressa come frazione decimale. |

### Attribuzione last-touch

Questa query restituisce il valore di attribuzione dell&#39;ultimo tocco e i dettagli per un singolo canale nel set di dati [!DNL Experience Event] di destinazione. La query restituisce un oggetto `struct` con l&#39;ultimo valore di tocco, marca temporale e attribuzione per ogni riga restituita per il canale selezionato.

Questa query è utile per visualizzare l&#39;interazione finale in una serie di azioni cliente. Nell&#39;esempio riportato di seguito, il codice di tracciamento nell&#39;oggetto restituito è l&#39;ultima interazione in ciascun record [!DNL Experience Event]. A ciascun codice viene attribuita la responsabilità del 100% (`1.0`) per le azioni del cliente, in quanto si trattava dell&#39;ultima interazione.

**Sintassi query**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo timestamp trovato nel set di dati. |
| `{CHANNEL_NAME}` | Etichetta dell&#39;oggetto restituito. |
| `{CHANNEL_VALUE}` | Colonna o campo che rappresenta il canale di destinazione per la query. |

Una spiegazione dei parametri all&#39;interno di `OVER()` si trova nella sezione [funzioni finestra](#window-functions).

**Query di esempio**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'trackingCode', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Risultati**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:06:12.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:02.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:55.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:08:44.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:10.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:10.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:43.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:53:02.0 |              | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:12.0 | sms:70175    | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:57.0 |              | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-01-02 19:41:38.0 | em:526702    | (Paid Last,em:526702,2018-01-02 19:41:38.0,1.0)
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `last_touch`. La colonna `last_touch` è composta dai seguenti componenti:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametri | Descrizione |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, immesso come etichetta nell&#39;ADF. |
| `{VALUE}` | Il valore di `{CHANNEL_VALUE}` che è l&#39;ultimo tocco in [!DNL Experience Event] |
| `{TIMESTAMP}` | La marca temporale del [!DNL Experience Event] in cui è stato utilizzato il `channelValue`. |
| `{FRACTION}` | L&#39;attribuzione dell&#39;ultimo tocco, espressa come frazione decimale. |

### Attribuzione del primo tocco con condizione di scadenza

Questa query restituisce il valore di attribuzione del primo tocco e i dettagli per un singolo canale nel set di dati [!DNL Experience Event] di destinazione, con scadenza dopo o prima di una condizione. La query restituisce un oggetto `struct` con il primo valore di tocco, marca temporale e attribuzione per ogni riga restituita per il canale selezionato.

Questa query è utile se si desidera vedere quale interazione ha portato a una serie di azioni da parte del cliente all&#39;interno di una parte del [!DNL Experience Event] dataset determinata da una condizione di scelta. Nell&#39;esempio riportato di seguito, un acquisto viene registrato (`commerce.purchases.value IS NOT NULL`) in ciascuno dei quattro giorni mostrati nei risultati (15 luglio, 21, 23 e 29) e il codice di tracciamento iniziale in ogni giorno viene attribuito al 100% (`1.0`) la responsabilità delle azioni del cliente.

**Sintassi query**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo timestamp trovato nel set di dati. |
| `{CHANNEL_NAME}` | Etichetta per l&#39;oggetto restituito. |
| `{CHANNEL_VALUE}` | Colonna o campo che rappresenta il canale di destinazione per la query. |
| `{EXP_CONDITION}` | La condizione che determina il punto di scadenza del canale. |
| `{EXP_BEFORE}` | Valore booleano che indica se il canale scade prima o dopo la condizione specificata, `{EXP_CONDITION}`, è soddisfatto. Questo è attivato principalmente per le condizioni di scadenza di una sessione, per garantire che il primo tocco non sia selezionato da una sessione precedente. Per impostazione predefinita, questo valore è impostato su `false`. |

Una spiegazione dei parametri all&#39;interno della funzione `OVER()` si trova nella sezione [funzioni finestra](#window-functions).

**Query di esempio**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Risultati**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `first_touch`. La colonna `first_touch` è composta dai seguenti componenti:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametri | Descrizione |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, immesso come etichetta nell&#39;ADF. |
| `{VALUE}` | Il valore di `CHANNEL_VALUE}` che è il primo tocco nella [!DNL Experience Event], prima della `{EXP_CONDITION}`. |
| `{TIMESTAMP}` | Il timestamp del [!DNL Experience Event] in cui si è verificato il primo tocco. |
| `{FRACTION}` | Attribuzione del primo tocco, espressa come frazione decimale. |

### Attribuzione primo tocco con timeout di scadenza

Questa query restituisce il valore di attribuzione del primo tocco e i dettagli per un singolo canale nel set di dati [!DNL Experience Event] di destinazione per un periodo di tempo specificato. La query restituisce un oggetto `struct` con il primo valore di tocco, marca temporale e attribuzione per ogni riga restituita per il canale selezionato.

Questa query è utile se si desidera vedere quale interazione, entro un intervallo di tempo selezionato, ha portato a un&#39;azione del cliente. Nell&#39;esempio riportato di seguito, il primo tocco restituito per ogni azione del cliente è la prima interazione nei sette giorni precedenti (`expTimeout = 86400 * 7`).

**Specifiche**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo timestamp trovato nel set di dati. |
| `{CHANNEL_NAME}` | Etichetta per l&#39;oggetto restituito. |
| `{CHANNEL_VALUE}` | Colonna o campo che rappresenta il canale di destinazione per la query. |
| `{EXP_TIMEOUT}` | La finestra di tempo prima dell&#39;evento del canale, in secondi, in cui la query cerca un primo evento di tocco. |

Una spiegazione dei parametri all&#39;interno della funzione `OVER()` si trova nella sezione [funzioni finestra](#window-functions).

**Query di esempio**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, 'Paid First', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Risultati**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `first_touch`. La colonna `first_touch` è composta dai seguenti componenti:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametri | Descrizione |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, immesso come etichetta nell&#39;ADF. |
| `{VALUE}` | Il valore di `CHANNEL_VALUE}` che rappresenta il primo tocco entro l&#39;intervallo `{EXP_TIMEOUT}` specificato. |
| `{TIMESTAMP}` | Il timestamp del [!DNL Experience Event] in cui si è verificato il primo tocco. |
| `{FRACTION}` | Attribuzione del primo tocco, espressa come frazione decimale. |

### Attribuzione dell’ultimo tocco con condizione di scadenza

Questa query restituisce il valore di attribuzione dell&#39;ultimo tocco e i dettagli per un singolo canale nel set di dati [!DNL Experience Event] di destinazione, con scadenza dopo o prima di una condizione. La query restituisce un oggetto `struct` con l&#39;ultimo valore di tocco, marca temporale e attribuzione per ogni riga restituita per il canale selezionato.

Questa query è utile se si desidera visualizzare l&#39;ultima interazione in una serie di azioni cliente all&#39;interno di una parte del [!DNL Experience Event] dataset determinata da una condizione di scelta. Nell&#39;esempio riportato di seguito, un acquisto viene registrato (`commerce.purchases.value IS NOT NULL`) in ciascuno dei quattro giorni mostrati nei risultati (15 luglio, 21, 23 e 29) e l&#39;ultimo codice di tracciamento in ogni giorno è attribuito al 100% (`1.0`) la responsabilità delle azioni del cliente.

**Sintassi query**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo timestamp trovato nel set di dati. |
| `{CHANNEL_NAME}` | Etichetta per l&#39;oggetto restituito. |
| `{CHANNEL_VALUE}` | Colonna o campo che rappresenta il canale di destinazione per la query. |
| `{EXP_CONDITION}` | La condizione che determina il punto di scadenza del canale. |
| `{EXP_BEFORE}` | Valore booleano che indica se il canale scade prima o dopo la condizione specificata, `{EXP_CONDITION}`, è soddisfatto. Questo è attivato principalmente per le condizioni di scadenza di una sessione, per garantire che il primo tocco non sia selezionato da una sessione precedente. Per impostazione predefinita, questo valore è impostato su `false`. |

**Query di esempio**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, 'trackingCode', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Esempio di risultati**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 | em:550984    | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 | em:380097    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `last_touch`. La colonna `last_touch` è composta dai seguenti componenti:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametri | Descrizione |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, immesso come etichetta nell&#39;ADF. |
| `{VALUE}` | Il valore di `{CHANNEL_VALUE}` che è l&#39;ultimo tocco nella [!DNL Experience Event], prima della `{EXP_CONDITION}`. |
| `{TIMESTAMP}` | Il timestamp del [!DNL Experience Event] in cui si è verificato l&#39;ultimo tocco. |
| `{FRACTION}` | L&#39;attribuzione dell&#39;ultimo tocco, espressa come frazione decimale. |

### Attribuzione last-touch con timeout di scadenza

Questa query restituisce il valore dell&#39;attribuzione last-touch e i dettagli per un singolo canale nel set di dati [!DNL Experience Event] di destinazione per un periodo di tempo specificato. La query restituisce un oggetto `struct` con l&#39;ultimo valore di tocco, marca temporale e attribuzione per ogni riga restituita per il canale selezionato.

Questa query è utile se si desidera visualizzare l&#39;ultima interazione entro un intervallo di tempo selezionato. Nell&#39;esempio riportato di seguito, l&#39;ultimo tocco restituito per ogni azione del cliente è l&#39;interazione finale entro i sette giorni successivi (`expTimeout = 86400 * 7`).

**Sintassi query**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo timestamp trovato nel set di dati. |
| `{CHANNEL_NAME}` | Etichetta per l&#39;oggetto restituito |
| `{CHANNEL_VALUE}` | Colonna o campo che rappresenta il canale di destinazione per la query |
| `{EXP_TIMEOUT}` | La finestra di tempo dopo l’evento del canale, in secondi, in cui la query cerca un ultimo evento di tocco. |

Una spiegazione dei parametri all&#39;interno della funzione `OVER()` si trova nella sezione [funzioni finestra](#window-functions).

**Query di esempio**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, 'trackingCode', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Risultati**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `last_touch`. La colonna `last_touch` è composta dai seguenti componenti:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametri | Descrizione |
| ---------- | ----------- |
| `{NAME}` | La `{CHANNEL_NAME}`, immessa come etichetta nell&#39;ADF. |
| `{VALUE}` | Il valore di `{CHANNEL_VALUE}` che è l&#39;ultimo tocco entro l&#39;intervallo `{EXP_TIMEOUT}` specificato |
| `{TIMESTAMP}` | Il timestamp della [!DNL Experience Event] in cui si è verificato l&#39;ultimo tocco |
| `{FRACTION}` | L&#39;attribuzione dell&#39;ultimo tocco, espressa come frazione decimale. |

## Tracciatura percorso

I percorsi possono essere utilizzati per comprendere la profondità di coinvolgimento del cliente, per confermare che le fasi previste di un&#39;esperienza funzionano correttamente e per identificare potenziali punti critici che possono avere un impatto sul cliente.

Le seguenti ADF supportano la definizione di visualizzazioni di percorso dalle relazioni precedenti e successive. Potrete creare pagine precedenti e pagine successive, oppure scorrere più eventi per creare percorsi.

### Pagina precedente

Determina il valore precedente di un particolare campo a un numero definito di passi dall&#39;interno della finestra. Tenere presente nell&#39;esempio che la funzione `WINDOW` è configurata con un frame di `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` che imposta l&#39;ADF in modo da visualizzare la riga corrente e tutte le righe successive.

**Sintassi query**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{KEY}` | Colonna o campo dell’evento. |
| `{SHIFT}` | (Facoltativo) Il numero di eventi lontani dall&#39;evento corrente. Per impostazione predefinita, il valore è 1. |
| `{IGNORE_NULLS}` | (Facoltativo) Valore booleano che indica se i valori null `{KEY}` devono essere ignorati. Per impostazione predefinita, il valore è `false`. |

Una spiegazione dei parametri all&#39;interno della funzione `OVER()` si trova nella sezione [funzioni finestra](#window-functions).

**Query di esempio**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Risultati**

```console
                id                 |       timestamp       |                 name                |                    previous_page                    
-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Cart Details)
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `previous_page`. Il valore all&#39;interno della colonna `previous_page` è basato sulla `{KEY}` utilizzata nell&#39;ADF.

### Pagina successiva

Determina il valore successivo di un particolare campo a un numero definito di passi di distanza all&#39;interno della finestra. Tenere presente nell&#39;esempio che la funzione `WINDOW` è configurata con un frame di `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` che imposta l&#39;ADF in modo da visualizzare la riga corrente e tutte le righe successive.

**Sintassi query**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{KEY}` | Colonna o campo dell’evento. |
| `{SHIFT}` | (Facoltativo) Il numero di eventi lontani dall&#39;evento corrente. Per impostazione predefinita, il valore è 1. |
| `{IGNORE_NULLS}` | (Facoltativo) Valore booleano che indica se i valori null `{KEY}` devono essere ignorati. Per impostazione predefinita, il valore è `false`. |

Una spiegazione dei parametri all&#39;interno della funzione `OVER()` si trova nella sezione [funzioni finestra](#window-functions).

**Query di esempio**

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS next_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

**Risultati**

```console
                id                 |       timestamp       |                name                 |             previous_page             
-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Shopping Cart: Cart Details)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Shopping Cart: Shipping Information)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Billing Information)
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `previous_page`. Il valore all&#39;interno della colonna `previous_page` è basato sulla `{KEY}` utilizzata nell&#39;ADF.

## Intervallo di tempo

Il time-between consente di esplorare il comportamento latente dei clienti entro un determinato periodo di tempo prima o dopo l’evento.

### Tempo tra la corrispondenza precedente

Questa query restituisce un numero che rappresenta l&#39;unità di tempo dopo la visualizzazione dell&#39;evento corrispondente precedente. Se non è stato trovato alcun evento corrispondente, restituisce null.

**Sintassi query**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo marca temporale trovato nel set di dati popolato su tutti gli eventi. |
| `{EVENT_DEFINITION}` | L&#39;espressione per qualificare l&#39;evento precedente. |
| `{TIME_UNIT}` | Unità di uscita. Il valore possibile include giorni, ore, minuti e secondi. Per impostazione predefinita, il valore è secondi. |

Una spiegazione dei parametri all&#39;interno della funzione `OVER()` si trova nella sezione [funzioni finestra](#window-functions).

**Query di esempio**

```sql
SELECT 
  page_name,
  SUM (time_between_previous_match) / COUNT(page_name) as average_minutes_since_registration
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_PREVIOUS_MATCH(timestamp, web.webPageDetails.name='Account Registration|Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS time_between_previous_match
FROM experience_events
)
WHERE time_between_previous_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_since_registration
LIMIT 10
```

**Risultati**

```console
             page_name             | average_minutes_since_registration 
-----------------------------------+------------------------------------
                                   |                                   
 Account Registration|Confirmation |                                0.0
 Seasonal                          |                   5.47029702970297
 Equipment                         |                  6.532110091743119
 Women                             |                  7.287081339712919
 Men                               |                  7.640918580375783
 Product List                      |                  9.387459807073954
 Unlimited Blog|February           |                  9.954545454545455
 Product Details|Buffalo           |                 13.304347826086957
 Unlimited Blog|June               |                  770.4285714285714
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `average_minutes_since_registration`. Il valore all&#39;interno della colonna `average_minutes_since_registration` è la differenza di tempo tra gli eventi corrente e precedente. L&#39;unità di tempo è stata definita in precedenza in `{TIME_UNIT}`.

### Tempo tra la partita successiva

Questa query restituisce un numero negativo che rappresenta l&#39;unità di tempo dietro l&#39;evento corrispondente successivo. Se non viene trovato un evento corrispondente, viene restituito null.

**Sintassi query**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo marca temporale trovato nel set di dati popolato su tutti gli eventi. |
| `{EVENT_DEFINITION}` | L&#39;espressione per qualificare l&#39;evento successivo. |
| `{TIME_UNIT}` | (Facoltativo) Unità di uscita. Il valore possibile include giorni, ore, minuti e secondi. Per impostazione predefinita, il valore è secondi. |

Una spiegazione dei parametri all&#39;interno della funzione `OVER()` si trova nella sezione [funzioni finestra](#window-functions).

**Query di esempio**

```sql
SELECT 
  page_name,
  SUM (time_between_next_match) / COUNT(page_name) as average_minutes_until_order_confirmation
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Shopping Cart|Order Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
    AS time_between_next_match
FROM experience_events
)
WHERE time_between_next_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_until_order_confirmation DESC
LIMIT 10
```

**Risultati**

```console
             page_name             | average_minutes_until_order_confirmation 
-----------------------------------+------------------------------------------
 Shopping Cart|Order Confirmation  |                                      0.0
 Men                               |                       -9.465295629820051
 Equipment                         |                       -9.682098765432098
 Product List                      |                       -9.690661478599221
 Women                             |                       -9.759459459459459
 Seasonal                          |                                  -10.295
 Shopping Cart|Order Review        |                      -366.33567364956144
 Unlimited Blog|February           |                       -615.0327868852459
 Shopping Cart|Billing Information |                       -775.6200495367711
 Product Details|Buffalo           |                      -1274.9571428571428
(10 rows)
```

Per la query di esempio fornita, i risultati sono riportati nella colonna `average_minutes_until_order_confirmation`. Il valore all&#39;interno della colonna `average_minutes_until_order_confirmation` corrisponde alla differenza di tempo tra gli eventi corrente e successivo. L&#39;unità di tempo è stata definita in precedenza in `{TIME_UNIT}`.

## Passaggi successivi

Utilizzando le funzioni qui descritte, è possibile scrivere query per accedere ai propri dataset [!DNL Experience Event] utilizzando [!DNL Query Service]. Per ulteriori informazioni sull&#39;authoring delle query in [!DNL Query Service], consultare la documentazione relativa alla creazione di query [in ](../best-practices/writing-queries.md).

## Risorse aggiuntive

Il seguente video mostra come eseguire le query nell&#39;interfaccia Adobe Experience Platform e in un client PSQL. Inoltre, il video utilizza anche esempi che coinvolgono singole proprietà in un oggetto XDM, utilizzando  funzioni definite dal Adobe e utilizzando CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)