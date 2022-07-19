---
title: Caso di utilizzo degli attributi derivati basati su dispositivi mobili
description: Questa guida illustra i passaggi necessari per utilizzare Query Service per creare attributi derivati basati su decile da utilizzare con i dati del profilo.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: c1ec6f949bd0ab9ec3b1ccc58baf74d8c71deca0
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 2%

---

# Caso di utilizzo degli attributi derivati basati su decile

Gli attributi derivati facilitano casi d’uso complessi per l’analisi dei dati provenienti dal data lake che possono essere utilizzati con altri servizi della piattaforma a valle o pubblicati nei dati del profilo cliente in tempo reale.

Questo esempio di caso d’uso illustra come creare attributi derivati basati su decile da utilizzare con i dati del profilo cliente in tempo reale. Utilizzando uno scenario di fidelizzazione della compagnia aerea come esempio, questa guida ti informa su come creare un set di dati che utilizza i decili categorici per segmentare e creare tipi di pubblico in base agli attributi classificati.

Vengono illustrati i seguenti concetti chiave:

* Creazione di uno schema per la divisione in blocchi di decile.
* Creazione di decile categoriche.
* Creazione di attributi derivati complessi.
* Calcolo dei decili in un periodo di lookback.
* Query di esempio per dimostrare l’aggregazione, la classificazione e l’aggiunta di identità univoche per consentire la generazione di tipi di pubblico in base a questi intervalli di decile.

## Introduzione

Questa guida richiede una buona comprensione [esecuzione query nel servizio query](../best-practices/writing-queries.md) e i seguenti componenti di Adobe Experience Platform:

* [Panoramica del profilo cliente in tempo reale](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): Introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi.
* [Come abilitare uno schema per il profilo cliente in tempo reale](../../profile/tutorials/add-profile-data.md): Questa esercitazione descrive i passaggi necessari per aggiungere dati al profilo cliente in tempo reale.
* [Come definire un tipo di dati personalizzato](../../xdm/api/data-types.md): I tipi di dati vengono utilizzati come campi di tipo riferimento in classi o gruppi di campi di schema e consentono l’uso coerente di una struttura a più campi che può essere inclusa in qualsiasi punto dello schema.

## Obiettivi

L’esempio riportato in questo documento utilizza i file deciles per creare attributi derivati per la classificazione dei dati da uno schema fedeltà di una linea aerea. Gli attributi derivati ti consentono di massimizzare l’utilità dei tuoi dati identificando un pubblico in base al &quot;n&quot; % superiore per una categoria selezionata.

## Creare attributi derivati basati su decile

Per definire la classificazione dei riquadri in base a una particolare dimensione e a una metrica corrispondente, è necessario progettare uno schema per consentire la divisione in blocchi di decile.

Questa guida utilizza un set di dati sulla fedeltà della compagnia aerea per dimostrare come utilizzare Query Service per creare decili in base alle miglia volate in diversi periodi di lookback.

## Utilizzare Query Service per creare decelle

Utilizzando Query Service, puoi creare un set di dati che contiene decili categorici, che possono essere segmentati per creare tipi di pubblico in base alla classificazione degli attributi. I concetti visualizzati negli esempi seguenti possono essere applicati per creare altri set di dati di bucket decile, purché sia definita una categoria e sia disponibile una metrica.

Ad esempio, i dati sulla fedeltà della compagnia aerea utilizzano un [Classe ExperienceEvents XDM](../../xdm/classes/experienceevent.md). Ogni evento è un record di una transazione commerciale per chilometraggio, accreditato o addebitato, e lo stato di fedeltà di appartenenza di &quot;Flyer&quot;, &quot;Frequent&quot;, &quot;Silver&quot;, o &quot;Gold&quot;. Il campo di identità principale è `membershipNumber`.

### Set di dati di esempio

Il set di dati iniziale sulla fedeltà della compagnia aerea per questo esempio è &quot;Airline Loyalty Data&quot; e presenta il seguente schema. Tieni presente che l’identità principale per lo schema è `_profilefoundationreportingstg.membershipNumber`.

![Diagramma dello schema dati fedeltà linea aerea.](../images/derived-attributes/deciles-use-case/airline-loyalty-data.png)

**Dati di esempio**

Nella tabella seguente sono visualizzati i dati di esempio contenuti nella `_profilefoundationreportingstg` oggetto utilizzato per questo esempio. Fornisce il contesto per l&#39;uso di secchi di decile per creare attributi derivati complessi.

>[!NOTE]
>
>Per brevità, l’ID tenant `_profilefoundationreportingstg` è stato omesso dall&#39;inizio dello spazio dei nomi nei titoli delle colonne e nelle menzioni successive in tutto il documento.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 01/01/2022 | STATUS_MILES | Nuovo membro | 5000 | VOLANTE |
| B789279247 | pgalton32n@barnesandnoble.com | 01/02/2022 | AWARD_MILES | JFK-FRA | 7500 | ARGENTO |
| B789279247 | pgalton32n@barnesandnoble.com | 01/02/2022 | STATUS_MILES | JFK-FRA | 7500 | ARGENTO |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | ARGENTO |
| A123487284 | rritson1zn@sciencedaily.com | 01/07/2022 | STATUS_MILES | Nuova carta di credito | 10000 | VOLANTE |

{style=&quot;table-layout:auto&quot;}

## Genera set di dati a decile

Nei dati relativi alla fedeltà della compagnia aerea di cui sopra, il `.mileage` Il valore contiene il numero di miglia trasportate da un membro per ogni singolo volo effettuato. Questi dati vengono utilizzati per creare decili per il numero di miglia che scorrono su lookback a vita e una varietà di periodi di lookback. A tal fine, viene creato un set di dati che contiene i decili in un tipo di dati mappa per ogni periodo di lookback e un decile appropriato per ogni periodo di lookback assegnato in `membershipNumber`.

Crea uno &quot;schema del decile fedeltà della compagnia aerea&quot; per creare un set di dati di decile utilizzando Query Service.

![Un diagramma dello &quot;schema del decile fedeltà aerea&quot;.](../images/derived-attributes/deciles-use-case/airline-loyalty-decile-schema.png)

### Abilitare lo schema per il profilo cliente in tempo reale

I dati che vengono acquisiti in Experience Platform per l’utilizzo da parte di Profilo cliente in tempo reale devono essere conformi a [schema Experience Data Model (XDM) abilitato per il profilo](../../xdm/ui/resources/schemas.md). Affinché uno schema sia abilitato per Profilo, deve implementare la classe Profilo individuale XDM o ExperienceEvent XDM.

[Abilita lo schema per l’utilizzo in Profilo cliente in tempo reale utilizzando l’API del Registro di sistema dello schema.](../../xdm/tutorials/create-schema-api.md) o [Interfaccia utente dell’Editor di schema](../../xdm/tutorials/create-schema-ui.md).  Istruzioni dettagliate su come abilitare uno schema per il profilo sono disponibili nella rispettiva documentazione.

Quindi, crea un tipo di dati da riutilizzare per tutti i gruppi di campi correlati a decile. La creazione del gruppo di campi decile è un unico passaggio per sandbox. Può anche essere riutilizzato per tutti gli schemi relativi ai decile.

### Crea uno spazio dei nomi di identità e contrassegnalo come identificatore principale {#identity-namespace}

A qualsiasi schema creato per l&#39;utilizzo con i decili deve essere assegnata un&#39;identità primaria. È possibile [definire un campo di identità nell’interfaccia utente di Adobe Experience Platform Schemas](../../xdm/ui/fields/identity.md#define-an-identity-field)o attraverso [API del Registro di sistema dello schema](../../xdm/api/descriptors.md#create).

Query Service consente inoltre di impostare un&#39;identità o un&#39;identità primaria per i campi di set di dati di schemi ad hoc direttamente tramite SQL. Consulta la documentazione su [impostazione di un&#39;identità secondaria e principale nelle identità dello schema ad hoc](../data-governance/ad-hoc-schema-identities.md) per ulteriori informazioni.

### Crea una query per il calcolo dei decili in un periodo di lookback {#create-a-query}

Nell&#39;esempio seguente viene illustrata la query SQL per il calcolo di un decile in un periodo di lookback.

È possibile creare un modello utilizzando l’editor delle query nell’interfaccia utente o tramite l’ [API del servizio query](../api/query-templates.md#create-a-query-template).

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

### Revisione della query

Le sezioni della query di esempio vengono esaminate più dettagliatamente di seguito.

#### Periodi di lookback

Il tipo di dati decile contiene un bucket per lookback su 1, 3, 6, 9, 12 e ciclo di vita. La query utilizza periodi di lookback di 1, 3 e 6 mesi, pertanto ogni sezione conterrà alcune query &quot;ripetute&quot; per creare tabelle temporanee per ogni periodo di lookback.

>[!NOTE]
>
>Se i dati di origine non dispongono di una colonna che può essere utilizzata per determinare un periodo di lookback, tutte le classificazioni della classe decile verranno eseguite in `decileMonthAll`.

#### Aggregazione

Utilizza le espressioni di tabella comuni (CTE, Common Table) per aggregare il chilometraggio prima di creare secchi di decile. Questo fornisce le miglia totali per un periodo di lookback specifico. I CTE esistono temporaneamente e sono utilizzabili solo nell’ambito della query più grande.

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

#### Classifica

I riquadri consentono di eseguire il bucket categorico. Per creare il numero di classificazione, la variabile `NTILE` viene utilizzata con un parametro di `10` all&#39;interno di una FINESTRA raggruppata dalla `loyaltyStatus` campo . Questo determina una classificazione da 1 a 10. Imposta la `ORDER BY` della `WINDOW` a `DESC` per garantire che un valore di classificazione di `1` è dato al **maggiore** all’interno della dimensione.

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

Con più periodi di lookback, devi creare in anticipo le mappe del bucket decile utilizzando la variabile `MAP_FROM_ARRAYS` e `COLLECT_LIST` funzioni. Nello snippet di esempio, `MAP_FROM_ARRAYS` crea una mappa con una coppia di chiavi (`loyaltyStatus`) e valori (`decileBucket`). `COLLECT_LIST` restituisce un array con tutti i valori della colonna specificata.

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
>L’aggregazione della mappa non è necessaria se la classificazione dei decile è necessaria solo per un periodo di vita.

#### Identità univoche

L&#39;elenco delle identità univoche (`membershipNumber`) è necessario per creare un elenco univoco di tutte le appartenenze.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>Se la classificazione dei decile è necessaria solo per un periodo di vita, questo passaggio può essere omesso e l&#39;aggregazione per `membershipNumber` può essere eseguito nel passaggio finale.

#### Unisci tutti i dati temporanei

Il passo finale è quello di unire tutti i dati temporanei in un modulo identico alla struttura dei deciles nel gruppo di campi.

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

Se sono disponibili solo i dati della durata, la query verrà visualizzata come segue:

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

Nei risultati della query è garantita una correlazione tra il numero di classificazione e il percentile a causa dell’uso di deciles. Ogni classificazione è pari al 10%, pertanto l’identificazione di un pubblico basato sul 30% superiore deve essere indirizzata solo ai gradi 1, 2 e 3.

### Esegui il modello di query

Esegui la query per compilare il set di dati decile. È inoltre possibile salvare la query come modello e pianificarla per l’esecuzione a cadenza. Quando viene salvata come modello, la query può anche essere aggiornata per utilizzare il pattern di creazione e inserimento che fa riferimento al `table_exists` comando. Ulteriori informazioni su come utilizzare il `table_exists`è possibile trovare nel [Guida alla sintassi SQL](../sql/syntax.md#table-exists).

## Passaggi successivi

Il caso d’uso di esempio fornito sopra evidenzia i passaggi per rendere disponibili gli attributi decile nel Profilo del cliente in tempo reale. Questo consente al servizio di segmentazione, tramite un’interfaccia utente o un’API RESTful, di generare tipi di pubblico in base a questi bucket decile. Consulta la sezione [Panoramica del servizio di segmentazione](../../segmentation/home.md) per informazioni su come creare, valutare e accedere ai segmenti.
