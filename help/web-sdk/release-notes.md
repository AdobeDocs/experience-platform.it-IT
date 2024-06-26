---
title: Note sulla versione di Adobe Experience Platform Web SDK
description: Note aggiornate sulla versione di Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;note sulla versione;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 060f6bb0ff6f57a84698a27bd9f640c0178e5b51
workflow-type: tm+mt
source-wordcount: '1811'
ht-degree: 1%

---


# Note sulla versione

Questo documento descrive le note sulla versione di Adobe Experience Platform Web SDK.
Per le ultime note sulla versione dell’estensione tag Web SDK, consulta [Note sulla versione dell’estensione tag Web SDK](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

>[!IMPORTANT]
>
>Google [ha annunciato](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout) pianifica di interrompere il supporto di Chrome per i cookie di terze parti nella seconda metà del 2024. Di conseguenza, i cookie di terze parti non saranno più supportati in nessuno dei principali browser.
>
>Quando questa modifica viene implementata, Adobe interromperà il supporto per `demdex` cookie attualmente supportato nell’SDK per web.

## Versione 2.20.0 - 21 maggio 2024

**Nuove funzioni**

* È stato aggiunto il supporto per [Raccolta di contenuti multimediali in streaming](../web-sdk/commands/configure/streamingmedia.md).

**Correzioni e miglioramenti**

* È stato corretto un bug a causa del quale il contenuto predefinito veniva nascosto dal frammento pre-hiding quando il consenso veniva negato.

## Versione 2.19.2 - 10 gennaio 2024

**Correzioni e miglioramenti**

* È stato risolto un problema a causa del quale gli errori di identità mascheravano altri errori e cambiavano gli errori di identità in avvisi.
* È stato risolto un problema a causa del quale la parte inferiore delle chiamate della pagina non veniva mai inviata quando si verificava una chiamata di livello superiore della pagina con `renderDecisions` imposta su `false`.
* È stato risolto un problema che impediva a Web SDK di leggere le identità tra domini in presenza di più `adobe_mc` parametri della stringa di query.

## Versione 2.19.1 - 10 novembre 2023

**Correzioni e miglioramenti**

* È stato risolto un problema a causa del quale l’array propositions restituiva da `sendEvent` le chiamate erano sempre vuote.

## Versione 2.19.0 - 1 novembre 2023

**Nuove funzioni**

* È stato aggiunto il supporto per il rendering dei messaggi in-app da Adobe Journey Optimizer.
* È stato aggiunto il supporto per [inizio e fine degli eventi di pagina](use-cases/top-bottom-page-events.md).
* Aggiunto [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) opzione per `sendEvent` per controllare la richiesta dell&#39;ambito a livello di pagina e della superficie predefinita.

**Correzioni e miglioramenti**

* La personalizzazione combinata mostra gli eventi insieme durante il rendering di più tipi di personalizzazione.
* È stato risolto un problema a causa del quale i nomi delle visualizzazioni delle applicazioni a pagina singola facevano distinzione tra maiuscole e minuscole.
* È stato risolto un problema relativo ai selettori di offerte personalizzati DOM ombra.

## Versione 2.18.0 - 31 luglio 2023

**Nuove funzioni**

* È stato aggiunto il supporto per [sostituzioni per comando dell’ID dello stream di dati](../datastreams/overrides.md).

**Correzioni e miglioramenti**

* È stato risolto un problema a causa del quale i collegamenti di uscita non venivano qualificati perché il dominio faceva parte della query.
* Obsoleto `edgeConfigId` a favore di `datastreamId` nella configurazione dell’SDK web.

## Versione 2.17.0 - 17 maggio 2023

**Correzioni e miglioramenti**

* L’SDK per web ora codifica i valori di destinazione dei cookie di Audience Manager, in modo simile al [Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=it).

## Versione 2.16.0 - 25 aprile 2023

**Nuove funzioni**

* È stato aggiunto il supporto per [sostituzioni della configurazione dello stream di dati](../datastreams/overrides.md).

## Versione 2.15.0 - 30 marzo 2023

**Nuove funzioni**

* È stato aggiunto il supporto per [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) link click callback.
* È stato aggiunto il supporto per il tracciamento dei clic di Adobe Journey Optimizer.

**Correzioni e miglioramenti**

* La raccolta di collegamenti ora include il nome del collegamento e l’area del visitatore.
* Errore della console rimosso per le destinazioni URL non riuscite.

## Versione 2.14.0 - 25 gennaio 2023

* (Beta) È stato aggiunto il supporto per superfici e proposte Adobe Journey Optimizer.

**Correzioni e miglioramenti**

* È stato risolto un problema relativo alle azioni del codice personalizzato del Compositore esperienza visivo di Adobe Target a causa del quale il codice veniva inserito in una posizione alternativa rispetto a con [!DNL at.js].
* È stato risolto un problema a causa del quale, in alcuni casi, l’intestazione &quot;referer&quot; non veniva impostata correttamente nelle richieste all’Edge Network.
* È stato risolto un problema a causa del quale [user agent client hint](/help/web-sdk/use-cases/client-hints.md) le proprietà potrebbero essere impostate su un tipo errato.
* È stato risolto un problema a causa del quale `placeContext.localTime` non corrisponde allo schema.

## Versione 2.13.1 - 13 ottobre 2022

* È stato risolto un problema che impediva il funzionamento della migrazione dei visitatori se window.Visitor veniva definito dopo la configurazione. Questo è un problema soprattutto quando si esegue con tag Adobe.
* È stato risolto un problema a causa del quale `device.screenWidth` e `device.screenHeight` sono state compilate come stringhe in alcuni ambienti.

## Versione 2.13.0 - 28 settembre 2022

**Nuove funzioni**

* È stato aggiunto il supporto per [Migrazione completa pagina per pagina](home.md#migrating-to-web-sdk). Il profilo Adobe Target verrà ora mantenuto quando un visitatore si sposta tra le pagine at.js e Web SDK.
* È stato aggiunto il supporto configurabile per [User-Agent Client Hints entropici elevati](/help/web-sdk/use-cases/client-hints.md).
* È stato aggiunto il supporto per [`applyResponse`](/help/web-sdk/commands/applyresponse.md) comando. Questo abilita la personalizzazione ibrida tramite [API server Edge Network](../server-api/overview.md).
* I collegamenti in modalità di controllo qualità ora funzionano su più pagine.

**Correzioni e miglioramenti**

* È stato risolto un problema a causa del quale le metriche di tracciamento dei clic di personalizzazione non venivano aggiornate quando il tracciamento dei collegamenti era disabilitato.
* Sono stati aggiornati i comandi per generare un errore di convalida quando sono specificate opzioni sconosciute.
* Il `_experience.decisioning.propositionEventType` La proprietà ora viene compilata quando si inviano automaticamente eventi di personalizzazione di visualizzazione e interazione.
* Aggiunta della convalida dello spazio dei nomi duplicato per `getIdentity` comando.
* È stata aggiunta la convalida dell’ambito di decisione duplicata per `sendEvent` comando.

## Versione 2.12.0 - 29 giugno 2022

* Modifica le richieste in Edge Network per utilizzare `cluster` suggerimento sulla posizione del cookie come parte dell’URL. In questo modo, gli utenti che cambiano posizione (ad esempio tramite una VPN o guidando con dispositivi mobili, ecc.) durante una sessione raggiungono lo stesso limite e hanno lo stesso profilo di personalizzazione.
* Stringif ha configurato le funzioni nella risposta del comando getLibraryInfo.

## Versione 2.11.0 - 13 giugno 2022

**Nuove funzioni**

* Ora puoi distribuire esperienze personalizzate in modo più accurato, condividendo gli ID visitatore tra le app mobili e i contenuti web per dispositivi mobili e tra più domini. Consulta la [documentazione dedicata](identity/id-sharing.md) per ulteriori informazioni.
* Ora puoi eseguire il rendering o l’esecuzione di un array di proposte da [!DNL Adobe Target] nelle applicazioni a pagina singola, senza incrementare le metriche di analisi. Questo riduce gli errori di reporting e aumenta l’accuratezza delle analisi. Consulta la [documentazione dedicata](personalization/rendering-personalization-content.md#applypropositions) per ulteriori informazioni.
* Sono state aggiunte ulteriori informazioni al `getLibraryInfo` comando che include i comandi disponibili e la configurazione finale per l&#39;istanza.

**Correzioni e miglioramenti**

* Sono state aggiornate le impostazioni dei cookie da utilizzare `sameSite="none"` e `secure` contrassegno attivo [!DNL HTTPS] pagine.
* È stato risolto un problema a causa del quale il contenuto personalizzato non veniva applicato correttamente quando si utilizzava il `eq` pseudo selettore.
* È stato risolto un problema a causa del quale `localTimezoneOffset` potrebbe non superare la convalida dell’Experience Platform.

## Versione 2.10.1 - 3 maggio 2022

* È stato risolto un problema che causava la creazione di più iframe persistenti per le sincronizzazioni ID e le destinazioni dei segmenti.

## Versione 2.10.0 - 22 aprile 2022

* Utilizza un iframe persistente per tutte le sincronizzazioni ID e le destinazioni dei segmenti.
* È stato risolto un problema a causa del quale le proposte di metriche unite venivano duplicate in `sendEvent` risultato.

## Versione 2.9.0 - 10 marzo 2022

* Aggiunto supporto per il tracciamento [!DNL control (default)] Esperienze Adobe Target.
* Sono stati ottimizzati gli eventi di modifica della visualizzazione per le applicazioni a pagina singola. La notifica di visualizzazione ora è inclusa nell’evento di modifica della visualizzazione quando vengono riprodotte esperienze personalizzate.
* Avviso della console rimossa se non `eventType` è presente.
* È stato risolto un problema a causa del quale `propositions` proprietà restituita solo da un `sendEvent` quando le esperienze sono state richieste o recuperate dalla cache. Il `propositions` La proprietà ora sarà sempre definita come un array.
* È stato risolto un problema che impediva la visualizzazione dei contenitori nascosti in caso di errore restituito dall’Edge Network.
* È stato risolto un problema che impediva il conteggio degli eventi di interazione in Adobe Target. Questo problema è stato risolto aggiungendo il nome della visualizzazione al file XDM in web.webPageDetails.viewName.
* Correggi i collegamenti interrotti alla documentazione nei messaggi della console.

## Versione 2.8.0 - 19 gennaio 2022

* Supporta i selettori DOM shadow per la personalizzazione.
* Tipi di eventi di personalizzazione rinominati. (`display` e `click` diventa `decisioning.propositionDisplay` e `decisioning.propositionInteract`)
* È stato risolto un problema a causa del quale le offerte HTML con tag di script in linea aggiungevano i tag di script due volte alla pagina, anche se lo script veniva eseguito una sola volta.

## Versione 2.7.0 - 26 ottobre 2021

* Espone informazioni aggiuntive dall’Edge Network nel valore restituito da `sendEvent`, tra cui `inferences` e `destinations`. Il formato di queste proprietà potrebbe cambiare in quanto queste funzioni vengono attualmente implementate come parte di una versione beta.

## Versione 2.6.4 - 7 settembre 2021

* È stato risolto un problema a causa del quale impostavano le azioni HTML Adobe Target applicabili al `head` sostituivano l&#39;intero `head` contenuto. Ora imposta le azioni HTML applicate al `head` vengono modificati in append HTML.

## Versione 2.6.3 - 16 agosto 2021

* È stato risolto un problema a causa del quale oggetti non destinati a uso pubblico venivano esposti tramite la promessa risolta da `configure` comando.

## Versione 2.6.2 - 4 agosto 2021

* È stato risolto un problema a causa del quale veniva visualizzato un avviso relativo alla rimozione di `result.decisions` (fornito da `sendEvent` ) verrebbe registrato nella console anche quando il `result.decisions` non era possibile accedere alla proprietà. Non verrà registrato alcun avviso quando si accede al `result.decisions` , ma la proprietà è ancora obsoleta.

## Versione 2.6.1 - 29 luglio 2021

* È stato risolto un problema a causa del quale il rendering della personalizzazione per una visualizzazione app a pagina singola priva di contenuto di personalizzazione generava un errore e causava la promessa restituita dal `sendEvent` da rifiutare.

## Versione 2.6.0 - 27 luglio 2021

* Fornisce ulteriori contenuti di personalizzazione nel `sendEvent` promessa risolta, inclusi i token di risposta di Adobe Target. Quando `sendEvent` viene eseguito il comando, viene restituita una promessa che viene infine risolta con un `result` oggetto contenente informazioni ricevute dal server. In precedenza, questo oggetto risultato includeva una proprietà denominata `decisions`. Questo `decisions` La proprietà è stata dichiarata obsoleta. Una nuova proprietà, `propositions`, è stato aggiunto. Questa nuova proprietà consente ai clienti di accedere a più contenuti di personalizzazione, tra cui [token di risposta](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md).

## Versione 2.5.0 - Giugno 2021

* È stato aggiunto il supporto per le offerte di personalizzazione di reindirizzamento.
* Le larghezze e le altezze dei riquadri di visualizzazione raccolti automaticamente che sono valori negativi non verranno più inviate al server.
* Quando un evento viene annullato restituendo `false` da un `onBeforeEventSend` callback, ora viene registrato un messaggio.
* È stato risolto un problema a causa del quale parti specifiche di dati XDM destinate a un singolo evento venivano incluse in più eventi.

## Versione 2.4.0 - Marzo 2021

* L’SDK può ora essere installato come [Pacchetto NPM](/help/web-sdk/install/npm.md).
* È stato aggiunto il supporto per `out` opzione quando [configurazione del consenso predefinito](/help/web-sdk/commands/configure/defaultconsent.md), che rilascia tutti gli eventi fino alla ricezione del consenso (il `pending` option accoda gli eventi e li invia dopo aver ricevuto il consenso).
* Il [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) è ora possibile utilizzare il callback per impedire l’invio di un evento.
* Ora utilizza un gruppo di campi dello schema XDM invece di `meta.personalization` durante l’invio di eventi relativi a contenuti personalizzati di cui viene eseguito il rendering o su cui si fa clic.
* Il [`getIdentity`](/help/web-sdk/commands/getidentity.md) ora restituisce l’ID dell’area edge insieme all’identità.
* Gli avvisi e gli errori ricevuti dal server sono stati migliorati e vengono gestiti in modo più appropriato.
* È stato aggiunto il supporto per lo standard Consent 2.0 di Adobe per [`setConsent`](/help/web-sdk/commands/setconsent.md) comando.
* Le preferenze di consenso, quando ricevute, vengono sottoposte a hashing e memorizzate nell’archiviazione locale per un’integrazione ottimizzata tra CMP, Platform Web SDK e Edge Network di Platform. Se raccogli le preferenze di consenso, ti invitiamo ora a chiamare `setConsent` a ogni caricamento di pagina.
* Due [hook di monitoraggio](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` e `onCommandRejected`, sono state aggiunte.
* Correzione bug: gli eventi di notifica dell’interazione di personalizzazione contenevano informazioni duplicate sulla stessa attività quando un utente passava a una nuova vista di app a pagina singola, tornava alla vista originale e faceva clic su un elemento idoneo per la conversione.
* Correzione bug: se il primo evento inviato dall’SDK aveva `documentUnloading` imposta su `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) verrebbe utilizzato per inviare l’evento, causando un errore relativo a un’identità non stabilita.

## Versione 2.3.0 - novembre 2020

* È stato aggiunto il supporto nonce per consentire criteri di sicurezza dei contenuti più severi.
* È stato aggiunto il supporto alla personalizzazione per le applicazioni a pagina singola.
* È stata migliorata la compatibilità con altri codici JavaScript su pagina che potrebbero essere in sovrascrittura `window.console` API.
* Correzione bug: `sendBeacon` non veniva utilizzato quando `documentUnloading` è stato impostato su `true` o quando i clic dei collegamenti venivano tracciati automaticamente.
* Correzione bug: se l’elemento di ancoraggio conteneva contenuto HTML, non veniva tracciato automaticamente alcun collegamento.
* Correzione bug: alcuni errori del browser contenenti un valore di sola lettura `message` proprietà non sono state gestite in modo appropriato, causando un errore diverso esposto al cliente.
* Correzione bug: l’esecuzione dell’SDK all’interno di un iframe generava un errore se la pagina HTML dell’iframe proveniva da un sottodominio diverso rispetto alla pagina HTML della finestra principale.

## Versione 2.2.0 - ottobre 2020

* Correzione bug: l&#39;oggetto Opt-in impediva a Web SDK di effettuare chiamate quando `idMigrationEnabled` è `true`.
* Correzione bug: rende Web SDK consapevole delle richieste che devono restituire offerte di personalizzazione per evitare problemi di sfarfallio.

## Versione 2.1.0 - Agosto 2020

* Rimuovi il `syncIdentity` e supportare il passaggio di tali ID nel `sendEvent` comando.
* Supporto dello standard di consenso IAB 2.0.
* È supportato il passaggio di ID aggiuntivi nella `setConsent` comando.
* Supporto per la sostituzione di `datasetId` nel `sendEvent` comando.
* Supporto degli hook di monitoraggio ([Ulteriori informazioni](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Superato `environment: browser` nei dettagli sull’implementazione, dati contestuali.
