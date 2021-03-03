---
title: Interagire con più proprietà nell’SDK per web di Adobe Experience Platform
description: Scopri come interagire con più proprietà dell’SDK web di Experience Platform.
keywords: più proprietà;configurare;sendEvent;edgeConfigId;orgId;
translation-type: tm+mt
source-git-commit: b865b7fb940ca2d5f8b44f71eb58e62e3473f52d
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Interagire con più proprietà

In alcuni casi può essere utile interagire con due proprietà diverse sulla stessa pagina. Questi casi includono:

* Aziende che sono state acquisite e stanno lavorando per integrare i loro siti web insieme
* Relazioni di condivisione dei dati tra più aziende
* Clienti che testano nuove soluzioni Adobe e non desiderano interrompere l’implementazione esistente

L’SDK consente di creare un’istanza separata per ciascuna proprietà aggiungendo un altro nome all’array nel codice di base. L&#39;esempio seguente fornisce due nomi, `mycustomname1` e `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Di conseguenza, lo script crea due istanze dell&#39;SDK. La funzione globale per l’interazione con la prima istanza è denominata `mycustomname1` e la funzione globale per l’interazione con la seconda istanza è denominata `mycustomname2`.

Creando due istanze separate, ciascuna può essere configurata per una proprietà diversa. Tutte le comunicazioni o la persistenza dei dati che si verificano a causa dell&#39;interazione con `mycustomname1` vengono tenute isolate da `mycustomname2`.

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

Assicurati di eseguire il comando `configure` per ogni istanza prima di eseguire altri comandi sulla stessa istanza.

## Limitazioni 

Per evitare conflitti con i cookie, solo un’istanza di Adobe Experience Platform [!DNL Web SDK] all’interno di una pagina può avere un `edgeConfigId` particolare. Allo stesso modo, solo una istanza di Adobe Experience Platform [!DNL Web SDK] può avere un particolare `orgId`.
