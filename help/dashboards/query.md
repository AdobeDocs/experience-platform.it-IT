---
solution: Experience Platform
title: Esplorare ed elaborare set di dati grezzi che alimentano dashboard di Experience Platform
type: Documentation
description: Scopri come utilizzare Query Service per esplorare ed elaborare set di dati non elaborati che alimentano dashboard di profili, segmenti e destinazioni in Experience Platform.
source-git-commit: 743367431144e9714a967b0340c755bf2120559c
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---


# Esplorare, verificare ed elaborare i set di dati del dashboard tramite Query Service

Adobe Experience Platform fornisce informazioni importanti sul profilo, sui segmenti e sulle destinazioni dell’organizzazione tramite dashboard disponibili nell’interfaccia utente di Experience Platform. Puoi quindi utilizzare Adobe Experience Platform Query Service per esplorare, verificare ed elaborare i set di dati non elaborati che alimentano queste dashboard nel data lake.

## Guida introduttiva a Query Service

Adobe Experience Platform Query Service supporta gli addetti al marketing nell’acquisizione di informazioni dai loro dati consentendo l’utilizzo di SQL standard per eseguire query sui dati nel data lake. Query Service offre un’interfaccia utente e un’API che possono essere utilizzati per unire qualsiasi set di dati nel data lake e acquisire i risultati della query come nuovi set di dati da utilizzare nel reporting, nell’apprendimento automatico o per l’inserimento nel Profilo cliente in tempo reale.

Per ulteriori informazioni sul servizio query e sul suo ruolo all&#39;interno di Experience Platform, inizia leggendo la [Panoramica del servizio query](../query-service/home.md).

## Set di dati disponibili

Puoi utilizzare Query Service per eseguire query sui set di dati non elaborati per le dashboard di profili, segmenti e destinazioni. Nelle sezioni seguenti vengono descritti i set di dati non elaborati disponibili nel data lake.

### Set di dati degli attributi del profilo

Per ogni criterio di unione attivo nel Profilo cliente in tempo reale, è disponibile un set di dati di attributi di profilo nel lago di dati.

La convenzione di denominazione di questo set di dati è **Attributo profilo** seguito da un valore alfanumerico. Ad esempio: `Profile Attribute 14adf268-2a20-4dee-bee6-a6b0e34616a9`

Per comprendere lo schema completo del set di dati, puoi visualizzare in anteprima ed esplorare lo schema utilizzando il visualizzatore di set di dati nell’interfaccia utente di Experience Platform.

### Set di dati dei metadati del segmento

Nel data lake è disponibile un set di dati per i metadati del segmento per ciascuno dei segmenti della tua organizzazione.

La convenzione di denominazione di questo set di dati è **Definizione del segmento di profilo** seguita da un valore alfanumerico. Ad esempio: `Profile Segment Definition 6591ba8f-1422-499d-822a-543b2f7613a3`

L’immagine seguente mostra lo schema del set di dati dei metadati del segmento.

![](images/query/segment-metadata.png)

### Set di dati metadati di destinazione

I metadati per le destinazioni attivate sono disponibili come set di dati non elaborati nel data lake.

La convenzione di denominazione di questo set di dati è **DIM_Destination**.

L’immagine seguente mostra lo schema del set di dati dei metadati di destinazione.

![](images/query/destinations-metadata.png)

## Query di esempio

Le query di esempio seguenti includono SQL di esempio che possono essere utilizzate in Query Service per esplorare, verificare ed elaborare i set di dati non elaborati che alimentano le dashboard.

### Numero di profili per identità

Questa informazione approfondita del profilo fornisce un raggruppamento delle identità in tutti i profili uniti nel set di dati. Il numero totale di profili per identità (in altre parole, l’aggiunta insieme dei valori mostrati per ogni spazio dei nomi) potrebbe essere superiore al numero totale di profili uniti, in quanto a un profilo potrebbero essere associati più namespace. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più namespace.

**Query**

```sql
Select
        Key namespace,
        count(1) count_of_profiles
     from
        (
           Select
               explode(identitymap)
           from
              profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
        )
     group by
        namespace;
```

### Numero di profili per segmento

Questa profondità di pubblico fornisce il numero totale di profili uniti all’interno di ciascun segmento del set di dati. Questo numero è il risultato dell’applicazione dei criteri di unione dei segmenti ai dati del profilo per unire i frammenti di profilo in modo da formare un unico profilo per ogni individuo nel segmento.

```sql
Select          
        concat_ws('-', key, source_namespace) segment_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Segmentmembership)
                  from
                    profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
              )
        )
      group by
      segment_id
```

### Numero di segmenti attivati per destinazione per tutte le destinazioni

## Passaggi successivi

Leggendo questa guida, ora puoi utilizzare Query Service per eseguire diverse query per esplorare ed elaborare i set di dati non elaborati che alimentano le dashboard di profili, segmenti e destinazioni.

Per ulteriori informazioni su ogni dashboard e sulle relative metriche, seleziona una dashboard dall’elenco delle dashboard disponibili nella navigazione della documentazione.
