---
title: Flusso SQL senza pari per gli attributi derivati
description: SQL di Query Service è stato esteso per fornire supporto senza soluzione di continuità per gli attributi derivati. Scopri come utilizzare questa estensione SQL per creare un attributo derivato abilitato per il profilo e come utilizzare l’attributo per il profilo cliente in tempo reale e il servizio di segmentazione.
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: 6202b1a5956da83691eeb5422d3ebe7f3fb7d974
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 1%

---

# Flusso SQL senza pari per gli attributi derivati

SQL di Query Service è stato esteso per fornire supporto senza soluzione di continuità per gli attributi derivati. Questo fornisce un metodo alternativo efficiente per creare attributi derivati per i casi d’uso aziendali di Profilo cliente in tempo reale.

Questo documento delinea varie convenienti estensioni SQL che generano un attributo derivato da utilizzare con Profilo cliente in tempo reale. Il flusso di lavoro semplifica il processo che altrimenti sarebbe necessario completare tramite varie chiamate API o interazioni con l’interfaccia utente di Platform.

In genere, la generazione e la pubblicazione di un attributo per Profilo cliente in tempo reale prevede i seguenti passaggi:

* Crea uno spazio dei nomi di identità, se non esiste già.
* Crea il tipo di dati per memorizzare l&#39;attributo derivato, se necessario.
* Crea un gruppo di campi con quel tipo di dati per memorizzare le informazioni sugli attributi derivati.
* Crea o assegna una colonna di identità principale con lo spazio dei nomi creato in precedenza.
* Crea uno schema utilizzando il gruppo di campi e il tipo di dati creati in precedenza.
* Crea un nuovo set di dati utilizzando lo schema e abilitalo per il profilo, se necessario.
* Facoltativamente, contrassegna un set di dati come abilitato per il profilo.

Dopo aver completato i passaggi indicati in precedenza, sei pronto per compilare il set di dati. Se hai abilitato il set di dati per il profilo, puoi anche creare segmenti che fanno riferimento al nuovo attributo e iniziare a produrre informazioni.

Query Service consente di eseguire tutte le azioni elencate sopra utilizzando query SQL. Ciò include l&#39;eventuale modifica dei set di dati e dei gruppi di campi.

## Creare una tabella con un’opzione per abilitarla per il profilo {#enable-dataset-for-profile}

>[!NOTE]
>
>La query SQL fornita di seguito presuppone l&#39;utilizzo di uno spazio dei nomi preesistente.

Utilizza una query Create Table as Select (CTAS) per creare un set di dati, assegnare i tipi di dati, impostare un’identità primaria, creare uno schema e contrassegnarlo come abilitato al profilo. L&#39;istruzione SQL di esempio seguente crea gli attributi e lo rende disponibile per Profilo dati cliente in tempo reale (Real-Time CDP). La query SQL seguirà il formato mostrato nell&#39;esempio seguente:

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

I tipi di dati supportati sono: booleano, data, datetime, text, float, bigint, integer, map, array e struct/row.

Il blocco di codice SQl seguente fornisce esempi per definire tipi di dati di struttura/riga, mappa e array. La riga 1 illustra la sintassi della riga. La riga 2 illustra la sintassi della mappa e la riga 3 la sintassi dell&#39;array.

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

In alternativa, i set di dati possono essere abilitati anche per il profilo tramite l’interfaccia utente di Platform. Per ulteriori informazioni su come contrassegnare un set di dati come abilitato per il profilo, consulta [abilitare un set di dati per la documentazione del profilo cliente in tempo reale](../../../catalog/datasets/user-guide.md#enable-profile).

Nella query di esempio riportata di seguito, il `decile_table` il set di dati viene creato con `id` come colonna di identità principale e ha lo spazio dei nomi `IDFA`. Dispone inoltre di un campo denominato `decile1Month` del tipo di dati mappa. La tabella creata (`decile_table`) è abilitata per il profilo.

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

Una volta eseguita correttamente la query, l’ID del set di dati viene restituito alla console, come illustrato nell’esempio seguente.

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

Utilizzo `label='PROFILE'` su `CREATE TABLE` per creare un set di dati abilitato per il profilo. La `upsert` per impostazione predefinita, la funzionalità è attivata. La `upsert` La funzionalità può essere sovrascritta utilizzando `ALTER` come illustrato nell&#39;esempio seguente.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Per ulteriori informazioni sull&#39;utilizzo della sintassi SQl, consulta la documentazione sulla sintassi SQl [TABELLA ALTERNATIVA](../../sql/syntax.md#alter-table) e [etichetta come parte di una query CTAS](../../sql/syntax.md#create-table-as-select).

## Costruzioni per facilitare la gestione degli attributi derivati tramite SQL

Le funzioni descritte di seguito sono di grande utilità nella gestione degli attributi derivati tramite SQL.

### Modificare i set di dati esistenti da abilitare per il profilo {#enable-existing-dataset-for-profile}

Il costrutto SQL ALTER TABLE può essere utilizzato per rendere abilitati i set di dati esistenti per il profilo. Questo richiede l’aggiunta di un tag abilitato per il profilo allo schema e al set di dati corrispondente.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>In caso di esito positivo dell&#39;esecuzione `ALTER TABLE` la console restituisce `ALTER SUCCESS`.

### Aggiungere un’identità primaria a un set di dati esistente {#add-primary-identity}

Contrassegna una colonna esistente in un set di dati come set di identità principale, altrimenti si verifica un errore. Per impostare un&#39;identità primaria utilizzando SQL, utilizzare il formato di query visualizzato di seguito.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Ad esempio:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

Nell’esempio fornito, `id2` è una colonna esistente in `test1_dataset`.

### Disattiva un set di dati per il profilo {#disable-dataset-for-profile}

Se desideri disattivare la tabella per gli usi del profilo, utilizza il comando DROP. Un esempio di istruzione SQL che UTILIZZA `DROP` qui sotto.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Ad esempio:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Questa istruzione SQL fornisce un metodo alternativo efficiente all&#39;utilizzo di una chiamata API. Per ulteriori informazioni, consulta la documentazione su come [disattivare un set di dati da utilizzare con Real-Time CDP utilizzando l’API dei set di dati](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### Consenti l&#39;aggiornamento e l&#39;inserimento di funzionalità per il set di dati {#enable-upsert-functionality-for-dataset}

Il comando UPSERT consente di inserire un nuovo record o di aggiornare i dati esistenti in una tabella. In particolare, consente di aggiornare una riga esistente se un valore specificato esiste già in una tabella oppure di inserire una nuova riga se il valore specificato non esiste già.

Di seguito è riportata un&#39;istruzione di esempio che utilizza il formato corretto.

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

Ad esempio:

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

Questa istruzione SQL fornisce un metodo alternativo efficiente all&#39;utilizzo di una chiamata API. Per ulteriori informazioni, consulta la documentazione su come [abilitare un set di dati da utilizzare con Real-Time CDP e UPSERT utilizzando l’API dei set di dati](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### Disattiva le funzionalità di aggiornamento e inserimento del set di dati {#disable-upsert-functionality-for-dataset}

Questo comando disattiva la possibilità di aggiornare e inserire righe nel set di dati.

Di seguito è riportata un&#39;istruzione di esempio che utilizza il formato corretto.

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

Ad esempio:

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### Mostra informazioni aggiuntive sulla tabella associate a ciascuna tabella {#show-labels-for-tables}

I metadati aggiuntivi vengono conservati per i set di dati abilitati per il profilo. Utilizza la `SHOW TABLES` per visualizzare un comando aggiuntivo `labels` che fornisce informazioni sulle etichette associate alle tabelle.

Di seguito è riportato un esempio dell&#39;output di questo comando:

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

L’esempio mostra che `table_with_a_decile` è stato abilitato per il profilo e applicato con etichette come [&#39;UPSERT&#39;](#enable-upsert-functionality-for-dataset), [&#39;PROFILE&#39;](#enable-existing-dataset-for-profile) come descritto in precedenza.

### Crea un gruppo di campi con SQL

È ora possibile creare gruppi di campi utilizzando SQL. Questo fornisce un’alternativa all’utilizzo dell’Editor di schema nell’interfaccia utente di Platform o all’esecuzione di una chiamata API al Registro di sistema dello schema.

Di seguito è riportata un&#39;istruzione di esempio per creare un gruppo di campi.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>La creazione del gruppo di campi tramite SQL avrà esito negativo se `label` Il flag non viene fornito nell&#39;istruzione o se il gruppo di campi esiste già.
>Assicurati che la query includa un `IF NOT EXISTS` clausola per evitare il problema della query perché il gruppo di campi esiste già.

Un esempio reale potrebbe essere simile a quello mostrato di seguito.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

L&#39;esecuzione di questa istruzione ha restituito l&#39;ID gruppo di campi creato. Ad esempio `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

Consulta la documentazione su come [creare un nuovo gruppo di campi nell’Editor di schema](../../../xdm/ui/resources/field-groups.md#create) o utilizzando [API del Registro di sistema dello schema](../../../xdm/api/field-groups.md#create) per ulteriori informazioni sui metodi alternativi.

### Rilascia un gruppo di campi

Talvolta può essere necessario rimuovere un gruppo di campi dal Registro di sistema dello schema. A questo scopo, esegui il comando `DROP FIELDGROUP` con l&#39;ID del gruppo di campi.

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Ad esempio:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>Se il gruppo di campi non esiste, l&#39;eliminazione di un gruppo di campi tramite SQL avrà esito negativo. Assicurati che l’istruzione includa un `IF EXISTS` clausola per evitare il fallimento della query.

### Mostra tutti i nomi dei gruppi di campi e gli ID per le tabelle

La `SHOW FIELDGROUPS` restituisce una tabella che contiene il nome, fieldgroupId e il proprietario delle tabelle.

Di seguito è riportato un esempio dell&#39;output di questo comando:

```sql
       name                      |        fieldgroupId                             |     owner      |
---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## Passaggi successivi

Dopo aver letto questo documento, è possibile comprendere meglio come utilizzare SQL per creare un profilo e un set di dati abilitati per gli utenti in base agli attributi derivati. Ora puoi utilizzare questo set di dati con flussi di lavoro di acquisizione batch per eseguire aggiornamenti ai dati del profilo. Per ulteriori informazioni sull’acquisizione di dati in Adobe Experience Platform, consulta la sezione [panoramica sull’acquisizione dei dati](../../../ingestion/home.md).
