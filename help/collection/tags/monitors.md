---
title: _monitoraggi
description: Aggiungi i listener di eventi per eseguire il debug dell’implementazione tag.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# `_monitors`

L&#39;oggetto `_satellite._monitors` consente di creare listener di eventi ed eseguire codice personalizzato quando la libreria rileva una regola attivata. Il suo utilizzo principale consiste nell’assistenza durante il debug dell’implementazione per garantire che le regole vengano attivate correttamente.

>[!IMPORTANT]
>
>Questo oggetto è solo a scopo di debug. Non collegare la logica di produzione a questo oggetto. La disponibilità di proprietà o nomi all’interno di questo oggetto può essere modificata da Adobe in qualsiasi momento.

```ts
_satellite._monitors?: {
  ruleTriggered(event: { rule: Rule }): void;
  ruleCompleted(event: { rule: Rule }): void;
  ruleConditionFailed(event: { rule: Rule; condition: Condition }): void;
}[];
```

È possibile ascoltare i seguenti tipi di evento:

## `ruleTriggered`

Questa funzione di callback viene attivata quando un evento attiva una regola prima dell&#39;elaborazione delle condizioni e azioni della regola. Se questa funzione viene attivata, `ruleCompleted` o `ruleConditionFailed` viene attivato poco dopo (reciprocamente esclusivo).

## `ruleCompleted`

La funzione di callback `ruleCompleted` viene attivata dopo `ruleTriggered` quando i criteri di condizione della regola hanno esito positivo e tutte le azioni della regola vengono eseguite.

## `ruleConditionFailed`

La funzione di callback `ruleConditionFailed` viene attivata dopo `ruleTriggered` quando almeno una delle condizioni della regola non riesce.

## `Rule` oggetto

Ogni funzione di callback espone un oggetto `Rule` che fornisce informazioni sulla regola stessa.

```ts
type Rule = {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}
```

| Nome | Tipo | Descrizione |
|---|---|---|
| **`id`** | `string` | Identificatore univoco della regola. |
| **`name`** | `string` | Nome descrittivo della regola. |
| **`events`** | `Event[]` | Array di eventi configurati per attivare la regola. |
| **`conditions`** | `Condition[]` | Matrice di condizioni configurata per attivare la regola. |
| **`actions`** | `Action[]` | Matrice di azioni configurata per l&#39;esecuzione quando la regola viene attivata. |

## Esempio

Aggiungi il seguente frammento di codice al tuo HTML nel tag `<head>` prima di chiamare il caricatore della libreria di tag:

```html
<script>
  window._satellite ??= {};
  window._satellite._monitors ??= [];
  window._satellite._monitors.push({
    ruleTriggered(event) { console.log('Rule triggered', event.rule);},
    ruleCompleted(event) { console.log('Rule completed', event.rule);},
    ruleConditionFailed(event) { console.log('Rule condition failed', event.rule, event.condition);}
  });
</script>
<script src="https://assets.adobedtm.com/.../launch-EN...js" async></script>
```

Poiché la libreria di tag non è ancora caricata in questo punto della pagina, viene creato l&#39;oggetto `_satellite` iniziale e viene inizializzato un array su `_satellite._monitors`. Lo script aggiunge quindi un oggetto di monitoraggio a tale array.

Quando si utilizzano i monitor, tenere presenti i suggerimenti riportati di seguito.

* Si noti che questi messaggi di debug utilizzano `console.log` invece di [`_satellite.logger`](logger.md) perché gli hook vengono creati prima del caricamento della libreria di tag.
* L&#39;esempio di codice include tutte e tre le funzioni di callback, ma non sono campi obbligatori. Puoi includere solo gli hook desiderati durante il debug delle regole sul sito.
* Sono consentiti più monitor, anche per gli stessi eventi. Se utilizzi più monitor per un singolo evento, l’ordine di chiamata non è garantito.
* Assicurati di creare `_monitors` _prima_ di caricare la libreria di tag. Se crei questi hook dopo il caricamento della libreria, vengono rilevate solo le regole che si attivano da quel momento in poi.
