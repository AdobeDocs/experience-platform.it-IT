---
title: Note sulla versione di Adobi Experience Platform Debugger
description: Note aggiornate sulla versione di Adobe Experience Platform Debugger.
keywords: debugger;estensione Experience Platform Debugger;chrome;estensione;note sulla versione
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: 70abe974aa7f94ea172d7ab90aacaf765b88de0e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 2%

---

# Note sulla versione di Adobi Experience Platform Debugger

## Versione 1.5.0 - 19 ottobre 2023

### Nuove funzionalità

* Mostra collegamenti a proprietà, ambiente e regole nel riepilogo e nei registri dei tag.

### Correzioni e miglioramenti

* È stato risolto un problema a causa del quale i dati di riepilogo dei tag non venivano inviati.
* È stato risolto un problema a causa del quale le sessioni di Assurance generavano un errore CORS
* È stato risolto un problema che impediva la visualizzazione di Target Trace.
* È stato corretto il pulsante Invia feedback.
* È stato risolto il problema relativo all’ID dello stream di dati mancante nel riepilogo dell’SDK web per la versione ≥2.18.0.
* È stato risolto un problema che impediva la ricerca dei registri Edge.
* È stata aggiunta una nota sui profili aggiuntivi per alcuni tipi di account.

## Versione 1.4.1 - 1 novembre 2022

* Prestazioni migliorate sulle pagine con molti eventi di Adobe Experience Platform Assurance.

## Versione 1.4.0 - 3 ottobre 2022

* È stato aggiunto il supporto per il debug di AEP Assurance per le implementazioni ibride dell’SDK per web.
* È stato aggiunto il supporto di più schede all’interno della stessa sessione di AEP Assurance.
* È stato risolto un problema che impediva agli utenti di cambiare profilo/organizzazione dopo l’accesso.
   * Per alcuni account, per cambiare organizzazione è necessario disconnettersi e accedere nuovamente.
* È stato aggiunto un messaggio di errore quando l’abilitazione di Target Trace non riesce.
* Sono state aggiornate le dipendenze.

## Versione 1.3.3 - 20 giugno 2022

* È stato risolto un problema che impediva l’apertura dei popup dalle tabelle degli eventi di rete.
* È stato risolto un problema che impediva il caricamento delle informazioni di Alloy sulla pagina.

## Versione 1.3.2 - 9 giugno 2022

* È stato aggiunto un avatar predefinito al momento dell’accesso dell’utente.
* È stata aggiunta l’evidenziazione della sintassi agli oggetti JSON nei registri.

## Versione 1.3.1 - 24 maggio 2022

* Sono state aggiornate le dipendenze.
* È stato risolto un problema di Analytics che impediva l’abilitazione degli hit di post-elaborazione.
* È stato risolto un problema a causa del quale il debugger si collegava alla finestra di accesso di Adobe.
* È stato risolto un problema AT.js a causa del quale i messaggi del registro non venivano visualizzati nel debugger.

## Versione 1.3.0 - 28 gennaio 2022

* È stato aggiunto il collegamento Informazioni su, che consente di visualizzare la versione corrente e le relative note.
* È stata aggiunta l’opzione per visualizzare gli hit post-elaborati per le richieste di Analytics. L’interruttore è disponibile nella sezione Analytics.
* È stato risolto un problema di sessione di debug remoto che si verificava alla chiusura della sessione all’esterno del debugger.
* È stata corretta la notifica di errore visibile nella scheda Transazioni Edge dell’SDK Web.
* È stato corretto l’avviso di deprecazione dei tag di Adobe nella pagina quando il debugger accedeva all’oggetto _satellite.
* Sono stati risolti alcuni casi in cui un’istanza AppMeasurement non veniva trovata nella pagina.
* È stato risolto un problema di connessione alla pagina che si verificava alla prima apertura della finestra del debugger.

## Versione 1.2.0 - 26 ottobre 2021

* Mostra gli eventi da tutte le schede del browser nella visualizzazione di rete. Per visualizzare solo gli eventi della scheda corrente, seleziona l’icona a forma di lucchetto nell’angolo inferiore destro del debugger.
* Branding aggiornato.

## Versione 1.1.0 - 5 ottobre 2021

* Visualizzazione debug remoto: organizza gli eventi di debug remoto in un diagramma di flusso visivo nella sezione Adobe Experience Platform Web SDK > Transazioni Edge.
* Richiedi che l’organizzazione Adobe Experience Platform Web SDK utilizzata nella pagina corrisponda a quella registrata all’avvio di una nuova sessione di debug remoto.
* Mostra solo le transazioni edge per la scheda connessa. I registri di traccia di Target sono ancora disponibili nella sezione Registri > Edge.
* Consenti la sostituzione della configurazione ID flusso di dati separata per ogni istanza di Adobe Experience Platform Web SDK sulla pagina. Attiva/disattiva l’opzione Aggiungi debug abilitato.
* È stato risolto un problema a causa del quale il token di traccia di Adobe Target non veniva sempre inviato con sessioni di debug remoto per Adobe Experience Platform Web SDK.

## Versione 1.0.0 del 5 maggio 2021

* Prima versione principale di Experienci Platform Debugger. Destinato a sostituire il Experience Cloud Debugger.
