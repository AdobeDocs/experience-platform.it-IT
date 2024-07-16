---
title: Caso di utilizzo dei set di dati derivati basati su Decile
description: Questa guida illustra i passaggi necessari per utilizzare Query Service per creare set di dati derivati basati su decile da utilizzare con i dati del profilo.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: 2ffb8724b2aca54019820335fb21038ec7e69a7f
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 0%

---

# Caso di utilizzo dei set di dati derivati basati su Decile

I set di dati derivati semplificano casi d’uso complessi per l’analisi di dati provenienti dal data lake che possono essere utilizzati con altri servizi Platform a valle o pubblicati nei dati del profilo cliente in tempo reale.

Questo caso d’uso di esempio illustra come creare set di dati derivati basati su decile da utilizzare con i dati del profilo cliente in tempo reale. Utilizzando come esempio uno scenario di fidelizzazione di una compagnia aerea, questa guida ti spiega come creare un set di dati che utilizza decili per categoria per segmentare e creare tipi di pubblico in base agli attributi classificati.

Sono illustrati i seguenti concetti chiave:

* Creazione di schemi per il bucket decile.
* Creazione decile categorica.
* Creazione di set di dati derivati complessi.
* Calcolo dei decili in un periodo di lookback.
* Una query di esempio per dimostrare l’aggregazione, la classificazione e l’aggiunta di identità univoche che consentono la generazione di tipi di pubblico in base a questi bucket di decile.

## Introduzione

Questa guida richiede una buona conoscenza dell&#39;esecuzione di [query in Query Service](../best-practices/writing-queries.md) e dei seguenti componenti di Adobe Experience Platform:

* [Panoramica del profilo cliente in tempo reale](../../profile/home.md): fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi.
* [Abilitare uno schema per Real-Time Customer Profile](../../profile/tutorials/add-profile-data.md): questo tutorial illustra i passaggi necessari per aggiungere dati a Real-Time Customer Profile.
* [Come definire un tipo di dati personalizzato](../../xdm/api/data-types.md): i tipi di dati vengono utilizzati come campi di tipo riferimento nelle classi o nei gruppi di campi dello schema e consentono l&#39;utilizzo coerente di una struttura a più campi che può essere inclusa in qualsiasi punto dello schema.

## Obiettivi

L’esempio fornito in questo documento utilizza i decili per creare set di dati derivati per la classificazione dei dati da uno schema di fedeltà delle compagnie aeree. I set di dati derivati ti consentono di massimizzare l’utilità dei dati identificando un pubblico in base al primo &quot;n&quot; % per una categoria selezionata.

## Creare set di dati derivati basati su decile

Per definire la classificazione dei decili in base a una dimensione particolare e a una metrica corrispondente, è necessario progettare uno schema per consentire il bucket decile.

Questa guida utilizza un set di dati sulla fedeltà delle compagnie aeree per dimostrare come utilizzare Query Service per creare decili in base alle miglia percorse in vari periodi di lookback.

## Utilizzare Query Service per creare decili

Query Service consente di creare un set di dati contenente decili per categoria, che possono quindi essere segmentati per creare tipi di pubblico in base alla classificazione degli attributi. I concetti visualizzati negli esempi seguenti possono essere applicati per creare altri set di dati a bucket decile, purché sia definita una categoria e sia disponibile una metrica.

L&#39;esempio di dati sulla fedeltà della compagnia aerea utilizza una [classe ExperienceEvents XDM](../../xdm/classes/experienceevent.md). Ogni evento è una registrazione di una transazione commerciale per chilometraggio, accreditata o addebitata, e lo stato di fedeltà di appartenenza di &quot;Flyer&quot;, &quot;Frequent&quot;, &quot;Silver&quot; o &quot;Gold&quot;. Il campo dell&#39;identità primaria è `membershipNumber`.

### Set di dati di esempio

Il set di dati iniziale sulla fedeltà della compagnia aerea per questo esempio è &quot;Dati sulla fedeltà della compagnia aerea&quot; e ha il seguente schema. Si noti che l&#39;identità primaria per lo schema è `_profilefoundationreportingstg.membershipNumber`.

![Diagramma dello schema dei dati sulla fedeltà della compagnia aerea.](../images/use-cases/airline-loyalty-data.png)

**Dati di esempio**

Nella tabella seguente vengono visualizzati i dati di esempio contenuti nell&#39;oggetto `_profilefoundationreportingstg` utilizzato per questo esempio. Fornisce il contesto per l’utilizzo di bucket decile per creare set di dati derivati complessi.

>[!NOTE]
>
>Per brevità, l&#39;ID tenant `_profilefoundationreportingstg` è stato omesso dall&#39;inizio dello spazio dei nomi nei titoli delle colonne e nelle successive menzioni in tutto il documento.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 01/01/2022 | STATUS_MILES | Nuovo membro | 5000 | VOLANTINO |
| B 789279247 | pgalton32n@barnesandnoble.com | 01/02/2022 | AWARD_MILES | JFK-FRA | 7500 | ARGENTO |
| B 789279247 | pgalton32n@barnesandnoble.com | 01/02/2022 | STATUS_MILES | JFK-FRA | 7500 | ARGENTO |
| B 789279247 | pgalton32n@barnesandnoble.com | 10/02/2022 | AWARD_MILES | FRA-JFK | 5000 | ARGENTO |
| A123487284 | rritson1zn@sciencedaily.com | 07/01/2022 | STATUS_MILES | Nuova carta di credito | 10000 | VOLANTINO |

{style="table-layout:auto"}

## Generare set di dati decile

Nei dati sulla fedeltà della compagnia aerea visualizzati sopra, il valore `.mileage` contiene il numero di miglia percorse da un membro per ogni singolo volo effettuato. Questi dati vengono utilizzati per creare decili per il numero di miglia percorse durante i lookback a vita e per una varietà di periodi di lookback. A questo scopo, viene creato un set di dati contenente decili in un tipo di dati mappa per ogni periodo di lookback e un decile appropriato per ogni periodo di lookback assegnato in `membershipNumber`.

Crea uno &quot;Schema del decile per la fedeltà della compagnia aerea&quot; per creare un set di dati decile utilizzando Query Service.

![Diagramma dello &quot;schema del decile della fedeltà della compagnia aerea&quot;.](../images/use-cases/airline-loyalty-decile-schema.png)

### Abilitare lo schema per Real-Time Customer Profile

I dati acquisiti in Experience Platform per l&#39;utilizzo da parte di Real-Time Customer Profile devono essere conformi a [uno schema Experience Data Model (XDM) abilitato per il profilo](../../xdm/ui/resources/schemas.md). Per abilitare uno schema per il profilo, è necessario implementare la classe XDM Individual Profile o XDM ExperienceEvent.

[Abilitare lo schema per l&#39;utilizzo in Real-Time Customer Profile utilizzando l&#39;API Schema Registry](../../xdm/tutorials/create-schema-api.md) o l&#39;interfaccia utente di [Schema Editor](../../xdm/tutorials/create-schema-ui.md).  Le istruzioni dettagliate su come abilitare uno schema per il profilo sono disponibili nella rispettiva documentazione.

Quindi, crea un tipo di dati da riutilizzare per tutti i gruppi di campi correlati al decile. La creazione del gruppo di campi decile è un passaggio unico per sandbox. Può essere riutilizzato anche per tutti gli schemi relativi al decile.

### Creare uno spazio dei nomi delle identità e contrassegnarlo come identificatore primario {#identity-namespace}

A qualsiasi schema creato per l&#39;utilizzo con decili deve essere assegnata un&#39;identità primaria. È possibile [definire un campo di identità nell&#39;interfaccia utente degli schemi di Adobe Experience Platform](../../xdm/ui/fields/identity.md#define-an-identity-field) o tramite l&#39;[API del registro degli schemi](../../xdm/api/descriptors.md#create).

Query Service consente inoltre di impostare un’identità o un’identità primaria per i campi di set di dati dello schema ad hoc direttamente tramite SQL. Per ulteriori informazioni, consulta la documentazione su [impostazione di un&#39;identità secondaria e di un&#39;identità primaria in identità di schema ad hoc](../data-governance/ad-hoc-schema-identities.md).

### Creare una query per il calcolo dei decili in un periodo di lookback {#create-a-query}

L’esempio seguente illustra la query SQL per calcolare un decile in un periodo di lookback.

È possibile creare un modello utilizzando l&#39;Editor query nell&#39;interfaccia utente o tramite l&#39;[API servizio query](../api/query-templates.md#create-a-query-template).

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

Il blocco viene ripetuto due volte nel modello (`summed_miles_3` e `summed_miles_6`) con una modifica nel calcolo della data per generare i dati per gli altri periodi di lookback.

È importante notare le colonne di identità, dimensione e metrica per la query (`membershipNumber`, `loyaltyStatus` e `totalMiles` rispettivamente).

#### Classificazione

I decili consentono di eseguire il bucket categoriale. Per creare il numero di classificazione, viene utilizzata la funzione `NTILE` con un parametro di `10` all&#39;interno di una FINESTRA raggruppata per il campo `loyaltyStatus`. Questo si traduce in una classificazione da 1 a 10. Impostare la clausola `ORDER BY` di `WINDOW` su `DESC` per garantire che venga assegnato un valore di classificazione di `1` alla metrica **most** nella dimensione.

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

Con più periodi di lookback, devi creare in anticipo le mappe decile bucket utilizzando le funzioni `MAP_FROM_ARRAYS` e `COLLECT_LIST`. Nel frammento di esempio `MAP_FROM_ARRAYS` crea una mappa con una coppia di matrici di chiavi (`loyaltyStatus`) e valori (`decileBucket`). `COLLECT_LIST` restituisce un array con tutti i valori nella colonna specificata.

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

L&#39;elenco di identità univoche (`membershipNumber`) è necessario per creare un elenco univoco di tutte le appartenenze.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>Se la classificazione decile è necessaria solo per un periodo di durata, questo passaggio può essere omesso e l&#39;aggregazione da `membershipNumber` può essere eseguita nel passaggio finale.

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

Esegui la query per popolare il set di dati decile. Puoi anche salvare la query come modello e pianificarla per l’esecuzione a una cadenza. Quando viene salvata come modello, la query può anche essere aggiornata per utilizzare il modello di creazione e inserimento che fa riferimento al comando `table_exists`. Ulteriori informazioni sull&#39;utilizzo del comando `table_exists`sono disponibili nella [guida alla sintassi SQL](../sql/syntax.md#table-exists).

## Passaggi successivi

Il caso d’uso di esempio fornito sopra evidenzia i passaggi per rendere disponibili i set di dati derivati basati su decile in Real-Time Customer Profile. Questo consente al servizio di segmentazione, tramite un’interfaccia utente o un’API RESTful, di generare tipi di pubblico in base a questi decile bucket. Per informazioni su come creare, valutare e accedere ai segmenti, consulta la [Panoramica del servizio di segmentazione](../../segmentation/home.md).
