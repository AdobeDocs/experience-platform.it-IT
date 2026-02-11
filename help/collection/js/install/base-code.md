---
title: Codice base
description: Comandi di coda (bootstrap) durante il caricamento asincrono della libreria di raccolta dati.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Codice base

Il codice di base consente l&#39;avvio automatico accodando i comandi mentre Adobe Experience Platform Web SDK viene caricato in modo asincrono. Dopo l&#39;esecuzione del codice di base, è possibile chiamare immediatamente qualsiasi comando come [`configure`](../commands/configure/overview.md) o [`sendEvent`](../commands/sendevent/overview.md) senza preoccuparsi delle race condition o della tempistica della libreria al termine del caricamento. Al termine del caricamento del Web SDK, i comandi in coda vengono eseguiti in ordine di primo ingresso e primo uscita (nello stesso ordine in cui erano in coda).

I comandi restituiscono promesse, anche quando sono in coda. Se un comando è in coda, la promessa viene risolta o rifiutata dopo l&#39;esecuzione del comando al termine del caricamento del Web SDK. Se il caricamento del Web SDK non viene mai completato (ad esempio, se la libreria non viene caricata), le promesse in coda rimangono in sospeso.

## Aggiungi il codice di base

Inserire il codice di base il più in alto possibile nel tag `<head>`, prima di qualsiasi script che potrebbe chiamare il Web SDK.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Dopo aver aggiunto il codice di base, caricare il Web SDK utilizzando il metodo scelto ([Caricatore libreria JavaScript](library.md) o [Codice di incorporamento tag](/help/tags/extensions/client/web-sdk/getting-started.md)). Per le implementazioni basate su tag, il codice di base è supportato nell’estensione tag Web SDK 2.34.0 e versioni successive.

Questo codice di base è **not** richiesto nei seguenti scenari:

* Se carichi la libreria JavaScript in modo sincrono. Il caricamento sincrono blocca l’analisi durante il recupero e l’esecuzione della libreria.
* Se utilizzi l’estensione tag, tutte le chiamate al Web SDK vengono effettuate all’interno di regole o azioni tag. Devi includere il codice di base solo se l’implementazione fa riferimento al SDK web all’esterno della libreria di tag. La maggior parte delle implementazioni di tag in genere non chiama il Web SDK all’esterno della libreria di tag, pertanto la maggior parte delle implementazioni di tag non richiede il codice di base.

## Esempi

Vedere i commenti all&#39;interno di questo esempio di codice per informazioni sui tempi di accodamento e risoluzione dei comandi. Questo esempio si applica sia alla libreria JavaScript che all’estensione tag:

```html
<head>
  <script>
    // Calls made before the base code runs are not captured (alloy is not yet defined).
    // Always make sure that the base code runs before any attempt to call commands.
    // alloy("getLibraryInfo").then(console.log).catch(console.error);
  </script>

  <!-- Base code -->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!-- Queued command -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Queued call resolved:", result);
    }).catch(console.error);
  </script>

  <!-- Load the Web SDK using the JavaScript loader -->
  <script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
  <!-- or the tag extension -->
  <!-- <script src=".../launch-<ENV>.min.js" async></script> -->

  <!-- Another call (queued if the library is still loading; immediate if it is ready) -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Immediate call resolved:", result);
    }).catch(console.error);
  </script>
</head>
```

## Rinomina istanza SDK

È possibile rinominare la funzione globale richiamata modificando l&#39;ultima riga del codice di base. Modifica:

```js
(window,["alloy"]);
```

A:

```js
(window,["ingot"]);
```

Questa modifica consente di chiamare i comandi utilizzando `ingot` anziché `alloy`:

```js
ingot("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

## Più istanze SDK

Facoltativamente, puoi utilizzare il codice di base per configurare più istanze di SDK in una pagina. Per ulteriori informazioni, vedere [Utilizzare più istanze di Web SDK](../../use-cases/multiple-instances.md).
