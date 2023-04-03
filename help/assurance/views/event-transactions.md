---
title: Visualizzazione transazioni evento
description: Questa guida fornisce informazioni dettagliate sulla vista Transazioni evento in Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---


# Vista Transazioni eventi

La visualizzazione Transazioni eventi in Adobe Experience Platform Assurance consente di convalidare ed eseguire il debug dell’implementazione client di Edge Network e di visualizzare i risultati della convalida a monte in tempo quasi reale.

## Imposta Assurance per il flusso di lavoro di Edge Network

Dopo [configurazione di Assurance](../tutorials/implement-assurance.md), assicurati di aver implementato le versioni più recenti delle estensioni Assurance e Edge Network nell’app.

Per visualizzare gli eventi, dal menu a sinistra seleziona **[!UICONTROL Transazioni evento]** in **[!UICONTROL Adobe Experience Platform Edge]** sezione .

Se questa opzione non viene visualizzata, seleziona **[!UICONTROL Configura]** in basso a sinistra della finestra, aggiungi la **[!UICONTROL Transazioni evento]** visualizza e seleziona **[!UICONTROL Salva]**.

## Introduzione alla vista Transazioni eventi

In questa sezione, acquisisci familiarità con la visualizzazione Transazione eventi e scopri come utilizzarla in modo efficiente per la convalida end to end sui flussi di lavoro di Edge Network.

### Flusso di elaborazione degli eventi

![Visualizzazione transazioni evento](./images/event-transactions/event-transactions-view.png)

Nella vista Transazioni eventi vengono visualizzate tre colonne nell’ordine del flusso di elaborazione dell’evento:

- **[!UICONTROL Lato client]**: In questa colonna vengono visualizzati gli eventi elaborati o ricevuti sul lato client, accessibili all’SDK di Mobile. Ciò include gli eventi creati utilizzando una chiamata API, ad esempio `Edge.sendEvent`, e gli eventuali handle dell&#39;evento di risposta ricevuti dal client dal server Edge Network. Esempi di eventi lato client:
   - AEP Request Event è l’evento inviato tramite l’estensione Edge e contiene i dati in formato libero XDM e facoltativi.
   - AEP Response Event Handle è l&#39;handle di evento ricevuto da Edge Network in risposta a un evento di richiesta AEP. Un evento di richiesta può ricevere handle di evento di risposta nessuno, uno o più.
   - La risposta di errore AEP può essere visualizzata in caso di errore, ad esempio se il payload XDM non può essere elaborato o se uno dei servizi a monte ha restituito un errore o un avviso.
- **[!UICONTROL Rete Edge]**: In questa colonna viene visualizzato l’evento ricevuto lato server da Edge Network tramite una richiesta di rete e quali dati e metadati contiene l’evento.
- **[!UICONTROL A monte]**: In questa colonna vengono visualizzati gli eventi ricevuti dai servizi a monte configurati, incluse informazioni dettagliate sui risultati di elaborazione e/o convalida dell&#39;evento in arrivo.
Tieni presente che questa colonna è dinamica e può mostrare diversi tipi di informazioni a seconda di due fattori principali:
   - La configurazione del datastream e i servizi su di esso abilitati.
   - Tipo di evento inviato alla rete Edge.

### Eventi Inspect

Gli eventi visualizzati nella visualizzazione Transazioni eventi forniscono informazioni sul formato e il contenuto dei dati elaborati in ogni stato, nonché dettagli approfonditi su eventuali avvisi o errori riscontrati durante l’elaborazione dei dati a monte. La visualizzazione aiuta a ridurre le informazioni di debug a livello di evento/richiesta e a identificare gli errori all’inizio del ciclo di sviluppo.

#### Espandi i dettagli dell’evento

Per ispezionare un evento, seleziona quello desiderato dalla visualizzazione. Questa azione espande la **[!UICONTROL Dettagli evento]** sul lato destro dello schermo.
I dati nidificati vengono visualizzati in un formato ad albero. Puoi controllare i valori chiave nidificati selezionando la **+** (più) a sinistra del nome della chiave.

![Dettagli evento](./images/event-transactions/event-details.png)

#### Avvisi o errori Inspect

Ogni nome dell’evento ha il prefisso di un’icona che indica lo stato di alto livello dell’elaborazione per quell’evento:

- Se l&#39;evento è stato elaborato correttamente, viene visualizzato un segno di spunta verde.
- Se sono stati rilevati avvisi o errori, viene visualizzato un segnale di avviso. Seleziona l’evento correlato per ulteriori informazioni sulla causa dell’avviso o dell’errore nel **[!UICONTROL Dettagli evento]** visualizza.

### Impostazioni di configurazione

Puoi controllare l&#39;identificatore del datastream attualmente utilizzato selezionando la descrizione comando accanto a **[!UICONTROL Rete Edge]** intestazione di colonna.

![Mostra l&#39;ID del datastream](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>Quando più client si connettono alla stessa sessione di Assurance e vengono utilizzati diversi ID di datastream, vengono visualizzati tutti qui. Tuttavia, questo non significa che l&#39;implementazione corrente utilizzi più datastreams. Solo l’ID del datastream corrente impostato nel tag (proprietà mobile) utilizzato dall’app viene utilizzato per elaborare nuovi eventi da quel client. Quando si sottopongono a test casi d’uso più complessi con diverse impostazioni di configurazione e più client collegati, può essere utile utilizzare sessioni di controllo separate per semplificare il processo di convalida.
