---
keywords: Experience Platform;home;argomenti popolari;Query service;servizio query;RStudio;rstudio;connect to query service;
solution: Experience Platform
title: Connetti Studio a Query Service
description: Questo documento illustra i passaggi necessari per la connessione di R Studio a Adobe Experience Platform Query Service.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Connetti [!DNL RStudio] a Query Service

Questo documento illustra i passaggi necessari per la connessione di [!DNL RStudio] a Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> [!DNL RStudio] è stato rinominato come [!DNL Posit]. [!DNL RStudio] prodotti sono stati rinominati in [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package] Manager, [!DNL Posit Cloud] e [!DNL Posit Academy].
>
> Questa guida presuppone che tu abbia già accesso a [!DNL RStudio] e che tu abbia familiarità con le modalità di utilizzo. Ulteriori informazioni su [!DNL RStudio] sono disponibili nella [documentazione [!DNL RStudio] ufficiale](https://rstudio.com/products/rstudio/).
> 
> Inoltre, per utilizzare [!DNL RStudio] con Query Service, è necessario installare il driver JDBC 4.2 di [!DNL PostgreSQL]. È possibile scaricare il driver JDBC dal [[!DNL PostgreSQL] sito ufficiale](https://jdbc.postgresql.org/download/).

## Crea una connessione [!DNL Query Service] nell&#39;interfaccia [!DNL RStudio]

Dopo aver installato [!DNL RStudio], è necessario installare il pacchetto RJDBC. Le istruzioni su come [connettere un database tramite la riga di comando](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) sono disponibili nella documentazione ufficiale di Posit.

Se utilizzi un sistema operativo Mac, puoi selezionare **[!UICONTROL Strumenti]** dalla barra dei menu, quindi **[!UICONTROL Installa pacchetti]** dal menu a discesa. In alternativa, selezionare la scheda **[!DNL Packages]** dall&#39;interfaccia utente di Studio e selezionare **[!DNL Install]**.

Viene visualizzato un pop-up che mostra la schermata **[!DNL Install Packages]**. Assicurarsi che **[!DNL Repository (CRAN)]** sia selezionato per la sezione **[!DNL Install from]**. Il valore per **[!DNL Packages]** deve essere `RJDBC`. Assicurarsi che **[!DNL Install dependencies]** sia selezionato. Dopo aver confermato che tutti i valori sono corretti, selezionare **[!DNL Install]** per installare i pacchetti. Dopo aver installato il pacchetto RJDBC, riavviare [!DNL RStudio] per completare il processo di installazione.

Dopo il riavvio di [!DNL RStudio], è ora possibile connettersi a Query Service. Selezionare il pacchetto **[!DNL RJDBC]** nel riquadro **[!DNL Packages]** e immettere il comando seguente nella console:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Dove `{PATH TO THE POSTGRESQL JDBC JAR}` rappresenta il percorso del JAR JDBC [!DNL PostgreSQL] installato nel computer.

Ora puoi creare la tua connessione a Query Service. Immetti il seguente comando nella console:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Consulta la [[!DNL Query Service] documentazione SSL](./ssl-modes.md) per informazioni sul supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e su come connettersi utilizzando la modalità SSL `verify-full`.

Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere la [guida delle credenziali](../ui/credentials.md). Per trovare le credenziali, accedi a [!DNL Experience Platform], quindi seleziona **[!UICONTROL Query]**, seguito da **[!UICONTROL Credenziali]**.

Un messaggio nell’output della console conferma la connessione a Query Service.

## Scrittura delle query

Dopo aver stabilito la connessione a [!DNL Query Service], è possibile scrivere query per eseguire e modificare istruzioni SQL. È ad esempio possibile utilizzare `dbGetQuery(con, sql)` per eseguire query, dove `sql` è la query SQL che si desidera eseguire.

La query seguente utilizza un set di dati contenente [Eventi esperienza](../../xdm/classes/experienceevent.md) e crea un istogramma delle visualizzazioni di pagina di un sito Web, data l&#39;altezza dello schermo del dispositivo.

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

In caso di esito positivo, la risposta restituisce i risultati della query:

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

Per ulteriori informazioni su come scrivere ed eseguire query, leggere la guida in [esecuzione di query](../best-practices/writing-queries.md).
