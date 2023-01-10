---
keywords: Experience Platform;dati web luma;Data Science Workspace;argomenti popolari;ricette;dati demo;dati web demo;dati luma
solution: Experience Platform
title: Creare schemi web e set di dati Luma
type: Tutorial
description: Questa esercitazione fornisce i prerequisiti e le risorse necessari per il modello di propensione demo Luma.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# Creare schemi e set di dati del modello di propensione Luma

Questa esercitazione fornisce i prerequisiti e le risorse necessari per tutti gli altri [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] esercitazioni. Una volta completati, i seguenti schemi e set di dati saranno disponibili per te e la tua organizzazione IMS.

**Schemi:**

- Schema dati web Luma
- Schema dei risultati del punteggio del modello di tendenza

**Set di dati:**

- Set di dati web Luma
- Set di dati di formazione per il modello di tendenza
- Set di dati di punteggio del modello di tendenza
- Set di dati dei risultati del punteggio del modello di tendenza

## Scaricare le risorse {#assets}

L’esercitazione seguente utilizza un modello di propensione di acquisto Luma personalizzato. Prima di procedere, [scarica le risorse richieste](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) cartella zip. Questa cartella contiene:

- Blocco appunti del modello di propensione all&#39;acquisto
- Un blocco appunti utilizzato per inserire i dati in un set di dati di formazione e valutazione (un sottoinsieme dei dati web Luma)
- Un file JSON demo contenente i dati web di 730.000 utenti Luma
- Un notebook opzionale Python 3 EDA (analisi dei dati esplorativi) che può essere utilizzato per aiutare a comprendere i dati web e il modello.

>[!NOTE]
>
> Puoi utilizzare il tuo schema e i tuoi dati per qualsiasi esercitazione. Tuttavia, il modello demo fornito nelle risorse non funziona a meno che non sia stato fornito il file di configurazione e il file dei requisiti corretti. Questo modello di propensione demo è stato progettato per funzionare con i dati web Luma.

### Creare lo schema di dati web Luma e acquisire i dati

Per creare un modello, è necessario disporre di un set di dati in Platform che viene utilizzato per addestrare e valutare il modello. Il seguente video tutorial tratto da [Corso su Data Science Workspace](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw) illustra come creare lo schema Luma e acquisire i dati utilizzati dal modello di propensione di acquisto.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### Creazione di set di dati di formazione, valutazione e valutazione dei risultati

Per eseguire il blocco appunti del generatore di ricette o utilizzare l&#39;API per addestrare e valutare un modello, è necessario specificare i set di dati e gli schemi utilizzati per la formazione/il punteggio. L’esercitazione video seguente illustra come impostare i set di dati dei risultati di formazione, valutazione e valutazione, nonché lo schema dei risultati di valutazione utilizzato nel modello di propensione di acquisto Luma.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente gli schemi e i set di dati richiesti per il modello di propensione Luma. Ora puoi continuare l’esercitazione successiva e creare il modello utilizzando la [blocco appunti del generatore di ricette](../jupyterlab/create-a-model.md) esercitazione.

Inoltre, è possibile esplorare i dati utilizzando il blocco appunti EDA (Exploratory Data Analysis) fornito. Questo blocco appunti può essere utilizzato per comprendere i pattern nei dati Luma, controllare l’integrità dei dati e riepilogare i dati rilevanti per il modello di propensione predittiva. Per ulteriori informazioni sull’analisi dei dati esplorativi, visita la sezione [Documentazione AED](../jupyterlab/eda-notebook.md).
