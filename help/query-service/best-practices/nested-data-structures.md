---
keywords: Experience Platform;servizio query;servizio query;strutture dati nidificate;dati nidificati;
title: Utilizzo delle strutture dati nidificate nel servizio query
description: Questo documento fornisce un esempio di lavoro per l’elaborazione e la trasformazione di campi di dati nidificati utilizzando le istruzioni CTAS e INSERT INTO.
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# Utilizzo delle strutture dati nidificate nel servizio query

Adobe Experience Platform Query Service supporta l’utilizzo di campi di dati nidificati. La complessità delle strutture di dati aziendali può rendere complicata la trasformazione o l’elaborazione di tali dati. Questo documento fornisce esempi su come creare, elaborare o trasformare set di dati con tipi di dati complessi, incluse le strutture di dati nidificate.

Il servizio di query fornisce un [!DNL PostgreSQL] interfaccia per eseguire query SQL su tutti i set di dati gestiti da Experience Platform. Platform supporta l’utilizzo di tipi di dati primitivi o complessi nelle colonne di tabelle quali struttura, array, mappe e strutture, array e mappe profondamente nidificate. I set di dati possono inoltre contenere strutture nidificate in cui il tipo di dati della colonna può essere complesso quanto una matrice di strutture nidificate, o una mappa di mappe in cui il valore di una coppia chiave-valore può essere una struttura con più livelli di nidificazione.

## Introduzione

Questa esercitazione richiede l’utilizzo di un client PSQL di terze parti o dello strumento Editor query per scrivere, convalidare ed eseguire query all’interno dell’interfaccia utente (UI) di Experience Platform. Per informazioni dettagliate su come eseguire le query tramite l’interfaccia utente, consulta [Guida all’interfaccia utente dell’editor delle query](../ui/user-guide.md). Per un elenco dettagliato in cui i client desktop di terze parti possono connettersi a Query Service, consulta [panoramica delle connessioni client](../clients/overview.md).

Dovrebbe anche avere una buona comprensione del `INSERT INTO` e `CTAS` sintassi. Informazioni specifiche sul loro utilizzo sono disponibili nella [`INSERT INTO`](../sql/syntax.md#insert-into) e [`CTAS`](../sql/syntax.md#create-table-as-select) sezioni [Documentazione di riferimento della sintassi SQL](../sql/syntax.md).

## Creare un set di dati

Il servizio Query fornisce la Crea tabella come selezione (`CTAS`) per creare una tabella basata sull’output di una `SELECT` o, come in questo caso, utilizzando un riferimento a uno schema XDM esistente in Adobe Experience Platform. Di seguito è riportato lo schema XDM per `Final_subscription` creato per questo esempio.

![Diagramma dello schema final_subscription.](../images/best-practices/final-subscription-schema.png)

Nell&#39;esempio seguente viene illustrato l&#39;SQL utilizzato per creare il `final_subscription_test2` set di dati. `final_subscription_test2` viene creato utilizzando `Final_subscription` schema. I dati vengono estratti dall’origine utilizzando un `SELECT` per compilare alcune righe.

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

Nel set di dati iniziale `final_subscription_test2`, il tipo di dati struct viene utilizzato per contenere sia il `subscription` e `userid` che è univoco per ogni utente. La `subscription` Il campo descrive gli abbonamenti ai prodotti per un utente. Possono essere presenti più abbonamenti, ma una tabella può contenere solo le informazioni per un abbonamento per riga.

## Utilizzare INSERT INTO per aggiornare i campi dati nidificati

Dopo la `final_subscription_test2` è stato creato il set di dati, `INSERT INTO` viene utilizzata per aggiungere dati aggiuntivi alla tabella. Durante la copia dei dati, i tipi di dati nell’origine e nella destinazione devono corrispondere. In alternativa, il tipo di dati di origine deve essere `CAST` al tipo di dati di destinazione. I dati incrementali vengono quindi aggiunti al set di dati di destinazione utilizzando il seguente SQL.

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

Per trovare l&#39;elenco delle sottoscrizioni attive di un utente da un set di dati, è necessario scrivere una query che separa gli elementi di una matrice in più righe e colonne. A questo scopo, è innanzitutto necessario comprendere la forma del modello dati in quanto le informazioni di sottoscrizione vengono mantenute all’interno di una matrice nidificata all’interno del set di dati.

PSQL `\d` viene utilizzato per navigare a livello in base ai dati di sottoscrizione richiesti. Le tabelle illustrano la struttura `final_subscription_test2` set di dati. I tipi di dati complessi possono essere riconosciuti immediatamente perché non sono valori di tipo tipici come testo, booleano, timestamp, ecc.

| Colonna | Tipo |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

I campi della colonna successiva vengono visualizzati utilizzando `\d final_subscription_test2__lumaservices3` comando.

| Colonna | Tipo |
|---------|-------|
| `userid` | text |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` è una matrice di elementi di struttura. I relativi campi vengono visualizzati utilizzando la `\d _lumaservices3_subscription_e[]` comando.

| Colonna | Tipo |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | text |
| `offer_id` | text |
| `subscription_id` | text |

Per eseguire una query sui campi nidificati della sottoscrizione, è innanzitutto necessario separare gli elementi della `subscription` in più righe e restituire i risultati utilizzando la funzione esplodi. L&#39;esempio SQL seguente restituisce la sottoscrizione attiva per un utente basato su `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

Questa soluzione semplificata di esempio consente solo un abbonamento utente attivo. Realisticamente, ci possono essere molti abbonamenti attivi per un singolo utente. L’esempio seguente modifica la query precedente per consentire più sottoscrizioni attive simultanee.

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

Nonostante la crescente complessità di questo esempio SQL, la `collect_list` per gli abbonamenti attivi non garantisce che l&#39;output sarà nello stesso ordine dell&#39;origine. Per creare un elenco di sottoscrizioni attive per un utente, è necessario utilizzare GROUP BY o shuffling per aggregare i risultati dell’elenco.

## Passaggi successivi

La lettura di questo documento illustra come elaborare o trasformare set di dati che utilizzano tipi di dati complessi in Adobe Experience Platform Query Service. Vedi la [istruzioni per l’esecuzione delle query](./writing-queries.md) per ulteriori informazioni sull&#39;esecuzione di query SQL sui set di dati all&#39;interno del Data Lake.
