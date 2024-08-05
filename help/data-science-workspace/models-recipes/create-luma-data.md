---
keywords: Experience Platform; dati web luma; Data Science Area di lavoro; argomenti popolari; Ricette; dati dimostrativi; dati web dimostrativi; Dati Luma
solution: Experience Platform
title: Crea gli schemi web e i set di dati Luma
type: Tutorial
description: In questo esercitazione vengono forniti i prerequisiti e le risorse necessari per il modello di propensione alla demo Luma.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Crea gli schemi e i dataset del modello di propensione Luma

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

In questo esercitazione vengono forniti i prerequisiti e le risorse necessari per tutte le altre [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] esercitazioni. Una volta completati, gli schemi e i set di dati seguenti saranno disponibili per l&#39;utente e l&#39;organizzazione.

**Schemi:**

- Schema dati web Luma
- Schema dei risultati del punteggio del modello di propensione

**Dataset:**

- Set di dati Web Luma
- Modello di propensione training dataset
- Dataset di dati con punteggio del modello di propensione
- Set di dati dei risultati del punteggio del modello di propensione

## Scarica l&#39;risorse {#assets}

La esercitazione seguente utilizza un modello personalizzato di propensione all&#39;acquisto Luma. Prima di procedere, [scaricare la cartella zip risorse](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip) richiesta. Questa cartella contiene:

- Il taccuino modello di propensione all&#39;acquisto
- Un blocco appunti utilizzato per inserire dati in un set di dati di training e punteggio (un sottoinsieme dei dati Web Luma)
- Un file JSON demo contenente i dati web di 730.000 utenti Luma
- Un notebook opzionale Python 3 EDA (analisi esplorativa dei dati) che può essere utilizzato per aiutare a comprendere i dati e il modello web.

>[!NOTE]
>
> È possibile utilizzare il proprio schema e i propri dati per qualsiasi esercitazione. Tuttavia, il modello demo fornito nel risorse non funziona a meno che non vengano forniti i file di configurazione e il file dei requisiti appropriati. Questo modello di propensione alla demo è stato progettato per funzionare con i dati web Luma.

### Crea lo schema dati web Luma e inserisci i dati

Per creare un modello, è necessario disporre di un set di dati in Platform utilizzato per eseguire il training e assegnare un punteggio al modello. Il seguente esercitazione video del [corso](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw&amp;lang=it) di Area di lavoro Data Science illustra come creare lo schema Luma e inserire i dati usati dal modello di propensione all&#39;acquisto.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### Crea i set di dati di training, punteggio e punteggio dei risultati

Per eseguire il blocco appunti di creazione di ricette o utilizzare l&#39;API per eseguire il training e assegnare un punteggio a un modello, è necessario specificare i set di dati e gli schemi utilizzati per il training/punteggio. Nella esercitazione video seguente viene illustrata la configurazione dei set di dati di training, assegnazione di punteggi e punteggi dei risultati, nonché dello schema dei risultati dei punteggi utilizzato nel modello di propensione all&#39;acquisto Luma.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente gli schemi e i set di dati necessari per il modello di propensione Luma. Ora sei pronto per passare alla esercitazione successiva e creare il modello utilizzando il esercitazione per notebook](../jupyterlab/create-a-model.md) per la creazione di [ricette.

È inoltre possibile esplorare i dati utilizzando il notebook EDA (Exploratory Data Analysis) fornito. Questo notebook può essere utilizzato per comprendere i modelli nei dati Luma, controllare la sanità dei dati e riepilogare i dati rilevanti per il modello di propensione predittiva. Per saperne di più sull&#39;analisi esplorativa dei dati, visita la [documentazione EDA](../jupyterlab/eda-notebook.md).
