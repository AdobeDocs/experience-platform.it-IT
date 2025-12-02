---
title: environment
description: L’ambiente di build attualmente utilizzato dalla proprietà tag.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 6%

---

# `environment`

L&#39;oggetto `_satellite.environment` indica l&#39;ambiente di build attualmente in uso dalla proprietà tag.

```js
readonly _satellite.environment: Environment
```

## Campi disponibili

I campi seguenti sono disponibili quando si chiama questo oggetto.

```json
{
  "id": "EN6b2...d6ff2",
  "stage": "production"
}
```

| Nome | Tipo | Descrizione |
|---|---|---|
| **`id`** | `string` | L’identificatore univoco dell’ambiente. È possibile individuare l&#39;ID ambiente selezionando l&#39;icona **[!UICONTROL Install]** in [[!UICONTROL Environments]](/help/tags/ui/publishing/environments.md) nell&#39;interfaccia utente dei tag. |
| **`stage`** | `development \| staging \| production` | Il tipo di ambiente. |
