---
title: Flusso SQL senza interruzioni per i set di dati derivati
description: L’istruzione SQL di Query Service è stata estesa per fornire supporto continuo per i set di dati derivati. Scopri come utilizzare questa estensione SQL per creare un set di dati derivato abilitato per il profilo e come utilizzare il set di dati per Real-Time Customer Profile e Segmentation Service.
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: 7364da23c261d83681af605047a7cd7539f4a83f
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 1%

---

# Flusso SQL senza interruzioni per i set di dati derivati

L’istruzione SQL di Query Service è stata estesa per fornire supporto continuo per i set di dati derivati. Questo fornisce un metodo alternativo efficiente per creare set di dati derivati per i casi d’uso aziendali di Profilo cliente in tempo reale.

Questo documento illustra varie estensioni SQL convenienti che generano un set di dati derivato da utilizzare con Real-Time Customer Profile. Il flusso di lavoro semplifica il processo che altrimenti dovrebbe essere completato tramite varie chiamate API o interazioni dell’interfaccia utente di Platform.

In genere, la generazione e la pubblicazione di un set di dati derivato per Real-Time Customer Profile richiede i seguenti passaggi:

* Crea uno spazio dei nomi di identità, se non ne esiste già uno.
* Se necessario, crea il tipo di dati per memorizzare il set di dati derivato.
* Crea un gruppo di campi con tale tipo di dati per memorizzare le informazioni derivate sul set di dati.
* Crea o assegna una colonna di identità primaria con lo spazio dei nomi creato in precedenza.
* Crea uno schema utilizzando il gruppo di campi e il tipo di dati creati in precedenza.
* Crea un nuovo set di dati utilizzando lo schema e, se necessario, abilitalo per il profilo.
* Facoltativamente, contrassegna un set di dati come abilitato per il profilo.

Dopo aver completato i passaggi indicati sopra, sei pronto a popolare il set di dati. Se hai attivato il set di dati per il profilo, puoi anche creare segmenti che fanno riferimento al nuovo set di dati e iniziare a produrre informazioni approfondite.

Query Service consente di eseguire tutte le azioni elencate sopra utilizzando query SQL. Se necessario, ciò include l’apporto di modifiche ai set di dati e ai gruppi di campi.

## Crea una tabella con un’opzione per abilitarla per il profilo {#enable-dataset-for-profile}

>[!NOTE]
>
>La query SQL fornita di seguito presuppone l&#39;utilizzo di uno spazio dei nomi preesistente.

Utilizza una query Create Table as Select (CTAS) per creare un set di dati, assegnare tipi di dati, impostare un’identità primaria, creare uno schema e contrassegnarlo come abilitato per il profilo. L’istruzione SQL di esempio seguente crea un set di dati e lo rende disponibile per Real-time Customer Data Platform (Real-Time CDP). La query SQL verrà eseguita nel formato illustrato nell&#39;esempio seguente:

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

I tipi di dati supportati sono: boolean, date, datetime, text, float, bigint, integer, map, array e struct/row.

Il blocco di codice SQl riportato di seguito fornisce esempi per definire i tipi di dati struct/row, map e array. La riga 1 illustra la sintassi della riga. La riga due illustra la sintassi della mappa e la riga tre la sintassi dell’array.

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

In alternativa, i set di dati possono essere abilitati anche per il profilo tramite l’interfaccia utente di Platform. Per ulteriori informazioni su come contrassegnare un set di dati come abilitato per il profilo, consulta [abilitare un set di dati per la documentazione di Real-Time Customer Profile](../../../catalog/datasets/user-guide.md#enable-profile).

Nell’esempio di query seguente, la `decile_table` set di dati creato con `id` come colonna di identità primaria e ha lo spazio dei nomi `IDFA`. Ha anche un campo denominato `decile1Month` del tipo di dati mappa. Tabella creata (`decile_table`) è abilitato per il profilo.

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

Se la query viene eseguita correttamente, l’ID del set di dati viene restituito alla console, come illustrato nell’esempio seguente.

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

Utilizzare `label='PROFILE'` su un `CREATE TABLE` per creare un set di dati abilitato per il profilo. Il `upsert` è attivata per impostazione predefinita. Il `upsert` La funzionalità può essere sovrascritta utilizzando `ALTER` come illustrato nell&#39;esempio seguente.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Consulta la documentazione sulla sintassi SQl per ulteriori informazioni sull’utilizzo di [MODIFICA TABELLA](../../sql/syntax.md#alter-table) comando e [etichetta come parte di una query CTAS](../../sql/syntax.md#create-table-as-select).

## Costrutti utili per la gestione dei set di dati derivati tramite SQL

Le funzioni descritte di seguito sono molto utili per la gestione dei set di dati derivati tramite SQL.

### Modificare i set di dati esistenti da abilitare per il profilo {#enable-existing-dataset-for-profile}

Il costrutto SQL ALTER TABLE può essere utilizzato per rendere abilitati i set di dati esistenti per il profilo. Questo richiede che un tag abilitato per il profilo venga aggiunto sia allo schema che al set di dati corrispondente.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>In caso di esecuzione corretta del `ALTER TABLE` , la console restituisce `ALTER SUCCESS`.

### Aggiungere un’identità primaria a un set di dati esistente {#add-primary-identity}

Contrassegna una colonna esistente in un set di dati come set di identità principale; in caso contrario, si verifica un errore. Per impostare un&#39;identità primaria utilizzando SQL, utilizzare il formato di query visualizzato di seguito.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Ad esempio:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

Nell’esempio fornito, `id2` è una colonna esistente in `test1_dataset`.

### Disattivare un set di dati per il profilo {#disable-dataset-for-profile}

Se si desidera disattivare la tabella per gli utilizzi del profilo, è necessario utilizzare il comando DROP. Esempio di istruzione SQL che UTILIZZA `DROP` viene visualizzato di seguito.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Ad esempio:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Questa istruzione SQL fornisce un metodo alternativo efficiente all’utilizzo di una chiamata API. Per ulteriori informazioni, consulta la documentazione su come [disattivare un set di dati da utilizzare con Real-Time CDP utilizzando l’API dei set di dati](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### Consenti funzionalità di aggiornamento e inserimento per il set di dati {#enable-upsert-functionality-for-dataset}

Il comando UPSERT consente di inserire un nuovo record o di aggiornare dati esistenti in una tabella. In particolare, consente di aggiornare una riga esistente se un valore specificato esiste già in una tabella o di inserire una nuova riga se il valore specificato non esiste già.

Di seguito è riportato un esempio di istruzione che utilizza il formato corretto.

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

Ad esempio:

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

Questa istruzione SQL fornisce un metodo alternativo efficiente all’utilizzo di una chiamata API. Per ulteriori informazioni, consulta la documentazione su come [abilitare un set di dati da utilizzare con Real-Time CDP e UPSERT utilizzando l’API dei set di dati](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### Disattiva la funzionalità di aggiornamento e inserimento per il set di dati {#disable-upsert-functionality-for-dataset}

Questo comando disabilita la possibilità di aggiornare e inserire righe nel set di dati.

Di seguito è riportato un esempio di istruzione che utilizza il formato corretto.

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

Ad esempio:

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### Mostra informazioni aggiuntive sulla tabella associate a ogni tabella {#show-labels-for-tables}

Vengono conservati metadati aggiuntivi per i set di dati abilitati per il profilo. Utilizza il `SHOW TABLES` per visualizzare un `labels` che fornisce informazioni su tutte le etichette associate alle tabelle.

Di seguito è riportato un esempio dell&#39;output di questo comando:

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

Si può vedere dall&#39;esempio che `table_with_a_decile` è stato abilitato per il profilo e applicato con etichette quali [&#39;UPSERT&#39;](#enable-upsert-functionality-for-dataset), [&#39;PROFILO&#39;](#enable-existing-dataset-for-profile) come descritto in precedenza.

### Creare un gruppo di campi con SQL

È ora possibile creare i gruppi di campi mediante SQL. Alternativa all’utilizzo dell’Editor di schema nell’interfaccia utente di Platform o all’esecuzione di una chiamata API al Registro di sistema dello schema.

Di seguito è riportato un esempio di istruzione per creare un gruppo di campi.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>La creazione di un gruppo di campi tramite SQL avrà esito negativo se `label` Il flag non viene fornito nell’istruzione o se il gruppo di campi esiste già.
>Assicurati che la query includa `IF NOT EXISTS` clausola per evitare che la query non riesca perché il gruppo di campi esiste già.

Un esempio reale potrebbe essere simile a quello riportato di seguito.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

Se questa istruzione viene eseguita correttamente, viene restituito l&#39;ID del gruppo di campi creato. Ad esempio `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

Consulta la documentazione su come [creare un nuovo gruppo di campi nell’Editor di schema](../../../xdm/ui/resources/field-groups.md#create) o utilizzando [API del Registro di sistema dello schema](../../../xdm/api/field-groups.md#create) per ulteriori informazioni su metodi alternativi.

### Rilascia un gruppo di campi

Talvolta può essere necessario rimuovere un gruppo di campi dal registro degli schemi. Questa operazione viene eseguita eseguendo `DROP FIELDGROUP` con l&#39;ID del gruppo di campi.

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Ad esempio:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>L&#39;eliminazione di un gruppo di campi tramite SQL avrà esito negativo se il gruppo di campi non esiste. Assicurati che l’istruzione includa `IF EXISTS` per evitare che la query non riesca.

### Mostra tutti i nomi e gli ID dei gruppi di campi per le tabelle

Il `SHOW FIELDGROUPS` restituisce una tabella che contiene il nome, il valore fieldgroupId e il proprietario delle tabelle.

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

Dopo aver letto questo documento, sarai in grado di comprendere meglio come utilizzare SQL per creare un profilo e un set di dati abilitati per l’upsert basati su set di dati derivati. Ora puoi utilizzare questo set di dati con flussi di lavoro di acquisizione batch per apportare aggiornamenti ai dati del profilo. Per ulteriori informazioni sull’acquisizione di dati in Adobe Experience Platform, consulta la sezione [panoramica sull’acquisizione dei dati](../../../ingestion/home.md).
