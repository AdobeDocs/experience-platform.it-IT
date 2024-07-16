---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
solution: Experience Platform
title: Panoramica di Self-Service Sources (SDK batch)
description: Sorgenti self-service di Adobe Experience Platform (SDK batch) è un set di API di configurazione che ti consente di integrare un’origine basata su API REST utilizzando l’API del servizio Flusso per portare i tuoi dati all’Experience Platform.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 3%

---

# Panoramica di Self-Serve Sources (SDK Batch)

Sorgenti self-service di Adobe Experience Platform (SDK batch) è un framework che consente di integrare un&#39;origine basata su API REST nel catalogo delle origini Experience Platform utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Self-Service Sources (Batch SDK) fornisce un set di API di configurazione per generare la propria origine e portare all’Experience Platform i dati batch.

Con Origini self-service (SDK batch), puoi:

* Configurare e integrare una nuova origine nel catalogo Experience Platform utilizzando l&#39;API [!DNL Flow Service].
* Definisci le specifiche per l’origine, incluse le informazioni relative ai tipi di autenticazione supportati e al modo in cui vengono recuperati i dati delle risorse.
* Crea una documentazione rivolta all’utente per la nuova sorgente.

La documentazione sulle origini self-service fornisce istruzioni per configurare, testare e rilasciare un’integrazione sorgente basata su API REST con Experience Platform e far sì che la tua origine diventi parte del catalogo delle origini in continua crescita.

![catalogo](./assets/catalog.png)

## Informazioni sulle origini

Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Experience Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Per ulteriori informazioni sulle origini e per visualizzare un elenco delle diverse origini attualmente supportate in Experience Platform, vedere la [panoramica delle origini](../home.md).

## Creare un’origine

Tramite le origini self-service, puoi integrare la tua origine basata su API REST e portare i tuoi dati a Experience Platform con [!DNL Flow Service]. È possibile integrare un&#39;origine nel catalogo delle origini Experienci Platform creando, configurando e inviando nuove specifiche di connessione tramite l&#39;API [!DNL Flow Service].

Per informazioni su come integrare una nuova origine in Experience Platform, consultare la guida alla [creazione di una nuova specifica di connessione](./api/api-overview.md).

## Documenta la sorgente

Una volta creata l&#39;origine, consultare la [guida alla documentazione](./documentation/doc-overview.md) per istruzioni su come documentarla tramite l&#39;interfaccia Web [!DNL GitHub] o il proprio editor di testo.

## Processo di alto livello

Di seguito è descritta la procedura dettagliata per configurare l’origine in Experience Platform:

* Leggere la guida dell&#39;API [Self-Serve Sources (Batch SDK)](./api/api-overview.md).
   * Leggi la [guida introduttiva](./api/getting-started.md).
   * Segui l&#39;esercitazione su [creazione di una nuova specifica di connessione](./api/create.md).
   * Segui il tutorial su [aggiornamento della specifica di connessione](./api/update-connection-specs.md).
   * Segui l&#39;esercitazione su [aggiunta del nuovo ID della specifica di connessione a una specifica di flusso](./api/update-flow-specs.md)
   * [Invia la nuova origine](./api/submit.md).
* Per comprendere meglio la struttura e le proprietà di una specifica di connessione, leggere la guida sulle [opzioni di configurazione per Self-Serve Sources (Batch SDK)](./config/config.md).
   * Leggi la guida sulla [configurazione delle specifiche di autenticazione](./config/authspec.md) per comprendere meglio i diversi tipi di autenticazione che puoi utilizzare per l&#39;origine.
   * Per informazioni sui diversi tipi di impaginazione, i formati di pianificazione e gli schemi personalizzati che è possibile configurare per l&#39;origine, leggere la guida alla [configurazione delle specifiche di origine](./config/sourcespec.md).
   * Per informazioni su come definire i parametri necessari per l&#39;esplorazione e l&#39;ispezione degli oggetti contenuti nell&#39;origine, leggere la guida sulla [configurazione delle specifiche di esplorazione](./config/explorespec.md).
* Per iniziare a documentare la tua origine, leggi la [panoramica sulla creazione di documentazione per le origini self-service](./documentation/doc-overview.md)
   * Puoi utilizzare questo modello di documentazione API [sources](./documentation/template.md) per strutturare la documentazione API.
   * Puoi utilizzare questo [modello di documentazione dell&#39;interfaccia utente di origini](./documentation/ui-template.md) per strutturare la documentazione dell&#39;interfaccia utente.
   * Consulta la guida su [utilizzo dell&#39;interfaccia Web GitHub](./documentation/github.md) per i passaggi su come creare documentazione utilizzando GitHub.
   * Consulta la guida su [utilizzo di un editor di testo](./documentation/text-editor.md) per i passaggi su come creare documentazione utilizzando il computer locale.
