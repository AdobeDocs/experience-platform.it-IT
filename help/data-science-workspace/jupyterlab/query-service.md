---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Servizio query nel blocco appunti Jupyter
topic: Tutorial
translation-type: tm+mt
source-git-commit: d0596dc3c744e192c4d2ad04d6365846a0115371

---


# Servizio query nel blocco appunti Jupyter

Adobe Experience Platform consente di utilizzare il linguaggio SQL (Structures Query Language) in Data Science Workspace integrando il servizio Query in JupyterLab come funzione standard.

Questa esercitazione illustra i seguenti esempi di query SQL per i casi di utilizzo più comuni per esplorare, trasformare e analizzare i dati di Adobe Analytics:

- [Accesso a JupyterLab e al servizio Query](#access-jupyterlab-and-query-service)
- [Query dei dati](#query-your-data)
   - [Conteggio orario dei visitatori](#hourly-visitor-count)
   - [Conteggio attività orario](#hourly-activity-count)
   - [Numero di eventi per sessione visitatore](#number-of-events-per-visitor-session)
   - [Pagine popolari per un dato giorno](#popular-pages-for-a-given-day)
   - [Utenti attivi per un dato giorno](#active-users-for-a-given-day)
   - [Città attive per attività utente](#active-cities-by-user-activity)

## Introduzione

Prima di iniziare questa esercitazione, è necessario disporre dei seguenti prerequisiti:

- Accesso ad Adobe Experience Platform. Se non disponete dell&#39;accesso a un&#39;organizzazione IMS in Experience Platform, rivolgetevi al vostro amministratore di sistema prima di procedere

- Un dataset di Adobe Analytics

- Una conoscenza approfondita dei seguenti concetti chiave utilizzati in questa esercitazione:
   - [Experience Data Model (XDM) e XDM System](../../xdm/home.md)
   - [Servizio query](../../query-service/home.md)
   - [Sintassi SQL Servizio query](../../query-service/sql/overview.md)
   - Adobe Analytics

## Accesso a JupyterLab e al servizio Query

1. In [Experience Platform](https://platform.adobe.com), andate a **Modelli** dalla colonna di navigazione a sinistra. Fate clic su **Blocco note** nell’intestazione superiore per aprire JupyterLab. Lasciate che venga caricato JupyterLab al momento.

   ![](../images/jupyterlab/query/notebook_ui.png)

   > [!NOTE] Se non viene visualizzata automaticamente una nuova scheda Avvio, apri una nuova scheda Avvio facendo clic su **File > Nuovo avvio**.

2. Nella scheda Launcher, fai clic sull&#39;icona **Vuoto** in un ambiente Python 3 per aprire un blocco appunti vuoto.

   ![](../images/jupyterlab/query/blank_notebook.png)

   > [!NOTE] Python 3 è attualmente l&#39;unico ambiente supportato per il servizio query nei notebook.

3. Nella barra di selezione a sinistra, fai clic sull&#39;icona **Dati** e fai doppio clic sulla directory **Set** dati per elencare tutti i set di dati.

   ![](../images/jupyterlab/query/dataset.png)

4. Trovate un set di dati di Adobe Analytics da esplorare e fate clic con il pulsante destro del mouse sull&#39;elenco, fate clic su Dati **query nel blocco appunti** per generare query SQL nel blocco appunti vuoto.

5. Fare clic sulla prima cella generata contenente la funzione `qs_connect()` ed eseguirla facendo clic sul pulsante di riproduzione. Questa funzione crea una connessione tra l&#39;istanza del blocco appunti e il servizio di query.

   ![](../images/jupyterlab/query/execute.png)

6. Copiate il nome del set di dati di Adobe Analytics dalla seconda query SQL generata, che sarà il valore successivo `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. Inserire una nuova cella blocco appunti facendo clic sul pulsante **+** .

   ![](../images/jupyterlab/query/insert_cell.gif)

8. Copiare, incollare ed eseguire le seguenti istruzioni di importazione in una nuova cella. Queste istruzioni verranno utilizzate per visualizzare i dati:

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. Quindi, copiate e incollate le seguenti variabili in una nuova cella. Modificate i valori in base alle esigenze, quindi eseguiteli.

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table` : Nome del set di dati di Adobe Analytics.
   - `target_year` : Anno specifico da cui provengono i dati obiettivo.
   - `target_month` : Mese specifico da cui proviene il target.
   - `target_day` : Giorno specifico da cui provengono i dati di destinazione.
   >[!NOTE] Potete modificare questi valori in qualsiasi momento. In questo modo, accertatevi di eseguire la cella delle variabili per le modifiche da applicare.

## Query dei dati

Immettere le seguenti query SQL nelle singole celle del blocco appunti. Per eseguire una query, fare clic sulla cella corrispondente, quindi fare clic sul pulsante di **riproduzione** . I risultati delle query o i registri degli errori vengono visualizzati sotto la cella eseguita.

Quando un blocco appunti è inattivo per un periodo di tempo prolungato, la connessione tra il blocco appunti e il servizio query potrebbe interrompersi. In questi casi, riavviare JupyterLab facendo clic sul pulsante **Power** situato nell&#39;angolo superiore destro.

![](../images/jupyterlab/query/restart_button.png)

Il kernel del notebook verrà reimpostato, ma le celle rimarranno, rieseguire **tutte** le celle per continuare dove si era lasciato.

### Conteggio orario dei visitatori

La seguente query restituisce il conteggio orario dei visitatori per una data specificata:

#### Query

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP  BY Day, Hour
ORDER  BY Hour;
```

Nella query precedente, la destinazione `_acp_year` nella `WHERE` clausola è impostata sul valore di `target_year`. Includere le variabili nelle query SQL includendole tra parentesi graffe (`{}`).

La prima riga della query contiene la variabile opzionale `hourly_visitor`. I risultati della query verranno memorizzati in questa variabile come fotogramma dati Pandas. La memorizzazione dei risultati in un dataframe consente di visualizzare in seguito i risultati della query utilizzando un pacchetto Python desiderato. Per generare un grafico a barre, eseguite il seguente codice Python in una nuova cella:

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

### Conteggio attività orario

La seguente query restituisce il conteggio delle azioni orarie per una data specificata:

#### Query <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  _acp_year = {target_year} 
       AND _acp_month = {target_month}  
       AND _acp_day = {target_day}
GROUP  BY Day, Hour
ORDER  BY Hour;
```

L&#39;esecuzione della query di cui sopra memorizzerà i risultati in `hourly_actions` una cornice dati. Esegui la seguente funzione in una nuova cella per visualizzare in anteprima i risultati:

```python
hourly_actions.head()
```

La query di cui sopra può essere modificata per restituire il conteggio delle azioni orarie per un intervallo di date specificato utilizzando gli operatori logici nella clausola **WHERE** :

#### Query <!-- omit in toc -->

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

Se si esegue la query modificata, i risultati vengono memorizzati `hourly_actions_date_range` come fotogramma dati. Esegui la seguente funzione in una nuova cella per visualizzare in anteprima i risultati:

```python
hourly_actions_date_rage.head()
```

### Numero di eventi per sessione visitatore

La seguente query restituisce il numero di eventi per sessione visitatore per una data specificata:

#### Query <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE  _acp_year = {target_year} 
       AND _acp_month = {target_month}  
       AND _acp_day = {target_day}
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

Eseguite il seguente codice Python per generare un istogramma per il numero di eventi per sessione visita:

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

### Pagine popolari per un dato giorno

La seguente query restituisce le dieci pagine più popolari per una data specificata:

#### Query <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### Utenti attivi per un dato giorno

La seguente query restituisce i dieci utenti più attivi per una data specificata:

#### Query <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### Città attive per attività utente

La seguente query restituisce le dieci città che stanno generando la maggior parte delle attività utente per una data specificata:

#### Query <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## Passaggi successivi <!-- omit in toc -->

Questa esercitazione ha mostrato alcuni esempi di utilizzo di Query Service nei notebook Jupyter. Segui l’esercitazione [Analizza i dati utilizzando Jupyter Notebooks](./analyze-your-data.md) per vedere come vengono eseguite operazioni simili con l’SDK per l’accesso ai dati.