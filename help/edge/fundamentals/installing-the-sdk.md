---
title: Installare Adobe Experience Platform Web SDK
description: Scopri come installare Experience Platform Web SDK.
keywords: installazione sdk web;installazione sdk web;internet explorer;promise;pacchetto npm
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: fccad34ad4ad028c7b34356dec7bb34892396317
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 2%

---

# Installa l&#39;SDK {#installing-the-sdk}

Sono disponibili tre modi supportati per utilizzare Adobe Experience Platform Web SDK:

1. Il modo migliore per utilizzare Adobe Experience Platform Web SDK è tramite [Adobe Experience Platform Launch](https://launch.adobe.com/).
1. Adobe Experience Platform Web SDK è disponibile anche su una rete CDN (Content Delivery Network) da usare.
1. Utilizzare la libreria NPM che esporta i moduli EcmaScript 5 ed EcmaScript 2015 (ES6).

## Opzione 1: Installazione dell’estensione Adobe Experience Platform Launch

Per la documentazione sull&#39;estensione Adobe Experience Platform Launch, consulta la [documentazione di avvio](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)

## Opzione 2: Installazione della versione autonoma predefinita

La versione precompilata è disponibile su una rete CDN. Puoi fare riferimento alla libreria sulla rete CDN direttamente sulla tua pagina, oppure scaricarla e ospitarla sulla tua infrastruttura. È disponibile in formati minimizzati e non minimizzati. La versione non minimizzata è utile a scopo di debug.

Struttura URL: https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OR alloy.js per la versione non minimizzata.

Esempio:


* Minimizzato: [https://cdn1.adoberesources.net/alloy/2.5.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.5.0/alloy.min.js)
* Non minimizzato: [https://cdn1.adoberesources.net/alloy/2.5.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.5.0/alloy.js)


### Aggiunta del codice {#adding-the-code}

La versione standalone predefinita richiede un &quot;codice base&quot; aggiunto direttamente alla pagina. Copia e incolla il seguente &quot;codice base&quot; il più in alto possibile nel tag `<head>` del codice HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.5.0/alloy.min.js" async></script>
```

Il &quot;codice base&quot; crea una funzione globale denominata `alloy`. Usa questa funzione per interagire con l&#39;SDK. Per assegnare alla funzione globale un nome diverso, modificare il nome `alloy` come segue:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.5.0/alloy.min.js" async></script>
```

In questo esempio, la funzione globale viene rinominata `mycustomname` anziché `alloy`.

>[!IMPORTANT]
>
>Per evitare potenziali problemi, utilizza un nome contenente almeno un carattere che non è una cifra e che non è in conflitto con il nome di una proprietà già trovata in `window`.

Questo codice base, oltre a creare una funzione globale, carica anche il codice aggiuntivo contenuto all&#39;interno di un file esterno \(`alloy.js`\) ospitato su un server. Per impostazione predefinita, questo codice viene caricato in modo asincrono per consentire alla pagina web di essere il più performante possibile. Questa è l’implementazione consigliata.

### Supporto di Internet Explorer {#support-internet-explore}

Questo SDK utilizza le promesse, un metodo per comunicare il completamento delle attività asincrone. L’implementazione [Promise](https://developer.mozilla.org/it-IT/docs/Web/JavaScript/Reference/Global_Objects/Promise) utilizzata dall’SDK è supportata in modo nativo da tutti i browser di destinazione eccetto [!DNL Internet Explorer]. Per utilizzare l&#39;SDK su [!DNL Internet Explorer], è necessario disporre di `window.Promise` [polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Per determinare se hai già un `window.Promise` polyfill:

1. Apri il tuo sito web in [!DNL Internet Explorer].
1. Apri la console di debug del browser.
1. Digita `window.Promise` nella console, quindi premi Invio.

Se viene visualizzato un elemento diverso da `undefined`, è probabile che sia già stato riempito in poliestere `window.Promise`. Un altro modo per determinare se `window.Promise` è polifuso è caricare il tuo sito web dopo aver completato le istruzioni di installazione di cui sopra. Se l&#39;SDK genera un errore che indica qualcosa su una promessa, è probabile che non si sia riempita in poliestere `window.Promise`.

Se hai determinato di dover eseguire il polyfill `window.Promise`, includi il seguente tag script sopra il codice base fornito in precedenza:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Questo tag carica uno script che assicura che `window.Promise` sia un’implementazione Promise valida.

>[!NOTE]
>
>Se scegli di caricare un’implementazione Promise diversa, assicurati che supporti `Promise.prototype.finally`.

### Caricamento del file JavaScript in modo sincrono {#loading-javascript-synchronously}

Come spiegato nella sezione [Aggiunta del codice](#adding-the-code), il codice di base copiato e incollato nell&#39;HTML del sito web carica un file esterno. Il file esterno contiene le funzionalità di base dell&#39;SDK. Qualsiasi comando che si tenta di eseguire durante il caricamento del file viene messo in coda e quindi elaborato dopo il caricamento del file. Il caricamento asincrono del file rappresenta il metodo di installazione più performante.

In alcune circostanze, tuttavia, potrebbe essere utile caricare il file in modo sincrono \ (ulteriori dettagli su queste circostanze saranno documentati più avanti\). In questo modo il resto del documento HTML non viene analizzato ed eseguito dal browser fino a quando il file esterno non viene caricato ed eseguito. Questo ritardo aggiuntivo prima di visualizzare il contenuto principale agli utenti è in genere scoraggiato, ma può avere senso a seconda delle circostanze.

Per caricare il file in modo sincrono anziché in modo asincrono, rimuovi l’attributo `async` dal secondo tag `script` come mostrato di seguito:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.5.0/alloy.min.js"></script>
```

## Opzione 3: Utilizzo del pacchetto NPM

Adobe Experience Platform Web SDK è disponibile anche come pacchetto NPM. [](https://www.npmjs.com) NPMè il gestore di pacchetti per JavaScript. L&#39;installazione del pacchetto NPM ti consente di avere il controllo del processo di creazione per il JavaScript Adobe Experience Platform Web SDK. Il pacchetto NPM espone i moduli EcmaScript versione 5 o EcmaScript versione 2015 (ES6) destinati ad essere eseguiti nel browser.

```bash
npm install @adobe/alloy
```

Il pacchetto NPM di Adobe Experience Platform Web SDK espone una funzione `createInstance` . Questa funzione viene utilizzata per creare un&#39;istanza. L&#39;opzione nome passata alla funzione controlla il prefisso utilizzato nella registrazione. Di seguito sono riportati alcuni esempi di utilizzo del pacchetto.

### Utilizzo del pacchetto come modulo ECMAScript 2015 (ES6)

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Il pacchetto NPM si basa su moduli CommonJS; pertanto, quando utilizzi un bundler, assicurati che il bundler supporti i moduli CommonJS. Alcuni bundler, come [Rollup](https://rollupjs.org), richiedono un [plug-in](https://www.npmjs.com/package/@rollup/plugin-commonjs) che fornisca il supporto CommonJS.

### Utilizzo del pacchetto come modulo ECMAScript 5

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Supporto di Internet Explorer

L’SDK di Adobe Experience Platform utilizza le promesse, che sono un metodo per comunicare il completamento delle attività asincrone. L’implementazione [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) utilizzata dall’SDK è supportata in modo nativo da tutti i browser di destinazione eccetto [!DNL Internet Explorer]. Per utilizzare l&#39;SDK su [!DNL Internet Explorer], è necessario disporre di `window.Promise` [polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Una libreria che si può utilizzare per promessa di polyfill è promise-polyfill. Per ulteriori informazioni su come installare con NPM, consulta la [documentazione promise-polyfill](https://www.npmjs.com/package/promise-polyfill) .

>[!NOTE]
>
>Se scegli di caricare un’implementazione Promise diversa, assicurati che supporti `Promise.prototype.finally`.
