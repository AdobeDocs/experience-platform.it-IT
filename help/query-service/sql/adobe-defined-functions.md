---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' funzioni definite dal Adobe'
topic: functions
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 3%

---


#  funzioni definite dal Adobe

 funzioni definite dal Adobe (ADF) sono funzioni preconfigurate [!DNL Query Service] che consentono di eseguire le comuni attività aziendali relative ai [!DNL ExperienceEvent] dati. tra cui funzioni di Sessionizzazione e Attribuzione, come quelle presenti in  Adobe Analytics. Per ulteriori informazioni su  Adobe Analytics e sui concetti alla base delle ADF definiti in questa pagina, consulta la [documentazione](https://docs.adobe.com/content/help/it-IT/analytics/landing/home.html) Adobe Analytics. Questo documento fornisce informazioni  funzioni definite dal Adobe disponibili in [!DNL Query Service].

## Funzioni della finestra

La maggior parte della logica di business richiede la raccolta dei punti di contatto per un cliente e l&#39;ordine per tempo. Questo supporto viene fornito da [!DNL Spark] SQL sotto forma di funzioni finestra. Le funzioni finestra fanno parte di SQL standard e sono supportate da molti altri motori SQL.

Una funzione finestra aggiorna un&#39;aggregazione e restituisce un singolo elemento per ogni riga del sottoinsieme ordinato. La funzione di aggregazione di base è `SUM()`. `SUM()` prende le righe e le dà un totale. Se invece si applica `SUM()` a una finestra, trasformandola in una funzione finestra, si riceve una somma cumulativa con ogni riga.

La maggior parte degli assistenti [!DNL Spark] SQL sono funzioni finestra che aggiornano ogni riga nella finestra, con l&#39;aggiunta dello stato della riga.

### Specifiche

Sintassi: `OVER ([partition] [order] [frame])`

| Parametro | Descrizione |
| --- | --- |
| [partizione] | Un sottogruppo delle righe in base a una colonna o a un campo disponibile. Esempio, `PARTITION BY endUserIds._experience.mcid.id` |
| [order] | Colonna o campo disponibile utilizzato per ordinare il sottoinsieme o le righe. Esempio, `ORDER BY timestamp` |
| [frame] | Un sottogruppo delle righe in una partizione. Esempio, `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionizzazione

Quando si lavora con [!DNL ExperienceEvent] dati provenienti da un sito Web, un&#39;applicazione mobile, un sistema di risposta vocale interattivo o qualsiasi altro canale di interazione con i clienti, è possibile raggruppare gli eventi intorno a un periodo di attività correlato. In genere, l&#39;attività è guidata da un intento specifico, come la ricerca di un prodotto, il pagamento di una fattura, il controllo del saldo del conto, la compilazione di un&#39;applicazione e così via. Questo raggruppamento consente di associare gli eventi per scoprire un contesto più ampio sull&#39;esperienza del cliente.

Per ulteriori informazioni sulle sessioni in  Adobe Analytics, consulta la documentazione sulle sessioni in base al [contesto](https://docs.adobe.com/content/help/en/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

### Specifiche

Sintassi: `SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])`

| Parametro | Descrizione |
| --- | --- |
| `timestamp` | Campo marca temporale trovato nel dataset |
| `expirationInSeconds` | Numero di secondi necessari tra gli eventi per qualificare la fine della sessione corrente e l&#39;inizio di una nuova sessione |

| Parametri oggetto restituiti | Descrizione |
| ---------------------- | ------------- |
| `timestamp_diff` | Tempo in secondi tra il record corrente e il record precedente |
| `num` | Un numero di sessione univoco, a partire da 1, per la chiave definita nella funzione `PARTITION BY` della finestra. |
| `is_new` | Valore booleano utilizzato per identificare se un record è il primo di una sessione |
| `depth` | Profondità del record corrente nella sessione |

#### Query di esempio

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

#### Risultati

```
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

## Attribution

Associare le azioni dei clienti al successo è una parte importante della comprensione dei fattori che influenzano l&#39;esperienza dei clienti. I seguenti ADF supportano l’attribuzione Primo e Ultimo con diverse impostazioni di scadenza.

Per ulteriori informazioni sull’attribuzione in  Adobe Analytics, consulta la [panoramica](https://docs.adobe.com/content/help/it-IT/analytics/analyze/analysis-workspace/panels/attribution.html) delle Attribution IQ nella Guida all’ [!DNL Analytics] analisi.

### Attribuzione primo tocco

Restituisce il primo valore di attribuzione touch e i dettagli per un singolo canale nel [!DNL ExperienceEvent] dataset di destinazione. La query restituisce un `struct` oggetto con il primo valore di tocco, marca temporale e attribuzione per ogni riga restituita per il canale selezionato.

Questa query è utile per visualizzare quale interazione ha portato a una serie di azioni da parte del cliente. Nell’esempio riportato di seguito, al codice di tracciamento iniziale (`em:946426`) nei [!DNL ExperienceEvent] dati viene attribuita la responsabilità del 100% (`1.0`) per le azioni del cliente, in quanto si trattava della prima interazione.

### Specifiche

Sintassi: `ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Parametro | Descrizione |
| --- | --- |
| `timestamp` | Campo marca temporale trovato nel dataset |
| `channelName` | Un nome descrittivo da utilizzare come etichetta nell&#39;oggetto restituito |
| `channelValue` | Colonna o campo che rappresenta il canale di destinazione per la query |


| Parametri oggetto restituiti | Descrizione |
| ---------------------- | ------------- |
| `name` | L’etichetta `channelName` immessa nell’ADF |
| `value` | Il valore di `channelValue` questo è il primo tocco nel pannello [!DNL ExperienceEvent] |
| `timestamp` | Timestamp del [!DNL ExperienceEvent] punto in cui si è verificato il primo tocco |
| `fraction` | Attribuzione del primo tocco espresso come credito frazionario |

#### Query di esempio

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

#### Risultati

```
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

### Ultima attribuzione tocco

Restituisce l’ultimo valore di attribuzione touch e i dettagli per un singolo canale nel [!DNL ExperienceEvent] dataset di destinazione. La query restituisce un `struct` oggetto con l&#39;ultimo valore di tocco, marca temporale e attribuzione per ogni riga restituita per il canale selezionato.

Questa query è utile per visualizzare l&#39;interazione finale in una serie di azioni cliente. Nell&#39;esempio riportato di seguito, il codice di tracciamento nell&#39;oggetto restituito è l&#39;ultima interazione in ciascun [!DNL ExperienceEvent] record. A ciascun codice viene attribuita la responsabilità al 100% (`1.0`) per le azioni dei clienti, così come è stata l&#39;ultima interazione.

### Specifiche

Sintassi: `ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Parametro | Descrizione |
| --- | --- |
| `timestamp` | Campo marca temporale trovato nel dataset |
| `channelName` | Un nome descrittivo da utilizzare come etichetta nell&#39;oggetto restituito |
| `channelValue` | Colonna o campo che rappresenta il canale di destinazione per la query |


| Parametri oggetto restituiti | Descrizione |
| ---------------------- | ------------- |
| `name` | L’etichetta `channelName` immessa nell’ADF |
| `value` | Il valore di `channelValue` questo è l’ultimo tocco nel pannello [!DNL ExperienceEvent] |
| `timestamp` | La marca temporale della [!DNL ExperienceEvent] posizione in cui `channelValue` è stato utilizzato |
| `fraction` | Attribuzione dell&#39;ultimo tocco espresso come credito frazionario |

#### Query di esempio

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

#### Risultati

```
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

### Attribuzione del primo tocco con condizione di scadenza

Restituisce il primo valore di attribuzione touch e i dettagli per un singolo canale nel [!DNL ExperienceEvent] dataset di destinazione, che scade dopo o prima di una condizione. La query restituisce un `struct` oggetto con il primo valore di tocco, marca temporale e attribuzione per ogni riga restituita per il canale selezionato.

Questa query è utile se si desidera vedere quale interazione ha portato a una serie di azioni da parte del cliente all&#39;interno di una parte del [!DNL ExperienceEvent] dataset determinata da una condizione scelta. Nell&#39;esempio riportato di seguito, un acquisto viene registrato (`commerce.purchases.value IS NOT NULL`) in ciascuno dei quattro giorni mostrati nei risultati (15 luglio, 21, 23 e 29) e al codice di tracciamento iniziale di ogni giorno viene attribuita la responsabilità del 100% (`1.0`) per le azioni dei clienti.

#### Specifiche

Sintassi: `ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Parametro | Descrizione |
| --- | --- |
| `timestamp` | Campo marca temporale trovato nel dataset |
| `channelName` | Un nome descrittivo da utilizzare come etichetta nell&#39;oggetto restituito |
| `channelValue` | Colonna o campo che rappresenta il canale di destinazione per la query |
| `expCondition` | La condizione che determina il punto di scadenza del canale |
| `expBefore` | Defaults to `false`. Valore booleano per indicare se il canale scade prima o dopo il soddisfacimento della condizione specificata. Attivato principalmente per le condizioni di scadenza di una sessione (ad esempio, `sess.depth = 1, true`), per fare in modo che il primo tocco non sia selezionato da una sessione precedente. |

| Parametri oggetto restituiti | Descrizione |
| ---------------------- | ------------- |
| `name` | L’etichetta `channelName` immessa nell’ADF |
| `value` | Il valore di `channelValue` questo è il primo tocco nella finestra [!DNL ExperienceEvent] precedente `expCondition` |
| `timestamp` | Timestamp del [!DNL ExperienceEvent] punto in cui si è verificato il primo tocco |
| `fraction` | Attribuzione del primo tocco espresso come credito frazionario |

#### Query di esempio

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

#### Risultati

```
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

### Prima attribuzione touch con timeout di scadenza

Restituisce il primo valore di attribuzione touch e i dettagli per un singolo canale nel [!DNL ExperienceEvent] dataset di destinazione per un periodo di tempo specificato. La query restituisce un `struct` oggetto con il primo valore di tocco, marca temporale e attribuzione per ogni riga restituita per il canale selezionato. Questa query è utile se si desidera vedere quale interazione, entro un intervallo di tempo selezionato, ha portato a un&#39;azione del cliente. Nell’esempio riportato di seguito, il primo tocco restituito per ogni azione del cliente è la prima interazione nei sette giorni precedenti (`expTimeout = 86400 * 7`).

#### Specifiche

Sintassi: `ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Parametro | Descrizione |
| --- | --- |
| `timestamp` | Campo marca temporale trovato nel dataset |
| `channelName` | Un nome descrittivo da utilizzare come etichetta nell&#39;oggetto restituito |
| `channelValue` | Colonna o campo che rappresenta il canale di destinazione per la query |
| `expTimeout` | La finestra di tempo (in secondi) prima dell&#39;evento del canale che la query cerca per un primo evento di tocco |

| Parametri oggetto restituiti | Descrizione |
| ---------------------- | ------------- |
| `name` | L’etichetta `channelName` immessa nell’ADF |
| `value` | Il valore da `channelValue` cui proviene il primo tocco entro l&#39;intervallo specificato `expTimeout` |
| `timestamp` | Timestamp del [!DNL ExperienceEvent] punto in cui si è verificato il primo tocco |
| `fraction` | Attribuzione del primo tocco espresso come credito frazionario |

#### Query di esempio

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

#### Risultati

```
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

### Attribuzione dell&#39;ultimo tocco con condizione di scadenza

Restituisce l’ultimo valore di attribuzione touch e i dettagli per un singolo canale nel [!DNL ExperienceEvent] set di dati di destinazione, che scade dopo o prima di una condizione. La query restituisce un `struct` oggetto con l&#39;ultimo valore di tocco, marca temporale e attribuzione per ogni riga restituita per il canale selezionato. Questa query è utile se si desidera visualizzare l&#39;ultima interazione in una serie di azioni cliente all&#39;interno di una parte del [!DNL ExperienceEvent] dataset determinata da una condizione di scelta. Nell&#39;esempio riportato di seguito, un acquisto viene registrato (`commerce.purchases.value IS NOT NULL`) in ciascuno dei quattro giorni mostrati nei risultati (15 luglio, 21, 23 e 29) e all&#39;ultimo codice di tracciamento in ogni giorno viene attribuito il 100% (`1.0`) di responsabilità per le azioni dei clienti.

#### Specifiche

Sintassi: `ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Parametro | Descrizione |
| --- | --- |
| `timestamp` | Campo marca temporale trovato nel dataset |
| `channelName` | Un nome descrittivo da utilizzare come etichetta nell&#39;oggetto restituito |
| `channelValue` | Colonna o campo che rappresenta il canale di destinazione per la query |
| `expCondition` | La condizione che determina il punto di scadenza del canale |
| `expBefore` | Defaults to `false`. Valore booleano per indicare se il canale scade prima o dopo il soddisfacimento della condizione specificata. Attivato principalmente per le condizioni di scadenza della sessione (ad esempio, `sess.depth = 1, true`), per fare in modo che l’ultimo tocco non sia selezionato da una sessione precedente. |

| Parametri oggetto restituiti | Descrizione |
| ---------------------- | ------------- |
| `name` | L’etichetta `channelName` immessa nell’ADF |
| `value` | Il valore di `channelValue` questo è l’ultimo tocco nella finestra [!DNL ExperienceEvent] precedente `expCondition` |
| `timestamp` | Il timestamp dell’ [!DNL ExperienceEvent] ultimo tocco |
| `percentage` | Attribuzione dell&#39;ultimo tocco espresso come credito frazionario |

#### Query di esempio

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

#### Risultati

```
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

### Ultima attribuzione touch con timeout di scadenza

Restituisce l’ultimo valore di attribuzione touch e i dettagli per un singolo canale nel [!DNL ExperienceEvent] dataset di destinazione per un periodo di tempo specificato. La query restituisce un `struct` oggetto con l&#39;ultimo valore di tocco, marca temporale e attribuzione per ogni riga restituita per il canale selezionato. Questa query è utile se si desidera visualizzare l&#39;ultima interazione entro un intervallo di tempo selezionato. Nell’esempio riportato di seguito, l’ultimo tocco restituito per ogni azione del cliente è l’interazione finale entro i sette giorni successivi (`expTimeout = 86400 * 7`).

#### Specifiche

Sintassi: `ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Parametro | Descrizione |
| --- | --- |
| `timestamp` | Campo marca temporale trovato nel dataset |
| `channelName` | Un nome descrittivo da utilizzare come etichetta nell&#39;oggetto restituito |
| `channelValue` | Colonna o campo che rappresenta il canale di destinazione per la query |
| `expTimeout` | La finestra di tempo (in secondi) dopo l’evento del canale che la query cerca per un ultimo evento di tocco |

| Parametri oggetto restituiti | Descrizione |
| ---------------------- | ------------- |
| `name` | L’etichetta `channelName` immessa nell’ADF |
| `value` | Il valore da `channelValue` cui proviene l&#39;ultimo tocco entro l&#39;intervallo specificato `expTimeout` |
| `timestamp` | Il timestamp dell’ [!DNL ExperienceEvent] ultimo tocco |
| `percentage` | Attribuzione dell&#39;ultimo tocco espresso come credito frazionario |

#### Query di esempio

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

#### Risultati

```
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

## Tocco precedente/successivo

È importante comprendere in che modo i clienti si spostano all&#39;interno di un&#39;esperienza. Può essere utilizzato per comprendere la profondità di coinvolgimento del cliente, confermare che i passaggi previsti di un&#39;esperienza funzionano correttamente e identificare potenziali punti di dolore che possono avere un impatto sul cliente. Le seguenti ADF supportano la definizione delle visualizzazioni dei percorsi dalle relazioni Precedente e Successivo. Potrete creare la pagina precedente e la pagina successiva, oppure seguire più eventi per creare il percorso.

### Tocco precedente

Determina il valore precedente di un particolare campo a un numero definito di passi dall&#39;interno della finestra. Tenere presente nell&#39;esempio che la `WINDOW` funzione è configurata con un fotogramma che consente di `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` impostare l&#39;ADF per osservare la riga corrente e tutti gli elementi precedenti.

#### Specifiche

Sintassi: `PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Parametro | Descrizione |
| --- | --- |
| `key` | Colonna o campo dell’evento. |
| `shift` | (Facoltativo) Il numero di eventi lontani dall’evento corrente. Il valore predefinito è 1. |
| `ingnoreNulls` | Valore booleano che indica se `key` i valori null devono essere ignorati. Default is `false`. |


| Parametri oggetto restituiti | Descrizione |
| ---------------------- | ------------- |
| `value` | Il valore basato sul valore `key` utilizzato nell&#39;ADF |

#### Query di esempio

```sql
SELECT endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id, _experience.analytics.session.num
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp ASC
```

#### Risultati

```
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

### Tasto successivo

Determina il valore successivo di un particolare campo a un numero definito di passi di distanza all&#39;interno della finestra. Tenere presente nell&#39;esempio che la `WINDOW` funzione è configurata con un fotogramma che consente di `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` impostare l&#39;ADF per osservare la riga corrente e tutte le righe successive.

#### Specifiche

Sintassi: `NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Parametro | Descrizione |
| --- | --- |
| `key` | Colonna o campo dell’evento |
| `shift` | (Facoltativo) Il numero di eventi lontani dall’evento corrente. Il valore predefinito è 1. |
| `ingnoreNulls` | Valore booleano che indica se `key` i valori null devono essere ignorati. Default is `false`. |


| Parametri oggetto restituiti | Descrizione |
| ---------------------- | ------------- |
| `value` | Il valore basato sul valore `key` utilizzato nell&#39;ADF |

#### Query di esempio

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

#### Risultati

```
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

## Intervallo di tempo

Il time-between consente di esplorare il comportamento latente dei clienti entro un periodo di tempo precedente o successivo all&#39;evento. Guardate gli eventi entro 7 giorni dalla campagna o da un altro tipo di evento per tutti i vostri clienti.

### Tempo tra la corrispondenza precedente

Fornisce una nuova dimensione che misura il tempo trascorso da un particolare incidente.

#### Specifiche

Sintassi: `TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Parametro | Descrizione |
| --- | --- |
| `timestamp` | Campo marca temporale trovato nel set di dati popolato su tutti gli eventi. |
| `eventDefintion` | Espressione per qualificare l&#39;evento precedente. |
| `timeUnit` | Unità di uscita: giorni, ore, minuti e secondi. Il valore predefinito è secondi. |

Output: Restituisce un numero che rappresenta l&#39;unità di tempo dal momento che l&#39;evento corrispondente precedente è stato visto o rimane null se non è stato trovato alcun evento corrispondente.

#### Query di esempio

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

#### Risultati

```
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

### Tempo tra la partita successiva

Fornisce una nuova dimensione, che misura il tempo prima che si verifichi un particolare evento.

#### Specifiche

Sintassi: `TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Parametro | Descrizione |
| --- | --- |
| `timestamp` | Campo marca temporale trovato nel set di dati popolato su tutti gli eventi. |
| `eventDefintion` | Espressione per qualificare l&#39;evento successivo. |
| `timeUnit` | Unità di uscita: giorni, ore, minuti e secondi. Il valore predefinito è secondi. |

Output: Restituisce un numero negativo che rappresenta l&#39;unità di tempo dietro l&#39;evento di corrispondenza successivo o rimane null se non viene trovato un evento corrispondente.

#### Query di esempio

```
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

#### Risultati

```
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

## Passaggi successivi

Utilizzando le funzioni qui descritte, è possibile scrivere query per accedere ai propri [!DNL ExperienceEvent] dataset utilizzando [!DNL Query Service]. Per ulteriori informazioni sull’authoring delle query in [!DNL Query Service], consulta la documentazione sulla [creazione delle query](../creating-queries/creating-queries.md).
