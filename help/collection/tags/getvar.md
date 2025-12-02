---
title: getVar()
description: Restituisce il valore di un elemento dati o di un set di valori utilizzando setVar().
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---

# `getVar()`

Il metodo `_satellite.getVar()` restituisce il valore corrente di un [elemento dati](/help/tags/ui/managing-resources/data-elements.md) o un valore impostato utilizzando [`_satellite.setVar()`](setvar.md). Se un elemento dati e un valore `setVar()` condividono lo stesso nome, l&#39;elemento dati ha la precedenza. Se si chiama un identificatore di stringa che non esiste ancora, il metodo restituisce `undefined`. Valutazione sincrona.

```js
_satellite.getVar(name: string, event?: unknown) => unknown
```

Il valore e il tipo restituiti dipendono dal tipo di elemento dati a cui si fa riferimento. Ad esempio, se si chiama `getVar()` che recupera una variabile stringa, il tipo restituito è `string`. Se si chiama `getVar()` che restituisce un elemento dati variabile di Web SDK, il tipo restituito è un `object` contenente tutte le proprietà impostate in tale variabile.

```js
// Retrieves the value in the `Example` data element
_satellite.getVar('Example');

// Execute custom logic depending on the numeric value in the `cartTotal` data element
const cartValue = Number(_satellite.getVar('cartTotal'));
if (cartValue > 100) {
  _satellite.logger.info('Purchase larger than $100 detected');
}

// Some data elements like Web SDK variables support deeply nested properties
const pageName = _satellite.getVar('Data layer')?.web?.webPageDetails?.name;
if (!pageName) {
  _satellite.logger.warn('Page name is not set');
}

// Custom code data elements support a second argument
// Works in a Launch custom code block where `event` is provided by the rule engine.
const rule = _satellite.getVar('Return event rule', event);
```

## Campi disponibili

Il metodo `getVar()` supporta due argomenti. La maggior parte dei casi d’uso non include il secondo argomento facoltativo.

| Nome | Tipo | Obbligatorio | Descrizione |
| --- | --- | --- | --- |
| **`name`** | `string` | Sì | Il nome dell’elemento dati che desideri recuperare. I nomi degli elementi dati fanno distinzione tra maiuscole e minuscole. |
| **`event`** | `object` | No | Contesto dell’evento dalla regola di attivazione. Utilizzato solo in casi d&#39;uso avanzati da elementi dati che utilizzano [codice personalizzato](/help/tags/ui/managing-resources/data-elements.md#custom-code) o estensioni personalizzate. Quando una regola viene attivata da un evento (ad esempio un clic, l’invio di un modulo o un invio JavaScript personalizzato), l’oggetto evento associato viene incluso qui. Gli elementi dati possono utilizzare queste informazioni per restituire valori contestuali, come i dettagli o le proprietà dell’elemento su cui è stato fatto clic da un evento personalizzato. |
