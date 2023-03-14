---
keywords: Experience Platform;anteprima dati schema;Data Science Workspace;argomenti più comuni
solution: Experience Platform
title: Anteprima dello schema e del set di dati di vendita al dettaglio
type: Tutorial
description: Il seguente documento illustra l’anteprima di schemi e set di dati su Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Anteprima dello schema e del set di dati di vendita al dettaglio

Dopo il completamento dello script di bootstrap da [schema e set di dati di vendita al dettaglio](./create-retails-sales-dataset.md) esercitazione. Gli schemi e i set di dati di output possono essere visualizzati su [!DNL Experience Platform]. Per visualizzare gli schemi e i set di dati, effettua le seguenti operazioni:

Seleziona la **[!UICONTROL Schemi]** nella barra di navigazione a sinistra e trova lo schema di input creato dallo script bootstrap. Il nome dello schema corrisponderà a quanto definito in `config.yaml` dal passaggio precedente. Per visualizzare i dettagli dello schema e la relativa composizione, fai clic su di essa.

![](../images/models-recipes/access-data/schema.PNG)

Seleziona la **[!UICONTROL Set di dati]** nella barra di navigazione a sinistra, apri il set di dati di input creato selezionando il nome del set di dati. Il nome del set di dati corrisponde a quanto definito in `config.yaml` dal passaggio precedente.

![](../images/models-recipes/access-data/dataset.PNG)

Seleziona **[!UICONTROL Anteprima set di dati]** in alto a destra per visualizzare in anteprima un sottoinsieme del set di dati.

![](../images/models-recipes/access-data/preview.PNG)

## Passaggi successivi

Ora hai acquisito correttamente i dati di esempio delle vendite al dettaglio in [!DNL Experience Platform] utilizzando lo script bootstrap fornito.

Per continuare a lavorare con i dati acquisiti:
- [Analizzare i dati utilizzando Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Utilizzare Jupyter Notebooks in [!DNL Data Science Workspace] per accedere, esplorare, visualizzare e comprendere i dati.
- [Creare pacchetti di file di origine in una ricetta](./package-source-files-recipe.md)
   - Segui questa esercitazione per scoprire come inserire un modello personalizzato in [!DNL Data Science Workspace] creando pacchetti di file di origine in un file di composizione importabile.
