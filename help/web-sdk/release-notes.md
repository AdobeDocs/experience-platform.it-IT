---
title: Note sulla versione di Adobe Experience Platform Web SDK
description: Note sulla versione più recente di Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;note sulla versione;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 3dacc991fd7760c1c358bec07aca83ffeb4f4f4d
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 5%

---


# Note sulla versione

Questo documento descrive le note sulla versione di Adobe Experience Platform Web SDK.
Per le ultime note sulla versione dell&#39;estensione tag Web SDK, consulta le [note sulla versione dell&#39;estensione tag Web SDK](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## Versione 2.24.0 - venerdì 31 ottobre 2024

**Nuove funzioni**

- [Le sostituzioni dello stream di dati](../datastreams/overrides.md) sono ora supportate all&#39;avvio di sessioni multimediali.

- È stato aggiunto il supporto per i token di risposta di Adobe Target nell&#39;hook di monitoraggio [`onContentRendering`](monitoring-hooks.md#onContentRendering).

**Correzioni e miglioramenti**

- Quando vengono restituiti più messaggi in-app, viene visualizzato solo quello con la priorità più elevata. Gli altri vengono registrati come soppressi.
- Le sostituzioni dello stream di dati vuote non vengono più inviate all’Edge Network, riducendo i potenziali conflitti con le configurazioni di routing lato server.
- I seguenti nomi dei componenti dei messaggi di log sono stati rinominati, in allineamento con altri SDK di Adobe:
   - `DecisioningEngine` è stato rinominato in `RulesEngine`
   - `LegacyMediaAnalytics` è stato rinominato in `MediaAnalyticsBridge`
   - `Privacy` è stato rinominato in `Consent`
- È stato corretto un errore che si verificava durante il rendering degli elementi di contenuto predefiniti tramite [`applyPropositions`](../web-sdk/commands/applypropositions.md).
- È stato corretto un errore CSS nelle azioni di spostamento e ridimensionamento di Adobe Target.
- La chiave `machineLearning` è stata rimossa dalle risposte [`sendEvent`](../web-sdk/commands/sendevent/overview.md).

## Versione 2.23.0 - 19 settembre 2024

**Nuove funzioni**

- È stato aggiunto il supporto per la richiesta dell&#39;[ID CORE](identity/overview.md#tracking-coreid-web-sdk) nel comando [getIdentity](commands/getidentity.md#get-identity-using-the-web-sdk-javascript-library).

**Correzioni e miglioramenti**

- È stato risolto un problema a causa del quale i cookie non venivano scritti correttamente durante l’esecuzione locale dell’SDK web.

## Versione 2.22.0 - 22 agosto 2024

**Nuove funzioni**

- È stato aggiunto il supporto per gli hook di monitoraggio della personalizzazione.

**Correzioni e miglioramenti**

- È stato rimosso il supporto per Internet Explorer, riducendo la dimensione gzip della libreria del 9%.
- È stato risolto un problema che impediva l&#39;inizializzazione dei dettagli del collegamento Activity Map quando veniva chiamato l&#39;hook di monitoraggio `onInstanceConfigured`.
- È stato risolto un problema a causa del quale le destinazioni dei cookie non venivano impostate sul percorso corretto.
- È stato risolto un problema del cliente relativo alla chiamata a ha.
- È stato risolto un problema che causava il mancato funzionamento di [sendEvent](commands/sendevent/overview.md) chiamate a causa di una codifica URL non valida nel parametro `adobe_mc`.

## Versione 2.21.1 - venerdì 18 luglio 2024

**Correzioni e miglioramenti**

- È stato corretto un errore di compilazione che si verificava con l’utilizzo della libreria NPM.

## Versione 2.21.0 - mercoledì 16 luglio 2024

**Nuove funzioni**

- È stato aggiunto il supporto per il tracciamento automatico delle interazioni delle proposte.
- È stato aggiunto uno script di build personalizzato che fornisce un file alloy.js.
- È stata migliorata la raccolta di clic con il supporto di ActivityMap e del raggruppamento di eventi.

## Versione 2.20.0, mercoledì 21 maggio 2024

**Nuove funzioni**

- Aggiunta del supporto per [Streaming Media Collection](../web-sdk/commands/configure/streamingmedia.md).

**Correzioni e miglioramenti**

- È stato corretto un bug a causa del quale il contenuto predefinito veniva nascosto dal frammento pre-hiding quando il consenso veniva negato.

## Versione 2.19.2 - giovedì 10 gennaio 2024

**Correzioni e miglioramenti**

- È stato risolto un problema a causa del quale gli errori di identità mascheravano altri errori e cambiavano gli errori di identità in avvisi.
- È stato risolto un problema che impediva l&#39;invio della parte inferiore delle chiamate della pagina in caso di una chiamata di inizio pagina con `renderDecisions` impostato su `false`.
- È stato risolto un problema che impediva a Web SDK di leggere le identità tra domini in presenza di più parametri della stringa di query `adobe_mc`.

## Versione 2.19.1 - sabato 10 novembre 2023

**Correzioni e miglioramenti**

- È stato risolto un problema a causa del quale l&#39;array propositions restituito da `sendEvent` chiamate era sempre vuoto.

## Versione 2.19.0 - giovedì 1 novembre 2023

**Nuove funzioni**

- È stato aggiunto il supporto per il rendering dei messaggi in-app da Adobe Journey Optimizer.
- È stato aggiunto il supporto per [eventi di inizio e fine pagina](use-cases/top-bottom-page-events.md).
- È stata aggiunta l&#39;opzione [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) al comando `sendEvent` per controllare la richiesta dell&#39;ambito a livello di pagina e della superficie predefinita.

**Correzioni e miglioramenti**

- La personalizzazione combinata mostra gli eventi insieme durante il rendering di più tipi di personalizzazione.
- È stato risolto un problema a causa del quale i nomi delle visualizzazioni delle applicazioni a pagina singola facevano distinzione tra maiuscole e minuscole.
- È stato risolto un problema relativo ai selettori di offerte personalizzati DOM ombra.

## Versione 2.18.0 - martedì 31 luglio 2023

**Nuove funzioni**

- Aggiunta del supporto per [sostituzioni per comando dell&#39;ID dello stream di dati](../datastreams/overrides.md).

**Correzioni e miglioramenti**

- È stato risolto un problema a causa del quale i collegamenti di uscita non venivano qualificati perché il dominio faceva parte della query.
- `edgeConfigId` è stato dichiarato obsoleto a favore di `datastreamId` nella configurazione dell&#39;SDK Web.

## Versione 2.17.0, giovedì 17 maggio 2023

**Correzioni e miglioramenti**

- L&#39;SDK Web ora codifica i valori di destinazione dei cookie di Audience Manager, in modo simile alla [Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=it).

## Versione 2.16.0 - 25 aprile 2023

**Nuove funzioni**

- È stato aggiunto il supporto per [sostituzioni della configurazione dello stream di dati](../datastreams/overrides.md).

## Versione 2.15.0 - 30 marzo 2023

**Nuove funzioni**

- È stato aggiunto il supporto per il callback di clic sul collegamento [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md).
- È stato aggiunto il supporto per il tracciamento dei clic di Adobe Journey Optimizer.

**Correzioni e miglioramenti**

- La raccolta di collegamenti ora include il nome del collegamento e l’area del visitatore.
- Errore della console rimosso per le destinazioni URL non riuscite.

## Versione 2.14.0 - giovedì 25 gennaio 2023

- (Beta) È stato aggiunto il supporto per le superfici e le proposte Adobe Journey Optimizer.

**Correzioni e miglioramenti**

- È stato risolto un problema relativo alle azioni del codice personalizzato del Compositore esperienza visivo di Adobe Target a causa del quale il codice veniva inserito in una posizione alternativa rispetto a [!DNL at.js].
- È stato risolto un problema a causa del quale, in alcuni casi, l’intestazione &quot;referer&quot; non veniva impostata correttamente nelle richieste all’Edge Network.
- È stato risolto un problema a causa del quale [le proprietà dell&#39;hint client dell&#39;agente utente](/help/web-sdk/use-cases/client-hints.md) potevano essere impostate su un tipo errato.
- È stato risolto un problema a causa del quale `placeContext.localTime` non corrispondeva allo schema.

## Versione 2.13.1 - venerdì 13 ottobre 2022

- È stato risolto un problema che impediva il funzionamento della migrazione dei visitatori se window.Visitor veniva definito dopo la configurazione. Questo è un problema soprattutto quando si esegue con Adobe Tags.
- È stato risolto un problema a causa del quale `device.screenWidth` e `device.screenHeight` venivano popolati come stringhe in alcuni ambienti.

## Versione 2.13.0 - 28 settembre 2022

**Nuove funzioni**

- È stato aggiunto il supporto per [Pagina per Pagina Migrazione completa](home.md#migrating-to-web-sdk). Il profilo Adobe Target verrà ora mantenuto quando un visitatore si sposta tra le pagine at.js e Web SDK.
- È stato aggiunto il supporto configurabile per [User-Agent Client Hints entropici elevati](/help/web-sdk/use-cases/client-hints.md).
- Aggiunta del supporto per il comando [`applyResponse`](/help/web-sdk/commands/applyresponse.md). Consente la personalizzazione ibrida tramite [Edge Network Server API](../server-api/overview.md).
- I collegamenti in modalità di controllo qualità ora funzionano su più pagine.

**Correzioni e miglioramenti**

- È stato risolto un problema a causa del quale le metriche di tracciamento dei clic di personalizzazione non venivano aggiornate quando il tracciamento dei collegamenti era disabilitato.
- Sono stati aggiornati i comandi per generare un errore di convalida quando sono specificate opzioni sconosciute.
- La proprietà `_experience.decisioning.propositionEventType` viene ora compilata quando si inviano automaticamente eventi di personalizzazione di visualizzazione e interazione.
- Aggiunta convalida spazio dei nomi duplicato per il comando `getIdentity`.
- Aggiunta della convalida dell&#39;ambito di decisione duplicata per il comando `sendEvent`.

## Versione 2.12.0 - giovedì 29 giugno 2022

- Modificare le richieste nell&#39;Edge Network per utilizzare l&#39;hint di posizione del cookie `cluster` come parte dell&#39;URL. In questo modo, gli utenti che cambiano posizione (ad esempio tramite una VPN o guidando con dispositivi mobili, ecc.) durante una sessione raggiungono lo stesso limite e hanno lo stesso profilo di personalizzazione.
- Stringif ha configurato le funzioni nella risposta del comando getLibraryInfo.

## Versione 2.11.0 - martedì 13 giugno 2022

**Nuove funzioni**

- Ora puoi distribuire esperienze personalizzate in modo più accurato, condividendo gli ID visitatore tra le app mobili e i contenuti web per dispositivi mobili e tra più domini. Per ulteriori informazioni, consulta la [documentazione dedicata](identity/id-sharing.md).
- È ora possibile eseguire il rendering o l&#39;esecuzione di un array di proposte da [!DNL Adobe Target] in applicazioni a pagina singola, senza incrementare le metriche di analisi. Questo riduce gli errori di reporting e aumenta l’accuratezza delle analisi. Per ulteriori informazioni, consulta la [documentazione dedicata](personalization/rendering-personalization-content.md#applypropositions).
- Sono state aggiunte ulteriori informazioni al comando `getLibraryInfo`, inclusi i comandi disponibili e la configurazione finale per l&#39;istanza.

**Correzioni e miglioramenti**

- Sono state aggiornate le impostazioni dei cookie per utilizzare i flag `sameSite="none"` e `secure` nelle pagine [!DNL HTTPS].
- È stato risolto un problema a causa del quale il contenuto personalizzato non veniva applicato correttamente quando si utilizzava lo pseudo selettore `eq`.
- È stato risolto un problema che impediva a `localTimezoneOffset` di superare la convalida dell&#39;Experience Platform.

## Versione 2.10.1, mercoledì 3 maggio 2022

- È stato risolto un problema che causava la creazione di più iframe persistenti per le sincronizzazioni ID e le destinazioni dei segmenti.

## Versione 2.10.0 - 22 aprile 2022

- Utilizza un iframe persistente per tutte le sincronizzazioni ID e le destinazioni dei segmenti.
- È stato risolto un problema a causa del quale le proposte di metriche unite venivano duplicate nel risultato `sendEvent`.

## Versione 2.9.0 - 10 marzo 2022

- È stato aggiunto il supporto per il tracciamento di [!DNL control (default)] esperienze Adobe Target.
- Sono stati ottimizzati gli eventi di modifica della visualizzazione per le applicazioni a pagina singola. La notifica di visualizzazione ora è inclusa nell’evento di modifica della visualizzazione quando vengono riprodotte esperienze personalizzate.
- Avviso della console rimossa quando non è presente `eventType`.
- È stato risolto un problema a causa del quale la proprietà `propositions` veniva restituita solo da un comando `sendEvent` quando le esperienze venivano richieste o recuperate dalla cache. La proprietà `propositions` verrà sempre definita come un array.
- È stato risolto un problema che impediva la visualizzazione dei contenitori nascosti in caso di errore restituito dall’Edge Network.
- È stato risolto un problema che impediva il conteggio degli eventi di interazione in Adobe Target. Questo problema è stato risolto aggiungendo il nome della visualizzazione al file XDM in web.webPageDetails.viewName.
- Correggi i collegamenti interrotti alla documentazione nei messaggi della console.

## Versione 2.8.0 - giovedì 19 gennaio 2022

- Supporta i selettori DOM shadow per la personalizzazione.
- Tipi di eventi di personalizzazione rinominati. (`display` e `click` diventano `decisioning.propositionDisplay` e `decisioning.propositionInteract`)
- È stato risolto un problema a causa del quale le offerte HTML con tag di script in linea aggiungevano i tag di script due volte alla pagina, anche se lo script veniva eseguito una sola volta.

## Versione 2.7.0 - mercoledì 26 ottobre 2021

- Esporre informazioni aggiuntive dall&#39;Edge Network nel valore restituito da `sendEvent`, inclusi `inferences` e `destinations`. Il formato di queste proprietà potrebbe cambiare in quanto queste funzioni vengono attualmente implementate come parte di un Beta.

## Versione 2.6.4 - 7 settembre 2021

- È stato risolto un problema a causa del quale le azioni set HTML Adobe Target applicate all&#39;elemento `head` sostituivano l&#39;intero contenuto `head`. Ora le azioni set HTML applicate all&#39;elemento `head` vengono modificate in append HTML.

## Versione 2.6.3 - 16 agosto 2021

- È stato risolto un problema a causa del quale oggetti non destinati all&#39;uso pubblico venivano esposti tramite la promessa risolta dal comando `configure`.

## Versione 2.6.2 - 4 agosto 2021

- È stato risolto un problema che causava la registrazione di un avviso relativo alla rimozione di `result.decisions` (fornito dal comando `sendEvent`) nella console anche quando non si accedeva alla proprietà `result.decisions`. Durante l&#39;accesso alla proprietà `result.decisions` non verrà registrato alcun avviso, ma la proprietà è ancora obsoleta.

## Versione 2.6.1 - venerdì 29 luglio 2021

- È stato risolto un problema che causava un errore durante il rendering della personalizzazione per una visualizzazione app a pagina singola priva di contenuto di personalizzazione e il rifiuto della promessa restituita dal comando `sendEvent`.

## Versione 2.6.0 - mercoledì 27 luglio 2021

- Fornisce ulteriori contenuti di personalizzazione nella promessa risolta `sendEvent`, inclusi i token di risposta di Adobe Target. Quando viene eseguito il comando `sendEvent`, viene restituita una promessa che viene infine risolta con un oggetto `result` contenente le informazioni ricevute dal server. In precedenza, questo oggetto risultato includeva una proprietà denominata `decisions`. Questa proprietà `decisions` è stata dichiarata obsoleta. È stata aggiunta una nuova proprietà, `propositions`. Questa nuova proprietà consente ai clienti di accedere a più contenuti di personalizzazione, inclusi [token di risposta](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md).

## Versione 2.5.0 - Giugno 2021

- È stato aggiunto il supporto per le offerte di personalizzazione di reindirizzamento.
- Le larghezze e le altezze dei riquadri di visualizzazione raccolti automaticamente che sono valori negativi non verranno più inviate al server.
- Quando un evento viene annullato restituendo `false` da un callback `onBeforeEventSend`, ora viene registrato un messaggio.
- È stato risolto un problema a causa del quale parti specifiche di dati XDM destinate a un singolo evento venivano incluse in più eventi.

## Versione 2.4.0 - Marzo 2021

- È ora possibile installare l&#39;SDK come pacchetto [NPM](/help/web-sdk/install/npm.md).
- È stato aggiunto il supporto per un&#39;opzione `out` durante la [configurazione del consenso predefinito](/help/web-sdk/commands/configure/defaultconsent.md), che elimina tutti gli eventi fino alla ricezione del consenso (l&#39;opzione `pending` esistente accoda gli eventi e li invia dopo la ricezione del consenso).
- È ora possibile utilizzare il callback [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) per impedire l&#39;invio di un evento.
- Ora utilizza un gruppo di campi dello schema XDM invece di `meta.personalization` per inviare eventi relativi a contenuti personalizzati di cui viene eseguito il rendering o su cui si fa clic.
- Il comando [`getIdentity`](/help/web-sdk/commands/getidentity.md) ora restituisce l&#39;ID dell&#39;area Edge insieme all&#39;identità.
- Gli avvisi e gli errori ricevuti dal server sono stati migliorati e vengono gestiti in modo più appropriato.
- È stato aggiunto il supporto per lo standard Consent 2.0 di Adobe per il comando [`setConsent`](/help/web-sdk/commands/setconsent.md).
- Le preferenze di consenso, quando ricevute, vengono sottoposte a hashing e memorizzate nell’archiviazione locale per un’integrazione ottimizzata tra CMP, Platform Web SDK e Edge Network di Platform. Se stai raccogliendo le preferenze di consenso, ti invitiamo ora a chiamare `setConsent` a ogni caricamento di pagina.
- Sono stati aggiunti due [hook di monitoraggio](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` e `onCommandRejected`.
- Correzione bug: gli eventi di notifica dell’interazione Personalization contenevano informazioni duplicate sulla stessa attività quando un utente passava a una nuova vista di app a pagina singola, tornava alla vista originale e faceva clic su un elemento idoneo per la conversione.
- Correzione bug: se il primo evento inviato dall&#39;SDK fosse impostato su `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) verrebbe utilizzato per inviare l&#39;evento, causando un errore relativo a un&#39;identità non stabilita.`documentUnloading`

## Versione 2.3.0 - novembre 2020

- È stato aggiunto il supporto nonce per consentire criteri di sicurezza dei contenuti più severi.
- È stato aggiunto il supporto alla personalizzazione per le applicazioni a pagina singola.
- È stata migliorata la compatibilità con altro codice JavaScript sulla pagina che potrebbe sovrascrivere le API `window.console`.
- Correzione bug: `sendBeacon` non veniva utilizzato quando `documentUnloading` era impostato su `true` o quando i clic sui collegamenti venivano tracciati automaticamente.
- Correzione bug: se l’elemento di ancoraggio conteneva contenuto HTML, non veniva tracciato automaticamente alcun collegamento.
- Correzione bug: alcuni errori del browser contenenti una proprietà `message` di sola lettura non sono stati gestiti in modo appropriato, causando un errore diverso esposto al cliente.
- Correzione bug: l’esecuzione dell’SDK all’interno di un iframe generava un errore se la pagina HTML dell’iframe proveniva da un sottodominio diverso rispetto alla pagina HTML della finestra principale.

## Versione 2.2.0 - ottobre 2020

- Correzione bug: l&#39;oggetto Opt-in impediva a Web SDK di effettuare chiamate quando `idMigrationEnabled` è `true`.
- Correzione bug: rende Web SDK consapevole delle richieste che devono restituire offerte di personalizzazione per evitare problemi di sfarfallio.

## Versione 2.1.0 - Agosto 2020

- Rimuovere il comando `syncIdentity` e supportare il passaggio di tali ID nel comando `sendEvent`.
- Supporto dello standard di consenso IAB 2.0.
- È supportato il passaggio di ID aggiuntivi nel comando `setConsent`.
- È supportata l&#39;override di `datasetId` nel comando `sendEvent`.
- Supporto degli hook di monitoraggio ([Ulteriori informazioni](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
- Passa `environment: browser` nei dati contestuali dei dettagli di implementazione.
