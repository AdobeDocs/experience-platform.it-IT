---
title: Implementazione di librerie di terze parti
description: Scopri i diversi metodi di hosting delle librerie di terze parti all’interno delle estensioni di tag Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 69%

---

# Implementazione di librerie di terze parti

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Uno degli scopi principali delle estensioni di tag in Adobe Experience Platform è quello di consentire di implementare facilmente le tecnologie di marketing esistenti (librerie) nel sito web. Utilizzando le estensioni, è possibile implementare le librerie fornite da reti CDN (content delivery network) di terze parti senza dover modificare manualmente il codice HTML del sito web.

Esistono diversi metodi per ospitare librerie di terze parti (fornitori) all’interno delle estensioni. Questo documento fornisce una panoramica di questi diversi metodi di implementazione, inclusi i pro e i contro di ciascuno.

## Prerequisiti 

Questo documento richiede una comprensione efficace delle estensioni all’interno dei tag, incluse le operazioni che possono eseguire e la loro composizione. Per ulteriori informazioni, consulta la [panoramica sullo sviluppo delle estensioni](./overview.md).

## Processo di caricamento del codice di base

Al di fuori del contesto dei tag, è importante comprendere in che modo le tecnologie di marketing generalmente si caricano su un sito web. I fornitori di librerie di terze parti distribuiscono uno snippet di codice (o codice di base) che deve essere incorporato nell’HTML del sito web per caricare le funzionalità della libreria.

In generale, il codice di base per le tecnologie di marketing esegue alcune varianti del seguente processo durante il caricamento sul sito:

1. Configura una funzione globale che possa essere utilizzata per interagire con la libreria del fornitore.
1. Carica la libreria del fornitore.
1. Effettua una serie di chiamate iniziali in coda alla funzione globale, a scopo di configurazione e tracciamento.

Una volta impostata la funzione globale, è possibile effettuare chiamate alla funzione anche prima che sia terminato il caricamento della libreria. Tutte le chiamate effettuate vengono aggiunte al meccanismo di accodamento del codice di base e vengono quindi eseguite in ordine sequenziale una volta caricata la libreria.

Al termine del caricamento della libreria, la funzione globale viene sostituita con una nuova che aggira la coda ed elabora immediatamente eventuali chiamate future alla funzione.

### Esempio di codice di base

Il seguente JavaScript è un esempio di codice di base non minimizzato per il [tag di conversione Pinterest](https://developers.pinterest.com/docs/ad-tools/conversion-tag/?), a cui verrà fatto riferimento in seguito in questo documento per dimostrare come il codice di base sia adattato per diverse strategie di implementazione con tag:

```js
!function(scriptUrl) {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = '3.0';
    var scriptElement = document.createElement('script');
    scriptElement.async = true;
    scriptElement.src = scriptUrl;
    var firstScriptElement = 
      document.getElementsByTagName('script')[0];
    firstScriptElement.parentNode.insertBefore(
      scriptElement, firstScriptElement
    );
  }
}('https://s.pinimg.com/ct/core.js');
pintrk('load', 'YOUR_TAG_ID');
pintrk('page');
```

In sintesi, il codice di base riportato sopra fornisce un’[espressione di funzione immediatamente richiamata (IIFE)](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) che crea una funzione globale per l’interazione con la libreria (`window.pintrk`). Inoltre, assegna a una variabile `scriptURL` il valore `https://s.pinimg.com/ct/core.js`, che corrisponde al percorso in cui si trova la libreria. Come spiegato in precedenza, tutte le funzioni richiamate prima del caricamento della libreria vengono inserite in una coda (`window.pintrk.queue`) che verrà eseguita in sequenza una volta che la libreria è disponibile.

La parte seguente del codice di base è la più importante per comprendere in che modo la libreria viene caricata sul sito:

```js
var scriptElement = document.createElement("script");
scriptElement.async = true;
scriptElement.src = scriptUrl;
var firstScriptElement = 
  document.getElementsByTagName("script")[0];
firstScriptElement.parentNode.insertBefore(
  scriptElement, firstScriptElement
);
```

Il codice di base crea un elemento script, lo imposta in modo da caricarlo in modo asincrono e imposta l’URL `src` su `https://s.pinimg.com/ct/core.js`. Quindi aggiunge l’elemento script al documento inserendolo prima del primo elemento script già presente nel documento.

## Opzioni di implementazione dei tag

Le sezioni seguenti illustrano i diversi modi in cui è possibile caricare le librerie dei fornitori nelle estensioni, utilizzando il codice di base Pinterest illustrato in precedenza come esempio. Ognuno di questi esempi comporta la creazione di un [tipo di azione per un&#39;estensione Web](./web/action-types.md) che carica la libreria sul tuo sito web.

>[!NOTE]
>
>Mentre gli esempi seguenti utilizzano tipi di azioni a scopo dimostrativo, puoi applicare gli stessi principi a qualsiasi funzione che carica la libreria di tag sul tuo sito.


Sono contemplati i seguenti metodi:

- [Implementazione di librerie di terze parti](#implementing-third-party-libraries)
   - [Prerequisiti ](#prerequisites)
   - [Processo di caricamento del codice di base](#base-code-loading-process)
      - [Esempio di codice di base](#base-code-example)
   - [Opzioni di implementazione dei tag](#tags-implementation-options)
      - [Caricare in fase di runtime dall’host del fornitore {#vendor-host}](#load-at-runtime-from-the-vendor-host-vendor-host)
      - [Carica in fase di runtime dall’host della libreria di tag](#load-at-runtime-from-the-tag-library-host)
      - [Incorporare direttamente la libreria](#embed-the-library-directly)
   - [Passaggi successivi](#next-steps)

### Caricare in fase di runtime dall’host del fornitore {#vendor-host}

Il metodo più comune per l’hosting della libreria fornitore consiste nell’utilizzare la CDN del fornitore. Poiché il codice di base per la maggior parte delle librerie è già configurato per caricare la libreria dal CDN del fornitore, si può impostare l’estensione per caricare la libreria dalla stessa posizione.

Questo approccio è solitamente il più semplice da mantenere, in quanto eventuali aggiornamenti apportati al file sulla rete CDN verranno caricati automaticamente dall&#39;estensione.

Quando si utilizza questo metodo, è sufficiente incollare l’intero codice di base direttamente in un tipo di azione, come segue:

```js
module.exports = function() {
  !function(scriptUrl) {
    if (!window.pintrk) {
      window.pintrk = function() {
        window.pintrk.queue.push(
          Array.prototype.slice.call(arguments)
        );
      };
      window.pintrk.queue = []; 
      window.pintrk.version = "3.0";
      var scriptElement = document.createElement("script");
      scriptElement.async = true;
      scriptElement.src = scriptUrl;
      var firstScriptElement = 
        document.getElementsByTagName("script")[0];
      firstScriptElement.parentNode.insertBefore(
        scriptElement, firstScriptElement
      );
    }
  }("https://s.pinimg.com/ct/core.js");
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

Facoltativamente, si possono intraprendere ulteriori passi per ridefinire l’implementazione. Poiché le variabili `scriptElement` e `firstScriptElement` sono ora incluse nell’ambito della funzione esportata, è possibile rimuovere l’IIFE poiché non corrono il rischio di diventare globali.

Inoltre, i tag forniscono diversi [moduli principali](./web/core.md) che sono utility utilizzabili da qualsiasi estensione. Nello specifico, il modulo `@adobe/reactor-load-script` carica uno script da una posizione remota creando un elemento script e aggiungendolo al documento. Utilizzando questo modulo per il processo di caricamento dello script, è possibile ridefinire ulteriormente il codice dell’azione:

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = 'https://s.pinimg.com/ct/core.js';
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

### Carica in fase di runtime dall’host della libreria di tag

L’utilizzo di una rete CDN di un fornitore per l’hosting di librerie comporta diversi potenziali rischi: errori o mancata disponibilità della rete CDN, aggiornamento del file per correggere eventuali bug critici, o compromissione del file da parte di una minaccia.

Per evitare questi problemi, puoi includere la libreria del fornitore come file separato all’interno dell’estensione. L&#39;estensione può quindi essere configurata in modo che il file sia ospitato accanto alla libreria dei tag principale. In fase di runtime, l’estensione carica la libreria del fornitore dallo stesso server che ha inviato la libreria principale al sito web.

>[!IMPORTANT]
>
>In alcuni casi, la libreria del fornitore può caricare codice aggiuntivo da server di terze parti, come accade con la libreria del fornitore Pinterest. In questi casi, unendo in bundle la libreria del fornitore con la tua estensione potrebbe non alleviare completamente tutti i problemi relativi ai rischi.

Per implementare questa soluzione, devi innanzitutto scaricare la libreria del fornitore sul tuo computer. Nel caso di Pinterest, la libreria del fornitore si trova all’indirizzo [https://s.pinimg.com/ct/core.js](https://s.pinimg.com/ct/core.js). Dopo aver scaricato il file, devi inserirlo nel progetto dell’estensione. Nell’esempio seguente, il file è denominato `pinterest.js` e si trova nella cartella `vendor` all’interno della directory del progetto.

Una volta che il file della libreria è nel progetto, devi aggiornare il file manifesto dell&#39;estensione [a1/> (`extension.json`) per indicare che la libreria fornitore deve essere consegnata accanto alla libreria dei tag principale. ](./manifest.md) A questo scopo, devi aggiungere il percorso al file di libreria all’interno di un array `hostedLibFiles`:

```json
{
  "hostedLibFiles": ["vendor/pinterest.js"]
}
```

Infine, è necessario configurare il codice dell’azione per caricare la libreria del fornitore dallo stesso server che ospita la libreria principale. L’esempio seguente utilizza come punto di partenza il codice dell’azione creato nella [sezione precedente](#vendor-host). Utilizzando l’[oggetto turbine](./turbine.md), devi passare il nome file (senza percorso) del file del fornitore come segue:

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = turbine.getHostedLibFileUrl('pinterest.js');
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

È importante notare che quando utilizzi questo metodo, devi aggiornare manualmente il file fornitore scaricato ogni volta che la libreria viene aggiornata sul proprio CDN e rilasciare le modifiche a una nuova versione dell&#39;estensione.

### Incorporare direttamente la libreria

Puoi evitare di dover caricare completamente la libreria fornitore incorporando direttamente il codice della libreria nel codice dell&#39;azione stesso, rendendolo di fatto parte della libreria di tag principale. Questo metodo aumenta le dimensioni della libreria principale, ma evita la necessità di effettuare un’ulteriore richiesta HTTP per recuperare un file separato.

Utilizzando come punto di partenza il codice dell’azione creato nella [sezione precedente](#vendor-host), puoi sostituire la riga in cui lo script viene caricato con il contenuto dello script stesso:

```js
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    // Paste the full vendor library code here.
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

## Passaggi successivi

Questo documento fornisce una panoramica dei diversi metodi per l&#39;hosting di librerie di terze parti nelle estensioni dei tag. Gli esempi forniti sono incentrati sulle librerie; tuttavia le stesse tecniche possono essere applicate anche a qualsiasi codice possa essere utilizzato dall’estensione.

Per ulteriori informazioni sugli strumenti per la configurazione delle estensioni, sui tipi di azione, sul manifesto dell’estensione, sui moduli core e sull’oggetto turbine, consulta la relativa documentazione di cui trovi in collegamenti in questa guida.
