---
title: Condivisione ID da dispositivo mobile a web e tra domini
description: Scopri come rendere persistenti gli ID visitatore da dispositivi mobili alle proprietà web e tra domini
keywords: Identity;mobile;id;condivisione;dominio;cross-domain;sdk;platform;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '457'
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

## Implementare la condivisione ID tra domini {#cross-domain-sharing}

Consulta la [`appendIdentityToUrl`](../commands/appendidentitytourl.md) comando per le istruzioni di implementazione tramite l’estensione tag Web SDK e la libreria JavaScript Web SDK.
