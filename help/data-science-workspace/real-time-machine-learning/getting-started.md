---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Guida introduttiva all'apprendimento automatico in tempo reale
topic: Getting started
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Guida introduttiva all&#39;apprendimento automatico in tempo reale (Alpha)

>[!IMPORTANT]
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in alfa e viene ancora testata. Questo documento è soggetto a modifiche.

Per utilizzare l&#39;apprendimento automatico in tempo reale, è necessario avere accesso a un&#39;organizzazione con  Adobe Experience Platform e [!DNL Data Science Workspace]. Inoltre, è necessario disporre di un set di dati completo da utilizzare per la formazione e il punteggio.

Le guide per l&#39;apprendimento automatico in tempo reale richiedono una conoscenza operativa di Python 3, [Jupyter notebook](../jupyterlab/overview.md), data science e machine learning.

**Termini chiave:**

- **DSL:** Lingua specifica del dominio.
- **Bordo:** Il servizio di valutazione del Machine Learning in tempo reale può essere eseguito su cluster Edge più vicini alle attivazioni e alle applicazioni.
- **Hub:** L&#39;alfa corrente esegue il servizio Real-time Machine Learning Scoring Service nell&#39;hub di Adobe Experience Platform  mentre Experience Edge Network è in fase di sviluppo.
- **Nodo:** Un nodo è l&#39;unità fondamentale di cui si formano i grafici. Ogni nodo esegue un&#39;attività specifica e può essere concatenato utilizzando i collegamenti per creare un grafico che rappresenta una pipeline ML. L&#39;attività eseguita da un nodo rappresenta un&#39;operazione sui dati di input, ad esempio una trasformazione di dati o schema, o un&#39;inferenza di apprendimento di una macchina. Il nodo genera il valore trasformato o dedotto nei nodi successivi.

## Set di dati in  Adobe Experience Platform

Per iniziare a utilizzare l&#39;apprendimento automatico in tempo reale, è necessario avere accesso a un dataset. È possibile utilizzare un set di dati esterno e caricarlo nell&#39; [!DNL JupyterLab] ambiente in uso o creare un nuovo set di dati in Platform, se non lo avete già fatto.

>[!NOTE]
>Se si dispone già di un set di dati da utilizzare, è possibile passare ai passaggi [](#next-steps)Successivi.

### Utilizzare un dataset esterno

Per ulteriori informazioni sull&#39;utilizzo di un set di dati esterno, ad esempio il caricamento di dati nell&#39; [!DNL JupyterLab] ambiente, visitare l&#39;esercitazione sull&#39; [analisi dei dati utilizzando i blocchi appunti](../jupyterlab/analyze-your-data.md#external-data).

### Creare un nuovo dataset

Per creare un nuovo dataset da utilizzare in Real-time Machine Learning, è necessario uno schema dati per il dataset. Successivamente, è necessario acquisire i dati utilizzando lo schema creato. Utilizzate le seguenti esercitazioni per creare e compilare un dataset per [!DNL Platform]:

- [Creazione e compilazione di un set di dati nell&#39;API](../../catalog/datasets/create.md)
- [Creazione e compilazione di un set di dati nell’interfaccia utente](../../ingestion/tutorials/ingest-batch-data.md)

## Passaggi successivi {#next-steps}

Dopo aver preparato i dati per l&#39;apprendimento automatico in tempo reale, iniziare seguendo la guida [utente del notebook](./rtml-authoring-notebook.md) Real-time Machine Learning per imparare a creare e caricare un modello ONNX nel negozio di modelli Real-time Machine Learning.

