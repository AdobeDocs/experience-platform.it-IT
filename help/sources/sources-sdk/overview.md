---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
solution: Experience Platform
title: Panoramica delle sorgenti self-service (SDK per batch)
topic-legacy: overview
description: Origini self-service di Adobe Experience Platform (SDK di batch) è un set di API di configurazione che ti consentono di integrare un’origine basata su API REST utilizzando l’API del servizio di flusso per fornire Experienci Platform ai tuoi dati.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Panoramica delle origini self-service (SDK per batch)

Origini self-service di Adobe Experience Platform (SDK batch) è un framework che consente di integrare una sorgente basata su API REST nel catalogo delle sorgenti di Experience Platform utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Origini self-service (SDK batch) fornisce un set di API di configurazione per creare la tua origine e portare i dati batch ad Experience Platform.

Con Origini self-service (SDK batch), puoi:

* Configura e integra una nuova origine nel catalogo di Experience Platform utilizzando [!DNL Flow Service] API.
* Definisci le specifiche dell’origine, comprese le informazioni relative ai tipi di autenticazione supportati e al modo in cui vengono recuperati i dati delle risorse.
* Crea la documentazione rivolta all’utente per la nuova sorgente.

La documentazione di Origini self-service fornisce istruzioni su come configurare, testare e rilasciare un’integrazione sorgente basata su API REST con Experience Platform e far sì che la tua sorgente diventi parte del catalogo origini in continua crescita.

![catalogo](./assets/catalog.png)

## Informazioni sulle origini

Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Experience Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

Per ulteriori informazioni sulle origini e per visualizzare un elenco delle diverse origini attualmente supportate all&#39;Experience Platform, consulta la [panoramica di origini](../home.md).

## Creare un’origine

Tramite Origini self-service puoi integrare la tua origine basata su API REST e portare i tuoi dati ad Experience Platform con [!DNL Flow Service]. È possibile integrare un&#39;origine nel catalogo origini Experience Platform creando, configurando e inviando nuove specifiche di connessione tramite la [!DNL Flow Service] API.

Consulta la guida su [creazione di una nuova specifica di connessione](./api/api-overview.md) per informazioni su come integrare una nuova origine in Experience Platform.

## Documentare l&#39;origine

Una volta creata la sorgente, consulta la sezione [guida alla documentazione](./documentation/doc-overview.md) per istruzioni su come documentare la propria origine attraverso [!DNL GitHub] interfaccia web o tramite il tuo editor di testo.

## Processo di alto livello

Il processo dettagliato per configurare l’origine in Experience Platform è descritto di seguito:

* Leggi la sezione [Guida all’API di Origini self-service (SDK per batch)](./api/api-overview.md).
   * Leggi la sezione [guida introduttiva](./api/getting-started.md).
   * Segui l’esercitazione su [creazione di una nuova specifica di connessione](./api/create.md).
   * Segui l’esercitazione su [aggiornamento delle specifiche di connessione](./api/update-connection-specs.md).
   * Segui l’esercitazione su [aggiunta del nuovo ID della specifica di connessione a una specifica di flusso](./api/update-flow-specs.md)
   * [Invia la nuova origine](./api/submit.md).
* Per comprendere meglio la struttura e le proprietà di una specifica di connessione, leggere la guida in [opzioni di configurazione per Origini self-service (SDK batch)](./config/config.md).
   * Leggi la guida su [configurazione delle specifiche di autenticazione](./config/authspec.md) per comprendere meglio i diversi tipi di autenticazione che puoi utilizzare per la tua origine.
   * Leggi la guida su [configurazione delle specifiche di origine](./config/sourcespec.md) per informazioni sui diversi tipi di impaginazione, formati di pianificazione e schemi personalizzati che possono essere configurati per la tua origine.
   * Leggi la guida su [configurazione delle specifiche di esplorazione](./config/explorespec.md) per informazioni su come definire i parametri necessari per l&#39;esplorazione e l&#39;ispezione degli oggetti contenuti nell&#39;origine.
* Per iniziare a documentare la tua origine, leggi la sezione [panoramica sulla creazione della documentazione per Origini self-service](./documentation/doc-overview.md)
   * Puoi utilizzarlo [modello di documentazione API di origini](./documentation/template.md) per strutturare la documentazione API.
   * Puoi utilizzarlo [modello di documentazione dell’interfaccia utente di origini](./documentation/ui-template.md) per strutturare la documentazione dell’interfaccia utente.
   * Consulta la guida su [utilizzo dell’interfaccia web GitHub](./documentation/github.md) per informazioni su come creare la documentazione utilizzando GitHub.
   * Consulta la guida su [utilizzo di un editor di testo](./documentation/text-editor.md) per informazioni su come creare la documentazione utilizzando il computer locale.
