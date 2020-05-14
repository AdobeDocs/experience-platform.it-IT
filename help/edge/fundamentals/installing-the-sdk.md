---
title: Installazione di Adobe Experience Platform Web SDK
seo-title: SDK Web per Adobe Experience Platform per l'installazione dell'SDK
description: Scopri come installare l’SDK Web per la piattaforma Experience
seo-description: Scopri come installare l’SDK Web per la piattaforma Experience
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 2%

---


# Installazione dell’SDK

Il primo passo per implementare l’SDK per Adobe Experience Platform Web è copiare e incollare il seguente &quot;codice di base&quot; il più possibile nel `<head>` tag del codice HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js" async></script>
```

Il codice di base crea una funzione globale denominata `alloy`. Utilizzate questa funzione per interagire con l&#39;SDK. Se si desidera assegnare un altro nome alla funzione globale, è possibile modificare il `alloy` nome nel modo seguente:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="alloy.js" async></script>
```

In questo esempio, la funzione globale viene rinominata `mycustomname`, anziché `alloy`.

>[!IMPORTANT]
>Per evitare potenziali problemi, utilizzare un nome contenente almeno un carattere che non sia una cifra e che non sia in conflitto con il nome di una proprietà già trovata in `window`.

Questo codice di base, oltre a creare una funzione globale, carica anche il codice aggiuntivo contenuto all&#39;interno di un file esterno \(`alloy.js`\) ospitato su un server. Per impostazione predefinita, questo codice viene caricato in modo asincrono per consentire alla pagina Web di essere il più performante possibile. Questa è l&#39;implementazione consigliata.

## Supporto di Internet Explorer

Questo SDK fa uso delle promesse, che è un metodo per comunicare il completamento delle attività asincrone. L’implementazione [Promise](https://developer.mozilla.org/it-IT/docs/Web/JavaScript/Reference/Global_Objects/Promise) utilizzata dall’SDK è supportata in modo nativo da tutti i browser di destinazione eccetto Internet Explorer. Per utilizzare l’SDK in Internet Explorer, è necessario disporre di un `window.Promise` riempimento [polivalente](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Per determinare se è già presente un `window.Promise` polivaletto:

1. Aprite il sito Web in Internet Explorer.
1. Aprite la console di debug del browser.
1. Digitate `window.Promise` la console, quindi premete Invio.

Se `undefined` appare qualcosa di diverso da quello, probabilmente avete già polilizzato `window.Promise`. Un altro modo per determinare se `window.Promise` è polivalente è caricare il sito Web dopo aver completato le istruzioni di installazione di cui sopra. Se l’SDK genera un errore che indica qualcosa di una promessa, probabilmente non hai ripieno `window.Promise`.

Se avete stabilito che è necessario eseguire il polifugo `window.Promise`, includete il seguente tag script sopra il codice di base fornito in precedenza:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Questo carica uno script che verifica che `window.Promise` sia un&#39;implementazione Promise valida.

## Caricamento sincrono del file JavaScript

Come spiegato in precedenza, il codice di base copiato e incollato nell’HTML del sito Web carica un file esterno con codice aggiuntivo. Questo codice aggiuntivo contiene le funzionalità di base dell’SDK. Qualsiasi comando che si tenta di eseguire durante il caricamento del file viene messo in coda e quindi elaborato dopo il caricamento del file. Questo è il metodo di installazione più performante.

In alcune circostanze, tuttavia, potrebbe essere utile caricare il file in modo sincrono \(ulteriori dettagli su queste circostanze verranno documentati più avanti\). In questo modo il resto del documento HTML non viene analizzato ed eseguito dal browser fino a quando il file esterno non viene caricato ed eseguito. Questo ritardo aggiuntivo prima della visualizzazione del contenuto principale agli utenti è generalmente scoraggiato, ma può avere senso a seconda delle circostanze.

Per caricare il file in modo sincrono invece che asincrono, rimuovete l’ `async` attributo dal secondo `script` tag come mostrato di seguito:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js"></script>
```
