---
title: Installare l’SDK per web utilizzando il pacchetto NPM
description: Utilizza un pacchetto NPM per installare e fare riferimento alla libreria SDK Web.
exl-id: 4c70ec5d-33fd-4ef7-ba9e-5b92ff6c3e86
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Installare l’SDK per web utilizzando il pacchetto NPM

Adobe Experience Platform Web SDK è disponibile come pacchetto [NPM](https://www.npmjs.com). L’installazione del pacchetto NPM consente di avere il controllo del processo di build per la libreria JavaScript di Adobe Experience Platform Web SDK. Il pacchetto NPM espone i moduli EcmaScript versione 5 o EcmaScript versione 2015 (ES6) destinati a essere eseguiti nel browser.

```bash
npm install @adobe/alloy
```

Il pacchetto NPM di Adobe Experience Platform Web SDK espone una funzione `createInstance`. L’opzione name passata alla funzione controlla il prefisso utilizzato nella registrazione. Di seguito sono riportati alcuni esempi di utilizzo del pacchetto.

## Utilizzo del pacchetto come modulo ECMAScript 2015 (ES6)

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Il pacchetto NPM si basa sui moduli CommonJS; pertanto, quando utilizzi un bundler, assicurati che il bundler supporti i moduli CommonJS. Alcuni bundle, ad esempio [Rollup](https://rollupjs.org), richiedono un [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) che fornisca supporto CommonJS.

## Utilizzo del pacchetto come modulo ECMAScript 5

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```
