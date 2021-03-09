---
keywords: Experience Platform;visualizzare in anteprima i dati dello schema;Data Science Workspace;argomenti comuni
solution: Experience Platform
title: Anteprima dello schema di vendita al dettaglio e del set di dati
topic: tutorial
type: Tutorial
description: Il documento seguente illustra l’anteprima di schemi e set di dati su Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 5129a75071af680bc54a7f60bb89ce32d3216d09
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 1%

---


# Anteprima dello schema e del set di dati di vendita al dettaglio

Una volta completato con successo lo script di avvio dal tutorial [schema di vendita al dettaglio e set di dati](./create-retails-sales-dataset.md). Gli schemi di output e i set di dati possono essere visualizzati su [!DNL Experience Platform]. Per visualizzare gli schemi e i set di dati, procedi come segue:

Seleziona la scheda **[!UICONTROL Schemas]** situata nella navigazione a sinistra e trova lo schema di input creato dallo script bootstrap. Il nome dello schema corrisponde a quello definito in `config.yaml` del passaggio precedente. Visualizza i dettagli dello schema e la sua composizione facendo clic su di esso.

![](../images/models-recipes/access-data/schema.PNG)

Seleziona la scheda **[!UICONTROL Datasets]** nella navigazione a sinistra e apri il set di dati di input creato selezionando il nome del set di dati. Il nome del set di dati corrisponde a ciò che è stato definito in `config.yaml` dal passaggio precedente.

![](../images/models-recipes/access-data/dataset.PNG)

Seleziona **[!UICONTROL Preview Dataset]** in alto a destra per visualizzare in anteprima un sottoinsieme di set di dati.

![](../images/models-recipes/access-data/preview.PNG)

## Passaggi successivi

È stato acquisito correttamente i dati di esempio Vendite al dettaglio in [!DNL Experience Platform] utilizzando lo script di avvio fornito.

Per continuare a utilizzare i dati acquisiti:
- [Analizzare i dati utilizzando Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Utilizza i notebook Jupyter in [!DNL Data Science Workspace] per accedere, esplorare, visualizzare e comprendere i tuoi dati.
- [Creare pacchetti di file di origine in una composizione](./package-source-files-recipe.md)
   - Segui questa esercitazione per scoprire come portare il tuo modello in [!DNL Data Science Workspace] creando pacchetti di file sorgente in un file Ricetta importabile.