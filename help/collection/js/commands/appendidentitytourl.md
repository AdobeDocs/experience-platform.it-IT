---
title: appendIdentityToUrl
description: Distribuisci esperienze personalizzate in modo più preciso tra app, web e tra domini diversi.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `appendIdentityToUrl`

Il comando `appendIdentityToUrl` consente di aggiungere un identificatore utente all&#39;URL come stringa di query. Questa azione ti consente di trasmettere l’identità di un visitatore tra più domini, evitando conteggi duplicati dei visitatori per i set di dati che includono sia domini che canali. È disponibile sul Web SDK versione 2.11.0 o successiva.

La stringa di query generata e aggiunta all&#39;URL è `adobe_mc`. Se il Web SDK non è in grado di trovare un ECID, chiama l&#39;endpoint `/acquire` per generarne uno.

>[!NOTE]
>
>Se non è stato fornito il consenso, l’URL di questo metodo viene restituito invariato. Questo comando viene eseguito immediatamente, senza attendere un aggiornamento del consenso.

Eseguire il comando `appendIdentityToUrl` con un URL come parametro. Il metodo restituisce un URL con l’identificatore aggiunto come stringa di query.

```js
alloy("appendIdentityToUrl",
  {
    url: document.location.href
  }
);
```

Puoi aggiungere un listener di eventi per tutti i clic ricevuti sulla pagina e verificare se l’URL corrisponde ai domini desiderati. In caso contrario, aggiungi l’identità all’URL e reindirizza l’utente.

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to the desired domain
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".adobe.com") && !url.hostname.endsWith(".behance.com")) return;

  // Append the identity to the URL, then direct the user to the URL
  event.preventDefault();
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => { window.open(result.url, anchor.target || "_self"); });
});
```

Questo comando supporta l&#39;oggetto [`edgeConfigOverrides`](configure/edgeconfigoverrides.md).

## Oggetto di risposta

Quando [gestisci le risposte](command-responses.md) con questo comando, l&#39;oggetto di risposta contiene **`url`**, il nuovo URL con informazioni di identità aggiunto come parametro della stringa di query.

## Aggiungere identità all’URL utilizzando l’estensione tag Web SDK

L&#39;estensione tag Web SDK equivalente a questo comando è l&#39;azione [Reindirizza con identità](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md).
