---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;deduplicazione dei dati;deduplicazione;
solution: Experience Platform
title: Deduplicazione dati nel servizio query
topic-legacy: queries
type: Tutorial
description: Questo documento illustra esempi di query di esempio completo e di sottoselezione per la deduplicazione di tre casi d’uso comuni Eventi di esperienza, acquisti e metriche.
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: b140037ed5f055a8e7c583540910cc6b18bbf0bd
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# Deduplicazione dati in [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] supporta la deduplicazione dei dati. La deduplicazione dei dati può essere eseguita quando è necessario rimuovere un’intera riga da un calcolo o ignorare un set specifico di campi, perché solo parte dei dati nella riga sono informazioni duplicate.

La deduplicazione comporta in genere l’utilizzo del `ROW_NUMBER()` funziona in una finestra per individuare un ID (o una coppia di ID) nel tempo ordinato, che restituisce un nuovo campo che rappresenta il numero di volte in cui è stato rilevato un duplicato. L’ora è spesso rappresentata utilizzando la variabile [!DNL Experience Data Model] (XDM) `timestamp` campo .

Quando il valore di `ROW_NUMBER()` è `1`, si riferisce all&#39;istanza originale. Generalmente, questo è l&#39;esempio che si desidera utilizzare. Nella maggior parte dei casi, questa operazione viene eseguita all’interno di una sottoselezione in cui la deduplicazione viene eseguita in un livello superiore `SELECT` come eseguire un conteggio aggregato.

I casi di utilizzo della deduplicazione possono essere globali o vincolati a un singolo utente o a un ID utente finale all’interno della `identityMap`.

Questo documento illustra come eseguire la deduplicazione per tre casi d’uso comuni: Eventi di esperienza, acquisti e metriche.

Ogni esempio include l&#39;ambito, la chiave della finestra, un profilo del metodo di deduplicazione e l&#39;intera query SQL.

## Eventi esperienza {#experience-events}

Nel caso di eventi di esperienza duplicati, probabilmente ignorerai l’intera riga.

>[!CAUTION]
>
>Molti set di dati in [!DNL Experience Platform], inclusi quelli prodotti da Adobe Analytics Data Connector, dispongono già della deduplicazione a livello di Experience-Event. Pertanto, la riapplicazione di questo livello di deduplicazione non è necessaria e rallenta la query.
>
>È importante comprendere l’origine dei set di dati e sapere se è già stata applicata la deduplicazione a livello di Experience-Event. Per tutti i set di dati trasmessi in streaming (ad esempio quelli provenienti da Adobe Target), **sarà** è necessario applicare la deduplicazione a livello di Experience-Event, poiché queste origini dati hanno semantica &quot;almeno una volta&quot;.

**Ambito di applicazione:** Globale

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

Se si dispone di acquisti duplicati, è probabile che si desidera mantenere la maggior parte dei [!DNL Experience Event] ma ignora i campi associati all’acquisto (ad esempio `commerce.orders` metrica). Gli acquisti contengono un campo speciale per l&#39;ID acquisto, ovvero `commerce.order.purchaseID`.

Si consiglia di utilizzare `purchaseID` nell’ambito del visitatore, in quanto è il campo semantico standard per gli ID acquisto in XDM. L’ambito del visitatore è consigliato per la rimozione dei dati di acquisto duplicati, perché la query è più veloce rispetto all’ambito globale ed è improbabile che un ID di acquisto sia duplicato su più ID visitatore.

**Ambito di applicazione:** Visitatore

**Tasto finestra:** identityMap[$NAMESPACE].id e commerce.order.purchaseID

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

>[!NOTE]
>
>In alcuni casi in cui i dati originali di Analytics presentano ID di acquisto duplicati tra gli ID visitatore, l’utente **possono** deve eseguire il conteggio duplicato dell&#39;ID acquisto per tutti i visitatori. Quando l’ID acquisto non è presente, questo metodo richiede di includere una condizione che utilizzi invece l’ID evento per mantenere la query il più veloce possibile.

### Esempio completo

Nell’esempio seguente viene utilizzata una clausola di condizione per utilizzare l’ID evento nel caso in cui l’ID acquisto non sia presente.

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

In XDM, quasi tutte le metriche utilizzano il `Measure` tipo di dati che include un `id` campo che è possibile utilizzare per la deduplicazione.

**Ambito di applicazione:** Visitatore

**Tasto finestra:** identityMap[$NAMESPACE]oggetto .id e id della misura

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

Questo documento illustra come eseguire la deduplicazione dei dati all’interno di Query Service, nonché esempi di deduplicazione dei dati. Per ulteriori best practice per la scrittura di query tramite Query Service, consulta [guida alla scrittura di query](./writing-queries.md).
