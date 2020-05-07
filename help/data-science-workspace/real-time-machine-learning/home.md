---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Panoramica sull'apprendimento automatico in tempo reale
topic: Overview
translation-type: tm+mt
source-git-commit: ab8b000bec0ae30c695582f57c40105b7ca1f22f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 2%

---


# Panoramica sull&#39;apprendimento automatico in tempo reale

>[!IMPORTANT]
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in alfa e viene ancora testata. Questo documento è soggetto a modifiche.

Il framework di apprendimento automatico in tempo reale di Adobe Experience Platform consente di utilizzare l&#39;apprendimento automatico per fornire agli utenti finali giusti le esperienze al momento giusto nei canali giusti con un intervallo di tempo inferiore ai secondi.

## Vantaggi

L&#39;apprendimento automatico in tempo reale può migliorare notevolmente la pertinenza dei contenuti dell&#39;esperienza digitale per gli utenti finali. Questo è possibile sfruttando la deduzione in tempo reale e l&#39;apprendimento continuo su Experience Edge.

La combinazione di un calcolo semplice sia su Hub che su Edge riduce drasticamente la latenza tradizionalmente associata all&#39;alimentazione di esperienze iper-personalizzate rilevanti e reattive. Di conseguenza, l&#39;apprendimento automatico in tempo reale offre inferenze con una latenza incredibilmente bassa per il processo decisionale sincrono. Alcuni esempi includono il rendering di contenuti personalizzati per le pagine Web o la visualizzazione di un&#39;offerta o uno sconto per ridurre il churn e aumentare le conversioni in un negozio Web.

## Architettura di apprendimento automatico in tempo reale

Il diagramma seguente fornisce una panoramica dell&#39;architettura Real-time Machine Learning.

![Panoramica semplificata](../images/rtml/simple-overview.png)

## Flusso di lavoro di apprendimento automatico in tempo reale (Alpha)

Il flusso di lavoro seguente illustra i passaggi e i risultati tipici relativi alla creazione e all&#39;utilizzo di un modello di apprendimento automatico in tempo reale.

### Iniezione e preparati di dati

I dati vengono assimilati e trasformati con Experience Data Model (XDM) in Adobe Experience Platform. Questi dati vengono utilizzati per la formazione dei modelli. Per ulteriori informazioni su XDM, visitare la panoramica [](../../xdm/home.md)XDM.

### Authoring  

Create un modello di apprendimento automatico in tempo reale creando un nuovo modulo partendo da zero o inserendolo come modello ONNX serializzato prepreparato nei notebook Jupyter della piattaforma Adobe Experience Platform.

### Implementazione

Distribuite il modello in Experience Edge per creare un servizio di machine Learning in tempo reale nella Galleria dei servizi utilizzando l&#39;endpoint API di previsione.

### Inferenza

Utilizzate l&#39;endpoint API REST di previsione per generare informazioni sull&#39;apprendimento automatico in tempo reale.

### Consegna

Gli addetti al marketing possono quindi definire segmenti e regole che mappano i punteggi di Machine Learning in tempo reale sulle esperienze utilizzando Adobe Target. Questo consente ai visitatori del sito Web del tuo marchio di visualizzare in tempo reale la stessa o l&#39;esperienza iper-personalizzata della pagina successiva (inferiore a 100 ms).

## Piano di sviluppo

L&#39;apprendimento automatico in tempo reale è attualmente in fase Alpha. La tabella seguente illustra alcune delle funzioni e degli aggiornamenti che dovrebbero essere rilasciati nell&#39;iterazione beta futura.

<table>
    <th></th>
    <th>Alfa (maggio)</th>
    <th>Beta</th>
    <tr>
        <td>
            <strong>Funzioni</strong>
        </td>
        <td>
            <li>Data Science Workspace porta il tuo modello e l'autore mediante l'integrazione di Notebook Launch.</li>
            <li>Set iniziale di operatori di authoring.</li>
            <li>Distribuisci nell'hub</li>
            <li>Scikit Impara modelli basati su.</li>
        </td>
        <td>
            <li>Integrazione dell’interfaccia utente Galleria servizi di Data Science Workspace.</li>
            <li>Arricchisci automaticamente il profilo cliente in tempo reale con risultati di inferenza.</li>
            <li>Modelli di apprendimento profondo.</li>
            <li>Set esteso di operatori di authoring, inclusi operatori personalizzati.</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Disponibilità</strong>
        </td>
        <td>
            America del Nord
        </td>
        <td>
            <li>America del Nord</li>
            <li>Europa e Medio Oriente (EMEA)</li>
            <li>Asia Pacifico (APAC)</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Authoring  </strong>
        </td>
        <td>
            <li>Supporto Python</li>
            <li>Real-time Machine Learning SDK</li>
            <li>Nodi di creazione Python: Panda, ScikitLearn, ONNXNode, Split, ModelUpload, OneHotEncoder.</li>
        </td>
        <td>
            <li>Supporto del flusso di tensioni.</li>
            <li>Nodi di creazione Python aggiuntivi: Lettore profilo cliente in tempo reale, Modulo di scrittura profilo cliente in tempo reale, array numerici, XDM2Frame, Frame2XDM. </li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Tempi di esecuzione dei punteggi</strong>
        </td>
        <td>
            ONNX
        </td>
        <td>
            ONNX
        </td>
    </tr>
</table>

## Passaggi successivi

Per iniziare, segui la guida [introduttiva](./getting-started.md) . Questa guida illustra come impostare tutti i prerequisiti necessari per creare un modello di apprendimento automatico in tempo reale.

