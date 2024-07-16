---
title: Impostare le identità primarie in un set di dati ad hoc
description: Adobe Experience Platform Query Service consente di impostare un’identità o un’identità primaria per i campi di set di dati dello schema ad hoc direttamente tramite il comando SQL ALTER TABLE. Nel documento viene illustrato come utilizzare il comando ALTER TABLE per impostare un'identità primaria o secondaria.
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: d9c3ccdf0c0e191af1ab18e894688f301378156d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Impostare le identità primarie in un set di dati ad hoc

Adobe Experience Platform Query Service consente di contrassegnare le colonne dei set di dati come identità primarie o secondarie utilizzando i vincoli per il comando SQL `ALTER TABLE`. Puoi utilizzare questa funzione per garantire che i campi contrassegnati siano coerenti con i requisiti sulla privacy dei dati. Questo comando consente di aggiungere o eliminare vincoli per le colonne della tabella delle identità primaria e secondaria direttamente tramite SQL.

## Introduzione

Per etichettare le colonne del set di dati come identità primaria o secondaria è necessario conoscere il comando SQL `ALTER TABLE` e comprendere correttamente i requisiti di privacy dei dati. Prima di continuare con questo documento, consulta la seguente documentazione:

* [Guida alla sintassi SQL per il comando `ALTER TABLE`](../sql/syntax.md).
* [Panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni.

## Aggiungere vincoli {#add-constraints}

Il comando `ALTER TABLE` consente di etichettare una colonna di set di dati come identità di una persona e quindi di utilizzare tale etichetta come identità primaria aggiornando i metadati associati tramite SQL. Questa funzione è particolarmente utile quando i set di dati vengono creati tramite SQL anziché direttamente da uno schema tramite l’interfaccia utente di Platform. Il comando può essere utilizzato per garantire che le operazioni sui dati in Platform siano conformi ai criteri di utilizzo dei dati.

**Esempi**

Nell&#39;esempio seguente viene aggiunto un vincolo alla tabella `t1` esistente. I valori della colonna `id` sono ora contrassegnati come identità primarie nello spazio dei nomi `IDFA`. Uno spazio dei nomi di identità è una parola chiave che dichiara il tipo di dati di identità che il campo rappresenta.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

Il secondo esempio assicura che la colonna `id` sia contrassegnata come identità secondaria.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Elimina vincoli {#drop-constraints}

I vincoli possono essere rimossi anche dalle colonne della tabella utilizzando il comando `ALTER TABLE`.

**Esempi**

Nell&#39;esempio seguente viene rimosso il requisito che la colonna `c1` sia etichettata come identità primaria nella tabella `t1` esistente.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Come mostrato di seguito, la stessa sintassi viene utilizzata per la rimozione di un vincolo di identità.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Mostra identità

Utilizzare il comando metadati `show identities` dall&#39;interfaccia della riga di comando per visualizzare una tabella con tutti gli attributi assegnati come identità.

```shell
> show identities;
```

Di seguito è riportato un esempio di tabella restituita.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## Limitazioni di XDM {#limitations}

L’elenco seguente spiega considerazioni importanti per l’aggiornamento delle identità nei set di dati esistenti quando si utilizza XDM.

* Per specificare una colonna come identità, **è necessario** definire anche lo spazio dei nomi da mantenere come metadati per la colonna.
* XDM non supporta la specifica di un nome di colonna nell’attributo namespace.
* Se lo schema utilizza il campo XDM `identityMap`, l&#39;oggetto **principale o di primo livello `identityMap` deve** essere etichettato come identità o identità primaria.
