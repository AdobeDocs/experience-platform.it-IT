---
keywords: Experience Platform;guida per sviluppatori;Data Science Workspace;argomenti popolari;apprendimento automatico in tempo reale;
solution: Experience Platform
title: Guida introduttiva di Real-time Machine Learning
description: Il documento seguente illustra i passaggi necessari per creare un modello di apprendimento automatico in tempo reale in Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Guida introduttiva di Real-time Machine Learning (Alpha)

>[!IMPORTANT]
>
>Real-time Machine Learning non è ancora disponibile per tutti gli utenti. Questa funzione è in formato alfa ed è ancora in fase di test. Questo documento è soggetto a modifiche.

Per utilizzare il machine learning in tempo reale, è necessario avere accesso a un&#39;organizzazione con provisioning Adobe Experience Platform e [!DNL Data Science Workspace]. Inoltre, è necessario disporre di un set di dati completo da utilizzare nell’apprendimento e nel punteggio.

Le guide per il machine learning in tempo reale richiedono una buona conoscenza di Python 3, [Jupyter Notebooks](../jupyterlab/overview.md), data science e machine learning.

**Termini chiave:**

- **DSL:** Lingua specifica del dominio.
- **Edge:** è possibile eseguire il servizio di punteggio di Real-time Machine Learning in cluster Edge più vicini alle attivazioni e alle applicazioni.
- **Hub:** L&#39;alfa corrente esegue il servizio di punteggio di Machine Learning in tempo reale sull&#39;hub Adobe Experience Platform mentre l&#39;Edge Network è in fase di sviluppo.
- **Nodo:** Un nodo è l&#39;unità fondamentale di cui vengono formati i grafici. Ogni nodo esegue un’attività specifica e può essere collegato utilizzando dei collegamenti per formare un grafico che rappresenta una pipeline ML. L’attività eseguita da un nodo rappresenta un’operazione sui dati di input, ad esempio una trasformazione di dati o schemi, o un’inferenza di apprendimento automatico. Il nodo restituisce il valore trasformato o dedotto ai nodi successivi.

## Set di dati in Adobe Experience Platform

Per iniziare a utilizzare Real-time Machine Learning, devi avere accesso a un set di dati. Se non lo hai già fatto, puoi utilizzare un set di dati esterno e caricarlo nell&#39;ambiente [!DNL JupyterLab] oppure creare un nuovo set di dati in Platform.

>[!NOTE]
>
>Se disponi già di un set di dati da utilizzare, puoi passare ai [passaggi successivi](#next-steps).

### Utilizzare un set di dati esterno

Per ulteriori informazioni sull&#39;utilizzo di un set di dati esterno, ad esempio il caricamento di dati nell&#39;ambiente [!DNL JupyterLab], visitare il tutorial su [analisi dei dati tramite blocchi appunti](../jupyterlab/analyze-your-data.md#external-data).

### Creare un nuovo set di dati

Per creare un nuovo set di dati da utilizzare in Real-time Machine Learning, è necessario uno schema di dati per il set di dati. Successivamente, devi acquisire i dati utilizzando lo schema creato. Utilizzare le seguenti esercitazioni per creare e popolare un set di dati per [!DNL Platform]:

- [Creare e popolare un set di dati nell’API](../../catalog/datasets/create.md)
- [Creare e popolare un set di dati nell’interfaccia utente](../../ingestion/tutorials/ingest-batch-data.md)

## Passaggi successivi {#next-steps}

Dopo aver preparato i dati per Real-time Machine Learning, iniziare seguendo la [Guida utente del blocco appunti di Real-time Machine Learning](./rtml-authoring-notebook.md) per apprendere come creare e caricare un modello ONNX nell&#39;archivio modelli di Real-time Machine Learning.
