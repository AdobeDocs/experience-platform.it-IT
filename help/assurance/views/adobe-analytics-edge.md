---
title: Eventi di Analytics 2.0 in Assurance
description: Questa guida spiega come utilizzare Adobe Analytics e Analytics Edge View con Adobe Experience Platform Assurance.
badgeBeta: label="Beta" type="Informative"
source-git-commit: f707554ea89731fbd3f013d6065fde27ba7fa811
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 19%

---

# Eventi di Analytics 2.0 in Assurance

Analytics Events 2.0 fornisce una visualizzazione più completa degli eventi SDK per gli utenti che eseguono il debug e la convalida dell’implementazione di Adobe Analytics. La visualizzazione mostra gli eventi inviati ad Adobe Analytics dal [SDK di Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/solution/adobe-analytics/) nonché [SDK di Adobe Experience Platform Edge Network](https://developer.adobe.com/client-sdks/edge/edge-network/). La vista dispone anche di un pannello dei dettagli che fornisce informazioni contestuali su come l’evento è stato elaborato dall’SDK client e dai servizi a monte dopo che ha lasciato il dispositivo.

## Introduzione

La procedura seguente illustra come utilizzare questa visualizzazione:

1. [Configurare Adobe Experience Platform Assurance](../tutorials/implement-assurance.md).
2. [Creare e connettersi a una sessione Assurance](../tutorials/using-assurance.md).
3. Nell’interfaccia utente Assurance dalla navigazione a sinistra **Home** menu visualizza, selezionare **Eventi di Analytics 2.0 (Beta)**. Se non trovi questa opzione, seleziona **Configura** in basso a sinistra nella finestra, aggiungi **Eventi di Analytics 2.0 (Beta)**, e seleziona **Salva**.

## Visualizzazione eventi di Analytics

Utilizza la Vista evento di Analytics se utilizzi il **Adobe Analytics** estensione per dispositivi mobili. Questa visualizzazione consente di visualizzare facilmente gli eventi di Analytics inviati dal client connesso, inclusi gli eventi Track Action, Track State e Lifecycle. Selezionando uno degli eventi di Analytics nella tabella, nel pannello di destra è possibile visualizzare i dettagli dell’elaborazione dell’evento.

![Immagine che illustra i diversi componenti nella visualizzazione Eventi di Analytics.](./images/adobe-analytics-edge/analytics-events.png)

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

- Un evento di richiesta dell’SDK di Analytics di origine.
- Metadati e dati contestuali della richiesta, come ID suite di rapporti, versioni dell’estensione SDK e dati contestuali.
- Informazioni post-elaborate sull’evento Analytics che contiene la mappatura di revar, evar e prop.

### Convalida visualizzazione Analytics

La vista di convalida consente di visualizzare facilmente i risultati sugli script di convalida relativi ad Analytics. Gli errori visualizzati dai validatori possono contenere collegamenti a dove devono essere corretti o visualizzare eventi in stato di errore.

![Immagine che mostra la scheda Convalida nella vista Analytics.](./images/adobe-analytics-edge/analytics-validation-view.png)

## Vista Edge di Analytics

Utilizza la vista Analytics Edge se utilizzi **Rete Edge** o **Bridge perimetrale** estensioni per dispositivi mobili. Per abilitare questa visualizzazione, seleziona l’interruttore &quot;Analytics Edge (Beta)&quot; in alto a destra per visualizzare gli eventi di Analytics inviati tramite rete Edge nella sessione corrente. Questo include tutti gli eventi che sono stati attivati dall’estensione del ciclo di vita, dalle richieste Edge e/o dagli eventi Edge Bridge basati su Track Action e Track State.

![Immagine che mostra l’interruttore utilizzato per passare dalla visualizzazione Analytics alla visualizzazione Edge di Analytics e viceversa.](./images/adobe-analytics-edge/analytics-view-toggle.png)

La vista Analytics Edge contiene informazioni sulle richieste Edge e i metodi del ciclo di vita relativi ad Analytics inviati dal client. Scegliendo un evento nell’elenco, il pannello di destra visualizza gli eventi elaborati dall’SDK del client e dal servizio a monte dopo che hanno lasciato il dispositivo, in modo da poter visualizzare facilmente la catena di eventi risultanti da una chiamata.

![Un’immagine che illustra diversi componenti nella vista Edge di Analytics.](./images/adobe-analytics-edge/edge-analytics-events.png)

### Convalida Analytics Edge

La vista di convalida di Analytics Edge consente di visualizzare facilmente i risultati sugli script di convalida relativi ad Analytics Edge. Gli errori visualizzati dai validatori possono contenere collegamenti a dove devono essere corretti o visualizzare eventi in stato di errore.

![Immagine che mostra la scheda Convalida nella vista Analytics Edge.](./images/adobe-analytics-edge/edge-analytics-validation-view.png)
