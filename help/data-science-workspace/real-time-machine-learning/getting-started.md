---
keywords: Experience Platform; guida per sviluppatori; Data Science Area di lavoro; argomenti popolari; Machine learning in tempo reale;
solution: Experience Platform
title: Guida introduttiva con il machine learning in tempo reale
description: Nel documento seguente vengono descritti i passaggi necessari per creare un modello di Machine Learning in tempo reale in Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Guida introduttiva al machine learning in tempo reale (Alpha)

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

>[!IMPORTANT]
>
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in versione alpha ed è ancora in fase di test. Questo documento è soggetto a modifiche.

Per utilizzare l&#39;apprendimento automatico in tempo reale, è necessario disporre di accesso a un&#39;organizzazione provvista di Adobe Experience Platform e [!DNL Data Science Workspace]. Inoltre, è necessario disporre di un set di dati completo da utilizzare nel training e nel punteggio.

Le guide per l&#39;apprendimento automatico in tempo reale richiedono una conoscenza pratica di Python 3, [Jupyter Notebooks](../jupyterlab/overview.md), data science e machine learning.

**Termini chiave:**

- **DSL:** Domain Specific Lingua.
- **Edge:** il servizio di punteggio di Machine Learning in tempo reale può essere eseguito su cluster Edge più vicini alle attivazioni e alle applicazioni.
- **Hub:** l&#39;alfa corrente esegue il servizio di punteggio di Machine Learning in tempo reale nell&#39;hub Adobe Experience Platform mentre la rete Edge è in fase di sviluppo.
- **Nodo:** Un nodo è l&#39;unità fondamentale di cui si formano i grafici. Ogni nodo esegue un&#39;attività specifica e possono essere concatenati utilizzando collegamenti per formare un grafico che rappresenta una pipeline ML. L&#39;attività eseguita da un nodo rappresenta un&#39;operazione sui dati di input, ad esempio una trasformazione di dati o schemi o un&#39;inferenza di Machine Learning. Il nodo emette il valore trasformato o dedotto ai nodi successivi.

## Set di dati in Adobe Experience Platform

Per iniziare a usare Apprendimento automatico in tempo reale, è necessario disporre accesso di un set di dati. È possibile utilizzare un dataset esterno e caricarlo nell&#39;ambiente [!DNL JupyterLab] oppure creare un nuovo dataset all&#39;interno di Platform se non lo si è già fatto.

>[!NOTE]
>
>Se si dispone già di un set di dati che si desidera utilizzare, è possibile saltare a [Successivo passaggi](#next-steps).

### Utilizzare un dataset esterno

Per ulteriori informazioni sull&#39;uso di un set di dati esterno, ad esempio il caricamento di dati nell&#39;ambiente [!DNL JupyterLab] , visita la esercitazione sull&#39;analisi [dei dati tramite i blocchi appunti](../jupyterlab/analyze-your-data.md#external-data).

### Crea un nuovo dataset

Per creare un nuovo set di dati da utilizzare in Real-time Machine Learning, è necessario uno schema di dati per il set di dati. Successivo, è necessario inserire i dati utilizzando lo schema creato. Utilizzare le esercitazioni seguenti per creare e popolare un dataset per [!DNL Platform]:

- [Crea e popolare un dataset nell&#39;API](../../catalog/datasets/create.md)
- [Crea e popolare un dataset nel interfaccia](../../ingestion/tutorials/ingest-batch-data.md)

## Passaggi successivi {#next-steps}

Dopo aver preparato i dati per Real-time Machine Learning, iniziare seguendo la guida](./rtml-authoring-notebook.md) all&#39;utente [del blocco appunti di Real-time Machine Learning per informazioni su come creare e caricare un modello ONNX nel modello di Machine Learning in tempo reale store.
