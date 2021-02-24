---
title: Note sulla versione di Adobe Experience Platform Web SDK Extension
description: Estensione Adobe Experience Platform Web SDK in Adobe Experience Platform Launch
seo-description: Estensione Adobe Experience Platform Web SDK in Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 89%

---


# Note sulla versione dell’estensione Adobe Experience Platform Web SDK

Questo documento illustra le note sulla versione dell’estensione Adobe Experience Platform Web SDK per  Adobe Experience Platform Launch. Per le ultime note sulla versione dell&#39;SDK stesso, vedi le note sulla versione dell&#39;SDK Web [della piattaforma](https://docs.adobe.com/content/help/it-IT/experience-platform/edge/release-notes.html).

## 4 novembre 2020

### Adobe Experience Platform Web SDK 2.3.0

Contiene la versione 2.3.0 della libreria dell’SDK per web di Adobe Experience Platform.

#### Funzioni

* È stato aggiunto il supporto per l’utilizzo di un elemento dati durante la configurazione del consenso predefinito.
* È stata aggiunta la possibilità di cercare schemi XDM con il tipo elemento dati di oggetti XDM.
* È stata aggiunta la duplicazione di dati XDM all’interno del tipo di azione Invia evento per garantire che eventuali modifiche successive all’oggetto dati XDM non vengano riportate nella richiesta.

## 1º ottobre 2020

### Adobe Experience Platform Web SDK 2.2.0

#### Correzioni di bug

* Quando si tentava di creare un oggetto XDM da schemi sandbox, si verificavano problemi di autenticazione. L&#39;API che chiama Piattaforma ora è a conoscenza degli ambienti, quindi agli utenti vengono presentati solo gli schemi a cui hanno accesso per la modifica.

#### Funzioni

* Quando si utilizza l’elemento dati `identityMap`, gli spazi dei nomi vengono ora precompilati in un menu a discesa e non è più necessario compilarli manualmente.
* È stata rivista l’interfaccia utente per l’elemento dati `xdmObject`. Nella nuova interfaccia è possibile vedere quali campi sono stati compilati, senza dover accedere a ciascun elemento nell’oggetto.


## 26 agosto 2020

### Adobe Experience Platform Web SDK 2.1.1

#### Funzioni

* È stato risolto un problema che impediva la corretta visualizzazione delle sandbox di Adobe Experience Platform nella vista Oggetto XDM. Con questa versione dell’estensione, se non viene elencata una sandbox prevista, l’utente deve rivolgersi al proprio amministratore di Adobe Experience Platform per verificare che le autorizzazioni di accesso siano impostate correttamente.


## 5 agosto 2020

### Adobe Experience Platform Web SDK 2.1.0

#### Funzioni

* Modifica necessaria: rimuovi l’azione `syncIdentity` e includi al suo posto il passaggio di tali ID nell’azione `sendEvent`. Prima di aggiornare l’estensione, disattiva eventuali regole esistenti che utilizzano l’azione rimossa.
* Aggiornamento ad Alloy v2.1.0 ([Note sulla versione](https://docs.adobe.com/content/help/en/experience-platform/edge/release-notes.html)).
* È supportato lo standard del consenso IAB 2.0 nell’azione `setConsent`.
* È supportata la possibilità di ignorare l’ID del set di dati nell’azione `sendEvent`.
* È stato aggiunto un nuovo elemento dati di tipo `IdentityMap` che può essere utilizzato per compilare la voce `identityMap` nell’elemento dati di oggetti XDM che è ora abilitato e nell’azione `setConsent`.
* È supportato il passaggio di una mappa di identità nell’azione `setConsent`.
* Supporto per la scelta di una sandbox della piattaforma nell&#39;elemento dati oggetto XDM.


## 26 maggio 2020

### Adobe Experience Platform Web SDK 1.0.0

#### Funzioni

* È supportata la selezione dell’ambiente dal servizio di configurazione.


## 4 maggio 2020

### Adobe Experience Platform Web SDK 0.1.2

#### Funzioni

* `configId` è stato rinominato `edgeConfigId`.
* `viewStart` è stato rinominato `renderDecisions` e impostato su false per impostazione predefinita. Se è impostato su true, le offerte di personalizzazione vengono recuperate e sottoposte a rendering automatico.
* Modifiche relative a `Get Decisions`:
   * È stato rimosso il comando `getDecisions`.
   * È stata aggiunta un’opzione `scopes` al comando `sendEvent`. Le decisioni vengono restituite nella promessa risolta `sendEvent`.
   * È stato aggiunto un ambito integrato `__view__` che darà luogo alla restituzione di offerte di visualizzazione ampia della pagina (ad esempio le offerte VEC in Target).
Queste decisioni sono restituite dal comando `sendEvent` solo se `renderDecisions` è impostato su false.
   * È stato aggiunto un evento `Decisions Received` che viene attivato quando le decisioni diventano disponibili.
* Sono state unite più notifiche di personalizzazione in una singola chiamata server.
* È stato risolto un problema in ID unione eventi a causa del quale veniva reimpostato ogni volta che si faceva riferimento all’elemento dati.
* L’azione `setCustomerIds` è stata rinominata `syncIdentity`.
* È stato aggiunto un comando `getIdentity`. Per il momento questo può essere utilizzato solo tramite codice personalizzato.
* Abilitando il debug con `_satellite` ora è possibile eseguire il debug nell&#39;SDK Web di Adobe Experience Platform.
* È stato aggiunto il supporto per i valori digitati nell’oggetto XDM: booleani, numeri e decimali.

## 16 marzo 2020

### Adobe Experience Platform Web SDK 0.0.10

#### Funzioni

* I concetti di Opt-in e Opt-out sono stati combinati in `Consent` ed è stato aggiunto un nuovo comando `setConsent`.
* È stato aggiunto un nuovo elemento dati di tipo `XDM Object` che consente la mappatura da JavaScript/JSON a XDM.

## 18 febbraio 2020

### Adobe Experience Platform Web SDK 0.0.7

#### Funzioni

* Le opzioni idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled e cookieDestinationsEnabled sono state rimosse.
* È stato aggiunto il supporto per i trattini nel valore dell&#39;opzione edgeDomain.
* La richiesta effettuata durante la migrazione degli ID viene inviata all&#39;endpoint demdex per migliorare l&#39;identificazione tra domini se il cookie demdex non è impostato.
* La richiesta effettuata durante la migrazione degli ID prevede sempre una risposta per assicurarsi che venga impostato il cookie di identità.
* Quando si esegue un comando non valido, nella console verrà registrato un elenco di nomi di comando validi.
* È stata aggiunta una casella di controllo per attivare o disattivare il supporto dei cookie di terze parti per l’estensione Adobe Experience Platform Launch. Questa funzione disattiva le chiamate a demdex.net.

## 20 dicembre 2019

### Adobe Experience Platform Web SDK 0.0.5

#### Funzioni

* Aggiunta della configurazione Activity Tracker all’estensione Platform Launch
* Comando esposizione di EventType ed EventMergeId su evento
* Aggiunta della configurazione onBeforeEventSend all’estensione Platform Launch
* Aggiunta della configurazione edgeBasePath all’estensione Platform Launch

#### Aggiornamento di Alloy v. 0.0.10 con le seguenti modifiche:

* Implementazione archiviazione client: logica di stato e cookie spostata nel server.
* Comando esposizione di EventType ed EventMergeId su evento.
* Utilizzo di sendBeacon per il rilevamento di collegamenti diversi dagli exit link.
* Sincronizzazioni ID senza il controllo della scadenza.
* Il comando setCustomerIds non esegue l&#39;hashing degli ID su pagine non SSL (http).
* Il dominio APEX passa al server per essere utilizzato durante l&#39;impostazione dello stato/dei cookie.
* Prelievo ECID dalla risposta attraverso un nuovo tipo di handle.
* Valori predefiniti per le configurazioni Attivazione e Identità rimossi.
* Opzioni query rinominate e spostate in meta.
* Migrazione ECID legacy.

#### Correzioni di bug

* In caso di codice di stato imprevisto, il contenuto della risposta viene analizzato e formattato per il messaggio di errore.
* La configurazione sovrascrive l&#39;esecuzione comando di debug o l&#39;utilizzo di alloy_debug.

## 25 novembre 2019

### Adobe Experience Platform Web SDK 0.0.3

#### Funzioni

* Nuovi campi ID unione e Tipo nell’azione Invia evento. L&#39;ID unione è associato a `xdm.eventMergeID` nello schema XDM e il Tipo è associato a `xdm.eventType` nello schema XDM.
* Generazione rapporti e gestione degli errori migliorati.
* Ora utilizza `sendBeacon` per tutti i collegamenti.

#### Correzioni di bug

* È stato risolto un problema che impediva l’attivazione del debugging attraverso un parametro della stringa di query o la persistenza del comando `debug` nella sessione.

## 18 novembre 2019

### Adobe Experience Platform Web SDK 0.0.2

#### Funzioni

* Estensione intrappolata nell&#39;esistenza.
* Supporto ECID senza librerie o chiamate di rete aggiuntive.
* Supporto per consenso.
* Supporto per l&#39;invio di XDM alla piattaforma
* Supporto del dominio di prime parti.
* Contenuto del browser raccolto automaticamente.
* Sorgente completamente aperta ([estensione](https://github.com/adobe/reactor-extension-alloy), [SDK](https://github.com/adobe/reactor-extension-alloy)).
* Registrazione dettagliata.
* Possibilità di nascondere gli errori durante la produzione.
