---
title: appendIdentityToUrl
description: Distribuisci esperienze personalizzate in modo più preciso tra app, web e tra domini diversi.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: 153c5bae42c027c25a38a8b63070249d1b1a8f01
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# `appendIdentityToUrl`

Il comando `appendIdentityToUrl` consente di aggiungere un identificatore utente all&#39;URL come stringa di query. Questa azione ti consente di trasmettere l’identità di un visitatore tra più domini, evitando conteggi duplicati dei visitatori per i set di dati che includono sia domini che canali. È disponibile su Web SDK versione 2.11.0 o successiva.

La stringa di query generata e aggiunta all&#39;URL è `adobe_mc`. Se l&#39;SDK Web non è in grado di trovare un ECID, chiama l&#39;endpoint `/acquire` per generarne uno.

>[!NOTE]
>
>Se non è stato fornito il consenso, l’URL di questo metodo viene restituito invariato. Questo comando viene eseguito immediatamente, senza attendere un aggiornamento del consenso.

## Aggiungere identità all’URL utilizzando l’estensione Web SDK {#extension}

L’aggiunta di un’identità a un URL viene eseguita come azione all’interno di una regola nell’interfaccia dei tag di Adobe Experience Platform Data Collection.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo azione] su **[!UICONTROL Reindirizza con identità]**.
1. Fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

Questo comando viene in genere utilizzato con una regola specifica che ascolta i clic e controlla i domini desiderati.

+++Criteri evento regola

Si attiva quando si fa clic su un tag di ancoraggio con una proprietà `href`.

* **[!UICONTROL Estensione]**: Core
* **[!UICONTROL Tipo evento]**: fare clic
* **[!UICONTROL Quando l&#39;utente fa clic su]**: elementi specifici
* **[!UICONTROL Elementi corrispondenti al selettore CSS]**: `a[href]`

![Evento regola](../assets/id-sharing-event-configuration.png)

+++

+++Condizione regola

Si attiva solo sui domini desiderati.

* **[!UICONTROL Tipo di logica]**: regolare
* **[!UICONTROL Estensione]**: Core
* **[!UICONTROL Tipo condizione]**: confronto valori
* **[!UICONTROL Operando sinistro]**: `%this.hostname%`
* **[!UICONTROL Operatore]**: corrisponde a Regex
* **[!UICONTROL Operando destro]**: espressione regolare che corrisponde ai domini desiderati. Ad esempio, `adobe.com$|behance.com$`

![Condizione regola](../assets/id-sharing-condition-configuration.png)

+++

+++Azione regola

Aggiungi l’identità all’URL.

* **[!UICONTROL Estensione]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Tipo azione]**: reindirizzare con identità

![Azione regola](../assets/id-sharing-action-configuration.png)

+++

## Aggiungere identità all’URL utilizzando la libreria JavaScript dell’SDK web

Eseguire il comando `appendIdentityToUrl` con un URL come parametro. Il metodo restituisce un URL con l’identificatore aggiunto come stringa di query.

```js
alloy("appendIdentityToUrl",document.location);
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
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => {document.location = result.url;});
});
```

## Oggetto di risposta

Se decidi di [gestire le risposte](command-responses.md) con questo comando, l&#39;oggetto di risposta contiene **`url`**, il nuovo URL con le informazioni di identità aggiunto come parametro della stringa di query.
