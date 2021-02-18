---
title: Interagire con più proprietà nell’SDK Adobe Experience Platform Web
description: Scopri come interagire con più proprietà SDK Web  Experience Platform.
keywords: più proprietà;configurare;sendEvent;edgeConfigId;orgId;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---


# Interagisci con più proprietà

In alcuni casi può essere utile interagire con due proprietà diverse sulla stessa pagina. Comprendono:

* Aziende acquisite e che stanno lavorando per integrare i propri siti Web
* Relazioni di condivisione dei dati tra più società
* Clienti che stanno testando nuove soluzioni  Adobe e non desiderano interrompere la loro implementazione esistente

L’SDK consente di creare un’istanza separata per ciascuna proprietà aggiungendo un altro nome all’array nel codice di base. Nell&#39;esempio seguente sono stati forniti due nomi, `mycustomname1` e `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Di conseguenza, lo script crea due istanze dell&#39;SDK. La funzione globale per l&#39;interazione con la prima istanza è denominata `mycustomname1` e la funzione globale per l&#39;interazione con la seconda istanza è denominata `mycustomname2`.

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

Assicurarsi di eseguire il comando `configure` per ogni istanza prima di eseguire altri comandi sulla stessa istanza.

## Limitazioni 

Per evitare conflitti con i cookie, solo un&#39;istanza di Adobe Experience Platform [!DNL Web SDK] all&#39;interno di una pagina può avere un `edgeConfigId` particolare.  Analogamente, solo un&#39;istanza di Adobe Experience Platform [!DNL Web SDK] può avere un `orgId` particolare.
