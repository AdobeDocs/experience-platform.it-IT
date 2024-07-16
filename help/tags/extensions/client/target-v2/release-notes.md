---
title: Note sulla versione per l’estensione Adobe Target v2
description: Note sulla versione dell’estensione tag Adobe Target v2 in Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: a062305e3ed0eb4d127f93ff37efe15e41eaa601
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 42%

---

# Note sulla versione dell’estensione Adobe Target v2

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

## v0.20.3 (23 gennaio 2024)

- Aggiornato per supportare `at.js` 2.11.4
- È stato corretto un bug per impedire l’invio di dati geografici non validi all’API di consegna.

## v0.20.2 (29 novembre 2023)

- Aggiornato per supportare `at.js` 2.11.3
- È stato corretto un bug che impediva l’invio dei token di risposta su eventi at-content-rendering-failed.

## v0.20.1 (3 novembre 2023)

- Aggiornato per supportare `at.js` 2.11.2.
- È stato corretto un bug che causava incoerenze nei token di risposta inviati su eventi personalizzati.

## v0.20.0 (9 ottobre 2023)

- Aggiornato per supportare `at.js` 2.11.0.
- È stato aggiunto il supporto per l’impostazione di sandboxId e sandboxName personalizzati per Adobe Experience Platform in targetGlobalSettings, che verranno trasmessi all’API di consegna nelle chiamate getOffer/getOffers.
- Correzione DOM shadow per il concatenamento :eq() nel selettore.

## v0.19.3 (18 settembre 2023)

- Aggiornato per supportare `at.js` v2.10.3.
- È stato risolto un problema che attivava erroneamente l’evento personalizzato di rendering del contenuto at quando non veniva eseguito il rendering di alcuna offerta. Ora viene attivato l’evento corretto, at-content-rendering-no-offers (Rendering-nessun’offerta).
- Sono stati aggiunti eventToken e responseTokens all’oggetto errore per l’evento personalizzato at-content-rendering-failed.

## v0.19.2 (14 febbraio 2023)

- È stato risolto un problema che consentiva di impostare il timeout su un elemento dati.

## v0.19.1 (3 febbraio 2023)

- Aggiornato per supportare `at.js` v2.10.1
- I parametri Mbox personalizzati del client ora supportano correttamente la notazione del punto
- Chiamate di consegna non più effettuate nel Compositore esperienza visivo

## v0.19.0 (19 settembre 2022)

- Aggiornato per supportare `at.js` v2.10.0
- È stato aggiunto il supporto per il tracciamento tra più domini.

## v0.18.0 (1° giugno 2022)

- Aggiornato per supportare `at.js` v2.9.0
- È stato aggiunto il supporto per i User Agent Client Hints.

## v0.17.1 (28 gennaio 2022)

- Aggiornato per supportare `at.js` v2.8.1
- È stato corretto un problema che impediva il mapping di `pageLoad` a `target-global-mbox` in modalità di esecuzione ibrida ODD
- È stato risolto un problema relativo ai dettagli di analisi per la richiesta `mbox`
- Sono state aggiornate le dipendenze di sviluppo per correggere le vulnerabilità di sicurezza

## v0.17.0 (7 gennaio 2022)

- Aggiornato per supportare `at.js` v2.8.0, che sta raccogliendo dati di telemetria relativi all&#39;utilizzo delle funzionalità e alle prestazioni.  I dati personali non vengono raccolti. Per rinunciare a questa funzione, impostare `telemetryEnabled` su `false` in `targetGlobalSettings`.

## v0.16.0 (28 ottobre 2021)

- Aggiornato per supportare `at.js` v2.7.0, ora disponibile per il download da Adobe Target.

## v0.15.2 (16 agosto 2021)

- Aggiornato per supportare `at.js` 2.6.1.
- Inizializza il decisioning sul dispositivo all’avvio, indipendentemente dall’evento Caricamento pagina.
- È ora possibile utilizzare le decisioni sul dispositivo alla prima visita dopo il download dell’artefatto.

## v0.15.1 (20 luglio 2021)

- È stato risolto un problema relativo a un conflitto nel nome della funzione `stringify` a causa del quale venivano generati valori UUID errati per `sessionId`, `requestId` e così via.

## v0.15.0 (16 luglio 2021)

- Aggiungi l&#39;attributo secure ai cookie ogni volta che `at.js` impostazioni secureOnly è impostato su true
- Ora quando si utilizza `triggerView()` sono disponibili i token di risposta.
- È stato corretto un bug relativo all’evento `CONTENT_RENDERING_NO_OFFERS`. Ora viene attivato correttamente ogni volta che non viene restituito alcun contenuto da Target.
- I dettagli delle metriche di clic di A4T vengono restituiti correttamente quando si utilizzano le richieste prefetch.
- La generazione di UUID non utilizza più `Math.random()`, ma si basa su `window.crypto`
- La scadenza dei cookie `sessionId` viene estesa correttamente a ogni chiamata di rete.
- L’inizializzazione della cache di visualizzazione delle applicazioni a pagina singola è ora gestita correttamente e rispetta le impostazioni `viewsEnable`.

## v0.14.2 (2 giugno 2021)

- È stato corretto un bug a causa del quale il bundle finale conteneva due versioni di `at.js`, una con decisioning sul dispositivo e una senza.

## v0.14.1 (19 maggio 2021)

- È stata corretta la regressione introdotta con la versione v0.14 in cui l’azione Load Target attivava chiamate mbox globali.

## v0.14 (14 maggio 2021)

- È stata aggiunta la nuova azione Carica Target con [Decisioning sul dispositivo](./overview.md#load-target-with-on-device-decisioning), che carica `at.js` 2.5 con funzionalità Decisioning sul dispositivo
- Aggiornamento di `at.js` a 2.5


## v0.13.7 (25 marzo 2021)

- È stato risolto un problema a causa del quale `targetPageParams` veniva incluso nelle richieste mbox. `targetPageParams` deve essere incluso solo nelle richieste `pageLoad`.
- È stato risolto un problema relativo agli oggetti globali di documenti e finestre nell’estensione tag, sostituendo le dipendenze degli oggetti globali con riferimenti diretti a essi.
- Aggiornamento di `at.js` alla versione 2.4.1.

## v0.13.6 (25 gennaio 2021)

- Aggiunge il supporto per l&#39;ID di piattaforma/profilo unificato agli ID cliente API di consegna
- Corregge l&#39;inserimento di tag di stile non validi
- Aggiornamento di at.s a 2.4.0
- È stato risolto un problema a causa del quale parametri non definiti possono causare richieste di consegna non valide.

## v0.13.4 (25 novembre 2020)

- È stato corretto un bug a causa del quale i parametri mbox non venivano visualizzati nell’interfaccia utente.
- Aggiornamenti degli elementi di branding
- Aggiornamento della versione `at.js` alla versione 2.3.3

## v0.13.3 (24 luglio 2020)

- È stato corretto un bug a causa del quale i collegamenti in modalità QA non funzionavano per le attività inattive
- È stato corretto un bug a causa del quale l’estensione non riusciva se uno script o un codice aggiungeva una proprietà `default` a `window` o `document`

## v0.13.2 (15 giugno 2020)

- È stato risolto un problema che si verificava durante l&#39;utilizzo di CNAME e Edge override, a causa del quale `at.js` 1.x poteva creare il dominio del server in modo errato e la richiesta Target non riusciva
- È stato risolto un problema a causa del quale, quando si utilizzava l’estensione tag v2 per Target e l’estensione tag Adobe Analytics, Target ritardava la chiamata sendBeacon di Analytics.
- È stata migliorata l’impostazione `deviceIdLifetime` rendendola sostituibile tramite `targetGlobalSettings`

## v0.13.0 (25 marzo 2020)

- Aggiornamento di `at.js` alla versione v2.3.
- È stato aggiunto il supporto per Target Global Mbox nell’API adobe.target.getOffer.
- È stato risolto un problema che impediva l’elaborazione corretta dei parametri e dei parametri di caricamento delle pagine.

## v0.12.0 (10 ottobre 2019)

- Aggiornamento di `at.js` a v2.2.
- Sono state migliorate le prestazioni per le integrazioni tra la libreria Experience Cloud ID (ECID) v4.4 e `at.js` 2.2.
- In precedenza, la libreria ECID effettuava due chiamate di blocco prima che `at.js` potesse recuperare le esperienze. Ora effettua una sola chiamata, migliorando notevolmente le prestazioni.

>[!NOTE]
>Aggiorna l’estensione tag ECID alla versione 4.4.1 per approfittare di questo miglioramento delle prestazioni.

## v0.11.1 (31 luglio 2019)

- Versione aggiornata dell&#39;estensione da utilizzare `at.js` 2.1.1
- È stata aggiunta una correzione per la gestione dei parametri.

## v0.11.0 (3 giugno 2019)

- Nuova estensione tag per supportare `at.js` 2.1
