---
title: clickCollection
description: Ottimizza le impostazioni della raccolta di clic.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# `clickCollection`

L&#39;oggetto `clickCollection` contiene diverse variabili che consentono di controllare i dati di collegamento raccolti automaticamente. Utilizzare queste variabili quando si desidera includere o escludere tipi di collegamenti dalla raccolta dati. È supportato dal Web SDK versione 2.25.0 o successiva.

Questa variabile richiede tutti i seguenti elementi:

* [`clickCollectionEnabled`](clickcollectionenabled.md) deve essere abilitato.
* Se si utilizza `clickCollection.filterClickDetails`, il metodo obsoleto [`onBeforeLinkClickSend`](onbeforelinkclicksend.md) deve essere vuoto.
* Il payload dell&#39;evento deve contenere un valore in `xdm.web.webPageDetails.name` a un certo punto della visita del visitatore.

Se l’implementazione non soddisfa tutti i requisiti di cui sopra, questo oggetto non esegue alcuna operazione.

Nell&#39;oggetto `clickCollection` sono disponibili le seguenti proprietà:

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| **`internalLinkEnabled`** | `boolean` | Determina se tenere traccia automaticamente dei collegamenti all&#39;interno del dominio corrente. Ad esempio, da `https://example.com/index.html` a `https://example.com/product.html` verrebbe considerato un collegamento interno. |
| **`downloadLinkEnabled`** | `boolean` | Determina se la libreria tiene traccia dei collegamenti qualificati come download in base alla proprietà [`downloadLinkQualifier`](downloadlinkqualifier.md). |
| **`externalLinkEnabled`** | `boolean` | Determina se tenere traccia automaticamente dei collegamenti ai domini esterni. Ad esempio, da `https://example.com` a `https://example.net` verrebbe considerato un collegamento esterno. |
| **`eventGroupingEnabled`** | `boolean` | Determina se la libreria attende il successivo evento &quot;visualizzazione pagina&quot; per inviare i dati di tracciamento dei collegamenti. La libreria considera un evento come una &quot;visualizzazione pagina&quot; quando i seguenti elementi sono inclusi nel payload:<ul><li>`xdm.web.webPageDetails.name` contiene un valore stringa</li><li>`xdm.web.webPageDetails.pageViews.value` è maggiore di `0`</li></ul>Al caricamento dell’evento &quot;visualizzazione pagina&quot;, la libreria combina i dati di tracciamento dei collegamenti memorizzati con il resto dei dati di quell’evento. L’abilitazione di questa opzione riduce il numero totale di eventi inviati ad Adobe. Se `internalLinkEnabled` è disabilitato, questa variabile non esegue alcuna operazione. |
| **`sessionStorageEnabled`** | `boolean` | Determina se i dati di tracciamento dei collegamenti vengono memorizzati nell&#39;archiviazione della sessione anziché nelle variabili locali. Se `internalLinkEnabled` o `eventGroupingEnabled` sono disabilitati, questa variabile non esegue alcuna operazione.<br>Adobe consiglia vivamente di abilitare questa variabile quando si utilizza `eventGroupingEnabled` al di fuori delle applicazioni a pagina singola. Se `eventGroupingEnabled` è abilitato mentre `sessionStorageEnabled` è disabilitato, facendo clic su una nuova pagina si verifica la perdita dei dati di tracciamento dei collegamenti, in quanto non vengono conservati nell&#39;archiviazione della sessione. Poiché le applicazioni a pagina singola in genere non passano a una nuova pagina, l’archiviazione della sessione non è necessaria per le pagine di applicazioni a pagina singola. |
| **`filterClickDetails`** | `function` | Funzione di callback che fornisce controlli completi sui dati di tracciamento dei collegamenti raccolti. Puoi utilizzare questa funzione di callback per modificare, offuscare o interrompere l’invio dei dati di tracciamento dei collegamenti. Questo callback è utile quando si desidera omettere informazioni specifiche, ad esempio informazioni personali identificabili all&#39;interno di collegamenti. |

Se non si imposta questo oggetto nel comando [`configure`](overview.md), le impostazioni predefinite per questo oggetto dipendono dal valore di [`clickCollectionEnabled`](clickcollectionenabled.md):

* `internalLinkEnabled`: corrisponde a `clickCollectionEnabled`
* `downloadLinkEnabled`: corrisponde a `clickCollectionEnabled`
* `externalLinkEnabled`: corrisponde a `clickCollectionEnabled`
* `eventGroupingEnabled`: impostazione predefinita `false`; deve essere abilitata in modo esplicito
* `sessionStorageEnabled`: impostazione predefinita `false`; deve essere abilitata in modo esplicito
* `filterClickDetails`: non contiene una funzione; deve essere registrato in modo esplicito

>[!TIP]
>
>Adobe consiglia di abilitare `eventGroupingEnabled` quando `internalLinkEnabled` è abilitato, in quanto riduce il numero di eventi che vengono conteggiati ai fini dell&#39;utilizzo contrattuale.

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

## Configurare la raccolta di clic per l&#39;estensione tag Web SDK

Queste impostazioni possono essere configurate nell&#39;estensione tag Web SDK utilizzando [Impostazioni di configurazione raccolta dati](/help/tags/extensions/client/web-sdk/configure/data-collection.md).
