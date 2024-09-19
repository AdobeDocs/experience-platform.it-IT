---
title: getIdentity
description: Ottenere l’identità di un visitatore senza inviare i dati dell’evento.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# `getIdentity`

Il comando `getIdentity` ti consente di ottenere un ID visitatore senza inviare dati evento. Quando esegui il comando `sendEvent`, Web SDK ottiene automaticamente l&#39;identità del visitatore, se non è già presente.

Se hai bisogno di chiamate separate per generare un ID visitatore e inviare dati, puoi utilizzare questo comando.

## Ottenere l’identità tramite l’estensione tag Web SDK

L’estensione tag Web SDK non offre questo comando tramite l’interfaccia utente dell’estensione tag. Utilizza l’editor di codice personalizzato utilizzando la sintassi della libreria di JavaScript.

## Ottenere l’identità tramite la libreria JavaScript dell’SDK web

Esegui il comando `getIdentity` quando chiami l&#39;istanza configurata dell&#39;SDK Web. Durante la configurazione di questo comando sono disponibili le seguenti opzioni:

* **`namespaces`**: matrice di spazi dei nomi. Il valore predefinito è `["ECID"]`. Altri valori supportati sono: `["CORE"]`, `null`, `undefined`. È possibile richiedere [!DNL ECID] e [!DNL CORE ID] contemporaneamente. Esempio: `"namespaces": ["ECID","CORE"]`.
* **`edgeConfigOverrides`**: [oggetto di override della configurazione dello stream di dati](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID","CORE"] //this command retrieves both ECID and CORE IDs.
});
```

## Oggetto di risposta

Se decidi di [gestire le risposte](command-responses.md) con questo comando, nell&#39;oggetto di risposta sono disponibili le seguenti proprietà:

* **`identity.ECID`**: stringa contenente l&#39;identificatore ECID del visitatore.
* **`identity.CORE`**: stringa contenente l&#39;ID CORE del visitatore.
* **`edge.regionID`**: numero intero che rappresenta l&#39;area di Edge Network visualizzata dal browser durante l&#39;acquisizione di un&#39;identità. È lo stesso dell’hint di posizione Audience Manager legacy.
