---
keywords: Experience Platform;anteprima dati schema;Data Science Workspace;argomenti popolari
solution: Experience Platform
title: Anteprima dello schema e del set di dati di vendita al dettaglio
type: Tutorial
description: Il seguente documento illustra l’anteprima di schemi e set di dati su Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 3%

---

# Anteprima dello schema e del set di dati di vendita al dettaglio

Al completamento dello script di avvio dall&#39;esercitazione [Retail Sales Schema and dataset](./create-retails-sales-dataset.md). Gli schemi e i set di dati di output possono essere visualizzati su [!DNL Experience Platform]. Per visualizzare gli schemi e i set di dati, effettua le seguenti operazioni:

Selezionare la scheda **[!UICONTROL Schemi]** nella barra di navigazione a sinistra e individuare lo schema di input creato dallo script di bootstrap. Il nome dello schema corrisponderà a quanto definito in `config.yaml` dal passaggio precedente. Per visualizzare i dettagli dello schema e la relativa composizione, fai clic su di essa.

![](../images/models-recipes/access-data/schema.PNG)

Selezionare la scheda **[!UICONTROL Set di dati]** nella barra di navigazione a sinistra e aprire il set di dati di input creato selezionando il nome del set di dati. Il nome del set di dati corrisponde a quanto definito in `config.yaml` dal passaggio precedente.

![](../images/models-recipes/access-data/dataset.PNG)

Seleziona **[!UICONTROL Anteprima set di dati]** in alto a destra per visualizzare in anteprima un sottoinsieme del set di dati.

![](../images/models-recipes/access-data/preview.PNG)

## Passaggi successivi

Sono stati acquisiti correttamente i dati di esempio di Retail Sales in [!DNL Experience Platform] utilizzando lo script di bootstrap fornito.

Per continuare a lavorare con i dati acquisiti:
- [Analizza i tuoi dati utilizzando Jupyter Notebook](../jupyterlab/analyze-your-data.md)
   - Utilizza Jupyter Notebooks in [!DNL Data Science Workspace] per accedere, esplorare, visualizzare e comprendere i tuoi dati.
- [Creare pacchetti di file di origine in una ricetta](./package-source-files-recipe.md)
   - Segui questa esercitazione per scoprire come inserire il tuo modello in [!DNL Data Science Workspace] creando un pacchetto dei file di origine in un file di ricetta importabile.
