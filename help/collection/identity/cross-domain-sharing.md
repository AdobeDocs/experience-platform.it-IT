---
title: Condividere l’identità tra domini
description: Mantenere la continuità delle identità tra i domini di proprietà della tua organizzazione per migliorare la personalizzazione e il reporting.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Condividere l’identità tra domini

Quando i visitatori passano da un dominio all’altro di proprietà della tua organizzazione, per impostazione predefinita ogni dominio mantiene la propria identità di visitatore. Senza un handoff esplicito, un visitatore che fa clic da uno dei tuoi domini a un altro viene trattato come una nuova persona sconosciuta sul sito di destinazione. Questo tipo di implementazione consente di generare rapporti sui frammenti e di riavviare la personalizzazione.

La condivisione delle identità tra domini diversi risolve questo problema aggiungendo un parametro della stringa di query `adobe_mc` all&#39;URL di destinazione quando un visitatore fa clic su un collegamento o viene reindirizzato. Questo parametro contiene l&#39;[Experience Cloud ID (ECID)](./overview.md) del visitatore, l&#39;ID organizzazione e una marca temporale. Quando la pagina di destinazione viene caricata con un parametro `adobe_mc` valido, il Web SDK la legge automaticamente e applica l&#39;identità consegnata alla sua prima richiesta Edge Network, in modo che entrambi i domini condividano lo stesso visitatore. Il parametro `adobe_mc` scade dopo cinque minuti, pertanto la pagina di destinazione deve essere caricata immediatamente dopo il reindirizzamento.

Questo caso d’uso riguarda la condivisione delle identità tra siti web su domini diversi. Se desideri passare un&#39;identità da un&#39;app mobile a una pagina Web Web WebView o mobile, utilizza invece [condivisione identità da dispositivo mobile a Web](./mobile-to-web.md).

## Prerequisiti

Prima di iniziare, assicurati che l’implementazione soddisfi i seguenti requisiti:

* **Web SDK**: [Web SDK](/help/collection/js/js-overview.md) versione **2.11.0 o successiva** o l&#39;estensione tag Web SDK è installata sia nel dominio di origine che in quello di destinazione.
* **Configurazione corrispondente**: tutti i domini partecipanti utilizzano lo stesso [`orgId`](../js/commands/configure/orgid.md) durante la configurazione del Web SDK.
* **Controllo URL**: il codice controlla i collegamenti o i reindirizzamenti tra domini in modo che sia possibile accodare i parametri della stringa di query all&#39;URL di destinazione.

## Implementare la condivisione tra più domini

Devi configurare la condivisione delle identità in ogni dominio che funge da origine in un handoff tra domini. Se i visitatori possono navigare in entrambe le direzioni tra due domini, configura entrambi i domini come origini.

>[!BEGINTABS]

>[!TAB Libreria JavaScript]

Utilizzare il comando [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) per aggiungere il parametro `adobe_mc` ai collegamenti in uscita. L’esempio seguente ascolta i clic sugli elementi di ancoraggio e aggiunge l’identità a qualsiasi collegamento che punta a un dominio desiderato:

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to a domain you want to share identity with
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".example.com") && !url.hostname.endsWith(".example.org")) return;

  // Append the identity to the URL, then navigate
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    window.open(result.url, anchor.target || "_self");
  });
});
```

>[!TAB Estensione tag Web SDK]

Utilizzare l&#39;azione [**[!UICONTROL Redirect with identity]**](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) per aggiungere il parametro `adobe_mc` ai collegamenti in uscita. Per ottenere il comportamento desiderato, puoi creare una regola con le seguenti condizioni:

1. **Evento**: impostare l&#39;estensione su **[!UICONTROL Core]** e il tipo di evento su **[!UICONTROL Click]**. Sotto **[!UICONTROL Elements matching the CSS selector]**, immetti `a[href]`.
2. **Condizione**: impostare l&#39;estensione su **[!UICONTROL Core]** e il tipo di condizione su **[!UICONTROL Value Comparison]**. Impostare **[!UICONTROL Left Operand]** su `%this.hostname%`, **[!UICONTROL Operator]** su **[!UICONTROL Matches Regex]** e **[!UICONTROL Right Operand]** su un&#39;espressione regolare corrispondente ai domini di destinazione (ad esempio, `example\.com$|example\.org$`).
3. **Azione**: impostare l&#39;estensione su **[!UICONTROL Adobe Experience Platform Web SDK]** e il tipo di azione su **[!UICONTROL Redirect with identity]**.

>[!ENDTABS]

## Ricevi identità sul dominio di destinazione

Non è richiesto alcun codice aggiuntivo nel dominio di destinazione. Quando il Web SDK è presente nella pagina e l&#39;URL contiene un parametro `adobe_mc` valido, SDK estrae automaticamente l&#39;ECID e lo applica alla mappa di identità del visitatore alla sua prima richiesta Edge Network.

Verifica che il dominio di destinazione soddisfi le seguenti condizioni:

* L&#39;estensione tag Web SDK o Web SDK è installata e configurata con lo stesso [`orgId`](../js/commands/configure/orgid.md) del dominio di origine. È possibile utilizzare la libreria JavaScript e l&#39;estensione tag Web SDK in modo intercambiabile tra domini, purché condividano lo stesso `orgId`.
* La pagina carica e invia la sua prima richiesta Edge Network entro **cinque minuti** dal reindirizzamento, prima della scadenza del parametro `adobe_mc`.
