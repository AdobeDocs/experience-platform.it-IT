---
title: Riferimento oggetto satellite
description: Scopri l’oggetto _satellite lato client e le varie funzioni che consente di eseguire con esso nei tag.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---

# `_satellite` Guida di riferimento per gli oggetti di

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
// Read and write a temporary data element value
const region = _satellite.getVar('user_region');
_satellite.setVar('promo_code', code);

// Local debugging
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');

// Manually trigger a rule configured in your tag property
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}
```
