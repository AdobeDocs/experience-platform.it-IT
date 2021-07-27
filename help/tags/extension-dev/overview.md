---
title: Panoramica sullo sviluppo di estensioni
description: Scopri i componenti principali di diversi tipi di estensione tag e il processo di sviluppo dell’estensione in Adobe Experience Platform.
source-git-commit: a165f0c254885b17db734ab09bf6523175a11dfb
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 21%

---

# Panoramica sullo sviluppo di estensioni

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Uno degli obiettivi principali dei tag in Adobe Experience Platform è quello di creare un ecosistema aperto in cui gli ingegneri al di fuori di Adobe possono esporre funzionalità aggiuntive sui loro siti web e applicazioni mobili. Questa operazione viene eseguita tramite le estensioni di tag. Una volta installata un&#39;estensione su una proprietà tag, la relativa funzionalità diventa disponibile per l&#39;uso da parte di tutti gli utenti della proprietà.

Questo documento illustra i componenti principali di un&#39;estensione e fornisce collegamenti a ulteriori documentazione per aiutarti nel processo di sviluppo dell&#39;estensione.

## Struttura delle estensioni

Un’estensione è costituita da una directory di file. In particolare, un&#39;estensione consiste in un file manifesto, moduli libreria e visualizzazioni.

### File manifesto

Nella directory principale della directory deve esistere un file manifesto ([`extension.json`](./manifest.md)). Questo file descrive la composizione dell&#39;estensione e dove alcuni file si trovano all&#39;interno della directory. Il manifesto funziona in modo simile a un file [`package.json`](https://docs.npmjs.com/files/package.json) in un progetto [npm](https://www.npmjs.com/).

### Moduli libreria

I moduli libreria sono i file che descrivono i diversi [componenti](#components) forniti da un&#39;estensione (in altre parole, la logica da emettere all&#39;interno della libreria di runtime di tag). Il contenuto di ciascun file del modulo libreria deve seguire lo standard del modulo [CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1.1).

Ad esempio, se stai creando un tipo di azione denominato &quot;invia beacon&quot;, devi disporre di un file contenente la logica che invia il beacon. Se utilizzi JavaScript, il file potrebbe essere denominato `sendBeacon.js`. Il contenuto di questo file verrà emesso all’interno della libreria di runtime di tag.

Puoi inserire i file dei moduli della libreria in qualsiasi punto ti piaccia all&#39;interno della directory dell&#39;estensione, purché ne descriva le posizioni in `extension.json`.

### Viste

Una visualizzazione è un file HTML che può essere caricato in un elemento [`iframe`](https://developer.mozilla.org/it-IT/docs/Web/HTML/Element/iframe) all&#39;interno dell&#39;applicazione tag, in particolare tramite l&#39;interfaccia utente di raccolta dati. Per comunicare con l’applicazione, la visualizzazione deve includere uno script fornito dall’estensione e deve essere conforme a una piccola API.

Il file di visualizzazione più importante per qualsiasi estensione è la sua configurazione. Per ulteriori informazioni, consulta la sezione sulle [configurazioni di estensione](#configuration) .

Non sono previste restrizioni per le modalità di utilizzo delle librerie nelle viste. In altre parole, è possibile utilizzare jQuery, Sottolineatura, React, Angular, Bootstrap o altri. Tuttavia, si consiglia comunque di fare in modo che l’estensione abbia un aspetto e un aspetto simili all’interfaccia utente di raccolta dati.

Si consiglia di inserire tutti i file relativi alla vista (HTML, CSS, JavaScript) in una singola sottodirectory, isolata dai file del modulo libreria. In `extension.json` è possibile descrivere la posizione della sottodirectory di visualizzazione. Platform distribuirà quindi questa sottodirectory (e solo questa sottodirectory) dai propri server web.

## Componenti della libreria {#components}

Ciascuna estensione definisce un set di funzionalità. Queste funzionalità vengono implementate includendo in una [libreria](../ui/publishing/libraries.md) implementata nel sito web o nell&#39;app. Le librerie sono una raccolta di singoli componenti, tra cui condizioni, azioni, elementi dati e altro ancora. Ogni componente libreria è un pezzo di codice riutilizzabile (fornito da un&#39;estensione) emesso all&#39;interno del runtime di tag.

A seconda che stiate sviluppando un’estensione Web o un’estensione Edge, i tipi di componenti disponibili e i relativi casi d’uso differiscono. Per una panoramica dei componenti disponibili per ciascun tipo di estensione, fai riferimento alle sottosezioni seguenti.

### Componenti per estensioni web {#web}

Nelle estensioni web, le regole vengono attivate attraverso gli eventi, che possono eseguire azioni specifiche se viene soddisfatta una determinata serie di condizioni. Per ulteriori informazioni, consulta la panoramica sul [flusso dei moduli nelle estensioni web](./web/flow.md).

Oltre ai [moduli di base](./web/core.md) forniti da Adobe, puoi definire i seguenti componenti della libreria nelle estensioni web:

* [Eventi](./web/event-types.md)
* [Condizioni](./web/condition-types.md)
* [Azioni](./web/action-types.md)
* [Elementi dati](./web/data-element-types.md)
* [Moduli condivisi](./web/shared.md)

>[!NOTE]
>
>Per informazioni dettagliate sul formato richiesto per l&#39;implementazione dei componenti libreria nelle estensioni web, consulta la [panoramica del formato modulo](./web/format.md).

### Componenti per estensioni edge {#edge}

Nelle estensioni Edge, le regole vengono attivate tramite controlli di condizione che, se vengono superati, eseguono azioni specifiche. Per ulteriori informazioni, consulta la panoramica sul [flusso di estensione edge](./edge/flow.md) .

Nelle estensioni edge di puoi definire i seguenti componenti della libreria:

* [Condizioni](./edge/condition-types.md)
* [Azioni](./edge/action-types.md)
* [Elementi dati](./edge/data-element-types.md)

>[!NOTE]
>
>Per informazioni dettagliate sul formato richiesto per l’implementazione dei moduli libreria nelle estensioni Edge, consulta la [panoramica sul formato dei moduli](./edge/format.md).

## Configurazione dell&#39;estensione {#configuration}

Per configurazione di un’estensione si intende il modo in cui essa raccoglie le impostazioni globali da un utente. La configurazione è costituita da un componente vista che esporta ed emette le impostazioni all’interno della libreria di runtime di tag come oggetto normale.

Ad esempio, considera un&#39;estensione che consente all&#39;utente di inviare un beacon utilizzando un&#39;azione &quot;Invia beacon&quot; e il beacon deve sempre contenere un ID account. Invece di richiedere agli utenti un ID account ogni volta che configurano un&#39;azione &quot;Invia beacon&quot;, l&#39;estensione deve richiedere l&#39;ID account una volta dalla vista di configurazione dell&#39;estensione. Ogni volta che un beacon viene inviato, l’azione &quot;Invia beacon&quot; può estrarre l’ID account dalla configurazione dell’estensione e aggiungerlo al beacon.

Quando gli utenti installano un&#39;estensione a una proprietà nell&#39;interfaccia utente, visualizzano la vista di configurazione dell&#39;estensione, che devono completare per completare l&#39;installazione.

Per ulteriori informazioni, consulta la guida sulle [configurazioni di estensione](./configuration.md).

## Invio di estensioni

Una volta completata la creazione dell’estensione, puoi inviarla per essere elencata nel catalogo delle estensioni in Platform. Per ulteriori informazioni, consulta la [panoramica del processo di invio dell’estensione](./submit/overview.md) .