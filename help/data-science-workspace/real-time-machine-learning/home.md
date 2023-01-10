---
keywords: Experience Platform;guida per sviluppatori;Data Science Workspace;argomenti comuni;apprendimento automatico in tempo reale;
solution: Experience Platform
title: Panoramica sull’apprendimento automatico in tempo reale
description: L'apprendimento automatico in tempo reale può migliorare notevolmente la pertinenza dei contenuti dell'esperienza digitale per gli utenti finali. Questo è possibile sfruttando l’inferenza in tempo reale e l’apprendimento continuo su Experience Edge.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# Panoramica sull’apprendimento automatico in tempo reale (Alpha)

>[!IMPORTANT]
>
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in alfa e viene ancora testata. Questo documento è soggetto a modifiche.

L&#39;apprendimento automatico in tempo reale può migliorare notevolmente la pertinenza dei contenuti dell&#39;esperienza digitale per gli utenti finali. Ciò è possibile sfruttando l&#39;inferenza in tempo reale e l&#39;apprendimento continuo sul [!DNL Experience Edge].

Una combinazione di calcolo senza soluzione di continuità sia su Hub che su [!DNL Edge] riduce drasticamente la latenza tradizionalmente associata alla creazione di esperienze iper-personalizzate rilevanti e reattive. Di conseguenza, l&#39;apprendimento automatico in tempo reale fornisce deduzioni con una latenza incredibilmente bassa per il processo decisionale sincrono. Ad esempio, è possibile eseguire il rendering di contenuti di pagina web personalizzati o visualizzare un’offerta o uno sconto per ridurre la fidelizzazione e aumentare le conversioni in un negozio web.

## Architettura di apprendimento automatico in tempo reale {#architecture}

I seguenti diagrammi forniscono una panoramica dell&#39;architettura di apprendimento automatico in tempo reale. Attualmente, l&#39;alfa ha una versione più semplificata.

![arco alfa](../images/rtml/alpha-arch.png)

![Panoramica semplificata](../images/rtml/end-to-end-arch.png)

## Flusso di lavoro di apprendimento automatico in tempo reale

Il flusso di lavoro seguente illustra i passaggi e i risultati tipici necessari per creare e utilizzare un modello di apprendimento automatico in tempo reale.

### Acquisizione e preparazione dei dati

I dati vengono acquisiti e trasformati con [!DNL Experience Data Model] (XDM) su Adobe Experience Platform. Questi dati vengono utilizzati per l’addestramento dei modelli. Per ulteriori informazioni su XDM, visita il [Panoramica di XDM](../../xdm/home.md).

### Authoring

Crea un modello di apprendimento automatico in tempo reale creando un nuovo modello da zero o inserendolo come modello ONNX serializzato pre-addestrato in Adobe Experience Platform Jupyter Notebooks.

### Implementazione

Distribuisci il modello in [!DNL Experience Edge] per creare un servizio di apprendimento automatico in tempo reale nel [!UICONTROL Raccolta servizi] utilizzando l’endpoint API di previsione.

### Inferenza

Utilizza l’endpoint API REST di previsione per generare informazioni sull’apprendimento automatico in tempo reale.

### Distribuzione

Gli addetti al marketing possono quindi definire segmenti e regole che mappano i punteggi di apprendimento automatico in tempo reale sulle esperienze utilizzando Adobe Target. Questo consente ai visitatori del sito web del tuo marchio di visualizzare in tempo reale un’esperienza iper-personalizzata della stessa pagina o della pagina successiva.

## Funzionalità corrente

L&#39;apprendimento automatico in tempo reale è attualmente in alfa. La funzionalità descritta di seguito è soggetta a modifiche man mano che vengono rese disponibili ulteriori funzioni e nodi.

>[!NOTE]
>
> Limiti alfa:
> - Attualmente, sono supportati solo i modelli basati su ONNX.
> - Le funzioni utilizzate nei nodi non possono essere serializzate. Ad esempio, una funzione lambda utilizzata in un nodo Pandas.
> - Ci sono 20 secondi di sonno dopo [!DNL Edge] la distribuzione viene eseguita manualmente.
> - Per l&#39;apprendimento profondo, i dati devono essere inviati in modo tale che quando `df.values` viene chiamato restituisce un array accettabile dal modello DL. Questo perché il nodo di punteggio del modello ONNX utilizza `df.values` e invia l&#39;output al punteggio rispetto al modello.



### Funzioni:

|  | Alfa (maggio) |
| --- | --- |
| **Funzioni** | - Utilizzo del modello di blocco appunti RTML, creazione, test e distribuzione di un modello di apprendimento automatico personalizzato. <br> - Supporto per l&#39;importazione di modelli di apprendimento automatico preformati. <br> - SDK per l’apprendimento automatico in tempo reale. <br> - Set iniziale di nodi di authoring. <br> - Distribuito su Adobe Experience Platform Hub. |
| **Disponibilità** | America del Nord |
| **Nodi di authoring** | - Panda <br> - ScikitLearning <br> - ONNXNode <br> - Divisione <br> - ModelUpload <br> - OneHotEncoder |
| **Tempi di esecuzione dei punteggi** | ONNX |

## Passaggi successivi

Puoi iniziare seguendo le [guida introduttiva](./getting-started.md) guida. Questa guida descrive come impostare tutti i prerequisiti necessari per la creazione di un modello di apprendimento automatico in tempo reale.
