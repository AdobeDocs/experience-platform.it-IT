---
title: Note sulla versione dell’SDK per web di Adobe Experience Platform
seo-title: Note sulla versione dell’SDK per web di Adobe Experience Platform
description: Note sulla versione dell’SDK per web di Adobe Experience Platform.
seo-description: Note sulla versione dell’SDK per web di Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 77c1e693668bc50a81713d02cfe4b0fabc661404
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 14%

---


# Note sulla versione

## Versione 2.3.0

* È stato aggiunto il supporto per consentire l&#39;applicazione di criteri di protezione dei contenuti più severi.
* È stato aggiunto il supporto per la personalizzazione per le applicazioni a pagina singola.
* È stata migliorata la compatibilità con altri codici JavaScript presenti sulla pagina che potrebbero sovrascrivere `window.console` le API.
* Correzione dei bug: `sendBeacon` non veniva utilizzato quando `documentUnloading` era impostato su `true` o quando i clic del collegamento venivano tracciati automaticamente.
* Correzione dei bug: Un collegamento non viene tracciato automaticamente se l&#39;elemento di ancoraggio conteneva contenuto HTML.
* Correzione dei bug: Alcuni errori del browser contenenti una proprietà di sola lettura non sono stati gestiti in modo appropriato, con conseguente esposizione al cliente di un errore diverso. `message`
* Correzione dei bug: L&#39;esecuzione dell&#39;SDK all&#39;interno di un iframe causerebbe un errore se la pagina HTML dell&#39;iframe provenisse da un sottodominio diverso rispetto alla pagina HTML della finestra principale.

## Versione 2.2.0

* Correzione dei bug: L&#39;oggetto Opt-in impediva ad Alloy di effettuare chiamate quando `idMigrationEnabled` è `true`.
* Correzione dei bug: Rendete già consapevoli delle richieste che dovrebbero restituire le offerte di personalizzazione per evitare un problema sfarfallio.

## Versione 2.1.0

* Rimuovere il `syncIdentity` comando e supportare il passaggio di tali ID nel `sendEvent` comando.
* Supporto di IAB 2.0 Consent Standard.
* Supporto per il passaggio di ID aggiuntivi nel `setConsent` comando.
* Supporto per la sostituzione del `datasetId` comando nel `sendEvent` .
* Monitor di supporto ([Per saperne di più](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Passa `environment: browser` i dati contestuali dei dettagli di implementazione.
