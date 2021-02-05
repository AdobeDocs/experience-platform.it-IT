---
keywords: Experience Platform ;home;argomenti più comuni;dsw;DSW
solution: Experience Platform
title: Esercitazioni su Data Science Workspace
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace utilizza l'apprendimento automatico e l'intelligenza artificiale per creare approfondimenti dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di fare previsioni utilizzando i contenuti e le risorse dati nelle soluzioni  Adobe.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---


# Esercitazioni del [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per creare approfondimenti dai dati. Integrato in Adobe Experience Platform, [!DNL Data Science Workspace] consente di creare previsioni utilizzando i contenuti e le risorse dati nelle soluzioni  Adobe. I Data Scienziati di tutti i livelli di abilità hanno sofisticati strumenti facili da usare che supportano lo sviluppo rapido, la formazione e l&#39;ottimizzazione delle ricette di machine learning - tutti i vantaggi della tecnologia AI, senza la complessità.

Per saperne di più, iniziare leggendo la [panoramica di Data Science Workspace](../data-science-workspace/home.md).

## [!DNL Sensei Machine Learning] API

L&#39;API [!DNL Sensei Machine Learning] fornisce un meccanismo che consente agli esperti di dati di organizzare e gestire i servizi di machine learning, dalla configurazione degli algoritmi alla sperimentazione e alla distribuzione dei servizi.

**Sono disponibili le seguenti guide per gli sviluppatori API:**
- [Motori](../data-science-workspace/api/engines.md)  - Scopri come cercare il  [!DNL Docker] Registro di sistema, creare un motore, creare un motore di pipeline delle funzionalità, recuperare le informazioni per un motore, aggiornare un motore ed eliminare un motore.
- [MLInances (ricette)](../data-science-workspace/api/mlinstances.md)  - Informazioni su come creare un&#39;istanza MLI, recuperare le informazioni per un&#39;istanza MLI, aggiornare un&#39;istanza MLIned eliminare un&#39;istanza MLI.
- [Esperimenti](../data-science-workspace/api/experiments.md)  - Scopri come creare un Esperimento, recuperare un Esperimento o un Esperimento, eseguire informazioni, aggiornare un Esperimento ed eliminare un Esperimento.
- [Modelli](../data-science-workspace/api/models.md)  - Scopri come registrare il modello personale, recuperare le informazioni per un modello, aggiornare un modello, eliminare un modello, creare una nuova transcodifica per un modello e recuperare i dettagli di un modello transcodificato.
- [MLServices](../data-science-workspace/api/mlservices.md)  - Informazioni su come creare un servizio MLS, recuperare le informazioni per un servizio MLService, aggiornare un servizio MLService ed eliminare un servizio MLService.
- [Approfondimenti](../data-science-workspace/api/insights.md)  - Scopri come recuperare le informazioni per un Insight, aggiungere un nuovo Model Insight e recuperare un elenco di metriche predefinite per gli algoritmi.

Per saperne di più e ottenere i valori richiesti per eseguire le operazioni CRUD con l&#39;API di apprendimento di Sensei Machine, visitare la [guida introduttiva](../data-science-workspace/api/getting-started.md).

## Come utilizzare [!DNL JupyterLab] Notebook

[!DNL JupyterLab] è un&#39;interfaccia utente basata sul Web per  [!DNL Project Jupyter] ed è strettamente integrata in Adobe Experience Platform. Fornisce un ambiente di sviluppo interattivo che consente agli esperti di dati di lavorare con [!DNL Jupyter Notebooks], codice e dati. Questo documento fornisce una panoramica di [!DNL JupyterLab] e delle relative funzioni, nonché istruzioni per eseguire azioni comuni.

**Questa guida è utile per:**
- Accesso e comprensione dell&#39;interfaccia [!DNL JupyterLab].
- Comprendere le celle di codice e i kernel disponibili all&#39;interno di [!DNL JupyterLab].
- Informazioni sulla configurazione di GPU e del server di memoria in [!DNL Python]/R.

Per saperne di più, visitare la [Guida utente di JupyterLab](../data-science-workspace/jupyterlab/overview.md).

## Accesso ai dati nei notebook JupyterLab

Attualmente JupyterLab in Data Science Workspace supporta i notebook per [!DNL Python], R, PySpark e Scala. Ogni kernel supportato fornisce funzionalità integrate che consentono di leggere i dati della piattaforma da un dataset all&#39;interno di un blocco appunti. Tuttavia, il supporto per l&#39;impaginazione dei dati è limitato ai notebook [!DNL Python] e R. Questa guida è incentrata su come utilizzare i notebook JupyterLab per accedere ai dati.

**Questa guida è utile per:**
- Lettura, scrittura e query dei dati della piattaforma utilizzando i notebook Python, R, PySpark o Scala.
- Comprendere le limitazioni di lettura di ciascun tipo di notebook.

Per saperne di più, visitare la [Guida per lo sviluppo di accesso ai dati del notebook JupyterLab](../data-science-workspace/jupyterlab/access-notebook-data.md)

## Creare pacchetti di file sorgente per la creazione di [!DNL Docker] ricette

Un&#39;immagine [!DNL Docker] consente di creare un pacchetto con tutte le parti necessarie. Questo include librerie e altre dipendenze in un unico pacchetto. L&#39;immagine [!DNL Docker] creata viene inviata a [!DNL Azure Container Registry] utilizzando le credenziali fornite durante il flusso di lavoro per la creazione delle ricette.

**Questa esercitazione aiuterà:**
- Scaricate i prerequisiti richiesti per la creazione delle ricette.
- Conoscere l&#39;authoring di modelli basati su [!DNL Docker].
- Create un&#39;immagine [!DNL Docker] per [!DNL Python], R, PySpark o Scala ([!DNL Spark]).
- Ottenete un URL del file sorgente [!DNL Docker].

Per saperne di più, segui i [pacchetti di file sorgente in un&#39;esercitazione sulle ricette](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Importare una ricetta

>[!NOTE]
>
>Questa esercitazione richiede l&#39;URL di un file sorgente [!DNL Docker]. Visitate i [file di origine del pacchetto in un&#39;esercitazione sulla ricetta](../data-science-workspace/models-recipes/package-source-files-recipe.md) se non disponete di un URL del file di origine [!DNL Docker].

Le esercitazioni sulle ricette di importazione forniscono informazioni approfondite su come configurare e importare una ricetta in un pacchetto. Al termine di questa esercitazione, puoi creare, formare e valutare un modello in Adobe Experience Platform [!DNL Data Science Workspace].

**Questa esercitazione aiuterà:**
- Create un set di configurazioni per una ricetta.
- Importare una ricetta basata su [!DNL Docker] per [!DNL Python], R, PySpark o Scala ([!DNL Spark]).

Per saperne di più, segui l&#39;esercitazione sull&#39;importazione di una ricetta in pacchetti [UI](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) o l&#39;esercitazione API [API](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Treno e valutazione di un modello

In Adobe Experience Platform [!DNL Data Science Workspace], viene creato un modello di machine learning incorporando una Ricetta esistente adatta all&#39;intento del modello. Il modello viene quindi addestrato e valutato per ottimizzare l&#39;efficienza operativa e l&#39;efficacia, affinando i relativi Hyperparameters associati. Le ricette sono riutilizzabili, il che significa che più modelli possono essere creati e personalizzati a scopi specifici con un&#39;unica ricetta.

**Questa esercitazione aiuterà:**
- Creare un nuovo modello.
- Crea un&#39;esecuzione di formazione per il modello.
- Valutare le esecuzioni della formazione Modello.

Per iniziare, segui la formazione e valuta un [tutorial API](../data-science-workspace/models-recipes/train-evaluate-model-api.md) o l&#39; [esercitazione sull&#39;interfaccia utente](../data-science-workspace/models-recipes/train-evaluate-model-ui.md) modello.

## Ottimizzare un modello utilizzando il framework Model Insights

Model Insights Framework fornisce agli esperti di dati strumenti in Adobe Experience Platform [!DNL Data Science Workspace] per effettuare scelte rapide e informate per modelli di machine learning ottimali basati su esperimenti. Il quadro migliorerà la velocità e l&#39;efficacia del flusso di lavoro di apprendimento automatico e migliorerà la facilità d&#39;uso per gli esperti in materia di dati. A tal fine, viene fornito un modello predefinito per ciascun tipo di algoritmo di machine learning per facilitare l&#39;ottimizzazione del modello. Il risultato finale consente agli esperti di data mining e ai cittadini di prendere decisioni migliori in merito all&#39;ottimizzazione dei modelli per i clienti finali.

**Questa esercitazione aiuterà:**
- Configurare il codice di ricetta.
- Definire metriche personalizzate.
- Utilizza metriche di valutazione e grafici di visualizzazione predefiniti.

Per iniziare, segui l&#39;esercitazione su [ottimizzazione di un modello](../data-science-workspace/models-recipes/optimize-model.md).

## Punteggio di un modello

Il punteggio in Adobe Experience Platform [!DNL Data Science Workspace] può essere ottenuto inserendo i dati in un modello già addestrato. I risultati del punteggio vengono quindi memorizzati e visualizzati in un set di dati di output specificato come nuovo batch.

**Questa esercitazione aiuterà:**
- Crea una nuova esecuzione del punteggio.
- Visualizza i risultati del punteggio.

Per iniziare, segui la valutazione di un modello [Esercitazione API](../data-science-workspace/models-recipes/score-model-api.md) o l&#39;esercitazione [UI](../data-science-workspace/models-recipes/score-model-ui.md).

## Pubblicare un modello come servizio

Adobe Experience Platform [!DNL Data Science Workspace] consente di pubblicare il modello come servizio, consentendo agli utenti all&#39;interno dell&#39;organizzazione IMS di valutare i dati senza creare i propri modelli. Ciò può essere fatto utilizzando l&#39;interfaccia utente [!DNL Platform] o l&#39;API [!DNL Sensei Machine Learning].

**Questa esercitazione aiuterà:**
- Pubblicate un modello come servizio.
- Punteggio dei dati utilizzando un servizio tramite [!DNL Platform] [!UICONTROL Service Gallery].

Per iniziare, segui la pubblicazione di un modello come servizio [Esercitazione API](../data-science-workspace/models-recipes/publish-model-service-api.md) o come [esercitazione sull&#39;interfaccia utente](../data-science-workspace/models-recipes/publish-model-service-ui.md).

## Pianificazione formazione e punteggio per un modello

Adobe Experience Platform [!DNL Data Science Workspace] consente di impostare l&#39;esecuzione programmata di punteggi e corsi di formazione su un servizio di machine learning. Automatizzare il processo di formazione e valutazione può contribuire a mantenere e migliorare l&#39;efficienza del servizio nel tempo, tenendo al passo con i pattern all&#39;interno dei dati.

**Questa esercitazione aiuterà:**
- Configurare il punteggio pianificato
- Configurare la formazione pianificata

Per iniziare, segui l&#39; [programma un&#39;esercitazione sull&#39;interfaccia utente del modello](../data-science-workspace/models-recipes/schedule-models-ui.md).

## Creazione di una pipeline di feature

>[!NOTE]
>
>Attualmente, le pipeline delle funzioni sono disponibili solo tramite API.

Adobe Experience Platform consente di creare e creare tubazioni di feature personalizzate per eseguire la progettazione di feature in scala tramite [!DNL Sensei Machine Learning Framework Runtime].

**Questa guida è utile per:**
- Implementare le classi di pipeline delle funzioni.
- Create un motore di pipeline delle funzionalità utilizzando l&#39;API.

Per ulteriori informazioni, visitare l&#39;esercitazione per [creare una pipeline delle funzioni](../data-science-workspace/authoring/feature-pipeline.md).

## Creare un&#39;applicazione [!DNL Real-Time Machine Learning] (alpha)

Una combinazione di calcolo semplice sia sull&#39;Hub che su [!DNL Edge] riduce drasticamente la latenza tradizionalmente impegnata nel fornire esperienze iper-personalizzate rilevanti e reattive. Di conseguenza, [!DNL Real-time Machine Learning] offre inferenze con una latenza incredibilmente bassa per il processo decisionale sincrono. Alcuni esempi includono il rendering di contenuti personalizzati per le pagine Web, la visualizzazione di un&#39;offerta e gli sconti per ridurre il churn pur aumentando le conversioni in uno store Web.

**Questa guida è utile per:**
- Conoscere l&#39;architettura [!DNL Real-time Machine Learning].
- Comprendere il flusso di lavoro [!DNL Real-time Machine Learning].
- Comprendere la funzionalità corrente per [!DNL Real-time Machine Learning].
- Fornire i passaggi successivi per la creazione di [!DNL Real-time Machine Learning model] personalizzati.

Per ulteriori informazioni, visitare la [Panoramica sull&#39;apprendimento automatico in tempo reale](../data-science-workspace/real-time-machine-learning/home.md).