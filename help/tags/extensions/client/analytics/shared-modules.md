---
title: Moduli condivisi per l'estensione Adobe Analytics
description: Scopri i moduli libreria condivisi forniti dall’estensione tag Adobe Analytics in Adobe Experience Platform.
exl-id: f1d7cb2b-0058-46f9-983c-079079e06057
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 95%

---

# Moduli condivisi per l&#39;estensione Adobe Analytics

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L&#39;estensione [Adobe Analytics](./overview.md) offre due diversi [moduli condivisi](../../../extension-dev/web/shared.md) che è possibile integrare nell&#39;applicazione Experience. Tali moduli sono trattati nelle sezioni seguenti.

## [!DNL get-tracker]

Prima di poter inviare i beacon, Adobe Analytics deve inizializzare l&#39;oggetto tracker. Il processo di inizializzazione inizia caricando [AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=it), seguito dalla creazione di un oggetto tracker.

Dopo che è stato completamente inizializzato, puoi accedere all&#39;oggetto tracker utilizzando il modulo condiviso `get-tracker` nel modo seguente:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

getTracker().then(function(tracker) {
  // Use tracker in some way
});
```

### Verifica dell&#39;installazione di Adobe Analytics

È possibile che Adobe Analytics non sia stata installata oppure non sia stata inclusa nella stessa libreria di tag come estensione. Per questo motivo, ti consigliamo di verificarlo nel codice e di gestirlo nel modo appropriato. Il JavaScript riportato qui di seguito mostra il modo in cui potresti implementarlo:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

if (getTracker) {
  getTracker().then(function(tracker) {
    // Use tracker in some way
  });
} else {
  turbine.logger.error("The Adobe Analytics extension is required for Extension XYZ to function properly.");
}
```

Se `getTracker` è `undefined`, significa che l’estensione Adobe Analytics non esiste nella libreria di tag. Puoi personalizzare il messaggio registrato per riflettere con precisione quale funzionalità potrebbe andare persa se l&#39;estensione Adobe Analytics non è stata installata.


## [!DNL augment-tracker]

Successivamente all&#39;inizializzazione dell&#39;oggetto tracker, il passaggio successivo della procedura è il potenziamento. Questo passaggio dà all’estensione la possibilità di potenziare il tracker con tutto ciò che è necessario prima che siano state applicate le variabili dalla configurazione di Adobe Analytics oppure prima che siano stati inviati i beacon.

Inoltre, l&#39;estensione ha l&#39;opportunità di sospendere il processo di inizializzazione del tracker mentre esegue un&#39;altra attività asincrona, come ad esempio il recupero di dati o di JavaScript da un server.

Puoi implementare il modulo `augment-tracker` nel modo seguente:

```js
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  // Augment tracker in some way
});
```

La funzione trasferita in `augmentTracker()` verrà richiamata non appena viene raggiunta la fase di potenziamento del processo di inizializzazione del tracker.

Se, prima di potenziare il tracker, l&#39;estensione deve completare un&#39;attività asincrona, puoi restituire una promessa dalla tua funzione nel modo seguente:

```js
var Promise = require('@adobe/reactor-promise');
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  return new Promise(function(resolve) {
    // Augment the tracker object, then call resolve()
  });
});
```

Restituendo una promessa, l&#39;estensione indica a Adobe Analytics di mettere in pausa il processo di inizializzazione del tracker fino a quando la promessa non è stata risolta.

>[!WARNING]
>
>Presta attenzione quando interrompi il processo di inizializzazione del tracker, in quanto può ritardare l&#39;invio dei beacon e quindi determinare la mancata raccolta dei dati (ad esempio, se l&#39;utente esce dalla pagina prima che il beacon sia inviato).
