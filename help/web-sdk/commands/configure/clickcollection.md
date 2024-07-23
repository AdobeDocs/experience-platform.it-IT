---
title: clickCollection
description: Ottimizza le impostazioni della raccolta di clic.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# `clickCollection`

L&#39;oggetto `clickCollection` contiene diverse variabili che consentono di controllare i dati di collegamento raccolti automaticamente. Utilizzare queste variabili quando si desidera includere o escludere tipi di collegamenti dalla raccolta dati.

Richiede l&#39;abilitazione di [`clickCollectionEnabled`](clickcollectionenabled.md).

È supportato dall’SDK web 2.25.0 o versione successiva.

Nell&#39;oggetto `clickCollection` sono disponibili le seguenti variabili:

* **`clickCollection.internalLinkEnabled`**: valore booleano che determina se i collegamenti all&#39;interno del dominio corrente vengono tracciati automaticamente. Ad esempio, da `https://example.com/index.html` a `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: valore booleano che determina se la libreria tiene traccia dei collegamenti qualificati come download in base alla proprietà [`downloadLinkQualifier`](downloadlinkqualifier.md).
* **`clickCollection.externalLinkEnabled`**: valore booleano che determina se i collegamenti a domini esterni vengono tracciati automaticamente. Ad esempio, da `https://example.com` a `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: valore booleano che determina se la libreria attende la pagina successiva per inviare i dati di tracciamento dei collegamenti. Al caricamento della pagina successiva, combina i dati di tracciamento dei collegamenti con l’evento di caricamento della pagina. L’abilitazione di questa opzione riduce il numero di eventi inviati all’Adobe. Se `internalLinkEnabled` è disabilitato, questa variabile non esegue alcuna operazione.
* **`clickCollection.sessionStorageEnabled`**: valore booleano che determina se i dati di tracciamento dei collegamenti vengono memorizzati nell&#39;archiviazione della sessione anziché nelle variabili locali. Se `internalLinkEnabled` o `eventGroupingEnabled` sono disabilitati, questa variabile non esegue alcuna operazione.

  L&#39;Adobe consiglia vivamente di abilitare questa variabile quando si utilizza `eventGroupingEnabled` al di fuori delle applicazioni a pagina singola. Se `eventGroupingEnabled` è abilitato mentre `sessionStorageEnabled` è disabilitato, facendo clic su una nuova pagina si verifica la perdita dei dati di tracciamento dei collegamenti, in quanto non vengono conservati nell&#39;archiviazione della sessione. Poiché le applicazioni a pagina singola in genere non passano a una nuova pagina, l’archiviazione della sessione non è necessaria per le pagine SPA.
* **`filterClickDetails`**: funzione di callback che fornisce controlli completi sui dati di tracciamento dei collegamenti raccolti. Puoi utilizzare questa funzione di callback per modificare, offuscare o interrompere l’invio dei dati di tracciamento dei collegamenti. Questo callback è utile quando si desidera omettere informazioni specifiche, ad esempio informazioni personali identificabili all&#39;interno di collegamenti.

## Fai clic sulle impostazioni della raccolta utilizzando l’estensione tag Web SDK

Selezionare una delle opzioni seguenti durante la [configurazione dell&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md):

* [!UICONTROL Raccogli collegamenti interni]
   * [!UICONTROL Opzioni di raggruppamento eventi]:
      * [!UICONTROL Nessun raggruppamento di eventi]
      * [!UICONTROL Raggruppamento eventi tramite archiviazione sessione]
      * [!UICONTROL Raggruppamento eventi tramite oggetto locale]
* [!UICONTROL Raccolta collegamenti esterni]
* [!UICONTROL Raccogli collegamenti di download]
* [!UICONTROL Proprietà clic filtro]

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione [!UICONTROL Raccolta dati], quindi seleziona le impostazioni desiderate per la raccolta di clic.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

Il callback [!UICONTROL Proprietà clic filtro] apre un editor di codice personalizzato che consente di inserire il codice desiderato. Nell’editor di codice puoi accedere alle seguenti variabili:

* **`content.clickedElement`**: elemento DOM su cui è stato fatto clic.
* **`content.pageName`**: nome della pagina quando si è verificato il clic.
* **`content.linkName`**: nome del collegamento su cui è stato fatto clic.
* **`content.linkRegion`**: area del collegamento su cui è stato fatto clic.
* **`content.linkType`**: tipo di collegamento (uscita, download o altro).
* **`content.linkURL`**: URL di destinazione del collegamento su cui è stato fatto clic.
* **`return true`**: uscire immediatamente dal callback con i valori della variabile corrente.
* **`return false`**: uscire immediatamente dal callback e interrompere la raccolta dei dati.

È possibile utilizzare qualsiasi variabile definita al di fuori di `content`, ma non è inclusa nel payload inviato a Adobe.

## Fai clic sulle impostazioni della raccolta utilizzando la libreria JavaScript dell’SDK per web

Impostare le variabili desiderate nell&#39;oggetto `clickCollection` durante l&#39;esecuzione del comando [`configure`](overview.md). Se non è impostato, le impostazioni predefinite per questo oggetto dipendono dal valore di [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`: corrisponde a `clickCollectionEnabled`
* `downloadLinkEnabled`: corrisponde a `clickCollectionEnabled`
* `externalLinkEnabled`: corrisponde a `clickCollectionEnabled`
* `eventGroupingEnabled`: impostazione predefinita `false`; deve essere abilitata in modo esplicito
* `sessionStorageEnabled`: impostazione predefinita `false`; deve essere abilitata in modo esplicito
* `filterClickDetails`: non contiene una funzione; deve essere registrato in modo esplicito

>[!TIP]
>L&#39;Adobe consiglia di abilitare `eventGroupingEnabled` quando `internalLinkEnabled` è abilitato, in quanto riduce il numero di eventi che vengono conteggiati ai fini dell&#39;utilizzo contrattuale.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
