---
title: Utilizzare più istanze di Web SDK
description: Scopri come interagire con più proprietà di Experience Platform Web SDK.
keywords: più proprietà
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 192739967e6b050bb04893ee7bab5119dd7f870c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Utilizzare più istanze di Web SDK

In alcuni casi potrebbe essere utile interagire con due proprietà diverse sulla stessa pagina. Gli scenari possibili includono:

* Aziende che sono state acquisite e stanno lavorando all’integrazione dei loro siti web
* Relazioni di condivisione dei dati tra più aziende
* Clienti che stanno testando nuove soluzioni Adobe e non desiderano interrompere l’implementazione esistente

SDK consente di creare un&#39;istanza separata per ogni proprietà aggiungendo un altro nome all&#39;array nel [codice base](../js/install/base-code.md). Nell&#39;esempio seguente vengono forniti due nomi, `titanium` e `copper`.

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>

<!-- Load the Web SDK (JavaScript library loader or Tags embed code) -->
<!-- <script src=".../alloy.min.js" async></script> -->
<!-- <script src=".../launch-<ENV>.min.js" async></script> -->
```

Di conseguenza, lo script crea due funzioni globali (`titanium` e `copper` nell&#39;esempio precedente) che diventano due istanze di SDK quando la libreria viene inizializzata. Ogni istanza mantiene la propria configurazione e il proprio stato; qualsiasi comando che utilizza `titanium` viene mantenuto isolato da `copper`.

>[!TIP]
>
>Se utilizzi il codice di base con i tag, assicurati che tutti i nomi di istanza impostati corrispondano a tutti i [nomi di istanza di SDK](/help/tags/extensions/client/web-sdk/configure/general.md) durante la configurazione dell&#39;estensione tag.

Seguendo l&#39;esempio del modello di denominazione di `titanium` e `copper` come istanze di Web SDK, è possibile eseguire in modo indipendente i comandi:

```javascript
titanium("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  data: {
    key: "value"
  }
});

copper("configure", {
  datastreamId: "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  orgId: "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  data: {
    key: "value"
  }
});
```

Assicurarsi di eseguire il comando [`configure`](../js/commands/configure/overview.md) per ogni istanza prima di eseguire altri comandi sulla stessa istanza.

>[!IMPORTANT]
>
>Per evitare conflitti con i cookie, ogni istanza di Web SDK deve avere il proprio `datastreamId` univoco e il proprio `orgId` univoco.
