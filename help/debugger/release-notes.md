---
title: Note sulla versione di Adobe Experience Platform Debugger
description: Note aggiornate sulla versione di Adobe Experience Platform Debugger.
keywords: debugger; estensione experience debugger;chrome;estensione;note sulla versione
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: 877e38154f6959d50bd0620290c2dce9decfc2b5
workflow-type: ht
source-wordcount: '781'
ht-degree: 100%

---

# Note sulla versione di Adobe Experience Platform Debugger

## Versione 1.6.1 - 25 luglio 2024

### Correzioni e miglioramenti

* È stato risolto un problema che impediva agli utenti di aggiungere nuovi codici di incorporamento dei tag alle pagine senza di essi.

## Versione 1.6.0 - 11 luglio 2024

### Nuove funzioni

* Consentono agli utenti di acconsentire o rinunciare alla raccolta di dati tecnici e personali.

### Correzioni e miglioramenti

* Sono stati corretti l’inserimento di script in Firefox e il collegamento dell’informativa sulla privacy.
* Acquisisci le richieste di Analytics mancanti.
* Correggi gli arresti anomali sulle pagine con molti messaggi complessi della console.
* Adobe Experience Platform Debugger è stato aggiornato a un’estensione Manifest v3.

## Versione 1.5.4 - 19 dicembre 2023

### Correzioni e miglioramenti

* È stato risolto un problema che impediva il mantenimento delle impostazioni.
* È stato risolto un problema che causava l’arresto anomalo del debugger durante la visualizzazione degli hit post-elaborati di Analytics.

## Versione 1.5.3 - 6 dicembre 2023

### Nuove funzioni

* È stata aggiunta l’impostazione “blocca sulla scheda attiva all’apertura del debugger”.

### Correzioni e miglioramenti

* È stato risolto un problema a causa del quale nei domini privati mancavano le richieste di Analytics.
* È stato risolto un problema che causava l’assenza di dati Activity Map nella tabella delle richieste di Analytics.
* È stato risolto un problema che causava un arresto anomalo durante la visualizzazione di Target Trace.
* È stato aggiunto un avviso quando il debugger non riesce a configurare l’infrastruttura su pagina in Firefox.

## Versione 1.5.2 - 10 novembre 2023

(Solo Firefox)

### Correzioni e miglioramenti

* È stata aggiornata l’organizzazione dei file.

## Versione 1.5.1 - 2 novembre 2023

### Correzioni e miglioramenti

* Sono stati risolti dei problemi a causa dei quali gli eventi di Analytics venivano ignorati o duplicati.
* È stato risolto un problema che causava il superamento della dimensione massima di archiviazione dello stato.
* È stato risolto un problema che impediva alla ricerca dei registri di Edge di filtrare gli eventi.

## Versione 1.5.0 - 19 ottobre 2023

### Nuove funzioni

* Mostra collegamenti a proprietà, ambiente e regole nel riepilogo e nei registri dei tag.

### Correzioni e miglioramenti

* È stato risolto un problema a causa del quale i dati di riepilogo dei tag non venivano inviati.
* È stato risolto un problema a causa del quale le sessioni di Assurance generavano un errore CORS
* È stato risolto un problema che impediva la visualizzazione di Target Trace.
* È stato corretto il pulsante “Invia feedback”.
* È stato risolto il problema relativo all’“ID dello stream di dati” mancante nel riepilogo del Web SDK per la versione ≥2.18.0.
* È stato risolto un problema che impediva la ricerca dei registri di Edge.
* È stata aggiunta una nota sui profili aggiuntivi per alcuni tipi di account.

## Versione 1.4.1 - 1 novembre 2022

* Prestazioni migliorate sulle pagine con molti eventi di Adobe Experience Platform Assurance.

## Versione 1.4.0 - 3 ottobre 2022

* È stato aggiunto il supporto per il debug di AEP Assurance per le implementazioni ibride del Web SDK.
* È stato aggiunto il supporto di più schede all’interno della stessa sessione di AEP Assurance.
* È stato risolto un problema che impediva agli utenti di cambiare profilo/organizzazione dopo l’accesso.
   * Per alcuni account, per cambiare organizzazione è necessario disconnettersi e accedere nuovamente.
* È stato aggiunto un messaggio di errore quando l’abilitazione di Target Trace non riesce.
* Sono state aggiornate le dipendenze.

## Versione 1.3.3 - 20 giugno 2022

* È stato risolto un problema che impediva l’apertura dei pop-up dalle tabelle degli eventi di rete.
* È stato risolto un problema che impediva il caricamento delle informazioni di Alloy sulla pagina.

## Versione 1.3.2 - 9 giugno 2022

* È stato aggiunto un avatar predefinito al momento dell’accesso dell’utente.
* È stata aggiunta l’evidenziazione della sintassi agli oggetti JSON nei registri.

## Versione 1.3.1, 24 maggio 2022

* Sono state aggiornate le dipendenze.
* È stato risolto un problema di Analytics che impediva l’abilitazione degli hit di post-elaborazione.
* È stato risolto un problema a causa del quale il debugger si collegava alla finestra di accesso di Adobe.
* È stato risolto un problema AT.js a causa del quale i messaggi del registro non venivano visualizzati nel debugger.

## Versione 1.3.0 - 28 gennaio 2022

* È stato aggiunto il collegamento Informazioni su, che consente di visualizzare la versione corrente e le relative note.
* È stato aggiunto il pulsante per visualizzare o nascondere gli hit post-elaborati per le richieste di Analytics. L’interruttore è disponibile nella sezione di Analytics.
* È stato risolto un problema di sessione di debug remoto che si verificava alla chiusura della sessione all’esterno del debugger.
* È stata corretta la notifica di errore visibile nella scheda Transazioni Edge del Web SDK.
* È stato corretto l’avviso di deprecazione dei tag di Adobe nella pagina quando il debugger accedeva all’oggetto _satellite.
* Sono stati risolti alcuni casi in cui un’istanza AppMeasurement non veniva trovata nella pagina.
* È stato risolto un problema di connessione alla pagina che si verificava alla prima apertura della finestra del debugger.

## Versione 1.2.0 - 26 ottobre 2021

* È possibile visualizzare gli eventi da tutte le schede del browser nella visualizzazione di rete. Per visualizzare solo gli eventi della scheda corrente, seleziona l’icona a forma di lucchetto nell’angolo inferiore destro del debugger.
* Branding aggiornato.

## Versione 1.1.0 - 5 ottobre 2021

* Visualizzazione debug remoto: organizza gli eventi di debug remoto in un grafico di flusso visivo nella sezione Adobe Experience Platform Web SDK > Transazioni Edge.
* All’avvio di una nuova sessione di debug remoto, viene richesto che l’organizzazione Adobe Experience Platform Web SDK utilizzata nella pagina corrisponda a quella con cui è stato eseguito l’accesso.
* È possibile mostraee solo le transazioni Edge per la scheda connessa. I registri di tracciamento di Target sono ancora disponibili nella sezione Registri > Edge.
* È consentito sostituire separatamente la configurazione dell’ID dello stream di dati per ogni istanza di Adobe Experience Platform Web SDK sulla pagina. È stato aggiunto un pulsante per abilitare/disabilitare il debug.
* È stato risolto un problema a causa del quale il token di tracciamento di Adobe Target non veniva sempre inviato con sessioni di debug remoto per Adobe Experience Platform Web SDK.

## Versione 1.0.0 del 5 maggio 2021

* Prima versione principale di Experience Platform Debugger. È destinato a sostistuire Experience Cloud Debugger.
