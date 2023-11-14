---
title: Best practice per l’organizzazione delle risorse dati in Query Service
description: Questo documento illustra un modo logico di organizzare i dati per facilitarne l’utilizzo con Query Service.
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: 6e2be299e3c1c0dfa2832ead22cdeaea0ca83591
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# Organizzare le risorse dati in Query Service

Questo documento fornisce indicazioni sulle best practice per organizzare le risorse dati, tra cui set di dati, viste e tabelle temporanee da utilizzare con Adobe Experience Platform Query Service. Vengono inoltre fornite informazioni su come strutturare i dati e su come accedere, aggiornare ed eliminare tali informazioni.

È importante organizzare in modo logico le risorse dati all’interno di Platform [!DNL Data Lake] mentre crescono. Query Service estende i costrutti SQL che consentono di raggruppare in modo logico le risorse di dati all’interno di una sandbox. Questo metodo di organizzazione consente la condivisione di risorse di dati tra schemi senza la necessità di spostarli fisicamente.

## Introduzione

Prima di continuare con questo documento, è necessario avere una buona conoscenza di [Servizio query](../home.md) e aver letto il [guida all’interfaccia utente](../ui/user-guide.md).

## Organizzazione dei dati in Query Service

Negli esempi seguenti vengono illustrati i costrutti disponibili tramite Adobe Experience Platform Query Service per organizzare in modo logico i dati utilizzando la sintassi SQL standard. È innanzitutto necessario creare un database che funga da contenitore per i punti dati. Un database può contenere uno o più schemi e ogni schema può quindi avere uno o più riferimenti a una risorsa dati (set di dati, viste, tabelle temporanee, ecc.). Tali riferimenti includono eventuali relazioni o associazioni tra i set di dati.

Consulta la [Guida utente di Query Editor](../ui/user-guide.md) per istruzioni dettagliate su come utilizzare l’interfaccia utente di Query Service per creare query SQL.

Sono supportati i seguenti costrutti SQL per organizzare in modo logico i set di dati in una sandbox.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

L’esempio (leggermente troncato per brevità) illustra questa metodologia dove `databaseA` contiene schema `schema1`.

## Associazione di risorse di dati a uno schema

Una volta creato uno schema che funge da contenitore per le risorse di dati, ogni set di dati può essere associato a uno o più schemi nel database utilizzando la sintassi standard SQL ALTER TABLE.

L’esempio seguente aggiunge `dataset1`, `dataset2`, `dataset3` e `v1` al `databaseA.schema1` contenitore creato nell’esempio precedente.

```SQL
ALTER TABLE dataset1 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 ADD SCHEMA databaseA.schema1;
 
ALTER VIEW v1  ADD SCHEMA databaseA.schema1;
```

## Accesso alle risorse di dati dal contenitore dati

Qualificando in modo appropriato il nome del database, qualsiasi [!DNL PostgreSQL] Il client può connettersi a qualsiasi struttura di dati creata utilizzando la parola chiave SHOW. Per ulteriori informazioni sulla parola chiave SHOW, vedere [MOSTRA sezione nella documentazione della sintassi SQL](../sql/syntax.md#show).

&quot;all&quot; è il nome predefinito del database che contiene ogni database e contenitore di schema in una sandbox. Quando si crea un [!DNL PostgreSQL] connessione tramite `dbname="all"`, puoi accedere a **qualsiasi** database e schema creati per organizzare i dati in modo logico.

Elenco di tutti i database in `dbname="all"` visualizza tre database disponibili.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

Elenco di tutti gli schemi in `dbname="all"` visualizza i tre schemi correlati a ogni database nella sandbox.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

Quando si crea un [!DNL PostgreSQL] connessione tramite `dbname="databaseA"`, è possibile accedere a qualsiasi schema associato a quel database specifico, come illustrato nell’esempio seguente.

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

La notazione del punto consente di accedere a ogni tabella associata a uno schema specifico connesso al database scelto. Tramite connessione a `DBNAME = databaseA.schema1;`, tutte le tabelle associate a tale schema specifico (`schema1`). Fornisce informazioni su quale set di dati contiene quale tabella.

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

## Aggiornare o rimuovere risorse di dati da un contenitore di dati

Man mano che la quantità di risorse di dati nell’organizzazione (o nella sandbox) aumenta, diventa necessario aggiornare o rimuovere le risorse di dati da un contenitore di dati. Le singole risorse possono essere rimosse dal contenitore organizzazione facendo riferimento al nome del database e dello schema appropriato utilizzando la notazione del punto. Tabella e vista (`t1` e `v1` rispettivamente) aggiunto a `databaseA.schema1` nel primo esempio, vengono rimossi utilizzando la sintassi dell&#39;esempio seguente.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Rimuovere risorse di dati

Il [RILASCIA TABELLA](../sql/syntax.md#drop-table) rimuove fisicamente una risorsa di dati solo dal [!DNL Data Lake] quando esiste un singolo riferimento alla tabella in tutti i database dell’organizzazione.

```sql
DROP TABLE databaseA.schema2.t1;
```

### Rimuovere un contenitore di risorse dati

È inoltre possibile rimuovere sia il database che lo schema utilizzando le funzioni SQL standard.

#### Rimuovere un database

Se esistono altri riferimenti alle risorse di dati associate al database, la funzione genera un errore quando si tenta di rimuovere il database.

```sql
DROP DATABASE databaseA;
```

#### Rimuovere uno schema

Durante la rimozione di uno schema è necessario tenere presenti tre considerazioni importanti:

- La rimozione di uno schema non comporta l’eliminazione fisica di risorse di dati quali tabelle, viste o tabelle temporanee.
- Se nello schema di destinazione sono presenti risorse di dati a cui si fa riferimento e la modalità è RESTRICT, viene generata un’eccezione.
- Se nello schema di destinazione sono presenti risorse di dati a cui si fa riferimento e la modalità è CASCADE, il sistema rimuove tutte le risorse di dati a cui fa riferimento il contenitore dello schema, quindi elimina il contenitore dello schema.

```sql
DROP SCHEMA databaseA.schema2;
```

## Passaggi successivi

La lettura di questo documento consente di comprendere meglio le best practice relative all’organizzazione e alla struttura delle risorse dati da utilizzare con Adobe Experience Platform Query Service. Si consiglia di continuare ad acquisire familiarità con le best practice di Query Service consultando [documentazione sulla deduplicazione dei dati](../essential-concepts/deduplication.md).
