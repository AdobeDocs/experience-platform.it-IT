---
keywords: Experience Platform;home;popular topics;Query service;query service;RStudio;rstudio;connect to query service;
solution: Experience Platform
title: Connessione con RStudio
topic: connect
description: In questo documento vengono descritti i passaggi per la connessione di R Studio con Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 2%

---


# Connetti con [!DNL RStudio]

Questo documento descrive i passaggi per la connessione di R Studio con Adobe Experience Platform [!DNL Query Service].

Dopo l&#39;installazione di [!DNL RStudio], nella schermata *Console* visualizzata, sarà prima necessario preparare lo script R per utilizzare [!DNL PostgreSQL].

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

Dopo aver preparato lo script R per l&#39;utilizzo di [!DNL PostgreSQL], è ora possibile connettersi [!DNL RStudio] a [!DNL Query Service] caricando il driver [!DNL PostgreSQL].

```r
drv <- dbDriver("PostgreSQL")
con <- dbConnect(drv, 
 dbname = "{DATABASE_NAME}",
 host="{HOST_NUMBER}",
 port={PORT_NUMBER},
 user="{USERNAME}",
 password="{PASSWORD}")
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{DATABASE_NAME}` | Nome del database che verrà utilizzato. |
| `{HOST_NUMBER` ed `{PORT_NUMBER}` | L&#39;endpoint host e la relativa porta per il servizio query. |
| `{USERNAME}` ed `{PASSWORD}` | Le credenziali di accesso che verranno utilizzate. Il nome utente assume la forma di `ORG_ID@AdobeOrg`. |

>[!NOTE]
>
>Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, visitare la pagina delle [credenziali sulla piattaforma](https://platform.adobe.com/query/configuration). Per trovare le credenziali, accedere a [!DNL Platform], fare clic su **[!UICONTROL Queries]**, quindi su **[!UICONTROL Credentials]**.

## Passaggi successivi

Ora che si è connessi a [!DNL Query Service], è possibile scrivere query per eseguire e modificare le istruzioni SQL. Ad esempio, è possibile utilizzare `dbGetQuery(con, sql)` per eseguire query, dove `sql` è la query SQL da eseguire.

La seguente query utilizza un dataset contenente [ExperienceEvents](../best-practices/experience-event-queries.md) e crea un istogramma delle visualizzazioni di pagina di un sito Web, in base all&#39;altezza dello schermo del dispositivo.

```sql
df_pageviews <- dbGetQuery(con,
"SELECT t.range AS buckets, 
 Count(*) AS pageviews 
FROM (SELECT CASE 
 WHEN device.screenheight BETWEEN 0 AND 99 THEN '0 - 99' 
 WHEN device.screenheight BETWEEN 100 AND 199 THEN '100-199' 
 WHEN device.screenheight BETWEEN 200 AND 299 THEN '200-299' 
 WHEN device.screenheight BETWEEN 300 AND 399 THEN '300-399' 
 WHEN device.screenheight BETWEEN 400 AND 499 THEN '400-499' 
 WHEN device.screenheight BETWEEN 500 AND 599 THEN '500-599' 
 ELSE '600-699' 
 end AS range 
 FROM aa_post_vals_3) t 
GROUP BY t.range 
ORDER BY buckets 
LIMIT 1000000")
```

Una risposta corretta restituisce i risultati della query:

```r
df_pageviews
 buckets pageviews
1 0 - 99 198985
2 500-599 67138
3 300-399 2147
4 200-299 354
5 400-499 6947
6 100-199 4415
7 600-699 3097040
```

Per ulteriori informazioni su come scrivere ed eseguire query, consultare la [guida alle query in esecuzione](../best-practices/writing-queries.md).