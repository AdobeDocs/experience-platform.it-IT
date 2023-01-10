---
keywords: Experience Platform;visualizzare in anteprima i dati dello schema;Data Science Workspace;argomenti comuni
solution: Experience Platform
title: Anteprima dello schema di vendita al dettaglio e del set di dati
type: Tutorial
description: Il documento seguente illustra l’anteprima di schemi e set di dati su Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Anteprima dello schema e del set di dati di vendita al dettaglio

Al completamento dello script di avvio dal [schema e set di dati di vendita al dettaglio](./create-retails-sales-dataset.md) esercitazione. Gli schemi di output e i set di dati possono essere visualizzati su [!DNL Experience Platform]. Per visualizzare gli schemi e i set di dati, procedi come segue:

Seleziona la **[!UICONTROL Schemi]** nella barra di navigazione a sinistra e trova lo schema di input creato dallo script bootstrap. Il nome dello schema corrisponde a quello definito in `config.yaml` dal passaggio precedente. Visualizza i dettagli dello schema e la sua composizione facendo clic su di esso.

![](../images/models-recipes/access-data/schema.PNG)

Seleziona la **[!UICONTROL Set di dati]** nella barra di navigazione a sinistra e apri il set di dati di input creato selezionando il nome del set di dati. Il nome del set di dati corrisponde a ciò che è stato definito in `config.yaml` dal passaggio precedente.

![](../images/models-recipes/access-data/dataset.PNG)

Seleziona **[!UICONTROL Anteprima set di dati]** in alto a destra per visualizzare in anteprima un sottoinsieme di set di dati.

![](../images/models-recipes/access-data/preview.PNG)

## Passaggi successivi

Ora i dati di esempio per le vendite al dettaglio sono stati correttamente acquisiti in [!DNL Experience Platform] utilizzando lo script bootstrap fornito.

Per continuare a utilizzare i dati acquisiti:
- [Analizzare i dati utilizzando Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Usa i notebook Jupyter in [!DNL Data Science Workspace] per accedere, esplorare, visualizzare e comprendere i tuoi dati.
- [Creare pacchetti di file di origine in una composizione](./package-source-files-recipe.md)
   - Segui questa esercitazione per scoprire come inserire il tuo modello in [!DNL Data Science Workspace] impacchettando i file di origine in un file di composizione importabile.
