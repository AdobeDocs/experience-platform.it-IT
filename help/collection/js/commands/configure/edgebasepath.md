---
title: edgeBasePath
description: Percorso di base dell’endpoint utilizzato per interagire con i servizi Adobe.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 1fa7b48f99948a5252635dc1a8c5142fea5df57b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# `edgeBasePath`

La proprietà `edgeBasePath` modifica il percorso di destinazione quando si interagisce con i servizi Adobe. Adobe potrebbe richiedere la modifica di questa variabile se partecipi a programmi alfa o beta per la raccolta di dati. La maggior parte delle organizzazioni non deve impostare o modificare questa proprietà.

Impostare il campo di testo `edgeBasePath` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà, verrà utilizzato il valore predefinito `ee`. Adobe consiglia di omettere questa proprietà dalla maggior parte delle configurazioni.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```

## Percorso di base di Edge tramite l’estensione tag Web SDK

L&#39;equivalente dell&#39;estensione tag Web SDK di questo campo si trova in [Impostazioni di configurazione avanzate](/help/tags/extensions/client/web-sdk/configure/advanced-settings.md) durante la configurazione dell&#39;estensione tag.
