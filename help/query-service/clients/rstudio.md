---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;RStudio;rstudio;connettersi al servizio query;
solution: Experience Platform
title: Collegare lo studio al servizio query
description: Questo documento descrive i passaggi necessari per la connessione di R Studio con Adobe Experience Platform Query Service.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Connetti [!DNL RStudio] al servizio query

Questo documento descrive i passaggi necessari per la connessione [!DNL RStudio] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL RStudio] e sono a conoscenza di come usarlo. Ulteriori informazioni [!DNL RStudio] si trova nella [ufficiale [!DNL RStudio] documentazione](https://rstudio.com/products/rstudio/).
> 
> Inoltre, per utilizzare [!DNL RStudio] con Query Service, è necessario installare [!DNL PostgreSQL] Driver JDBC 4.2. È possibile scaricare il driver JDBC dal [[!DNL PostgreSQL] sito ufficiale](https://jdbc.postgresql.org/download/).

## Crea un [!DNL Query Service] connessione [!DNL RStudio] interfaccia

Dopo l&#39;installazione [!DNL RStudio], devi installare il pacchetto RJDBC. Vai a **[!DNL Packages]** e seleziona **[!DNL Install]**.

![La [!DNL RStudio] dashboard con pacchetti e installazione evidenziata.](../images/clients/rstudio/install-package.png)

Viene visualizzato un pop-up che mostra la **[!DNL Install Packages]** schermo. Assicurati che **[!DNL Repository (CRAN)]** è selezionato per **[!DNL Install from]** sezione . Valore per **[!DNL Packages]** devono `RJDBC`. Assicurati **[!DNL Install dependencies]** è selezionato. Dopo aver confermato la correttezza di tutti i valori, seleziona **[!DNL Install]** per installare i pacchetti.

![La finestra di dialogo Installa pacchetti con RJDBC è stata inserita nel campo Pacchetti e Installa evidenziata.](../images/clients/rstudio/install-jrdbc.png)

Ora che il pacchetto RJDBC è stato installato, riavvia [!DNL RStudio] per completare il processo di installazione.

Dopo [!DNL RStudio] riavviato, è ora possibile connettersi al servizio query. Seleziona la **[!DNL RJDBC]** nel pacchetto **[!DNL Packages]** e immetti il comando seguente nella console:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Dove `{PATH TO THE POSTGRESQL JDBC JAR}` rappresenta il percorso della [!DNL PostgreSQL] JDBC JAR installato sul tuo computer.

Ora è possibile creare la connessione a Query Service. Immetti il seguente comando nella console:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Consulta la sezione [[!DNL Query Service] Documentazione SSL](./ssl-modes.md) per informazioni sul supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e su come connettersi utilizzando `verify-full` Modalità SSL.

Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere il [guida alle credenziali](../ui/credentials.md). Per trovare le tue credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguita da **[!UICONTROL Credenziali]**.

![Uscita della console in [!DNL RStudio] dalla connessione a Query Service.](../images/clients/rstudio/connection-rjdbc.png)

## Scrittura di query

Ora che ti sei connesso a [!DNL Query Service], è possibile scrivere query per eseguire e modificare le istruzioni SQL. Ad esempio, puoi utilizzare `dbGetQuery(con, sql)` per eseguire query, dove `sql` è la query SQL che si desidera eseguire.

La seguente query utilizza un set di dati contenente [Eventi esperienza](../sample-queries/experience-event.md) crea un istogramma delle visualizzazioni di pagina di un sito web, in base all&#39;altezza dello schermo del dispositivo.

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

Per ulteriori informazioni su come scrivere ed eseguire le query, leggere la guida in [query in esecuzione](../best-practices/writing-queries.md).
