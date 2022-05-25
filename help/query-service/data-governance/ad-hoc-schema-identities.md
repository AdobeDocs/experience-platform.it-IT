---
title: Impostare le identità principali in un set di dati ad hoc
description: Adobe Experience Platform Query Service consente di impostare un'identità o un'identità primaria per i campi di set di dati di schema ad hoc direttamente tramite il comando SQL ALTER TABLE. Il documento spiega come utilizzare il comando ALTER TABLE per impostare un'identità principale o secondaria.
source-git-commit: bf51fc3e0c9635c0555f87f3389fb4a9542c092d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Impostare le identità primarie in un set di dati ad hoc

Adobe Experience Platform Query Service consente di contrassegnare le colonne dei set di dati come identità principali o secondarie utilizzando i vincoli per SQL `ALTER TABLE` comando. Puoi utilizzare questa funzione per garantire che i campi contrassegnati siano coerenti con i requisiti di privacy dei dati. Questo comando consente di aggiungere o eliminare vincoli per le colonne della tabella di identità primaria e secondaria direttamente tramite SQL.

## Introduzione

Etichettare le colonne dei set di dati come identità primaria o secondaria richiede una comprensione del `ALTER TABLE` Comando SQL e una buona comprensione dei requisiti di privacy dei dati. Prima di continuare con questo documento, consulta la seguente documentazione:

* [Guida alla sintassi SQL per `ALTER TABLE` command](../sql/syntax.md).
* [Panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni.

## Aggiungere vincoli {#add-constraints}

La `ALTER TABLE` Il comando consente di etichettare una colonna di set di dati come identità di una persona e quindi utilizzarla come identità principale aggiornando i metadati associati utilizzando SQL. Questa funzione è particolarmente utile quando i set di dati vengono creati tramite SQL anziché direttamente da uno schema tramite l’interfaccia utente di Platform. Il comando può essere utilizzato per garantire che le operazioni sui dati all’interno di Platform siano conformi ai criteri di utilizzo dei dati.

**Esempi**

Nell&#39;esempio seguente viene aggiunto un vincolo all&#39;esistente `t1` tabella. I valori delle `id` le colonne sono ora contrassegnate come identità principali nella sezione `IDFA` spazio dei nomi. Uno spazio dei nomi di identità è una parola chiave che dichiara il tipo di dati di identità che il campo rappresenta.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

Il secondo esempio assicura che il `id` è contrassegnata come identità secondaria.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Limiti di rilascio {#drop-constraints}

I vincoli possono essere rimossi anche dalle colonne della tabella utilizzando `ALTER TABLE` comando.

**Esempi**

L&#39;esempio seguente elimina il requisito che il `c1` deve essere etichettata come identità principale nella colonna esistente `t1` tabella.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Come mostrato di seguito, la stessa sintassi viene utilizzata per rimuovere un vincolo di identità.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Mostra identità

Utilizzare il comando metadati `show identities` dall’interfaccia della riga di comando per visualizzare una tabella con ogni attributo assegnato come identità.

```shell
> show identities;
```

Di seguito è riportato un esempio di tabella restituita.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## Limiti XDM {#limitations}

Nell&#39;elenco seguente vengono illustrate considerazioni importanti sull&#39;aggiornamento delle identità nei set di dati esistenti quando si utilizza XDM.

* Per specificare una colonna come identità, è necessario **deve** definisci anche lo spazio dei nomi da mantenere come metadati per la colonna.
* XDM non supporta la specifica di un nome di colonna nell’attributo namespace.
* Se lo schema utilizza `identityMap` Campo XDM, radice o livello principale `identityMap` oggetto **deve** essere etichettate come identità o identità principale.
