---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Deduplicazione dei dati
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Deduplicazione dei dati in [!DNL Query Service]

 Adobe Experience Platform [!DNL Query Service] supporta la deduplicazione dei dati quando potrebbe essere necessario rimuovere un&#39;intera riga da un calcolo o ignorare un set specifico di campi, perché solo parte dei dati nella riga è un duplicato. Il pattern comune per la deduplicazione prevede l&#39;uso della `ROW_NUMBER()` funzione in una finestra per un ID, o una coppia di ID, nel tempo ordinato (utilizzando il campo [!DNL Experience Data Model] (XDM) `timestamp` ) per restituire un nuovo campo che rappresenta il numero di volte in cui è stato rilevato un duplicato. Quando questo valore è `1`, si riferisce all&#39;istanza originale e, nella maggior parte dei casi, all&#39;istanza che si desidera utilizzare, ignorando ogni altra istanza. Nella maggior parte dei casi, questa operazione viene eseguita all&#39;interno di una sottoselezione, in cui la deduplicazione viene eseguita in un livello superiore, `SELECT` come per esempio l&#39;esecuzione di un conteggio aggregato.

## Casi di utilizzo

Alcuni casi di utilizzo per la deduplicazione sono globali nell’intervallo di date e alcuni sono vincolati a un singolo visitatore o a un ID utente finale all’interno dell’ `identityMap`.

In questo documento sono riportati esempi di query di selezione secondaria e di esempio completo per la deduplicazione di tre casi d’uso comuni:
- [ExperienceEvents](#experienceevents)
- [Acquisti](#purchases)
- [Metriche](#metrics)

### ExperienceEvents {#experienceevents}

Nel caso di ExperienceEvents duplicati, probabilmente si desidera ignorare l’intera riga.

>[!CAUTION]
>
>Molti DataSet in [!DNL Experience Platform], inclusi quelli prodotti da Adobe  Analytics Data Connector, dispongono già della deduplicazione a livello di ExperienceEvent. Pertanto, la riapplicazione di questo livello di deduplicazione non è necessaria e rallenta la query. È importante comprendere l’origine dei DataSet e sapere se è già stata applicata la deduplicazione a livello di ExperienceEvent. Per qualsiasi DataSet trasmesso in streaming (ad esempio, quelli provenienti da  Adobe Target), dovrete applicare la deduplicazione a livello ExperienceEvent perché tali origini dati hanno una semantica &quot;almeno una volta&quot;.

**Ambito:** Globale

**Tasto finestra:** id

#### Sottoselezione

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

#### Full example

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

### Acquisti {#purchases}

Se disponete di acquisti duplicati, è probabile che desideriate mantenere la maggior parte della riga ExperienceEvent, ma ignorare i campi associati all’acquisto (ad esempio la `commerce.orders` metrica). Per gli acquisti, esiste un campo speciale per l&#39;ID acquisto. Questo campo è `commerce.order.purchaseID`.

**Ambito:** Visitatore

**Tasto finestra:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

#### Sottoselezione

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

#### Full example

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

### Metriche {#metrics}

Se hai una metrica che utilizza l’ID univoco facoltativo e viene visualizzato un duplicato di tale ID, probabilmente vorrai ignorare tale valore della metrica e mantenere il resto dell’ExperienceEvent. In XDM, quasi tutte le metriche utilizzano il tipo di `Measure` dati che include un `id` campo facoltativo da utilizzare per la deduplicazione.

**Ambito:** Visitatore

**Tasto finestra:** oggetto identityMap[$NAMESPACE].id e id of Measure

#### Sottoselezione

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

#### Full example

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
