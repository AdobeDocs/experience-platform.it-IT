---
title: Debug in Adobe Experience Platform Web SDK
description: Scopri come attivare/disattivare le funzionalità di debug nell’SDK per web di Experience Platform.
keywords: debugging sdk Web;debugging;configurare;comando di configurazione;comando di debug;edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: c0e2d01bd21405f07f4857e1ccf45dd0e4d0f414
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# Eseguire il debug di

Quando il debug è abilitato, l’SDK invia messaggi alla console del browser che possono essere utili per eseguire il debug dell’implementazione e comprendere il comportamento dell’SDK.

Il debug è disattivato per impostazione predefinita, ma può essere attivato in tre modi diversi:

* `configure` command
* `setDebug` command
* parametro della stringa di query

## Attivazione del debugging con il comando Configura

Durante la configurazione dell&#39;SDK tramite il comando `configure`, abilita il debug impostando l&#39;opzione `debugEnabled` su `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>Questo consente il debug di tutti gli utenti della pagina web anziché solo del browser personale.

## Attivazione del debugging con il comando Debug

Attiva il debug con un comando `debug` separato come segue:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Se si preferisce non modificare il codice sulla pagina web o non si desidera che i messaggi di log vengano prodotti per tutti gli utenti del sito web, questo è particolarmente utile perché è possibile eseguire il comando `debug` nella console JavaScript del browser in qualsiasi momento.

## Attivazione del debugging con un parametro della stringa di query

Attiva il debug impostando un parametro della stringa di query `alloy_debug` su `true` o `false` come segue:

```HTTP
http://example.com/?alloy_debug=true
```

Simile al comando `debug`, se preferisci non modificare il codice sulla pagina web o non vuoi produrre messaggi di registrazione per tutti gli utenti del sito web, questo è particolarmente utile perché puoi impostare il parametro della stringa query quando carichi la pagina web all’interno del browser.

## Priorità e durata

Quando il debug viene impostato tramite il parametro `debug` del comando o della stringa di query, sostituisce qualsiasi opzione `debug` impostata nel comando `configure`. In questi due casi, il debug rimane attivato anche per la durata della sessione. In altre parole, se si abilita il debug utilizzando il comando di debug o il parametro della stringa di query, rimane abilitato fino a una delle seguenti operazioni:

* Fine della sessione
* Esegui il comando `debug`
* Impostare nuovamente il parametro della stringa query

## Recupero delle informazioni sulla libreria

Spesso è utile accedere ad alcuni dei dettagli della libreria caricata sul sito web. A questo scopo, esegui il comando `getLibraryInfo` come segue:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

Attualmente, l&#39;oggetto `libraryInfo` fornito contiene le seguenti proprietà:

* `version` Questa è la versione della libreria caricata. Ad esempio, se la versione della libreria caricata fosse 1.0.0, il valore sarebbe `1.0.0`. Quando la libreria viene eseguita all&#39;interno dell&#39;estensione tag (denominata &quot;AEP Web SDK&quot;), la versione è la versione della libreria e la versione dell&#39;estensione tag è unita con un segno &quot;+&quot;. Ad esempio, se la versione della libreria fosse 1.0.0 e l&#39;estensione tag fosse 1.2.0, il valore sarebbe `1.0.0+1.2.0`.
