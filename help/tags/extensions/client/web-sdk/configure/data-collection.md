---
title: Impostazioni di configurazione della raccolta dati
description: Configurare le impostazioni di raccolta dati nell'estensione tag Web SDK.
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Impostazioni di configurazione della raccolta dati

Questa sezione di configurazione consente di determinare come vengono raccolti i dati nell’estensione.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione **[!UICONTROL Data collection]**.

![Immagine che mostra le impostazioni di raccolta dati dell&#39;estensione tag Web SDK nell&#39;interfaccia utente Tag.](../assets/web-sdk-ext-collection.png)

Sono disponibili le seguenti opzioni:

## [!UICONTROL On before event send callback]

Funzione di callback per valutare e modificare il payload inviato ad Adobe. Nell’editor di codice puoi accedere alle seguenti variabili:

* **`content.xdm`**: payload XDM per l&#39;evento.
* **`content.data`**: payload dell&#39;oggetto dati per l&#39;evento.
* **`return true`**: uscire immediatamente dal callback e inviare dati ad Adobe con i valori correnti nell&#39;oggetto `content`.
* **`return false`**: uscire immediatamente dal callback e interrompere l&#39;invio di dati ad Adobe.

È possibile utilizzare qualsiasi variabile definita al di fuori di `content`, ma non è inclusa nel payload inviato ad Adobe.

>[!WARNING]
>
>Questo callback consente l’utilizzo di codice personalizzato. Se un codice incluso nel callback genera un&#39;eccezione non rilevata, l&#39;elaborazione per l&#39;evento si interrompe. **Dati non inviati ad Adobe.**

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>Evita di restituire `false` nel primo evento di una pagina. La restituzione di `false` sul primo evento può avere un impatto negativo sulla personalizzazione.

Questo callback è l&#39;equivalente del tag [`onBeforeEventSend`](/help/collection/js/commands/configure/onbeforeeventsend.md) nella libreria JavaScript.

## [!UICONTROL Collect internal link clicks]

Una casella di controllo che abilita la raccolta di dati di tracciamento dei collegamenti interni al sito o alla proprietà. Questa casella di controllo è l&#39;equivalente del tag [`clickCollection.internalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) nella libreria JavaScript. Quando si attiva questa casella di controllo, vengono visualizzate le opzioni di raggruppamento degli eventi:

* **[!UICONTROL No event grouping]**: i dati di tracciamento dei collegamenti vengono inviati ad Adobe in eventi separati. I clic sui collegamenti inviati in eventi separati possono aumentare l’utilizzo contrattuale dei dati inviati a Adobe Experience Platform.
* **[!UICONTROL Event grouping using session storage]**: archivia i dati di tracciamento dei collegamenti nell&#39;archivio della sessione fino al prossimo evento &quot;visualizzazione pagina&quot;. Al successivo evento considerato come &quot;visualizzazione pagina&quot;, i dati di tracciamento dei collegamenti memorizzati vengono uniti al payload dell’evento &quot;visualizzazione pagina&quot;. Adobe consiglia di abilitare questa impostazione durante il tracciamento dei collegamenti interni.
* **[!UICONTROL Event grouping using local object]**: archivia i dati di tracciamento dei collegamenti in un oggetto locale fino al successivo evento &quot;visualizzazione pagina&quot;. Se un visitatore passa a una nuova pagina del browser, i dati di tracciamento dei collegamenti andranno persi. Questa impostazione è particolarmente utile nel contesto delle applicazioni a pagina singola.

La libreria di tag considera un dato evento una &quot;visualizzazione pagina&quot; quando i seguenti elementi sono inclusi nel payload:

* `xdm.web.webPageDetails.name` contiene un valore stringa
* `xdm.web.webPageDetails.pageViews.value` è maggiore di `0`

## [!UICONTROL Collect external link clicks]

Casella di controllo che abilita la raccolta di collegamenti esterni. Questa casella di controllo è l&#39;equivalente del tag [`clickCollection.externalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) nella libreria JavaScript.

## [!UICONTROL Collect download link clicks]

Casella di controllo che abilita la raccolta di collegamenti di download. Questa casella di controllo è l&#39;equivalente del tag [`clickCollection.downloadLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) nella libreria JavaScript.

## [!UICONTROL Download link qualifier]

Un’espressione regolare che qualifica un URL di collegamento come collegamento di download. Questa stringa è l&#39;equivalente del tag [`downloadLinkQualifier`](/help/collection/js/commands/configure/downloadlinkqualifier.md) nella libreria JavaScript.

## [!UICONTROL Filter click properties]

Funzione di callback per valutare e modificare le proprietà relative ai clic prima della raccolta. Questa funzione viene eseguita prima di [!UICONTROL On before event send callback] ed è l&#39;equivalente tag di [`clickCollection.filterClickDetails`](/help/collection/js/commands/configure/clickcollection.md) nella libreria JavaScript. Nell’editor di codice puoi accedere alle seguenti variabili:

* **`content.clickedElement`**: elemento DOM su cui è stato fatto clic.
* **`content.pageName`**: nome della pagina quando si è verificato il clic.
* **`content.linkName`**: nome del collegamento su cui è stato fatto clic.
* **`content.linkRegion`**: area del collegamento su cui è stato fatto clic.
* **`content.linkType`**: tipo di collegamento (uscita, download o altro).
* **`content.linkURL`**: URL di destinazione del collegamento su cui è stato fatto clic.
* **`return true`**: uscire immediatamente dal callback con i valori della variabile corrente.
* **`return false`**: uscire immediatamente dal callback e interrompere la raccolta dei dati.
* È possibile utilizzare qualsiasi variabile definita al di fuori di `content`, ma non è inclusa nel payload inviato ad Adobe.

>[!TIP]
>
>Il campo **[!UICONTROL On before link click send]** è un callback obsoleto visibile solo per le proprietà per le quali è già configurato. Equivale al tag [`onBeforeLinkClickSend`](/help/collection/js/commands/configure/onbeforelinkclicksend.md) nella libreria JavaScript. Utilizza il callback **[!UICONTROL Filter click properties]** per filtrare o regolare i dati di clic, oppure utilizza **[!UICONTROL On before event send callback]** per filtrare o regolare il payload complessivo inviato ad Adobe. Se sono impostati sia il callback **[!UICONTROL Filter click properties]** che il callback **[!UICONTROL On before link click send]**, verrà eseguito solo il callback **[!UICONTROL Filter click properties]**.

## Impostazioni di contesto

Raccogli automaticamente le informazioni sui visitatori, compilando specifici campi XDM. È possibile scegliere **[!UICONTROL All default context information]** o **[!UICONTROL Specific context information]**. Equivale al tag [`context`](/help/collection/js/commands/configure/context.md) nella libreria JavaScript.

* **[!UICONTROL Web]**: raccoglie informazioni sulla pagina corrente.
* **[!UICONTROL Device]**: raccoglie informazioni sul dispositivo dell&#39;utente.
* **[!UICONTROL Environment]**: raccoglie informazioni sul browser dell&#39;utente.
* **[!UICONTROL Place context]**: raccoglie informazioni sulla posizione dell&#39;utente.
* **[!UICONTROL High entropy user-agent hints]**: raccoglie informazioni più dettagliate sul dispositivo dell&#39;utente.
