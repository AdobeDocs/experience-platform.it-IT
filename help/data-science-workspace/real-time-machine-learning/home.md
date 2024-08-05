---
keywords: Experience Platform; guida per sviluppatori; Data Science Area di lavoro; argomenti popolari; Machine learning in tempo reale;
solution: Experience Platform
title: Panoramica di Machine Learning in tempo reale
description: Il machine learning in tempo reale può migliorare notevolmente la pertinenza dell'esperienza digitale contenuto per gli utenti finali. Ciò è reso possibile sfruttando l'inferenza in tempo reale e l'apprendimento continuo sulla rete Edge Experience Platform.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---

# Panoramica di Machine Learning in tempo reale (Alpha)

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

>[!IMPORTANT]
>
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in versione alpha ed è ancora in fase di test. Questo documento è soggetto a modifiche.

Il machine learning in tempo reale può migliorare notevolmente la pertinenza dell&#39;esperienza digitale contenuto per gli utenti finali. Ciò è reso possibile sfruttando l&#39;inferenza in tempo reale e l&#39;apprendimento [!DNL Experience Platform Edge Network]continuo su .

Una combinazione di elaborazione senza soluzione di continuità sia sull&#39;Hub che sull&#39;Hub riduce drasticamente la latenza tradizionalmente coinvolta nell&#39;alimentazione [!DNL Edge] di esperienze iper-personalizzate che siano sia rilevanti che dinamico. Pertanto, l&#39;apprendimento automatico in tempo reale fornisce inferenze con latenza incredibilmente bassa per il processo decisionale sincrono. Gli esempi includono il rendering di una pagina Web personalizzata contenuto o l&#39;emergere di un&#39;offerta o di uno sconto per ridurre il tasso di abbandono e aumentare le conversioni su un web store.

## Architettura di Machine Learning in tempo reale {#architecture}

I seguenti diagrammi forniscono una panoramica dell’architettura di machine learning in tempo reale. Attualmente, alpha ha una versione più semplificata.

![arco alfa](../images/rtml/alpha-arch.png)

![Panoramica semplificata](../images/rtml/end-to-end-arch.png)

## workflow di Machine Learning in tempo reale

La workflow seguente delinea i passaggi e i risultati tipici coinvolti nella creazione e nell&#39;utilizzo di un modello di Machine Learning in tempo reale.

### Assimilazione e preparazione dei dati

I dati vengono assimilati e trasformati con ( [!DNL Experience Data Model] XDM) su Adobe Experience Platform. Questi dati vengono utilizzati per training del modello. Per ulteriori informazioni su XDM, visita la [panoramica](../../xdm/home.md) di XDM.

### Authoring

Crea un modello di Machine Learning in tempo reale creandolo da zero o inserendolo come modello ONNX serializzato pre-addestrato in Adobe Experience Platform notebook Jupyter.

### Spiegamento

Distribuisci il tuo modello nel [!DNL Edge Network] per creare un servizio di Machine Learning in tempo reale nella [!UICONTROL raccolta] di servizi usando l&#39;endpoint API di stima.

### Inferenza

Usa l&#39;endpoint REST API di stima per generare informazioni dettagliate sul machine learning in tempo reale.

### Consegna

Gli addetti al marketing possono quindi definire segmenti e regole che mappano i punteggi di Machine Learning in tempo reale alle esperienze con Adobe Target. Ciò consente ai visitatori del sito web del tuo marchio di vedere un&#39;esperienza iper-personalizzata della stessa pagina o della pagina successiva in tempo reale.

## Funzionalità corrente

L&#39;apprendimento automatico in tempo reale è attualmente in alpha. Le funzionalità descritte di seguito sono soggette a modifiche man mano che vengono rese disponibili ulteriori funzionalità e nodi.

>[!NOTE]
>
> Limitazioni di Alpha:
> - Attualmente sono supportati solo i modelli basati su ONNX.
> - Impossibile serializzare le funzioni utilizzate nei nodi. Ad esempio, una funzione lambda utilizzata in un nodo Pandas.
> - La sospensione è di 20 secondi dopo l&#39;esecuzione manuale della distribuzione di [!DNL Edge].
> - Per l&#39;apprendimento profondo, i dati devono essere inviati in modo tale che quando si chiama `df.values` venga restituito un array accettabile per il modello DL. Questo perché il nodo di punteggio del modello ONNX utilizza `df.values` e invia l&#39;output per assegnare un punteggio rispetto al modello.


### Tratti somatici:

| | Alfa (maggio) |
| --- | --- |
| **Funzioni** | - Utilizzo del modello di notebook RTML, creazione, test e distribuire un modello di apprendimento automatico personalizzato. <br> - Supporto per l&#39;importazione di modelli di apprendimento automatico pre-addestrati. <br> - SDK di apprendimento automatico in tempo reale. <br> - Set iniziale di nodi di authoring. <br> - Implementato in Adobe Experience Platform Hub. |
| **Disponibilità** | America del Nord |
| **Creazione dei nodi** | - Panda <br> - ScikitLearn <br> - ONNXNode <br> - Spalato <br> - ModelUpload <br> - OneHotEncoder |
| **Tempi di esecuzione del punteggio** | ONNX |

## Passaggi successivi

Per iniziare, segui la [guida introduttiva](./getting-started.md). Questa guida illustra come configurare tutti i prerequisiti necessari per la creazione di un modello di Machine Learning in tempo reale.
