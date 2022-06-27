---
title: Debug in Adobe Experience Platform Web SDK
description: Scopri come attivare/disattivare le funzionalità di debug nell’SDK per web di Experience Platform.
keywords: debugging sdk Web;debugging;configurare;comando di configurazione;comando di debug;edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: c1e6b1519bc40e7d36bd83dc49e442d3d5583fed
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---

# Eseguire il debug di

Quando il debug è abilitato, l’SDK invia messaggi alla console del browser che possono essere utili per eseguire il debug dell’implementazione e comprendere il comportamento dell’SDK.

Il debug è disattivato per impostazione predefinita, ma può essere attivato in quattro modi diversi:

* `configure` command
* `setDebug` command
* parametro della stringa di query
* Attivazione del debug in Adobe Experience Platform Debugger. Adobe Experience Platform è uno strumento potente che esamina le pagine web e ti aiuta a eseguire il debug dei problemi di implementazione con i prodotti Experience Cloud. Adobe Experience Platform Debugger è disponibile sia come [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) e [Firefox](https://addons.mozilla.org/it/firefox/addon/adobe-experience-platform-dbg/) estensione. Il debug può essere abilitato dalla scheda di configurazione della sezione AEP Web SDK .

![](../images/enable-debugging.png)

## Attivazione del debugging con il comando Configura

Quando configuri l&#39;SDK utilizzando la variabile `configure` attiva il debug impostando il comando `debugEnabled` opzione per `true`.

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

Attiva/disattiva il debug con un altro `debug` come segue:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Se preferisci non modificare il codice sulla pagina web o non desideri che i messaggi di registrazione vengano prodotti per tutti gli utenti del sito web, questo è particolarmente utile perché puoi eseguire il `debug` nella console JavaScript del browser in qualsiasi momento.

## Attivazione del debugging con un parametro della stringa di query

Attiva/disattiva il debug impostando un `alloy_debug` parametro della stringa di query a `true` o `false` come segue:

```HTTP
http://example.com/?alloy_debug=true
```

Simile al `debug` , se preferisci non modificare il codice sulla pagina web o non desideri generare messaggi di registrazione per tutti gli utenti del sito web, questo è particolarmente utile perché puoi impostare il parametro della stringa query quando carichi la pagina web all&#39;interno del browser.

## Priorità e durata

Quando il debug viene impostato tramite la `debug` parametro della stringa di comando o di query sostituisce qualsiasi `debug` impostato in `configure` comando. In questi due casi, il debug rimane attivato anche per la durata della sessione. In altre parole, se si abilita il debug utilizzando il comando di debug o il parametro della stringa di query, rimane abilitato fino a una delle seguenti operazioni:

* Fine della sessione
* Esegui il `debug` command
* Impostare nuovamente il parametro della stringa query

## Recupero delle informazioni sulla libreria

Spesso è utile accedere ad alcuni dei dettagli della libreria caricata sul sito web. A questo scopo, esegui la `getLibraryInfo` come segue:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

Attualmente, il `libraryInfo` l&#39;oggetto contiene le proprietà seguenti:

* `version`: Questa è la versione della libreria caricata. Ad esempio, se la versione della libreria caricata fosse 1.0.0, il valore sarebbe `1.0.0`. Quando la libreria viene eseguita all&#39;interno dell&#39;estensione tag (denominata &quot;AEP Web SDK&quot;), la versione è la versione della libreria e la versione dell&#39;estensione tag è unita con un segno &quot;+&quot;. Ad esempio, se la versione della libreria fosse 1.0.0 e l&#39;estensione tag fosse 1.2.0, il valore sarebbe `1.0.0+1.2.0`.
* `commands`: Sono tutti i comandi disponibili supportati dalla libreria caricata.
* `configs`: Sono tutte le configurazioni correnti nella libreria caricata.
