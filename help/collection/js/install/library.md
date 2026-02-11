---
title: Installare la libreria JavaScript di Web SDK
description: Fai riferimento alla libreria Web SDK utilizzando un file CDN autonomo.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 010192e91185c11d5454d4153913c06b90fe2122
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Installare la libreria JavaScript di Web SDK

Se si sceglie di non utilizzare l&#39;estensione tag [Web SDK](/help/tags/extensions/client/web-sdk/overview.md), è possibile installare Web SDK facendo riferimento alla libreria JavaScript autonoma ospitata sul CDN di Adobe. Puoi fare riferimento direttamente alla libreria, oppure scaricarla e ospitarla sulla tua infrastruttura. È disponibile in formati minimizzati e completi.

La libreria SDK Web è disponibile utilizzando la seguente struttura URL:

* **Minificato**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js`
* **Completo**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.js`

Consulta le [note sulla versione di Web SDK](../release-notes.md) per conoscere la versione più recente da includere nell&#39;URL. Ad esempio, l&#39;URL della versione completa 2.19.1 è `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Aggiunta del codice di base e del caricatore della libreria

Il codice da aggiungere è costituito da due sezioni:

* **Codice di base**: consente l&#39;avvio automatico accodando i comandi durante il caricamento asincrono del Web SDK. Per ulteriori informazioni, vedere [Codice base](base-code.md). Adobe consiglia di utilizzare il codice di base durante il caricamento della libreria in modo asincrono, per evitare race condition durante la chiamata di comandi Web SDK durante il caricamento della pagina.
* **Library loader**: carica l&#39;intera libreria JavaScript.

Aggiungere il seguente blocco di codice il più in alto possibile nel tag `<head>`, prima di qualsiasi script che potrebbe chiamare il Web SDK:

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!-- Library loader -->
<script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
```

Se si desidera caricare il Web SDK in modo sincrono, è possibile rimuovere l&#39;attributo `async` durante il caricamento della libreria. La rimozione dell&#39;attributo `async` blocca l&#39;analisi di HTML mentre il browser recupera ed esegue la libreria. Questo ritardo aggiuntivo prima di mostrare il contenuto principale agli utenti è in genere sconsigliato, ma può avere un senso a seconda delle esigenze della tua organizzazione.
