---
title: Panoramica sullo sviluppo di estensioni
description: Scopri i componenti principali di diverse estensioni di tag e il processo di sviluppo delle stesse in Adobe Experience Platform.
exl-id: b72df3df-f206-488d-a690-0f086973c5b6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 23%

---

# Panoramica sullo sviluppo di estensioni

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch è ora una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Uno degli obiettivi principali dei tag in Adobe Experience Platform è la creazione di un ecosistema aperto che consenta anche ai tecnici che non fanno parte di Adobe di pubblicare funzionalità aggiuntive sui propri siti web e applicazioni mobili. Questa operazione viene eseguita tramite le estensioni tag. Una volta installata un’estensione su una proprietà tag, la relativa funzionalità diventa disponibile per tutti gli utenti della proprietà.

Questo documento illustra i componenti principali di un’estensione e fornisce i collegamenti a ulteriore documentazione per aiutarti a fornire una guida nel processo di sviluppo.

## Struttura delle estensioni

Un’estensione è costituita da una directory di file. In particolare, un’estensione è costituita da un file manifesto, moduli libreria e viste.

### File manifesto

Nella directory principale deve esistere un file manifesto ([`extension.json`](./manifest.md)). Questo file descrive la composizione dell’estensione e la posizione in cui si trovano alcuni file all’interno della directory. Il manifesto funziona in modo simile a un file [`package.json`](https://docs.npmjs.com/files/package.json) in un progetto [npm](https://www.npmjs.com/).

### Moduli libreria

I moduli libreria sono file che descrivono i diversi [componenti](#components) forniti da un&#39;estensione, ovvero la logica da emettere nella libreria runtime dei tag. Il contenuto di ogni file del modulo libreria deve seguire lo standard del modulo [CommonJS](https://nodejs.org/api/modules.html#modules-commonjs-modules).

Ad esempio, se stai creando un tipo di azione denominato &quot;send beacon&quot;, devi disporre di un file contenente la logica che invia il beacon. Se si utilizza JavaScript, il file potrebbe essere denominato `sendBeacon.js`. Il contenuto di questo file verrà emesso nella libreria runtime dei tag.

È possibile inserire i file del modulo libreria in qualsiasi posizione all&#39;interno della directory dell&#39;estensione, purché si descriva la loro posizione in `extension.json`.

### Viste

Una visualizzazione è un file HTML che può essere caricato in un elemento [`iframe`](https://developer.mozilla.org/it-IT/docs/Web/HTML/Element/iframe) all&#39;interno dell&#39;applicazione dei tag, in particolare tramite l&#39;interfaccia utente di Experience Platform e l&#39;interfaccia utente di Data Collection. Per comunicare con l’applicazione, la vista deve includere uno script fornito dall’estensione e deve essere conforme a una piccola API.

La configurazione è il file di visualizzazione più importante per qualsiasi estensione. Per ulteriori informazioni, consulta la sezione sulle [configurazioni delle estensioni](#configuration).

Non sono previste restrizioni per le modalità di utilizzo delle librerie nelle viste. In altre parole, puoi utilizzare jQuery, Underscore, React, Angular, Bootstrap o altri. Tuttavia, si consiglia comunque di conferire all’estensione un aspetto simile a quello dell’interfaccia utente.

Si consiglia di inserire tutti i file relativi alla vista (HTML, CSS, JavaScript) in una singola sottodirectory, isolata dai file del modulo libreria. In `extension.json` è possibile descrivere la posizione di questa sottodirectory di visualizzazione. Experience Platform distribuirà quindi questa sottodirectory (e solo questa sottodirectory) dai propri server web.

## Componenti libreria {#components}

Ogni estensione definisce un set di funzionalità. Queste funzionalità vengono implementate includendo una [libreria](../ui/publishing/libraries.md) distribuita nel sito Web o nell&#39;app. Le librerie sono una raccolta di singoli componenti, tra cui condizioni, azioni, elementi dati e altro ancora. Ogni componente della libreria è un codice riutilizzabile (fornito da un’estensione) emesso all’interno del runtime dei tag.

A seconda che tu stia sviluppando un’estensione web o un’estensione edge, i tipi di componenti disponibili e i relativi casi d’uso variano. Per una panoramica dei componenti disponibili per ciascun tipo di estensione, fai riferimento alle sottosezioni seguenti.

### Componenti per estensioni web {#web}

Nelle estensioni web, le regole vengono attivate attraverso gli eventi, che possono eseguire azioni specifiche se viene soddisfatta una determinata serie di condizioni. Per ulteriori informazioni, consulta la panoramica sul [flusso dei moduli nelle estensioni web](./web/flow.md).

Oltre ai [moduli core](./web/core.md) forniti da Adobe, è possibile definire i seguenti componenti libreria nelle estensioni Web:

* [Eventi](./web/event-types.md)
* [Condizioni](./web/condition-types.md)
* [Azioni](./web/action-types.md)
* [Elementi dati](./web/data-element-types.md)
* [Moduli condivisi](./web/shared.md)

>[!NOTE]
>
>Per informazioni dettagliate sul formato richiesto per l&#39;implementazione dei componenti libreria nelle estensioni Web, vedere la [panoramica sul formato dei moduli](./web/format.md).

### Componenti per estensioni Edge {#edge}

Nelle estensioni Edge, le regole vengono attivate tramite controlli di condizione che, se vengono superati, eseguono azioni specifiche. Per ulteriori informazioni, consulta la panoramica sul [flusso di estensioni Edge](./edge/flow.md).

Nelle estensioni Edge è possibile definire i seguenti componenti libreria:

* [Condizioni](./edge/condition-types.md)
* [Azioni](./edge/action-types.md)
* [Elementi dati](./edge/data-element-types.md)

>[!NOTE]
>
>Per informazioni dettagliate sul formato richiesto per l’implementazione dei moduli libreria nelle estensioni Edge, consulta la [panoramica sul formato dei moduli](./edge/format.md).

## Configurazione dell&#39;estensione {#configuration}

Per configurazione di un’estensione si intende il modo in cui essa raccoglie le impostazioni globali da un utente. La configurazione è costituita da un componente vista che esporta ed emette le impostazioni all’interno della libreria runtime dei tag come oggetto semplice.

Ad esempio, considera un’estensione che consente all’utente di inviare un beacon utilizzando un’azione &quot;Invia beacon&quot; e che il beacon debba sempre contenere un ID account. Invece di richiedere agli utenti un ID account ogni volta che configurano un’azione &quot;Invia beacon&quot;, l’estensione deve richiedere l’ID account una volta dalla vista di configurazione dell’estensione. Ogni volta che un beacon viene inviato, l&#39;azione &quot;Invia beacon&quot; può richiamare l&#39;ID account dalla configurazione dell&#39;estensione e aggiungerlo al beacon.

Quando un utente installa un’estensione su una proprietà nell’interfaccia utente di, viene visualizzata la vista per la configurazione dell’estensione, che deve essere completata per completare l’installazione.

Per ulteriori informazioni, consulta la guida sulle [configurazioni delle estensioni](./configuration.md).

## Invio di estensioni

Una volta completata la creazione dell’estensione, puoi inviarla per essere elencata nel catalogo delle estensioni in Experience Platform. Per ulteriori informazioni, consulta la [panoramica del processo di invio dell&#39;estensione](./submit/overview.md).
