---
title: Eseguire il debug
seo-title: Adobe Experience Platform Web SDK debugging
description: Learn how to toggle Experience Platform Web SDK debugging
seo-description: Learn how to toggle Experience Platform Web SDK debugging
translation-type: tm+mt
source-git-commit: 31a527cb4ad1348262131f827c7e932404542c4b
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Eseguire il debug

When debugging is enabled, the SDK outputs messages to the browser console that can be helpful in debugging your implementation and understanding how the SDK is behaving. Debugging also results in a server-side synchronous validation of the data being collected against the schema you have configured.

Il debug è disattivato per impostazione predefinita, ma può essere attivato in tre modi diversi:

* `configure` command
* `setDebug` command
* parametro stringa query

## Attivazione del debug con il comando Configura

Quando configuri l’SDK con il `configure` comando, abilita il debug impostando l’ `debugEnabled` opzione su `true`.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!Hint]
>Questo consente il debug per tutti gli utenti della pagina Web anziché solo per il browser personale.

## Attivazione del debug con il comando Debug

Attiva il debug con un `debug` comando separato, come segue:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Se preferite non modificare il codice della pagina Web o non desiderate che i messaggi di registrazione vengano prodotti per tutti gli utenti del sito Web, questo è particolarmente utile perché potete eseguire il `debug` comando nella console JavaScript del browser in qualsiasi momento.

## Attivazione del debug con un parametro di stringa di query

Per attivare o disattivare il debugging, impostare un parametro di stringa di `alloy_debug` query su `true` o `false` :

```HTTP
http://example.com/?alloy_debug=true
```

Simile al `debug` comando, se preferite non modificare il codice della pagina Web o non desiderate che i messaggi di registrazione vengano prodotti per tutti gli utenti del sito Web, questo è particolarmente utile perché potete impostare il parametro della stringa di query quando caricate la pagina Web all&#39;interno del browser.

## Priorità e durata

Quando il debugging viene impostato tramite il parametro della stringa di `debug` comando o query, sostituisce qualsiasi `debug` opzione impostata nel `configure` comando. In questi due casi, anche il debug rimane attivato per tutta la durata della sessione. In altre parole, se si abilita il debug utilizzando il comando di debug o il parametro della stringa di query, rimane attivato fino a quando non viene eseguita una delle operazioni seguenti:

* Fine della sessione
* Esecuzione del `debug` comando
* Impostare di nuovo il parametro della stringa di query
