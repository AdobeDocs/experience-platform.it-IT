---
title: Vista di Adobe Analytics in Assurance
description: Questa guida spiega come utilizzare Adobe Analytics con Adobe Experience Platform Assurance.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 66c9b8c1489b86b0b928fc37380f2187a7d237cf
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 17%

---

# Visualizzazione eventi di Adobe Analytics in Assurance

Gli eventi di Analytics forniscono una visualizzazione più completa degli eventi SDK agli utenti che eseguono il debug e la convalida dell’implementazione di Adobe Analytics. La visualizzazione mostra gli eventi inviati ad Adobe Analytics da [Adobe Experience Platform Edge Network SDK](https://developer.adobe.com/client-sdks/edge/edge-network/) e da [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/solution/adobe-analytics/). La visualizzazione include anche un pannello dei dettagli che fornisce informazioni contestuali su come l’evento è stato elaborato dall’SDK client e dai servizi a monte dopo che ha lasciato il dispositivo.

## Introduzione

La procedura seguente illustra come utilizzare questa visualizzazione:

1. [Configura Adobe Experience Platform Assurance](../tutorials/implement-assurance.md).
2. [Crea e connetti a una sessione Assurance](../tutorials/using-assurance.md).
3. Nell&#39;interfaccia utente Assurance dal menu di visualizzazione **Home** della navigazione a sinistra, seleziona **Eventi di Analytics**. Se non trovi questa opzione, seleziona **Configura** in basso a sinistra nella finestra, aggiungi **Eventi di Analytics** e seleziona **Salva**.

## Vista Edge di Analytics

Utilizza la visualizzazione Edge di Analytics se utilizzi **estensioni mobili Edge Network** o **Edge Bridge**. Questa visualizzazione viene attivata quando nell’angolo in alto a destra è attivato l’interruttore &quot;Analytics Edge View&quot; (Visualizzazione Analytics), che mostra gli eventi Analytics inviati tramite la rete Edge nella sessione corrente. Sono inclusi tutti gli eventi attivati dall’estensione del ciclo di vita, dall’estensione Edge e/o dall’estensione Edge Bridge.

![Immagine che mostra l&#39;interruttore che ha cambiato la visualizzazione Edge di Analytics.](./images/adobe-analytics/edge-analytics-view-toggle.png)

La vista Edge di Analytics contiene informazioni sugli eventi Edge correlati ad Analytics e sugli eventi del ciclo di vita inviati dal client. Scegliendo un evento nell’elenco, il pannello della visualizzazione dettagli evento a destra mostra gli eventi elaborati dall’SDK client e dal servizio a monte dopo che hanno lasciato il dispositivo. Questo consente di visualizzare facilmente la catena di eventi risultanti da una chiamata.

![Immagine che illustra i diversi componenti presenti nella vista Edge di Analytics per lo scenario Edge Bridge.](./images/adobe-analytics/edgebridge-analytics-events.png)

L&#39;evento **Dati post-elaborati** nell&#39;elenco conferma che i dati sono stati elaborati e inviati correttamente ad Adobe Analytics. Se manca questo evento o qualsiasi dato elaborato, gli utenti possono espandere ogni evento nell’elenco per visualizzare informazioni di debug dettagliate.

### Visualizzazione dettagli evento Edge di Analytics

Per un evento di richiesta di Edge o un evento di tracciamento di Analytics, la vista dettagliata contiene le seguenti informazioni:

* Dettagli evento: un evento di richiesta Edge SDK di origine.
* Richiesta Edge Bridge: evento esclusivamente per il flusso di lavoro dell’estensione Edge Bridge.
* Stream di dati: evento rappresentato per lo stream di dati per questa sessione.
* Hit di Edge ricevuto: rappresenta l’hit ricevuto da Edge.
* Hit di Edge elaborato: rappresenta l’hit elaborato in Edge.
* Hit di Analytics: rappresenta l’hit ricevuto da Analytics.
* Mappatura di Analytics: rappresenta lo stato di mappatura dei dati in Analytics.
* Analytics Responsed: stato di risposta da Analytics.
* Dati post-elaborazione: informazioni sull’evento che contiene la mappatura di revar, evar e prop.

### Convalida di Analytics Edge

La vista di convalida di Analytics Edge consente di visualizzare facilmente i risultati sugli script di convalida relativi alla sessione di Analytics Edge. Gli errori visualizzati dai validatori possono contenere collegamenti a dove devono essere corretti o visualizzare eventi in stato di errore.

![Immagine che mostra la scheda Convalida nella visualizzazione Edge di Analytics.](./images/adobe-analytics/edge-analytics-validation-view.png)

## Visualizzazione eventi di Analytics

Utilizza la visualizzazione eventi di Analytics se utilizzi l&#39;estensione mobile **Adobe Analytics**. Questa vista consente di visualizzare facilmente gli eventi di Analytics inviati dal client connesso, inclusi gli eventi Track Action, Track State e Lifecycle. Questa visualizzazione è attiva quando l’opzione &quot;Analytics Edge View&quot; (Visualizzazione Analytics) in alto a destra è disabilitata.

![Immagine che mostra l&#39;interruttore che ha cambiato la visualizzazione Analytics.](./images/adobe-analytics/direct-analytics-view-toggle-button.png)

Selezionando uno degli eventi di Analytics nella tabella degli eventi, nel pannello di destra è possibile visualizzare i dettagli dell’elaborazione dell’evento.

![Immagine che illustra componenti diversi nella visualizzazione eventi di Analytics.](./images/adobe-analytics/analytics-events.png)

### Stato post-elaborazione

Dopo che l’SDK ha effettuato una richiesta di rete con Adobe Analytics, lo stato ti dirà se Assurance è stato in grado di recuperare le informazioni di post-elaborazione per la richiesta di Adobe Analytics. La vista Eventi di Analytics deve rimanere attiva finché lo stato di post-elaborazione è in funzione dopo l’attivazione della richiesta.

Per recuperare le informazioni di post-elaborazione, l’utente connesso deve avere accesso alla suite di rapporti corrispondente.

| Stato | Descrizione |
| :----- | :---------- |
| `Queued` | La richiesta di rete sta recuperando le informazioni di post-elaborazione. |
| `Processed` | La richiesta di rete è riuscita e vengono ricevute le informazioni di post-elaborazione. |
| `Delayed` | È stato superato il numero massimo di tentativi per recuperare le informazioni di post-elaborazione. |
| `Error` | Un errore ha causato un errore nella richiesta di rete. Maggiori dettagli sull’errore vengono visualizzati nella vista dettagli dell’evento. |
| `Unauthorized` | L’utente non ha accesso alla suite di rapporti di Adobe Analytics. |
| `Unavailable` | La richiesta di Adobe Analytics non ha un evento `AnalyticsResponse` corrispondente. |
| `No Debug Flag` | La versione corrente di Adobe Analytics o Assurance SDK potrebbe non supportare la funzione di debug di Analytics. Per ulteriori informazioni, consulta la [Guida alla risoluzione dei problemi](../troubleshooting.md). |
| `Expired` | L’evento `AnalyticsTrack` o `LifecycleStart` è precedente alle 24 ore. |

### Vista dettagli dell’evento

Per un evento di tracciamento di Analytics, la vista dettagliata contiene le parti seguenti:

* Un evento di richiesta dell’SDK di Analytics di origine.
* Metadati e dati contestuali della richiesta, come ID suite di rapporti, versioni dell’estensione SDK e dati contestuali.
* Informazioni post-elaborate sull’evento Analytics che contiene la mappatura di revar, evar e prop.

### Convalida visualizzazione Analytics

La vista di convalida consente di visualizzare facilmente i risultati sugli script di convalida relativi ad Analytics. Gli errori visualizzati dai validatori possono contenere collegamenti a dove devono essere corretti o visualizzare eventi in stato di errore.

![Immagine che mostra la scheda Convalida nella visualizzazione Analytics.](./images/adobe-analytics/analytics-validation-view.png)