---
title: Gestione di Flicker per esperienze personalizzate
seo-title: ' Adobe Experience Platform Web SDK gestione dello sfarfallio'
description: Scopri come gestire lo sfarfallio sulle esperienze utente
seo-description: 'Scopri come gestire lo sfarfallio con le proprietà SDK Web del Experience Platform '
translation-type: tm+mt
source-git-commit: 4bea14d18ce119bdec0d428f885d240f92244cfc
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# Gestione dello sfarfallio

Quando si tenta di eseguire il rendering del contenuto di personalizzazione, l’SDK deve assicurarsi che non vi siano sfarfallii. Flicker, detto anche FOOC (Flash di contenuti originali), è quando un contenuto originale viene visualizzato brevemente prima che l’alternativa venga visualizzata durante il test/la personalizzazione. L’SDK tenta di applicare stili CSS agli elementi della pagina per assicurarsi che tali elementi siano nascosti finché il rendering del contenuto di personalizzazione non viene eseguito correttamente.

La funzionalità di gestione dello sfarfallio prevede alcune fasi:

1. Verifica preliminare
1. Pre-elaborazione
1. Rendering

## Verifica preliminare

Durante la fase di predisattivazione, l’SDK utilizza l’opzione di `prehidingStyle` configurazione per creare un tag di stile HTML e aggiungerlo al DOM per assicurarsi che parti grandi della pagina siano nascoste. Se non sei sicuro di quali parti della pagina saranno personalizzate, si consiglia di impostare `prehidingStyle` su `body { opacity: 0 !important }`. In questo modo l’intera pagina viene nascosta. Questo, tuttavia, comporta un peggioramento delle prestazioni di rendering della pagina segnalate da strumenti come Lighthouse, Web Page Test, ecc. Per ottenere le migliori prestazioni di rendering della pagina, si consiglia di impostare `prehidingStyle` un elenco di elementi contenitore che contengono le parti della pagina che verranno personalizzate.

Presupponendo di disporre di una pagina HTML come quella riportata di seguito e sapendo che solo gli elementi `bar` e `bazz` contenitori saranno mai personalizzati:

```html
<html>
  <head>
  </head>
  <body>
    <div id="foo">
      Foo foo foo
    </div>

    <div id="bar">
      Bar bar bar
    </div>

    <div id="bazz">
      Bazz bazz bazz
    </div>
  </body>
</html>
```

Allora `prehidingStyle` dovrebbe essere impostato su qualcosa come `#bar, #bazz { opacity: 0 !important }`.

## Pre-elaborazione

La fase di pre-elaborazione viene eseguita una volta che l’SDK ha ricevuto il contenuto personalizzato dal server. Durante questa fase, la risposta viene preelaborata, verificando che gli elementi che devono contenere contenuti personalizzati siano nascosti. Una volta nascosti questi elementi, il tag di stile HTML creato in base all&#39;opzione di `prehidingStyle` configurazione viene rimosso e vengono visualizzati il corpo HTML o gli elementi contenitori nascosti.

## Rendering

Dopo che il rendering di tutto il contenuto di personalizzazione è stato eseguito correttamente, o in caso di errore, vengono visualizzati tutti gli elementi precedentemente nascosti per essere certi che non ci siano elementi nascosti sulla pagina che erano nascosti dall’SDK.

## Gestione dello sfarfallio quando l’SDK viene caricato in modo asincrono

Si consiglia di caricare sempre l&#39;SDK in modo asincrono per ottenere le migliori prestazioni di rendering delle pagine. Tuttavia, questo ha alcune implicazioni per il rendering di contenuti personalizzati. Quando l’SDK viene caricato in modo asincrono, è necessario utilizzare lo snippet di pregenerazione. Lo snippet di pregenerazione deve essere aggiunto prima dell’SDK nella pagina HTML. Di seguito è riportato un frammento di esempio che nasconde l’intero corpo:

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Per garantire che il corpo HTML o gli elementi contenitore non siano nascosti per un periodo di tempo prolungato, lo snippet di pregenerazione utilizza un timer che per impostazione predefinita rimuove lo snippet dopo `3000` millisecondi. Il tempo di attesa massimo `3000` in millisecondi. Se la risposta dal server è stata ricevuta ed elaborata prima, il tag di stile HTML di pre-nascondere viene rimosso il prima possibile.
