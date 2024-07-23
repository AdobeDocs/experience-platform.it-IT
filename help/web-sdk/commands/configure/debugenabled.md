---
title: debugEnabled
description: Utilizza il codice per abilitare le funzionalità di debug nell’SDK per web.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

La proprietà `debugEnabled` consente di abilitare o disabilitare il debug utilizzando il codice Web SDK. È uno dei modi disponibili per abilitare [il debug](../../use-cases/debugging.md). L’abilitazione del debug all’interno dell’implementazione può essere più pratica di altri metodi durante lo sviluppo di siti web quando si desidera sempre che il debug sia abilitato. Questo metodo di debug lo abilita per tutti i visitatori, pertanto non è consigliato per le pagine di produzione.

Consulta la pagina del caso d&#39;uso [Debug](../../use-cases/debugging.md) per ulteriori modi per abilitare il debug.

## Abilitare il debug tramite l’estensione tag Web SDK

Non sono disponibili opzioni di debug in modalità nativa tramite l’estensione tag Web SDK. Utilizzare un [metodo di debug alternativo](../../use-cases/debugging.md).

## Abilitare il debug utilizzando la libreria JavaScript dell’SDK per web

Impostare il valore booleano `debugEnabled` su `true` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione dell&#39;SDK, per impostazione predefinita viene impostato su `false`.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```
