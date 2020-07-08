---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Set di dati e tabelle e schemi
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---


# Set di dati e tabelle e schemi

Esaminate l&#39;elenco dei set di dati disponibili nell&#39;interfaccia utente [del Adobe Experience Platform](https://platform.adobe.com/datasets), avendo cura di osservare i nomi dei set di dati.
>[!NOTE]
>
>Alcuni nomi di set di dati hanno spazi e potrebbero non essere sicuri per SQL.

![](../images/queries/datasets-and-tables/dataset-names.png)


Esaminare la struttura gerarchica dello schema del set di dati nell&#39;interfaccia utente facendo clic sul nome di uno schema nella tabella di dati.

![](../images/queries/datasets-and-tables/schema-information.png)

Aprite la riga di comando PSQL e utilizzate i dettagli di connessione da qui: [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration).

![](../images/clients/psql/connect-bi.png)

Per visualizzare le tabelle disponibili in Platform con SQL, è possibile utilizzare `\d` o `SHOW TABLES;`.


`\d` visualizza la visualizzazione PostSQL standard

```
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` è un comando personalizzato che offre una visualizzazione più dettagliata e presenta la tabella, nonché il nome del set di dati nell’interfaccia utente di Platform.

```
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

Per visualizzare lo schema principale di una tabella, utilizzare il `\d table_name` comando.

>[!NOTE]
>
>Lo schema presentato mostra i campi principali, la maggior parte dei quali complessi, che si riferiscono a un tipo di oggetto nell&#39;interfaccia utente dello schema DataSet.

`\d luma_midvalues`

```
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

Per approfondire lo schema, utilizzare caratteri di sottolineatura (`_`) per dichiarare la colonna nella tabella da descrivere. Ad esempio, `\d table_name_column`

`\d luma_midvalues_web`

```
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
