---
title: Panoramica dell’estensione Adobe Target v2
description: Scopri le caratteristiche dell’estensione Tag di Adobe Target v2 in Adobe Experience Platform.
exl-id: 8f491d67-86da-4e27-92bf-909cd6854be1
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 98%

---

# Panoramica dell’estensione Adobe Target v2

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Utilizza questo riferimento per informazioni sulle opzioni disponibili quando utilizzi questa estensione per creare una regola.

## Configura l&#39;estensione Adobe Target v2

>[!IMPORTANT]
>
>L’estensione Adobe Target richiede At.js 2.x.

Se l’estensione Adobe Target non è ancora installata, apri la proprietà, quindi seleziona **[!UICONTROL Estensioni > Catalogo]**, passa il puntatore sull’estensione Target e fai clic su **[!UICONTROL Installa]**.

Per configurare l’estensione, apri la scheda Estensioni, passa il puntatore sull’estensione e fai clic su **[!UICONTROL Configura]**.

![](../../../images/targetv2config.png)

### Impostazioni at.js

Tutte le impostazioni at.js, a eccezione del Timeout, vengono recuperate automaticamente dalla configurazione at.js nell’interfaccia utente di Target. L’estensione recupera le impostazioni dall’interfaccia utente di Target solo quando viene aggiunta per la prima volta; pertanto, in caso di aggiornamenti aggiuntivi, tutte le impostazioni dovranno essere gestite nell’interfaccia di Data Collection.

Sono disponibili le seguenti configurazioni:

#### Codice client

Il codice client è l&#39;identificatore account di Target. Questo valore dovrebbe essere quasi sempre lasciato come predefinito. Può essere modificato tramite elementi di dati.

#### ID organizzazione

Questo ID collega l&#39;implementazione al tuo account Adobe Experience Cloud. Questo valore dovrebbe essere quasi sempre lasciato come predefinito. Può essere modificato tramite elementi di dati.

#### Dominio server

Il dominio del server fa riferimento al dominio in cui vengono inviate le richieste Target. Questo valore dovrebbe essere quasi sempre lasciato come predefinito.

#### Consenso RGPD

Quando abilitato, Adobe Target fornisce funzionalità opt-in per supportare la strategia di gestione del consenso. La funzionalità opt-in consente ai clienti di controllare come e quando viene attivato il tag di Target. Per ulteriori informazioni sul consenso di Adobe, consulta [Privacy e Regolamento generale sulla protezione dei dati (RGPD)](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=it).

#### Timeout (ms)

Se la risposta di Target non viene ricevuta entro il periodo definito, la richiesta scade e viene visualizzato il contenuto predefinito. Durante la sessione del visitatore vengono ripetuti ulteriori tentativi di richiesta. Il valore predefinito è 3000 ms, che potrebbe essere diverso dal Timeout configurato nell&#39;interfaccia utente di Target.

Per ulteriori informazioni sul funzionamento dell&#39;impostazione Timeout, consulta la guida di [Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/deploy-at-js/implementing-target-without-a-tag-manager.html?lang=it).

## Tipi di azione dell&#39;estensione Target

In questa sezione sono descritti i tipi di azione disponibili nell&#39;estensione Target.

L&#39;estensione Target fornisce le seguenti azioni nella sezione Then di una regola:

### Load Target

Aggiungi questa azione alla regola di tag nel punto più appropriato per caricare Target nel contesto della regola. Questo carica la libreria at.js nella pagina. Nella maggior parte delle implementazioni, Target deve essere caricato su ogni pagina del sito. Adobe consiglia di utilizzare l’azione Load Target solo se è preceduta da una chiamata Target. In caso contrario, potrebbero verificarsi problemi come il ritardo della chiamata Analytics.

Non è necessaria alcuna configurazione.

### Caricare Target con Decisioning sul dispositivo

Aggiungi questa azione alla regola di tag nel punto più appropriato per caricare Target con [decisioning sul dispositivo](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/on-device-decisioning/on-device-decisioning.html?lang=it) abilitato nel contesto della regola. In questo modo viene caricata nella pagina la libreria at.js con decisioning sul dispositivo abilitato. Nella maggior parte delle implementazioni, Target deve essere caricato su ogni pagina del sito. Adobe consiglia di utilizzare l’azione Carica Target con Decisioning sul dispositivo solo se è preceduta da una chiamata Target. In caso contrario, potrebbero verificarsi problemi come il ritardo della chiamata Analytics.

Non è necessaria alcuna configurazione.

### Aggiungi parametri a All Requests

Questo tipo di azione consente di aggiungere parametri a tutte le richieste Target. L&#39;azione Load Target deve essere utilizzata in precedenza.

1. Specifica il nome e il valore del parametro che desideri aggiungere.
1. Seleziona l’icona Aggiungi per aggiungere altri parametri.

### Aggiungi parametri alla Page Load Request

Questo tipo di azione consente di aggiungere parametri specifici alle richieste di caricamento pagina. L&#39;azione Load Target deve essere utilizzata in precedenza.

1. Specifica il nome e il valore del parametro che desideri aggiungere.
1. Seleziona l’icona Aggiungi per aggiungere altri parametri.

### Attivare Richiesta di caricamento pagina

Questo tipo di azione consente a Target di attivare una richiesta al caricamento della pagina. L&#39;azione Load Target deve essere utilizzata in precedenza.

Specifica se abilitare la funzione per nascondere l’elemento “body”, in modo da evitare lo sfarfallio iniziale della pagina, e lo stile utilizzato per nasconderlo. Sono disponibili le seguenti opzioni:

* **Nascondi corpo:** puoi abilitare o disabilitare questa impostazione. Il valore predefinito è Enabled: ciò significa che HTML BODY è nascosta.
* **Stile corpo nascosto:** il valore predefinito è body{opacity:0}. Questo valore può essere modificato in uno diverso, ad esempio body{display:none}.

Per ulteriori informazioni, consulta la [documentazione online di Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html?lang=it).

### Attiva visualizzazione

È possibile utilizzare l’azione Attiva visualizzazione quando viene caricata una nuova pagina o quando si esegue di nuovo il rendering di un componente di una pagina. L’azione Attiva visualizzazione deve essere implementata per le applicazioni a pagina singola.

1. Specifica il nome della visualizzazione da attivare.
1. Specifica se l&#39;attivazione della visualizzazione deve essere attribuita a un&#39;impression per il reporting controllando la casella di controllo Page. Se la visualizzazione è correlata a un componente nuovamente sottoposto a rendering e non attribuisce a un&#39;impression per il reporting, lascia la casella di controllo Page deselezionata.

Per ulteriori informazioni sull’attivazione di una visualizzazione, consulta la [`triggerView()`documentazione dell’Aiuto](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/functions-overview/adobe-target-triggerview-atjs-2.html?lang=it).

## Implementazione di base di Adobe Target

Una volta installata l&#39;estensione Target, crea almeno una regola per distribuita correttamente. Devi innanzitutto caricare la libreria Target (at.js), specificare i parametri che desideri utilizzare con la richiesta di caricamento della pagina e attivare la richiesta di caricamento della pagina.

Una regola Target con questa implementazione di base si presenta così:

![](../../../images/targetv2deploy.png)

Dopo aver salvato questa regola, devi aggiungerla a una libreria e generarla/implementarla in modo da testarne il comportamento.

## Estensione Adobe Target con implementazione asincrona

I tag possono essere distribuiti in modo asincrono. Se carichi la libreria di tag in modo asincrono con Target al suo interno, anche Target verrà caricato in modo asincrono. Si tratta di uno scenario completamente supportato, ma bisogna fare una valutazione aggiuntiva.

In implementazioni asincrone, la pagina può terminare il rendering del contenuto predefinito prima che la libreria di Target sia completamente caricata e abbia eseguito lo scambio di contenuto. Questo può causare il cosiddetto &quot;sfarfallio&quot; in cui il contenuto predefinito viene visualizzato brevemente prima di essere sostituito dal contenuto personalizzato specificato da Target. Se vuoi evitare questo sfarfallio, ti consigliamo di utilizzare uno snippet per nascondere il contenuto e caricare il bundle di tag in modo asincrono.

Di seguito sono riportati alcuni aspetti da tenere presenti quando si utilizza lo snippet per nascondere il contenuto:

* Lo snippet deve essere aggiunto prima di caricare il codice di incorporamento dell’intestazione del tag.
* Questo codice non può essere gestito dai tag, pertanto deve essere aggiunto direttamente alla pagina.
* La pagina viene visualizzata quando si verifica il primo degli eventi seguenti:
   * Quando è stata ricevuta la risposta di caricamento della pagina
   * Quando la richiesta di caricamento della pagina scade
   * Quando lo stesso frammento scade
* L&#39;azione &quot;Fire Page Load Request&quot; deve essere utilizzata in tutte le pagine che utilizzano il frammento pre-hiding per ridurne la durata.
* L’impostazione Nascondi corpo deve essere abilitata anche nell’azione Page Load Request nella regola Page Load utilizzata per Target nell’interfaccia utente di Data Collection; in caso contrario, tutti i caricamenti di pagina rimangono nascosti per il periodo di timeout.

Il frammento di codice pre-hiding è il seguente e può essere ridotto. Le opzioni configurabili sono alla fine:

```js
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

Per impostazione predefinita, il frammento nasconde l&#39;intera sezione HTML BODY. In alcuni casi, puoi voler nascondere solo alcuni elementi HTML e non l&#39;intera pagina. Per farlo, puoi personalizzare il parametro di stile. Sostituiscilo con un elemento che nasconde solo determinate aree della pagina.

Ad esempio, se hai due aree identificate dagli ID container-1 e container-2, puoi sostituire lo stile come segue:

```css
#container-1, #container-2 {opacity: 0 !important}
```

invece del codice di default:

```css
body {opacity: 0 !important}
```

Per impostazione predefinita, il frammento scade a 3000 ms o 3 secondi. Questo valore può essere personalizzato.
