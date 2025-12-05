---
title: Riferimento oggetto satellite
description: Scopri l’oggetto _satellite lato client e le varie funzioni che consente di eseguire con esso nei tag.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 05bf3a8c92aa221af153b4ce9949f0fdfc3c86ab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# `_satellite` Guida di riferimento per gli oggetti di

_Queste pagine descrivono come utilizzare l&#39;oggetto `_satellite`, che consente di gestire e personalizzare la logica dei tag tramite JavaScript. Per informazioni dettagliate su come configurare l&#39;implementazione nell&#39;interfaccia utente di Data Collection, vedere [Estensione tag di Adobe Experience Platform Web SDK](/help/tags/extensions/client/web-sdk/overview.md)._

L&#39;oggetto `_satellite` espone diversi punti di ingresso supportati che consentono di interagire con la libreria di tag pubblicata sul sito. Tutte le distribuzioni di tag espongono `_satellite` se il tag del caricatore è implementato correttamente. Esistono diversi casi d’uso principali per questo oggetto:

* Utilizzo all’interno della libreria di tag in blocchi di codice personalizzati, per un accesso completo alla libreria di tag stessa.
* Eseguire il debug dell’implementazione implementata in qualsiasi ambiente (sviluppo, staging o produzione)
* Implementazione diretta sul sito web, per un controllo completo su quando si attivano eventi o regole di tag. Per le nuove implementazioni, Adobe consiglia di utilizzare una strategia più flessibile come [Adobe Client Data Layer](/help/tags/extensions/client/client-data-layer/overview.md).

>[!IMPORTANT]
>
>Se chiami `_satellite` dal codice del sito (ad esempio, `_satellite.track()`), **proteggi ogni chiamata** in modo che il sito non sia strettamente associato alla libreria di tag.
>
>L&#39;utilizzo di `_satellite` all&#39;interno del codice personalizzato di una proprietà tag o localmente nella console del browser non richiede protezione.

## Esempi di utilizzo comuni

```js
// Read and write a temporary data element value (guarded)
if(window._satellite?.getVar && window._satellite?.setVar) {
  const region = _satellite.getVar('user_region');
  _satellite.setVar('promo_code', code);
}

// Manually trigger a rule configured in your tag property (guarded)
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}

// Local console debugging (guarding not needed)
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');
```
