---
title: Analisi di attribuzione
description: Questo documento spiega come utilizzare Query Service per creare una tecnica di misurazione dell’efficacia del marketing basata sul modello di attribuzione del marketing di primo e ultimo contatto.
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 1%

---

# Analisi di attribuzione

Attribution è un concetto analitico che aiuta a determinare le tattiche di marketing come canali, offerte e messaggi, che contribuiscono alle vendite o conversioni aziendali. Questo concetto valuta il percorso di consumatori (il processo con cui un cliente interagisce con un&#39;azienda per raggiungere un obiettivo) che si traduce in un acquisto o in un&#39;acquisizione in base ai punti di contatto del cliente (ogni volta che un consumatore interagisce con il tuo marchio). Mediante l’analisi dell’attribuzione, gli addetti al marketing possono valutare il ritorno sull’investimento dei canali che li collegano a un potenziale cliente.

## Introduzione

Gli esempi SQL presenti in questo documento sono query comunemente utilizzate con i dati di Adobe Analytics. Questa esercitazione richiede una buona comprensione dei seguenti componenti:

* [Panoramica del connettore sorgente Adobe Analytics per i dati della suite di rapporti](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [Documentazione sulle mappature dei campi di Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) fornisce ulteriori informazioni sull’acquisizione e la mappatura dei dati analitici da utilizzare con Query Service.
* [Panoramica sulla Attribution IQ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=it)
* [Guida al pannello Attribuzione di Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html?lang=it).

Una spiegazione dei parametri all&#39;interno del `OVER()` si trova nella [sezione sulle funzioni della finestra](../sql/adobe-defined-functions.md#window-functions). La [Glossario dei termini di marketing e commercio per Adobe](https://business.adobe.com/glossary/index.html) può anche essere utile.

Per ciascuno dei seguenti casi d&#39;uso, viene fornito un esempio di query SQL con parametri come modello da personalizzare. Fornisci parametri ovunque vedi `{ }` negli esempi SQL che si desidera valutare.

## Obiettivi

Un caso di utilizzo di attribuzione utilizza i dati di Adobe Analytics per facilitare l’associazione delle azioni dei clienti a un risultato di successo. Questa associazione è una parte fondamentale per comprendere i fattori che influenzano le esperienze dei clienti. I dati di analisi dell’attribuzione possono essere utilizzati per comprendere l’importanza del punto di contatto di un cliente durante il percorso del cliente.

Gli esempi di query contenuti in questo documento supportano vari casi d’uso per l’attribuzione di primo e ultimo contatto con diverse impostazioni di scadenza. Questa guida illustra i seguenti concetti chiave:

* Attribuzione di primo e ultimo contatto.
* Attribuzione di primo e ultimo contatto con timeout di scadenza.
* Attribuzione di primo e ultimo contatto con condizione di scadenza.

## Parametri query di attribuzione {#attribution-query-parameters}

La tabella seguente fornisce una suddivisione dei parametri e delle relative descrizioni utilizzate nelle query di attribuzione di primo e ultimo contatto:

| Parametro | Descrizione |
|---|---|
| `{TIMESTAMP}` | Il campo timestamp trovato nel set di dati. |
| `{CHANNEL_NAME}` | Etichetta per l&#39;oggetto restituito. |
| `{CHANNEL_VALUE}` | La colonna o il campo di destinazione della query. |
| `{EXP_TIMEOUT}` | La finestra di tempo precedente all’evento del canale, in secondi, in cui la query cerca un primo evento di contatto. |
| `{EXP_CONDITION}` | La condizione che determina il punto di scadenza del canale. |
| `{EXP_BEFORE}` | Valore booleano che indica se il canale scade prima o dopo la condizione specificata, `{EXP_CONDITION}`, è soddisfatto. Questo è abilitato principalmente per le condizioni di scadenza di una sessione, per garantire che il primo contatto non sia selezionato da una sessione precedente. Per impostazione predefinita, questo valore è impostato su `false`. |

## Componenti della colonna dei risultati della query {#query-result-column-components}

I risultati per le query di attribuzione sono forniti nella variabile `first_touch` o `last_touch` colonna. Queste colonne sono costituite dai seguenti componenti:

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametri | Descrizione |
| ---------- | ----------- |
| `{NAME}` | La `{CHANNEL_NAME}`, immesso come etichetta in Azure Data Factory (ADF). |
| `{VALUE}` | Valore da `{CHANNEL_VALUE}` che è l’ultimo contatto all’interno del `{EXP_TIMEOUT}` intervallo |
| `{TIMESTAMP}` | La marca temporale del [!DNL Experience Event] dove si è verificato l’ultimo contatto |
| `{FRACTION}` | L’attribuzione dell’ultimo contatto, espressa come frazione decimale. |

### Attribuzione primo contatto {#first-touch}

L’attribuzione di primo contatto attribuisce il 100% della responsabilità di un esito positivo al canale iniziale rilevato dal consumatore. Questo esempio SQL viene utilizzato per evidenziare l&#39;interazione che ha portato a una serie successiva di azioni del cliente.

La query seguente restituisce il valore di attribuzione del primo contatto e i dettagli del canale nel target [!DNL Experience Event] set di dati. Restituisce anche un `struct` oggetto per il canale selezionato con il primo valore di contatto, la marca temporale e l’attribuzione per ogni riga.

>[!NOTE]
>
>L’ID Experience Cloud (ECID) è noto anche come MCID e continua a essere utilizzato nei namespace.

**Sintassi della query**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

Per un elenco completo dei parametri potenzialmente richiesti e delle relative descrizioni, consulta [sezione sui parametri della query di attribuzione](#attribution-query-parameters).

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

Nei risultati seguenti, il codice di tracciamento iniziale `em:946426` è tratto dal [!DNL Experience Event] set di dati. Questo codice di tracciamento è attribuito al 100% (`1.0`) della responsabilità per le azioni dei clienti, perché è stata la prima interazione.

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Per una suddivisione dei risultati visualizzati nella variabile `first_touch` , vedi la colonna [sezione componenti colonna](#query-result-column-components).

### Attribuzione ultimo contatto {#second-touch}

L’attribuzione Last Touch accredita il 100% della responsabilità di un esito positivo all’ultimo canale rilevato dal consumatore. Questo esempio SQL viene utilizzato per evidenziare l&#39;interazione finale in una serie di azioni del cliente.

La query restituisce il valore di attribuzione dell’ultimo contatto e i dettagli del canale nel target [!DNL Experience Event] set di dati. Restituisce anche un `struct` oggetto per il canale selezionato con il valore di ultimo contatto, la marca temporale e l’attribuzione per ogni riga.

**Sintassi della query**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

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

Nei risultati visualizzati di seguito, il codice di tracciamento nell’oggetto restituito è l’ultima interazione in ogni [!DNL Experience Event] record. Ogni codice è attribuito al 100% (`1.0`) responsabilità delle azioni del cliente, in quanto è stata l’ultima interazione.

```console
                 id                |       timestamp       | trackingCode |                   last_touch                   
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

Per una suddivisione dei risultati visualizzati nella variabile `last_touch` , vedi la colonna [sezione componenti colonna](#query-result-column-components).

### Attribuzione del primo contatto con condizione di scadenza {#first-touch-attribution-with-expiration-condition}

Questa query viene utilizzata per vedere quale interazione ha portato a una serie di azioni del cliente all’interno di una parte della [!DNL Experience Event] set di dati determinato da una condizione a scelta.

La query restituisce il valore di attribuzione e i dettagli del primo contatto per un singolo canale nel target [!DNL Experience Event] set di dati che scade dopo o prima di una condizione. Restituisce anche un `struct` oggetto con il primo valore di contatto, la marca temporale e l’attribuzione per ogni riga restituita per il canale selezionato.

**Sintassi della query**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Per un elenco completo dei parametri potenzialmente richiesti e delle relative descrizioni, consulta [sezione sui parametri della query di attribuzione](#attribution-query-parameters).

**Query di esempio**

Nell’esempio seguente, viene registrato un acquisto (`commerce.purchases.value IS NOT NULL`) in ciascuno dei quattro giorni mostrati nei risultati (15 luglio, 21, 23 e 29) e il codice di tracciamento iniziale di ogni giorno è attribuito al 100% (`1.0`) responsabilità delle azioni dei clienti.

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
                 id               |       timestamp       | trackingCode |                   first_touch                   
----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Per una suddivisione dei risultati visualizzati nella variabile `first_touch` , vedi la colonna [sezione componenti colonna](#query-result-column-components).

### Attribuzione primo contatto con timeout di scadenza {#first-touch-attribution-with-expiration-timeout}

Questa query viene utilizzata per trovare l’interazione, entro un periodo di tempo selezionato, che ha portato all’azione del cliente di successo.

La query seguente restituisce il valore di attribuzione e i dettagli del primo contatto per un singolo canale nel target [!DNL Experience Event] set di dati per un periodo di tempo specificato. La query restituisce un `struct` oggetto con il primo valore di contatto, la marca temporale e l’attribuzione per ogni riga restituita per il canale selezionato.

**Sintassi della query**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Per un elenco completo dei parametri potenzialmente richiesti e delle relative descrizioni, consulta [sezione sui parametri della query di attribuzione](#attribution-query-parameters).

**Query di esempio**

Nell’esempio seguente, il primo contatto restituito per ogni azione del cliente è la prima interazione nei sette giorni precedenti (expTimeout = 86400 * 7).

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
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Per una suddivisione dei risultati visualizzati nella variabile `first_touch` , vedi la colonna [sezione componenti colonna](#query-result-column-components).

### Attribuzione dell’ultimo contatto con condizione di scadenza {#last-touch-attribution-with-expiration-condition}

Questa query viene utilizzata per trovare l’ultima interazione in una serie di azioni del cliente all’interno di una parte della [!DNL Experience Event] set di dati determinato da una condizione a scelta.

La query seguente restituisce il valore di attribuzione dell’ultimo contatto e i dettagli di un singolo canale nel target [!DNL Experience Event] set di dati che scade dopo o prima di una condizione. La query restituisce un `struct` oggetto con valore ultimo contatto, marca temporale e attribuzione per ogni riga restituita per il canale selezionato.

**Sintassi della query**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Per un elenco completo dei parametri potenzialmente richiesti e delle relative descrizioni, consulta [sezione sui parametri della query di attribuzione](#attribution-query-parameters).

**Query di esempio**

Nell’esempio seguente, viene registrato un acquisto (`commerce.purchases.value IS NOT NULL`) in ciascuno dei quattro giorni mostrati nei risultati (15 luglio, 21, 23 e 29) e l’ultimo codice di tracciamento di ogni giorno è attribuito al 100% (`1.0`) responsabilità delle azioni dei clienti.

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

**Risultati di esempio**

```console
                id                 |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+------------------------------------------------
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

Per una suddivisione dei risultati visualizzati nella variabile `last_touch` , vedi la colonna [sezione componenti colonna](#query-result-column-components).

### Attribuzione dell’ultimo contatto con timeout di scadenza {#last-touch-attribution-with-expiration-timeout}

Questa query viene utilizzata per trovare l’ultima interazione all’interno di un intervallo di tempo selezionato. La query restituisce il valore di attribuzione dell’ultimo contatto e i dettagli di un singolo canale nel target [!DNL Experience Event] set di dati per un periodo di tempo specificato. La query restituisce un `struct` oggetto con valore ultimo contatto, marca temporale e attribuzione per ogni riga restituita per il canale selezionato.

**Sintassi della query**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Per un elenco completo dei parametri potenzialmente richiesti e delle relative descrizioni, consulta [sezione sui parametri della query di attribuzione](#attribution-query-parameters).

**Query di esempio**

Nell’esempio seguente, l’ultimo contatto restituito per ogni azione del cliente è l’interazione finale entro i sette giorni successivi (`expTimeout = 86400 * 7`).

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

Per una suddivisione dei risultati visualizzati nella variabile `last_touch` , vedi la colonna [sezione componenti colonna](#query-result-column-components).
