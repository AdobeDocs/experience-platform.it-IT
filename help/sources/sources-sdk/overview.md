---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
solution: Experience Platform
title: Panoramica dell’SDK per sorgenti (Beta)
topic-legacy: overview
description: Adobe Experience Platform Sources SDK è un set di API di configurazione che ti consente di integrare una sorgente basata su API REST utilizzando l’API del servizio di flusso per Experience Platform i tuoi dati.
hide: true
hidefromtoc: true
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: ce902e461c748e30e0307558da894a4dbdd212a4
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# Panoramica dell’SDK per sorgenti (Beta)

>[!IMPORTANT]
>
>L&#39;SDK di Origini è attualmente in versione beta e la tua organizzazione potrebbe non averne ancora accesso. La funzionalità descritta in questa documentazione è soggetta a modifiche.

Adobe Experience Platform Sources SDK è un set di API di configurazione che ti consente di integrare una sorgente basata su API REST utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) per dare Experience Platform ai tuoi dati.

Con l&#39;SDK di Origini puoi:

* Configurare una nuova origine per il catalogo Platform, completa di creare, leggere, aggiornare ed eliminare funzionalità utilizzando [!DNL Flow Service] API.
* Definisci le specifiche dell’origine, comprese le informazioni relative ai tipi di autenticazione supportati e al modo in cui vengono recuperati i dati delle risorse.
* Crea la documentazione rivolta all’utente per la nuova sorgente.

La documentazione di Origini SDK fornisce istruzioni per l’utilizzo di Adobe Experience Platform Sources SDK per configurare, testare e rilasciare un’integrazione sorgente basata su API REST con Platform e affinché la tua sorgente diventi parte del catalogo origini in continua crescita.

![catalogo](./assets/catalog.png)

## Informazioni sulle origini

Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi di Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

Per ulteriori informazioni sulle origini e per visualizzare un elenco delle diverse origini attualmente supportate in Platform, consulta la sezione [panoramica di origini](../home.md).

## Creare un’origine

Attraverso l’SDK di Origini è possibile integrare la propria origine basata su API REST e trasferire i dati a Platform con [!DNL Flow Service]. L’SDK di Origini consente di integrare una nuova origine con Platform, creando e inviando nuove specifiche di connessione tramite [!DNL Flow Service] API.

Consulta la guida su [creazione di una nuova specifica di connessione](./api/api-overview.md) per informazioni su come integrare una nuova sorgente in Platform.

## Documentare l&#39;origine

Una volta creata la sorgente, consulta la sezione [guida alla documentazione](./documentation/doc-overview.md) per istruzioni su come documentare la propria origine attraverso [!DNL GitHub] interfaccia web o tramite il tuo editor di testo.

## Processo di alto livello

Il processo dettagliato per configurare l’origine in Experience Platform è descritto di seguito:

* Leggi la sezione [Guida all’API SDK per le sorgenti](./api/api-overview.md);
   * Leggi la sezione [guida introduttiva](./api/getting-started.md);
   * Segui l’esercitazione su [creazione di una nuova specifica di connessione](./api/create.md);
   * Segui l’esercitazione su [aggiornamento delle specifiche di connessione](./api/update-connection-specs.md);
   * Segui l’esercitazione su [aggiunta del nuovo ID della specifica di connessione a una specifica di flusso](./api/update-flow-specs.md)
   * [Invia la nuova origine](./api/submit.md).
* Per comprendere meglio la struttura e le proprietà di una specifica di connessione, consulta la guida [opzioni di configurazione per l’SDK di Origini](./config/config.md);
   * Consulta la guida su [configurazione delle specifiche di autenticazione](./config/authspec.md);
   * Consulta la guida su [configurazione delle specifiche di origine](./config/sourcespec.md);
   * Consulta la guida su [configurazione delle specifiche di esplorazione](./config/explorespec.md);
* Per iniziare a documentare la sorgente, vedi [panoramica sulla creazione della documentazione per l&#39;SDK di Origini](./documentation/doc-overview.md)
   * Puoi utilizzarlo [modello di documentazione API di origini](./documentation/template.md) per strutturare la documentazione API;
   * Puoi utilizzarlo [modello di documentazione dell’interfaccia utente di origini](./documentation/ui-template.md) per strutturare la documentazione dell’interfaccia utente;
   * Consulta la guida su [utilizzo dell’interfaccia web GitHub](./documentation/github.md) per i passaggi su come creare la documentazione utilizzando GitHub;
   * Consulta la guida su [utilizzo di un editor di testo](./documentation/text-editor.md) per informazioni su come creare la documentazione utilizzando il computer locale.
