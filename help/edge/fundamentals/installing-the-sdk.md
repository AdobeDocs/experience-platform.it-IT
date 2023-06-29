---
title: Installare Adobe Experience Platform Web SDK
description: Scopri come installare Experience Platform Web SDK.
keywords: installazione web sdk;installazione web sdk;internet explorer;promise;npm package
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 2%

---

# Installare l’SDK {#installing-the-sdk}

Sono disponibili tre modi supportati per utilizzare Adobe Experience Platform Web SDK:

1. Il modo migliore per utilizzare Adobe Experience Platform Web SDK è tramite l’interfaccia utente di Data Collection o l’interfaccia utente di Experience Platform.
1. Adobe Experience Platform Web SDK è disponibile anche su una rete CDN (Content Delivery Network).
1. Utilizza la libreria NPM che esporta i moduli EcmaScript 5 ed EcmaScript 2015 (ES6).

## Opzione 1: installazione dell’estensione tag

Per la documentazione sull’estensione tag, consulta [Documentazione sui tag](../../tags/extensions/client/web-sdk/overview.md)

## Opzione 2: installazione della versione standalone precompilata

La versione predefinita è disponibile su una rete CDN. Puoi fare riferimento alla libreria sulla rete CDN direttamente sulla tua pagina, oppure scaricarla e ospitarla sulla tua infrastruttura. È disponibile in formati minimizzati e non minimizzati. La versione non minimizzata è utile a scopo di debug.

Struttura URL: https://cdn1.adoberesources.net/alloy/[VERSIONE]/alloy.min.js OR alloy.js per la versione non minimizzata.

Ad esempio:


* Minimizzato: [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js)
* Non minimizzato: [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js)


### Aggiunta del codice {#adding-the-code}

La versione standalone precompilata richiede l’aggiunta di un &quot;codice di base&quot; direttamente alla pagina. Copia e incolla il seguente &quot;codice di base&quot; il più in alto possibile nel `<head>` tag del HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

Il &quot;codice di base&quot; crea una funzione globale denominata `alloy`. Utilizza questa funzione per interagire con l’SDK. Se si desidera assegnare un altro nome alla funzione globale, modificare il `alloy` nome come segue:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

In questo esempio, la funzione globale viene rinominata `mycustomname`, invece di `alloy`.

>[!IMPORTANT]
>
>Per evitare potenziali problemi, utilizza un nome contenente almeno un carattere che non sia una cifra e che non sia in conflitto con il nome di una proprietà già trovata in `window`.

Questo codice di base, oltre a creare una funzione globale, carica anche il codice aggiuntivo contenuto in un file esterno \(`alloy.js`\) ospitato su un server. Per impostazione predefinita, questo codice viene caricato in modo asincrono per consentire alla pagina Web di ottenere le massime prestazioni possibili. Questa è l’implementazione consigliata.

### Supporto di Internet Explorer {#support-internet-explore}

Questo SDK utilizza le promesse, un metodo per comunicare il completamento di attività asincrone. Il [Promessa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) L&#39;implementazione utilizzata dall&#39;SDK è supportata in modalità nativa da tutti i browser di destinazione eccetto [!DNL Internet Explorer]. Per utilizzare l’SDK su [!DNL Internet Explorer], devi avere `window.Promise` [poleriempito](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Per determinare se si dispone già di `window.Promise` poleriempito:

1. Apri il sito web in [!DNL Internet Explorer].
1. Apri la console di debug del browser.
1. Tipo `window.Promise` nella console, quindi premere Invio.

Se qualcosa di diverso da `undefined` è probabile che sia già stato eseguito il polyfill `window.Promise`. Un altro modo per determinare se `window.Promise` è polyfill è caricando il tuo sito web dopo aver completato le istruzioni di installazione di cui sopra. Se l’SDK genera un errore nel menzionare qualcosa su una promessa, probabilmente non sei stato polilemizzato `window.Promise`.

Se hai stabilito che devi riempire il computer `window.Promise`, includi il seguente tag script sopra il codice di base fornito in precedenza:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Questo tag carica uno script che assicura che `window.Promise` è un’implementazione Promise valida.

>[!NOTE]
>
>Se scegli di caricare un’implementazione Promise diversa, assicurati che supporti `Promise.prototype.finally`.

### Caricamento del file JavaScript in modo sincrono {#loading-javascript-synchronously}

Come spiegato nella sezione [Aggiunta del codice](#adding-the-code), il codice di base copiato e incollato nel HTML del sito web carica un file esterno. Il file esterno contiene le funzionalità principali dell’SDK. Qualsiasi comando che si tenta di eseguire durante il caricamento del file viene messo in coda e quindi elaborato dopo il caricamento del file. Il caricamento del file in modo asincrono è il metodo di installazione più performante.

In determinate circostanze, tuttavia, potrebbe essere utile caricare il file in modo sincrono \(ulteriori dettagli su queste circostanze verranno documentati in seguito\). In questo modo si impedisce al resto del documento HTML di essere analizzato e renderizzato dal browser fino a quando il file esterno non viene caricato ed eseguito. Questo ritardo aggiuntivo prima di visualizzare il contenuto principale agli utenti è in genere sconsigliato, ma può essere utile a seconda delle circostanze.

Per caricare il file in modo sincrono anziché asincrono, rimuovere `async` attributo dal secondo `script` come mostrato di seguito:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>
```

## Opzione 3: utilizzo del pacchetto NPM

Adobe Experience Platform Web SDK è disponibile anche come pacchetto NPM. [NPM](https://www.npmjs.com) è il gestore di pacchetti per JavaScript. L’installazione del pacchetto NPM consente di avere il controllo del processo di build per il JavaScript di Adobe Experience Platform Web SDK. Il pacchetto NPM espone i moduli EcmaScript versione 5 o EcmaScript versione 2015 (ES6) destinati a essere eseguiti nel browser.

```bash
npm install @adobe/alloy
```

Il pacchetto NPM di Adobe Experience Platform Web SDK espone un `createInstance` funzione. Questa funzione viene utilizzata per creare un’istanza. L’opzione name passata alla funzione controlla il prefisso utilizzato nella registrazione. Di seguito sono riportati alcuni esempi di utilizzo del pacchetto.

### Utilizzo del pacchetto come modulo ECMAScript 2015 (ES6)

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Il pacchetto NPM si basa sui moduli CommonJS; pertanto, quando utilizzi un bundler, assicurati che il bundler supporti i moduli CommonJS. Alcuni bundle, come [Rollup](https://rollupjs.org), richiedono un [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) che fornisce supporto per CommonJS.

### Utilizzo del pacchetto come modulo ECMAScript 5

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Supporto di Internet Explorer

L’SDK di Adobe Experience Platform utilizza le promesse, un metodo per comunicare il completamento di attività asincrone. Il [Promessa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) L&#39;implementazione utilizzata dall&#39;SDK è supportata in modalità nativa da tutti i browser di destinazione eccetto [!DNL Internet Explorer]. Per utilizzare l’SDK su [!DNL Internet Explorer], devi avere `window.Promise` [poleriempito](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Una libreria che potresti utilizzare per il polyfill della promessa è promise-polyfill. Consulta la [documentazione promise-polyfill](https://www.npmjs.com/package/promise-polyfill) per ulteriori informazioni su come eseguire l&#39;installazione con NPM.

>[!NOTE]
>
>Se scegli di caricare un’implementazione Promise diversa, assicurati che supporti `Promise.prototype.finally`.
