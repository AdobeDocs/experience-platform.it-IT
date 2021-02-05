---
keywords: ' Experience Platform;guida allo sviluppo;Data Science Workspace;argomenti più comuni;Real time machine learning;'
solution: Experience Platform
title: Panoramica sull'apprendimento automatico in tempo reale
topic: Overview
description: L'apprendimento automatico in tempo reale può migliorare notevolmente la pertinenza dei contenuti dell'esperienza digitale per gli utenti finali. Questo è possibile sfruttando la deduzione in tempo reale e l'apprendimento continuo su Experience Edge.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 1%

---


# Panoramica sull&#39;apprendimento automatico in tempo reale (Alpha)

>[!IMPORTANT]
>
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in alfa e viene ancora testata. Questo documento è soggetto a modifiche.

L&#39;apprendimento automatico in tempo reale può migliorare notevolmente la pertinenza dei contenuti dell&#39;esperienza digitale per gli utenti finali. Questo è possibile sfruttando la deduzione in tempo reale e l&#39;apprendimento continuo su [!DNL Experience Edge].

Una combinazione di calcolo semplice sia sull&#39;Hub che su [!DNL Edge] riduce drasticamente la latenza tradizionalmente impegnata nel fornire esperienze iper-personalizzate rilevanti e reattive. Di conseguenza, l&#39;apprendimento automatico in tempo reale offre inferenze con una latenza incredibilmente bassa per il processo decisionale sincrono. Alcuni esempi includono il rendering di contenuti personalizzati per le pagine Web o la visualizzazione di un&#39;offerta o uno sconto per ridurre il churn e aumentare le conversioni in un negozio Web.

## Architettura di apprendimento automatico in tempo reale {#architecture}

I diagrammi seguenti forniscono una panoramica dell&#39;architettura Real-time Machine Learning. Al momento, l&#39;alfa dispone di una versione più semplificata.

![arco alfa](../images/rtml/alpha-arch.png)

![Panoramica semplificata](../images/rtml/end-to-end-arch.png)

## Flusso di lavoro di apprendimento automatico in tempo reale

Il flusso di lavoro seguente illustra i passaggi e i risultati tipici relativi alla creazione e all&#39;utilizzo di un modello di apprendimento automatico in tempo reale.

### Iniezione e preparati di dati

I dati vengono assimilati e trasformati con [!DNL Experience Data Model] (XDM) in Adobe Experience Platform. Questi dati vengono utilizzati per la formazione dei modelli. Per ulteriori informazioni su XDM, visitare la [panoramica XDM](../../xdm/home.md).

### Authoring

Create un modello Real-time Machine Learning creando un nuovo modello da zero o inserendolo come modello ONNX serializzato prepreparato in Adobe Experience Platform Jupyter Notebooks.

### Implementazione

Distribuire il modello su [!DNL Experience Edge] per creare un servizio di machine Learning in tempo reale in [!UICONTROL Service Gallery] utilizzando l&#39;endpoint API Predizione.

### Inferenza

Utilizzate l&#39;endpoint API REST di previsione per generare informazioni sull&#39;apprendimento automatico in tempo reale.

### Consegna

Gli addetti al marketing possono quindi definire segmenti e regole che mappano i punteggi di apprendimento automatico in tempo reale alle esperienze utilizzando  Adobe Target. Questo consente ai visitatori del sito Web del tuo marchio di visualizzare in tempo reale un&#39;esperienza iper-personalizzata della stessa pagina o successiva.

## Funzionalità corrente

L&#39;apprendimento automatico in tempo reale è attualmente in alfa. La funzionalità descritta di seguito è soggetta a modifiche man mano che vengono rese disponibili ulteriori funzionalità e nodi.

>[!NOTE]
>
> Limiti alfa:
> - Attualmente, sono supportati solo i modelli basati su ONNX.
> - Le funzioni utilizzate nei nodi non possono essere serializzate. Ad esempio, una funzione lambda utilizzata in un nodo Pandas.
> - Dopo che la distribuzione di [!DNL Edge] è stata eseguita manualmente, è possibile che siano trascorsi 20 secondi di sospensione.
> - Per l&#39;apprendimento profondo, i dati devono essere inviati in modo tale che quando si chiama `df.values` restituisca un array accettabile dal modello DL. Questo perché il nodo di punteggio del modello ONNX utilizza `df.values` e invia l&#39;output al punteggio rispetto al modello.



### Funzioni:

|  | Alfa (maggio) |
| --- | --- |
| **Funzioni** | - Utilizzo del modello di blocco appunti RTML, creazione, test e implementazione di un modello di machine learning personalizzato. <br> - Supporto per l&#39;importazione di modelli di machine learning preformati. <br> - Real-time Machine Learning SDK. <br> - Set iniziale di nodi di authoring. <br> - Distribuito su Adobe Experience Platform Hub. |
| **Disponibilità** | America del Nord |
| **Creazione di nodi** | - Panda <br> - ScikitLearn <br> - ONNXNode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **Tempi di esecuzione dei punteggi** | ONNX |

## Passaggi successivi

Per iniziare, seguire la guida [guida introduttiva](./getting-started.md). Questa guida illustra come impostare tutti i prerequisiti necessari per creare un modello di apprendimento automatico in tempo reale.

