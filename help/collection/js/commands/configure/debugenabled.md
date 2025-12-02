---
title: debugEnabled
description: Utilizza il codice per abilitare le funzionalità di debug in Web SDK.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `debugEnabled`

La proprietà `debugEnabled` consente di abilitare o disabilitare il debug utilizzando il codice Web SDK. È uno dei modi disponibili per abilitare [il debug](/help/collection/use-cases/debugging.md). L’abilitazione del debug all’interno dell’implementazione può essere più pratica di altri metodi durante lo sviluppo di siti web quando si desidera sempre che il debug sia abilitato. Questo metodo di debug lo abilita per tutti i visitatori, pertanto non è consigliato per le pagine di produzione. Consulta la pagina del caso d&#39;uso [Debug](/help/collection/use-cases/debugging.md) per ulteriori modi per abilitare il debug.

Impostare il valore booleano `debugEnabled` su `true` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione di SDK, per impostazione predefinita viene utilizzato il valore `false`.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

## Abilitare il debug tramite l’estensione tag Web SDK

Non sono disponibili opzioni di debug per l’utilizzo nativo dell’estensione tag Web SDK. Utilizza un [metodo di debug alternativo](/help/collection/use-cases/debugging.md) durante la configurazione della proprietà tag.
