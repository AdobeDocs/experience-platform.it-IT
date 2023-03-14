---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;funzioni definite di adobe;sql;
solution: Experience Platform
title: Funzioni SQL definite dall'Adobe in Query Service
description: Questo documento fornisce informazioni sulle funzioni definite dagli Adobi disponibili in Adobe Experience Platform Query Service.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 3%

---

# Funzioni SQL definite dall&#39;Adobe in Query Service

Le funzioni definite dall’Adobe, di seguito ADF, sono funzioni predefinite di Adobe Experience Platform Query Service che consentono di eseguire attività di business comuni sulle [!DNL Experience Event] dati. Queste includono funzioni per [Sessionizzazione](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) e [Attribuzione](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=it) come quelli trovati in Adobe Analytics.

Questo documento fornisce informazioni sulle funzioni definite dagli Adobi disponibili in [!DNL Query Service].

>[!NOTE]
>
>L’ID Experience Cloud (ECID) è noto anche come MCID e continua a essere utilizzato nei namespace.

## Funzioni finestra {#window-functions}

La maggior parte della logica di business richiede la raccolta dei punti di contatto per un cliente e l’ordine dei punti in base al tempo. Questo supporto è fornito da [!DNL Spark] SQL sotto forma di funzioni di finestra. Le funzioni di finestra fanno parte di SQL standard e sono supportate da molti altri motori SQL.

Una funzione finestra aggiorna un&#39;aggregazione e restituisce un singolo elemento per ogni riga del sottoinsieme ordinato. La funzione di aggregazione di base è `SUM()`. `SUM()` prende le tue righe e ti dà un totale. Se invece si applica `SUM()` a una finestra, trasformandola in una funzione finestra, si riceve una somma cumulativa con ogni riga.

La maggior parte dei [!DNL Spark] Gli helper SQL sono funzioni di finestra che aggiornano ogni riga della finestra, con lo stato di tale riga aggiunto.

**Sintassi della query**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `{PARTITION}` | Un sottogruppo di righe basato su una colonna o un campo disponibile. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | Colonna o campo disponibile utilizzato per ordinare il sottoinsieme o le righe. | `ORDER BY timestamp` |
| `{FRAME}` | Sottogruppo delle righe di una partizione. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionizzazione

Quando si lavora con [!DNL Experience Event] dati provenienti da un sito web, un’app mobile, un sistema interattivo di risposta vocale o qualsiasi altro canale di interazione con il cliente, può essere utile raggruppare gli eventi in base a un periodo di attività correlato. In genere, uno scopo specifico guida l’attività di, ad esempio la ricerca di un prodotto, il pagamento di una fattura, la verifica del saldo del conto, la compilazione di un’applicazione e così via.

Questo raggruppamento, o sessionizzazione dei dati, consente di associare gli eventi per individuare più contesto sull’esperienza del cliente.

Per ulteriori informazioni sulla sessionizzazione in Adobe Analytics, consulta la documentazione su [sessioni in base al contesto](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

**Sintassi della query**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Il campo timestamp trovato nel set di dati. |
| `{EXPIRATION_IN_SECONDS}` | Il numero di secondi necessari tra gli eventi per qualificare la fine della sessione corrente e l’inizio di una nuova sessione. |

Una spiegazione dei parametri all&#39;interno del `OVER()` è disponibile nella sezione [sezione funzioni finestra](#window-functions).

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

Per la query di esempio specificata, i risultati sono riportati nella `session` colonna. Il `session` La colonna è costituita dai seguenti componenti:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parametri | Descrizione |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Differenza di tempo, in secondi, tra il record corrente e il record precedente. |
| `{NUM}` | Un numero di sessione univoco, a partire da 1, per la chiave definita nella `PARTITION BY` della funzione finestra. |
| `{IS_NEW}` | Valore booleano utilizzato per identificare se un record è il primo di una sessione. |
| `{DEPTH}` | Profondità del record corrente nella sessione. |

### SESS_START_IF

Questa query restituisce lo stato della sessione per la riga corrente, in base alla marca temporale corrente e all’espressione specificata, e avvia una nuova sessione con la riga corrente.

**Sintassi della query**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Il campo timestamp trovato nel set di dati. |
| `{TEST_EXPRESSION}` | Espressione in base alla quale si desidera verificare i campi dei dati. Ad esempio, `application.launches > 0`. |

Una spiegazione dei parametri all&#39;interno del `OVER()` è disponibile nella sezione [sezione funzioni finestra](#window-functions).

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

Per la query di esempio specificata, i risultati sono riportati nella `session` colonna. Il `session` La colonna è costituita dai seguenti componenti:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parametri | Descrizione |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Differenza di tempo, in secondi, tra il record corrente e il record precedente. |
| `{NUM}` | Un numero di sessione univoco, a partire da 1, per la chiave definita nella `PARTITION BY` della funzione finestra. |
| `{IS_NEW}` | Valore booleano utilizzato per identificare se un record è il primo di una sessione. |
| `{DEPTH}` | Profondità del record corrente nella sessione. |

### SESS_END_IF

Questa query restituisce lo stato della sessione per la riga corrente, in base alla marca temporale corrente e all&#39;espressione specificata, termina la sessione corrente e avvia una nuova sessione sulla riga successiva.

**Sintassi della query**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Il campo timestamp trovato nel set di dati. |
| `{TEST_EXPRESSION}` | Espressione in base alla quale si desidera verificare i campi dei dati. Ad esempio, `application.launches > 0`. |

Una spiegazione dei parametri all&#39;interno del `OVER()` è disponibile nella sezione [sezione funzioni finestra](#window-functions).

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

Per la query di esempio specificata, i risultati sono riportati nella `session` colonna. Il `session` La colonna è costituita dai seguenti componenti:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parametri | Descrizione |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Differenza di tempo, in secondi, tra il record corrente e il record precedente. |
| `{NUM}` | Un numero di sessione univoco, a partire da 1, per la chiave definita nella `PARTITION BY` della funzione finestra. |
| `{IS_NEW}` | Valore booleano utilizzato per identificare se un record è il primo di una sessione. |
| `{DEPTH}` | Profondità del record corrente nella sessione. |


## Tracciatura percorso

I percorsi possono essere utilizzati per comprendere la profondità di coinvolgimento del cliente, confermare che i passaggi previsti di un’esperienza funzionino come previsto e identificare potenziali punti critici che influiscono sul cliente.

Le seguenti ADF supportano la creazione di viste dei percorsi dalle relazioni precedenti e successive. Potrai creare pagine precedenti e successive, oppure esaminare più eventi per creare un percorso.

### Pagina precedente

Determina il valore precedente di un particolare campo a un numero definito di passi all&#39;interno della finestra. Osserva nell’esempio che il `WINDOW` è configurato con un frame di `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` impostazione dell&#39;ADF per esaminare la riga corrente e tutte le righe successive.

**Sintassi della query**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{KEY}` | La colonna o il campo dell’evento. |
| `{SHIFT}` | (Facoltativo) Il numero di eventi lontani dall’evento corrente. Per impostazione predefinita, il valore è 1. |
| `{IGNORE_NULLS}` | (Facoltativo) Valore booleano che indica se null `{KEY}` i valori devono essere ignorati. Per impostazione predefinita, il valore è `false`. |

Una spiegazione dei parametri all&#39;interno del `OVER()` è disponibile nella sezione [sezione funzioni finestra](#window-functions).

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

Per la query di esempio specificata, i risultati sono riportati nella `previous_page` colonna. Il valore all’interno del `previous_page` si basa sulla colonna `{KEY}` utilizzato nell&#39;ADF.

### Pagina successiva

Determina il valore successivo di un particolare campo a un numero definito di passi all&#39;interno della finestra. Osserva nell’esempio che il `WINDOW` è configurato con un frame di `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` impostazione dell&#39;ADF per esaminare la riga corrente e tutte le righe successive.

**Sintassi della query**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{KEY}` | La colonna o il campo dell’evento. |
| `{SHIFT}` | (Facoltativo) Il numero di eventi lontani dall’evento corrente. Per impostazione predefinita, il valore è 1. |
| `{IGNORE_NULLS}` | (Facoltativo) Valore booleano che indica se null `{KEY}` i valori devono essere ignorati. Per impostazione predefinita, il valore è `false`. |

Una spiegazione dei parametri all&#39;interno del `OVER()` è disponibile nella sezione [sezione funzioni finestra](#window-functions).

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

Per la query di esempio specificata, i risultati sono riportati nella `previous_page` colonna. Il valore all’interno del `previous_page` si basa sulla colonna `{KEY}` utilizzato nell&#39;ADF.

## Intervallo di tempo

Intervallo di tempo consente di esplorare il comportamento latente del cliente entro un determinato periodo di tempo prima o dopo il verificarsi di un evento.

### Intervallo di tempo tra la corrispondenza precedente

Questa query restituisce un numero che rappresenta l’unità di tempo trascorsa dalla visualizzazione dell’evento corrispondente precedente. Se non è stato trovato alcun evento corrispondente, restituisce null.

**Sintassi della query**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Un campo marca temporale trovato nel set di dati popolato su tutti gli eventi. |
| `{EVENT_DEFINITION}` | L’espressione per qualificare l’evento precedente. |
| `{TIME_UNIT}` | L’unità di output. I valori possibili includono giorni, ore, minuti e secondi. Per impostazione predefinita, il valore è secondi. |

Una spiegazione dei parametri all&#39;interno del `OVER()` è disponibile nella sezione [sezione funzioni finestra](#window-functions).

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

Per la query di esempio specificata, i risultati sono riportati nella `average_minutes_since_registration` colonna. Il valore all’interno del `average_minutes_since_registration` è la differenza di tempo tra gli eventi corrente e precedente. L’unità di tempo è stata definita in precedenza nel `{TIME_UNIT}`.

### Intervallo di tempo tra la corrispondenza successiva

Questa query restituisce un numero negativo che rappresenta l’unità di tempo che precede l’evento corrispondente successivo. Se non viene trovato un evento corrispondente, viene restituito null.

**Sintassi della query**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TIMESTAMP}` | Un campo marca temporale trovato nel set di dati popolato su tutti gli eventi. |
| `{EVENT_DEFINITION}` | L’espressione per qualificare l’evento successivo. |
| `{TIME_UNIT}` | (Facoltativo) L’unità di output. I valori possibili includono giorni, ore, minuti e secondi. Per impostazione predefinita, il valore è secondi. |

Una spiegazione dei parametri all&#39;interno del `OVER()` è disponibile nella sezione [sezione funzioni finestra](#window-functions).

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

Per la query di esempio specificata, i risultati sono riportati nella `average_minutes_until_order_confirmation` colonna. Il valore all’interno del `average_minutes_until_order_confirmation` è la differenza di tempo tra l&#39;evento corrente e quello successivo. L’unità di tempo è stata definita in precedenza nel `{TIME_UNIT}`.

## Passaggi successivi

Utilizzando le funzioni descritte qui, puoi scrivere query per accedere a [!DNL Experience Event] set di dati tramite [!DNL Query Service]. Per ulteriori informazioni sull’authoring delle query in [!DNL Query Service], consulta la documentazione su [creazione di query](../best-practices/writing-queries.md).

## Risorse aggiuntive

Il video seguente illustra come eseguire query nell’interfaccia di Adobe Experience Platform e in un client PSQL. Inoltre, il video utilizza anche esempi che coinvolgono singole proprietà in un oggetto XDM, utilizzando funzioni definite da Adobe e utilizzando CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
