---
title: Note sulla versione di Adobe Experience Platform Web SDK
description: Note sulla versione più recente di Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;note sulla versione;
translation-type: tm+mt
source-git-commit: b0e6d1f7cf7302bb3a7403bb18dfd8b7489d583e
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 4%

---


# Note sulla versione

## Versione 2.4.0

* L&#39;SDK può ora essere [installato come pacchetto npm](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html).
* È stato aggiunto il supporto per un&#39;opzione `out` quando [configuri il consenso predefinito](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), che rilascia tutti gli eventi fino alla ricezione del consenso (l&#39;opzione esistente `pending` mette in coda gli eventi e li invia una volta ricevuto il consenso).
* È ora possibile utilizzare il callback [onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) per impedire l&#39;invio di un evento.
* Ora utilizza un mixin XDM invece di `meta.personalization` quando si inviano eventi su contenuti personalizzati di cui si sta facendo clic o su di essi.
* Il comando [getIdentity](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) restituisce ora l’ID dell’area perimetrale accanto all’identità.
* Gli avvisi e gli errori ricevuti dal server sono stati migliorati e vengono gestiti in modo più appropriato.
* È stato aggiunto il supporto per [Adobe Consent 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Quando vengono ricevute, le preferenze di consenso vengono hashing e memorizzate nell’archivio locale per un’integrazione ottimizzata tra CMP, Platform Web SDK e Platform Edge Network. Se raccogli le preferenze di consenso, ora ti invitiamo a chiamare `setConsent` a ogni caricamento di pagina.
* Sono stati aggiunti due [hook di monitoraggio](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` e `onCommandRejected`.
* Correzione bug: Gli eventi di notifica dell’interazione di personalizzazione conterrebbero informazioni duplicate sulla stessa attività quando un utente passava a una nuova visualizzazione di app a pagina singola, tornava alla visualizzazione originale e faceva clic su un elemento idoneo alla conversione.
* Correzione bug: Se il primo evento inviato dall&#39;SDK aveva `documentUnloading` impostato su `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) verrebbe utilizzato per inviare l&#39;evento, dando luogo a un errore relativo a un&#39;identità non stabilita.

## Versione 2.3.0

* È stato aggiunto il supporto nonce per consentire criteri di sicurezza dei contenuti più rigorosi.
* È stato aggiunto il supporto per la personalizzazione per le applicazioni a pagina singola.
* È stata migliorata la compatibilità con altri codici JavaScript on-page che potrebbero sovrascrivere `window.console` API.
* Correzione bug: `sendBeacon` non veniva utilizzato quando `documentUnloading` era impostato su `true` o quando i clic sul collegamento venivano tracciati automaticamente.
* Correzione bug: Un collegamento non viene tracciato automaticamente se l’elemento di ancoraggio contiene contenuto HTML.
* Correzione bug: Alcuni errori del browser contenenti una proprietà di sola lettura `message` non sono stati gestiti in modo appropriato, causando un diverso errore esposto al cliente.
* Correzione bug: L&#39;esecuzione dell&#39;SDK all&#39;interno di un iframe comporterebbe un errore se la pagina HTML dell&#39;iframe proviene da un sottodominio diverso rispetto alla pagina HTML della finestra principale.

## Versione 2.2.0

* Correzione bug: L&#39;oggetto Opt-in impediva ad Alloy di effettuare chiamate quando `idMigrationEnabled` è `true`.
* Correzione bug: Presta attenzione alle richieste che dovrebbero restituire le offerte di personalizzazione per evitare un problema di sfarfallio.

## Versione 2.1.0

* Rimuovi il comando `syncIdentity` e supporta il passaggio di tali ID nel comando `sendEvent` .
* Supporto dello standard di consenso IAB 2.0.
* Supporto per il passaggio di ID aggiuntivi nel comando `setConsent` .
* È supportata l&#39;override di `datasetId` nel comando `sendEvent`.
* Monitor compatibili ([Ulteriori informazioni](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Passa `environment: browser` nei dati contestuali dei dettagli di implementazione.
