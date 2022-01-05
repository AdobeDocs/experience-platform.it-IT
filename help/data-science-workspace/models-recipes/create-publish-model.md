---
keywords: Experience Platform;modello di apprendimento automatico;Data Science Workspace;argomenti comuni;creare e pubblicare un modello
solution: Experience Platform
title: Creare e pubblicare un modello di apprendimento automatico
topic-legacy: tutorial
type: Tutorial
description: La guida seguente descrive i passaggi necessari per creare e pubblicare un modello di apprendimento automatico.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: ff8a3612f34d6547577564ba40261052cd78ef01
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 0%

---


# Creare e pubblicare un modello di apprendimento automatico

La guida seguente descrive i passaggi necessari per creare e pubblicare un modello di apprendimento automatico. Ogni sezione contiene una descrizione delle operazioni da eseguire e un collegamento alla documentazione dell’interfaccia utente e API per eseguire il passaggio descritto.

## Introduzione

Prima di avviare questa esercitazione, è necessario disporre dei seguenti prerequisiti:

- Accesso a [!DNL Adobe Experience Platform]. Se non hai accesso a un’organizzazione IMS in [!DNL Experience Platform]Prima di procedere, rivolgiti all’amministratore di sistema.

- Tutte le esercitazioni di Data Science Workspace utilizzano il modello di propensione Luma. Per procedere, devi aver creato il [Schemi e set di dati del modello di propensione Luma](./create-luma-data.md).

### Esplorare i dati e comprendere gli schemi

Accedi a [Adobe Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Set di dati]** per elencare tutti i set di dati esistenti e selezionare il set di dati da esplorare. In questo caso, seleziona la **Dati web Luma** set di dati.

![seleziona set di dati web Luma](../images/models-recipes/model-walkthrough/luma-dataset.png)

Viene visualizzata la pagina dell’attività del set di dati, in cui sono elencate le informazioni relative al set di dati. È possibile selezionare **[!UICONTROL Anteprima set di dati]** in alto a destra per esaminare i record campione. Puoi anche visualizzare lo schema per il set di dati selezionato.

![visualizzare in anteprima i dati web Luma](../images/models-recipes/model-walkthrough/preview-dataset.png)

Seleziona il collegamento dello schema nella barra a destra. Viene visualizzato un puntatore, selezionando il collegamento sotto **[!UICONTROL nome dello schema]** apre lo schema in una nuova scheda.

![visualizzare in anteprima lo schema dei dati web luma](../images/models-recipes/model-walkthrough/preview-schema.png)

È possibile esplorare ulteriormente i dati utilizzando il blocco appunti EDA (Exploratory Data Analysis) fornito. Questo notebook può essere utilizzato per comprendere i pattern nei dati Luma, controllare l’integrità dei dati e riepilogare i dati rilevanti per il modello di propensione predittiva. Per ulteriori informazioni sull’analisi dei dati esplorativi, visita la sezione [Documentazione AED](../jupyterlab/eda-notebook.md).

## Creare la ricetta di propensione Luma {#author-your-model}

Un componente principale del [!DNL Data Science Workspace] Il ciclo di vita prevede l&#39;authoring di recinti e modelli. Il modello di propensione Luma è progettato per generare una previsione sull’elevata propensione dei clienti all’acquisto di un prodotto da Luma.

Per creare il modello di propensione Luma, viene utilizzato il modello di generatore di ricette. Le ricette sono la base di un modello, in quanto contengono algoritmi di apprendimento automatico e logica progettati per risolvere problemi specifici. Ancora più importante, le entrate consentono di democratizzare l&#39;apprendimento automatico in tutta l&#39;organizzazione, consentendo ad altri utenti di accedere a un modello per diversi casi d&#39;uso senza scrivere alcun codice.

Segui [creare un modello utilizzando i notebook JupyterLab](../jupyterlab/create-a-model.md) esercitazione per creare la ricetta del modello di propensione Luma utilizzata nelle esercitazioni successive.

## Importa e prepara una ricetta da fonti esterne (*facoltativo*)

Se desideri importare e creare un pacchetto di una ricetta da utilizzare in Data Science Workspace, devi creare un pacchetto dei file sorgente in un file di archivio. Segui [creare pacchetti di file sorgente in una ricetta](./package-source-files-recipe.md) esercitazione. Questa esercitazione mostra come creare un pacchetto di file sorgente in una ricetta, che è il passaggio preliminare per importare una ricetta in Data Science Workspace. Al termine dell’esercitazione, riceverai un’immagine Docker in un Registro di sistema dei contenitori di Azure, insieme all’URL dell’immagine corrispondente, in altre parole un file di archivio.

Questo file di archivio può essere utilizzato per creare una ricetta in Data Science Workspace seguendo il flusso di lavoro di importazione della ricetta utilizzando [Flusso di lavoro dell’interfaccia](./import-packaged-recipe-ui.md) o [Flusso di lavoro API](./import-packaged-recipe-api.md).

## Treno e valutazione di un modello {#train-and-evaluate-your-model}

Ora che i tuoi dati sono preparati e una ricetta è pronta, hai la capacità di creare, addestrare e valutare ulteriormente il tuo modello di apprendimento automatico. Durante l&#39;utilizzo del Generatore di ricette, è necessario aver già formato, valutato e valutato il modello prima di confezionarlo in una ricetta.

L’interfaccia utente e l’API di Data Science Workspace consentono di pubblicare la ricetta come modello. Inoltre, è possibile perfezionare ulteriormente aspetti specifici del modello, ad esempio l’aggiunta, la rimozione e la modifica di parametri ipertestuali.

### Creare un modello

Per ulteriori informazioni sulla creazione di un modello utilizzando l’interfaccia utente, visita il treno e valuta un modello in Data Science Workspace [Esercitazione sull’interfaccia utente](./train-evaluate-model-ui.md) o [Esercitazione API](./train-evaluate-model-api.md). Questa esercitazione fornisce un esempio su come creare, addestrare e aggiornare i parametri ipertestuali per ottimizzare il modello.

>[!NOTE]
>
> Non è possibile apprendere gli iperparametri, pertanto è necessario assegnarli prima che si verifichino gli allenamenti. La regolazione degli iperparametri può modificare la precisione del modello addestrato. Poiché l&#39;ottimizzazione di un modello è un processo iterativo, possono essere necessarie più fasi di formazione prima di ottenere una valutazione soddisfacente.

## Punteggio di un modello {#score-a-model}

Il passaggio successivo nella creazione e nella pubblicazione di un modello consiste nell’operazionalizzare il modello al fine di valutare e utilizzare le informazioni provenienti dal data lake e dal Profilo cliente in tempo reale.

Il punteggio in Data Science Workspace può essere ottenuto inserendo i dati di input in un modello addestrato esistente. I risultati del punteggio vengono quindi memorizzati e visualizzati in un set di dati di output specificato come nuovo batch.

Per scoprire come valutare il modello, visita il punteggio di un modello [Esercitazione sull’interfaccia utente](./score-model-ui.md) o [Esercitazione API](./score-model-api.md).

## Pubblicare un modello con punteggio come servizio

Data Science Workspace consente di pubblicare il modello addestrato come servizio. Questo consente agli utenti all’interno dell’organizzazione IMS di valutare i dati senza la necessità di creare modelli personalizzati.

Per scoprire come pubblicare un modello come servizio, visita la pagina [Esercitazione sull’interfaccia utente](./publish-model-service-ui.md) o [Esercitazione API](./publish-model-service-api.md).

### Pianificazione della formazione automatizzata per un servizio

Dopo aver pubblicato un modello come servizio, puoi impostare le esecuzioni programmate di valutazione e formazione per il servizio di apprendimento automatico. L&#39;automazione del processo di formazione e valutazione può contribuire a mantenere e migliorare l&#39;efficienza del servizio nel tempo, tenendo il passo con i modelli all&#39;interno dei tuoi dati. Visita il [pianificare un modello nell’interfaccia utente di Data Science Workspace](./schedule-models-ui.md) esercitazione.

>[!NOTE]
>
> È possibile pianificare un modello per la formazione e il punteggio automatizzati solo dall’interfaccia utente.

## Passaggi successivi {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] fornisce gli strumenti e le risorse per creare, valutare e utilizzare modelli di apprendimento automatico per generare previsioni e insights sui dati. Quando le informazioni sull’apprendimento automatico vengono acquisite in un [!DNL Profile]set di dati abilitati, gli stessi dati vengono acquisiti anche come [!DNL Profile] record che possono quindi essere segmentati utilizzando [!DNL Adobe Experience Platform Segmentation Service].

Man mano che i dati di profilo e serie temporali vengono acquisiti, Profilo cliente in tempo reale decide automaticamente di includere o escludere tali dati dai segmenti attraverso un processo continuo denominato segmentazione in streaming, prima di unirli ai dati esistenti e di aggiornare la visualizzazione unione. Di conseguenza, puoi eseguire istantaneamente i calcoli e prendere decisioni per fornire ai clienti esperienze ottimizzate e personalizzate mentre interagiscono con il tuo marchio.

Visita il tutorial per [arricchimento del profilo cliente in tempo reale con informazioni sull’apprendimento automatico](./enrich-profile.md) per ulteriori informazioni su come utilizzare le informazioni sull&#39;apprendimento automatico.
