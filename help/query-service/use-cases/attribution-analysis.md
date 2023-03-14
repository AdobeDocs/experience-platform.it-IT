---
title: Analisi dell’attribuzione
description: Questo documento spiega come utilizzare Query Service per creare una tecnica di misurazione dell’efficacia del marketing basata sul modello di attribuzione marketing di primo e ultimo contatto.
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 1%

---

# Analisi dell’attribuzione

L’attribuzione è un concetto analitico che consente di determinare le tattiche di marketing, come canali, offerte e messaggi, che contribuiscono alle vendite o alle conversioni aziendali. Questo concetto valuta il percorso del consumatore (il processo con cui un cliente interagisce con un’azienda per raggiungere un obiettivo) che si traduce in un acquisto o in un’acquisizione basata sui punti di contatto del cliente (ogni volta che un consumatore interagisce con il brand). Mediante l’analisi dell’attribuzione, gli esperti di marketing possono valutare il ritorno sull’investimento dei canali che li collegano a un potenziale cliente.

## Introduzione

Gli esempi SQL in questo documento sono query comunemente utilizzate con i dati di Adobe Analytics. Questo tutorial richiede una buona conoscenza dei seguenti componenti:

* [Connettore di origine di Adobe Analytics per la panoramica dei dati della suite di rapporti](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [Documentazione sulle mappature dei campi di Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) fornisce ulteriori informazioni sull’acquisizione e la mappatura dei dati analitici da utilizzare con Query Service.
* [Panoramica di Attribution IQ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=it)
* [Guida del pannello Attribuzione di Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html?lang=it).

Una spiegazione dei parametri all&#39;interno del `OVER()` è disponibile nella sezione [sezione funzioni finestra](../sql/adobe-defined-functions.md#window-functions). Il [Glossario dei termini di Adobe Marketing and Commerce](https://business.adobe.com/glossary/index.html) può essere utile.

Per ciascuno dei seguenti casi d’uso, come modello da personalizzare viene fornito un esempio di query SQL con parametri. Fornisci i parametri ovunque ti trovi `{ }` negli esempi SQL che si desidera valutare.

## Obiettivi

Un caso di utilizzo di attribuzione utilizza i dati di Adobe Analytics per aiutare ad associare le azioni dei clienti a un risultato positivo. Questa associazione è fondamentale per comprendere i fattori che influenzano le esperienze dei clienti. I dati di analisi dell’attribuzione possono essere utilizzati per comprendere la significatività del punto di contatto di un cliente durante il percorso del cliente.

Gli esempi di query contenuti in questo documento supportano vari casi d’uso per l’attribuzione del primo e dell’ultimo contatto con impostazioni di scadenza diverse. Questa guida illustra i seguenti concetti chiave:

* Attribuzione del primo contatto e dell’ultimo contatto.
* Attribuzione del primo contatto e dell’ultimo contatto con timeout di scadenza.
* Attribuzione del primo contatto e dell’ultimo contatto con condizione di scadenza.

## Parametri query di attribuzione {#attribution-query-parameters}

La tabella seguente fornisce una suddivisione dei parametri e delle relative descrizioni utilizzati nelle query di attribuzione di primo contatto e ultimo contatto:

| Parametro | Descrizione |
|---|---|
| `{TIMESTAMP}` | Il campo timestamp trovato nel set di dati. |
| `{CHANNEL_NAME}` | Etichetta per l&#39;oggetto restituito. |
| `{CHANNEL_VALUE}` | Colonna o campo che rappresenta il canale di destinazione della query. |
| `{EXP_TIMEOUT}` | Finestra di tempo precedente all’evento del canale, in secondi, in cui la query cerca un evento di primo contatto. |
| `{EXP_CONDITION}` | La condizione che determina il punto di scadenza del canale. |
| `{EXP_BEFORE}` | Valore booleano che indica se il canale scade prima o dopo la condizione specificata. `{EXP_CONDITION}`, è soddisfatto. Questa opzione è abilitata principalmente per le condizioni di scadenza di una sessione, per garantire che il primo contatto non sia selezionato da una sessione precedente. Per impostazione predefinita, questo valore è impostato su `false`. |

## Componenti colonna risultati query {#query-result-column-components}

I risultati delle query di attribuzione sono forniti nel `first_touch` o `last_touch` colonna. Queste colonne sono costituite dai seguenti componenti:

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametri | Descrizione |
| ---------- | ----------- |
| `{NAME}` | Il `{CHANNEL_NAME}`, immesso come etichetta in Azure Data Factory (ADF). |
| `{VALUE}` | Il valore da `{CHANNEL_VALUE}` questo è l’ultimo contatto all’interno del `{EXP_TIMEOUT}` intervallo |
| `{TIMESTAMP}` | Il timestamp del [!DNL Experience Event] dove si è verificato l’ultimo contatto |
| `{FRACTION}` | Attribuzione dell’ultimo contatto, espressa come frazione decimale. |

### Attribuzione del primo contatto {#first-touch}

L’attribuzione del primo contatto attribuisce il 100% della responsabilità per un esito positivo al canale iniziale incontrato dal consumatore. Questo esempio SQL viene utilizzato per evidenziare l’interazione che ha portato a una serie successiva di azioni del cliente.

La query seguente restituisce il valore di attribuzione del primo contatto e i dettagli del canale nel target [!DNL Experience Event] set di dati. Inoltre, restituisce un `struct` oggetto per il canale selezionato con il valore di primo contatto, la marca temporale e l’attribuzione per ogni riga.

>[!NOTE]
>
>L’ID Experience Cloud (ECID) è noto anche come MCID e continua a essere utilizzato nei namespace.

**Sintassi della query**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

Per un elenco completo dei parametri potenzialmente richiesti e delle relative descrizioni, vedere [sezione parametri query di attribuzione](#attribution-query-parameters).

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

Nei risultati seguenti, il codice di tracciamento iniziale `em:946426` è tratto da [!DNL Experience Event] set di dati. Questo codice di tracciamento è attribuito al 100% (`1.0`) della responsabilità per le azioni del cliente, perché è stata la prima interazione.

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

Per una suddivisione dei risultati visualizzati nel `first_touch` , vedere la [sezione dei componenti colonna](#query-result-column-components).

### Attribuzione ultimo contatto {#second-touch}

L’attribuzione dell’ultimo contatto attribuisce il 100% della responsabilità per un esito positivo all’ultimo canale incontrato dal consumatore. Questo esempio SQL viene utilizzato per evidenziare l’interazione finale in una serie di azioni del cliente.

La query restituisce il valore di attribuzione dell’ultimo contatto e i dettagli del canale nel target [!DNL Experience Event] set di dati. Inoltre, restituisce un `struct` oggetto per il canale selezionato con il valore dell’ultimo contatto, la marca temporale e l’attribuzione per ogni riga.

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

Nei risultati visualizzati di seguito, il codice di tracciamento nell’oggetto restituito è l’ultima interazione in ogni [!DNL Experience Event] record. A ciascun codice è attribuito il 100% (`1.0`) la responsabilità per le azioni del cliente, in quanto si trattava dell’ultima interazione.

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

Per una suddivisione dei risultati visualizzati nel `last_touch` , vedere la [sezione dei componenti colonna](#query-result-column-components).

### Attribuzione del primo contatto con condizione di scadenza {#first-touch-attribution-with-expiration-condition}

Questa query viene utilizzata per vedere quale interazione ha portato a una serie di azioni del cliente all’interno di una parte del [!DNL Experience Event] set di dati determinato da una condizione scelta.

La query restituisce il valore di attribuzione del primo contatto e i dettagli per un singolo canale nella destinazione [!DNL Experience Event] set di dati, con scadenza dopo o prima di una condizione. Inoltre, restituisce un `struct` oggetto con il valore di primo contatto, la marca temporale e l’attribuzione per ogni riga restituita per il canale selezionato.

**Sintassi della query**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Per un elenco completo dei parametri potenzialmente richiesti e delle relative descrizioni, vedere [sezione parametri query di attribuzione](#attribution-query-parameters).

**Query di esempio**

Nell’esempio riportato di seguito, viene registrato un acquisto (`commerce.purchases.value IS NOT NULL`) in ciascuno dei quattro giorni indicati nei risultati (15, 21, 23 e 29 luglio) e il codice di tracciamento iniziale per ogni giorno è attribuito al 100% (`1.0`) responsabilità per le azioni del cliente.

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

Per una suddivisione dei risultati visualizzati nel `first_touch` , vedere la [sezione dei componenti colonna](#query-result-column-components).

### Attribuzione del primo contatto con timeout di scadenza {#first-touch-attribution-with-expiration-timeout}

Questa query viene utilizzata per trovare l’interazione, entro un periodo di tempo selezionato, che ha portato all’azione del cliente riuscita.

La query seguente restituisce il valore di attribuzione del primo contatto e i dettagli per un singolo canale nel target [!DNL Experience Event] set di dati per un periodo di tempo specificato. La query restituisce un `struct` oggetto con il valore di primo contatto, la marca temporale e l’attribuzione per ogni riga restituita per il canale selezionato.

**Sintassi della query**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Per un elenco completo dei parametri potenzialmente richiesti e delle relative descrizioni, vedere [sezione parametri query di attribuzione](#attribution-query-parameters).

**Query di esempio**

Nell’esempio mostrato di seguito, il primo contatto restituito per ogni azione del cliente è la prima interazione entro i sette giorni precedenti (expTimeout = 86400 * 7).

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

Per una suddivisione dei risultati visualizzati nel `first_touch` , vedere la [sezione dei componenti colonna](#query-result-column-components).

### Attribuzione ultimo contatto con condizione di scadenza {#last-touch-attribution-with-expiration-condition}

Questa query viene utilizzata per trovare l’ultima interazione in una serie di azioni del cliente all’interno di una parte del [!DNL Experience Event] set di dati determinato da una condizione scelta.

La query seguente restituisce il valore di attribuzione dell’ultimo contatto e i dettagli per un singolo canale nella destinazione [!DNL Experience Event] set di dati, con scadenza dopo o prima di una condizione. La query restituisce un `struct` oggetto con il valore dell’ultimo contatto, la marca temporale e l’attribuzione per ogni riga restituita per il canale selezionato.

**Sintassi della query**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Per un elenco completo dei parametri potenzialmente richiesti e delle relative descrizioni, vedere [sezione parametri query di attribuzione](#attribution-query-parameters).

**Query di esempio**

Nell’esempio riportato di seguito, viene registrato un acquisto (`commerce.purchases.value IS NOT NULL`) in ciascuno dei quattro giorni indicati nei risultati (15, 21, 23 e 29 luglio) e all&#39;ultimo codice di tracciamento per ogni giorno è attribuito il 100% (`1.0`) responsabilità per le azioni del cliente.

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

Per una suddivisione dei risultati visualizzati nel `last_touch` , vedere la [sezione dei componenti colonna](#query-result-column-components).

### Attribuzione ultimo contatto con timeout di scadenza {#last-touch-attribution-with-expiration-timeout}

Questa query viene utilizzata per trovare l’ultima interazione entro un intervallo di tempo selezionato. La query restituisce il valore di attribuzione dell’ultimo contatto e i dettagli per un singolo canale nella destinazione [!DNL Experience Event] set di dati per un periodo di tempo specificato. La query restituisce un `struct` oggetto con il valore dell’ultimo contatto, la marca temporale e l’attribuzione per ogni riga restituita per il canale selezionato.

**Sintassi della query**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Per un elenco completo dei parametri potenzialmente richiesti e delle relative descrizioni, vedere [sezione parametri query di attribuzione](#attribution-query-parameters).

**Query di esempio**

Nell’esempio mostrato di seguito, l’ultimo contatto restituito per ogni azione del cliente è l’interazione finale entro i sette giorni successivi (`expTimeout = 86400 * 7`).

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

Per una suddivisione dei risultati visualizzati nel `last_touch` , vedere la [sezione dei componenti colonna](#query-result-column-components).
