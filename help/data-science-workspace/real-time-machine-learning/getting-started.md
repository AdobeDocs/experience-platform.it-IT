---
keywords: Experience Platform;guida per sviluppatori;Data Science Workspace;argomenti comuni;apprendimento automatico in tempo reale;
solution: Experience Platform
title: Guida introduttiva all'apprendimento automatico in tempo reale
description: Il documento seguente illustra i passaggi necessari per creare un modello di apprendimento automatico in tempo reale in Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Guida introduttiva all’apprendimento automatico in tempo reale (Alpha)

>[!IMPORTANT]
>
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in alfa e viene ancora testata. Questo documento è soggetto a modifiche.

Per utilizzare l&#39;apprendimento automatico in tempo reale, è necessario avere accesso a un&#39;organizzazione con provisioning Adobe Experience Platform e [!DNL Data Science Workspace]. Inoltre, devi disporre di un set di dati completo per l’utilizzo in formazione e valutazione.

Le guide per l&#39;apprendimento automatico in tempo reale richiedono una comprensione funzionante di Python 3, [Jupyter Notebooks](../jupyterlab/overview.md), scienza dei dati e apprendimento automatico.

**Termini chiave:**

- **DSL:** Lingua specifica del dominio.
- **Bordo:** Il servizio di valutazione del machine learning in tempo reale può essere eseguito su cluster Edge più vicini alle tue attivazioni e applicazioni.
- **Hub:** L&#39;alfa corrente esegue il servizio di valutazione del machine learning in tempo reale su Adobe Experience Platform Hub mentre Experience Edge Network è in fase di sviluppo.
- **Nodo:** Un Nodo è l&#39;unità fondamentale di cui si formano i grafici. Ogni nodo esegue un&#39;attività specifica e può essere concatenato utilizzando i collegamenti per formare un grafico che rappresenta una pipeline ML. L&#39;attività eseguita da un nodo rappresenta un&#39;operazione sui dati di input, ad esempio una trasformazione di dati o schemi o un&#39;inferenza di apprendimento automatico. Il nodo restituisce il valore trasformato o dedotto ai nodi successivi.

## Set di dati in Adobe Experience Platform

Per iniziare a utilizzare l&#39;apprendimento automatico in tempo reale, è necessario avere accesso a un set di dati. Hai la possibilità di utilizzare un set di dati esterno e caricarlo nel tuo [!DNL JupyterLab] crea un nuovo set di dati all’interno di Platform , se non lo hai già fatto.

>[!NOTE]
>
>Se disponi già di un set di dati da utilizzare, puoi passare a [Passaggi successivi](#next-steps).

### Utilizzare un set di dati esterno

Per ulteriori informazioni sull’utilizzo di un set di dati esterno, ad esempio il caricamento di dati nel [!DNL JupyterLab] ambiente, visita il tutorial su [analisi dei dati con i notebook](../jupyterlab/analyze-your-data.md#external-data).

### Creare un nuovo set di dati

Per creare un nuovo set di dati da utilizzare in Real-time Machine Learning, è necessario uno schema di dati per il set di dati. Successivamente, devi acquisire i dati utilizzando lo schema creato. Utilizza le seguenti esercitazioni per creare e compilare un set di dati per [!DNL Platform]:

- [Creare e popolare un set di dati nell’API](../../catalog/datasets/create.md)
- [Creare e popolare un set di dati nell’interfaccia utente](../../ingestion/tutorials/ingest-batch-data.md)

## Passaggi successivi {#next-steps}

Una volta preparati i dati per l&#39;apprendimento automatico in tempo reale, inizia seguendo [Guida utente del notebook Real-time Machine Learning](./rtml-authoring-notebook.md) per scoprire come creare e caricare un modello ONNX nello store del modello Real-time Machine Learning.
