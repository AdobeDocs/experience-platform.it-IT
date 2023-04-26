---
title: Note sulla versione dell’estensione Adobe Experience Platform Web SDK
description: Estensione tag Adobe Experience Platform Web SDK
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: ccd02ea014d514b56a8e1bd540bb2c2c4bb2eb1b
workflow-type: tm+mt
source-wordcount: '1654'
ht-degree: 38%

---


# Note sulla versione dell’estensione Adobe Experience Platform Web SDK

Questo documento illustra le note sulla versione per l&#39;estensione tag Adobe Experience Platform Web SDK. Per le ultime note sulla versione dell’SDK stesso, consulta la sezione [Note sulla versione di Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html?lang=it).

## Versione 2.17.0 - 25 aprile 2023

**Nuove funzioni**

* È stato aggiunto il supporto per le sostituzioni della configurazione del datastream.
* Aggiungi un avviso di elementi obsoleti al `datasetId` l&#39;opzione `sendEvent` comando.

**Correzioni e miglioramenti**

* È stato risolto un problema a causa del quale lo scorrimento in Safari chiudeva il selettore del datastream.

## Versione 2.16.1 - 14 aprile 2023

* È stato risolto un problema relativo agli elementi di dati Oggetto e Variabile XDM a causa del quale non era possibile selezionare uno schema da una sandbox non predefinita.

## Versione 2.16.0 - 30 marzo 2023

**Nuove funzioni**

* (Beta) Aggiunto **[!UICONTROL Aggiorna variabile]** e **[!UICONTROL Variabile]** elemento dati.
* È stata aggiunta la configurazione per [`onBeforeLinkClickSend`](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend) funzione di callback.

**Correzioni e miglioramenti**

* È stato risolto un problema a causa del quale il clic sugli elementi all’interno di un tag di ancoraggio non funzionava quando **[!UICONTROL Reindirizzamento con identità]** è stata utilizzata l&#39;azione .
* È stato risolto un problema a causa del quale gli elementi dati dell’oggetto XDM non funzionavano quando era presente un solo schema.
* Contiene la versione 2.15.0 dell’SDK Web per Adobe Experience Platform.


## Versione 2.15.1 - 26 gennaio 2023

* È stato risolto un problema che impediva agli utenti senza accesso ai datastreams di modificare la configurazione dell’estensione.
* È stato aggiunto il supporto per le superfici nel `sendEvent` azione.

Contiene la versione 2.14.0 dell’SDK Web per Adobe Experience Platform.


## Versione 2.14.1 - 13 ottobre 2022

* È stato risolto un problema a causa del quale l’SDK web non rispettava l’ID dal servizio Experience Cloud ID.

Contiene la versione 2.13.1 della libreria Adobe Experience Platform Web SDK.

## Versione 2.14.0 - 28 settembre 2022

* Aggiunto nuovo `targetMigrationEnabled` configurazione che abilita la migrazione completa della pagina.
* È stata aggiunta un’azione di risposta di applicazione per abilitare le implementazioni ibride server-client.
* È stata aggiunta l’opzione di contesto per suggerimenti client entropici elevati.

Contiene la versione 2.13.0 della libreria Adobe Experience Platform Web SDK.

## Versione 2.13.0 - 29 giugno 2022

* È stato corretto l’ordinamento delle proprietà numeriche nell’elemento dati Oggetto XDM, ad esempio eVar.

Contiene la versione 2.12.0 della libreria Adobe Experience Platform Web SDK.

## Versione 2.12.0 - 13 giugno 2022

* È stato aggiornato il `identityMap` elemento dati per popolare le opzioni dello spazio dei nomi in base alle sandbox definite dalle impostazioni dell’estensione.
* Aggiunto **[!UICONTROL Reindirizzamento con identità]** per consentire la condivisione di identità tra domini diversi.
* Sono stati aggiunti collegamenti alla documentazione per `sendEvent` azione.
* Libreria dell&#39;interfaccia utente React Spectrum aggiornata.
* Miglioramenti a più interfacce utente.

Contiene la versione 2.11.0 della libreria Adobe Experience Platform Web SDK.

## Versione 2.11.2 - 3 maggio 2022

Contiene la versione 2.10.1 della libreria Adobe Experience Platform Web SDK.

## Versione 2.11.1 - 22 aprile 2022

* È stato corretto l’errore di configurazione del comando dalla versione 2.11.0.

Contiene la versione 2.10.0 della libreria Adobe Experience Platform Web SDK.

## Versione 2.11.0 - 22 aprile 2022

* Miglioramento delle prestazioni dell’interfaccia utente dei tag.
* Aggiungi i selettori sandbox alla configurazione dell&#39;estensione datastreams.

Contiene la versione 2.10.0 della libreria Adobe Experience Platform Web SDK.

## Versione 2.10.0 - 10 marzo 2022

* Aggiorna il frammento pre-hiding disponibile per la copia nella pagina di configurazione per lavorare con l’editor VEC di Adobe Target aggiornato.

Contiene la versione 2.9.0 della libreria dell’SDK per web di Adobe Experience Platform.

## Versione 2.9.0 - 19 gennaio 2022

Contiene la versione 2.8.0 della libreria dell’SDK per web di Adobe Experience Platform.

## Versione 2.8.0 - 26 ottobre 2021

Contiene la versione 2.7.0 della libreria dell’SDK per web di Adobe Experience Platform.

* Ulteriori informazioni da Experience Edge sono disponibili nell’evento Send Event Complete , tra cui `inferences` e `destinations`. Il formato di queste proprietà può cambiare in quanto queste funzioni vengono attualmente distribuite come parte di una versione beta. Per ulteriori informazioni, consulta [Tracciamento degli eventi.](../fundamentals/tracking-events.md)

## Versione 2.7.3 - 7 settembre 2021

Contiene la versione 2.6.4 della libreria dell’SDK per web di Adobe Experience Platform.

* Non esiste più un avviso di obsolescenza per `container.buildInfo.environment.`

## Versione 2.7.0 - 16 agosto 2021

Contiene la versione 2.6.3 della libreria dell’SDK per web di Adobe Experience Platform.

* Quando si utilizza il tipo di elemento dati Identity Map, gli identificatori i cui ID vengono risolti in valori che non sono stringhe popolate vengono ora rimossi automaticamente dalla mappa di identità.
* È stato corretto un errore che si verificava durante il tentativo di salvataggio di un elemento dati utilizzando il tipo di elemento dati Oggetto XDM e non era stato selezionato alcuno schema.
* È stata migliorata la composizione tipografica dell’interfaccia utente.

## Versione 2.6.2 - 4 agosto 2021

Contiene la versione 2.6.2 della libreria dell’SDK per web di Adobe Experience Platform.

## Versione 2.6.1 - 29 luglio 2021

Contiene la versione 2.6.1 della libreria dell’SDK per web di Adobe Experience Platform.

## Versione 2.6.0 - 27 luglio 2021

Contiene la versione 2.6.0 della libreria dell’SDK per web di Adobe Experience Platform.

* Etichette, descrizioni e messaggi di errore che utilizzano il termine &quot;configurazione perimetrale&quot; sono stati modificati per utilizzare il termine &quot;datastream&quot; per allinearsi alla terminologia Adobe Experience Platform più recente.
* Nella visualizzazione di configurazione dell’estensione, è stato aggiunto il supporto per la gestione di un numero elevato di flussi di dati e ambienti di datastream.
* Nella visualizzazione degli elementi dati di oggetti XDM, è stato aggiunto il supporto per la gestione di un numero elevato di schemi.
* È stato aggiunto un tipo di evento Send Event Complete , che può essere utilizzato per eseguire una regola dopo che un evento è stato inviato al server e una risposta ricevuta. A breve sarà disponibile ulteriore documentazione.
* Il tipo di evento Decisioni ricevute è stato dichiarato obsoleto. Utilizzare invece il tipo di evento Send Event Complete.
* L’interfaccia utente e la gestione degli errori sono stati generalmente migliorati.

## Versione 2.5.0 - 1 giugno 2021

Contiene la versione 2.5.0 della libreria dell’SDK per web di Adobe Experience Platform.

* Aggiunta di un `data` all&#39;azione Invia evento. La prossima documentazione descriverà come può essere utilizzato in alcuni scenari.
* Nella visualizzazione dell’elemento dati oggetto XDM è stato risolto un problema che causava la generazione di un errore se l’utente aveva accesso alle sandbox Adobe Experience Platform ma non alla sandbox configurata come predefinita per l’organizzazione.
* Nella visualizzazione dell’elemento dati oggetto XDM è stato risolto un problema a causa del quale un campo di schema obbligatorio veniva considerato non valido anche se l’oggetto principale non conteneva valori.

## Versione 2.4.0 - 9 marzo 2021

Contiene la versione 2.4.0 della libreria dell’SDK per web di Adobe Experience Platform.

* Aggiunto [&quot;scarico documento&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) casella di controllo Invia interfaccia utente azione evento.
* È stato aggiunto il supporto per un `out` opzione quando [configurazione del consenso predefinito](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) che rilascia tutti gli eventi fino alla ricezione del consenso (l&#39;esistente `pending` mette in coda gli eventi e li invia una volta ricevuto il consenso).
* È stata aggiunta una descrizione al campo consenso predefinito.
* È stato aggiunto il supporto per [Standard Adobe Consent 2.0](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Un errore migliore ora viene visualizzato nell’interfaccia utente dell’elemento dati oggetto XDM se il token di accesso dell’utente non è valido o se il provisioning del token di accesso è errato.
* È stato corretto un errore di origine incrociata (che non influisce sul funzionamento dell’estensione) che veniva visualizzato nella console per sviluppatori del browser quando si visualizzava un elemento dati di oggetti XDM.

## Versione 2.3.0 - 4 novembre 2020

Contiene la versione 2.3.0 della libreria dell’SDK per web di Adobe Experience Platform.

* È stato aggiunto il supporto per l’utilizzo di un elemento dati durante la configurazione del consenso predefinito.
* È stata aggiunta la possibilità di cercare schemi XDM con il tipo elemento dati di oggetti XDM.
* È stata aggiunta la duplicazione di dati XDM all’interno del tipo di azione Invia evento per garantire che eventuali modifiche successive all’oggetto dati XDM non vengano riportate nella richiesta.

## Versione 2.2.0 - 1 ottobre 2020

* Quando si tentava di creare un oggetto XDM da schemi sandbox, si verificavano problemi di autenticazione. L’API che chiama Platform ora conosce gli ambienti e agli utenti vengono presentati solo gli schemi che possono modificare.
* Quando utilizzi `identityMap` data element, i namespace ora sono precompilati in un menu a discesa, quindi non è necessario compilarli manualmente.
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
* È supportata la scelta di una sandbox di Platform nell’elemento dati oggetto XDM.

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

* Aggiungi la configurazione Activity Tracker all&#39;estensione tag
* Comando esposizione di EventType ed EventMergeId su evento
* Aggiungi la configurazione onBeforeEventSend all&#39;estensione tag
* Aggiungi la configurazione edgeBasePath all’estensione tag

## Versione 0.0.3 - 25 novembre 2019

* Nuovi campi ID unione e Tipo nell’azione Invia evento. L&#39;ID unione è associato a `xdm.eventMergeID` nello schema XDM e il Tipo è associato a `xdm.eventType` nello schema XDM.

## Versione 0.0.2 - 18 novembre 2019

* Versione iniziale
