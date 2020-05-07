---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Guida introduttiva all'apprendimento automatico in tempo reale
topic: Getting started
translation-type: tm+mt
source-git-commit: c9e6eb41e51ad17ad11b9a669ca5e4cf6c899f8b
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# Guida introduttiva all&#39;apprendimento automatico in tempo reale

>[!IMPORTANT]
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in alfa e viene ancora testata. Questo documento è soggetto a modifiche.

Per utilizzare l&#39;apprendimento automatico in tempo reale, è necessario avere accesso a un&#39;organizzazione con Adobe Experience Platform e Data Science Workspace. Inoltre, è necessario disporre di un set di dati in Piattaforma.

Le guide per l&#39;apprendimento automatico in tempo reale richiedono una comprensione operativa di Python 3, notebook [Jupyter](../jupyterlab/overview.md), scienza dei dati e apprendimento automatico.

## Set di dati in Adobe Experience Platform

Per iniziare a utilizzare l&#39;apprendimento automatico in tempo reale, è necessario disporre di un set di dati popolato all&#39;interno di Experience Platform. Potete utilizzare un dataset esterno e caricarlo nell’ambiente JupyterLab oppure creare un nuovo dataset all’interno della piattaforma, se non lo avete già fatto.

>[!NOTE]
>Se si dispone già di un set di dati da utilizzare, è possibile saltare i due passaggi seguenti.

### Utilizzare un dataset esterno

Per ulteriori informazioni sull’utilizzo di un set di dati esterno, ad esempio il caricamento di dati nell’ambiente JupyterLab, vedere l’esercitazione sull’ [analisi dei dati utilizzando i notebook](../jupyterlab/analyze-your-data.md#external-data).

### Creare un nuovo dataset

Per creare un nuovo dataset da utilizzare in Real-time Machine Learning, è necessario uno schema dati per il dataset. Successivamente, è necessario acquisire i dati utilizzando lo schema creato. Utilizzate le seguenti esercitazioni per creare e compilare un dataset per Piattaforma:

- [Creazione e compilazione di un set di dati nell&#39;API](../../catalog/datasets/create.md)
- [Creazione e compilazione di un set di dati nell’interfaccia utente](../../ingestion/tutorials/ingest-batch-data.md)

## Git e Docker

Se pianificate la formazione di un modello utilizzando il flusso di lavoro di ricetta Data Science Workplace, sono necessari Git e Docker.

>[!NOTE]
>Non è necessario scaricare Git e Docker se si pianifica la formazione di un modello utilizzando un notebook Python o se si utilizza il proprio modello ONNX.

- [Guida all&#39;installazione del Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Guida all&#39;installazione del docker](https://docs.docker.com/get-docker/)

## Passaggi successivi

Dopo aver preparato i dati per l&#39;apprendimento automatico in tempo reale, iniziare seguendo l&#39;esercitazione sulla [formazione di un modello](./training-ml-model.md) per apprendere come creare e caricare un modello ONNX nel negozio di modelli di apprendimento automatico in tempo reale.

