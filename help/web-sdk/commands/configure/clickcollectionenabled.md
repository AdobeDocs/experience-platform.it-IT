---
title: clickCollectionEnabled
description: Scopri come configurare Web SDK per determinare se i dati dei clic di collegamento vengono raccolti automaticamente.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: fdb809ea86e91a98b45877c99c3e64d7c49d1cd5
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# `clickCollectionEnabled`

La proprietà `clickCollectionEnabled` è un valore booleano che determina se Web SDK raccoglie automaticamente i dati di collegamento. Se non si imposta questa variabile, il suo valore predefinito è `true`, il che significa che i dati di tracciamento dei collegamenti vengono raccolti automaticamente per impostazione predefinita. L&#39;impostazione di questa proprietà su `false` è utile nei casi in cui si preferisce tenere traccia manualmente dei dati di collegamento.

Quando `clickCollectionEnabled` è abilitato, i seguenti elementi XDM vengono compilati automaticamente con i dati:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

I collegamenti interni, i collegamenti di download e i collegamenti di uscita vengono tracciati automaticamente per impostazione predefinita quando questo valore booleano è abilitato. Se desideri un maggiore controllo sul tracciamento automatico dei collegamenti, Adobe consiglia di utilizzare l&#39;oggetto [`clickCollection`](clickcollection.md).

## Supporto per [!DNL Shadow DOM] elementi aperti

Il Web SDK supporta il tracciamento automatico dei clic per i collegamenti all&#39;interno di **elementi DOM shadow aperti**.

Molti siti Web moderni utilizzano [Componenti Web](https://developer.mozilla.org/en-US/docs/Web/Web_Components) per creare elementi riutilizzabili e incapsulati dell&#39;interfaccia utente. Questi componenti utilizzano spesso una tecnologia denominata [**Shadow DOM**](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM) per mantenere la struttura interna e gli stili separati dal resto della pagina.

Esistono due tipi di DOM ombra:

* **Open Shadow DOM:** La struttura interna è accessibile a JavaScript in esecuzione sulla pagina. Questo significa che altri script possono interagire con il contenuto del componente o esaminarlo.
* **DOM shadow chiuso:** La struttura interna è nascosta da JavaScript all&#39;esterno del componente, rendendolo inaccessibile per il tracciamento o la manipolazione.

Web SDK tiene traccia automaticamente dei clic sugli elementi `<a>` e `<area>` all&#39;interno di **DOM shadow aperti**, come avviene per i collegamenti nel documento principale. In questo modo i clic sui collegamenti all&#39;interno dei componenti Web che utilizzano [!DNL Shadow DOM] aperti verranno inclusi nei dati di analisi. I clic all&#39;interno di **DOM shadow chiusi** non vengono tracciati, in quanto la struttura interna è nascosta dal codice JavaScript che opera all&#39;esterno del componente.

## Logica di tracciamento automatico dei collegamenti

Il Web SDK tiene traccia di tutti i clic sugli elementi HTML `<a>` e `<area>` se non dispone di un attributo `onClick`. I clic vengono acquisiti con un listener di eventi di clic [capture](https://www.w3.org/TR/uievents/#capture-phase) allegato al documento. Quando si fa clic su un collegamento valido, viene eseguita la logica seguente in ordine:

1. Se il collegamento corrisponde ai criteri basati sui valori in [`downloadLinkQualifier`](downloadlinkqualifier.md) o se contiene un attributo HTML `download`, `xdm.web.webInteraction.type` è impostato su `"download"` (se `clickCollection.downloadLinkEnabled` è abilitato).
1. Se il dominio di destinazione del collegamento è diverso dal `window.location.hostname` corrente, `xdm.web.webInteraction.type` è impostato su `"exit"` (se `clickCollection.exitLinkEnabled` è abilitato).
1. Se il collegamento non è idoneo per `"download"` o `"exit"`, `xdm.web.webInteraction.type` è impostato su `"other"`.

In tutti i casi, `xdm.web.webInteraction.name` è impostato sull&#39;etichetta di testo del collegamento e `xdm.web.webInteraction.URL` è impostato sull&#39;URL di destinazione del collegamento. Se desideri impostare anche il nome del collegamento sull&#39;URL, puoi sovrascrivere questo campo XDM utilizzando il callback `filterClickDetails` nell&#39;oggetto `clickCollection`.

## Abilitare il tracciamento automatico dei collegamenti tramite l’estensione tag Web SDK {#tag-extension}

Questa variabile viene gestita automaticamente dall’estensione tag; non è necessario impostarla esplicitamente. Se durante la [configurazione dell&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) viene selezionato uno dei seguenti elementi, vengono raccolti i dati di tracciamento dei collegamenti applicabili:

* [!UICONTROL Raccogliere i clic sul collegamento interno]
* [!UICONTROL Raccogli i clic sul collegamento esterno]
* [!UICONTROL Raccogli clic sul collegamento di download]

Per ulteriori informazioni, vedere [`clickCollection`](clickcollection.md).

## Abilitare il tracciamento automatico dei collegamenti utilizzando la libreria JavaScript di Web SDK {#library}

Impostare il valore booleano `clickCollectionEnabled` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione del Web SDK, per impostazione predefinita viene utilizzato `true`. Impostare questo valore su `false` se si preferisce impostare `xdm.web.webInteraction.type` e `xdm.web.webInteraction.value` manualmente.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
