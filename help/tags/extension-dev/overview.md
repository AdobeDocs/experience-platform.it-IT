---
title: Panoramica sullo sviluppo di estensioni
description: Scopri i componenti principali di diversi tipi di estensione tag e il processo di sviluppo dell’estensione in Adobe Experience Platform.
source-git-commit: 421d1d0660c4c9c7280974f8a812a8f0e4f7cbea
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 68%

---

# Panoramica sullo sviluppo di estensioni

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Uno degli obiettivi principali di Adobe Experience Platform è la creazione di un ecosistema aperto in cui gli ingegneri al di fuori del team di progettazione principale possono esporre funzionalità aggiuntive tramite tag. Questo avviene tramite le estensioni di tag. Una volta che un utente ha installato un&#39;estensione su una proprietà tag, la sua funzionalità diventa disponibile per l&#39;uso da parte di tutti gli utenti della proprietà.

Questo documento illustra i componenti principali di diversi tipi di estensione e fornisce collegamenti per ulteriore documentazione che ti guiderà sul processo di sviluppo dell&#39;estensione.

## Moduli libreria

I moduli libreria sono parti di codice riutilizzabile fornito da un&#39;estensione che vengono emesse all&#39;interno della libreria di runtime di tag. A seconda del fatto che tu stia sviluppando un&#39;estensione Web o un&#39;estensione edge, i tipi di modulo disponibili e i relativi casi di utilizzo saranno diversi. Per una panoramica dei moduli per ciascun tipo di estensione, fai riferimento alle seguenti sottosezioni:

* [Moduli per estensioni web](#web-modules)
* [Moduli per estensioni Edge](#edge-modules)

### Moduli per estensioni web {#web-modules}

Nelle estensioni web, le regole vengono attivate attraverso gli eventi, che possono eseguire azioni specifiche se viene soddisfatta una determinata serie di condizioni. Per ulteriori informazioni, consulta la panoramica sul [flusso dei moduli nelle estensioni web](./web/flow.md).

Oltre ai [moduli core](./web/core.md) forniti da Adobe, nelle estensioni è possibile definire i seguenti tipi di moduli libreria:

* [Tipi di evento](#web-event)
* [Tipi di condizione](#web-condition)
* [Tipi di azioni](#web-action)
* [Tipi di elementi dati](#web-data-element)
* [Moduli condivisi](#shared)

>[!NOTE]
>
>Per informazioni dettagliate sul formato richiesto per l’implementazione dei moduli libreria nelle estensioni web, consulta la [panoramica sul formato dei moduli](./web/format.md).

#### Tipi di evento {#web-event}

Un evento regola è un’attività che deve essere eseguita prima dell’attivazione di una regola.

Ad esempio, un’estensione potrebbe fornire un tipo di evento “gesture” che controlla se si verifica un determinato movimento del mouse o del tocco. Quando si verifica il gesto, la logica dell’evento attiva la regola.

I tipi di evento sono in genere costituiti da (1) una visualizzazione mostrata all’interno dell’interfaccia utente Raccolta dati che consente agli utenti di modificare le impostazioni per l’evento e (2) un modulo libreria emesso all’interno della libreria runtime di tag per interpretare le impostazioni e controllare che si verifichi una determinata attività.

[Per saperne di più](./web/event-types.md)

#### Tipi di condizione {#web-condition}

La condizione di una regola viene valutata dopo che si è verificato un evento regola. Tutte le condizioni devono restituire true affinché la regola possa continuare l’elaborazione. L’eccezione si verifica quando gli utenti inseriscono esplicitamente le condizioni in un bucket di “eccezione”, nel qual caso tutte le condizioni all’interno del bucket devono restituire false per consentire alla regola di continuare l’elaborazione.

Ad esempio, un’estensione potrebbe fornire un tipo di condizione “viewport contains” in cui l’utente di potrebbe specificare un selettore CSS. Quando la condizione viene valutata sul sito web del client, l’estensione sarà in grado di trovare elementi che corrispondono al selettore CSS e restituire se uno di essi è contenuto nella finestra dell’utente.

I tipi di condizioni in genere consistono in (1) una visualizzazione mostrata all’interno dell’interfaccia utente Raccolta dati che consente agli utenti di modificare le impostazioni della condizione e (2) un modulo libreria emesso all’interno della libreria runtime di tag per interpretare le impostazioni e valutare una condizione.

[Per saperne di più](./web/condition-types.md)

#### Tipi di azioni {#web-action}

Un’azione regola viene eseguita dopo che si è verificato l’evento regola e se le condizioni hanno superato la valutazione.

Ad esempio, un’estensione potrebbe fornire un tipo di azione “show support chat” che potrebbe mostrare una finestra di dialogo con la chat di supporto per aiutare gli utenti che riscontrano difficoltà nel concludere un acquisto.

I tipi di azione in genere consistono in (1) una visualizzazione mostrata all’interno dell’interfaccia utente Raccolta dati che consente agli utenti di modificare le impostazioni per l’azione e (2) un modulo libreria emesso all’interno della libreria runtime di tag per interpretare le impostazioni ed eseguire un’azione.

[Per saperne di più](./web/action-types.md)

#### Tipi di elementi dati {#web-data-element}

Gli elementi dati sono essenzialmente alias per parti di dati su una pagina, indipendentemente dal fatto che tali dati siano presenti in parametri di stringa di query, cookie, elementi DOM o in altre aree. Le regole possono fare riferimento a un elemento dati che funge da astrazione per accedere a tali dati. Quando la posizione dei dati cambia in futuro (ad esempio, da un elemento DOM `innerHTML` al valore di una variabile JavaScript), è possibile riconfigurare un singolo elemento dati mantenendo invariate tutte le regole che vi fanno riferimento.

Un tipo di elemento dati consente agli utenti di configurare elementi dati per accedere a determinati dati in un modo particolare. Ad esempio, un’estensione potrebbe fornire un tipo di elemento dati “elemento di archiviazione locale” in cui l’utente di può specificare il nome di un elemento specifico. Quando una regola fa riferimento all’elemento dati, l’estensione sarà in grado di cercare il valore dell’elemento nell’archiazione locale utilizzando il nome fornito dall’utente durante la configurazione dell’elemento dati.

I tipi di elementi dati in genere consistono in (1) una visualizzazione mostrata nell’interfaccia utente di raccolta dati che consente agli utenti di modificare le impostazioni per l’elemento dati e (2) un modulo libreria emesso all’interno della libreria di runtime di tag per interpretare le impostazioni e recuperare parti di dati.

[Per saperne di più](./web/data-element-types.md)

#### Moduli condivisi {#shared}

Un modulo condiviso è un modulo esposto da un’estensione in modo che un’altra vi possa accedere. Questo può essere un meccanismo molto utile per la comunicazione tra le estensioni. Ad esempio, l’estensione A può caricare una parte di dati in modo asincrono e renderla disponibile all’estensione B tramite una [promise](https://developer.mozilla.org/it-IT/docs/Web/JavaScript/Reference/Global_Objects/Promise), o promessa.

I moduli condivisi sono inclusi nella libreria anche quando non vengono mai richiamati dall’interno di altre estensioni. Per non aumentare inutilmente la dimensione della libreria, occorre prestare attenzione a ciò che viene esposto come modulo condiviso.

I moduli condivisi non hanno un componente vista.

[Per saperne di più](./web/shared.md)

### Moduli per estensioni Edge {#edge-modules}

Nelle estensioni Edge, le regole vengono attivate tramite controlli di condizione che, se vengono superati, eseguono azioni specifiche. Per ulteriori informazioni, consulta la panoramica sul [flusso dei moduli nelle estensioni Edge](./edge/flow.md).

Nelle estensioni Edge, è possibile definire moduli libreria personalizzati. Questi possono essere suddivisi in categorie nei seguenti tipi:

* [Tipi di condizione](#condition)
* [Tipi di azioni](#action)
* [Tipi di elementi dati](#data-element)

>[!NOTE]
>
>Per informazioni dettagliate sul formato richiesto per l’implementazione dei moduli libreria nelle estensioni Edge, consulta la [panoramica sul formato dei moduli](./edge/format.md).

#### Tipi di condizione {#condition}

La condizione di una regola viene valutata dopo che si è verificato un evento regola. Tutte le condizioni devono restituire true affinché la regola possa continuare l’elaborazione. L’eccezione si verifica quando gli utenti inseriscono esplicitamente le condizioni in un bucket di “eccezione”, nel qual caso tutte le condizioni all’interno del bucket devono restituire false per consentire alla regola di continuare l’elaborazione.

Ad esempio, un’estensione potrebbe fornire un tipo di condizione “viewport contains” in cui l’utente di potrebbe specificare un selettore CSS. Quando la condizione viene valutata sul sito web del client, l’estensione sarà in grado di trovare elementi che corrispondono al selettore CSS e restituire se uno di essi è contenuto nella finestra dell’utente.

I tipi di condizioni in genere consistono in (1) una visualizzazione mostrata all’interno dell’interfaccia utente Raccolta dati che consente agli utenti di modificare le impostazioni della condizione e (2) un modulo libreria emesso all’interno della libreria runtime di tag per interpretare le impostazioni e valutare una condizione.

[Per saperne di più](./web/condition-types.md)

#### Tipi di azioni {#action}

Un’azione di una regola viene eseguita dopo che le condizioni della regola hanno superato la valutazione.

Ad esempio, un’estensione potrebbe fornire un tipo di azione “show support chat” che potrebbe mostrare una finestra di dialogo con la chat di supporto per aiutare gli utenti che riscontrano difficoltà nel concludere un acquisto.

I tipi di azione in genere consistono in (1) una visualizzazione mostrata all’interno dell’interfaccia utente Raccolta dati che consente agli utenti di modificare le impostazioni per l’azione e (2) un modulo libreria emesso all’interno della libreria runtime di tag per interpretare le impostazioni ed eseguire un’azione.

[Per saperne di più](./web/action-types.md)

#### Tipi di elementi dati {#data-element}

Essenzialmente, gli elementi dati sono alias per porzioni di dati su una pagina, indipendentemente dalla posizione in cui tali dati si trovano all’interno dell’evento ricevuto dal server. Le regole possono fare riferimento a un elemento dati che funge da astrazione per accedere a tali dati. Se la posizione dei dati cambia in futuro (ad esempio se viene modificato l’evento chiave che contiene il valore), è possibile riconfigurare un singolo elemento dati mantenendo invariate tutte le regole che vi fanno riferimento.

I tipi di elementi dati in genere consistono in (1) una visualizzazione mostrata nell’interfaccia utente di raccolta dati che consente agli utenti di modificare le impostazioni per l’elemento dati e (2) un modulo libreria emesso all’interno della libreria di runtime di tag per interpretare le impostazioni e recuperare parti di dati.

[Per saperne di più](./web/data-element-types.md)

## Configurazione dell&#39;estensione

Per configurazione di un’estensione si intende il modo in cui essa raccoglie le impostazioni globali da un utente. Consideriamo ad esempio un’estensione che consente all’utente di inviare un beacon utilizzando un’azione Invia beacon, e che il beacon debba sempre contenere un ID account. Vogliamo evitare che agli utenti venga richiesto di immettere l’ID account ogni volta che devono configurare un’azione Invia beacon. L’estensione dovrà quindi richiedere l’ID account una sola volta, dalla vista di configurazione dell’estensione. Ogni volta che un beacon viene inviato, il modulo libreria dell’azione Invia beacon può richiamare l’ID account dalla configurazione dell’estensione e aggiungerlo al beacon.

Quando gli utenti installano un&#39;estensione a una proprietà tag, viene visualizzata la vista di configurazione dell&#39;estensione. Non possono completare l&#39;installazione dell&#39;estensione senza completare la configurazione dell&#39;estensione.

La configurazione dell’estensione è costituita da un componente vista che esporta le impostazioni che vengono quindi emesse all’interno della libreria di runtime di tag come oggetto normale.

[Per saperne di più](./configuration.md)

## Struttura delle estensioni

Un’estensione è costituita da una directory di file. Di seguito viene fornita una panoramica della struttura di questi file. Il contenuto dei file è trattato in altre sezioni.

Nella directory principale deve esistere un file [`extension.json`](./manifest.md). Questo file descriverà, tra le altre cose, la composizione dell’estensione e la collocazione di alcuni file all’interno della directory. Per alcuni aspetti, è simile al file [`package.json`](https://docs.npmjs.com/files/package.json) in [npm](https://www.npmjs.com/).

Ogni modulo di libreria (la logica da emettere all&#39;interno della libreria di runtime di tag) deve essere un proprio file il cui contenuto segue lo [standard del modulo CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1.1). Ad esempio, se si deve creare un tipo di azione “send beacon”, è necessario un file contenente la logica per l’invio del beacon. Il contenuto di questo file verrà emesso all’interno della libreria di runtime di tag. Puoi denominarlo `sendBeacon.js`. La posizione del file nella directory non è importante, in quanto è già descritta in `extension.json`.

Ogni visualizzazione deve essere un file HTML in grado di essere caricato in un iframe all&#39;interno dell&#39;applicazione tags. Per comunicare con l’applicazione, la visualizzazione deve includere uno script fornito dai tag e conforme a una piccola API. Non sono previste restrizioni per le modalità di utilizzo delle librerie nelle viste. In altre parole, puoi utilizzare jQuery, Sottolineatura, React, Angular, Bootstrap o altre librerie. Tuttavia, è consigliabile che l’aspetto dell’estensione sia simile a quello dell’applicazione.

Si consiglia di inserire tutti i file relativi alla vista (HTML, CSS, JavaScript) in una singola sottodirectory, isolata dai file del modulo libreria. In `extension.json` si dovrà descrivere la posizione di questa sottodirectory della vista. Platform distribuirà quindi questa sottodirectory (e solo questa sottodirectory) dai propri server web.
