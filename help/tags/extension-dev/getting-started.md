---
title: Guida introduttiva allo sviluppo delle estensioni
description: Introduzione allo sviluppo di estensioni tag in Adobe Experience Platform.
exl-id: 3925b928-0180-4a4f-aaa6-42f342089560
source-git-commit: 0a4883cff4f8e04dd0dd62a9e01435fa302a9e54
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 91%

---

# Guida introduttiva allo sviluppo delle estensioni

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Per imparare a creare estensioni, utilizzeremo lo strumento di scaffolding open source, fornito da ingegneri Adobe per creare i file e la struttura di file necessari per il pacchetto di estensione. Non ti resterà quindi che occuparti della parte importante: scrivere di fatto il codice.

## Prerequisiti 

* Installa [Node.js](https://nodejs.org/it/download).

## Impostazione dell’estensione

Crea una directory in cui sistemare i file dell’estensione.

```shell
mkdir example && cd example
```

Questa guida utilizza lo strumento di scaffolding delle estensioni per creare la struttura iniziale dell’estensione, in modo che gli sviluppatori possano iniziare rapidamente a scrivere il codice. Se necessario, questo processo può essere eseguito manualmente senza lo strumento di scaffolding.

Avvia lo strumento di scaffolding.

```shell
npx @adobe/reactor-scaffold
```

Lo strumento di scaffolding richiede alcune opzioni di configurazione iniziali, come segue:

* Nome visualizzato: il nome visibile dell’estensione
* Versione: versione dell’estensione
* Descrizione: breve descrizione dello scopo dell’estensione
* Autore: nome dell’autore dell’estensione

Lo strumento di scaffolding fornirà quindi le opzioni per la creazione della struttura dell’estensione:

* [Vista di configurazione dell’estensione](./configuration.md): vista (file HTML) attraverso la quale un’estensione raccoglie le impostazioni globali fornite da un utente.
* [Tipi di evento](./web/event-types.md): definisce un’attività da monitorare. Ad esempio, è utile per sapere quando un utente scorre rapidamente la pagina o interagisce con un suo elemento. Gli eventi possono quindi essere utilizzati nelle regole per eseguire delle azioni.
* [Tipi di condizione](./web/condition-types.md): i tipi di condizione controllano se un elemento è vero o falso. Ad esempio, è utile per sapere se l’utente utilizza il browser Chrome, se usa un iPad o se si trova su un dominio specifico.
* [Tipi di azione](./web/action-types.md): l’azione da eseguire quando si verifica un evento. Ad esempio, si può inviare un beacon di analisi, mostrare un’offerta, salvare un cookie o aprire una chat di supporto.
* [Tipi di elementi dati](./web/data-element-types.md): un tipo di elemento dati recupera dei dati. Questi possono provenire dall’archivio locale, da un cookie, da un elemento DOM o da uno specifico percorso.
* [Moduli condivisi](./web/shared.md): un modulo condiviso è un meccanismo mediante il quale le estensioni possono comunicare con altre estensioni.
* [Viste](./web/views.md): ogni evento, condizione, azione o tipo di elemento dati può fornire una vista che consenta all’utente di fornire le impostazioni.

>[!NOTE]
>
>* Le successive esecuzioni dello strumento di scaffolding salteranno il passaggio di configurazione iniziale.
>* È possibile aggiungere più eventi, condizioni e azioni.
>* Può esistere una sola vista di configurazione.


## Passaggi successivi

* Segui le [Panoramica del processo di invio](./submit/overview.md) e prepararsi a [convalida](./submit/upload-and-test.md#validate) e [caricare](./submit/upload-and-test.md#integration) l’estensione per il test all’interno dell’ecosistema di tag.
