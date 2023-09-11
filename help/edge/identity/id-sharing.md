---
title: Condivisione ID da dispositivo mobile a web e tra domini
description: Scopri come rendere persistenti gli ID visitatore da dispositivi mobili alle proprietà web e tra domini
keywords: Identity;mobile;id;condivisione;dominio;cross-domain;sdk;platform;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 139d6a6632532b392fdf8d69c5c59d1fd779a6d1
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# Condivisione ID da dispositivo mobile a web e tra domini

## Panoramica

Adobe Experience Platform Web SDK supporta le funzionalità di condivisione degli ID visitatore, che consentono ai clienti di fornire esperienze personalizzate in modo più accurato, tra app mobili e contenuti web per dispositivi mobili e tra domini diversi.

## Casi d’uso {#use-cases}

### Distribuire una personalizzazione coerente tra app mobili e siti web per dispositivi mobili

Un’azienda di abbigliamento vuole personalizzare l’esperienza dei propri clienti in base ai loro interessi e mantenere accurata la personalizzazione in un’app mobile che carica anche WebViews. Utilizzando la funzione di condivisione ID da dispositivo mobile a web, possono garantire che vengano presentate ai clienti le offerte più precise, utilizzando lo stesso identificatore visitatore nell’app e contenuti web per dispositivi mobili trasmettendo [!DNL ECID] all’URL web del dispositivo mobile.

### Distribuire una personalizzazione coerente tra i domini

Un rivenditore con più negozi online desidera personalizzare l’esperienza dell’acquirente nei suoi domini, in base agli interessi del cliente. Utilizzando la funzione di condivisione ID tra domini dell’SDK web, il rivenditore può distribuire offerte precise in base agli interessi dei clienti, su tutti i loro domini.

### Migliorare il reporting delle attività dei visitatori

Un rivenditore di tecnologia vuole migliorare il reporting delle attività dei visitatori con informazioni su quando i visitatori passano dall’app mobile al sito web mobile o ad altri domini. Utilizzando la funzione di condivisione ID tra domini diversi dell’SDK per web, il team marketing può tracciare con precisione i visitatori nelle loro proprietà web e generare rapporti sulle attività.

## Prerequisiti {#prerequisites}

Per utilizzare la condivisione ID da dispositivo mobile a web e tra domini diversi, devi utilizzare [!DNL Web SDK] versione 2.11.0 o successiva.

Per le implementazioni mobili Edge Network, questa funzione è supportata nella [Identità per Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) estensione che inizia con la versione 1.1.0 (iOS e Android).

Questa funzione è compatibile anche con [!DNL VisitorAPI.js] versione 1.7.0 o successiva.

## Condivisione ID da dispositivo mobile a web {#mobile-to-web}

Utilizza il `getUrlVariables` API da [Identità per Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) per recuperare gli identificatori come parametri di query e allegarli all’URL quando apri [!DNL webViews].

Non è richiesta alcuna configurazione aggiuntiva per l’accettazione da parte dell’SDK web `ECID` valori nella stringa query.

Il parametro della stringa di query include:

* `MCID`: ID dell’Experience Cloud (`ECID`)
* `MCORGID`: L’Experience Cloud `orgID` che deve corrispondere al `orgID` configurato in [!DNL Web SDK].
* `TS`: parametro di marca temporale che non può essere precedente ai cinque minuti.


La condivisione ID da dispositivo mobile a Web utilizza `adobe_mc` parametro. Quando `adobe_mc` è presente e valido, il `ECID` dalla stringa di query viene aggiunta automaticamente alla mappa delle identità nella prima richiesta effettuata alla rete Edge. Tutte le interazioni successive di Edge Network utilizzeranno tale `ECID`.

Per ulteriori informazioni su come passare gli ID visitatore da un’app mobile a una WebView, consulta la documentazione su [gestione di WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Condivisione ID tra domini {#cross-domain-sharing}

Per la condivisione ID tra domini, l&#39;SDK Web versione 2.11.0 aggiunge il supporto per `appendIdentityToUrl` comando. Se utilizzato, questo comando genera il `adobe_mc` parametro stringa query.

Il comando accetta un oggetto con una proprietà, `url`, e restituisce un oggetto con la proprietà `url`.

Questo comando non attende alcun aggiornamento del consenso. Se non è stato fornito il consenso, l’URL viene restituito invariato.

Se un `ECID` non viene fornito, il `/acquire` verrà chiamato l&#39;endpoint per generare un `ECID`.

Di seguito è riportato un esempio di come un cliente può implementare la condivisione ID tra domini diversi sul proprio sito web.

Questo codice aggiunge un listener di eventi per tutti i clic sulla pagina e, se il clic si trovava su un collegamento a un dominio corrispondente (in questo caso `adobe.com` o `behance.com`), aggiunge l’identità all’URL e reindirizza l’utente lì.

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

Simile all&#39;utilizzo di [!DNL Web SDK], non è necessaria alcuna configurazione aggiuntiva nel [!DNL Tags] per utilizzare le identità passate attraverso l&#39;URL.

Per utilizzare la condivisione ID da dispositivo mobile a web e tra domini diversi tramite l’estensione Tag, è necessario utilizzare la versione 2.12.0 o successiva dell’estensione Tag.

Per condividere le identità dalla pagina corrente ad altri domini, è disponibile una nuova azione in [!DNL Web SDK] [!DNL Tags] estensione. Questa azione è progettata per essere utilizzata con **[!UICONTROL Core - Clic]** tipo di evento e una condizione di confronto dei valori.

Segui i passaggi descritti [qui](../../tags/ui/managing-resources/rules.md) per creare una regola con la seguente configurazione:

* [!UICONTROL Configurazione evento]:
   * **[!UICONTROL Estensione: Core]**
   * **[!UICONTROL Tipo evento: fai clic su]**
   * Seleziona **[!UICONTROL Quando l’utente fa clic su > elementi specifici]**
   * Digita nella **[!UICONTROL Selettore]**: `a[href]`. Questo evento si attiva ogni volta che si fa clic su un tag di ancoraggio sulla pagina con un `href` proprietà.

     ![Immagine dell’interfaccia utente che mostra la configurazione dell’evento con le impostazioni descritte in precedenza](assets/id-sharing-event-configuration.png)

* [!UICONTROL Configurazione condizione]
   * **[!UICONTROL Tipo di logica]**: [!UICONTROL Normale]
   * **[!UICONTROL Estensione]**: [!UICONTROL Core]
   * **[!UICONTROL Tipo di condizione]**: [!UICONTROL Value Comparison]
   * **[!UICONTROL Operando sinistro]**: [!UICONTROL `%this.hostname%`]. Questo è un elemento dati speciale che funziona con [!UICONTROL Core - Clic] e viene risolto nel nome host del collegamento su cui è stato fatto clic.
   * **[!UICONTROL Operatore]**: [!UICONTROL Corrisponde a Regex]
   * **[!UICONTROL Operando destro]**: digita un’espressione regolare che corrisponda ai domini con cui desideri condividere le identità. Ad esempio, per associare i collegamenti con nomi host che terminano con `adobe.com` o `behance.com`, utilizza questa espressione regolare: `behance.com$|adobe.com$`. La pagina collegata deve avere [!DNL Web SDK] o [!DNL Visitor ID] installato per accettare l’identità.

     ![Immagine dell’interfaccia utente che mostra la configurazione della condizione con le impostazioni descritte in precedenza](assets/id-sharing-condition-configuration.png)

* [!UICONTROL Configurazione azione]
   * **[!UICONTROL Estensione]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Tipo di azione]**: [!UICONTROL Reindirizza con identità]
   * **[!UICONTROL Istanza]**: seleziona l’istanza. Nella maggior parte dei casi, sarà configurata una sola istanza. Se disponi di più istanze, seleziona quella con l’identità da condividere.

     ![Immagine dell’interfaccia utente che mostra la configurazione dell’azione con le impostazioni descritte in precedenza](assets/id-sharing-action-configuration.png)

Il **[!UICONTROL Reindirizza con identità]** impedirà al browser di passare al collegamento. Quindi, chiamerà `appendIdentityToUrl` metodo su [!DNL Web SDK] dell&#39;istanza.

Infine, reindirizza l’utente al [!DNL URL] con `adobe_mc` parametro stringa query aggiunto.
