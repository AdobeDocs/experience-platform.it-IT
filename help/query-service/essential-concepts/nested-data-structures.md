---
keywords: Experience Platform;servizio query;servizio query;strutture dati nidificate;dati nidificati;query service;Query service;nested data structures;nested data;
title: Utilizzo delle strutture di dati nidificati in Query Service
description: In questo documento viene fornito un esempio di funzionamento per l'elaborazione e la trasformazione di campi dati nidificati mediante istruzioni CTAS e INSERT INTO.
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# Utilizzo delle strutture di dati nidificati in Query Service

Adobe Experience Platform Query Service supporta l’utilizzo di campi dati nidificati. La complessità delle strutture di dati aziendali può complicare la trasformazione o l&#39;elaborazione di tali dati. Questo documento fornisce esempi su come creare, elaborare o trasformare set di dati con tipi di dati complessi, comprese le strutture di dati nidificate.

Query Service fornisce una [!DNL PostgreSQL] interfaccia per eseguire query SQL su tutti i set di dati gestiti da Experience Platform. Platform supporta l’utilizzo di tipi di dati primitivi o complessi nelle colonne di tabella, ad esempio struct, array, mappe e strutture, array e mappe annidati in profondità. I set di dati possono anche contenere strutture nidificate in cui il tipo di dati della colonna può essere complesso come una matrice di strutture nidificate o una mappa di mappe in cui il valore di una coppia chiave-valore può essere una struttura con più livelli di nidificazione.

## Introduzione

Questo tutorial richiede l’utilizzo di un client PSQL di terze parti o dello strumento editor di query per scrivere, convalidare ed eseguire query nell’interfaccia utente di Experience Platform. Per informazioni complete su come eseguire query tramite l’interfaccia utente, consulta [Guida dell’interfaccia utente di Query Editor](../ui/user-guide.md). Per un elenco dettagliato dei client desktop di terze parti che possono connettersi a Query Service, vedi [panoramica delle connessioni client](../clients/overview.md).

Dovresti anche avere una buona comprensione del `INSERT INTO` e `CTAS` sintassi. Informazioni specifiche sul loro utilizzo sono reperibili nella [`INSERT INTO`](../sql/syntax.md#insert-into) e [`CTAS`](../sql/syntax.md#create-table-as-select) sezioni del [Documentazione di riferimento sulla sintassi SQL](../sql/syntax.md).

## Creare un set di dati

Il servizio Query fornisce il comando Crea tabella come selezionato (`CTAS`) per creare una tabella basata sull&#39;output di una `SELECT` o, come in questo caso, utilizzando un riferimento a uno schema XDM esistente in Adobe Experience Platform. Di seguito è riportato lo schema XDM per `Final_subscription` creato per questo esempio.

![Diagramma dello schema final_subscription.](../images/best-practices/final-subscription-schema.png)

L&#39;esempio seguente illustra l&#39;istruzione SQL utilizzata per creare `final_subscription_test2` set di dati. `final_subscription_test2` viene creato utilizzando `Final_subscription` schema. I dati vengono estratti dall’origine utilizzando una `SELECT` per compilare alcune righe.

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

Nel set di dati iniziale `final_subscription_test2`, il tipo di dati struct viene utilizzato per contenere entrambi `subscription` e `userid` che è univoco per ciascun utente. Il `subscription` descrive le sottoscrizioni di prodotti per un utente. Possono esistere più sottoscrizioni, ma una tabella può contenere solo le informazioni relative a una sottoscrizione per riga.

## Utilizzare INSERT INTO per aggiornare i campi dati nidificati

Dopo il `final_subscription_test2` set di dati creato, il `INSERT INTO` per aggiungere dati aggiuntivi alla tabella. Quando si copiano i dati, i tipi di dati in origine e destinazione devono corrispondere. In alternativa, il tipo di dati di origine deve essere `CAST` al tipo di dati di destinazione. I dati incrementali vengono quindi aggiunti al set di dati di destinazione utilizzando l’istruzione SQL seguente.

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

PSQL `\d` Il comando viene utilizzato per passare livello per livello ai dati di sottoscrizione richiesti. Le tabelle illustrano la struttura del `final_subscription_test2` set di dati. I tipi di dati complessi possono essere riconosciuti a colpo d’occhio perché non sono valori di tipo tipici come testo, booleano, marca temporale, ecc.

| Colonna | Tipo |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

I campi della colonna successiva vengono visualizzati utilizzando `\d final_subscription_test2__lumaservices3` comando.

| Colonna | Tipo |
|---------|-------|
| `userid` | testo |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` è un array di elementi struct. I relativi campi vengono visualizzati utilizzando `\d _lumaservices3_subscription_e[]` comando.

| Colonna | Tipo |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | testo |
| `offer_id` | testo |
| `subscription_id` | testo |

Per eseguire una query sui campi nidificati della sottoscrizione, è necessario innanzitutto separare gli elementi della `subscription` in più righe e restituire i risultati utilizzando la funzione explode. Nell&#39;esempio SQL seguente viene restituita la sottoscrizione attiva per un utente basata su `userid`.

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

Nonostante la crescente complessità di questo esempio SQL, `collect_list` per le sottoscrizioni attive non garantisce che l’output sia nello stesso ordine dell’origine. Per creare un elenco di sottoscrizioni attive per un utente, è necessario utilizzare GROUP BY o miscelazione per aggregare i risultati dell&#39;elenco.

## Passaggi successivi

Una volta letto questo documento, sarai in grado di elaborare o trasformare set di dati che utilizzano tipi di dati complessi in Adobe Experience Platform Query Service. Consulta la sezione [guida all’esecuzione delle query](../best-practices/writing-queries.md) per ulteriori informazioni sull’esecuzione di query SQL sui set di dati all’interno del Data Lake,
