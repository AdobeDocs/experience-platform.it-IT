---
title: Interazione con più proprietà
seo-title: SDK Web per Adobe Experience Platform che interagisce con più proprietà
description: Scopri come interagire con più proprietà SDK Web della piattaforma Experience
seo-description: Scopri come interagire con più proprietà SDK Web della piattaforma Experience
translation-type: tm+mt
source-git-commit: 7d4f364ebb9df1ce58481a35007ea75f86ab7825
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---


# Interazione con più proprietà

In alcuni casi può essere utile interagire con due proprietà diverse sulla stessa pagina. Comprendono:

* Aziende acquisite e che stanno lavorando per integrare i propri siti Web
* Relazioni di condivisione dei dati tra più società
* Clienti che stanno testando nuove soluzioni Adobe e non desiderano interrompere la loro implementazione esistente

L’SDK consente di creare un’istanza separata per ciascuna proprietà aggiungendo un altro nome all’array nel codice di base. Nell&#39;esempio seguente sono stati forniti due nomi `mycustomname1` e `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Di conseguenza, lo script crea due istanze dell&#39;SDK. Viene denominata la funzione globale per l’interazione con la prima istanza `mycustomname1` e viene denominata la funzione globale per l’interazione con la seconda `mycustomname2`.

Creando due istanze separate, ciascuna può essere configurata per una proprietà diversa. Qualsiasi comunicazione o persistenza di dati che si verifica a causa dell&#39;interazione con `mycustomname1` viene mantenuta isolata da `mycustomname2` e viceversa.

Seguendo l&#39;esempio precedente, è possibile eseguire comandi utilizzando ciascuna istanza, come segue:

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

Assicurarsi di eseguire il `configure` comando per ogni istanza prima di eseguire altri comandi sulla stessa istanza.

## Limitazioni 

Per evitare conflitti con i cookie, una sola istanza di Adobe Experience Platform Web SDK all’interno di una pagina può avere una particolare `edgeConfigId`.  Analogamente, solo un’istanza dell’SDK Web per Adobe Experience Platform può avere un particolare `orgId`.
