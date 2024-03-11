---
title: Installare l’SDK web utilizzando la libreria JavaScript
description: Fai riferimento alla libreria dell’SDK web utilizzando un file CDN indipendente.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Installare l’SDK web utilizzando la libreria JavaScript

Alternativa all’installazione dell’SDK per web senza [utilizzo dell’estensione tag](extension.md) fa riferimento alla libreria JavaScript ospitata su una rete CDN. Puoi fare riferimento direttamente alla libreria, oppure scaricarla e ospitarla sulla tua infrastruttura. È disponibile in formati minimizzati e completi.

La libreria SDK web è disponibile utilizzando la seguente struttura URL:

* **Minimizzato**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Completo**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Consulta la [note sulla versione](../release-notes.md) la versione più recente da includere nell’URL. Ad esempio, l’URL per la versione completa della versione 2.19.1 di è `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Aggiunta del codice

Aggiungi il seguente blocco di codice il più in alto possibile nel `<head>` tag del HTML:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Questo codice crea in modo asincrono un `alloy` oggetto che consente di chiamare qualsiasi comando Web SDK. Se desideri caricare l’SDK Web in modo sincrono, puoi rimuovere `async` nell&#39;ultima riga del blocco di codice. Rimozione di `async` Questo attributo impedisce al resto del documento HTML di essere analizzato e renderizzato dal browser finché la libreria non viene caricata ed eseguita. Questo ritardo aggiuntivo prima di mostrare il contenuto principale agli utenti è in genere sconsigliato, ma può avere un senso a seconda delle esigenze della tua organizzazione.
