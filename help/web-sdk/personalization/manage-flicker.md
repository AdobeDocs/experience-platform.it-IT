---
title: Gestire la visualizzazione momentanea di altri contenuti per esperienze personalizzate tramite Adobe Experience Platform Web SDK
description: Scopri come utilizzare Adobe Experience Platform Web SDK per gestire la visualizzazione momentanea di altri contenuti sulle esperienze utente.
keywords: target;sfarfallio;prehidingStyle;asincrono;asincrono;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Gestisci visualizzazione momentanea di altri contenuti

Quando tenti di eseguire il rendering del contenuto di personalizzazione, l’SDK deve assicurarsi che non vi sia alcuno sfarfallio. Lo sfarfallio, chiamato anche FOOC (Flash del contenuto originale), si verifica quando un contenuto originale viene visualizzato brevemente prima che l’alternativa venga visualizzata durante il test/la personalizzazione. L’SDK tenta di applicare stili CSS agli elementi della pagina per garantire che siano nascosti fino a quando il contenuto di personalizzazione non viene renderizzato correttamente.

La modalità di gestione della visualizzazione momentanea di altri contenuti dipende dalla distribuzione dell&#39;SDK Web in modo sincrono o asincrono. Controllare il tag `<head>` in cui si distribuisce `alloy.js` o il caricatore di tag. La presenza dell&#39;attributo `async` nel tag `<script>` determina se Web SDK viene caricato in modo asincrono.

```html
<!-- This tag loads synchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js"></script>

<!-- This tag loads asynchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js" async></script>

<!-- This library loads synchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>

<!-- This library loads asynchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

## Gestire la visualizzazione momentanea di altri contenuti per le distribuzioni sincrone

La gestione dello sfarfallio sincrono è suddivisa in tre fasi:

1. Pre-hiding
1. Preelaborazione
1. Rendering

Durante la **fase di pre-hiding**, l&#39;SDK utilizza la proprietà di configurazione [`prehidingStyle`](../commands/configure/prehidingstyle.md) per creare un tag di stile HTML e aggiungerlo al DOM per assicurarsi che le sezioni desiderate della pagina siano nascoste. Se non si è sicuri di quali parti della pagina saranno personalizzate, si consiglia di impostare `prehidingStyle` su `body { opacity: 0 !important }`. In questo modo l’intera pagina sarà nascosta. Questo, tuttavia, ha l’effetto negativo di portare a prestazioni di rendering della pagina peggiori riportate da strumenti come Lighthouse, Test di pagine web, ecc. Per ottenere le migliori prestazioni di rendering della pagina, si consiglia di impostare `prehidingStyle` su un elenco di elementi contenitore che contengono le parti della pagina che verranno personalizzate.

Supponendo di disporre di una pagina HTML come quella riportata di seguito e di sapere che solo `bar` e `bazz` elementi contenitore saranno mai personalizzati:

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

Quindi `prehidingStyle` deve essere impostato su qualcosa come `#bar, #bazz { opacity: 0 !important }`.

Una volta che l&#39;SDK ha ricevuto contenuti personalizzati dal server, inizia la **fase di pre-elaborazione**. Durante questa fase, la risposta viene preelaborata, assicurandosi che gli elementi che devono contenere contenuti personalizzati siano nascosti. Quando questi elementi sono nascosti, il tag di stile HTML creato in base all&#39;opzione di configurazione `prehidingStyle` viene rimosso e vengono visualizzati il corpo del HTML o gli elementi contenitore nascosti.

Dopo che tutto il contenuto di personalizzazione è stato renderizzato correttamente o se si è verificato un errore, inizia la **fase di rendering**. Vengono visualizzati tutti gli elementi precedentemente nascosti per verificare che nella pagina non siano presenti elementi nascosti dall’SDK.

## Gestire la visualizzazione momentanea di altri contenuti per le implementazioni asincrone

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

Per assicurarsi che il corpo del HTML o gli elementi contenitore non siano nascosti per un periodo di tempo prolungato, il frammento pre-hiding utilizza un timer che per impostazione predefinita rimuove il frammento dopo `3000` millisecondi. `3000` millisecondi è il tempo di attesa massimo. Se la risposta dal server è stata ricevuta ed elaborata in precedenza, il tag di pre-hiding in stile HTML viene rimosso il prima possibile.
