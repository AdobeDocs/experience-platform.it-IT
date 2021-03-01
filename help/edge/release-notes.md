---
title: Note sulla versione di Adobe Experience Platform Web SDK
description: Note sulla versione più recente di Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;note sulla versione;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 10%

---


# Note sulla versione

## Versione 2.3.0

* È stato aggiunto il supporto per consentire l&#39;applicazione di criteri di protezione dei contenuti più severi.
* È stato aggiunto il supporto per la personalizzazione per le applicazioni a pagina singola.
* È stata migliorata la compatibilità con altri codici JavaScript presenti sulla pagina che potrebbero sovrascrivere le API `window.console`.
* Correzione dei bug: `sendBeacon` non veniva utilizzato quando `documentUnloading` era impostato su `true` o quando i clic del collegamento venivano tracciati automaticamente.
* Correzione dei bug: Un collegamento non viene tracciato automaticamente se l&#39;elemento di ancoraggio conteneva contenuto HTML.
* Correzione dei bug: Alcuni errori del browser contenenti una proprietà di sola lettura `message` non sono stati gestiti in modo appropriato, causando un errore diverso da essere esposto al cliente.
* Correzione dei bug: L&#39;esecuzione dell&#39;SDK all&#39;interno di un iframe causerebbe un errore se la pagina HTML dell&#39;iframe provenisse da un sottodominio diverso rispetto alla pagina HTML della finestra principale.

## Versione 2.2.0

* Correzione dei bug: L&#39;oggetto Opt-in impediva ad Alloy di effettuare chiamate quando `idMigrationEnabled` è `true`.
* Correzione dei bug: Rendete già consapevoli delle richieste che dovrebbero restituire le offerte di personalizzazione per evitare un problema sfarfallio.

## Versione 2.1.0

* Rimuovere il comando `syncIdentity` e supportare il passaggio di tali ID nel comando `sendEvent`.
* Supporto di IAB 2.0 Consent Standard.
* Supporto per il passaggio di ID aggiuntivi nel comando `setConsent`.
* Supporto per la sostituzione di `datasetId` nel comando `sendEvent`.
* Monitor di supporto ([Leggi tutto](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Passa `environment: browser` nei dati contestuali dei dettagli di implementazione.
