---
title: Installare il Web SDK utilizzando la libreria JavaScript
description: Fai riferimento alla libreria Web SDK utilizzando un file CDN autonomo.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# Installare il Web SDK utilizzando la libreria JavaScript

Un&#39;alternativa all&#39;installazione del Web SDK senza [utilizzo dell&#39;estensione tag](extension.md) consiste nel fare riferimento alla libreria JavaScript ospitata su una rete CDN. Puoi fare riferimento direttamente alla libreria, oppure scaricarla e ospitarla sulla tua infrastruttura. È disponibile in formati minimizzati e completi.

La libreria SDK Web è disponibile utilizzando la seguente struttura URL:

* **Minificato**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Completo**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Consulta le [note sulla versione](../release-notes.md) per conoscere la versione più recente da includere nell&#39;URL. Ad esempio, l&#39;URL della versione completa 2.19.1 è `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Aggiunta del codice

Aggiungi il seguente blocco di codice il più in alto possibile nel tag `<head>` del tuo HTML:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Questo codice crea in modo asincrono un oggetto `alloy` che consente di chiamare qualsiasi comando di Web SDK. Se si desidera caricare il Web SDK in modo sincrono, è possibile rimuovere l&#39;attributo `async` nell&#39;ultima riga del blocco di codice. La rimozione dell&#39;attributo `async` impedisce l&#39;analisi e il rendering del resto del documento HTML da parte del browser fino al caricamento e all&#39;esecuzione della libreria. Questo ritardo aggiuntivo prima di mostrare il contenuto principale agli utenti è in genere sconsigliato, ma può avere un senso a seconda delle esigenze della tua organizzazione.
