---
keywords: Experience Platform ;anteprima dati schema;Data Science Workspace;argomenti più comuni
solution: Experience Platform
title: Anteprima dello schema di vendita al dettaglio e del set di dati
topic: tutorial
type: Tutorial
description: Nel seguente documento sono illustrati gli schemi di anteprima e i set di dati in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Anteprima dello schema di vendita al dettaglio e del dataset

Al completamento corretto dello script di avvio dall&#39;esercitazione [Crea lo schema di vendita al dettaglio e il dataset](./create-retails-sales-dataset.md). Gli schemi di output e i set di dati possono essere visualizzati su [!DNL Experience Platform]. Per visualizzare gli schemi e i set di dati, procedere come segue:

1. Fate clic sul collegamento **[!UICONTROL Schemas]** situato nella colonna di navigazione a sinistra e individuate lo schema di input creato dallo script di avvio. Il nome dello schema corrisponderà a quello definito in `config.yaml` dal passaggio precedente. Visualizzare i dettagli dello schema e la relativa composizione facendo clic su di esso.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Fate clic sul collegamento **[!UICONTROL Datasets]** situato nella colonna di navigazione a sinistra e aprite il set di dati di input creato facendo clic sul nome dell&#39;elenco. Il nome del set di dati corrisponderà a quanto definito in `config.yaml` dal passaggio precedente.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Fare clic su **[!UICONTROL Preview Dataset]** in alto a destra per visualizzare in anteprima un sottoinsieme del set di dati.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Passaggi successivi

I dati di esempio Vendite al dettaglio sono stati inviati correttamente in [!DNL Experience Platform] utilizzando lo script di avvio fornito.

Per continuare a utilizzare i dati acquisiti:
- [Analizzare i dati utilizzando i blocchi appunti Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilizzare i notebook Jupyter in [!DNL Data Science Workspace] per accedere, esplorare, visualizzare e comprendere i dati.
- [Creare pacchetti di file sorgente in una casella](./package-source-files-recipe.md)
   - Segui questa esercitazione per apprendere come portare il tuo modello in [!DNL Data Science Workspace] creando pacchetti di file sorgente in un file Recipe importabile.