---
title: Tecniche consigliate per l’organizzazione delle risorse dati nel servizio query
description: Questo documento delinea un modo logico di organizzare i dati per facilitarne l’utilizzo con Query Service.
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Organizzare le risorse dati in Query Service

Questo documento fornisce indicazioni sulle best practice per l’organizzazione delle risorse dati, compresi set di dati, visualizzazioni e tabelle temporanee da utilizzare con Adobe Experience Platform Query Service. Vengono descritte le modalità di struttura dei dati e le informazioni su come accedere, aggiornare ed eliminare tali informazioni.

È importante organizzare in modo logico le risorse di dati all’interno di Platform [!DNL Data Lake] mentre crescono. Query Service estende i costrutti SQL che consentono di raggruppare in modo logico le risorse di dati all’interno di una sandbox. Questo metodo di organizzazione consente la condivisione di risorse di dati tra schemi senza la necessità di spostarle fisicamente.

## Introduzione

Prima di continuare con questo documento, è necessario avere una buona comprensione di [Servizio query](../home.md) funzioni e hanno letto [guida all’interfaccia utente](../ui/user-guide.md).

## Organizzazione dei dati in Query Service

Gli esempi seguenti illustrano i costrutti disponibili tramite Adobe Experience Platform Query Service per organizzare i dati in modo logico utilizzando una sintassi SQL standard. È innanzitutto necessario creare un database che funga da contenitore per i punti dati. Un database può contenere uno o più schemi e ogni schema può quindi avere uno o più riferimenti a una risorsa dati (set di dati, visualizzazioni, tabelle temporanee, ecc.). Questi riferimenti includono qualsiasi relazione o associazione tra i set di dati.

Consulta la sezione [Guida utente dell’editor delle query](../ui/user-guide.md) per informazioni dettagliate su come utilizzare l’interfaccia utente del servizio query per creare query SQL.

Sono supportati i seguenti costrutti SQL per organizzare i set di dati in modo logico in una sandbox.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

L’esempio (leggermente troncato per brevità) mostra questa metodologia dove `databaseA` contiene lo schema `schema1`.

## Associazione delle risorse dati a uno schema

Una volta creato uno schema per fungere da contenitore per le risorse di dati, ogni set di dati può essere associato a uno o più schemi nel database utilizzando la sintassi standard SQL ALTER TABLE.

L&#39;esempio seguente aggiunge `dataset1`, `dataset2`, `dataset3` e `v1` al `databaseA.schema1` contenitore creato nell’esempio precedente.

```SQL
ALTER TABLE dataset1 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 SET SCHEMA databaseA.schema1;
 
ALTER VIEW v1  SET SCHEMA databaseA.schema1;
```

## Accesso alle risorse dati dal contenitore dati

Qualificando in modo appropriato il nome del database, qualsiasi [!DNL PostgreSQL] client può connettersi a una qualsiasi delle strutture di dati create utilizzando la parola chiave SHOW . Per ulteriori informazioni sulla parola chiave SHOW, consulta la [Sezione SHOW nella documentazione relativa alla sintassi SQL](../sql/syntax.md#show).

&quot;all&quot; è il nome di database predefinito che contiene ogni database e contenitore di schema in una sandbox. Quando si effettua una [!DNL PostgreSQL] connessione tramite `dbname="all"`, puoi accedere a **qualsiasi** database e schema creati per organizzare i dati in modo logico.

Elencare tutti i database in `dbname="all"` visualizza tre database disponibili.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

Elencare tutti gli schemi in `dbname="all"` visualizza i tre schemi relativi a ogni database nella sandbox.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

Quando si effettua una [!DNL PostgreSQL] connessione tramite `dbname="databaseA"`, puoi accedere a qualsiasi schema associato a quel database specifico, come mostrato nell’esempio seguente.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
 

SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
```

La notazione del punto consente di accedere a ogni tabella associata a uno schema specifico connesso al database scelto. Connettendosi a `DBNAME = databaseA.schema1;`, tutte le tabelle associate a tale schema specifico (`schema1`). Questo fornisce informazioni su quale set di dati contiene quale tabella.

```sql
SHOW DATABASES;
  
name     
---------
databaseA


SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1


SHOW tables;
name       | type
----------------------
dataset1| table
dataset2| table
dataset3| table
```

## Aggiornare o rimuovere le risorse dati da un contenitore dati

Man mano che cresce la quantità di risorse di dati nell’organizzazione IMS (o sandbox), diventa necessario aggiornare o rimuovere le risorse di dati da un contenitore di dati. Le singole risorse possono essere rimosse dal contenitore dell’organizzazione facendo riferimento al nome del database e dello schema appropriato utilizzando la notazione del punto. Tabella e visualizzazione (`t1` e `v1` aggiunti rispettivamente a `databaseA.schema1` nel primo esempio, vengono rimossi utilizzando la sintassi nell&#39;esempio seguente.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Rimuovere le risorse dati

La [TABELLA A DISCESA](../sql/syntax.md#drop-table) rimuove fisicamente una risorsa dati dal [!DNL Data Lake] quando esiste un singolo riferimento alla tabella in tutti i database dell’organizzazione IMS.

```sql
DROP TABLE databaseA.schema2.t1;
```

### Rimuovere un contenitore di risorse dati

È inoltre possibile rimuovere il database e lo schema utilizzando funzioni SQL standard.

#### Rimuovere un database

Se sono presenti altri riferimenti alle risorse di dati associate al database, la funzione genera un errore durante il tentativo di rimozione del database.

```sql
DROP DATABASE databaseA;
```

#### Rimuovere uno schema

Durante la rimozione di uno schema è necessario tenere presenti tre considerazioni importanti:

- La rimozione di uno schema non comporta l’eliminazione fisica delle risorse di dati quali tabelle, viste o tabelle temporanee.
- Se nello schema di destinazione sono presenti risorse di dati a cui viene fatto riferimento e la modalità è RESTRICT, verrà generata un&#39;eccezione.
- Se nello schema di destinazione sono presenti risorse di dati a cui viene fatto riferimento e la modalità è CASCADE, il sistema rimuove tutte le risorse di dati a cui fa riferimento il contenitore dello schema e quindi elimina il contenitore dello schema.

```sql
DROP SCHEMA databaseA.schema2;
```

## Passaggi successivi

Leggendo questo documento, ora hai una migliore comprensione delle best practice relative all’organizzazione e alla struttura delle risorse di dati da utilizzare con Adobe Experience Platform Query Service. È consigliabile continuare a imparare le best practice relative al servizio query leggendo informazioni [documentazione sulla deduplicazione dei dati](../essential-concepts/deduplication.md).
