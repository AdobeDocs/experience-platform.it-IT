---
title: Attributi derivati
description: Gli attributi derivati ti consentono di calcolare gli attributi con cadenza regolare ed eventualmente di pubblicare questi attributi derivati in Profilo cliente in tempo reale come attributi di profilo. Questo documento fornisce una panoramica sull’utilizzo di Query Service per creare attributi derivati da utilizzare con i dati del profilo.
hide: true
hidefromtoc: true
source-git-commit: fc2d2e7dadb95460f5d735ba33e5f106880a0198
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 1%

---

# Attributi derivati

Gli attributi derivati ti consentono di calcolare gli attributi con cadenza regolare ed eventualmente di pubblicare questi attributi derivati in Profilo cliente in tempo reale come attributi di profilo.

Gli attributi derivati, come quelli creati con dati decile, sono necessari per diversi casi d’uso che analizzano i dati del profilo. Utilizzando dati decile puoi creare tipi di pubblico dai segmenti in base al loro percentile o classificazione di un dato attributo. Ad esempio, i potenziali casi di utilizzo possono includere:

* Identificare il 10% più basso di abbonati in base al pubblico per canale. In questo modo, gli esperti di marketing possono eseguire il targeting di un pubblico specifico e vendere un nuovo pacchetto di abbonati.
* Identificare un pubblico che si trova nel 10% dei volantini più richiesti in base alle miglia totali percorse e con lo stato di &quot;Flyer&quot;. Questo pubblico potrebbe essere utilizzato per indirizzare in modo selettivo la vendita di una nuova offerta di carta di credito.

## Introduzione

Questa panoramica richiede una buona comprensione [Chiamate API per Platform](../landing/api-guide.md) e i seguenti componenti di Adobe Experience Platform:

* [Panoramica del profilo cliente in tempo reale](../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Nozioni di base sulla composizione dello schema](../xdm/schema/composition.md): Introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi.
* [Come abilitare uno schema per il profilo cliente in tempo reale](../profile/tutorials/add-profile-data.md): Questa esercitazione descrive i passaggi necessari per aggiungere dati al profilo cliente in tempo reale.

## Supporto SQL per gli attributi derivati

Per definire la classificazione dei riquadri in base a una particolare dimensione (categoria) e a una metrica corrispondente (ricavi, punti, durata del visualizzatore, ecc.), è necessario progettare uno schema per consentire la divisione in blocchi di decile. Questo schema può essere utilizzato come parte dello schema di profilo più grande.

### Creare uno spazio dei nomi di identità per lo schema del profilo {#identity-namespace}

Gli spazi dei nomi di identità sono un componente di [ Identity Service](../identity-service/home.md) che fungono da indicatori del contesto a cui si riferisce un’identità. Un&#39;identità completa include un valore ID e uno spazio dei nomi. Quando i dati dei record vengono confrontati e uniti tra frammenti di profilo, il valore dell’identità e lo spazio dei nomi devono corrispondere.

I set di dati creati relativi all’identità possono essere raggruppati come gruppo di dati e contribuire a mantenere il ciclo di vita dei dati. Gli spazi dei nomi personalizzati possono essere creati utilizzando [API del servizio Identity](../identity-service/api/create-custom-namespace.md) o tramite l’interfaccia utente. Consulta la sezione [gestire la documentazione dei namespace personalizzati](../identity-service/namespaces.md#manage-namespaces) per informazioni su come eseguire questa operazione tramite l’interfaccia utente di .

Il descrittore di identità principale può essere assegnato a un campo nell’interfaccia utente di Schema oppure può essere creato utilizzando l’API del Registro di schema. Consulta la documentazione per le istruzioni su come [definire un campo di identità nell’interfaccia utente di Adobe Experience Platform](../xdm/ui/fields/identity.md#define-an-identity-field)o attraverso [API del Registro di sistema dello schema](../xdm/api/descriptors.md#create).

Query Service consente inoltre di impostare un&#39;identità o un&#39;identità primaria per i campi di set di dati di schemi ad hoc direttamente tramite SQL. Consulta la documentazione su [impostazione di un&#39;identità secondaria e principale nelle identità dello schema ad hoc](./data-governance/ad-hoc-schema-identities.md) per ulteriori informazioni.

## Creare attributi derivati

La query di esempio fornita in questo documento si concentra sui decili per classificare set di dati di grandi dimensioni e classificare i dati dai valori più alti a quelli più bassi (o viceversa) e filtrare in base al periodo di tempo.

### Decole {#deciles}

Un decile è un metodo per suddividere un insieme di dati classificati in 10 parti uguali. Quando i dati sono suddivisi in decile, a ogni riga del set di dati viene assegnato un rango di decile. Ciò consente di ordinare i dati in ordine decrescente o crescente.

Un grado di decile organizza i dati in ordine dal più basso al più alto ed è fatto su una scala da 1 a 10 dove ogni numero successivo corrisponde a un aumento di 10 punti percentuali.

I bucket con decibel rappresentano il numero di gruppi con classifica e vengono utilizzati per assegnare una classificazione a una dimensione (categoria) nel set di dati. Il bucket può essere un numero o un&#39;espressione che restituisce un valore intero positivo per ogni partizione. I bucket non devono avere un valore null.

I quartili vengono utilizzati per dividere la distribuzione per quattro e percentili per 100.

### Creare lo schema per i bucket decile {#create-schema}

Lo schema creato per i blocchi decile è costituito da tre parti integranti: un tipo di dati, un gruppo di campi per il tipo di dati (per set di dati di origine) e un campo di identità principale.

>[!NOTE]
>
>È necessario creare uno spazio dei nomi di identità prima di creare lo schema. Consulta la sezione [spazio dei nomi identità](#identity-namespace) per ulteriori dettagli.

Adobe fornisce diverse classi XDM standard (&quot;core&quot;), tra cui Profilo individuale XDM e ExperienceEvent XDM. Oltre a queste classi principali, puoi anche creare classi personalizzate per descrivere casi d’uso più specifici per la tua organizzazione. Consulta le guide su come [creare e modificare schemi nell’interfaccia utente](../xdm/ui/resources/schemas.md#create) o utilizzando [endpoint schemas nell’API del Registro di sistema dello schema](../xdm/api/schemas.md#create) per ulteriori dettagli.

I dati che vengono acquisiti in Experience Platform per l’utilizzo da parte di Profilo cliente in tempo reale devono essere conformi a uno schema Experience Data Model (XDM) abilitato per Profilo. Affinché uno schema sia abilitato per Profilo, deve implementare la classe Profilo individuale XDM o ExperienceEvent XDM.

È possibile [abilitare uno schema da utilizzare nel profilo cliente in tempo reale utilizzando l’API del Registro di sistema dello schema](../xdm/tutorials/create-schema-api.md) o [Interfaccia utente dell’Editor di schema](../xdm/tutorials/create-schema-ui.md).  Istruzioni dettagliate su come abilitare uno schema per il profilo sono disponibili nella rispettiva documentazione.

### Creare un tipo di dati {#create-data-type}

I tipi di dati vengono utilizzati come campi di tipo riferimento in classi o gruppi di campi di schema e consentono l’uso coerente di una struttura a più campi che può essere inclusa in qualsiasi punto dello schema. La creazione del tipo di dati è un unico passaggio per sandbox, in quanto può essere riutilizzata per tutti i gruppi di campi correlati a decile.

Consulta la documentazione per le istruzioni su come [definire un tipo di dati personalizzato](../xdm/api/data-types.md) utilizzando [API del Registro di sistema dello schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

### Crea il gruppo di campi decile {#create-field-group}

La creazione del gruppo di campi è un unico passaggio per sandbox. Può anche essere riutilizzato per tutti gli schemi relativi ai decile.

Consulta la documentazione per le istruzioni su come [creare gruppi di campi tramite l’interfaccia utente](../xdm/ui/resources/field-groups.md#create)

## Utilizzare Query Service per creare decelle

Query Service offre un modo ideale per creare un set di dati contenente decili categorici. Può essere quindi utilizzato insieme al servizio di segmentazione per creare tipi di pubblico in base alla classificazione degli attributi.

I concetti visualizzati negli esempi seguenti possono essere applicati per creare altri set di dati bucket decile, purché sia definita una categoria (dimensione) e sia disponibile una metrica. Gli esempi si basano sui dati relativi a un programma di fidelizzazione delle compagnie aeree. I dati sulla fidelizzazione della compagnia aerea utilizzano la classe Experience Events in cui ogni evento è un record di una transazione commerciale per **chilometraggio**, accreditati o addebitati, e l&#39;iscrizione **stato fedeltà** &quot;Volantino&quot;, &quot;Frequente&quot;, &quot;Argento&quot; o &quot;Oro&quot;. Il campo di identità principale è `membershipNumber`.

### Creare un modello di query {#create-a-query-template}

Il modello può essere creato utilizzando l’editor delle query nell’interfaccia utente o tramite l’ [API del servizio query](./api/query-templates.md#create-a-query-template).

Le sezioni del modello di query visualizzate di seguito saranno esaminate più dettagliatamente.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/query-templates \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
         "name": "Airline Loyalty Deciles Insert into profile",
         "sql":
            "WITH summed_miles_1 AS (
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
                LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)"
        }'
```

#### Periodi di lookback

Il tipo di dati decile contiene un bucket per look-back 1, 3, 6, 9, 12 e del ciclo di vita. La query utilizza i periodi di look-back di 1, 3 e 6 mesi, quindi ogni sezione conterrà alcune query &quot;ripetute&quot; per creare tabelle temporanee per ogni periodo di look-back.

>[!NOTE]
>
>Se i dati di origine non dispongono di una colonna che può essere utilizzata per determinare un periodo di look-back, tutte le classificazioni della classe decile verranno eseguite in `decileMonthAll`.

#### Aggregazione

Utilizza le espressioni di tabella comuni (CTE, Common Table) per aggregare il chilometraggio prima di creare secchi di decile. Questo fornisce le miglia totali per un periodo di look-back specifico. I CTE esistono temporaneamente e sono utilizzabili solo nell’ambito della query più grande.

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

Il blocco viene ripetuto due volte nel modello (`summed_miles_3` e `summed_miles_6`) con una modifica nel calcolo della data al fine di generare i dati per gli altri periodi di look-back.

Osserva le colonne di identità, dimensione e metrica per la query (`membershipNumber`, `loyaltyStatus` e `totalMiles` rispettivamente).

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

Con più periodi di look-back, è necessario creare in anticipo le mappe del bucket decile utilizzando il `MAP_FROM_ARRAYS` e `COLLECT_LIST` funzioni. Nello snippet di esempio, `MAP_FROM_ARRAYS` crea una mappa con una coppia di chiavi (`loyaltyStatus`) e valori (`decileBucket`). `COLLECT_LIST` restituisce un array con tutti i valori della colonna specificata.

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

### Esegui il modello di query

Le query possono essere [eseguito tramite l’interfaccia utente](./ui/user-guide.md#executing-queries) o [API del servizio query](./api/queries.md#create-a-query).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/queries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "dbName": "prod:all",
    "templateId": "{{airline_decile_query_template_id}}",
    "insertIntoParameters": {
        "datasetName": "airline_loyalty_decile"
    }
}'
```

Nei risultati della query è garantita una correlazione tra il numero di classificazione e il percentile a causa dell’uso di deciles. Ogni classificazione è pari al 10%, pertanto l’identificazione di un pubblico basato sul 30% superiore deve essere indirizzata solo ai gradi 1, 2 e 3.

## Passaggi successivi

Il servizio di segmentazione fornisce un’interfaccia utente e un’API RESTful che consente di generare tipi di pubblico in base a questi bucket decile. Consulta la sezione [Panoramica del servizio di segmentazione](../segmentation/home.md) per informazioni su come creare, valutare e accedere ai segmenti.

Per informazioni dettagliate su come creare e utilizzare i segmenti nel Generatore di segmenti (l’implementazione dell’interfaccia utente del servizio di segmentazione), consulta la sezione [Guida al Generatore di segmenti](../segmentation/ui/overview.md).

Per informazioni sulla creazione di definizioni di segmenti utilizzando l’API, consulta l’esercitazione su [creazione di segmenti di pubblico tramite API](../segmentation/tutorials/create-a-segment.md).
