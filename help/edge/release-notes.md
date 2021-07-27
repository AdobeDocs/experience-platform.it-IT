---
title: Note sulla versione di Adobe Experience Platform Web SDK
description: Note sulla versione più recente di Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;note sulla versione;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: e158b8129fe5afe71af48b7c64ca34b00e79965c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Note sulla versione

## Versione 2.6.0 - 27 luglio 2021

* Fornisce più contenuto di personalizzazione nella promessa risolta `sendEvent`, inclusi i token di risposta di Adobe Target. Quando viene eseguito il comando `sendEvent`, viene restituita una promessa, che viene risolta con un oggetto `result` contenente le informazioni ricevute dal server. Questo oggetto risultato include una proprietà denominata `decisions`. Questa proprietà `decisions` è stata dichiarata obsoleta. È stata aggiunta una nuova proprietà, `propositions`. Questa nuova proprietà consente ai clienti di accedere a più contenuti di personalizzazione, inclusi i token di risposta. A breve sarà disponibile ulteriore documentazione.

## Versione 2.5.0 - giugno 2021

* È stato aggiunto il supporto per le offerte di personalizzazione di reindirizzamento.
* Le larghezze e le altezze del riquadro di visualizzazione raccolte automaticamente con valori negativi non verranno più inviate al server.
* Quando un evento viene annullato restituendo `false` da un callback `onBeforeEventSend`, ora viene registrato un messaggio.
* È stato risolto un problema a causa del quale parti specifiche di dati XDM destinate a un singolo evento venivano incluse in più eventi.

## Versione 2.4.0 - marzo 2021

* L&#39;SDK può ora essere [installato come pacchetto npm](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html).
* È stato aggiunto il supporto per un&#39;opzione `out` quando [configuri il consenso predefinito](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), che rilascia tutti gli eventi fino alla ricezione del consenso (l&#39;opzione esistente `pending` mette in coda gli eventi e li invia una volta ricevuto il consenso).
* È ora possibile utilizzare il callback [onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) per impedire l&#39;invio di un evento.
* Utilizza ora un gruppo di campi di schema XDM invece di `meta.personalization` quando invii eventi relativi a contenuti personalizzati di cui viene eseguito il rendering o su cui si fa clic.
* Il comando [getIdentity](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) restituisce ora l’ID dell’area perimetrale accanto all’identità.
* Gli avvisi e gli errori ricevuti dal server sono stati migliorati e vengono gestiti in modo più appropriato.
* È stato aggiunto il supporto per [Adobe Consent 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Quando vengono ricevute, le preferenze di consenso vengono hashing e memorizzate nell’archivio locale per un’integrazione ottimizzata tra CMP, Platform Web SDK e Platform Edge Network. Se raccogli le preferenze di consenso, ora ti invitiamo a chiamare `setConsent` a ogni caricamento di pagina.
* Sono stati aggiunti due [hook di monitoraggio](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` e `onCommandRejected`.
* Correzione bug: Gli eventi di notifica dell’interazione di personalizzazione conterrebbero informazioni duplicate sulla stessa attività quando un utente passava a una nuova visualizzazione di app a pagina singola, tornava alla visualizzazione originale e faceva clic su un elemento idoneo alla conversione.
* Correzione bug: Se il primo evento inviato dall&#39;SDK aveva `documentUnloading` impostato su `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) verrebbe utilizzato per inviare l&#39;evento, dando luogo a un errore relativo a un&#39;identità non stabilita.

## Versione 2.3.0 - novembre 2020

* È stato aggiunto il supporto nonce per consentire criteri di sicurezza dei contenuti più rigorosi.
* È stato aggiunto il supporto per la personalizzazione per le applicazioni a pagina singola.
* È stata migliorata la compatibilità con altri codici JavaScript on-page che potrebbero sovrascrivere `window.console` API.
* Correzione bug: `sendBeacon` non veniva utilizzato quando `documentUnloading` era impostato su `true` o quando i clic sul collegamento venivano tracciati automaticamente.
* Correzione bug: Un collegamento non viene tracciato automaticamente se l’elemento di ancoraggio contiene contenuto HTML.
* Correzione bug: Alcuni errori del browser contenenti una proprietà di sola lettura `message` non sono stati gestiti in modo appropriato, causando un diverso errore esposto al cliente.
* Correzione bug: L&#39;esecuzione dell&#39;SDK all&#39;interno di un iframe comporterebbe un errore se la pagina HTML dell&#39;iframe proviene da un sottodominio diverso rispetto alla pagina HTML della finestra principale.

## Versione 2.2.0 - ottobre 2020

* Correzione bug: L&#39;oggetto Opt-in impediva ad Alloy di effettuare chiamate quando `idMigrationEnabled` è `true`.
* Correzione bug: Presta attenzione alle richieste che dovrebbero restituire le offerte di personalizzazione per evitare un problema di sfarfallio.

## Versione 2.1.0 - agosto 2020

* Rimuovi il comando `syncIdentity` e supporta il passaggio di tali ID nel comando `sendEvent` .
* Supporto dello standard di consenso IAB 2.0.
* Supporto per il passaggio di ID aggiuntivi nel comando `setConsent` .
* È supportata l&#39;override di `datasetId` nel comando `sendEvent`.
* Monitor compatibili ([Ulteriori informazioni](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Passa `environment: browser` nei dati contestuali dei dettagli di implementazione.
