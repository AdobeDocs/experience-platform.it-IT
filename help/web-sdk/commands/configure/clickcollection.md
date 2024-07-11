---
title: clickCollection
description: Ottimizza le impostazioni della raccolta di clic.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---


# `clickCollection`

Il `clickCollection` L&#39;oggetto contiene diverse variabili che consentono di controllare i dati di collegamento raccolti automaticamente. Utilizzare queste variabili quando si desidera includere o escludere tipi di collegamenti dalla raccolta dati.

Richiede [`clickCollectionEnabled`](clickcollectionenabled.md) da attivare.

È supportato dall’SDK web 2.25.0 o versione successiva.

Le seguenti variabili sono disponibili nel `clickCollection` oggetto:

* **`clickCollection.internalLinkEnabled`**: valore booleano che determina se i collegamenti all’interno del dominio corrente vengono tracciati automaticamente. Ad esempio: `https://example.com/index.html` a `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: valore booleano che determina se la libreria tiene traccia dei collegamenti idonei come download in base al [`downloadLinkQualifier`](downloadlinkqualifier.md) proprietà.
* **`clickCollection.externalLinkEnabled`**: valore booleano che determina se i collegamenti a domini esterni vengono tracciati automaticamente. Ad esempio: `https://example.com` a `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: valore booleano che determina se la libreria attende la pagina successiva per inviare i dati di tracciamento dei collegamenti. Al caricamento della pagina successiva, combina i dati di tracciamento dei collegamenti con l’evento di caricamento della pagina. L’abilitazione di questa opzione riduce il numero di eventi inviati all’Adobe. Se `internalLinkEnabled` è disattivato, quindi questa variabile non esegue alcuna operazione.
* **`clickCollection.sessionStorageEnabled`**: valore booleano che determina se i dati di tracciamento dei collegamenti vengono memorizzati nell’archiviazione della sessione anziché nelle variabili locali. Se `internalLinkEnabled` o `eventGroupingEnabled` sono disattivati, quindi questa variabile non esegue alcuna operazione.

  L’Adobe consiglia vivamente di abilitare questa variabile quando si utilizza `eventGroupingEnabled`. Se `eventGroupingEnabled` è abilitato durante `sessionStorageEnabled` è disattivato, facendo clic su una nuova pagina si verifica la perdita dei dati di tracciamento dei collegamenti, in quanto non vengono conservati nell’archiviazione della sessione. Mentre è accettabile disabilitare `sessionStorageEnabled` nelle applicazioni a pagina singola, non è ideale per le pagine non SPA.
* **`filterClickDetails`**: funzione di callback che fornisce controlli completi sui dati di tracciamento dei collegamenti raccolti. Puoi utilizzare questa funzione di callback per modificare, offuscare o interrompere l’invio dei dati di tracciamento dei collegamenti. Questo callback è utile quando si desidera omettere informazioni specifiche, ad esempio informazioni personali identificabili all&#39;interno di collegamenti.

## Fai clic sulle impostazioni della raccolta utilizzando l’estensione tag Web SDK

Seleziona la **[!UICONTROL Abilita raccolta dati di clic]** casella di controllo [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). L’attivazione di questa casella di controllo mostra le seguenti opzioni relative alla raccolta di clic:

* [!UICONTROL Collegamenti interni]
   * [!UICONTROL Abilita raggruppamento eventi]
   * [!UICONTROL Abilita archiviazione sessione]
* [!UICONTROL Collegamenti esterni]
* [!UICONTROL Collegamenti di download]
* [!UICONTROL Proprietà clic filtro]

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a [!UICONTROL Raccolta dati] , quindi selezionare la casella di controllo **[!UICONTROL Abilita raccolta dati di clic]**.
1. Seleziona le impostazioni desiderate per la raccolta di clic.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

Il [!UICONTROL Proprietà clic filtro] callback apre un editor di codice personalizzato che consente di inserire il codice desiderato. Nell’editor di codice puoi accedere alle seguenti variabili:

* **`content.clickedElement`**: elemento DOM su cui è stato fatto clic.
* **`content.pageName`**: nome della pagina al momento del clic.
* **`content.linkName`**: nome del collegamento su cui è stato fatto clic.
* **`content.linkRegion`**: area del collegamento in cui è stato fatto clic.
* **`content.linkType`**: tipo di collegamento (uscita, download o altro).
* **`content.linkURL`**: URL di destinazione del collegamento su cui è stato fatto clic.
* **`return true`**: chiude immediatamente il callback con i valori della variabile corrente.
* **`return false`**: chiudi immediatamente il callback e interrompi la raccolta dei dati.

Qualsiasi variabile definita al di fuori di `content` possono essere utilizzati, ma non sono inclusi nel payload inviato ad Adobe.

## Fai clic sulle impostazioni della raccolta utilizzando la libreria JavaScript dell’SDK per web

Imposta le variabili desiderate all&#39;interno di `clickCollection` oggetto durante l&#39;esecuzione di [`configure`](overview.md) comando. Se non viene impostata, le impostazioni predefinite per questo oggetto dipendono dal valore di [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`: corrisponde a `clickCollectionEnabled`
* `downloadLinkEnabled`: corrisponde a `clickCollectionEnabled`
* `externalLinkEnabled`: corrisponde a `clickCollectionEnabled`
* `eventGroupingEnabled`: valore predefinito `false`; deve essere abilitato in modo esplicito
* `sessionStorageEnabled`: valore predefinito `false`; deve essere abilitato in modo esplicito
* `filterClickDetails`: non contiene una funzione; deve essere registrato in modo esplicito

>[!TIP]
>L’Adobe consiglia di abilitare `eventGroupingEnabled`, in quanto consente di ridurre il numero di eventi che vengono conteggiati ai fini dell’utilizzo contrattuale.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true,
    filterClickDetails: function(content) {
      // If the link is a clickable telephone number, anonymize it
      if(content.linkUrl?.includes("tel:")) {
        content.linkName = content.linkUrl = "Phone number";
      }
      // If the link is an email address, anonymize it
      if(content.linkUrl?.includes("mailto:")) {
        content.linkName = content.linkUrl = "Email address";
      }
    }
  }
});
```
