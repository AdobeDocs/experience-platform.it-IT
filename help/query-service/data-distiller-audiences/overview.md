---
title: Creare tipi di pubblico con SQL
description: Scopri come utilizzare l’estensione del pubblico SQL in Data Distiller di Adobe Experience Platform per creare, gestire e pubblicare tipi di pubblico utilizzando i comandi SQL. Questa guida tratta tutti gli aspetti del ciclo di vita del pubblico, inclusa la creazione, l’aggiornamento e l’eliminazione di profili, e l’utilizzo di definizioni di pubblico basate sui dati per eseguire il targeting di destinazioni basate su file.
source-git-commit: b790dc0a485011022ac637f9d9c55f21c882d5fc
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 1%

---

# Creare tipi di pubblico con SQL

Questo documento illustra come utilizzare l’estensione SQL audience in Data Distiller di Adobe Experience Platform per creare, gestire e pubblicare tipi di pubblico utilizzando i comandi SQL.

Utilizza l’estensione SQL audience per creare tipi di pubblico con i dati del data lake, comprese eventuali entità dimensione esistenti. Questa estensione consente di definire i segmenti di pubblico direttamente utilizzando SQL, offrendo flessibilità senza la necessità di dati non elaborati nei profili. I tipi di pubblico creati con questo metodo vengono registrati automaticamente nell’area di lavoro Pubblico, dove puoi indirizzarli ulteriormente a destinazioni basate su file.

![Infografica che mostra il flusso di lavoro dell&#39;estensione del pubblico SQL. Le fasi includono la creazione di tipi di pubblico con Query Service mediante comandi SQL, la gestione nell&#39;interfaccia utente di Platform e l&#39;attivazione in destinazioni basate su file.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

## Ciclo di vita della creazione di tipi di pubblico in Data Distiller {#audience-creation-lifecycle}

Segui questi passaggi per gestire in modo efficace i tipi di pubblico. I tipi di pubblico creati si integrano perfettamente nel flusso di pubblico, consentendoti di creare segmenti da tali tipi di pubblico di base e di eseguire il targeting delle destinazioni basate su file per i clienti. Utilizza i seguenti comandi SQL per [creare](#create-audience), [modificare](#add-profiles-to-audience) e [eliminare](#delete-audience) tipi di pubblico in Adobe Experience Platform.

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
| `identity_namespace` | Spazio dei nomi dell’identità. |
| `select_query` | Un’istruzione SELECT che definisce il pubblico. La sintassi della query SELECT è disponibile nella sezione [Query SELECT](../sql/syntax.md#select-queries). |

{style="table-layout:auto"}

**Esempio:**

L’esempio seguente illustra come strutturare la query di creazione del pubblico SQL:

```sql
CREATE Audience aud_test 
WITH (primary_identity=month, identity_namespace=queryService) 
AS SELECT month FROM profile_dim_date LIMIT 5;
```

**Limitazioni:**

Tieni presente le seguenti limitazioni quando utilizzi SQL per la creazione di tipi di pubblico:

- La colonna dell&#39;identità primaria **deve** essere a livello principale.
- I nuovi batch sovrascrivono i set di dati esistenti; la funzionalità di aggiunta non è attualmente supportata.
- Gli attributi nidificati non sono attualmente supportati.

### Aggiungere profili a un pubblico esistente {#add-profiles-to-audience}

Utilizza il comando `INSERT INTO` per aggiungere profili a un pubblico esistente.

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
SELECT month FROM profile_dim_date LIMIT 10;
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

### Pubblicazione automatica dei tipi di pubblico {#auto-publish-audiences}

I tipi di pubblico creati con l’estensione SQL si registrano automaticamente in Data Distiller nell’area di lavoro Pubblico. Una volta registrati, questi tipi di pubblico sono disponibili per il targeting e possono essere utilizzati in destinazioni basate su file, migliorando la segmentazione e le strategie di targeting.

![Area di lavoro Pubblico in Adobe Experience Platform, con i tipi di pubblico di Data Distiller pubblicati automaticamente e pronti per l&#39;uso.](../images/data-distiller/sql-audiences/audiences.png)

## Attivare i tipi di pubblico nelle destinazioni {#activate-audiences}

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

I tipi di pubblico di Data Distiller non sono attualmente disponibili in Adobe Journey Optimizer. Devi creare un nuovo pubblico nel generatore di regole di Adobe Journey Optimizer affinché sia disponibile in Adobe Journey Optimizer.

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
- **Verifica prestazioni pubblico**: analizza le prestazioni dei tipi di pubblico definiti da SQL su canali diversi. Utilizza le informazioni sui dati per regolare e migliorare le definizioni dei tipi di pubblico e le strategie di targeting. Leggi il documento su [Audience Insights](../../dashboards/insights/audiences.md) per scoprire come accedere e adattare le query SQL per gli approfondimenti sul pubblico in Adobe Real-time Customer Data Platform. Puoi quindi creare informazioni personalizzate e trasformare i dati non elaborati in informazioni utilizzabili personalizzando la dashboard Tipi di pubblico per visualizzare e utilizzare in modo efficace tali informazioni per migliorare il processo decisionale.
