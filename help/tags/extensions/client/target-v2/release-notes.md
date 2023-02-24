---
title: Note sulla versione per l’estensione Adobe Target v2
description: Note sulla versione dell’estensione tag Adobe Target v2 in Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: ffbb68c9c84b834984e1adb2640d8806ce9f9962
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 58%

---

# Note sulla versione dell&#39;estensione Adobe Target v2

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

## v0.19.2 (14 febbraio 2023)

- È stato risolto un problema che impediva l’impostazione del timeout su un elemento dati.

## v0.19.1 (3 febbraio 2023)

- Aggiornamento al supporto `at.js` v2.10.1
- I parametri mbox personalizzati del client ora supportano correttamente la notazione del punto
- Le chiamate di consegna non vengono più effettuate nel Compositore esperienza visivo

## v0.19.0 (19 settembre 2022)

- Aggiornamento al supporto `at.js` v2.10.0
- È stato aggiunto il supporto per il tracciamento tra domini diversi.

## v0.18.0 (1° giugno 2022)

- Aggiornamento al supporto `at.js` v2.9.0
- È stato aggiunto il supporto per i User Agent Client Hints.

## v0.17.1 (28 gennaio 2022)

- Aggiornamento al supporto `at.js` v2.8.1
- Fisso `pageLoad` non mappato su `target-global-mbox` in modalità di esecuzione ibrida ODD
- È stato risolto un problema relativo ai dettagli di analisi per `mbox` richiesta
- Sono state aggiornate le dipendenze di sviluppo per correggere alcune vulnerabilità di sicurezza

## v0.17.0 (7 gennaio 2022)

- Aggiornamento al supporto `at.js` v2.8.0, che sta raccogliendo dati di utilizzo delle funzioni e telemetria delle prestazioni.  I dati personali non vengono raccolti. Per rinunciare a questa funzione, imposta `telemetryEnabled` a `false` in `targetGlobalSettings`.

## v0.16.0 (28 ottobre 2021)

- Aggiornamento al supporto `at.js` v2.7.0, ora disponibile per il download da Adobe Target.

## v0.15.1 (20 luglio 2021)

- È stato risolto un problema relativo a un conflitto nel nome della funzione `stringify` a causa del quale venivano generati valori UUID errati per `sessionId`, `requestId` e così via.

## v0.15.0 (16 luglio 2021)

- Aggiungi un attributo sicuro ai cookie ogni volta `at.js` settings secureOnly è impostato su true
- Ora quando si utilizza `triggerView()` sono disponibili i token di risposta.
- È stato corretto un bug relativo all’evento `CONTENT_RENDERING_NO_OFFERS`. Ora viene attivato correttamente ogni volta che non viene restituito alcun contenuto da Target.
- I dettagli delle metriche di clic di A4T vengono restituiti correttamente quando si utilizzano le richieste prefetch.
- La generazione di UUID non utilizza più `Math.random()`, ma si basa su `window.crypto`
- La scadenza dei cookie `sessionId` viene estesa correttamente a ogni chiamata di rete.
- L’inizializzazione della cache di visualizzazione delle applicazioni a pagina singola è ora gestita correttamente e rispetta le impostazioni `viewsEnable`.

## v0.14.2 (2 giugno 2021)

- Correggi un bug in cui il bundle finale contiene due `at.js` versioni, una con On-Device Decisioning e una senza.

## v0.14.1 (19 maggio 2021)

- È stata corretta la regressione introdotta con la versione v0.14 in cui l’azione Load Target attivava chiamate mbox globali.

## v0.14 (14 maggio 2021)

- È stata aggiunta la nuova azione Carica Target con [decisioning sul dispositivo](./overview.md#load-target-with-on-device-decisioning), che carica 2.5 con funzionalità Decisioning sul dispositivo.`at.js`
- Aggiornato `at.js` a 2.5


## v0.13.7 (25 marzo 2021)

- È stato risolto un problema a causa del quale `targetPageParams` veniva incluso nelle richieste mbox. `targetPageParams` deve essere incluso solo nelle richieste `pageLoad`.
- È stato risolto un problema relativo agli oggetti globali di documenti e finestre nell’estensione tag, sostituendo le dipendenze degli oggetti globali con riferimenti diretti a essi.
- Aggiornato `at.js` da 2.4.1 a 2.4.1.

## v0.13.6 (25 gennaio 2021)

- Aggiunge il supporto per l&#39;ID di piattaforma/profilo unificato agli ID cliente API di consegna
- Corregge l&#39;inserimento di tag di stile non validi
- Aggiornamento di at.s a 2.4.0
- È stato risolto un problema a causa del quale parametri non definiti possono causare richieste di consegna non valide.

## v0.13.4 (25 novembre 2020)

- È stato corretto un bug a causa del quale i parametri mbox non venivano visualizzati nell’interfaccia utente.
- Aggiornamenti degli elementi di branding
- È stato aggiornato il `at.js` versione a 2.3.3

## v0.13.3 (24 luglio 2020)

- È stato corretto un bug a causa del quale i collegamenti in modalità QA non funzionavano per le attività inattive
- È stato corretto un bug a causa del quale l’estensione non riusciva se uno script o un codice aggiungeva una proprietà `default` a `window` o `document`

## v0.13.2 (15 giugno 2020)

- È stato risolto un problema che si verificava con l’utilizzo di CNAME e Edge override, dove `at.js` 1.x potrebbe creare il dominio del server in modo errato, causando l’errore della richiesta Target
- È stato risolto un problema a causa del quale, quando si utilizzava l’estensione tag v2 per Target e l’estensione tag Adobe Analytics, Target ritardava la chiamata sendBeacon di Analytics.
- È stata migliorata l’impostazione `deviceIdLifetime` rendendola sostituibile tramite `targetGlobalSettings`

## v0.13.0 (25 marzo 2020)

- Aggiornato `at.js` alla versione v2.3.
- È stato aggiunto il supporto per Target Global Mbox nell’API adobe.target.getOffer.
- È stato risolto un problema che impediva l’elaborazione corretta dei parametri e dei parametri di caricamento delle pagine.

## v0.12.0 (10 ottobre 2019)

- Aggiornato `at.js` alla versione v2.2.
- Migliorate le prestazioni per le integrazioni tra la libreria Experience Cloud ID (ECID) v4.4 e `at.js` 2.2.
- In precedenza, la libreria ECID effettuava due chiamate di blocco prima di `at.js` potrebbero recuperare le esperienze. Ora effettua una sola chiamata, migliorando notevolmente le prestazioni.

>[!NOTE]
>Aggiorna l’estensione tag ECID alla versione 4.4.1 per approfittare di questo miglioramento delle prestazioni.

## v0.11.1 (31 luglio 2019)

- Versione aggiornata dell&#39;estensione da utilizzare `at.js` 2.1.1.
- È stata aggiunta una correzione per la gestione dei parametri.

## v0.11.0 (3 giugno 2019)

- Nuova estensione tag per il supporto `at.js` 2.1
