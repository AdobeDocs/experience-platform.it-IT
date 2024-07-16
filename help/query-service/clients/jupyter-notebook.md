---
title: Connetti Jupyter Notebook a Query Service
description: Scopri come collegare Jupyter Notebook a Adobe Experience Platform Query Service.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Connetti [!DNL Jupyter Notebook] a Query Service

Questo documento descrive i passaggi necessari per connettere [!DNL Jupyter Notebook] a Adobe Experience Platform Query Service.

## Introduzione

Questa guida richiede che tu abbia già accesso a [!DNL Jupyter Notebook] e che tu abbia familiarità con la relativa interfaccia. Per scaricare [!DNL Jupyter Notebook] o per ulteriori informazioni, consulta la [documentazione [!DNL Jupyter Notebook] ufficiale](https://jupyter.org/).

Per acquisire le credenziali necessarie per la connessione di [!DNL Jupyter Notebook] a Experience Platform, è necessario avere accesso all&#39;area di lavoro [!UICONTROL Query] nell&#39;interfaccia utente di Platform. Contatta l&#39;amministratore dell&#39;organizzazione se al momento non hai accesso all&#39;area di lavoro [!UICONTROL Query].

>[!TIP]
>
>[!DNL Anaconda Navigator] è un&#39;interfaccia utente grafica (GUI) desktop che consente di installare e avviare con maggiore facilità i programmi [!DNL Python] comuni, ad esempio [!DNL Jupyter Notebook]. Consente inoltre di gestire pacchetti, ambienti e canali senza utilizzare i comandi della riga di comando.
>Segui il processo di installazione guidata sul loro sito Web per [installare la tua versione preferita dell&#39;applicazione](https://docs.anaconda.com/anaconda/install/).
>Dalla schermata iniziale di Anaconda Navigator, selezionare **[!DNL Jupyter Notebook]** dall&#39;elenco delle applicazioni supportate per avviare il programma.
>Ulteriori informazioni sono disponibili nella [documentazione ufficiale di Anaconda](https://docs.anaconda.com/anaconda/navigator/).

La documentazione ufficiale di Jupyter fornisce istruzioni per [eseguire il blocco appunti dall&#39;interfaccia della riga di comando](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Launch [!DNL Jupyter Notebook]

Dopo aver aperto una nuova applicazione Web [!DNL Jupyter Notebook], selezionare il menu a discesa **[!DNL New]** dall&#39;interfaccia utente, seguito da **[!DNL Python 3]** per creare un nuovo blocco appunti. Viene visualizzato l&#39;editor [!DNL Notebook].

Nella prima riga dell&#39;editor [!DNL Notebook] immettere il valore seguente: `pip install psycopg2-binary` e selezionare **[!DNL Run]** dalla barra dei comandi. Sotto la riga di input viene visualizzato un messaggio di operazione riuscita.

>[!IMPORTANT]
>
>Come parte di questo processo per formare una connessione, è necessario selezionare **[!DNL Run]** per eseguire ogni riga di codice.

Importare quindi un adattatore di database [!DNL PostgreSQL] per [!DNL Python]. Immettere il valore `import psycopg2` e selezionare **[!DNL Run]**. Nessun messaggio di operazione riuscita per questo processo. Se non viene visualizzato alcun messaggio di errore, procedere al passaggio successivo.

Immettere le credenziali Adobe Experience Platform immettendo il valore: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Le credenziali di connessione sono disponibili nella sezione [!UICONTROL Query] della scheda [!UICONTROL Credenziali] dell&#39;interfaccia utente di Platform. Per istruzioni dettagliate, consulta la documentazione su come [trovare le credenziali della tua organizzazione](../ui/credentials.md).

L’utilizzo di credenziali senza scadenza è consigliato quando si utilizzano client di terze parti per facilitare l’immissione ripetuta dei dettagli. Per istruzioni su [come generare e utilizzare credenziali senza scadenza](../ui/credentials.md#non-expiring-credentials), consulta la documentazione.

>[!IMPORTANT]
>
>Quando si copiano le credenziali dall’interfaccia utente di Platform, non è necessario formattarle ulteriormente. Possono essere forniti in una riga, con un singolo spazio tra le proprietà e i valori. Le credenziali sono racchiuse tra virgolette e **non** separate da virgola.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

L&#39;istanza [!DNL Jupyter Notebook] è ora connessa a Query Service.

## Esempio di esecuzione di una query

Dopo aver connesso [!DNL Jupyter Notebook] a Query Service, è possibile eseguire query sui set di dati utilizzando gli input di [!DNL Notebook]. Nell&#39;esempio seguente viene utilizzata una query semplice per illustrare il processo.

Immetti i seguenti valori:

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

Chiamare quindi il parametro (`data` nell&#39;esempio precedente) per visualizzare i risultati della query in una risposta non formattata.

Per formattare i risultati in modo più leggibile, utilizzare i seguenti comandi:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

Questi comandi non generano un messaggio di successo. Se non viene visualizzato alcun messaggio di errore, è possibile utilizzare una funzione per generare i risultati della query SQL in un formato tabella.

Immettere ed eseguire la funzione `df.head()` per visualizzare i risultati delle query tabulari.

## Passaggi successivi

Dopo aver stabilito la connessione a Query Service, è possibile utilizzare [!DNL Jupyter Notebook] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, leggere la [guida alle query in esecuzione](../best-practices/writing-queries.md).
