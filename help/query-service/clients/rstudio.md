---
keywords: ' Experience Platform;home;argomenti popolari;Query service;query service;RStudio;rstudio;connect to query service;'
solution: Experience Platform
title: Connessione RSudio a Query Service
topic: connect
description: In questo documento vengono descritti i passaggi per la connessione di R Studio con Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: f1b2fd7efd43f317a85c831cd64c09be29688f7a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Connetti [!DNL RStudio] al servizio query

Questo documento descrive i passaggi per la connessione di [!DNL RStudio] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che abbiate già accesso a [!DNL RStudio] e che abbiate familiarità con come usarlo. Ulteriori informazioni su [!DNL RStudio] sono disponibili nella [documentazione  [!DNL RStudio] ufficiale](https://rstudio.com/products/rstudio/).
> 
> Inoltre, per utilizzare RStudio con Query Service, è necessario installare il driver PostgreSQL JDBC 4.2. È possibile scaricare il driver JDBC dal [sito ufficiale PostgreSQL](https://jdbc.postgresql.org/download.html).

## Creare una connessione [!DNL Query Service] nell&#39;interfaccia [!DNL RStudio]

Dopo aver installato [!DNL RStudio], è necessario installare il pacchetto RJDBC. Fare clic sul riquadro **[!DNL Packages]** e selezionare **[!DNL Install]**.

![](../images/clients/rstudio/install-package.png)

Viene visualizzato un pop-up che mostra la schermata **[!DNL Install Packages]**. Assicurarsi che **[!DNL Repository (CRAN)]** sia selezionato per la sezione **[!DNL Install from]**. Il valore di **[!DNL Packages]** deve essere `RJDBC`. Assicurarsi che **[!DNL Install dependencies]** sia selezionato. Dopo aver confermato che tutti i valori sono corretti, selezionare **[!DNL Install]** per installare i pacchetti.

![](../images/clients/rstudio/install-jrdbc.png)

Dopo aver installato il pacchetto RJDBC, riavviare RStudio per completare il processo di installazione.

Dopo il riavvio di RStudio, ora è possibile connettersi a Query Service. Selezionate il pacchetto **[!DNL RJDBC]** nel riquadro **[!DNL Packages]** e immettete il comando seguente nella console:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Dove {PATH TO THE POSTGRESQL JDBC JAR} rappresenta il percorso del JAR JDBC JAR PostgreSQL installato sul computer.

A questo punto, è possibile creare la connessione a Query Service immettendo il seguente comando nella console:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!NOTE]
>
>Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, visitare la pagina delle [credenziali sulla piattaforma](https://platform.adobe.com/query/configuration). Per trovare le credenziali, accedere a [!DNL Platform], quindi selezionare **[!UICONTROL Queries]**, seguito da **[!UICONTROL Credentials]**.

![](../images/clients/rstudio/connection-rjdbc.png)

## Scrittura di query

Ora che si è connessi a [!DNL Query Service], è possibile scrivere query per eseguire e modificare le istruzioni SQL. Ad esempio, è possibile utilizzare `dbGetQuery(con, sql)` per eseguire query, dove `sql` è la query SQL da eseguire.

La seguente query utilizza un dataset contenente [Eventi esperienza](../best-practices/experience-event-queries.md) e crea un istogramma delle visualizzazioni di pagina di un sito Web, in base all&#39;altezza dello schermo del dispositivo.

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

## Passaggi successivi

Per ulteriori informazioni su come scrivere ed eseguire query, consultare la guida in [esecuzione query](../best-practices/writing-queries.md).