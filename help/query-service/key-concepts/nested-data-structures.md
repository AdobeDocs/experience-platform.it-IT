---
keywords: Experience Platform;servizio query;servizio query;strutture dati nidificate;dati nidificati;query service;Query service;nested data structures;nested data;
title: Utilizzo delle strutture di dati nidificati in Query Service
description: In questo documento viene fornito un esempio di funzionamento per l'elaborazione e la trasformazione di campi dati nidificati mediante istruzioni CTAS e INSERT INTO.
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 2%

---

# Utilizzo delle strutture di dati nidificati in Query Service

Adobe Experience Platform Query Service supporta l’utilizzo di campi dati nidificati. La complessità delle strutture di dati aziendali può complicare la trasformazione o l&#39;elaborazione di tali dati. Questo documento fornisce esempi su come creare, elaborare o trasformare set di dati con tipi di dati complessi, comprese le strutture di dati nidificate.

Query Service fornisce un&#39;interfaccia [!DNL PostgreSQL] per eseguire query SQL su tutti i set di dati gestiti da Experience Platform. Platform supporta l’utilizzo di tipi di dati primitivi o complessi nelle colonne di tabella, ad esempio struct, array, mappe e strutture, array e mappe annidati in profondità. I set di dati possono anche contenere strutture nidificate in cui il tipo di dati della colonna può essere complesso come una matrice di strutture nidificate o una mappa di mappe in cui il valore di una coppia chiave-valore può essere una struttura con più livelli di nidificazione.

## Introduzione

Questo tutorial richiede l’utilizzo di un client PSQL di terze parti o dello strumento editor di query per scrivere, convalidare ed eseguire query nell’interfaccia utente di Experience Platform. Per informazioni dettagliate su come eseguire query tramite l&#39;interfaccia utente, consulta la [guida dell&#39;interfaccia utente di Query Editor](../ui/user-guide.md). Per un elenco dettagliato dei client desktop di terze parti che possono connettersi a Query Service, vedere la [panoramica delle connessioni client](../clients/overview.md).

È inoltre necessario avere una buona conoscenza della sintassi `INSERT INTO` e `CTAS`. Informazioni specifiche sul loro utilizzo sono disponibili nelle sezioni [`INSERT INTO`](../sql/syntax.md#insert-into) e [`CTAS`](../sql/syntax.md#create-table-as-select) della [documentazione di riferimento sulla sintassi SQL](../sql/syntax.md).

## Creare un set di dati

Il servizio Query fornisce la funzionalità Create Table As Select (`CTAS`) per creare una tabella basata sull&#39;output di un&#39;istruzione `SELECT` oppure, come in questo caso, utilizzando un riferimento a uno schema XDM esistente in Adobe Experience Platform. Di seguito è riportato lo schema XDM per `Final_subscription` creato per questo esempio.

![Diagramma dello schema final_subscription.](../images/best-practices/final-subscription-schema.png)

Nell&#39;esempio seguente viene illustrato l&#39;SQL utilizzato per creare il set di dati `final_subscription_test2`. `final_subscription_test2` viene creato utilizzando lo schema `Final_subscription`. I dati vengono estratti dall&#39;origine utilizzando una clausola `SELECT` per compilare alcune righe.

```sql
CREATE TABLE final_subscription_test2 with(schema='Final_subscription') AS (
        SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM (
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

Nel set di dati iniziale `final_subscription_test2`, il tipo di dati struct viene utilizzato per contenere sia il campo `subscription` che il `userid`, che è univoco per ogni utente. Il campo `subscription` descrive le sottoscrizioni di prodotti per un utente. Possono esistere più sottoscrizioni, ma una tabella può contenere solo le informazioni relative a una sottoscrizione per riga.

## Utilizzare INSERT INTO per aggiornare i campi dati nidificati

Dopo la creazione del set di dati `final_subscription_test2`, l&#39;istruzione `INSERT INTO` viene utilizzata per aggiungere dati aggiuntivi alla tabella. Quando si copiano i dati, i tipi di dati in origine e destinazione devono corrispondere. In alternativa, il tipo di dati di origine deve essere `CAST` per il tipo di dati di destinazione. I dati incrementali vengono quindi aggiunti al set di dati di destinazione utilizzando l’istruzione SQL seguente.

```sql
INSERT INTO final_subscription_test
      SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM  SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , timestamp eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

## Elabora dati da un set di dati nidificato

Per individuare l’elenco delle sottoscrizioni attive di un utente da un set di dati, è necessario scrivere una query che separi gli elementi di un array in più righe e colonne. A questo scopo, devi innanzitutto comprendere la forma del modello dati, in quanto le informazioni di abbonamento vengono mantenute all’interno di un array nidificato all’interno del set di dati.

Il comando PSQL `\d` viene utilizzato per spostarsi a livello dei dati di sottoscrizione richiesti. Le tabelle illustrano la struttura del set di dati `final_subscription_test2`. I tipi di dati complessi possono essere riconosciuti a colpo d’occhio perché non sono valori di tipo tipici come testo, booleano, marca temporale, ecc.

| Colonna | Tipo |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

I campi della colonna successiva vengono visualizzati utilizzando il comando `\d final_subscription_test2__lumaservices3`.

| Colonna | Tipo |
|---------|-------|
| `userid` | testo |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` è una matrice di elementi struct. I relativi campi vengono visualizzati utilizzando il comando `\d _lumaservices3_subscription_e[]`.

| Colonna | Tipo |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | testo |
| `offer_id` | testo |
| `subscription_id` | testo |

Per eseguire una query sui campi nidificati della sottoscrizione, è innanzitutto necessario separare gli elementi dell&#39;array `subscription` in più righe e restituire i risultati utilizzando la funzione di esplosione. Nell&#39;esempio SQL seguente viene restituita la sottoscrizione attiva per un utente basato su `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

Questa soluzione di esempio semplificata consente un solo abbonamento utente attivo. Realisticamente, ci possono essere molti abbonamenti attivi per un singolo utente. L’esempio seguente modifica la query precedente per consentire più abbonamenti attivi simultanei.

```sql
SELECT userid, collect_list(subs) AS active_subscriptions FROM (
     SELECT
          _lumaservices3.userid AS userid,
          explode(_lumaservices3.subscription) AS subs
     FROM final_subscription_test2
     )
WHERE subs.last_status='Active' 
GROUP BY userid ;
```

Nonostante la crescente complessità di questo esempio SQL, `collect_list` per le sottoscrizioni attive non garantisce che l&#39;output sia nello stesso ordine dell&#39;origine. Per creare un elenco di sottoscrizioni attive per un utente, è necessario utilizzare GROUP BY o miscelazione per aggregare i risultati dell&#39;elenco.

## Passaggi successivi

Una volta letto questo documento, sarai in grado di elaborare o trasformare set di dati che utilizzano tipi di dati complessi in Adobe Experience Platform Query Service. Per ulteriori informazioni sull&#39;esecuzione di query SQL sui set di dati nel Data Lake, vedere le [istruzioni per l&#39;esecuzione di query](../best-practices/writing-queries.md).
