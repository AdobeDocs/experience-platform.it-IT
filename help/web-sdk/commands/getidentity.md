---
title: getIdentity
description: Ottenere l’identità di un visitatore senza inviare i dati dell’evento.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

Il `getIdentity` consente di ottenere un ID visitatore senza inviare i dati dell’evento. Quando si esegue `sendEvent` Web SDK ottiene automaticamente l’identità del visitatore, se non è già presente.

Se hai bisogno di chiamate separate per generare un ID visitatore e inviare dati, puoi utilizzare questo comando.

## Ottenere l’identità tramite l’estensione tag Web SDK

L’estensione tag Web SDK non offre questo comando tramite l’interfaccia utente dell’estensione tag. Utilizza l’editor di codice personalizzato utilizzando la sintassi della libreria JavaScript.

## Ottenere l’identità tramite la libreria JavaScript dell’SDK web

Esegui il `getIdentity` quando si chiama l’istanza configurata dell’SDK per web. Durante la configurazione di questo comando sono disponibili le seguenti opzioni:

* **`namespaces`**: array di spazi dei nomi. Il valore predefinito è `["ECID"]`. I valori validi includono `["ECID"]`, `null`, o `undefined`.
* **`edgeConfigOverrides`**: un [oggetto di sostituzione della configurazione dello stream di dati](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## Oggetto di risposta

Se decidi di [gestire le risposte](command-responses.md) con questo comando, nell’oggetto di risposta sono disponibili le seguenti proprietà:

* **`identity.ECID`**: stringa contenente l’identificatore ECID del visitatore.
* **`edge.regionID`**: numero intero che rappresenta l’area della rete Edge interessata dal browser durante l’acquisizione di un’identità. È lo stesso dell’hint di posizione Audience Manager legacy.
