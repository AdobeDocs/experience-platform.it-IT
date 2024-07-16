---
title: Utilizzare più istanze di Web SDK
description: Scopri come interagire con più proprietà di Experience Platform Web SDK.
keywords: più proprietà;configurare;sendEvent;edgeConfigId;orgId;
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Utilizzare più istanze di Web SDK

In alcuni casi potrebbe essere utile interagire con due proprietà diverse sulla stessa pagina. Tali casi includono:

* Aziende che sono state acquisite e stanno lavorando all’integrazione dei loro siti web
* Relazioni di condivisione dei dati tra più aziende
* Clienti che stanno testando nuove soluzioni Adobe e non desiderano interrompere l’implementazione esistente

L’SDK consente di creare un’istanza separata per ogni proprietà aggiungendo un altro nome all’array nel codice di base. Nell&#39;esempio seguente vengono forniti due nomi, `titanium` e `copper`.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

Di conseguenza, lo script crea due istanze dell’SDK. La funzione globale per interagire con la prima istanza è denominata `titanium` e la funzione globale per interagire con la seconda istanza è denominata `copper`.

Creando due istanze separate, ciascuna può essere configurata per una proprietà diversa. Qualsiasi comunicazione o persistenza dei dati che si verifica a causa dell&#39;interazione con `titanium` viene mantenuta isolata da `copper`.

Seguendo l’esempio precedente, è possibile eseguire comandi utilizzando ogni istanza:

```javascript
titanium("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  "data": {
    "key": "value"
  }
});

copper("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

Assicurarsi di eseguire il comando `configure` per ogni istanza prima di eseguire altri comandi sulla stessa istanza.

>[!IMPORTANT]
>
>Per evitare conflitti con i cookie, ogni istanza di Web SDK deve avere il proprio `edgeConfigId` univoco e il proprio `orgId` univoco.
