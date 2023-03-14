---
keywords: Experience Platform;guida per sviluppatori;Data Science Workspace;argomenti popolari;apprendimento automatico in tempo reale;
solution: Experience Platform
title: Panoramica dell’apprendimento automatico in tempo reale
description: Il machine learning in tempo reale può migliorare notevolmente la rilevanza dei contenuti delle esperienze digitali per gli utenti finali. Ciò è possibile sfruttando le inferenze in tempo reale e l’apprendimento continuo in Experience Edge.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# Panoramica di apprendimento automatico in tempo reale (Alpha)

>[!IMPORTANT]
>
>Real-time Machine Learning non è ancora disponibile per tutti gli utenti. Questa funzione è in formato alfa ed è ancora in fase di test. Questo documento è soggetto a modifiche.

Il machine learning in tempo reale può migliorare notevolmente la rilevanza dei contenuti delle esperienze digitali per gli utenti finali. Ciò è possibile sfruttando l’inferenza in tempo reale e l’apprendimento continuo sul [!DNL Experience Edge].

Una combinazione di elaborazione perfetta sia sull&#39;hub che sul [!DNL Edge] riduce drasticamente la latenza tradizionalmente associata alle esperienze iper-personalizzate, rilevanti e reattive. Pertanto, il machine learning in tempo reale fornisce inferenze con latenza incredibilmente bassa per il processo decisionale sincrono. Alcuni esempi includono il rendering di contenuti personalizzati di pagine web o l’esposizione di un’offerta o di uno sconto per ridurre l’abbandono e aumentare le conversioni in un negozio web.

## Architettura di apprendimento automatico in tempo reale {#architecture}

I seguenti diagrammi forniscono una panoramica dell’architettura di machine learning in tempo reale. Attualmente, l&#39;alfa ha una versione più semplificata.

![arco alfa](../images/rtml/alpha-arch.png)

![Panoramica semplificata](../images/rtml/end-to-end-arch.png)

## Flusso di lavoro di apprendimento automatico in tempo reale

Il flusso di lavoro seguente illustra i passaggi e i risultati tipici necessari per la creazione e l’utilizzo di un modello di apprendimento automatico in tempo reale.

### Acquisizione dei dati e preparativi

I dati vengono acquisiti e trasformati con [!DNL Experience Data Model] (XDM) su Adobe Experience Platform. Questi dati vengono utilizzati per l’apprendimento dei modelli. Per ulteriori informazioni su XDM, visita [Panoramica di XDM](../../xdm/home.md).

### Authoring

Crea un modello di apprendimento automatico in tempo reale creandolo da zero o inserendolo come modello ONNX serializzato pre-addestrato nei notebook Adobe Experience Platform Jupyter.

### Implementazione

Distribuire il modello in [!DNL Experience Edge] per creare un servizio di apprendimento automatico in tempo reale in [!UICONTROL Raccolta servizi] utilizzando l’endpoint API di previsione.

### Inferenza

Utilizza l’endpoint API REST per la previsione per generare informazioni di apprendimento automatico in tempo reale.

### Distribuzione

Gli addetti al marketing possono quindi definire segmenti e regole che mappano i punteggi di Machine Learning in tempo reale alle esperienze utilizzando Adobe Target. Questo consente ai visitatori del sito web del tuo marchio di visualizzare in tempo reale un’esperienza iper-personalizzata della stessa pagina o di quella successiva.

## Funzionalità corrente

L’apprendimento automatico in tempo reale è attualmente in formato alfa. Le funzionalità descritte di seguito sono soggette a modifiche in quanto sono disponibili più funzioni e nodi.

>[!NOTE]
>
> Limitazioni alfa:
> - Attualmente, sono supportati solo i modelli basati su ONNX.
> - Impossibile serializzare le funzioni utilizzate nei nodi. Ad esempio, una funzione lambda utilizzata in un nodo Pandas.
> - Dopo 20 secondi si dorme [!DNL Edge] la distribuzione viene eseguita manualmente.
> - Per l’apprendimento profondo, i dati devono essere inviati in modo che, quando `df.values` viene chiamato restituisce un array accettabile dal modello DL. Questo perché il nodo di punteggio del modello ONNX utilizza `df.values` e invia l’output per valutare il modello.



### Funzioni:

|  | Alfa (maggio) |
| --- | --- |
| **Funzioni** | - Utilizzo del modello di notebook RTML, creazione, test e distribuzione di un modello di apprendimento automatico personalizzato. <br> - Supporto per l&#39;importazione di modelli di apprendimento automatico preformati. <br> - SDK per l’apprendimento automatico in tempo reale. <br> - Set iniziale di nodi di authoring. <br> : implementato nell’hub Adobe Experience Platform. |
| **Disponibilità** | America del Nord |
| **Authoring dei nodi** | - Panda <br> - ScikitLearn <br> - ONNXNode <br> - Divisione <br> - CaricamentoModello <br> - OneHotEncoder |
| **Tempi di esecuzione del punteggio** | ONNX |

## Passaggi successivi

Per iniziare, segui questi [introduzione](./getting-started.md) guida. Questa guida illustra come impostare tutti i prerequisiti necessari per la creazione di un modello di apprendimento automatico in tempo reale.
