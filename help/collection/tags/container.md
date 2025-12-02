---
title: _contenitore
description: Visualizza l’intero contenitore di tag in un singolo oggetto.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# `_container`

L&#39;oggetto `_satellite._container` contiene la configurazione completa e il contesto di runtime della proprietà tag caricata sulla pagina. Tutte le informazioni, ad esempio regole, elementi dati, estensioni e ambienti, sono disponibili all’interno di questo oggetto. Il suo utilizzo principale consiste nell’assistere nel debug dell’implementazione in modo da poter vedere esattamente quale logica viene esposta o pubblicata.

```ts
readonly _satellite._container: {
  buildInfo: BuildInfo;
  company: Company;
  dataElements: { [name: string]: DataElement };
  environment: Environment;
  extensions: { [name: string]: Extension };
  property: Property;
  rules: Rule[];
}
```

>[!IMPORTANT]
>
>Questo oggetto è solo a scopo di debug. Non collegare la logica di produzione a questo oggetto, non fare riferimento a questo oggetto nell&#39;implementazione e non modificare i valori all&#39;interno di questo oggetto. La disponibilità di proprietà o nomi all’interno di questo oggetto può essere modificata da Adobe in qualsiasi momento.

## Campi disponibili

I seguenti oggetti sono disponibili come riferimento:

```json
{
  "buildInfo": {
    "minified": true,
    "buildDate": "YYYY-06-13T01:22:12Z"
  },
  "company": {
    "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
    "dynamicCdnEnabled": true,
    "cdnAllowList": [ "assets.adobedtm.com" ]
  },
  "dataElements": { ... },
  "environment": {
    "id": "EN6b2...d6ff2",
    "stage": "production"
  },
  "extensions": {
    "adobe-alloy": { ... },
    "core": { ... },
    "common-web-sdk-plugins": { ... }
  },
  "property": {
    "name": "Example tag property",
    "settings": {
      "domains": [ "example.com" ],
      "undefinedVarsReturnEmpty": false,
      "ruleComponentSequencingEnabled": true
    },
    "id": "PR845...6cf92"
  },
  "rules": [ { ... } ]
}
```

## `buildInfo`

L&#39;oggetto `_satellite._container.buildInfo` contiene una copia di [`_satellite.buildInfo`](buildinfo.md).

```ts
readonly _satellite._container.buildInfo: {
  minified: boolean;
  buildDate: string;
  turbineBuildDate: string;
  turbineVersion: string;
}
```

## `company`

L&#39;oggetto `_satellite._container.company` contiene una copia di [`_satellite.company`](company.md).

```ts
readonly _satellite._container.company: {
  orgId: string;
  dynamicCdnEnabled: boolean;
  cdnAllowList: string[];
}
```

## `dataElements`

L&#39;oggetto `_satellite._container.dataElements` fornisce un riferimento di tutti gli elementi dati all&#39;interno della proprietà tag.

```ts
readonly _satellite._container.dataElements: {
  [name: string]: {
    modulePath: string;
    settings: Settings; // Varies by data element type
  }
}
```

Ogni elemento dati include le seguenti proprietà:

| Nome | Tipo | Descrizione |
|---|---|---|
| **`modulePath`** | `string` | Percorso del file JavaScript che determina la logica di quel tipo di elemento dati. |
| **`settings`** | `Settings` | Impostazioni dell’elemento dati. Le proprietà all’interno di questo oggetto dipendono dal tipo di elemento dati. |

## `environment`

L&#39;oggetto `_satellite._container.environment` contiene una copia di [`_satellite.environment`](environment.md).

```ts
readonly _satellite._container.environment: {
  id: string;
  stage: string;
}
```

## `extensions`

L&#39;oggetto `_satellite._container.extensions` elenca tutte le estensioni pubblicate nella proprietà tag.

```ts
readonly _satellite._container.extensions: {
  [name: string]: {
    displayName: string;
    hostedLibFilesUrl: string;
    modules: Modules; // Extension-specific module definitions
  }
}
```

Ogni estensione include le seguenti proprietà:

| Nome | Tipo | Descrizione |
|---|---|---|
| **`displayName`** | `string` | Il nome descrittivo dell’estensione. |
| **`hostedLibFilesUrl`** | `string` | Posizione sulla rete CDN in cui risiede l’estensione. |
| **`modules`** | `Modules` | La logica JavaScript per tutti gli eventi, le azioni, le condizioni e gli elementi dati utilizzati dall’estensione. Il contenuto di questo oggetto è diverso per ogni estensione. |

## `property`

L&#39;oggetto `_satellite._container.property` fornisce informazioni sulla proprietà tag stessa.

```ts
readonly _satellite._container.property: {
  id: string;
  name: string;
  settings: {
    domains: string[];
    ruleComponentSequencingEnabled: boolean;
    undefinedVarsReturnEmpty: boolean;
  };
}
```

| Nome | Tipo | Descrizione |
|---|---|---|
| **`id`** | `string` | Identificatore univoco della proprietà tag. |
| **`name`** | `string` | Nome descrittivo della proprietà tag. |
| **`settings`** | `PropertySettings` | Impostazioni per questa proprietà. Vedi la tabella seguente. |

| Nome impostazione | Tipo | Descrizione |
|---|---|---|
| **`domains`** | `string[]` | I domini configurati per la proprietà, come impostato durante [la configurazione di una proprietà tag](/help/tags/ui/administration/companies-and-properties.md). |
| **`ruleComponentSequencingEnabled`** | `boolean` | Determina se la casella di controllo **[!UICONTROL Run rule components in sequence]** è abilitata durante la configurazione della proprietà tag. |
| **`undefinedVarsReturnEmpty`** | `boolean` | Determina se la casella di controllo **[!UICONTROL Return an empty string for undefined data elements]** è abilitata durante la configurazione della proprietà tag. |

## `_container.rules`

L&#39;array di oggetti `rules` fornisce un riferimento di tutte le regole all&#39;interno della proprietà tag.

```ts
readonly _satellite._container.rules: {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}[]
```

Ogni regola contiene i campi seguenti:

| Nome | Tipo | Descrizione |
|---|---|---|
| **`id`** | `string` | Identificatore univoco della regola. |
| **`name`** | `string` | Nome descrittivo della regola. |
| **`events`** | `Event[]` | Array di eventi configurati per attivare la regola. |
| **`conditions`** | `Condition[]` | Matrice di condizioni configurata per attivare la regola. |
| **`actions`** | `Action[]` | Matrice di azioni configurata per l&#39;esecuzione quando la regola viene attivata. |
