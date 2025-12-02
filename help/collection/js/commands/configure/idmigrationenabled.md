---
title: idMigrationEnabled
description: Consente al Web SDK di leggere i cookie AMCV.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `idMigrationEnabled`

La proprietà `idMigrationEnabled` consente al Web SDK di leggere i cookie AMCV impostati da implementazioni Adobe Experience Cloud precedenti. Se l’organizzazione aggiorna l’implementazione al Web SDK, questa impostazione consente una transizione più fluida al servizio Adobe Experience Cloud ID corrente. Questa impostazione è utile per evitare un netto aumento dei visitatori univoci durante l&#39;aggiornamento al Web SDK.

Se l’organizzazione esegue una nuova implementazione di Web SDK, l’abilitazione di questa impostazione non ha alcun impatto sulla raccolta dei dati o sull’identificazione dei visitatori. Non ci sono svantaggi a lasciarla abilitata per tutte le implementazioni.

Impostare il valore booleano `idMigrationEnabled` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione del Web SDK, per impostazione predefinita viene utilizzato `true`. Imposta questa proprietà se vuoi disabilitare la capacità di leggere i cookie AMCV impostati dall&#39;API visitatore. La maggior parte delle organizzazioni non deve impostare questa proprietà.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Abilitare la migrazione degli ID visitatore tramite l’estensione tag Web SDK

Queste impostazioni possono essere configurate nell&#39;estensione tag Web SDK utilizzando [Impostazioni di configurazione identità](/help/tags/extensions/client/web-sdk/configure/identity.md).
