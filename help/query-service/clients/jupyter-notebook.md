---
title: Connetti Jupyter Notebook a Query Service
description: Scopri come collegare Jupyter Notebook a Adobe Experience Platform Query Service.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Connetti [!DNL Jupyter Notebook] a Query Service

Questo documento descrive i passaggi necessari per la connessione [!DNL Jupyter Notebook] con Adobe Experience Platform Query Service.

## Introduzione

Questa guida richiede di avere già accesso a [!DNL Jupyter Notebook] e hanno familiarità con la relativa interfaccia. Per scaricare [!DNL Jupyter Notebook] o per ulteriori informazioni, consulta [ufficiale [!DNL Jupyter Notebook] documentazione](https://jupyter.org/).

Per acquisire le credenziali necessarie per la connessione [!DNL Jupyter Notebook] ad Experience Platform, devi avere accesso al [!UICONTROL Query] nell’interfaccia utente di Platform. Contatta l’amministratore dell’organizzazione se al momento non hai accesso a [!UICONTROL Query] Workspace.

>[!TIP]
>
>[!DNL Anaconda Navigator] è un&#39;interfaccia utente grafica (GUI) per desktop che offre un modo più semplice di installare e avviare [!DNL Python] programmi come [!DNL Jupyter Notebook]. Consente inoltre di gestire pacchetti, ambienti e canali senza utilizzare i comandi della riga di comando.
>Seguire la procedura di installazione guidata sul sito Web per [installare la versione preferita dell&#39;applicazione](https://docs.anaconda.com/anaconda/install/).
>Dalla schermata iniziale di Anaconda Navigator, selezionare **[!DNL Jupyter Notebook]** dall’elenco delle applicazioni supportate per avviare il programma.
>Ulteriori informazioni sono disponibili nella sezione [documentazione ufficiale di Anaconda](https://docs.anaconda.com/anaconda/navigator/).

La documentazione ufficiale di Jupyter fornisce istruzioni per [eseguire il blocco appunti dall&#39;interfaccia della riga di comando](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI)

## Launch [!DNL Jupyter Notebook]

Dopo aver aperto un nuovo [!DNL Jupyter Notebook] applicazione web, seleziona la **[!DNL New]** dall’interfaccia utente, seguito da **[!DNL Python 3]** per creare un nuovo blocco appunti. Il [!DNL Notebook] viene visualizzato l&#39;editor.

Sulla prima riga del [!DNL Notebook] , immetti il seguente valore: `pip install psycopg2-binary` e seleziona **[!DNL Run]** dalla barra dei comandi. Sotto la riga di input viene visualizzato un messaggio di operazione riuscita.

>[!IMPORTANT]
>
>Come parte di questo processo per formare una connessione, devi selezionare **[!DNL Run]** per eseguire ogni riga di codice.

Quindi, importa un [!DNL PostgreSQL] adattatore di database per [!DNL Python]. Immetti il valore: `import psycopg2`e seleziona **[!DNL Run]**. Nessun messaggio di operazione riuscita per questo processo. Se non viene visualizzato alcun messaggio di errore, procedere al passaggio successivo.

A questo punto è necessario fornire le credenziali Adobe Experience Platform immettendo il valore: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Le credenziali di connessione sono disponibili in [!UICONTROL Query] sezione, sotto [!UICONTROL Credenziali] dell’interfaccia utente di Platform. Consulta la documentazione su come [trova le credenziali della tua organizzazione](../ui/credentials.md) per istruzioni dettagliate.

L’utilizzo di credenziali senza scadenza è consigliato quando si utilizzano client di terze parti per facilitare l’immissione ripetuta dei dettagli. Per istruzioni su, consulta la documentazione di [come generare e utilizzare credenziali senza scadenza](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Quando si copiano le credenziali dall’interfaccia utente di Platform, non è necessario formattarle ulteriormente. Possono essere forniti in una riga, con un singolo spazio tra le proprietà e i valori. Le credenziali sono racchiuse tra virgolette e **non** separato da virgole.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Il tuo [!DNL Jupyter Notebook] L’istanza è ora connessa a Query Service.

## Esempio di esecuzione di una query

Ora che hai effettuato la connessione [!DNL Jupyter Notebook] In Query Service, puoi eseguire query sui set di dati utilizzando il tuo [!DNL Notebook] input. Nell&#39;esempio seguente viene utilizzata una query semplice per illustrare il processo.

Immetti i seguenti valori:

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

Quindi, chiama il parametro (`data` nell’esempio precedente) per visualizzare i risultati della query in una risposta non formattata.

Per formattare i risultati in modo più leggibile, utilizzare i seguenti comandi:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

Questi comandi non generano un messaggio di successo. Se non viene visualizzato alcun messaggio di errore, è possibile utilizzare una funzione per generare i risultati della query SQL in un formato tabella.

Inserisci ed esegui il `df.head()` per visualizzare i risultati della query tabularizzata.

## Passaggi successivi

Dopo aver stabilito la connessione a Query Service, puoi utilizzare [!DNL Jupyter Notebook] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, leggere [guida all’esecuzione delle query](../best-practices/writing-queries.md).
