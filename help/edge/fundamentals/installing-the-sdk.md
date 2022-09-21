---
title: Installare Adobe Experience Platform Web SDK
description: Scopri come installare Experience Platform Web SDK.
keywords: installazione sdk web;installazione sdk web;internet explorer;promise;pacchetto npm
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 2%

---

# Installare l’SDK {#installing-the-sdk}

Sono disponibili tre modi supportati per utilizzare Adobe Experience Platform Web SDK:

1. Il modo migliore per utilizzare Adobe Experience Platform Web SDK è tramite l’interfaccia utente di raccolta dati o di Experience Platform.
1. Adobe Experience Platform Web SDK è disponibile anche su una rete CDN (Content Delivery Network) da usare.
1. Utilizzare la libreria NPM che esporta i moduli EcmaScript 5 ed EcmaScript 2015 (ES6).

## Opzione 1: Installazione dell’estensione tag

Per la documentazione sull’estensione tag, consulta la sezione [documentazione di launch](../../tags/extensions/web/sdk/overview.md)

## Opzione 2: Installazione della versione autonoma predefinita

La versione precompilata è disponibile su una rete CDN. Puoi fare riferimento alla libreria sulla rete CDN direttamente sulla tua pagina, oppure scaricarla e ospitarla sulla tua infrastruttura. È disponibile in formati minimizzati e non minimizzati. La versione non minimizzata è utile a scopo di debug.

Struttura URL: https://cdn1.adoberesources.net/alloy/[VERSIONE]/alloy.min.js OR alloy.js per la versione non minimizzata.

Esempio:


* Minimizzato: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* Non minimizzato: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)


### Aggiunta del codice {#adding-the-code}

La versione standalone predefinita richiede un &quot;codice base&quot; aggiunto direttamente alla pagina. Copia e incolla il seguente &quot;codice base&quot; il più in alto possibile nel `<head>` tag del HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

Il &quot;codice base&quot; crea una funzione globale denominata `alloy`. Usa questa funzione per interagire con l&#39;SDK. Se si desidera assegnare alla funzione globale un nome diverso, modificare la `alloy` nome:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

In questo esempio, la funzione globale viene rinominata `mycustomname`anziché `alloy`.

>[!IMPORTANT]
>
>Per evitare potenziali problemi, utilizza un nome contenente almeno un carattere che non è una cifra e che non è in conflitto con il nome di una proprietà già trovata in `window`.

Questo codice base, oltre a creare una funzione globale, carica anche il codice aggiuntivo contenuto all&#39;interno di un file esterno \(`alloy.js`\) ospitato su un server. Per impostazione predefinita, questo codice viene caricato in modo asincrono per consentire alla pagina web di essere il più performante possibile. Questa è l’implementazione consigliata.

### Supporto di Internet Explorer {#support-internet-explore}

Questo SDK utilizza le promesse, un metodo per comunicare il completamento delle attività asincrone. La [Promessa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) l&#39;implementazione utilizzata dall&#39;SDK è supportata in modo nativo da tutti i browser di destinazione, tranne [!DNL Internet Explorer]. Per utilizzare l&#39;SDK su [!DNL Internet Explorer], devi `window.Promise` [policarbonato](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Per determinare se sono già disponibili `window.Promise` poliriempito:

1. Apri il tuo sito web in [!DNL Internet Explorer].
1. Apri la console di debug del browser.
1. Tipo `window.Promise` nella console, quindi premere Invio.

Se qualcosa di diverso da `undefined` apparentemente, è probabile che tu abbia già policolfato `window.Promise`. Un altro modo per determinare se `window.Promise` è polifuso è caricando il tuo sito web dopo aver completato le istruzioni di installazione di cui sopra. Se l&#39;SDK genera un errore che indica qualcosa su una promessa, è probabile che non si sia riempita in policarbonato `window.Promise`.

Se hai stabilito che devi polyfill `window.Promise`, includi il seguente tag script sopra il codice base fornito in precedenza:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Questo tag carica uno script che assicura che `window.Promise` è un&#39;implementazione Promise valida.

>[!NOTE]
>
>Se scegli di caricare un’implementazione Promise diversa, assicurati che supporti `Promise.prototype.finally`.

### Caricamento del file JavaScript in modo sincrono {#loading-javascript-synchronously}

Come spiegato nella sezione [Aggiunta del codice](#adding-the-code), il codice di base copiato e incollato in HTML del sito web carica un file esterno. Il file esterno contiene le funzionalità di base dell&#39;SDK. Qualsiasi comando che si tenta di eseguire durante il caricamento del file viene messo in coda e quindi elaborato dopo il caricamento del file. Il caricamento asincrono del file rappresenta il metodo di installazione più performante.

In alcune circostanze, tuttavia, potrebbe essere utile caricare il file in modo sincrono \ (ulteriori dettagli su queste circostanze saranno documentati più avanti\). In questo modo il resto del documento HTML non viene analizzato ed eseguito dal browser fino a quando il file esterno non viene caricato ed eseguito. Questo ritardo aggiuntivo prima di visualizzare il contenuto principale agli utenti è in genere scoraggiato, ma può avere senso a seconda delle circostanze.

Per caricare il file in modo sincrono anziché in modo asincrono, rimuovi il `async` attributo dal secondo `script` come mostrato di seguito:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js"></script>
```

## Opzione 3: Utilizzo del pacchetto NPM

Adobe Experience Platform Web SDK è disponibile anche come pacchetto NPM. [NPM](https://www.npmjs.com) è il gestore di pacchetti per JavaScript. L&#39;installazione del pacchetto NPM ti consente di avere il controllo del processo di creazione per il JavaScript Adobe Experience Platform Web SDK. Il pacchetto NPM espone i moduli EcmaScript versione 5 o EcmaScript versione 2015 (ES6) destinati ad essere eseguiti nel browser.

```bash
npm install @adobe/alloy
```

Il pacchetto NPM dell&#39;SDK Web di Adobe Experience Platform espone un `createInstance` funzione . Questa funzione viene utilizzata per creare un&#39;istanza. L&#39;opzione nome passata alla funzione controlla il prefisso utilizzato nella registrazione. Di seguito sono riportati alcuni esempi di utilizzo del pacchetto.

### Utilizzo del pacchetto come modulo ECMAScript 2015 (ES6)

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Il pacchetto NPM si basa su moduli CommonJS; pertanto, quando utilizzi un bundler, assicurati che il bundler supporti i moduli CommonJS. Alcuni bundle, come [Rollup](https://rollupjs.org), richiedono un [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) che fornisce supporto CommonJS.

### Utilizzo del pacchetto come modulo ECMAScript 5

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Supporto di Internet Explorer

L’SDK di Adobe Experience Platform utilizza le promesse, che sono un metodo per comunicare il completamento delle attività asincrone. La [Promessa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) l&#39;implementazione utilizzata dall&#39;SDK è supportata in modo nativo da tutti i browser di destinazione, tranne [!DNL Internet Explorer]. Per utilizzare l&#39;SDK su [!DNL Internet Explorer], devi `window.Promise` [policarbonato](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Una libreria che si può utilizzare per promessa di polyfill è promise-polyfill. Consulta la sezione [documentazione di promise-polyfill](https://www.npmjs.com/package/promise-polyfill) per ulteriori informazioni su come installare con NPM.

>[!NOTE]
>
>Se scegli di caricare un’implementazione Promise diversa, assicurati che supporti `Promise.prototype.finally`.
