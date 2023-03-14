---
title: 'Caso di utilizzo: attributi derivati basati su decile'
description: Questa guida illustra i passaggi necessari per utilizzare Query Service per creare attributi derivati basati su decile da utilizzare con i dati del profilo.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 2%

---

# Caso di utilizzo: attributi derivati basati su decile

Gli attributi derivati semplificano casi d’uso complicati per l’analisi di dati provenienti dal data lake che possono essere utilizzati con altri servizi Platform a valle o pubblicati nei dati del profilo cliente in tempo reale.

Questo caso d’uso di esempio illustra come creare attributi derivati basati su decile da utilizzare con i dati del profilo cliente in tempo reale. Utilizzando come esempio uno scenario di fidelizzazione di una compagnia aerea, questa guida ti spiega come creare un set di dati che utilizza decili per categoria per segmentare e creare tipi di pubblico in base agli attributi classificati.

Sono illustrati i seguenti concetti chiave:

* Creazione di schemi per il bucket decile.
* Creazione decile categorica.
* Creazione di attributi derivati complessi.
* Calcolo dei decili in un periodo di lookback.
* Una query di esempio per dimostrare l’aggregazione, la classificazione e l’aggiunta di identità univoche che consentono la generazione di tipi di pubblico in base a questi bucket di decile.

## Introduzione

Questa guida richiede una buona conoscenza di [esecuzione di query in Query Service](../best-practices/writing-queries.md) e i seguenti componenti di Adobe Experience Platform:

* [Panoramica del profilo cliente in tempo reale](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi.
* [Abilitare uno schema per Real-Time Customer Profile](../../profile/tutorials/add-profile-data.md): questa esercitazione illustra i passaggi necessari per aggiungere dati a Real-Time Customer Profile.
* [Come definire un tipo di dati personalizzato](../../xdm/api/data-types.md): i tipi di dati vengono utilizzati come campi del tipo di riferimento nelle classi o nei gruppi di campi dello schema e consentono l’utilizzo coerente di una struttura a più campi che può essere inclusa ovunque nello schema.

## Obiettivi

L’esempio fornito in questo documento utilizza i decili per creare attributi derivati per la classificazione dei dati da uno schema di fedeltà per compagnie aeree. Gli attributi derivati consentono di massimizzare l’utilità dei dati identificando un pubblico in base alla &quot;n&quot; % superiore per una categoria selezionata.

## Creare attributi derivati basati su decile

Per definire la classificazione dei decili in base a una dimensione particolare e a una metrica corrispondente, è necessario progettare uno schema per consentire il bucket decile.

Questa guida utilizza un set di dati sulla fedeltà delle compagnie aeree per dimostrare come utilizzare Query Service per creare decili in base alle miglia percorse in vari periodi di lookback.

## Utilizzare Query Service per creare decili

Query Service consente di creare un set di dati contenente decili per categoria, che possono quindi essere segmentati per creare tipi di pubblico in base alla classificazione degli attributi. I concetti visualizzati negli esempi seguenti possono essere applicati per creare altri set di dati a bucket decile, purché sia definita una categoria e sia disponibile una metrica.

L’esempio di dati sulla fedeltà delle compagnie aeree utilizza un [Classe XDM ExperienceEvents](../../xdm/classes/experienceevent.md). Ogni evento è una registrazione di una transazione commerciale per chilometraggio, accreditata o addebitata, e lo stato di fedeltà di appartenenza di &quot;Flyer&quot;, &quot;Frequent&quot;, &quot;Silver&quot; o &quot;Gold&quot;. Il campo dell’identità primaria è `membershipNumber`.

### Set di dati di esempio

Il set di dati iniziale sulla fedeltà della compagnia aerea per questo esempio è &quot;Dati sulla fedeltà della compagnia aerea&quot; e ha il seguente schema. L’identità primaria dello schema è `_profilefoundationreportingstg.membershipNumber`.

![Un diagramma dello schema Dati fedeltà compagnia aerea.](../images/use-cases/airline-loyalty-data.png)

**Dati di esempio**

Nella tabella seguente vengono visualizzati i dati di esempio contenuti nel `_profilefoundationreportingstg` oggetto utilizzato per questo esempio. Fornisce il contesto per l&#39;utilizzo di bucket decile per creare attributi derivati complessi.

>[!NOTE]
>
>Per brevità, l’ID tenant `_profilefoundationreportingstg` è stato omesso dall’inizio dello spazio dei nomi nei titoli delle colonne e nelle successive menzioni in tutto il documento.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | Nuovo membro | 5000 | VOLANTINO |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | ARGENTO |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | ARGENTO |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | ARGENTO |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | Nuova carta di credito | 10000 | VOLANTINO |

{style="table-layout:auto"}

## Generare set di dati decile

Nei dati sulla fedeltà delle compagnie aeree riportati sopra, la `.mileage` il valore contiene il numero di miglia percorse da un membro per ogni singolo volo effettuato. Questi dati vengono utilizzati per creare decili per il numero di miglia percorse durante i lookback a vita e per una varietà di periodi di lookback. A questo scopo, viene creato un set di dati che contiene decili in un tipo di dati mappa per ogni periodo di lookback e un decile appropriato per ogni periodo di lookback assegnato in `membershipNumber`.

Crea uno &quot;Schema del decile per la fedeltà della compagnia aerea&quot; per creare un set di dati decile utilizzando Query Service.

![Diagramma dello &quot;schema del decile della fedeltà della compagnia aerea&quot;.](../images/use-cases/airline-loyalty-decile-schema.png)

### Abilitare lo schema per Real-Time Customer Profile

I dati acquisiti in Experience Platform per l’utilizzo da parte di Real-Time Customer Profile devono essere conformi a [uno schema Experience Data Model (XDM) abilitato per il profilo](../../xdm/ui/resources/schemas.md). Per abilitare uno schema per il profilo, è necessario implementare la classe XDM Individual Profile o XDM ExperienceEvent.

[Abilita lo schema per l’utilizzo in Real-Time Customer Profile utilizzando lo Schema Registry API (API del registro degli schemi).](../../xdm/tutorials/create-schema-api.md) o [Interfaccia utente dell’Editor di schema](../../xdm/tutorials/create-schema-ui.md).  Le istruzioni dettagliate su come abilitare uno schema per il profilo sono disponibili nella rispettiva documentazione.

Quindi, crea un tipo di dati da riutilizzare per tutti i gruppi di campi correlati al decile. La creazione del gruppo di campi decile è un passaggio unico per sandbox. Può essere riutilizzato anche per tutti gli schemi relativi al decile.

### Creare uno spazio dei nomi delle identità e contrassegnarlo come identificatore primario {#identity-namespace}

A qualsiasi schema creato per l&#39;utilizzo con decili deve essere assegnata un&#39;identità primaria. È possibile [definire un campo di identità nell’interfaccia utente degli schemi di Adobe Experience Platform](../../xdm/ui/fields/identity.md#define-an-identity-field), o tramite [API del registro dello schema](../../xdm/api/descriptors.md#create).

Query Service consente inoltre di impostare un’identità o un’identità primaria per i campi di set di dati dello schema ad hoc direttamente tramite SQL. Consulta la documentazione su [impostazione di un’identità secondaria e primaria in identità di schema ad hoc](../data-governance/ad-hoc-schema-identities.md) per ulteriori informazioni.

### Creare una query per il calcolo dei decili in un periodo di lookback {#create-a-query}

L’esempio seguente illustra la query SQL per calcolare un decile in un periodo di lookback.

È possibile creare un modello utilizzando l’Editor query nell’interfaccia utente o tramite [API servizio query](../api/query-templates.md#create-a-query-template).

```sql
CREATE TABLE AS airline_loyality_decile 
{  WITH summed_miles_1 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
    ),
    summed_miles_3 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 1))
    GROUP BY 1,2
    ),
    summed_miles_6 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 4))
    GROUP BY 1,2
    ),
    rankings_1 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_1
    ),
    rankings_3 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_3
    ),
    rankings_6 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_6
    ),
    map_1 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
        FROM rankings_1
        GROUP BY membershipNumber
    ),
    map_3 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth3
        FROM rankings_3
        GROUP BY membershipNumber
    ),
    map_6 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth6
        FROM rankings_6
        GROUP BY membershipNumber
    ),
    all_memberships AS (
        SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
    )
    SELECT STRUCT(
            all_memberships.membershipNumber AS membershipNumber,
            STRUCT(
                    map_1.decileMonth1 AS decileMonth1,
                    map_3.decileMonth3 AS decileMonth3,
                    map_6.decileMonth6 AS decileMonth6
            ) AS decilesMileage
        ) AS _profilefoundationreportingstg
    FROM all_memberships
        LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
        LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
        LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
    }
```

### Revisione query

Le sezioni della query di esempio vengono esaminate più dettagliatamente di seguito.

#### Periodi di lookback

Il tipo di dati decile contiene un bucket per i lookback a 1, 3, 6, 9, 12 e durata. La query utilizza periodi di lookback di 1, 3 e 6 mesi, pertanto ogni sezione conterrà alcune query &quot;ripetute&quot; per creare tabelle temporanee per ogni periodo di lookback.

>[!NOTE]
>
>Se i dati di origine non dispongono di una colonna che può essere utilizzata per determinare un periodo di lookback, tutte le classificazioni delle classi decile verranno eseguite in `decileMonthAll`.

#### Aggregazione

Utilizza espressioni di tabella comuni (CTE, Common Table Expression) per aggregare il chilometraggio prima di creare periodi fissi. Questo fornisce i chilometri totali per un periodo di lookback specifico. I CTE esistono temporaneamente e sono utilizzabili solo nell’ambito della query più grande.

```sql
summed_miles_1 AS (
    SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
           _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
           SUM(_profilefoundationreportingstg.mileage) AS totalMiles
    FROM airline_loyalty_data
    WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
)
```

Il blocco viene ripetuto due volte nel modello (`summed_miles_3` e `summed_miles_6`) con una modifica nel calcolo della data al fine di generare i dati per gli altri periodi di lookback.

È importante notare le colonne di identità, dimensione e metrica per la query (`membershipNumber`, `loyaltyStatus` e `totalMiles` rispettivamente).

#### Classificazione

I decili consentono di eseguire il bucket categoriale. Per creare il numero di classificazione, `NTILE` viene utilizzata con un parametro di `10` in una FINESTRA raggruppata per `loyaltyStatus` campo. Questo si traduce in una classificazione da 1 a 10. Imposta il `ORDER BY` clausola del `WINDOW` a `DESC` per garantire che un valore di classificazione di `1` viene assegnato al **più grande** all’interno della dimensione.

```sql
rankings_1 AS (
    SELECT membershipNumber,
           loyaltyStatus,
           totalMiles,
           NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
    FROM summed_miles_1
)
```

#### Aggregazione mappa

Con più periodi di lookback, devi creare in anticipo le mappe del decile bucket utilizzando `MAP_FROM_ARRAYS` e `COLLECT_LIST` funzioni. Nello snippet di esempio: `MAP_FROM_ARRAYS` crea una mappa con una coppia di chiavi (`loyaltyStatus`) e valori (`decileBucket`). `COLLECT_LIST` restituisce un array con tutti i valori nella colonna specificata.

```sql
map_1 AS (
    SELECT membershipNumber,
           MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
    FROM rankings_1
    GROUP BY membershipNumber
)
```

>[!NOTE]
>
>L’aggregazione della mappa non è necessaria se la classificazione decile è richiesta solo per un periodo di vita.

#### Identità univoche

L’elenco delle identità univoche (`membershipNumber`) è necessario per creare un elenco univoco di tutte le appartenenze.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>Se la classificazione decile è necessaria solo per un periodo di durata, questo passaggio può essere omesso e l’aggregazione può essere eseguita da `membershipNumber` possono essere eseguite nel passaggio finale.

#### Unire tutti i dati temporanei

Il passaggio finale consiste nell’unire tutti i dati temporanei in un modulo identico alla struttura dei decili nel gruppo di campi.

```sql
SELECT STRUCT(
           all_memberships.membershipNumber AS membershipNumber,
           STRUCT(
                map_1.decileMonth1 AS decileMonth1,
                map_3.decileMonth3 AS decileMonth3,
                map_6.decileMonth6 AS decileMonth6
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM all_memberships
    LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
    LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
    LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
```

Se sono disponibili solo i dati relativi al ciclo di vita, la query verrà visualizzata come segue:

```sql
SELECT STRUCT(
           rankings.membershipNumber AS membershipNumber,
           STRUCT(
                MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonthAll
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM rankings
GROUP BY rankings.membershipNumber
```

Nei risultati della query viene garantita una correlazione tra il numero di classificazione e il percentile a causa dell’utilizzo di decili. Ogni classificazione equivale al 10%, pertanto l’identificazione di un pubblico in base al 30% più numeroso deve mirare solo ai livelli 1, 2 e 3.

### Eseguire il modello di query

Esegui la query per popolare il set di dati decile. Puoi anche salvare la query come modello e pianificarla per l’esecuzione a una cadenza. Quando viene salvata come modello, la query può anche essere aggiornata per utilizzare il pattern di creazione e inserimento che fa riferimento al `table_exists` comando. Ulteriori informazioni su come utilizzare il `table_exists`Il comando si trova nel [Guida alla sintassi SQL](../sql/syntax.md#table-exists).

## Passaggi successivi

Il caso di utilizzo di esempio fornito sopra evidenzia i passaggi per rendere disponibili gli attributi decile in Real-Time Customer Profile. Questo consente al servizio di segmentazione, tramite un’interfaccia utente o un’API RESTful, di generare tipi di pubblico in base a questi decile bucket. Consulta la [Panoramica del servizio di segmentazione](../../segmentation/home.md) per informazioni su come creare, valutare e accedere ai segmenti.
