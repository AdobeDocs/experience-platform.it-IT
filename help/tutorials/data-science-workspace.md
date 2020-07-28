---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Esercitazioni su Data Science Workspace
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 0%

---


# [!DNL Data Science Workspace] esercitazioni

 Adobe Experience Platform [!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per creare approfondimenti dai dati. Integrato in  Adobe Experience Platform, [!DNL Data Science Workspace] consente di fare previsioni utilizzando i contenuti e le risorse di dati nelle soluzioni  Adobe. I Data Scienziati di tutti i livelli di abilità hanno sofisticati strumenti facili da usare che supportano lo sviluppo rapido, la formazione e l&#39;ottimizzazione delle ricette di machine learning - tutti i vantaggi della tecnologia AI, senza la complessità.

Per saperne di più, iniziare leggendo la panoramica [di](../data-science-workspace/home.md)Data Science Workspace.

## [!DNL Sensei Machine Learning] API

L&#39; [!DNL Sensei Machine Learning] API fornisce agli esperti di dati un meccanismo per organizzare e gestire i servizi di machine learning, dall&#39;installazione degli algoritmi alla sperimentazione e all&#39;implementazione dei servizi.

**Sono disponibili le seguenti guide per gli sviluppatori API:**
- [Motori](../data-science-workspace/api/engines.md) - Scopri come cercare il [!DNL Docker] Registro di sistema, creare un motore, creare un motore di pipeline delle funzionalità, recuperare le informazioni per un motore, aggiornare un motore ed eliminare un motore.
- [MLInances (ricette)](../data-science-workspace/api/mlinstances.md) - Informazioni su come creare un&#39;istanza MLI, recuperare le informazioni per un&#39;istanza MLI, aggiornare un&#39;istanza MLIned eliminare un&#39;istanza MLI.
- [Esperimenti](../data-science-workspace/api/experiments.md) - Scopri come creare un esperimento, recuperare un esperimento o un esperimento esegue informazioni, aggiornare un esperimento ed eliminare un esperimento.
- [Modelli](../data-science-workspace/api/models.md) - Informazioni su come registrare il proprio modello, recuperare le informazioni per un modello, aggiornare un modello, eliminare un modello, creare una nuova transcodifica per un modello e recuperare i dettagli di un modello transcodificato.
- [MLServices](../data-science-workspace/api/mlservices.md) - Informazioni su come creare un servizio MLS, recuperare le informazioni per un servizio MLService, aggiornare un servizio MLService ed eliminare un servizio MLService.
- [Approfondimenti](../data-science-workspace/api/insights.md) - Scopri come recuperare le informazioni per un Insight, aggiungere un nuovo Model Insight e recuperare un elenco di metriche predefinite per gli algoritmi.

Per saperne di più e ottenere i valori richiesti per eseguire le operazioni CRUD con l&#39;API di apprendimento di Sensei Machine, visita la guida [](../data-science-workspace/api/getting-started.md)introduttiva.

## How to use [!DNL JupyterLab] Notebooks

[!DNL JupyterLab] è un&#39;interfaccia utente basata sul Web per [!DNL Project Jupyter] ed è strettamente integrata nel Adobe Experience Platform . Fornisce un ambiente di sviluppo interattivo che consente agli esperti di dati di lavorare con [!DNL Jupyter notebooks], codice e dati. Questo documento fornisce una panoramica delle funzioni [!DNL JupyterLab] e delle istruzioni per eseguire azioni comuni.

**Questa guida è utile per:**
- Accesso e comprensione dell&#39; [!DNL JupyterLab] interfaccia.
- Comprendere le celle di codice e i kernel disponibili all&#39;interno [!DNL JupyterLab].
- Informazioni sulla configurazione di GPU e del server di memoria in [!DNL Python]/R.
- Leggere e interrogare [!DNL Platform] i dati utilizzando i blocchi appunti.
- Comprendere i limiti dei dati del blocco appunti.

Per saperne di più, visita la guida [utente di](../data-science-workspace/jupyterlab/overview.md)JupyterLab.

## Creare pacchetti di file sorgente per la creazione di [!DNL Docker] ricette

Un’ [!DNL Docker] immagine consente di creare un pacchetto con tutte le parti necessarie. Questo include librerie e altre dipendenze in un unico pacchetto. L&#39;immagine creata viene inviata [!DNL Docker] al [!DNL Azure Container Registry] visitatore utilizzando le credenziali fornite durante il flusso di lavoro per la creazione delle ricette.

**Questa esercitazione aiuterà:**
- Scaricate i prerequisiti richiesti per la creazione delle ricette.
- Comprendere l&#39;authoring basato [!DNL Docker] su modelli.
- Create un’ [!DNL Docker] immagine per [!DNL Python], R, PySpark o Scala ([!DNL Spark]).
- Ottenete un URL del file [!DNL Docker] sorgente.

Per saperne di più, seguite i file sorgente del [pacchetto in un&#39;esercitazione](../data-science-workspace/models-recipes/package-source-files-recipe.md)sulle ricette.

## Importare una ricetta

>[!NOTE]
>
>
>Questa esercitazione richiede l&#39;URL di un file [!DNL Docker] sorgente. Se non disponete di un URL del file [sorgente, visitate i file sorgente del](../data-science-workspace/models-recipes/package-source-files-recipe.md) pacchetto in un&#39;esercitazione [!DNL Docker] sulla ricetta.

Le esercitazioni sulle ricette di importazione forniscono informazioni approfondite su come configurare e importare una ricetta in un pacchetto. Al termine di questa esercitazione, è possibile creare, formare e valutare un modello in  Adobe Experience Platform [!DNL Data Science Workspace].

**Questa esercitazione aiuterà:**
- Create un set di configurazioni per una ricetta.
- Importare una ricetta [!DNL Docker] basata su [!DNL Python], R, PySpark o Scala ([!DNL Spark]).

Per saperne di più, seguite l&#39;esercitazione [per l&#39;importazione di un&#39;](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) interfaccia utente per ricette inclusa nel pacchetto o l&#39;esercitazione [sulle](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)API.

## Treno e valutazione di un modello

In  Adobe Experience Platform [!DNL Data Science Workspace], un modello di apprendimento automatico viene creato incorporando una Ricetta esistente adatta all&#39;intento del modello. Il modello viene quindi addestrato e valutato per ottimizzare l&#39;efficienza operativa e l&#39;efficacia, affinando i relativi Hyperparameters associati. Le ricette sono riutilizzabili, il che significa che più modelli possono essere creati e personalizzati a scopi specifici con un&#39;unica ricetta.

**Questa esercitazione aiuterà:**
- Creare un nuovo modello.
- Crea un&#39;esecuzione di formazione per il modello.
- Valutare le esecuzioni della formazione Modello.

Per iniziare, segui la formazione e valuta un&#39;esercitazione [sulle](../data-science-workspace/models-recipes/train-evaluate-model-api.md) API modello o l&#39;esercitazione [sull&#39;](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)interfaccia utente.

## Ottimizzare un modello utilizzando il framework Model Insights

Model Insights Framework fornisce allo scienziato dei dati strumenti in  Adobe Experience Platform [!DNL Data Science Workspace] per effettuare scelte rapide e informate per modelli ottimali di machine learning basati su esperimenti. Il quadro migliorerà la velocità e l&#39;efficacia del flusso di lavoro di apprendimento automatico e migliorerà la facilità d&#39;uso per gli esperti in materia di dati. A tal fine, viene fornito un modello predefinito per ciascun tipo di algoritmo di machine learning per facilitare l&#39;ottimizzazione del modello. Il risultato finale consente agli esperti di data mining e ai cittadini di prendere decisioni migliori in merito all&#39;ottimizzazione dei modelli per i clienti finali.

**Questa esercitazione aiuterà:**
- Configurare il codice di ricetta.
- Definire metriche personalizzate.
- Utilizza metriche di valutazione e grafici di visualizzazione predefiniti.

Per iniziare, seguite l&#39;esercitazione sull&#39; [ottimizzazione di un modello](../data-science-workspace/models-recipes/optimize-model.md).

## Punteggio di un modello

Il punteggio nel Adobe Experience Platform  [!DNL Data Science Workspace] può essere ottenuto inserendo i dati in un modello già preparato. I risultati del punteggio vengono quindi memorizzati e visualizzati in un set di dati di output specificato come nuovo batch.

**Questa esercitazione aiuterà:**
- Crea una nuova esecuzione del punteggio.
- Visualizza i risultati del punteggio.

Per iniziare, segui la valutazione di un&#39;esercitazione [sulle](../data-science-workspace/models-recipes/score-model-api.md) API modello o l&#39;esercitazione [sull&#39;](../data-science-workspace/models-recipes/score-model-ui.md)interfaccia utente.

## Pubblicare un modello come servizio

 Adobe Experience Platform [!DNL Data Science Workspace] consente di pubblicare il modello come servizio, consentendo agli utenti all&#39;interno dell&#39;organizzazione IMS di valutare i dati senza creare i propri modelli. Questo può essere fatto utilizzando l&#39;interfaccia [!DNL Platform] utente o l&#39; [!DNL Sensei Machine Learning] API.

**Questa esercitazione aiuterà:**
- Pubblicate un modello come servizio.
- Punteggio dei dati tramite un servizio tramite [!DNL Platform] il [!UICONTROL Service Gallery].

Per iniziare, segui l’esercitazione [di pubblicazione di un modello come servizio](../data-science-workspace/models-recipes/publish-model-service-api.md) API o l’esercitazione [](../data-science-workspace/models-recipes/publish-model-service-ui.md)sull’interfaccia utente.

## Pianificazione formazione e punteggio per un modello

 Adobe Experience Platform [!DNL Data Science Workspace] consente di impostare l’esecuzione programmata di punteggi e corsi di formazione su un servizio di machine learning. Automatizzare il processo di formazione e valutazione può contribuire a mantenere e migliorare l&#39;efficienza del servizio nel tempo, tenendo al passo con i pattern all&#39;interno dei dati.

**Questa esercitazione aiuterà:**
- Configurare il punteggio pianificato
- Configurare la formazione pianificata

Per iniziare, segui l’ [esercitazione](../data-science-workspace/models-recipes/schedule-models-ui.md)per l’interfaccia utente del modello.

## Creazione di una pipeline di feature

>[!NOTE]
>Attualmente, le pipeline delle funzioni sono disponibili solo tramite API.

 Adobe Experience Platform consente di creare e creare tubazioni di feature personalizzate per eseguire la progettazione di feature su scala attraverso [!DNL Sensei Machine Learning Framework Runtime].

**Questa guida è utile per:**
- Implementare le classi di pipeline delle funzioni.
- Create un motore di pipeline delle funzionalità utilizzando l&#39;API.

Per ulteriori informazioni, vedere l&#39;esercitazione per [creare una pipeline](../data-science-workspace/authoring/feature-pipeline.md)di feature.

## Creare un&#39; [!DNL Real-Time Machine Learning] applicazione (alfa)

Una combinazione di un calcolo senza soluzione di continuità sia sull&#39;Hub che [!DNL Edge] riduce drasticamente la latenza tradizionalmente impegnata nel fornire esperienze iper-personalizzate rilevanti e reattive. Di conseguenza, [!DNL Real-time Machine Learning] fornisce le inferenze con una latenza incredibilmente bassa per il processo decisionale sincrono. Alcuni esempi includono il rendering di contenuti personalizzati per le pagine Web, la visualizzazione di un&#39;offerta e gli sconti per ridurre il churn pur aumentando le conversioni in uno store Web.

**Questa guida è utile per:**
- Comprendere l&#39; [!DNL Real-time Machine Learning] architettura.
- Comprendere il [!DNL Real-time Machine Learning] flusso di lavoro.
- Comprendere la funzionalità corrente per [!DNL Real-time Machine Learning].
- Fornire i passaggi successivi per la creazione di nuovi modelli personalizzati [!DNL Real-time Machine Learning model].

Per ulteriori informazioni, consultare la panoramica [sull&#39;apprendimento automatico in tempo](../data-science-workspace/real-time-machine-learning/home.md)reale.