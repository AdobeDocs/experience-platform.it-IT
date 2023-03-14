---
title: Interagire con più proprietà in Adobe Experience Platform Web SDK
description: Scopri come interagire con più proprietà di Experience Platform Web SDK.
keywords: più proprietà;configurare;sendEvent;edgeConfigId;orgId;
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Interagire con più proprietà

In alcuni casi potrebbe essere utile interagire con due proprietà diverse sulla stessa pagina. Tali casi includono:

* Aziende che sono state acquisite e stanno lavorando all’integrazione dei loro siti web
* Relazioni di condivisione dei dati tra più aziende
* Clienti che stanno testando nuove soluzioni Adobe e non desiderano interrompere l’implementazione esistente

L’SDK consente di creare un’istanza separata per ogni proprietà aggiungendo un altro nome all’array nel codice di base. Nell&#39;esempio seguente vengono forniti due nomi: `mycustomname1` e `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Di conseguenza, lo script crea due istanze dell’SDK. La funzione globale per l’interazione con la prima istanza è denominata `mycustomname1` e la funzione globale per interagire con la seconda istanza è denominata `mycustomname2`.

Creando due istanze separate, ciascuna può essere configurata per una proprietà diversa. Qualsiasi comunicazione o persistenza dei dati che si verifica a causa dell’interazione con `mycustomname1` è tenuto isolato da `mycustomname2`.

Seguendo l&#39;esempio precedente, è possibile eseguire comandi utilizzando ciascuna delle istanze, come indicato di seguito:

```javascript
mycustomname1("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("sendEvent", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

Assicurati di eseguire `configure` per ogni istanza prima di eseguire altri comandi sulla stessa istanza.

## Limitazioni 

Per evitare conflitti con i cookie, è sufficiente una sola istanza di Adobe Experience Platform [!DNL Web SDK] all&#39;interno di una pagina può avere un particolare `edgeConfigId`. Analogamente, solo un’istanza di Adobe Experience Platform [!DNL Web SDK] può avere un particolare `orgId`.
