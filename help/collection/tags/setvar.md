---
title: setVar()
description: Imposta un valore che è possibile recuperare in seguito utilizzando getVar().
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# `setVar()`

Il metodo `_satellite.setVar()` consente di impostare una o più coppie nome/valore personalizzate alle quali [`_satellite.getVar()`](getvar.md) può fare successivamente riferimento.

```ts
// Set a single name/value pair
_satellite.setVar(name: string, value: unknown): void

// Set multiple name/value pairs at once
_satellite.setVar(vars: { [name: string]: unknown }): void;
```

>[!IMPORTANT]
>
>Sebbene il metodo `getVar()` possa recuperare sia gli elementi dati che i valori impostati da `setVar()`, questi due tipi di entità sono separati. L&#39;utilizzo di `setVar()` per impostare un valore con lo stesso nome di un elemento dati nell&#39;interfaccia utente dei tag non lo sovrascrive.

## Persistenza e ambito

I valori `setVar()` sono attivi solo nella memoria della pagina:

* **Solo pagina corrente**: i valori rimangono invariati fino a quando la pagina non viene scaricata. Nelle applicazioni a pagina singola, persistono fino a quando non vengono completamente ricaricate oppure vengono sovrascritte o cancellate.
* **Archiviazione browser assente**: non viene scritto nulla nei cookie, nell&#39;archiviazione locale o nell&#39;archiviazione di sessione.

## Valori di riferimento impostati con `setVar()`

È possibile recuperare i valori nel codice personalizzato utilizzando `getVar()`:

```js
// Set a custom variable using setVar()
_satellite.setVar('Ad location','Banner advertisement');

// Returns the string 'Banner advertisement'
_satellite.getVar('Ad location');
```

Puoi anche fare riferimento a queste variabili nell’interfaccia utente dei tag nei campi che supportano la notazione degli elementi dati:

```text
%Ad location%
```

>[!NOTE]
>
>Se un set di valori che utilizza `setVar()` utilizza lo stesso nome di un elemento dati e si fa riferimento a tale nome nella notazione dell&#39;elemento dati, l&#39;elemento dati ha la precedenza.

## Esempi

```js
// Set a single name/value pair
_satellite.setVar('product', 'Circuit Pro');

// Set multiple name/value pairs at once (same as calling setVar() three times)
_satellite.setVar({ 'title': 'Blinding Light', 'category': 'Game', 'genre': 'Tower defense' });

// Retrieve each value
_satellite.getVar('title'); // Blinding Light
_satellite.getVar('category'); // Game
_satellite.getVar('genre'); // Tower defense
```
