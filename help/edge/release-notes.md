---
title: Note sulla versione di Adobe Experience Platform Web SDK
description: Note sulla versione più recente di Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;note sulla versione;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: b12f97a7c5e937a116d86495b3434dd9c0805b04
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 2%

---


# Note sulla versione

Questo documento illustra le note sulla versione dell’SDK Web per Adobe Experience Platform.
Per le ultime note sulla versione dell&#39;estensione tag SDK per web, vedi [Note sulla versione dell’estensione del tag SDK per web](extension/web-sdk-ext-release-notes.md).

## Versione 2.12.0 - 29 giugno 2022

* Modifica le richieste in Edge Network per utilizzare il `cluster` hint di posizione cookie come parte dell’URL. In questo modo gli utenti che cambiano posizione (ad esempio tramite una VPN o guidando con dispositivi mobili, ecc.) a metà sessione hanno lo stesso perimetro e lo stesso profilo di personalizzazione.
* Rafforzare le funzioni configurate nella risposta del comando getLibraryInfo.

## Versione 2.11.0 - 13 giugno 2022

**Nuove funzioni**

* È ora possibile fornire esperienze personalizzate con maggiore precisione, condividendo ID visitatore tra app mobili e contenuti web per dispositivi mobili, e tra domini diversi. Consulta la sezione [documentazione dedicata](identity/id-sharing.md) per saperne di più.
* Ora è possibile eseguire il rendering o l&#39;esecuzione di un array di proposizioni da [!DNL Adobe Target] nelle applicazioni a pagina singola, senza incrementare le metriche di analisi. Questo riduce gli errori di reporting e aumenta l’accuratezza dell’analisi. Consulta la sezione [documentazione dedicata](personalization/rendering-personalization-content.md#applypropositions) per saperne di più.
* Sono state aggiunte ulteriori informazioni alla sezione `getLibraryInfo` Compresi i comandi disponibili e la configurazione finale per l&#39;istanza.

**Correzioni e miglioramenti**

* Sono state aggiornate le impostazioni dei cookie da utilizzare `sameSite="none"` e `secure` flag su [!DNL HTTPS] pagine.
* È stato risolto un problema a causa del quale il contenuto personalizzato non veniva applicato correttamente quando si utilizzava il comando `eq` pseudo selettore.
* È stato risolto un problema in cui `localTimezoneOffset` potrebbe non riuscire a convalidare l&#39;Experience Platform.

## Versione 2.10.1 - 3 maggio 2022

* È stato risolto un problema che causava la creazione di più iframe persistenti per le sincronizzazioni ID e le destinazioni dei segmenti.

## Versione 2.10.0 - 22 aprile 2022

* Utilizza un iframe permanente per tutte le sincronizzazioni ID e le destinazioni dei segmenti.
* È stato risolto un problema a causa del quale le proposizioni delle metriche unite venivano duplicate nel `sendEvent` risultato.

## Versione 2.9.0 - 10 marzo 2022

* È stato aggiunto il supporto per il tracciamento [!DNL control (default)] Esperienze Adobe Target.
* Ottimizzazione degli eventi di visualizzazione e modifica per le applicazioni a pagina singola. La notifica di visualizzazione è ora inclusa con l’evento di visualizzazione cambiamento quando si esegue il rendering di esperienze personalizzate.
* Avviso della console rimosso in caso di assenza `eventType` è presente.
* È stato risolto un problema che causava la `propositions` è stata restituita solo da un `sendEvent` quando le esperienze sono state richieste o recuperate dalla cache. La `propositions` ora viene sempre definita come array.
* È stato risolto un problema che impediva la visualizzazione dei contenitori nascosti in caso di errore restituito da Adobe Experience Edge.
* È stato risolto un problema che impediva il conteggio degli eventi interattivi in Adobe Target. Questo problema è stato risolto aggiungendo il nome della visualizzazione a XDM in web.webPageDetails.viewName.
* Correggere i collegamenti interrotti alla documentazione nei messaggi della console.

## Versione 2.8.0 - 19 gennaio 2022

* Supporta i selettori DOM ombra per la personalizzazione.
* Tipi di eventi di personalizzazione rinominati. (`display` e `click` diventare `decisioning.propositionDisplay` e `decisioning.propositionInteract`)
* È stato risolto un problema a causa del quale le offerte HTML con tag script in linea aggiungevano due volte i tag script alla pagina anche se lo script veniva eseguito una sola volta.

## Versione 2.7.0 - 26 ottobre 2021

* Esporre informazioni aggiuntive da Experience Edge nel valore restituito da `sendEvent`, tra cui `inferences` e `destinations`. Il formato di queste proprietà può cambiare in quanto queste funzioni vengono attualmente distribuite come parte di una versione beta. Per ulteriori informazioni, consulta [Tracciamento degli eventi.](fundamentals/tracking-events.md)

## Versione 2.6.4 - 7 settembre 2021

* È stato risolto un problema che causava l’impostazione di azioni HTML Adobe Target applicate al `head` stavano sostituendo l&#39;intero `head` contenuto. Ora imposta le azioni di HTML applicate al `head` vengono modificati per aggiungere HTML.

## Versione 2.6.3 - 16 agosto 2021

* È stato risolto un problema a causa del quale gli oggetti non destinati all’uso pubblico venivano esposti tramite la promessa risolta dal `configure` comando.

## Versione 2.6.2 - 4 agosto 2021

* È stato risolto un problema che causava un avviso di elementi obsoleti di `result.decisions` (forniti `sendEvent` viene registrato nella console anche quando `result.decisions` non è stato effettuato l&#39;accesso alla proprietà. Non verrà registrato alcun avviso quando si accede al `result.decisions` , ma la proprietà rimane obsoleta.

## Versione 2.6.1 - 29 luglio 2021

* È stato risolto un problema a causa del quale il rendering della personalizzazione per una visualizzazione di app a pagina singola senza contenuto di personalizzazione generava un errore e causava la restituzione della promessa dal `sendEvent` comando da rifiutare.

## Versione 2.6.0 - 27 luglio 2021

* Fornisce più contenuto di personalizzazione nel `sendEvent` promessa risolta, inclusi i token di risposta di Adobe Target. Quando il `sendEvent` viene eseguito un comando, viene restituita una promessa, che alla fine viene risolta con un `result` oggetto contenente le informazioni ricevute dal server. In precedenza, questo oggetto risultato includeva una proprietà denominata `decisions`. Questo `decisions` La proprietà è stata dichiarata obsoleta. Una nuova proprietà, `propositions`è stato aggiunto . Questa nuova proprietà consente ai clienti di accedere a più contenuti di personalizzazione, tra cui [token di risposta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## Versione 2.5.0 - giugno 2021

* È stato aggiunto il supporto per le offerte di personalizzazione di reindirizzamento.
* Le larghezze e le altezze del riquadro di visualizzazione raccolte automaticamente con valori negativi non verranno più inviate al server.
* Quando un evento viene annullato restituendo `false` da `onBeforeEventSend` callback, ora viene registrato un messaggio.
* È stato risolto un problema a causa del quale parti specifiche di dati XDM destinate a un singolo evento venivano incluse in più eventi.

## Versione 2.4.0 - marzo 2021

* L&#39;SDK può ora essere [installato come pacchetto npm](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=it).
* È stato aggiunto il supporto per un `out` opzione quando [configurazione del consenso predefinito](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), che rilascia tutti gli eventi finché non viene ricevuto il consenso (il `pending` mette in coda gli eventi e li invia una volta ricevuto il consenso).
* La [callback onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) può ora essere utilizzato per impedire l’invio di un evento.
* Ora utilizza un gruppo di campi di schema XDM anziché `meta.personalization` quando si inviano eventi relativi a contenuti personalizzati di cui si sta eseguendo il rendering o si fa clic su di essi.
* La [getIdentity, comando](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) ora restituisce l&#39;ID della regione perimetrale accanto all&#39;identità.
* Gli avvisi e gli errori ricevuti dal server sono stati migliorati e vengono gestiti in modo più appropriato.
* È stato aggiunto il supporto per [Standard Adobe Consent 2.0](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Quando vengono ricevute, le preferenze di consenso vengono hashing e memorizzate nell’archivio locale per un’integrazione ottimizzata tra CMP, Platform Web SDK e Platform Edge Network. Se raccogli le preferenze di consenso, ti invitiamo a chiamare `setConsent` a ogni caricamento di pagina.
* Due [ganci di monitoraggio](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` e `onCommandRejected`, sono stati aggiunti.
* Correzione bug: Gli eventi di notifica dell’interazione di personalizzazione conterrebbero informazioni duplicate sulla stessa attività quando un utente passava a una nuova visualizzazione di app a pagina singola, tornava alla visualizzazione originale e faceva clic su un elemento idoneo alla conversione.
* Correzione bug: Se il primo evento inviato dall’SDK era `documentUnloading` impostato su `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) viene utilizzato per inviare l&#39;evento, con conseguente errore relativo a un&#39;identità non stabilita.

## Versione 2.3.0 - novembre 2020

* È stato aggiunto il supporto nonce per consentire criteri di sicurezza dei contenuti più rigorosi.
* È stato aggiunto il supporto per la personalizzazione per le applicazioni a pagina singola.
* È stata migliorata la compatibilità con altri codici JavaScript on-page che potrebbero essere sovrascritti `window.console` API.
* Correzione bug: `sendBeacon` non è stato utilizzato quando `documentUnloading` è impostato su `true` o quando i clic sul collegamento sono stati tracciati automaticamente.
* Correzione bug: Un collegamento non viene tracciato automaticamente se l’elemento di ancoraggio contiene contenuto HTML.
* Correzione bug: Alcuni errori del browser contenenti una sola lettura `message` la proprietà non è stata gestita in modo appropriato e si è verificato un errore diverso.
* Correzione bug: L&#39;esecuzione dell&#39;SDK all&#39;interno di un iframe genererebbe un errore se la pagina HTML dell&#39;iframe proveniva da un sottodominio diverso rispetto alla pagina HTML della finestra principale.

## Versione 2.2.0 - ottobre 2020

* Correzione bug: L&#39;oggetto Opt-in impediva ad Alloy di effettuare chiamate quando `idMigrationEnabled` è `true`.
* Correzione bug: Presta attenzione alle richieste che dovrebbero restituire le offerte di personalizzazione per evitare un problema di sfarfallio.

## Versione 2.1.0 - agosto 2020

* Rimuovi `syncIdentity` e supportano il passaggio di tali ID nel `sendEvent` comando.
* Supporto dello standard di consenso IAB 2.0.
* Supporto per il passaggio di ID aggiuntivi nella `setConsent` comando.
* Supporto per ignorare i `datasetId` in `sendEvent` comando.
* Supporta i monitor della lega ([Leggi tutto](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Pass `environment: browser` nei dettagli di implementazione dati contestuali.
