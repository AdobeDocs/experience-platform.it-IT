---
solution: Experience Platform
title: Esplorare ed elaborare i dashboard della piattaforma di gestione dei dati grezzi
type: Documentation
description: Scopri come utilizzare Query Service per esplorare ed elaborare set di dati non elaborati che alimentano dashboard di profili, segmenti e destinazioni in Experience Platform.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: b9dd7584acc43b5946f8c0669d7a81001e44e702
workflow-type: tm+mt
source-wordcount: '738'
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

Le informazioni sul dashboard dei profili sono legate ai criteri di unione definiti dall’organizzazione. Per ogni criterio di unione attivo, è disponibile un set di dati di attributi di profilo nel data lake.

La convenzione di denominazione di questi set di dati è **Profilo-Snapshot-Export** seguita da un valore numerico alfanumerico casuale generato dal sistema. Ad esempio: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Per comprendere lo schema completo di ciascun set di dati di esportazione dello snapshot del profilo, puoi visualizzare in anteprima ed esplorare i set di dati [utilizzando il visualizzatore di set di dati](../catalog/datasets/user-guide.md) nell&#39;interfaccia utente di Experience Platform.

![](images/query/profile-attribute.png)

#### Mappatura dei set di dati degli attributi di profilo per unire gli ID dei criteri

Ogni set di dati di attributi di profilo si intitola **Esportazione snapshot di profilo** seguito da un valore numerico alfanumerico casuale generato dal sistema. Ad esempio: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Questo valore alfanumerico è una stringa casuale generata dal sistema e mappata su un ID di criteri di unione di uno dei criteri di unione creati dall&#39;organizzazione. La mappatura di ciascun ID criterio di unione alla relativa stringa di set di dati di attributi di profilo viene mantenuta nel set di dati `adwh_dim_merge_policies`.

Il set di dati `adwh_dim_merge_policies` contiene i campi seguenti:

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Questo set di dati può essere esplorato utilizzando l’interfaccia utente dell’Editor query in Experience Platform. Per ulteriori informazioni sull’utilizzo dell’editor delle query, consulta la [Guida all’interfaccia utente dell’editor delle query](../query-service/ui/user-guide.md).

### Set di dati dei metadati del segmento

È disponibile un set di dati per metadati del segmento nel lago di dati contenente metadati per ciascuno dei segmenti della tua organizzazione.

La convenzione di denominazione di questo set di dati è **Segmentdefinition-Snapshot-Export** seguita da un valore alfanumerico. Ad esempio: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Per comprendere lo schema completo di ciascun set di dati per l’esportazione di snapshot di definizione del segmento, puoi visualizzare in anteprima ed esplorare i set di dati [utilizzando il visualizzatore di set di dati](../catalog/datasets/user-guide.md) nell’interfaccia utente di Experience Platform.

![](images/query/segment-metadata.png)

### Set di dati metadati di destinazione

I metadati per tutte le destinazioni attivate della tua organizzazione sono disponibili come set di dati non elaborati nel lago di dati.

La convenzione di denominazione di questo set di dati è **DIM_Destination**.

Per comprendere lo schema completo del set di dati di destinazione DIM, puoi visualizzare in anteprima ed esplorare il set di dati [utilizzando il visualizzatore di set di dati](../catalog/datasets/user-guide.md) nell’interfaccia utente di Experience Platform.

![](images/query/destinations-metadata.png)

## Query di esempio

Le query di esempio seguenti includono SQL di esempio che possono essere utilizzate in Query Service per esplorare, verificare ed elaborare i set di dati non elaborati che alimentano le dashboard.

### Numero di profili per identità

Questa informazione approfondita del profilo fornisce un raggruppamento delle identità in tutti i profili uniti nel set di dati.

>[!NOTE]
>
>Il numero totale di profili per identità (in altre parole, l’aggiunta insieme dei valori mostrati per ogni spazio dei nomi) potrebbe essere superiore al numero totale di profili uniti, in quanto a un profilo potrebbero essere associati più namespace. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più namespace.

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
              Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
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
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      segment_id
```

## Passaggi successivi

Leggendo questa guida, ora puoi utilizzare Query Service per eseguire diverse query per esplorare ed elaborare i set di dati non elaborati che alimentano le dashboard di profili, segmenti e destinazioni.

Per ulteriori informazioni su ogni dashboard e sulle relative metriche, seleziona una dashboard dall’elenco delle dashboard disponibili nella navigazione della documentazione.
