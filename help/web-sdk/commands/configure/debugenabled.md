---
title: debugEnabled
description: Utilizza il codice per abilitare le funzionalità di debug nell’SDK per web.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

Il `debugEnabled` consente di abilitare o disabilitare il debug utilizzando il codice Web SDK. È uno dei modi disponibili per abilitare [debug](../../use-cases/debugging.md). L’abilitazione del debug all’interno dell’implementazione può essere più pratica di altri metodi durante lo sviluppo di siti web quando si desidera sempre che il debug sia abilitato. Questo metodo di debug lo abilita per tutti i visitatori, pertanto non è consigliato per le pagine di produzione.

Consulta la [Debug](../../use-cases/debugging.md) caso d’uso per altri modi di abilitare il debug.

## Abilitare il debug tramite l’estensione tag Web SDK

Non sono disponibili opzioni di debug in modalità nativa tramite l’estensione tag Web SDK. Utilizza un [metodo di debug alternativo](../../use-cases/debugging.md).

## Abilitare il debug utilizzando la libreria JavaScript di Web SDK

Imposta il `debugEnabled` booleano a `true` durante l&#39;esecuzione di `configure` comando. Se ometti questa proprietà durante la configurazione dell’SDK, per impostazione predefinita viene `false`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```
