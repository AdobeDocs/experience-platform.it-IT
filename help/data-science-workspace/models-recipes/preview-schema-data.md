---
keywords: Experience Platform;preview schema data;Data Science Workspace;popular topics
solution: Experience Platform
title: Anteprima di schemi e set di dati
topic: Tutorial
translation-type: tm+mt
source-git-commit: 4b0f0dda97f044590f55eaf75a220f631f3313ee
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Anteprima di schemi e set di dati

Al completamento dello script di avvio da [Create the retail sales schema and dataset](./create-retails-sales-dataset.md) tutorial (Creare lo schema di vendita al dettaglio e l&#39;esercitazione sui dataset). Gli schemi di output e i set di dati possono essere visualizzati su [!DNL Experience Platform]. Per visualizzare gli schemi e i set di dati, procedere come segue:

1. Fate clic sul **[!UICONTROL Schemas]** collegamento situato nella colonna di navigazione a sinistra e individuate lo schema di input creato dallo script di avvio. Il nome dello schema corrisponderà a quello definito `config.yaml` dal passaggio precedente. Visualizzare i dettagli dello schema e la relativa composizione facendo clic su di esso.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Fate clic sul **[!UICONTROL Datasets]** collegamento situato nella colonna di navigazione a sinistra e aprite il set di dati di input creato facendo clic sul nome dell&#39;elenco. Il nome del set di dati corrisponderà a quanto definito `config.yaml` nel passaggio precedente.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Fare clic **[!UICONTROL Preview Dataset]** in alto a destra per visualizzare un sottoinsieme del set di dati.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Passaggi successivi

I dati di esempio Vendite al dettaglio sono stati inviati correttamente [!DNL Experience Platform] utilizzando lo script di avvio fornito.

Per continuare a utilizzare i dati acquisiti:
- [Analizzare i dati utilizzando i notebook Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilizza i notebook Jupyter [!DNL Data Science Workspace] per accedere, esplorare, visualizzare e comprendere i tuoi dati.
- [Creare pacchetti di file sorgente in una composizione](./package-source-files-recipe.md)
   - Segui questa esercitazione per scoprire come inserire un modello personalizzato [!DNL Data Science Workspace] creando pacchetti di file sorgente in un file Recipe importabile.