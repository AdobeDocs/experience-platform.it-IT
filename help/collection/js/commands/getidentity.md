---
title: getIdentity
description: Ottenere l’identità di un visitatore senza inviare i dati dell’evento.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: aea46e3804d315c1237fc853540771f1b5c2b767
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 2%

---

# `getIdentity`

Quando si esegue il comando [`sendEvent`](sendevent/overview.md), Web SDK ottiene automaticamente l&#39;identità del visitatore, se non ne è già presente una. Il comando `getIdentity` ti consente di ottenere un ID visitatore senza inviare dati evento. Se hai bisogno di chiamate separate per generare un ID visitatore e inviare dati, puoi utilizzare questo comando.

Il comando `getIdentity` esegue il seguente flusso per recuperare `ECID`.

1. Il Web SDK viene utilizzato per chiamare `getIdentity` o [`appendIdentityToUrl`](appendidentitytourl.md).
1. Web SDK attende di ricevere le informazioni sul consenso.
1. Web SDK controlla se lo spazio dei nomi `ECID` è stato richiesto nella chiamata. Per impostazione predefinita, lo spazio dei nomi `ECID` è sempre incluso.
1. Web SDK legge il cookie `kndctr` e restituisce il relativo valore come `ECID`, se esiste. Restituisce solo il valore `ECID`, ma non `regionId`.
1. Se il cookie di identità `kndctr` non è impostato o è stato richiesto lo spazio dei nomi `"CORE"`, Web SDK invia una richiesta all&#39;Edge Network.
1. Edge Network restituisce sia `ECID` che `regionId` (e `CORE ID`, se richiesto).

Eseguire il comando `getIdentity` quando si chiama l&#39;istanza configurata del Web SDK. Durante la configurazione di questo comando sono disponibili le seguenti opzioni:

* **`namespaces`**: matrice di spazi dei nomi. Il valore predefinito è `["ECID"]`. Altri valori supportati includono:
   * `["CORE"]`
   * `["ECID","CORE"]`
   * `null`
   * `undefined`

  È possibile richiedere `"ECID"` e `"CORE ID"` contemporaneamente. Esempio: `"namespaces": ["ECID","CORE"]`.

* **`edgeConfigOverrides`**: [oggetto di override della configurazione dello stream di dati](configure/edgeconfigoverrides.md).

```js
alloy("getIdentity",{
  // This command retrieves both ECID and CORE IDs
  "namespaces": ["ECID","CORE"] 
});
```

## Oggetto di risposta

Se decidi di [gestire le risposte](command-responses.md) con questo comando, nell&#39;oggetto di risposta sono disponibili le seguenti proprietà:

* **`identity.ECID`**: stringa contenente l&#39;identificatore ECID del visitatore.
* **`identity.CORE`**: stringa contenente l&#39;ID CORE del visitatore.
* **`edge.regionID`**: un numero intero che rappresenta l&#39;area Edge Network che il browser ha raggiunto quando ha acquisito un&#39;identità. È lo stesso dell’hint di posizione legacy di Audience Manager.

```js
// Get the visitor's ECID
alloy('getIdentity').then(result => {
  console.log(result.identity.ECID);
});
```

## Ottenere l’identità tramite l’estensione tag Web SDK

L’estensione tag Web SDK non offre questo comando tramite l’interfaccia utente dell’estensione tag. Utilizza l’editor di codice personalizzato utilizzando la sintassi della libreria di JavaScript.
