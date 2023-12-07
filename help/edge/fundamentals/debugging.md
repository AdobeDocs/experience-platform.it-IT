---
title: Debug in Adobe Experience Platform Web SDK
description: Scopri come attivare/disattivare le funzionalità di debug in Experienci Platform Web SDK.
keywords: debug web sdk;debugging;configurare;configurare comando;debug comando;edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# Debugging

Quando è abilitato il debug, l’SDK invia messaggi alla console del browser che possono essere utili per eseguire il debug dell’implementazione e per comprendere il comportamento dell’SDK.

Il debug è disabilitato per impostazione predefinita, ma può essere attivato in quattro modi diversi:

* `configure` comando
* `setDebug` comando
* parametro stringa query
* Attivazione/disattivazione di Abilita debug in Adobi Experience Platform Debugger. Adobe Experience Platform è uno strumento potente che esamina le pagine web e consente di eseguire il debug dei problemi di implementazione con i prodotti di Experience Cloud. L’Adobe Experience Platform Debugger è disponibile come [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) estensione. Il debug può essere abilitato dalla scheda di configurazione della sezione AEP Web SDK.

![Experience Platform di immagine dell’interfaccia utente di Debugger che mostra la schermata di configurazione.](../assets/enable-debugging.png)

## Attivazione/disattivazione del debug con il comando Configura

Quando si configura l’SDK utilizzando `configure` , abilitare il debug impostando il comando `debugEnabled` opzione per `true`.

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

## Attivazione/disattivazione del debug con il comando Debug

Attiva/disattiva il debug con un `debug` comando come segue:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Se preferisci non modificare il codice nella pagina Web o non desideri che i messaggi di registrazione vengano prodotti per tutti gli utenti del sito Web, ciò è particolarmente utile perché puoi eseguire il comando `debug` nella console JavaScript del browser in qualsiasi momento.

## Attivazione/disattivazione del debug con un parametro di stringa query

Attiva/disattiva debug impostando un&#39; `alloy_debug` parametro stringa query su `true` o `false` come segue:

```HTTP
http://example.com/?alloy_debug=true
```

Simile a `debug` , se si preferisce non modificare il codice nella pagina Web o non si desidera che i messaggi di registrazione vengano generati per tutti gli utenti del sito Web, ciò è particolarmente utile perché è possibile impostare il parametro della stringa query durante il caricamento della pagina Web nel browser.

## Priorità e durata

Quando il debug è impostato tramite `debug` parametro di stringa di comando o query, sostituisce qualsiasi `debug` opzione impostata in `configure` comando. In questi due casi, il debug rimane attivato anche per la durata della sessione. In altre parole, se si abilita il debug utilizzando il comando debug o il parametro della stringa di query, il debug rimarrà attivato fino a quando non si verifica una delle seguenti condizioni:

* Fine della sessione
* Esegui il comando `debug` comando
* È necessario impostare nuovamente il parametro della stringa di query

## Recupero delle informazioni della libreria

Spesso è utile accedere ad alcuni dettagli della libreria caricata sul sito web. A questo scopo, esegui `getLibraryInfo` comando come segue:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

Attualmente, il fornito `libraryInfo` L&#39;oggetto contiene le seguenti proprietà:

* `version`: versione della libreria caricata. Ad esempio, se la versione della libreria da caricare era 1.0.0, il valore sarebbe `1.0.0`. Quando la libreria viene eseguita all’interno dell’estensione tag (denominata &quot;AEP Web SDK&quot;), la versione è quella della libreria e quella dell’estensione tag è unita a un segno &quot;+&quot;. Ad esempio, se la versione della libreria è 1.0.0 e la versione dell’estensione tag è 1.2.0, il valore sarà `1.0.0+1.2.0`.
* `commands`: questi sono tutti i comandi disponibili supportati dalla libreria caricata.
* `configs`: tutte le configurazioni correnti nella libreria caricata.
