---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;RStudio;rstudio;connettersi al servizio query;
solution: Experience Platform
title: Collegare lo studio al servizio query
topic-legacy: connect
description: Questo documento descrive i passaggi necessari per la connessione di R Studio con Adobe Experience Platform Query Service.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Connetti [!DNL RStudio] al servizio query

Questo documento descrive i passaggi necessari per la connessione di [!DNL RStudio] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL RStudio] e che tu abbia familiarità con come usarlo. Ulteriori informazioni su [!DNL RStudio] sono disponibili nella [documentazione [!DNL RStudio] ufficiale](https://rstudio.com/products/rstudio/).
> 
> Inoltre, per utilizzare RStudio con Query Service, è necessario installare il driver PostgreSQL JDBC 4.2. È possibile scaricare il driver JDBC dal sito ufficiale [PostgreSQL](https://jdbc.postgresql.org/download.html).

## Creare una connessione [!DNL Query Service] nell&#39;interfaccia [!DNL RStudio]

Dopo aver installato [!DNL RStudio], è necessario installare il pacchetto RJDBC. Vai al riquadro **[!DNL Packages]** e seleziona **[!DNL Install]**.

![](../images/clients/rstudio/install-package.png)

Viene visualizzato un pop-up che mostra la schermata **[!DNL Install Packages]**. Assicurati che sia selezionato **[!DNL Repository (CRAN)]** per la sezione **[!DNL Install from]** . Il valore di **[!DNL Packages]** deve essere `RJDBC`. Assicurati che sia selezionato **[!DNL Install dependencies]**. Dopo aver confermato che tutti i valori sono corretti, seleziona **[!DNL Install]** per installare i pacchetti.

![](../images/clients/rstudio/install-jrdbc.png)

Ora che il pacchetto RJDBC è stato installato, riavviare RStudio per completare il processo di installazione.

Dopo il riavvio di RStudio, è ora possibile connettersi a Query Service. Seleziona il pacchetto **[!DNL RJDBC]** nel riquadro **[!DNL Packages]** e immetti il seguente comando nella console:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Dove {PATH TO THE POSTGRESQL JDBC} rappresenta il percorso del JAR JDBC PostgreSQL installato sul computer.

Ora è possibile creare la connessione a Query Service immettendo il seguente comando nella console:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!NOTE]
>
>Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere la [guida alle credenziali](../ui/credentials.md). Per trovare le tue credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguito da **[!UICONTROL Credenziali]**.

![](../images/clients/rstudio/connection-rjdbc.png)

## Scrittura di query

Dopo aver effettuato la connessione a [!DNL Query Service], è possibile scrivere query per eseguire e modificare le istruzioni SQL. Ad esempio, è possibile utilizzare `dbGetQuery(con, sql)` per eseguire le query, dove `sql` è la query SQL che si desidera eseguire.

La seguente query utilizza un set di dati contenente [Eventi esperienza](../best-practices/experience-event-queries.md) e crea un istogramma di visualizzazioni di pagina di un sito web, in base all&#39;altezza dello schermo del dispositivo.

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

Per ulteriori informazioni su come scrivere ed eseguire le query, leggere la guida sull&#39; [esecuzione delle query](../best-practices/writing-queries.md).
