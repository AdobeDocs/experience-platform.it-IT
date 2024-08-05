---
keywords: Experience Platform;JupyterLab;notebook;Data Science Workspace;argomenti popolari;servizio query
solution: Experience Platform
title: Servizio query in Jupyter Notebook
type: Tutorial
description: Adobe Experience Platform consente di utilizzare SQL (Structured Query Language) in Data Science Workspace integrando Query Service in JupyterLab come funzione standard. Questo tutorial illustra query SQL di esempio per casi d’uso comuni per esplorare, trasformare e analizzare i dati di Adobe Analytics.
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---

# Servizio query in Jupyter Notebook

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto.
>
>Questa documentazione è destinata ai clienti esistenti che dispongono di diritti precedenti su Data Science Workspace.

[!DNL Adobe Experience Platform] consente di utilizzare SQL (Structured Query Language) in [!DNL Data Science Workspace] integrando [!DNL Query Service] in [!DNL JupyterLab] come funzionalità standard.

Questo tutorial illustra query SQL di esempio per casi d&#39;uso comuni per esplorare, trasformare e analizzare i dati [!DNL Adobe Analytics].

## Introduzione

Prima di iniziare questa esercitazione, è necessario disporre dei seguenti prerequisiti:

- Accesso a [!DNL Adobe Experience Platform]. Se non si dispone di accesso a un&#39;organizzazione in [!DNL Experience Platform], si prega di parlare con l&#39;amministratore di sistema prima di procedere

- Un [!DNL Adobe Analytics] dataset

- Una comprensione operativa dei seguenti concetti chiave utilizzati in questo esercitazione:
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## Accedi a [!DNL JupyterLab] e [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. In [[!DNL Experience Platform]](https://platform.adobe.com), passa a **[!UICONTROL Blocchi appunti]** dalla colonna di navigazione a sinistra. Attendere. Caricamento di JupyterLab.

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >Se non viene visualizzata automaticamente una nuova scheda di avvio, aprire una nuova scheda di avvio facendo clic su **[!UICONTROL File]**, quindi selezionare **[!UICONTROL Nuovo modulo di avvio]**.

2. Nella scheda di avvio fare clic sull&#39;icona **[!UICONTROL Vuoto]** in un ambiente Python 3 per aprire un blocco appunti vuoto.

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3 è attualmente l&#39;unico ambiente supportato per Query Service nei notebook.

3. Nella barra di selezione a sinistra, fai clic sull&#39;icona **[!UICONTROL Dati]** e fai doppio clic sulla directory **[!UICONTROL Set di dati]** per elencare tutti i set di dati.

   ![](../images/jupyterlab/query/dataset.png)

4. Trova un set di dati [!DNL Adobe Analytics] da esplorare e fai clic con il pulsante destro del mouse sull&#39;elenco, quindi fai clic su **[!UICONTROL Esegui query sui dati nel blocco appunti]** per generare query SQL nel blocco appunti vuoto.

5. Fare clic sulla prima cella generata contenente la funzione `qs_connect()` ed eseguirla facendo clic sul pulsante di riproduzione. Questa funzione crea una connessione tra l&#39;istanza del notebook e [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. Copiare il nome del set di dati [!DNL Adobe Analytics] dalla seconda query SQL generata. Sarà il valore dopo `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. Inserire una nuova cella del blocco appunti facendo clic sul pulsante **+**.

   ![](../images/jupyterlab/query/insert_cell.gif)

8. Copiare, incollare ed eseguire le istruzioni di importazione seguenti in una nuova cella. Queste istruzioni verranno utilizzate per visualizzare i dati:

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. Quindi, copia e incolla le seguenti variabili in una nuova cella. Modifica i valori in base alle esigenze, quindi eseguili.

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table`: nome del set di dati [!DNL Adobe Analytics].
   - `target_year`: anno specifico da cui provengono i dati di destinazione.
   - `target_month`: mese specifico per il quale proviene il destinazione.
   - `target_day`: giorno specifico per il quale provengono i dati destinazione.

   >[!NOTE]
   >
   >Puoi modificare questi valori in qualsiasi momento. Durante questa operazione, assicurati di eseguire la cella delle variabili per applicare le modifiche.

## Interrogare i dati {#query-your-data}

Immettere le seguenti query SQL nelle singole celle del blocco appunti. Esegui una query selezionando sulla relativa cella e selezionando il **[!UICONTROL pulsante di riproduzione]** . I risultati della query o i registri di errore vengono visualizzati sotto la cella eseguita.

Quando un blocco appunti è inattivo per un periodo di tempo prolungato, la connessione tra il blocco appunti e [!DNL Query Service] potrebbe interrompersi. In questi casi, riavviare [!DNL JupyterLab] selezionando il pulsante **Riavvia** ![Riavvia pulsante](/help/images/icons/restart.png) nell&#39;angolo superiore destro accanto al pulsante di alimentazione.

Il kernel del notebook si ripristina ma le celle rimarranno, eseguiranno nuovamente tutte le celle per continuare da dove si erano interrotte.

### Conteggio visitatori orari {#hourly-visitor-count}

La query seguente restituisce il conteggio dei visitatori orari per una data specificata:

#### Query

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

Nella query precedente, la marca temporale nella clausola `WHERE` è impostata sul valore di `target_year`. Includere le variabili nelle query SQL includendole tra parentesi graffe (`{}`).

La prima riga della query contiene la variabile facoltativa `hourly_visitor`. I risultati della query verranno memorizzati in questa variabile come un dataframe Pandas. L&#39;archiviazione dei risultati in un dataframe consente di visualizzare i risultati della query in un secondo momento utilizzando il pacchetto [!DNL Python] desiderato. Eseguire il codice [!DNL Python] seguente in una nuova cella per generare un grafico a barre:

```python
trace = go.Bar(
    x = hourly_visitor['Hour'],
    y = hourly_visitor['Visit_Count'],
    name = "Visitor Count"
)
layout = go.Layout(
    title = 'Visit Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)
fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

### Conteggio attività orarie {#hourly-activity-count}

La query seguente restituisce il conteggio delle azioni orarie per una data specificata:

#### Quesito <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

L&#39;esecuzione della query precedente store i risultati come `hourly_actions` frame di dati. Eseguire la seguente funzione in una nuova cella per visualizzare in anteprima i risultati:

```python
hourly_actions.head()
```

La query precedente può essere modificata per restituire il conteggio delle azioni orarie per un intervallo di date specificato utilizzando operatori **logici nella clausola WHERE** :

#### Quesito <!-- omit in toc -->

```sql
%%read_sql hourly_actions_date_range -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  timestamp >= TO_TIMESTAMP('2019-06-01 00', 'YYYY-MM-DD HH')
       AND timestamp <= TO_TIMESTAMP('2019-06-02 23', 'YYYY-MM-DD HH')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

L&#39;esecuzione della query modificata memorizza i risultati in `hourly_actions_date_range` come un dataframe. Esegui la funzione seguente in una nuova cella per visualizzare in anteprima i risultati:

```python
hourly_actions_date_rage.head()
```

### Numero di eventi per sessione visitatore {#number-of-events-per-visitor-session}

La query seguente restituisce il numero di eventi per sessione visitatore per una data specificata:

#### Query <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

Eseguire il codice seguente [!DNL Python] per generare un istogramma per il numero di eventi per visita sessione:

```python
data = [go.Histogram(x = events_per_session['Count'])]

layout = go.Layout(
    title = 'Histogram of Number of Events per Visit Session',
    xaxis = dict(title = 'Number of Events'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = data, layout = layout)
iplot(fig)
```

### Pagine popolari per un dato giorno {#popular-pages-for-a-given-day}

La query seguente restituisce le dieci pagine più popolari per una data specificata:

#### Query <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### Utenti attivi per un dato giorno {#active-users-for-a-given-day}

La query seguente restituisce i dieci utenti più attivi per una data specificata:

#### Query <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### Città attive per attività utente {#active-cities-by-user-activity}

La query seguente restituisce le dieci città che generano la maggior parte delle attività utente per una data specificata:

#### Query <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## Passaggi successivi

In questo tutorial sono stati illustrati alcuni esempi di utilizzo di [!DNL Query Service] in [!DNL Jupyter] notebook. Seguire la [esercitazione Analizzare i dati utilizzando Jupyter Notebooks](./analyze-your-data.md) per vedere come vengono eseguite operazioni simili utilizzando l&#39;SDK di accesso ai dati.
