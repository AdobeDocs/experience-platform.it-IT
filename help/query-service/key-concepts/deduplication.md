---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;deduplicazione dati;deduplicazione;
solution: Experience Platform
title: Deduplicazione dei dati in Query Service
type: Tutorial
description: 'Questo documento illustra alcuni esempi di query di esempio completi e di selezione secondaria per la deduplicazione di tre casi d’uso comuni: Eventi di esperienza, acquisti e metriche.'
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Deduplicazione dei dati in [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] supporta la deduplicazione dei dati. La deduplicazione dei dati può essere eseguita quando è necessario rimuovere un’intera riga da un calcolo o ignorare un set specifico di campi, perché solo una parte dei dati nella riga sono informazioni duplicate.

La deduplicazione comporta in genere l&#39;utilizzo della funzione `ROW_NUMBER()` in una finestra per un ID (o una coppia di ID) nel tempo ordinato, che restituisce un nuovo campo che rappresenta il numero di volte in cui è stato rilevato un duplicato. L&#39;ora viene spesso rappresentata utilizzando il campo `timestamp` di [!DNL Experience Data Model] (XDM).

Quando il valore di `ROW_NUMBER()` è `1`, fa riferimento all&#39;istanza originale. In genere, è questa l’istanza che desideri utilizzare. Questa operazione viene eseguita il più delle volte all&#39;interno di una sottoselezione in cui la deduplicazione viene eseguita in un `SELECT` di livello superiore, come l&#39;esecuzione di un conteggio aggregato.

I casi di utilizzo di deduplicazione possono essere globali o vincolati a un singolo utente o ID utente finale all&#39;interno di `identityMap`.

Questo documento illustra come eseguire la deduplicazione per tre casi d’uso comuni: eventi di esperienza, acquisti e metriche.

Ogni esempio include l&#39;ambito, la chiave della finestra, una struttura del metodo di deduplicazione e la query SQL completa.

## Eventi esperienza {#experience-events}

Nel caso di eventi di esperienza duplicati, è probabile che si desideri ignorare l’intera riga.

>[!CAUTION]
>
>A molti set di dati in [!DNL Experience Platform], inclusi quelli prodotti dal connettore dati di Adobe Analytics, è già stata applicata la deduplicazione a livello di Experience-Event. Pertanto, la riapplicazione di questo livello di deduplicazione non è necessaria e rallenterà la query.
>
>È importante comprendere l’origine dei set di dati e sapere se la deduplicazione a livello di Experience-Event è già stata applicata. Per qualsiasi set di dati inviato in streaming (ad esempio, quelli di Adobe Target), **sarà** necessario applicare la deduplicazione a livello di Experience-Event, poiché tali origini di dati hanno semantica &quot;almeno una volta&quot;.

**Ambito:** Globale

**Chiave finestra:** `id`

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

Se hai acquisti duplicati, probabilmente vorrai mantenere la maggior parte della riga [!DNL Experience Event], ma ignorare i campi associati all&#39;acquisto (ad esempio la metrica `commerce.orders`). Gli acquisti contengono un campo speciale per l&#39;ID acquisto, che è `commerce.order.purchaseID`.

Si consiglia di utilizzare `purchaseID` nell&#39;ambito del visitatore, in quanto è il campo semantico standard per gli ID acquisto in XDM. L’ambito del visitatore è consigliato per la rimozione dei dati di acquisto duplicati, in quanto la query è più rapida rispetto all’utilizzo dell’ambito globale ed è improbabile che un ID acquisto venga duplicato su più ID visitatore.

**Ambito:** Visitatore

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

>[!NOTE]
>
>In alcuni casi in cui i dati Analytics originali presentano ID acquisto duplicati per gli ID visitatore, **maggio** deve eseguire il conteggio dei duplicati degli ID acquisto per tutti i visitatori. Quando l’ID acquisto non è presente, questo metodo richiede di includere una condizione che utilizza invece l’ID evento per mantenere la query il più veloce possibile.

### Esempio completo

L’esempio seguente utilizza una clausola condizionale per utilizzare l’ID evento nel caso in cui l’ID acquisto non sia presente.

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

Se disponi di una metrica che utilizza l’ID univoco facoltativo e viene visualizzato un duplicato di tale ID, è probabile che tu voglia ignorare tale valore della metrica e mantenere il resto dell’evento esperienza.

In XDM, quasi tutte le metriche utilizzano il tipo di dati `Measure` che include un campo `id` facoltativo che può essere utilizzato per la deduplicazione.

**Ambito:** Visitatore

**Chiave finestra:** identityMap[$NAMESPACE].id e ID dell&#39;oggetto Measure

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

Questo documento fornisce esempi di deduplicazione dei dati e illustra come eseguire la deduplicazione dei dati in Query Service. Per ulteriori best practice per la scrittura di query tramite Query Service, leggere la [guida alla scrittura di query](../best-practices/writing-queries.md).
