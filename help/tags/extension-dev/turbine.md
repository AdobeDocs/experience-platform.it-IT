---
title: Variabile libera “turbine”
description: Scopri l’oggetto turbine, una variabile gratuita che fornisce informazioni e utility specifiche per il runtime di tag Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 58%

---

# Variabile libera “turbine”

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’oggetto `turbine` rappresenta una “variabile libera” nell’ambito dei moduli libreria dell’estensione. Fornisce informazioni e utility specifiche per il runtime di tag Adobe Experience Platform ed è sempre disponibile per i moduli della libreria senza utilizzare `require()`.

## [!DNL buildInfo]

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` è un oggetto contenente informazioni sulla build della libreria di runtime di tag corrente.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z",
    environment: "development"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `turbineVersion` | La versione di [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilizzata all&#39;interno della libreria corrente. |
| `turbineBuildDate` | La data di creazione della versione di [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilizzata all&#39;interno del contenitore in formato ISO 8601. |
| `buildDate` | La data di creazione della libreria corrente in formato ISO 8601. |
| `environment` | L&#39;ambiente per il quale è stata generata la libreria. I valori accettati sono `development`, `staging` e `production`. |


## [!DNL debugEnabled]

Se il debug dei tag è attualmente abilitato.

Se intendi semplicemente registrare i messaggi, probabilmente non dovrai utilizzarlo. Al contrario, registra sempre i messaggi utilizzando `turbine.logger` per garantire che vengano stampati sulla console solo quando è abilitato il debug dei tag.

### [!DNL getDataElementValue]

```js
console.log(turbine.getDataElementValue(dataElementName));
```

Restituisce il valore di un elemento dati.

### [!DNL getExtensionSettings] {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

Restituisce l’ultimo oggetto impostazioni salvato dalla vista di [configurazione delle estensioni](./configuration.md).

I valori negli oggetti impostazioni restituiti potrebbero provenire da elementi di dati. Per questo motivo, se richiami `getExtensionSettings()` in momenti diversi potresti ottenere risultati diversi, dovuti all’eventuale cambiamento dei valori degli elementi dati. Per ottenere i valori più aggiornati, attendi il più a lungo possibile prima di chiamare `getExtensionSettings()`.

### [!DNL getHostedLibFileUrl] {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

La proprietà [hostingLibFiles](./manifest.md) può essere definita all&#39;interno del manifesto dell&#39;estensione per ospitare vari file insieme alla libreria di runtime del tag. Questo modulo restituisce l’URL in cui è ospitato il file libreria specificato.

### [!DNL getSharedModule] {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Recupera un modulo condiviso da un&#39;altra estensione. Se non viene trovato alcun modulo corrispondente, verrà restituito `undefined`. Per ulteriori informazioni sui moduli condivisi, consulta [Implementazione di moduli condivisi](./web/shared.md).

### [!DNL logger]

```js
turbine.logger.error('Error!');
```

L&#39;utilità di registrazione viene utilizzata per registrare i messaggi nella console. I messaggi vengono mostrati nella console solo se il debug è attivato dall’utente. Per attivare il debug, si consiglia di utilizzare l’estensione [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda) oppure [ Launch e l’estensione DTM Switch](https://chrome.google.com/webstore/detail/adobe-dtm-switch/nlgdemkdapolikbjimjajpmonpbpmipk) di Chrome. In alternativa, l’utente può eseguire il seguente comando `_satellite.setDebug(true)` all’interno della console per sviluppatori del browser. Il logger dispone dei seguenti metodi:

* `logger.log(message: string)`: registra un messaggio nella console.
* `logger.info(message: string)`: registra un messaggio informativo nella console.
* `logger.warn(message: string)`: registra un messaggio di avvertenza nella console.
* `logger.error(message: string)`: registra un messaggio di errore nella console.
* `logger.debug(message: string)`: registra un messaggio di debug nella console. (Visibile solo se la registrazione `verbose` è abilitata nella console del browser.)

### [!DNL onDebugChanged]

Trasmettendo una funzione di callback in `turbine.onDebugChanged`, i tag richiameranno il callback ogni volta che il debug viene attivato. I tag trasmettono un valore booleano alla funzione di callback che sarà true se il debug è stato abilitato o false se il debug è stato disattivato.

Se intendi semplicemente registrare i messaggi, probabilmente non dovrai utilizzarlo. Al contrario, i messaggi di registro che utilizzano `turbine.logger` e garantiscono la stampa dei messaggi nella console solo quando è abilitato il debug dei tag.

### [!DNL propertySettings] {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Un oggetto contenente le seguenti impostazioni definite dall&#39;utente per la proprietà della libreria runtime di tag corrente:

* `propertySettings.domains: Array<String>`

   Array di domini coperti dalla proprietà.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   Questa impostazione non dovrebbe interessare gli sviluppatori di estensioni.
