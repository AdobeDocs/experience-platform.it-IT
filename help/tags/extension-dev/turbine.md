---
title: Variabile libera “turbine”
description: Scopri l’oggetto turbine, una variabile libera che fornisce informazioni e utility specifiche per il runtime dei tag di Adobe Experience Platform.
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: 57b4d11d0a7fd587dc45066737726a52533e33f0
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 91%

---

# Variabile libera “turbine”

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’oggetto `turbine` rappresenta una “variabile libera” nell’ambito dei moduli libreria dell’estensione. Fornisce informazioni e utility specifiche per il runtime dei tag di Adobe Experience Platform ed è sempre disponibile per i moduli libreria senza che sia necessario utilizzare `require()`.

## [!DNL buildInfo]

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` è un oggetto che contiene informazioni sulla versione attuale della libreria runtime dei tag.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `turbineVersion` | La versione di [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilizzata all&#39;interno della libreria corrente. |
| `turbineBuildDate` | La data di creazione della versione di [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilizzata all&#39;interno del contenitore in formato ISO 8601. |
| `buildDate` | La data di creazione della libreria corrente in formato ISO 8601. |


## [!DNL environment]

```js
console.log(turbine.environment.stage);
```

`turbine.environment` è un oggetto contenente informazioni sull&#39;ambiente in cui viene distribuita la libreria.

```js
{
    id: "EN123456...",
    stage: "development"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID dell&#39;ambiente. |
| `stage` | L&#39;ambiente per il quale è stata generata la libreria. I valori accettati sono `development`, `staging` e `production`. |


## [!DNL debugEnabled]

Specifica se il debug dei tag è attualmente abilitato.

Se intendi semplicemente registrare i messaggi, probabilmente non dovrai utilizzarlo. Piuttosto, per registrare i messaggi utilizza sempre `turbine.logger` per assicurarti che i messaggi vengano riportati nella console solo quando è abilitato il debug dei tag.

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

I valori negli oggetti impostazioni restituiti potrebbero provenire da elementi di dati. Per questo motivo, se richiami `getExtensionSettings()` in momenti diversi potresti ottenere risultati diversi, dovuti all’eventuale cambiamento dei valori degli elementi dati. Per ottenere i valori più aggiornati, attendi il più tardi possibile prima di richiamare `getExtensionSettings()`.

### [!DNL getHostedLibFileUrl] {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

La proprietà [hostedLibFiles](./manifest.md) può essere definita nel manifesto dell’estensione in modo da includere vari file oltre alla libreria runtime dei tag. Questo modulo restituisce l’URL in cui è ospitato il file libreria specificato.

### [!DNL getSharedModule] {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Recupera un modulo che è stato condiviso da un’altra estensione. Se non viene trovato alcun modulo corrispondente, verrà restituito `undefined`. Per ulteriori informazioni sui moduli condivisi, consulta [Implementazione di moduli condivisi](./web/shared.md).

### [!DNL logger]

```js
turbine.logger.error('Error!');
```

Utility di registrazione utilizzata per registrare i messaggi nella console. I messaggi vengono mostrati nella console solo se il debug è attivato dall’utente. Il modo consigliato per attivare il debug è quello di utilizzare il [debugger Adobe Experience Cloud](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda). In alternativa, è possibile eseguire il comando `_satellite.setDebug(true)` seguente nella console di sviluppo del browser. Il logger dispone dei seguenti metodi:

* `logger.log(message: string)`: registra un messaggio nella console.
* `logger.info(message: string)`: registra un messaggio informativo nella console.
* `logger.warn(message: string)`: registra un messaggio di avvertenza nella console.
* `logger.error(message: string)`: registra un messaggio di errore nella console.
* `logger.debug(message: string)`: registra un messaggio di debug nella console. (Visibile solo se la registrazione `verbose` è abilitata nella console del browser.)

### [!DNL onDebugChanged]

Quando si trasmette una funzione di callback in `turbine.onDebugChanged`, i tag richiameranno il callback ogni volta che viene attivato il debug. I tag trasmetteranno un valore booleano alla funzione di callback che sarà true se il debug è abilitato o false se è disabilitato.

Se intendi semplicemente registrare i messaggi, probabilmente non dovrai utilizzarlo. Piuttosto, per registrare i messaggi utilizza sempre `turbine.logger` e i tag faranno sì che i messaggi vengano riportati nella console solo quando è abilitato il debug di tag.

### [!DNL propertySettings] {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Oggetto contenente le seguenti impostazioni definite dall’utente per la proprietà della libreria runtime attuale di tag:

* `propertySettings.domains: Array<String>`

   Array di domini coperti dalla proprietà.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   Questa impostazione non dovrebbe interessare gli sviluppatori di estensioni.
