---
title: Note sulla versione dell’estensione Adobe Experience Platform Web SDK
description: Estensione tag Adobe Experience Platform Web SDK
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 8cec606849489ef1e8845254117d184d5dc3c70a
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 36%

---


# Note sulla versione dell’estensione Adobe Experience Platform Web SDK

Questo documento descrive le note sulla versione dell’estensione tag Adobe Experience Platform Web SDK. Per le ultime note sulla versione dell’SDK, consulta [Note sulla versione di Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html?lang=it).

## Versione 2.21.3 - 10 novembre 2023

Contiene la versione 2.19.1 di Adobe Experience Platform Web SDK.

**Correzioni e miglioramenti**

* È stato risolto un problema a causa del quale l’array propositions era disponibile in `Send event complete` Gli eventi sono sempre stati vuoti.

## Versione 2.21.2 - 1 novembre 2023

**Nuove funzioni**

* Aggiunto `Request default personalization` opzione per inviare l’azione evento.
* È stato aggiunto il supporto per gli eventi di inizio e fine pagina nell’azione invia evento.
* Aggiunto `Apply propositions` azione.
* Aggiunto `Evaluate rulesets` azione e `Subscribe ruleset items` per i messaggi in-app.
* Aggiunto `Decision context` per inviare un&#39;azione evento.

**Correzioni e miglioramenti**

* Contiene la versione 2.19.0 di Adobe Experience Platform Web SDK.

## Versione 2.20.3 - 8 agosto 2023

**Correzioni e miglioramenti**

* È stato risolto un problema che impediva il salvataggio degli elementi dati nel campo di sostituzione ID contenitore sincronizzazione ID.

## Versione 2.20.1 - 3 agosto 2023

**Correzioni e miglioramenti**

* È stata migliorata la convalida delle impostazioni di sostituzione dello stream di dati salvato.

## Versione 2.20.0 - 31 luglio 2023

**Nuove funzioni**

* È stato aggiunto il supporto per [sostituzioni per comando dell’ID dello stream di dati](../../../../datastreams/overrides.md).

**Correzioni e miglioramenti**

* Obsoleto `edgeConfigId` a favore di `datastreamId` nella configurazione dell’SDK.
* Diversi miglioramenti all’esperienza utente per la configurazione dello stream di dati sostituiscono l’interfaccia utente di.

## Versione 2.19.0 - 21 giugno 2023

* Il **[!UICONTROL Variabile]** data element e **[!UICONTROL Aggiorna variabile]** Le azioni sono ora generalmente disponibili.

## Versione 2.18.0 - 18 maggio 2023

* Contiene la versione 2.17.0 di Adobe Experience Platform Web SDK.

## Versione 2.17.0 - 25 aprile 2023

**Nuove funzioni**

* Contiene la versione 2.16.0 di Adobe Experience Platform Web SDK.
* È stato aggiunto il supporto per [sostituzioni della configurazione dello stream di dati](../../../../datastreams/overrides.md).
* Aggiungi avviso di deprecazione al `datasetId` opzione sul `sendEvent` comando.


**Correzioni e miglioramenti**

* È stato risolto un problema a causa del quale lo scorrimento in Safari chiudeva il selettore dello stream di dati.

## Versione 2.16.1 - 14 aprile 2023

* È stato risolto un problema relativo agli elementi dati Variable e Oggetto XDM a causa del quale non era possibile selezionare uno schema da una sandbox non predefinita.

## Versione 2.16.0 - 30 marzo 2023

**Nuove funzioni**

* (Beta) aggiunto **[!UICONTROL Aggiorna variabile]** azione e **[!UICONTROL Variabile]** elemento dati.
* È stata aggiunta la configurazione per [`onBeforeLinkClickSend`](../../../../edge/fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend) callback.

**Correzioni e miglioramenti**

* È stato risolto un problema che impediva il funzionamento del clic sugli elementi all’interno di un tag di ancoraggio quando il **[!UICONTROL Reindirizza con identità]** è stata utilizzata l&#39;azione.
* È stato risolto un problema che impediva il funzionamento degli elementi dati dell’oggetto XDM in presenza di un solo schema.
* Contiene la versione 2.15.0 di Adobe Experience Platform Web SDK.


## Versione 2.15.1 - 26 gennaio 2023

* È stato risolto un problema che impediva agli utenti senza accesso ai flussi di dati di modificare la configurazione dell’estensione.
* È stato aggiunto il supporto per le superfici in `sendEvent` azione.

Contiene la versione 2.14.0 di Adobe Experience Platform Web SDK.


## Versione 2.14.1 - 13 ottobre 2022

* È stato risolto un problema a causa del quale l’SDK per web non rispettava l’ID del servizio ID Experience Cloud.

Contiene la versione 2.13.1 della libreria Adobe Experience Platform Web SDK.

## Versione 2.14.0 - 28 settembre 2022

* Aggiunto nuovo `targetMigrationEnabled` che abilita la migrazione completa pagina per pagina.
* È stata aggiunta un’azione di risposta di applicazione per abilitare le implementazioni ibride server-client.
* È stata aggiunta l’opzione di contesto User-Agent Client Hints ad alta entropia.

Contiene la versione 2.13.0 della libreria Adobe Experience Platform Web SDK.

## Versione 2.13.0 - 29 giugno 2022

* È stato corretto l’ordinamento delle proprietà numeriche nell’elemento dati dell’oggetto XDM, ad esempio le eVar.

Contiene la versione 2.12.0 della libreria Adobe Experience Platform Web SDK.

## Versione 2.12.0 - 13 giugno 2022

* È stato aggiornato il `identityMap` elemento dati per popolare le opzioni namespace in base alle sandbox definite dalle impostazioni di estensione.
* Aggiunto **[!UICONTROL Reindirizza con identità]** per consentire la condivisione di identità tra domini diversi.
* Sono stati aggiunti collegamenti alla documentazione di `sendEvent` azione.
* È stata aggiornata la libreria dell’interfaccia utente di React Spectrum.
* Sono stati apportati diversi miglioramenti all’interfaccia utente.

Contiene la versione 2.11.0 della libreria Adobe Experience Platform Web SDK.

## Versione 2.11.2 - 3 maggio 2022

Contiene la versione 2.10.1 della libreria Adobe Experience Platform Web SDK.

## Versione 2.11.1 - 22 aprile 2022

* È stato corretto l’errore del comando di configurazione dalla versione 2.11.0.

Contiene la versione 2.10.0 della libreria Adobe Experience Platform Web SDK.

## Versione 2.11.0 - 22 aprile 2022

* Sono state migliorate le prestazioni dell’interfaccia utente Tag.
* Aggiungi selettori sandbox alla configurazione dell’estensione per gli stream di dati.

Contiene la versione 2.10.0 della libreria Adobe Experience Platform Web SDK.

## Versione 2.10.0 - 10 marzo 2022

* Aggiorna il frammento pre-hiding disponibile per la copia nella pagina di configurazione in modo che funzioni con l’editor del Compositore esperienza visivo di Adobe Target aggiornato.

Contiene la versione 2.9.0 della libreria dell’SDK per web di Adobe Experience Platform.

## Versione 2.9.0 - 19 gennaio 2022

Contiene la versione 2.8.0 della libreria dell’SDK per web di Adobe Experience Platform.

## Versione 2.8.0 - 26 ottobre 2021

Contiene la versione 2.7.0 della libreria dell’SDK per web di Adobe Experience Platform.

* Ulteriori informazioni da Edge Network sono disponibili nell’evento Send Event Complete, tra cui `inferences` e `destinations`. Il formato di queste proprietà potrebbe cambiare in quanto queste funzioni vengono attualmente implementate come parte di una versione beta. Per ulteriori informazioni, consulta [Tracciamento degli eventi.](../../../../edge/fundamentals/tracking-events.md)

## Versione 2.7.3 - 7 settembre 2021

Contiene la versione 2.6.4 della libreria dell’SDK per web di Adobe Experience Platform.

* Non viene più visualizzato un avviso di elementi obsoleti per `container.buildInfo.environment.`

## Versione 2.7.0 - 16 agosto 2021

Contiene la versione 2.6.3 della libreria dell’SDK per web di Adobe Experience Platform.

* Quando si utilizza il tipo di elemento dati Identity Map, gli identificatori i cui ID vengono risolti in valori che non sono stringhe popolate vengono ora rimossi automaticamente dalla mappa di identità.
* È stato corretto un errore che si verificava durante il tentativo di salvare un elemento dati utilizzando il tipo di elemento dati Oggetto XDM e non era selezionato alcuno schema.
* È stata migliorata la composizione tipografica dell’interfaccia utente.

## Versione 2.6.2 - 4 agosto 2021

Contiene la versione 2.6.2 della libreria dell’SDK per web di Adobe Experience Platform.

## Versione 2.6.1 - 29 luglio 2021

Contiene la versione 2.6.1 della libreria dell’SDK per web di Adobe Experience Platform.

## Versione 2.6.0 - 27 luglio 2021

Contiene la versione 2.6.0 della libreria dell’SDK per web di Adobe Experience Platform.

* Le etichette, le descrizioni e i messaggi di errore che utilizzano il termine &quot;configurazione Edge&quot; sono stati modificati per utilizzare il termine &quot;flusso di dati&quot; in linea con la terminologia più recente di Adobe Experience Platform.
* Nella vista di configurazione dell’estensione è stato aggiunto il supporto per la gestione di un numero elevato di flussi di dati e ambienti di flussi di dati.
* Nella visualizzazione dell’elemento dati Oggetto XDM, è stato aggiunto il supporto per la gestione di un numero elevato di schemi.
* È stato aggiunto un tipo di evento Invia evento completato, che può essere utilizzato per eseguire una regola dopo che un evento è stato inviato al server e una risposta ricevuta. La documentazione aggiuntiva sarà presto disponibile.
* Il tipo di evento Decisioni ricevute è stato dichiarato obsoleto. Utilizza invece il tipo di evento Invia evento completato.
* L’interfaccia utente e la gestione degli errori sono state generalmente migliorate.

## Versione 2.5.0 - 1 giugno 2021

Contiene la versione 2.5.0 della libreria dell’SDK per web di Adobe Experience Platform.

* È stato aggiunto un `data` all&#39;azione Invia evento. La prossima documentazione descriverà come questo può essere utilizzato in alcuni scenari.
* Nella vista dell’elemento dati Oggetto XDM è stato risolto un problema che causava la generazione di un errore se l’utente aveva accesso alle sandbox di Adobe Experience Platform ma non a quelle configurate come predefinite per l’organizzazione.
* Nella visualizzazione dell’elemento dati Oggetto XDM è stato risolto un problema a causa del quale un campo schema richiesto veniva considerato non valido anche se l’oggetto principale non conteneva valori.

## Versione 2.4.0 - 9 marzo 2021

Contiene la versione 2.4.0 della libreria dell’SDK per web di Adobe Experience Platform.

* Aggiunto [&quot;scaricamento documento&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html#using-the-sendbeacon-api) Casella di controllo per inviare l’interfaccia utente dell’azione Evento.
* È stato aggiunto il supporto per `out` opzione quando [configurazione del consenso predefinito](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) che rilascia tutti gli eventi fino alla ricezione del consenso (il `pending` option accoda gli eventi e li invia dopo aver ricevuto il consenso).
* È stata aggiunta una descrizione comando al campo del consenso predefinito.
* È stato aggiunto il supporto per [Consenso Adobe 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Ora viene visualizzato un errore migliore nell’interfaccia utente dell’elemento dati di oggetti XDM se il token di accesso dell’utente non è valido o se il provisioning del token di accesso non è corretto.
* È stato corretto un errore tra origini diverse (che non influisce sul funzionamento dell’estensione) visualizzato nella console di sviluppo del browser durante la visualizzazione di un elemento dati Oggetto XDM.

## Versione 2.3.0 - 4 novembre 2020

Contiene la versione 2.3.0 della libreria dell’SDK per web di Adobe Experience Platform.

* È stato aggiunto il supporto per l’utilizzo di un elemento dati durante la configurazione del consenso predefinito.
* È stata aggiunta la possibilità di cercare schemi XDM con il tipo elemento dati di oggetti XDM.
* È stata aggiunta la duplicazione di dati XDM all’interno del tipo di azione Invia evento per garantire che eventuali modifiche successive all’oggetto dati XDM non vengano riportate nella richiesta.

## Versione 2.2.0 - 1 ottobre 2020

* Quando si tentava di creare un oggetto XDM da schemi sandbox, si verificavano problemi di autenticazione. L’API che chiama Platform ora riconosce gli ambienti e agli utenti vengono presentati solo gli schemi che possono modificare.
* Quando si utilizza `identityMap` data element, gli spazi dei nomi sono ora precompilati in un menu a discesa e non è più necessario compilarli manualmente.
* È stata rivista l’interfaccia utente per l’elemento dati `xdmObject`. Nella nuova interfaccia è possibile vedere quali campi sono stati compilati, senza dover accedere a ciascun elemento nell’oggetto.

## Versione 2.1.1 - 26 agosto 2020

* È stato risolto un problema che impediva la corretta visualizzazione delle sandbox di Adobe Experience Platform nella vista Oggetto XDM. Con questa versione dell’estensione, se non viene elencata una sandbox prevista, l’utente deve rivolgersi al proprio amministratore di Adobe Experience Platform per verificare che le autorizzazioni di accesso siano impostate correttamente.

## Versione 2.1.0 - 5 agosto 2020

* Modifica necessaria: rimuovi l’azione `syncIdentity` e includi al suo posto il passaggio di tali ID nell’azione `sendEvent`. Prima di aggiornare l’estensione, disattiva eventuali regole esistenti che utilizzano l’azione rimossa.
* Aggiornamento ad Alloy v2.1.0 ([Note sulla versione](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html?lang=it)).
* È supportato lo standard del consenso IAB 2.0 nell’azione `setConsent`.
* È supportata la possibilità di ignorare l’ID del set di dati nell’azione `sendEvent`.
* È stato aggiunto un nuovo elemento dati di tipo `IdentityMap` che può essere utilizzato per compilare la voce `identityMap` nell’elemento dati di oggetti XDM che è ora abilitato e nell’azione `setConsent`.
* È supportato il passaggio di una mappa di identità nell’azione `setConsent`.
* È supportata la scelta di una sandbox di Platform nell’elemento dati di oggetti XDM.

## Versione 1.0.0 - 26 maggio 2020

* È supportata la selezione dell’ambiente dal servizio di configurazione.

## Versione 0.1.2 - 4 maggio 2020

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
* Abilitazione del debug tramite `_satellite` ora abilita il debug in Adobe Experience Platform Web SDK.
* È stato aggiunto il supporto per i valori digitati nell’oggetto XDM: booleani, numeri e decimali.

## Versione 0.0.10 - 16 marzo 2020

* I concetti di Opt-in e Opt-out sono stati combinati in `Consent` ed è stato aggiunto un nuovo comando `setConsent`.
* È stato aggiunto un nuovo elemento dati di tipo `XDM Object` che consente la mappatura da JavaScript/JSON a XDM.

## Versione 0.0.7 - 18 febbraio 2020

* Le opzioni idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled e cookieDestinationsEnabled sono state rimosse.
* È stato aggiunto il supporto per i trattini nel valore dell&#39;opzione edgeDomain.
* La richiesta effettuata durante la migrazione degli ID viene inviata all&#39;endpoint demdex per migliorare l&#39;identificazione tra domini se il cookie demdex non è impostato.
* La richiesta effettuata durante la migrazione degli ID prevede sempre una risposta per assicurarsi che venga impostato il cookie di identità.
* Quando si esegue un comando non valido, nella console verrà registrato un elenco di nomi di comando validi.
* È stata aggiunta una casella di controllo per attivare o disattivare il supporto dei cookie di terze parti per l’estensione tag. Questa funzione disattiva le chiamate a demdex.net.

## Versione 0.0.5 - 20 dicembre 2019

* Aggiunta della configurazione Activity Tracker all’estensione tag
* Comando esposizione di EventType ed EventMergeId su evento
* Aggiunta della configurazione onBeforeEventSend all&#39;estensione tag
* Aggiunta della configurazione edgeBasePath all’estensione tag

## Versione 0.0.3 - 25 novembre 2019

* Nuovi campi ID unione e Tipo nell’azione Invia evento. L&#39;ID unione è associato a `xdm.eventMergeID` nello schema XDM e il Tipo è associato a `xdm.eventType` nello schema XDM.

## Versione 0.0.2 - 18 novembre 2019

* Versione iniziale
