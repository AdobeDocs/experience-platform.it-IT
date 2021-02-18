---
title: Installare Adobe Experience Platform Web SDK
description: Scoprite come installare l’SDK Web  Experience Platform.
keywords: installazione web sdk;installazione web sdk;internet explorer;promessa;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 2%

---


# Installare l&#39;SDK {#installing-the-sdk}

Il modo migliore per utilizzare Adobe Experience Platform Web SDK è tramite [ Adobe Experience Platform Launch](http://launch.adobe.com/it). Cercare `AEP Web SDK` nel catalogo delle estensioni, installare e configurare l&#39;estensione.

Adobe Experience Platform Web SDK è disponibile anche su una rete CDN da usare. È possibile fare riferimento a questo file o scaricarlo e ospitarlo nella propria infrastruttura. È disponibile in una versione ridotta e non minificata. La versione non limitata è utile per il debug.

Struttura URL: https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OR alloy.js per la versione non minificata.

Esempio:

* Ridotto: [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js)
* Non ridotto: [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js)

## Aggiunta del codice {#adding-the-code}

Il primo passaggio nell&#39;implementazione di Adobe Experience Platform [!DNL Web SDK] consiste nel copiare e incollare il seguente &quot;codice di base&quot; il più in alto possibile nel tag `<head>` del codice HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

Il codice di base crea una funzione globale denominata `alloy`. Utilizzate questa funzione per interagire con l&#39;SDK. Se si desidera assegnare un altro nome alla funzione globale, è possibile modificare il nome `alloy` nel modo seguente:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

In questo esempio, la funzione globale viene rinominata `mycustomname` invece di `alloy`.

>[!IMPORTANT]
>
>Per evitare potenziali problemi, utilizzare un nome contenente almeno un carattere che non sia una cifra e che non sia in conflitto con il nome di una proprietà già trovata in `window`.

Questo codice di base, oltre a creare una funzione globale, carica anche il codice aggiuntivo contenuto in un file esterno \(`alloy.js`\) ospitato su un server. Per impostazione predefinita, questo codice viene caricato in modo asincrono per consentire alla pagina Web di essere il più performante possibile. Questa è l&#39;implementazione consigliata.

## Supporto di Internet Explorer {#support-internet-explore}

Questo SDK fa uso delle promesse, che è un metodo per comunicare il completamento delle attività asincrone. L&#39;implementazione [Promise](https://developer.mozilla.org/it-IT/docs/Web/JavaScript/Reference/Global_Objects/Promise) utilizzata dall&#39;SDK è supportata in modo nativo da tutti i browser di destinazione tranne [!DNL Internet Explorer]. Per utilizzare l&#39;SDK su [!DNL Internet Explorer], è necessario disporre di un `window.Promise` [polifuso](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Per determinare se avete già `window.Promise` polivalato:

1. Apri il tuo sito Web in [!DNL Internet Explorer].
1. Aprite la console di debug del browser.
1. Digitare `window.Promise` nella console, quindi premere Invio.

Se viene visualizzato un elemento diverso da `undefined`, è probabile che si sia già riempiti in polivaletti `window.Promise`. Un altro modo per determinare se `window.Promise` è polivalente è caricare il sito Web dopo aver completato le istruzioni di installazione sopra riportate. Se l&#39;SDK genera un errore che indica qualcosa su una promessa, probabilmente non hai polivalito `window.Promise`.

Se hai stabilito che è necessario eseguire il polifugo `window.Promise`, includi il seguente tag script sopra il codice di base fornito in precedenza:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Questo carica uno script che verifica che `window.Promise` sia un&#39;implementazione Promise valida.

>[!NOTE]
>
>Se scegli di caricare un&#39;implementazione Promise diversa, assicurati che supporti `Promise.prototype.finally`.

## Caricamento del file JavaScript in modo sincrono {#loading-javascript-synchronously}

Come spiegato nella sezione [Aggiunta del codice](#adding-the-code), il codice di base copiato e incollato nell&#39;HTML del sito Web carica un file esterno con codice aggiuntivo. Questo codice aggiuntivo contiene le funzionalità di base dell’SDK. Qualsiasi comando che si tenta di eseguire durante il caricamento del file viene messo in coda e quindi elaborato dopo il caricamento del file. Questo è il metodo di installazione più performante.

In alcune circostanze, tuttavia, potrebbe essere utile caricare il file in modo sincrono \(ulteriori dettagli su queste circostanze verranno documentati più avanti\). In questo modo il resto del documento HTML non viene analizzato ed eseguito dal browser fino a quando il file esterno non viene caricato ed eseguito. Questo ritardo aggiuntivo prima della visualizzazione del contenuto principale agli utenti è generalmente scoraggiato, ma può avere senso a seconda delle circostanze.

Per caricare il file in modo sincrono invece che asincrono, rimuovete l&#39;attributo `async` dal secondo tag `script` come illustrato di seguito:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js"></script>
```
