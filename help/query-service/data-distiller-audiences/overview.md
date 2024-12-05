---
title: Creare tipi di pubblico con SQL
description: Scopri come utilizzare l’estensione del pubblico SQL in Data Distiller di Adobe Experience Platform per creare, gestire e pubblicare tipi di pubblico utilizzando i comandi SQL. Questa guida tratta tutti gli aspetti del ciclo di vita del pubblico, inclusa la creazione, l’aggiornamento e l’eliminazione di profili, e l’utilizzo di definizioni di pubblico basate sui dati per eseguire il targeting di destinazioni basate su file.
exl-id: c35757c1-898e-4d65-aeca-4f7113173473
source-git-commit: 7db055f598e3fa7d5a50214a0cfa86e28e5bfe47
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 1%

---

# Creare tipi di pubblico con SQL

Utilizza l’estensione SQL audience per creare tipi di pubblico con dati provenienti dal data lake, incluse eventuali entità dimensione esistenti (come attributi del cliente o informazioni di prodotto).

L’utilizzo di questa estensione SQL migliora la possibilità di creare tipi di pubblico, in quanto non sono necessari dati non elaborati nei profili durante la definizione dei segmenti di pubblico. I tipi di pubblico creati con questo metodo vengono registrati automaticamente nell’area di lavoro Pubblico, dove puoi indirizzarli ulteriormente a destinazioni basate su file.

![Infografica che mostra il flusso di lavoro dell&#39;estensione del pubblico SQL. Le fasi includono la creazione di tipi di pubblico con Query Service mediante comandi SQL, la gestione nell&#39;interfaccia utente di Platform e l&#39;attivazione in destinazioni basate su file.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

Questo documento illustra come utilizzare l’estensione SQL audience in Data Distiller di Adobe Experience Platform per creare, gestire e pubblicare tipi di pubblico utilizzando i comandi SQL.

## Ciclo di vita della creazione di tipi di pubblico in Data Distiller {#audience-creation-lifecycle}

Segui questi passaggi per creare, gestire e attivare i tipi di pubblico. I tipi di pubblico creati si integrano perfettamente nel &quot;flusso di pubblico&quot;, in modo da creare segmenti dai tipi di pubblico di base e indirizzarli a destinazioni basate su file (ad esempio, caricamenti CSV o posizioni di archiviazione cloud) per la sensibilizzazione dei clienti. Con &quot;flusso di pubblico&quot; si intende l’intero processo di creazione, gestione e attivazione dei tipi di pubblico, per garantire un’integrazione perfetta tra le destinazioni.

Come parte del flusso di pubblico, utilizza i seguenti comandi SQL per [creare](#create-audience), [modificare](#add-profiles-to-audience) e [eliminare](#delete-audience) tipi di pubblico in Adobe Experience Platform.

### Creazione di un pubblico {#create-audience}

Utilizza il comando `CREATE AUDIENCE AS SELECT` per definire un nuovo pubblico. Il pubblico creato viene salvato in un set di dati e registrato nell&#39;area di lavoro [!UICONTROL Tipi di pubblico] in Data Distiller.

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title'])
AS (select_query)
```

**Parametri**

Utilizza questi parametri per definire la query di creazione del pubblico SQL:

| Parametro | Descrizione |
|--------------------|------------------------------------------------------------------|
| `schema` | Facoltativo. Definisce lo schema XDM per il set di dati creato dalla query. |
| `table_name` | Nome della tabella e del pubblico. |
| `primary_identity` | Specifica la colonna di identità primaria per il pubblico. |
| `identity_namespace` | Spazio dei nomi dell’identità. Puoi utilizzare uno spazio dei nomi esistente o crearne uno nuovo. Per visualizzare gli spazi dei nomi disponibili, utilizzare il comando `SHOW NAMESPACE`. Per creare un nuovo spazio dei nomi, utilizzare `CREATE NAMESPACE`. Esempio: `CREATE NAMESPACE lumaCrmId WITH (code='testns', TYPE='Email')`. |
| `select_query` | Un’istruzione SELECT che definisce il pubblico. La sintassi della query SELECT è disponibile nella sezione [Query SELECT](../sql/syntax.md#select-queries). |

{style="table-layout:auto"}

>[!NOTE]
>
>Per fornire maggiore flessibilità per strutture di dati complesse, puoi nidificare attributi arricchiti durante la definizione dei tipi di pubblico. Gli attributi arricchiti, come `orders`, `total_revenue`, `recency`, `frequency` e `monetization`, possono essere utilizzati per filtrare i tipi di pubblico in base alle esigenze.

**Esempio:**

L’esempio seguente illustra come strutturare la query di creazione del pubblico SQL:

```sql
CREATE Audience aud_test
WITH (primary_identity=userId, identity_namespace=lumaCrmId)
AS SELECT userId, orders, total_revenue, recency, frequency, monetization FROM profile_dim_customer;
```

In questo esempio, la colonna `userId` è identificata come colonna Identity e viene assegnato uno spazio dei nomi appropriato (`lumaCrmId`). Le colonne rimanenti (`orders`, `total_revenue`, `recency`, `frequency` e `monetization`) sono attributi arricchiti che forniscono ulteriore contesto per il pubblico.

**Limitazioni:**

Tieni presente le seguenti limitazioni quando utilizzi SQL per la creazione di tipi di pubblico:

- La colonna di identità primaria **deve** trovarsi al livello più alto del set di dati, senza essere nidificata in altri attributi o categorie.
- I tipi di pubblico esterni creati con comandi SQL hanno un periodo di conservazione di 30 giorni. Dopo 30 giorni, questi tipi di pubblico vengono eliminati automaticamente, un aspetto importante per la pianificazione delle strategie di gestione dell’audience.

### Aggiungere profili a un pubblico esistente {#add-profiles-to-audience}

Utilizza il comando `INSERT INTO` per aggiungere profili (o interi tipi di pubblico) a un pubblico esistente.

```sql
INSERT INTO table_name
SELECT select_query
```

**Parametri**

Nella tabella seguente sono illustrati i parametri necessari per il comando `INSERT INTO`:

| Parametro | Descrizione |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | Nome della tabella creata come parte del comando create audience. |
| `select_query` | Un&#39;istruzione SELECT. La sintassi della query SELECT è disponibile nella sezione Query SELECT. |

{style="table-layout:auto"}

**Esempio:**

Nell&#39;esempio seguente viene illustrato come aggiungere profili a un pubblico esistente con il comando `INSERT INTO`:

```sql
INSERT INTO Audience aud_test
SELECT userId, orders, total_revenue, recency, frequency, monetization FROM customer_ds;
```

### Esempio di pubblico del modello RFM {#rfm-model-audience-example}

L’esempio seguente illustra come creare un pubblico utilizzando il modello Recency, Frequency, and Monetization (RFM). Questo esempio segmenta i clienti in base ai loro punteggi di attualità, frequenza e monetizzazione per identificare gruppi chiave, come clienti fedeli, nuovi clienti e clienti di alto valore.

<!--  Q) Since the focus of this document is on external audiences, or should I just include this temporarily? We could simply provide a link to the separate RFM modeling documentation rather than including the full example here. (Add link to new RFM document when it is published) -->

La query seguente crea uno schema per il pubblico RFM. L&#39;istruzione imposta i campi in modo che contengano informazioni sul cliente come `userId`, `days_since_last_purchase`, `orders`, `total_revenue` e così via.

```sql
CREATE Audience adls_rfm_profile
WITH (primary_identity=userId, identity_namespace=lumaCrmId) AS
SELECT
    cast(NULL AS string) userId,
    cast(NULL AS integer) days_since_last_purchase,
    cast(NULL AS integer) orders,
    cast(NULL AS decimal(18,2)) total_revenue,
    cast(NULL AS integer) recency,
    cast(NULL AS integer) frequency,
    cast(NULL AS integer) monetization,
    cast(NULL AS string) rfm_model
WHERE false;
```

Dopo aver creato il pubblico, popolalo con i dati del cliente e segmentalo in base ai loro punteggi RFM. L&#39;istruzione SQL seguente utilizza la funzione `NTILE(4)` per classificare i clienti in quartili in base ai punteggi RFM (recency, frequenza, monetizzazione). Questi punteggi classificano i clienti in sei segmenti, ad esempio &quot;Core&quot;, &quot;Loyal&quot; e &quot;Whales&quot;. I dati cliente segmentati vengono quindi inseriti nella tabella `adls_rfm_profile` del pubblico.&quot;

```sql
INSERT INTO Audience adls_rfm_profile
SELECT
    userId,
    days_since_last_purchase,
    orders,
    total_revenue,
    recency,
    frequency,
    monetization,
    CASE
        WHEN Recency=1 AND Frequency=1 AND Monetization=1 THEN '1. Core - Your Best Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency=1 AND Monetization IN (1,2,3,4) THEN '2. Loyal - Your Most Loyal Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN (1,2,3,4) AND Monetization=1 THEN '3. Whales - Your Highest Paying Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN(1,2,3) AND Monetization IN(2,3,4) THEN '4. Promising - Faithful Customers'
        WHEN Recency=1 AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '5. Rookies - Your Newest Customers'
        WHEN Recency IN (2,3,4) AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '6. Slipping - Once Loyal, Now Gone'
    END AS rfm_model
FROM (
    SELECT
        userId,
        days_since_last_purchase,
        orders,
        total_revenue,
        NTILE(4) OVER (ORDER BY days_since_last_purchase) AS recency,
        NTILE(4) OVER (ORDER BY orders DESC) AS frequency,
        NTILE(4) OVER (ORDER BY total_revenue DESC) AS monetization
    FROM (
        SELECT
            userid,
            DATEDIFF(current_date, MAX(purchase_date)) AS days_since_last_purchase,
            COUNT(purchaseid) AS orders,
            CAST(SUM(total_revenue) AS double) AS total_revenue
        FROM (
            SELECT DISTINCT
                ENDUSERIDS._EXPERIENCE.EMAILID.ID AS userid,
                commerce.`ORDER`.purchaseid AS purchaseid,
                commerce.`ORDER`.pricetotal AS total_revenue,
                TO_DATE(timestamp) AS purchase_date
            FROM sample_data_for_ootb_templates
            WHERE commerce.`ORDER`.purchaseid IS NOT NULL
        ) AS b
        GROUP BY userId
    )
);
```

### Eliminare un pubblico (DROP AUDIENCE) {#delete-audience}

Utilizza il comando `DROP AUDIENCE` per eliminare un pubblico esistente. Se il pubblico non esiste, si verifica un&#39;eccezione a meno che non sia specificato `IF EXISTS`.

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**Parametri**

La tabella contiene i parametri necessari per il comando `DROP AUDIENCE`:

| Parametro | Descrizione |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | Facoltativo. Se specificato, nel caso in cui la tabella non venga trovata, non viene generata alcuna eccezione. |
| `db_name` | Specifica il gruppo di dati utilizzato per qualificare il set di dati sul pubblico. |
| `table_name` | Nome della tabella creata come parte del comando create audience. |

{style="table-layout:auto"}

**Esempio:**

L’esempio seguente illustra come eliminare un pubblico utilizzando il comando DROP AUDIENCE:

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### Registrazione e disponibilità automatiche del pubblico {#registration-and-availability}

I tipi di pubblico creati con l&#39;estensione SQL vengono registrati automaticamente in Data Distiller [!UICONTROL Origin] nell&#39;area di lavoro Pubblico. Una volta registrati, questi tipi di pubblico sono disponibili per il targeting in destinazioni basate su file, migliorando la segmentazione e le strategie di targeting. Questo processo non richiede alcuna configurazione aggiuntiva, semplificando la gestione dell’audience. Per ulteriori dettagli su come visualizzare, gestire e creare tipi di pubblico nell&#39;interfaccia utente di Platform, consulta la [panoramica di Audience Portal](../../segmentation/ui/audience-portal.md).

<!-- Q) Do you know how long it takes for the audience to register? This info would help manage user expectations. -->

![Area di lavoro Pubblico in Adobe Experience Platform, con i tipi di pubblico di Data Distiller pubblicati automaticamente e pronti per l&#39;uso.](../images/data-distiller/sql-audiences/audiences.png)

## Attiva tipi di pubblico nelle destinazioni {#activate-audiences}

Attiva i tipi di pubblico eseguendo il targeting su qualsiasi destinazione basata su file, ad esempio [!DNL Amazon S3], [!DNL SFTP] o [!DNL Azure Blob]. Gli attributi del pubblico arricchiti sono disponibili per ulteriori perfezionamenti e filtri in base alle esigenze.

![Diagramma di flusso dei tipi di destinazione di Adobe Experience Platform, che mostra le destinazioni pubbliche e private/personalizzate, incluse le opzioni batch e di streaming.](../images/data-distiller/sql-audiences/destination-types.png)

## Chiarimenti sulle funzioni {#faqs}

Questa sezione tratta le domande frequenti sulla creazione e la gestione di tipi di pubblico esterni tramite SQL in Data Distiller.

**Domande**:

- La creazione di tipi di pubblico è supportata solo per set di dati piatti?

+++Risposta

Attualmente, la creazione di un pubblico è limitata agli attributi piatti (a livello di radice) durante la definizione del pubblico.

+++

- La creazione di tipi di pubblico si traduce in uno o più set di dati o varia a seconda della configurazione?

+++Risposta

Esiste una mappatura uno-a-uno tra un pubblico e un set di dati.

+++

- Il set di dati creato durante la creazione del pubblico è contrassegnato per Profilo?

+++Risposta

No, il set di dati creato durante la creazione del pubblico non è contrassegnato per il profilo.

+++

- Il set di dati è creato nel data lake?

+++Risposta

Sì, il set di dati associato al pubblico viene creato sul data lake. Gli attributi di questo set di dati sono disponibili nel Compositore pubblico e nel flusso di destinazione come attributi arricchiti.

+++

- Gli attributi nel pubblico sono limitati alle destinazioni basate su file batch dell&#39;organizzazione? (Sì o No)

+++Risposta

No. Gli attributi arricchiti nel pubblico sono disponibili per l’utilizzo sia nelle destinazioni Enterprise Batch che in quelle basate su file. Se riscontri un errore simile a &quot;I seguenti ID segmento hanno spazi dei nomi non consentiti per questa destinazione: e917f626-a038-42f7-944c-xyxyxyx&quot;, crea un nuovo segmento in Data Distiller e utilizzalo con qualsiasi destinazione disponibile.

+++

- È possibile creare un pubblico di tipi di pubblico che utilizza un pubblico di Data Distiller?

+++Risposta

Sì, puoi creare un pubblico di tipi di pubblico che utilizza un pubblico di Data Distiller.

+++

- Questi tipi di pubblico vengono visualizzati in Adobe Journey Optimizer? In caso contrario, cosa succede quando creo un nuovo pubblico nel generatore di regole che include tutti i membri del pubblico?

+++Risposta

I tipi di pubblico di Data Distiller sono disponibili anche in Adobe Journey Optimizer. Puoi utilizzare i tipi di pubblico di Data Distiller in Adobe Journey Optimizer e filtrare i risultati in base agli attributi arricchiti.

+++

- I tipi di pubblico di Data Distiller vengono eliminati ogni 30 giorni poiché sono tipi di pubblico esterni?

+++Risposta

Sì, i tipi di pubblico di Data Distiller vengono eliminati ogni 30 giorni poiché sono tipi di pubblico esterni.

+++

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a utilizzare l’estensione del pubblico SQL in Data Distiller per creare, gestire e pubblicare in modo efficace i tipi di pubblico utilizzando i comandi SQL. Ora puoi personalizzare le definizioni dei tipi di pubblico in base ai tuoi requisiti aziendali specifici e attivarle su varie destinazioni, ottimizzando le strategie di marketing e le decisioni basate sui dati.

Successivamente, puoi leggere la seguente documentazione per sviluppare e ottimizzare ulteriormente le strategie di gestione dell’audience di Platform:

- **Esplora valutazione del pubblico**: scopri i [metodi di valutazione del pubblico in Adobe Experience Platform](../../segmentation/home.md#evaluate-segments): segmentazione in streaming per aggiornamenti in tempo reale, segmentazione batch per elaborazione pianificata o su richiesta e segmentazione Edge per valutazione immediata nell&#39;Edge Network.
- **Integrare con le destinazioni**: leggi la guida su come [esportare i file on-demand in destinazioni batch](../../destinations/ui/export-file-now.md) utilizzando l&#39;interfaccia utente delle destinazioni di Platform.
- **Verifica prestazioni pubblico**: analizza le prestazioni dei tipi di pubblico definiti da SQL su canali diversi. Utilizza le informazioni sui dati per regolare e migliorare le definizioni dei tipi di pubblico e le strategie di targeting. Leggi il documento su [Audience Insights](../../dashboards/insights/audiences.md) per scoprire come accedere e adattare le query SQL per gli approfondimenti sul pubblico in Adobe Real-Time CDP. Puoi quindi creare informazioni personalizzate e trasformare i dati non elaborati in informazioni utilizzabili personalizzando la dashboard Tipi di pubblico per visualizzare e utilizzare in modo efficace tali informazioni per migliorare il processo decisionale.

