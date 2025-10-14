---
keywords: Experience Platform;dati web luma;Data Science Workspace;argomenti popolari;ricette;dati demo;dati web demo;dati luma;;luma web data;luma data;luma data;
solution: Experience Platform
title: Creare schemi web e set di dati Luma
type: Tutorial
description: Questa esercitazione ti fornisce i prerequisiti e le risorse necessari per il modello di propensione demo Luma.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Creare schemi e set di dati del modello di propensione Luma

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto.
>
>Questa documentazione è destinata ai clienti esistenti che dispongono di diritti precedenti su Data Science Workspace.

Questo tutorial ti fornisce i prerequisiti e le risorse necessari per tutte le altre esercitazioni di [!DNL Adobe Experience Platform] [!DNL Data Science Workspace]. Una volta completati, i seguenti schemi e set di dati saranno disponibili per te e la tua organizzazione.

**Schemi:**

- Schema dati web Luma
- Schema dei risultati del punteggio del modello tendenza

**Set di dati:**

- Set di dati web Luma
- Set di dati di apprendimento del modello tendenza
- Set di dati di punteggio del modello tendenza
- Set di dati dei risultati del punteggio del modello tendenza

## Scaricare le risorse {#assets}

L’esercitazione seguente utilizza un modello di propensione all’acquisto Luma personalizzato. Prima di procedere, [scarica la cartella zip delle risorse richieste](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip). Questa cartella contiene:

- Il notebook del modello di propensione all&#39;acquisto
- Notebook utilizzato per acquisire dati in un set di dati di formazione e punteggio (un sottoinsieme di dati web Luma)
- Un file JSON demo contenente i dati web di 730.000 utenti Luma
- Un notebook opzionale Python 3 EDA (analisi esplorativa dei dati) che può essere utilizzato per aiutare a comprendere i dati e il modello web.

>[!NOTE]
>
> Puoi utilizzare schemi e dati personalizzati per qualsiasi esercitazione. Tuttavia, il modello demo fornito nelle risorse non funziona se non viene fornito il file di configurazione e i file dei requisiti corretti. Questo modello di propensione demo è stato progettato per funzionare con i dati web Luma.

### Creare lo schema di dati web Luma e acquisire i dati

Per creare un modello, è necessario disporre di un set di dati in Experience Platform utilizzato per addestrare e valutare il modello. Il seguente tutorial video del corso [Data Science Workspace](https://experienceleague.adobe.com/?lang=it&recommended=ExperiencePlatform-U-1-2021.1.dsw&lang=it) illustra come creare lo schema Luma e acquisire i dati utilizzati dal modello di propensione all’acquisto.

>[!VIDEO](https://video.tv.adobe.com/v/3447162?captions=ita)

### Creare i set di dati dei risultati di apprendimento, punteggio e punteggio

Per eseguire il notebook per la generazione di formule o utilizzare l’API per addestrare e valutare un modello, è necessario specificare i set di dati e gli schemi utilizzati per l’apprendimento e il punteggio. Il seguente tutorial video illustra come impostare i set di dati dei risultati di apprendimento, punteggio e punteggio, nonché lo schema dei risultati di punteggio utilizzato nel modello di propensione all’acquisto Luma.

>[!VIDEO](https://video.tv.adobe.com/v/3447429?captions=ita)

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente gli schemi e i set di dati richiesti per il modello di propensione Luma. Ora puoi passare all&#39;esercitazione successiva e creare il modello utilizzando l&#39;esercitazione [blocco appunti per la generazione di formule](../jupyterlab/create-a-model.md).

Inoltre, puoi esplorare i dati utilizzando il blocco appunti EDA (Exploratory Data Analysis) fornito. Questo blocco appunti può essere utilizzato per comprendere i pattern nei dati Luma, verificare la correttezza dei dati e riepilogare i dati rilevanti per il modello di propensione predittiva. Per ulteriori informazioni sull&#39;analisi esplorativa dei dati, consulta la [documentazione EDA](../jupyterlab/eda-notebook.md).
