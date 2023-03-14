---
title: Gestire la visualizzazione momentanea di altri contenuti per esperienze personalizzate tramite Adobe Experience Platform Web SDK
description: Scopri come utilizzare Adobe Experience Platform Web SDK per gestire la visualizzazione momentanea di altri contenuti sulle esperienze utente.
keywords: target;sfarfallio;prehidingStyle;asincrono;asincrono;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: e5d279397cab30e997103496beda5265520dca77
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Gestisci visualizzazione momentanea di altri contenuti

Quando tenti di eseguire il rendering del contenuto di personalizzazione, l’SDK deve assicurarsi che non vi sia alcuno sfarfallio. Lo sfarfallio, chiamato anche FOOC (Flash del contenuto originale), si verifica quando un contenuto originale viene visualizzato brevemente prima che l’alternativa venga visualizzata durante il test/la personalizzazione. L’SDK tenta di applicare stili CSS agli elementi della pagina per garantire che siano nascosti fino a quando il contenuto di personalizzazione non viene renderizzato correttamente.

La funzionalità di gestione della visualizzazione momentanea di altri contenuti prevede alcune fasi:

1. Pre-hiding
1. Preelaborazione
1. Rendering

## Pre-hiding

Durante la fase di pre-hiding, l&#39;SDK utilizza `prehidingStyle` opzione di configurazione per creare un tag in stile HTML e aggiungerlo al DOM per fare in modo che parti grandi della pagina siano nascoste. Se non sai quali parti della pagina saranno personalizzate, ti consigliamo di impostare `prehidingStyle` a `body { opacity: 0 !important }`. In questo modo l’intera pagina sarà nascosta. Questo, tuttavia, ha l’effetto negativo di portare a prestazioni di rendering della pagina peggiori riportate da strumenti come Lighthouse, Test di pagine web, ecc. Per ottenere le migliori prestazioni di rendering della pagina, si consiglia di impostare `prehidingStyle` in un elenco di elementi contenitore che contengono le parti della pagina che verranno personalizzate.

Supponendo di avere una pagina HTML come quella di seguito e di sapere che solo `bar` e `bazz` gli elementi contenitore saranno sempre personalizzati:

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

Quindi il `prehidingStyle` deve essere impostato su qualcosa di simile a `#bar, #bazz { opacity: 0 !important }`.

## Preelaborazione

La fase di pre-elaborazione viene avviata una volta che l’SDK ha ricevuto il contenuto personalizzato dal server. Durante questa fase, la risposta viene preelaborata, assicurandosi che gli elementi che devono contenere contenuti personalizzati siano nascosti. Dopo aver nascosto questi elementi, il tag di stile HTML creato in base al `prehidingStyle` l’opzione di configurazione viene rimossa e vengono visualizzati il corpo del HTML o gli elementi del contenitore nascosto.

## Rendering

Una volta eseguito correttamente il rendering di tutto il contenuto di personalizzazione, o in caso di errore, vengono visualizzati tutti gli elementi precedentemente nascosti per verificare che non vi siano elementi nascosti nella pagina nascosti dall’SDK.

## Gestione della visualizzazione momentanea di altri contenuti quando l’SDK viene caricato in modo asincrono

Ti consigliamo di caricare l’SDK in modo sempre asincrono per ottenere le migliori prestazioni di rendering delle pagine. Tuttavia, questo ha alcune implicazioni per il rendering di contenuti personalizzati. Quando l’SDK viene caricato in modo asincrono, è necessario utilizzare il frammento pre-hiding. Il frammento pre-hiding deve essere aggiunto prima dell&#39;SDK nella pagina HTML. Di seguito è riportato un frammento di codice che nasconde l&#39;intero corpo:

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

Per evitare che il corpo del HTML o gli elementi contenitore vengano nascosti per un periodo di tempo prolungato, il frammento pre-hiding utilizza un timer che, per impostazione predefinita, rimuove il frammento dopo `3000` millisecondi. Il `3000` millisecondi è il tempo di attesa massimo. Se la risposta dal server è stata ricevuta ed elaborata in precedenza, il tag di pre-hiding in stile HTML viene rimosso il prima possibile.
