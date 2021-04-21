---
keywords: Experience Platform;home;argomenti popolari;dsw;DSW
solution: Experience Platform
title: Tutorial su Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per creare informazioni dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di fare previsioni utilizzando i contenuti e le risorse di dati nelle soluzioni Adobe.
exl-id: 7cfd71b1-584f-4588-bbcd-bc42a08a0bc0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# Esercitazioni del [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per creare informazioni dai tuoi dati. Integrato in Adobe Experience Platform, [!DNL Data Science Workspace] consente di fare previsioni utilizzando i contenuti e le risorse dati nelle soluzioni Adobe. Gli scienziati dei dati di tutti i livelli di abilità hanno strumenti sofisticati e facili da usare che supportano lo sviluppo rapido, la formazione e la messa a punto di ricette di apprendimento automatico - tutti i vantaggi della tecnologia AI, senza la complessità.

Per ulteriori informazioni, inizia leggendo la [panoramica di Data Science Workspace](../data-science-workspace/home.md).

## [!DNL Sensei Machine Learning] API

L’ API [!DNL Sensei Machine Learning] fornisce un meccanismo che consente agli scienziati dei dati di organizzare e gestire i servizi di apprendimento automatico, dall’onboarding degli algoritmi alla sperimentazione e alla distribuzione dei servizi.

**Sono disponibili le seguenti guide per gli sviluppatori API:**
- [Motori](../data-science-workspace/api/engines.md)  - Scopri come cercare il  [!DNL Docker] Registro di sistema, creare un motore, creare un motore di pipeline delle funzioni, recuperare le informazioni per un motore, aggiornare un motore ed eliminare un motore.
- [Istanze (ricette)](../data-science-workspace/api/mlinstances.md)  - Scopri come creare un’istanza MLI, recuperare le informazioni per un’istanza MLI, aggiornare un’istanza MLI ed eliminare un’istanza MLI.
- [Esperimenti](../data-science-workspace/api/experiments.md)  - Scopri come creare un esperimento, recuperare un esperimento o un esperimento esegue informazioni, aggiornare un esperimento ed eliminare un esperimento.
- [Modelli](../data-science-workspace/api/models.md)  - Scopri come registrare il tuo modello, recuperare le informazioni per un modello, aggiornare un modello, eliminare un modello, creare una nuova transcodifica per un modello e recuperare i dettagli di un modello transcodificato.
- [MLServices](../data-science-workspace/api/mlservices.md)  - Scopri come creare un servizio MLS, recuperare le informazioni per un servizio MLS, aggiornare un servizio MLService ed eliminare un servizio MLService.
- [Approfondimenti](../data-science-workspace/api/insights.md) : scopri come recuperare le informazioni per Insight, aggiungere un nuovo Model Insight e recuperare un elenco di metriche predefinite per gli algoritmi.

Per ulteriori informazioni e ottenere i valori richiesti per l&#39;esecuzione delle operazioni CRUD con l&#39;API di apprendimento automatico per i motori di tecnologia Sensei, visita la [guida introduttiva](../data-science-workspace/api/getting-started.md).

## Come utilizzare i [!DNL JupyterLab] Notebook

[!DNL JupyterLab] è un’interfaccia utente basata sul web per  [!DNL Project Jupyter] ed è strettamente integrata in Adobe Experience Platform. Fornisce un ambiente di sviluppo interattivo che consente agli scienziati dei dati di lavorare con [!DNL Jupyter Notebooks], codice e dati. Questo documento fornisce una panoramica di [!DNL JupyterLab] e delle relative funzioni, nonché istruzioni per eseguire le azioni comuni.

**Questa guida ti aiuterà a:**
- Accedi e comprendi l’interfaccia [!DNL JupyterLab] .
- Comprendere le celle del codice e i kernel disponibili in [!DNL JupyterLab].
- Comprendere la configurazione della GPU e del server di memoria in [!DNL Python]/R.

Per ulteriori informazioni, visita la [guida utente di JupyterLab](../data-science-workspace/jupyterlab/overview.md).

## Accesso ai dati nei notebook JupyterLab

Al momento JupyterLab in Data Science Workspace supporta i notebook per [!DNL Python], R, PySpark e Scala. Ogni kernel supportato fornisce funzionalità integrate che consentono di leggere i dati di Platform da un set di dati all’interno di un blocco appunti. Tuttavia, il supporto per i dati di impaginazione è limitato ai notebook [!DNL Python] e R. Questa guida si concentra su come utilizzare i notebook JupyterLab per accedere ai dati.

**Questa guida ti aiuterà a:**
- Leggere, scrivere ed eseguire query sui dati di Platform utilizzando i notebook Python, R, PySpark o Scala.
- Comprendere le limitazioni di lettura di ogni tipo di blocco appunti.

Per ulteriori informazioni, visita la [Guida per gli sviluppatori dell&#39;accesso ai dati del notebook JupyterLab](../data-science-workspace/jupyterlab/access-notebook-data.md)

## File di origine del pacchetto per la creazione di ricette [!DNL Docker]

Un&#39;immagine [!DNL Docker] consente di creare un pacchetto di un&#39;applicazione con tutte le parti necessarie. Questo include librerie e altre dipendenze in un unico pacchetto. L&#39;immagine [!DNL Docker] creata viene inviata a [!DNL Azure Container Registry] utilizzando le credenziali fornite durante il flusso di lavoro di creazione delle ricette.

**Questa esercitazione ti aiuterà a:**
- Scarica i prerequisiti richiesti per la creazione delle ricette.
- Comprendere la creazione di modelli basati su [!DNL Docker].
- Crea un&#39;immagine [!DNL Docker] per [!DNL Python], R, PySpark o Scala ([!DNL Spark]).
- Ottieni un URL del file di origine [!DNL Docker] .

Per ulteriori informazioni, segui i [file di origine del pacchetto in un&#39;esercitazione sulla ricetta](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Importare una ricetta

>[!NOTE]
>
>Questa esercitazione richiede l&#39;URL di un file di origine [!DNL Docker] . Visita i file di origine del pacchetto [in un tutorial sulla composizione](../data-science-workspace/models-recipes/package-source-files-recipe.md) se non hai un URL del file di origine [!DNL Docker].

Le esercitazioni sulle ricette di importazione forniscono informazioni su come configurare e importare una ricetta in pacchetto. Al termine di questa esercitazione, puoi creare, addestrare e valutare un modello in Adobe Experience Platform [!DNL Data Science Workspace].

**Questa esercitazione ti aiuterà a:**
- Crea un set di configurazioni per una ricetta.
- Importa una ricetta basata su [!DNL Docker] per [!DNL Python], R, PySpark o Scala ([!DNL Spark]).

Per ulteriori informazioni, segui l&#39;esercitazione sull&#39;importazione di una ricetta in pacchetto [Interfaccia utente](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) o il tutorial [API](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Treno e valutazione di un modello

In Adobe Experience Platform [!DNL Data Science Workspace], viene creato un modello di apprendimento automatico incorporando una composizione esistente appropriata per l&#39;intento del modello. Il modello viene quindi addestrato e valutato per ottimizzarne l&#39;efficienza operativa e l&#39;efficacia, regolando con precisione i relativi Hyperparameters associati. Le ricette sono riutilizzabili, il che significa che è possibile creare più modelli e personalizzarli per scopi specifici con un&#39;unica ricetta.

**Questa esercitazione ti aiuterà a:**
- Crea un nuovo modello.
- Crea un&#39;esecuzione di formazione per il modello.
- Valutare le esecuzioni del training Model.

Per iniziare, segui il corso di formazione e valuta un modello [tutorial API](../data-science-workspace/models-recipes/train-evaluate-model-api.md) o l&#39; [tutorial di interfaccia utente](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

## Ottimizzare un modello utilizzando il framework Model Insights

Il framework Model Insights fornisce allo scienziato strumenti in Adobe Experience Platform [!DNL Data Science Workspace] per effettuare scelte rapide e informate per modelli ottimali di apprendimento automatico basati su esperimenti. Il quadro migliorerà la velocità e l&#39;efficacia del flusso di lavoro di apprendimento automatico e migliorerà la facilità d&#39;uso per gli scienziati dei dati. Questo viene fatto fornendo un modello predefinito per ogni tipo di algoritmo di apprendimento automatico per assistere con la regolazione del modello. Il risultato finale consente agli scienziati dei dati e ai cittadini scienziati dei dati di prendere migliori decisioni di ottimizzazione dei modelli per i loro clienti finali.

**Questa esercitazione ti aiuterà a:**
- Configura il codice di ricetta.
- Definire metriche personalizzate.
- Utilizza metriche di valutazione e grafici di visualizzazione predefiniti.

Per iniziare, segui l&#39;esercitazione su [ottimizzazione di un modello](../data-science-workspace/models-recipes/optimize-model.md).

## Punteggio di un modello

Il punteggio in Adobe Experience Platform [!DNL Data Science Workspace] può essere ottenuto inserendo i dati di input in un modello addestrato esistente. I risultati del punteggio vengono quindi memorizzati e visualizzati in un set di dati di output specificato come nuovo batch.

**Questa esercitazione ti aiuterà a:**
- Crea una nuova esecuzione del punteggio.
- Visualizza i risultati del punteggio.

Per iniziare, segui il punteggio di un tutorial API [modello](../data-science-workspace/models-recipes/score-model-api.md) o il tutorial [UI](../data-science-workspace/models-recipes/score-model-ui.md).

## Pubblicare un modello come servizio

Adobe Experience Platform [!DNL Data Science Workspace] consente di pubblicare il modello come servizio, consentendo agli utenti all’interno dell’organizzazione IMS di valutare i dati senza la necessità di creare modelli personalizzati. Questa operazione può essere eseguita utilizzando l’ [!DNL Platform] interfaccia utente o l’ API [!DNL Sensei Machine Learning] .

**Questa esercitazione ti aiuterà a:**
- Pubblica un modello come servizio.
- Punteggio dei dati utilizzando un servizio tramite [!DNL Platform] [!UICONTROL Service Gallery].

Per iniziare, segui il tutorial di pubblicazione di un modello come servizio [API](../data-science-workspace/models-recipes/publish-model-service-api.md) o il tutorial [UI](../data-science-workspace/models-recipes/publish-model-service-ui.md).

## Pianificazione formazione e valutazione per un modello

Adobe Experience Platform [!DNL Data Science Workspace] consente di impostare le esecuzioni programmate di punteggio e formazione su un servizio di apprendimento automatico. L&#39;automazione del processo di formazione e valutazione può contribuire a mantenere e migliorare l&#39;efficienza del servizio nel tempo, tenendo il passo con i modelli all&#39;interno dei tuoi dati.

**Questa esercitazione ti aiuterà a:**
- Configurare il punteggio pianificato
- Configurare l’addestramento pianificato

Per iniziare, segui il [tutorial sull&#39;interfaccia utente di un modello](../data-science-workspace/models-recipes/schedule-models-ui.md).

## Creare una pipeline di feature

>[!NOTE]
>
>Attualmente, le pipeline di funzioni sono disponibili solo tramite API.

Adobe Experience Platform consente di creare e creare pipeline di funzioni personalizzate per eseguire la progettazione delle funzioni su scala tramite [!DNL Sensei Machine Learning Framework Runtime].

**Questa guida ti aiuterà a:**
- Implementa le classi di pipeline delle funzioni.
- Crea un motore di pipeline di funzionalità utilizzando l’API .

Per ulteriori informazioni, visita l’esercitazione per [creare una pipeline di funzionalità](../data-science-workspace/authoring/feature-pipeline.md).

## Creare un&#39;applicazione [!DNL Real-Time Machine Learning] (alfa)

Una combinazione di calcolo senza soluzione di continuità sia su Hub che su [!DNL Edge] riduce notevolmente la latenza tradizionalmente associata alla generazione di esperienze iper-personalizzate rilevanti e reattive. Pertanto, [!DNL Real-time Machine Learning] fornisce deduzioni con una latenza incredibilmente bassa per il processo decisionale sincrono. Alcuni esempi includono il rendering di contenuti di pagine web personalizzati, la visualizzazione di un’offerta e sconti per ridurre la fidelizzazione e aumentare le conversioni in un negozio web.

**Questa guida ti aiuterà a:**
- Comprendere l’architettura [!DNL Real-time Machine Learning].
- Comprendere il flusso di lavoro [!DNL Real-time Machine Learning].
- Comprendere la funzionalità corrente per [!DNL Real-time Machine Learning].
- Fornisci i passaggi successivi per creare il tuo [!DNL Real-time Machine Learning model].

Per ulteriori informazioni, visita la [Panoramica sull&#39;apprendimento automatico in tempo reale](../data-science-workspace/real-time-machine-learning/home.md).
