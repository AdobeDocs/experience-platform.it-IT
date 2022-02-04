---
title: Gestione della visualizzazione momentanea di altri contenuti per esperienze personalizzate tramite l’SDK per web di Adobe Experience Platform
description: Scopri come utilizzare Adobe Experience Platform Web SDK per gestire la visualizzazione momentanea di altri contenuti sulle esperienze utente.
keywords: target;visualizzazione momentanea;pre-hidingStyle;asincrono;asincrono;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: e5d279397cab30e997103496beda5265520dca77
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Gestione della visualizzazione momentanea di altri contenuti

Quando tenti di eseguire il rendering del contenuto di personalizzazione, l’SDK deve assicurarsi che non vi sia alcuno sfarfallio. La visualizzazione momentanea di altri contenuti, denominata anche FOOC (Flash di contenuti originali), si verifica quando un contenuto originale viene visualizzato brevemente prima che l’alternativa venga visualizzata durante il test/personalizzazione. L’SDK tenta di applicare gli stili CSS agli elementi della pagina per garantire che tali elementi siano nascosti finché il contenuto di personalizzazione non viene riprodotto correttamente.

La funzionalità di gestione della visualizzazione momentanea di altri contenuti prevede alcune fasi:

1. Preconfigurazione
1. Pre-elaborazione
1. Rendering

## Preconfigurazione

Durante la fase di pre-hiding, l&#39;SDK utilizza `prehidingStyle` opzione di configurazione per creare un tag stile di HTML e aggiungerlo al DOM per assicurarti che parti importanti della pagina siano nascoste. Se non sei sicuro di quali parti della pagina saranno personalizzate, si consiglia di impostare `prehidingStyle` a `body { opacity: 0 !important }`. In questo modo l’intera pagina viene nascosta. Questo, tuttavia, ha il lato negativo di portare a prestazioni di rendering della pagina peggiori segnalati da strumenti come faro, test di pagina web, ecc. Per ottenere le migliori prestazioni di rendering della pagina, è consigliabile impostare `prehidingStyle` a un elenco di elementi contenitore che contengono le parti della pagina che verranno personalizzate.

Supponendo di avere una pagina HTML come quella sottostante e di sapere solo che `bar` e `bazz` Gli elementi contenitore verranno sempre personalizzati:

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

Quindi il `prehidingStyle` deve essere impostato su qualcosa di simile `#bar, #bazz { opacity: 0 !important }`.

## Pre-elaborazione

La fase di preelaborazione viene eseguita una volta che l’SDK ha ricevuto il contenuto personalizzato dal server. Durante questa fase, la risposta viene preelaborata, assicurandosi che gli elementi che devono contenere contenuti personalizzati siano nascosti. Una volta nascosti questi elementi, il tag stile di HTML creato in base alla `prehidingStyle` l’opzione di configurazione viene rimossa e vengono visualizzati il corpo di HTML o gli elementi del contenitore nascosto.

## Rendering

Dopo che il rendering di tutti i contenuti di personalizzazione è stato eseguito correttamente o in caso di errore, vengono visualizzati tutti gli elementi nascosti in precedenza per assicurarti che non vi siano elementi nascosti nella pagina che erano nascosti dall’SDK.

## Gestione della visualizzazione momentanea di altri contenuti quando l&#39;SDK viene caricato in modo asincrono

Si consiglia di caricare sempre l&#39;SDK in modo asincrono per ottenere le migliori prestazioni di rendering della pagina. Tuttavia, questo ha alcune implicazioni per il rendering di contenuti personalizzati. Quando l&#39;SDK viene caricato in modo asincrono, è necessario utilizzare il frammento pre-hiding. Il frammento pre-hiding deve essere aggiunto prima dell&#39;SDK nella pagina HTML. Ecco un frammento di esempio che nasconde l&#39;intero corpo:

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Per garantire che il corpo di HTML o gli elementi del contenitore non siano nascosti per un periodo di tempo prolungato, il frammento pre-hiding utilizza un timer che per impostazione predefinita rimuove il frammento dopo `3000` millisecondi. La `3000` millisecondi indica il tempo massimo di attesa. Se la risposta dal server è stata ricevuta ed elaborata prima, il tag stile di HTML che nasconde preventivamente viene rimosso il prima possibile.
