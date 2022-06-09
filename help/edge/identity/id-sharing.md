---
title: Condivisione di ID da mobile a web e tra domini diversi
description: Scopri come mantenere gli ID visitatore da dispositivi mobili a proprietà web e tra domini diversi
keywords: identità;mobile;id;condivisione;dominio;tra domini diversi;sdk;piattaforma;
source-git-commit: 55e28f749741c653a230b42fabf5a047ba8c7d01
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---


# Condivisione di ID da mobile a web e tra domini diversi

## Panoramica

Adobe Experience Platform Web SDK supporta le funzionalità di condivisione degli ID visitatore che consentono ai clienti di fornire esperienze personalizzate più accuratamente, tra app mobili e contenuti web per dispositivi mobili, e tra domini diversi.

## Casi d’uso {#use-cases}

### Personalizzazione coerente tra app mobili e siti web per dispositivi mobili

Un&#39;azienda di abbigliamento vuole personalizzare l&#39;esperienza dei propri clienti in base ai propri interessi e mantenere la personalizzazione accurata in un&#39;applicazione mobile che carica anche WebViews. Utilizzando la funzione di condivisione di ID da mobile a web, possono garantire che le offerte più precise siano presentate ai clienti, utilizzando lo stesso identificatore visitatore nell’app e il contenuto web per dispositivi mobili, passando il [!DNL ECID] all’URL web per dispositivi mobili.

### Fornire una personalizzazione coerente tra i domini

Un rivenditore con più store online vuole personalizzare l&#39;esperienza dell&#39;acquirente nei propri domini in base agli interessi dei clienti. Utilizzando la funzione di condivisione ID tra domini diversi dell’SDK per web, il rivenditore può distribuire offerte accurate in base agli interessi dei clienti, su tutti i loro domini.

### Migliorare la generazione di rapporti sulle attività dei visitatori

Un rivenditore di tecnologia desidera migliorare il rapporto sulle attività dei visitatori con informazioni su quando i visitatori passano dall’app mobile al sito web mobile o ad altri domini. Utilizzando la funzione di condivisione ID tra domini diversi dell’SDK per web, il team di marketing può tracciare con precisione i visitatori attraverso le loro proprietà web e generare rapporti sulle attività.

## Prerequisiti {#prerequisites}

Per utilizzare la condivisione di ID da mobile a web e tra più domini, devi eseguire l’aggiornamento a [!DNL Web SDK] versione 2.11.0 o successiva.

Per le implementazioni mobili di Edge Network, questa funzione è supportata nel [Identità per rete Edge](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) estensione che inizia con la versione 1.1.0 (iOS e Android).

## Condivisione di ID da mobile a web {#mobile-to-web}

Utilizza la `getUrlVariables` API da [Identità per rete Edge](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) per recuperare gli identificatori come parametri di query e allegarli all&#39;URL all&#39;apertura [!DNL webViews].

Per accettare l’SDK web, non è necessaria alcuna configurazione aggiuntiva `ECID` nella stringa query.

Il parametro della stringa di query include:

* `MCID`: L&#39;ID Experience Cloud (`ECID`)
* `MCORGID`: L&#39;Experience Cloud `orgID` che deve corrispondere al `orgID` configurato in [!DNL Web SDK].
* `TS`: Un parametro di marca temporale che non può essere più vecchio di cinque minuti.


La condivisione degli ID da mobile a web utilizza l’ `adobe_mc` parametro . Quando il `adobe_mc` è presente e valido, il `ECID` dalla stringa query viene aggiunta automaticamente alla mappa identità nella prima richiesta effettuata a Edge Network. Tutte le successive interazioni di Edge Network utilizzeranno `ECID`.

Per ulteriori informazioni su come passare gli ID visitatore da un’app mobile a una WebView, consulta la documentazione su [gestione di WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Condivisione di ID tra domini diversi {#cross-domain-sharing}

Per la condivisione di ID tra domini diversi, la versione 2.11.0 dell’SDK per web aggiunge il supporto per la `appendIdentityToUrl` comando. Se utilizzato, questo comando genera il `adobe_mc` parametro della stringa query.

Il comando accetta un oggetto con una proprietà, `url`e restituisce un oggetto con la proprietà `url`.

Questo comando non attende alcun aggiornamento del consenso. Se non è stato fornito il consenso, l’URL viene restituito invariato.

Se `ECID` non è fornito, `/acquire` verrà chiamato per generare un `ECID`.

Di seguito è riportato un esempio di come un cliente può implementare la condivisione di ID tra domini diversi sul suo sito web.

Questo codice aggiunge un listener di eventi per tutti i clic sulla pagina e se il clic si trovava su un collegamento a un dominio corrispondente (in questo caso `adobe.com` o `behance.com`), aggiunge l&#39;identità all&#39;URL e vi reindirizzerà l&#39;utente.

```js
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

## Utilizzo dell’estensione Tag {#tags-extension}

Simile all’utilizzo del [!DNL Web SDK], non è necessaria alcuna configurazione aggiuntiva nel [!DNL Tags] per utilizzare le identità trasmesse attraverso l&#39;URL.

Per utilizzare la condivisione di ID da mobile a web e tra domini diversi tramite l’estensione Tag, devi utilizzare la versione 2.12.0 o successiva dell’estensione Tag.

Per condividere le identità dalla pagina corrente ad altri domini, è disponibile una nuova azione nel [!DNL Web SDK] [!DNL Tags] estensione. Questa azione è progettata per essere utilizzata con un **[!UICONTROL Core - Click]** tipo di evento e condizione di confronto dei valori.

Segui i passaggi descritti [qui](../../tags/ui/managing-resources/rules.md) per creare una regola con la configurazione seguente:

* [!UICONTROL Configurazione evento]:
   * **[!UICONTROL Estensione: Core]**
   * **[!UICONTROL Tipo evento: Fai clic su]**
   * Seleziona **[!UICONTROL Quando l&#39;utente fa clic su > elementi specifici]**
   * Digita nel **[!UICONTROL Selettore]**: `a[href]`. Questo evento si attiva ogni volta che si fa clic su un tag di ancoraggio sulla pagina con un `href` proprietà.

      ![Immagine dell’interfaccia utente che mostra la configurazione dell’evento con le impostazioni descritte sopra](assets/id-sharing-event-configuration.png)

* [!UICONTROL Configurazione condizione]
   * **[!UICONTROL Tipo di logica]**: [!UICONTROL Regolare]
   * **[!UICONTROL Estensione]**: [!UICONTROL Core]
   * **[!UICONTROL Tipo di condizione]**: [!UICONTROL Value Comparison]
   * **[!UICONTROL Operatore a sinistra]**: [!UICONTROL `%this.hostname%`]. Questo è un elemento dati speciale che funziona con [!UICONTROL Core - Click] e restituisce il nome host del collegamento su cui hai fatto clic.
   * **[!UICONTROL Operatore]**: [!UICONTROL Matches Regex]
   * **[!UICONTROL Opera destra]**: Digita un’espressione regolare che corrisponda ai domini con cui desideri condividere le identità. Ad esempio, per far corrispondere i collegamenti con i nomi host che terminano con `adobe.com` o `behance.com`, utilizza questa espressione regolare: `behance.com$|adobe.com$`. La pagina collegata deve avere [!DNL Web SDK] o [!DNL Visitor ID] installato per accettare l&#39;identità.

      ![Immagine dell’interfaccia utente che mostra la configurazione della condizione con le impostazioni descritte sopra](assets/id-sharing-condition-configuration.png)

* [!UICONTROL Configurazione azione]
   * **[!UICONTROL Estensione]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Tipo di azione]**: [!UICONTROL Reindirizzamento con identità]
   * **[!UICONTROL Istanza]**: Seleziona la tua istanza. Nella maggior parte dei casi, sarà configurata una sola istanza. Se disponi di più istanze, seleziona quella con l’identità da condividere.

      ![Immagine dell’interfaccia utente che mostra la configurazione dell’azione con le impostazioni descritte sopra](assets/id-sharing-action-configuration.png)

La **[!UICONTROL Reindirizzamento con identità]** impedisce al browser di spostarsi all’interno del collegamento. Quindi, chiamerà il `appendIdentityToUrl` metodo [!DNL Web SDK] istanza.

Infine, reindirizza l’utente al [!DNL URL] con `adobe_mc` parametro della stringa query aggiunto.
