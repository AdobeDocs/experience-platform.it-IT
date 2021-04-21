---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;deduplicazione dei dati;deduplicazione;
solution: Experience Platform
title: Deduplicazione dati nel servizio query
topic-legacy: queries
type: Tutorial
description: Questo documento illustra esempi di query di esempio completo e di sottoselezione per la deduplicazione di tre casi d’uso comuni Eventi di esperienza, acquisti e metriche.
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Deduplicazione dati in [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] supporta la deduplicazione dei dati. La deduplicazione dei dati può essere eseguita quando è necessario rimuovere un’intera riga da un calcolo o ignorare un set specifico di campi, perché solo parte dei dati nella riga sono informazioni duplicate.

La deduplicazione comporta solitamente l’utilizzo della funzione `ROW_NUMBER()` in una finestra per individuare un ID (o una coppia di ID) nel tempo ordinato, che restituisce un nuovo campo che rappresenta il numero di volte in cui è stato rilevato un duplicato. L’ora è spesso rappresentata utilizzando il campo [!DNL Experience Data Model] (XDM) `timestamp` .

Quando il valore di `ROW_NUMBER()` è `1`, si riferisce all&#39;istanza originale. Generalmente, questo è l&#39;esempio che si desidera utilizzare. Nella maggior parte dei casi, questa operazione viene eseguita all’interno di una sottoselezione in cui la deduplicazione viene eseguita in un livello più alto `SELECT`, come per l’esecuzione di un conteggio aggregato.

I casi di utilizzo della deduplicazione possono essere globali o vincolati a un singolo utente o a un ID utente finale all&#39;interno di `identityMap`.

Questo documento illustra come eseguire la deduplicazione per tre casi d’uso comuni: Eventi di esperienza, acquisti e metriche.

Ogni esempio include l&#39;ambito, la chiave della finestra, un profilo del metodo di deduplicazione e l&#39;intera query SQL.

## Eventi esperienza {#experience-events}

Nel caso di eventi di esperienza duplicati, probabilmente ignorerai l’intera riga.

>[!CAUTION]
>
>Molti set di dati in [!DNL Experience Platform], inclusi quelli prodotti dal connettore dati Adobe Analytics, dispongono già della deduplicazione a livello di Experience-Event applicata. Pertanto, la riapplicazione di questo livello di deduplicazione non è necessaria e rallenta la query.
>
>È importante comprendere l’origine dei set di dati e sapere se è già stata applicata la deduplicazione a livello di Experience-Event. Per qualsiasi set di dati in streaming (ad esempio, quelli provenienti da Adobe Target), è necessario **will** applicare la deduplicazione a livello di Experience-Event, in quanto tali origini dati hanno semantica &quot;almeno una volta&quot;.

**Ambito:** globale

**Tasto finestra:** `id`

### Esempio di deduplicazione

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### Esempio completo

```sql
SELECT COUNT(*) AS num_events FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num
  FROM experience_events
) WHERE id_dup_num = 1
```

## Acquisti {#purchases}

Se hai acquisti duplicati, probabilmente desideri mantenere la maggior parte della riga Evento esperienza, ma ignora i campi associati all’acquisto (come la metrica `commerce.orders` ). Gli acquisti contengono un campo speciale per l’ID acquisto, che è `commerce.order.purchaseID`.

**Ambito:** visitatore

**Chiave finestra:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### Esempio di deduplicazione

```sql
SELECT *,
  IF(LENGTH(commerce.`order`.purchaseID) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, commerce.`order`.purchaseID
            ORDER BY timestamp ASC
      ),
    1) AS purchaseID_dup_num
FROM experience_events
```

### Esempio completo

```sql
SELECT SUM(commerce.purchases.value) AS num_purchases FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(commerce.`order`.purchaseID) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, commerce.order.purchaseID
              ORDER BY timestamp ASC
        ),
      1) AS purchaseID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND purchaseID_dup_num = 1
```

## Metriche {#metrics}

Se hai una metrica che utilizza l’ID univoco facoltativo e viene visualizzato un duplicato di tale ID, probabilmente ignorerai quel valore della metrica e mantieni il resto dell’evento esperienza.

In XDM, quasi tutte le metriche utilizzano il tipo di dati `Measure` che include un campo facoltativo `id` che può essere utilizzato per la deduplicazione.

**Ambito:** visitatore

**Chiave finestra: oggetto** identityMap[$NAMESPACE].id e id of Measure

### Esempio di deduplicazione

```sql
SELECT *,
  IF(LENGTH(application.launches.id) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
            ORDER BY timestamp ASC
      ),
    1) AS launchesID_dup_num
FROM experience_events
```

### Esempio completo

```sql
SELECT SUM(application.launches.value) AS num_launches FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(application.launches.id) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
              ORDER BY timestamp ASC
        ),
      1) AS launchesID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND launchesID_dup_num = 1
```

## Passaggi successivi

Questo documento illustra come eseguire la deduplicazione dei dati all’interno di Query Service, nonché esempi di deduplicazione dei dati. Per ulteriori best practice per la scrittura di query tramite Query Service, consulta la [guida alla scrittura di query](./writing-queries.md).
