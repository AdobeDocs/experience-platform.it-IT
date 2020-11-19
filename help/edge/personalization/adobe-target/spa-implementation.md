---
title: ' Adobe Target e Adobe Experience Platform Web SDK. '
seo-title: Adobe Experience Platform Web SDK e utilizzo di  Adobe Target
description: Scopri come eseguire il rendering del contenuto personalizzato con  Experience Platform Web SDK tramite  Adobe Target
seo-description: Scopri come eseguire il rendering del contenuto personalizzato con  Experience Platform Web SDK tramite  Adobe Target
keywords: target;adobe target;xdm views; views;single page applications;SPA;SPA lifecycle;client-side;AB testing;AB;Experience targeting;XT;VEC
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 14%

---


# Implementazione di un’applicazione a pagina singola

Adobe Experience Platform Web SDK offre funzionalità avanzate che consentono alla tua azienda di eseguire la personalizzazione su tecnologie lato client di prossima generazione, come le applicazioni a pagina singola (SPA).

I siti web tradizionali funzionavano su modelli di navigazione “da pagina a pagina”, altrimenti noti come Applicazioni a più pagine, in cui le progettazioni del sito web erano strettamente collegate a URL e le transizioni da una pagina web a un’altra richiedevano un caricamento di pagina.

Le moderne applicazioni Web, come le applicazioni per pagina singola, hanno invece adottato un modello che consente di utilizzare rapidamente il rendering dell&#39;interfaccia utente del browser, spesso indipendente dai ricarichi di pagina. Queste esperienze possono essere attivate dalle interazioni con i clienti, ad esempio con scorrimento, clic e movimenti del cursore. Con l&#39;evoluzione dei paradigmi del web moderno, la rilevanza degli eventi generici tradizionali, come il caricamento di una pagina, per implementare la personalizzazione e la sperimentazione non funziona più.

![](assets/spa-vs-traditional-lifecycle.png)

## Vantaggi di Platform Web SDK per SPA

Di seguito sono riportati alcuni vantaggi derivanti dall’utilizzo di Adobe Experience Platform Web SDK per le applicazioni a pagina singola:

* Capacità di memorizzare nella cache tutte le offerte al caricamento di pagina per ridurre più chiamate al server a una singola chiamata al server.
* Migliorate notevolmente l&#39;esperienza utente sul vostro sito, perché le offerte vengono visualizzate immediatamente tramite la cache senza ritardi, grazie alle chiamate server tradizionali.
* Una singola riga di codice e una configurazione per sviluppatori una tantum consentono agli addetti al marketing di creare ed eseguire attività A/B e Experience Targeting (XT) tramite Visual Experience Composer (VEC) sul SPA.

## Visualizzazioni XDM e applicazioni per pagina singola

Il Compositore esperienza visivo di Adobe Target per applicazioni a pagina singola (SPA) sfrutta un nuovo concetto chiamato Visualizzazioni: un gruppo logico di elementi visivi che insieme formano un’esperienza SPA. Pertanto, un’applicazione a pagina singola può essere considerata come un passaggio tra le visualizzazioni, anziché tramite gli URL, in base alle interazioni dell’utente. In genere, una visualizzazione può rappresentare un intero sito o elementi visivi raggruppati all&#39;interno di un sito.

Per spiegare meglio le visualizzazioni, l&#39;esempio seguente utilizza un ipotetico sito di e-commerce online implementato in React per esplorare le visualizzazioni di esempio.

Dopo aver visitato il sito principale, un&#39;immagine hero promuove una vendita di Pasqua e i prodotti più recenti disponibili sul sito. In questo caso, è possibile definire una visualizzazione per l&#39;intera schermata principale. Questa vista potrebbe semplicemente essere chiamata &quot;casa&quot;.

![](assets/example-views.png)

As the customer becomes more interested in the products that the business is selling, they decide to click the **Products** link. Come con la home page, l’intero sito dei prodotti può essere definito come visualizzazione. Questa visualizzazione potrebbe essere denominata &quot;products-all&quot;.

![](assets/example-products-all.png)

Poiché una vista può essere definita come un intero sito o un gruppo di elementi visivi su un sito, i quattro prodotti mostrati sul sito prodotti possono essere raggruppati e considerati come una vista. Questa visualizzazione potrebbe essere denominata &quot;products&quot;.

![](assets/example-products.png)

Quando il cliente decide di fare clic sul pulsante **Carica altro** per esplorare più prodotti sul sito, l&#39;URL del sito Web non cambia in questo caso, ma è possibile creare una visualizzazione qui per rappresentare solo la seconda riga di prodotti visualizzati. Il nome visualizzato potrebbe essere &quot;products-page-2&quot;.

![](assets/example-load-more.png)

Il cliente decide di acquistare alcuni prodotti dal sito e procede alla schermata di estrazione. Sul sito di checkout il cliente ha le opzioni per scegliere la consegna normale o la consegna espressa. Una vista può essere un qualsiasi gruppo di elementi visivi in un sito, in modo che sia possibile creare una vista per le preferenze di distribuzione e chiamarla &quot;Preferenze di consegna&quot;.

![](assets/example-check-out.png)

Il concetto di punti di vista può essere ampliato molto più di questo. Questi sono solo alcuni esempi di visualizzazioni che è possibile definire in un sito.

## Implementazione delle visualizzazioni XDM

Le visualizzazioni XDM possono essere sfruttate in  Adobe Target per consentire agli esperti di marketing di eseguire test A/B e XT su SPA tramite Visual Experience Composer (Compositore esperienza visivo). A tal fine, è necessario eseguire i seguenti passaggi per completare una configurazione per sviluppatori una tantum:

1. Install [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md)
2. Determinare tutte le visualizzazioni XDM nell&#39;applicazione a pagina singola che si desidera personalizzare.
3. Dopo aver definito le visualizzazioni XDM, per distribuire le attività AB o XT VEC, implementate la `sendEvent()` funzione con `renderDecisions` impostato su `true` e la visualizzazione XDM corrispondente nell&#39;applicazione a pagina singola. La vista XDM deve essere passata `xdm.web.webPageDetails.viewName`. Questo passaggio consente agli esperti di marketing di utilizzare Visual Experience Composer (Compositore esperienza visivo) per avviare test A/B e XT per tali XDM.

   ```javascript
   alloy("sendEvent", { 
     "renderDecisions": true, 
     "xdm": { 
       "web": { 
         "webPageDetails": { 
         "viewName":"home" 
         }
       } 
     } 
   });
   ```

>[!NOTE]
>
>Nella prima `sendEvent()` chiamata, tutte le visualizzazioni XDM di cui deve essere eseguito il rendering per l’utente finale verranno recuperate e memorizzate nella cache. Le `sendEvent()` chiamate successive con le visualizzazioni XDM trasmesse verranno lette dalla cache e sottoposte a rendering senza una chiamata al server.

## `sendEvent()` esempi di funzioni

Questa sezione illustra tre esempi che mostrano come invocare la `sendEvent()` funzione in React per un ipotetico SPA di e-commerce.

### Esempio 1: Pagina principale test A/B

Il team marketing desidera eseguire test A/B sull&#39;intera pagina principale.

![](assets/use-case-1.png)

Per eseguire i test A/B sull&#39;intero sito principale, `sendEvent()` è necessario richiamare con XDM `viewName` impostato su `home`:

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### Esempio 2: Prodotti personalizzati

Il team marketing desidera personalizzare la seconda riga di prodotti modificando il colore dell&#39;etichetta del prezzo in rosso dopo che l&#39;utente fa clic su **Carica di più**.

![](assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
} 

class Products extends Component { 
  
  render() { 
    return ( 
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component’s state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Esempio 3: Preferenze per la distribuzione dei test A/B

The marketing team want to run an A/B test to see whether changing the color of the button from blue to red when **Express Delivery** is selected can boost conversions (as opposed to keeping the button color blue for both delivery options).

![](assets/use-case-3.png)

Per personalizzare il contenuto del sito in base alla preferenza di consegna selezionata, è possibile creare una visualizzazione per ogni preferenza di consegna. Quando è selezionata l’opzione Consegna **** normale, la vista può essere denominata &quot;cassa normale&quot;. If **Express Delivery** is selected, the View can be named &quot;checkout-express&quot;.

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
} 

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## Utilizzo di Visual Experience Composer (Compositore esperienza visivo) per un SPA

Una volta completata la definizione delle visualizzazioni XDM e implementate `sendEvent()` con le viste XDM passate, il VEC sarà in grado di rilevare queste visualizzazioni e consentire agli utenti di creare azioni e modifiche per le attività A/B o XT.

>[!NOTE]
>
>Per utilizzare il VEC per il vostro SPA, è necessario installare e attivare [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

### Pannello delle modifiche

Il pannello Modifiche acquisisce le azioni create per una vista specifica. Tutte le azioni per una vista sono raggruppate sotto tale vista.

![](assets/modifications-panel.png)

### Azioni

Facendo clic su un’azione viene evidenziato l’elemento del sito dove questa verrà applicata. Each VEC action created under a View has the following icons: **Information**, **Edit**, **Clone**, **Move**, and **Delete**. Queste icone sono spiegate più dettagliatamente nella tabella seguente.

![](assets/action-icons.png)

| Icona | Descrizione |
|---|---|
| Informazioni | Visualizza i dettagli dell’azione. |
| Modifica | Ti consente di modificare direttamente le proprietà dell’azione. |
| Clona | Clona l’azione in una o più visualizzazioni presenti nel pannello Modifiche o in una o più visualizzazioni a cui sei passato nel Compositore esperienza visivo. L’azione non deve necessariamente essere presente nel pannello Modifiche.<br/><br/>**Nota:** Dopo aver eseguito un&#39;operazione di duplicazione, è necessario passare alla vista nel VEC tramite Sfoglia per verificare se l&#39;azione clonata era un&#39;operazione valida. Se non può essere applicata alla visualizzazione, viene visualizzato un errore. |
| Sposta | Sposta l’azione in un evento di caricamento pagina o in un’altra visualizzazione già esistente nel pannello delle modifiche.<br/><br/>**Evento di caricamento pagina:** Eventuali azioni corrispondenti all&#39;evento di caricamento della pagina vengono applicate al caricamento iniziale della pagina dell&#39;applicazione Web. <br/><br/>**Nota:** una volta eseguita l&#39;operazione di spostamento, è necessario passare alla vista nel VEC tramite Sfoglia per verificare se lo spostamento era un&#39;operazione valida. Se non può essere applicata alla visualizzazione, viene visualizzato un errore. |
| Elimina | Elimina l’azione. |

## Utilizzo di VEC per SPA esempi

Questa sezione illustra tre esempi per l&#39;utilizzo di Visual Experience Composer (Compositore esperienza visivo) per creare azioni e modifiche per le attività A/B o XT.

### Esempio 1: Aggiorna visualizzazione &quot;principale&quot;

In precedenza in questo documento era stata definita una vista denominata &quot;home&quot; per l’intero sito principale. Ora il team marketing desidera aggiornare la visualizzazione &quot;principale&quot; nei seguenti modi:

* Modificate i pulsanti **Aggiungi al carrello** e **Simili** in modo da ottenere una condivisione più leggera del blu. Ciò dovrebbe verificarsi durante il caricamento della pagina perché comporta la modifica dei componenti dell’intestazione.
* Change the **Latest Products for 2019** label to **Hottest Products for 2019** and change the text color to purple.

To make these updates in the VEC, select **Compose** and apply those changes to the &quot;home&quot; view.

![](assets/vec-home.png)

### Esempio 2: Modificare le etichette di prodotto

Per la visualizzazione &quot;products-page-2&quot;, il team marketing desidera modificare l&#39;etichetta **Price** in **Sale Price** e cambiare il colore dell&#39;etichetta in rosso.

Per eseguire questi aggiornamenti in VEC, sono necessari i seguenti passaggi:

1. Selezionate **Sfoglia** nel VEC.
2. Selezionate **Prodotti** nella parte superiore del sito.
3. Select **Load More** once to view the second row of products.
4. Selezionate **Componi** nel VEC.
5. Apply actions to change the text label to **Sale Price** and the color to red.

![](assets/vec-products-page-2.png)

### Esempio 3: Personalizzare lo stile delle preferenze di consegna

Le viste possono essere definite a un livello granulare, ad esempio uno stato o un&#39;opzione di un pulsante di scelta. In precedenza in questo documento le viste erano definite per le preferenze di consegna, &quot;checkout-normal&quot; e &quot;checkout-express&quot;. Il team marketing desidera modificare il colore del pulsante in rosso per la visualizzazione &quot;checkout-express&quot;.

Per eseguire questi aggiornamenti in VEC, sono necessari i seguenti passaggi:

1. Selezionate **Sfoglia** nel VEC.
2. Aggiungi prodotti al carrello sul sito.
3. Selezionate l&#39;icona del carrello nell&#39;angolo superiore destro del sito.
4. Selezionare **Checkout your Order**.
5. Fate clic sul pulsante di scelta Consegna **** rapida in Preferenze **** consegna.
6. Selezionate **Componi** nel VEC.
7. Cambia in rosso il colore del pulsante **Paga** .

>[!NOTE]
>
>La visualizzazione &quot;checkout-express&quot; non viene visualizzata nel pannello Modifiche finché non viene selezionato il pulsante di scelta **Express Delivery** . Questo perché la`sendEvent()` funzione viene eseguita quando si seleziona il pulsante di scelta **Express Delivery** , quindi il VEC non è a conoscenza della Vista &quot;checkout-express&quot; finché non viene selezionato il pulsante di scelta.

![](assets/vec-delivery-preference.png)
