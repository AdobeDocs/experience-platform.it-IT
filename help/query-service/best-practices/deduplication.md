---
keywords: ' Experience Platform;home;argomenti popolari;servizio query;servizio query;deduplicazione dei dati;deduplicazione;'
solution: Experience Platform
title: Deduplicazione dei dati
topic: queries
type: Tutorial
description: In questo documento sono riportati esempi di query di sottoselezione e di esempio completo per la deduplicazione di tre casi d’uso comuni Eventi esperienza, acquisti e metriche.
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# Deduplicazione dei dati in [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] supporta la deduplicazione dei dati. È possibile eseguire la deduplicazione dei dati quando è necessario rimuovere un&#39;intera riga da un calcolo o ignorare un insieme specifico di campi, perché solo parte dei dati nella riga è informazione duplicata.

La deduplicazione richiede in genere l&#39;utilizzo della funzione `ROW_NUMBER()` in una finestra per un ID (o una coppia di ID) nel tempo ordinato, che restituisce un nuovo campo che rappresenta il numero di volte in cui è stato rilevato un duplicato. Il tempo è spesso rappresentato utilizzando il campo [!DNL Experience Data Model] (XDM) `timestamp`.

Quando il valore di `ROW_NUMBER()` è `1`, si riferisce all&#39;istanza originale. In genere, si tratta dell’esempio che si desidera utilizzare. Questa operazione viene spesso eseguita all&#39;interno di una sottoselezione, dove la deduplicazione viene eseguita in un livello superiore `SELECT`, come per l&#39;esecuzione di un conteggio aggregato.

I casi di utilizzo della deduplicazione possono essere globali o vincolati a un singolo utente o a un ID utente finale all&#39;interno di `identityMap`.

In questo documento viene illustrato come eseguire la deduplicazione per tre casi d’uso comuni: Eventi esperienza, acquisti e metriche.

Ogni esempio include l&#39;ambito, la chiave della finestra, un profilo del metodo di deduplicazione, nonché la query SQL completa.

## Eventi esperienza {#experience-events}

Nel caso di eventi esperienza duplicati, è probabile che si desideri ignorare l&#39;intera riga.

>[!CAUTION]
>
>Molti set di dati in [!DNL Experience Platform], inclusi quelli prodotti dal Connettore dati Adobe Analytics , dispongono già di una deduplicazione a livello di esperienza. Pertanto, la riapplicazione di questo livello di deduplicazione non è necessaria e rallenta la query.
>
>È importante comprendere l&#39;origine dei set di dati e sapere se è già stata applicata la deduplicazione a livello di Experience-Event. Per tutti i set di dati in streaming (ad esempio, quelli provenienti da  Adobe Target), **sarà** necessario applicare la deduplicazione a livello di esperienza, poiché tali origini dati hanno una semantica &quot;almeno una volta&quot;.

**Ambito:** Globale

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

### Full example

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

Se disponete di acquisti duplicati, è probabile che desideriate mantenere la maggior parte della riga Evento esperienza, ma ignorare i campi associati all&#39;acquisto (ad esempio la metrica `commerce.orders`). Gli acquisti contengono un campo speciale per l&#39;ID acquisto, che è `commerce.order.purchaseID`.

**Ambito:** Visitatore

**Chiave della finestra:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

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

### Full example

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

Se hai una metrica che utilizza l&#39;ID univoco facoltativo e viene visualizzato un duplicato di tale ID, probabilmente vorrai ignorare tale valore della metrica e mantenere il resto dell&#39;Evento esperienza.

In XDM, quasi tutte le metriche utilizzano il tipo di dati `Measure` che include un campo opzionale `id` utilizzabile per la deduplicazione.

**Ambito:** Visitatore

**Chiave della finestra:oggetto** identityMap[$NAMESPACE].id e id of Measure

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

### Full example

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

Questo documento descrive come eseguire la deduplicazione dei dati in Query Service, nonché esempi di deduplicazione dei dati. Per ulteriori procedure ottimali per la scrittura di query tramite Query Service, consultare la [guida alla scrittura di query](./writing-queries.md).