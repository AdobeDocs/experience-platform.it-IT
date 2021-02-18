---
title: Debug in Adobe Experience Platform Web SDK
description: Scoprite come attivare/disattivare le funzionalità di debug nell’SDK Web per Experience Platform .
keywords: debugging web sdk;debugging;configure;configure command;debug command;edgeConfigId;setDebug;debugEnabled;debug;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Eseguire il debug di

Quando il debug è abilitato, l’SDK invia messaggi alla console del browser che possono essere utili per eseguire il debug dell’implementazione e comprendere il funzionamento dell’SDK. Il debug comporta inoltre una convalida sincrona lato server dei dati raccolti rispetto allo schema configurato.

Il debug è disattivato per impostazione predefinita, ma può essere attivato in tre modi diversi:

* `configure` command
* `setDebug` command
* parametro stringa query

## Attivazione del debug con il comando Configura

Per configurare l&#39;SDK con il comando `configure`, abilita il debug impostando l&#39;opzione `debugEnabled` su `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>Questo consente il debug per tutti gli utenti della pagina Web anziché solo per il browser personale.

## Attivazione del debug con il comando Debug

Attiva il debug con un comando `debug` separato, come segue:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Se si preferisce non modificare il codice della pagina Web o non si desidera che i messaggi di registrazione vengano prodotti per tutti gli utenti del sito Web, ciò è particolarmente utile perché è possibile eseguire il comando `debug` nella console JavaScript del browser in qualsiasi momento.

## Attivazione del debug con un parametro di stringa di query

Per attivare o disattivare il debug, impostare un parametro di stringa di query `alloy_debug` su `true` o `false` come segue:

```HTTP
http://example.com/?alloy_debug=true
```

Simile al comando `debug`, se si preferisce non modificare il codice della pagina Web o non si desidera che i messaggi di registrazione vengano prodotti per tutti gli utenti del sito Web, questo è particolarmente utile perché è possibile impostare il parametro della stringa di query quando si carica la pagina Web all&#39;interno del browser.

## Priorità e durata

Quando il debug viene impostato tramite il parametro `debug` del comando o della stringa di query, sostituisce qualsiasi opzione `debug` impostata nel comando `configure`. In questi due casi, anche il debug rimane attivato per tutta la durata della sessione. In altre parole, se si abilita il debug utilizzando il comando di debug o il parametro della stringa di query, rimane attivato fino a quando non viene eseguita una delle operazioni seguenti:

* Fine della sessione
* Eseguire il comando `debug`
* Impostare di nuovo il parametro della stringa di query

## Recupero delle informazioni sulla libreria

Spesso è utile accedere ad alcuni dei dettagli della libreria caricata sul sito Web. A tal fine, eseguite il comando `getLibraryInfo` come segue:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

Attualmente, l&#39;oggetto `libraryInfo` fornito contiene le proprietà seguenti:

* `version` Questa è la versione della libreria caricata. Ad esempio, se la versione della libreria caricata fosse 1.0.0, il valore sarebbe `1.0.0`.
