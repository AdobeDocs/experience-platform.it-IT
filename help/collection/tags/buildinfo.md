---
title: buildInfo
description: Ottieni informazioni sulla build del tag implementata sul tuo sito.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# `buildInfo`

L&#39;oggetto `_satellite.buildInfo` contiene informazioni sulla build della proprietà tag implementata. Questo oggetto è più utile quando esegui il debug di build frequenti per assicurarti di utilizzare la versione più recente.

```ts
readonly _satellite.buildInfo: BuildInfo
```

## Campi disponibili

I campi seguenti sono disponibili quando si chiama questo oggetto.

```json
{
  "minified": true,
  "buildDate": "YYYY-06-13T01:22:12Z",
  "turbineBuildDate": "YYYY-08-22T17:32:44Z",
  "turbineVersion": "28.0.0"
}
```

| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **`minified`** | `boolean` | Indica se la libreria è minimizzata. Le build di produzione sono in genere ridotte (`true`), mentre le build di sviluppo e di staging non sono in genere (`false`). |
| **`buildDate`** | `string (ISO-8601 datetime)` | La data e l’ora in cui il file JavaScript è stato creato e pubblicato. |
| **`turbineBuildDate`** | `string (ISO-8601 datetime)` | [Turbine](https://github.com/adobe/reactor-turbine) è il motore di Adobe che elabora le regole di tag e delega la logica alle estensioni di tag. Questo campo contiene la data e l’ora della build Turbine utilizzata per pubblicare la proprietà tag. |
| **`turbineVersion`** | `string` | Versione di Turbine utilizzata per generare e pubblicare la proprietà tag. |

Informazioni simili sono contenute anche in `_satellite._container.buildInfo`. Per ulteriori informazioni, vedere [`_container`](container.md).
