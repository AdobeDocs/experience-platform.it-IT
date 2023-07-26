---
title: Vista Transazioni evento
description: Questa guida contiene informazioni dettagliate sulla vista Transazioni evento in Adobe Experience Platform Assurance.
exl-id: ad97f2c1-5bbc-49e2-8378-edcb8af149a3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '695'
ht-degree: 100%

---

# Vista Transazioni evento

La vista Transazioni evento in Adobe Experience Platform Assurance consente di convalidare ed eseguire il debug dell’implementazione del client della rete Edge e di visualizzare i risultati della convalida a monte quasi in tempo reale.

## Imposta Assurance per il flusso di lavoro della rete Edge

Dopo [aver impostato Assurance](../tutorials/implement-assurance.md), accertati di aver implementato nell’app le versioni più recenti delle estensioni Assurance e rete Edge.

Per visualizzare i tuoi eventi, dal menu a sinistra seleziona **[!UICONTROL Transazioni evento]** nella sezione **[!UICONTROL Adobe Experience Platform Edge]**.

Se non trovi questa opzione, seleziona **[!UICONTROL Configura]** in basso a sinistra nella finestra, aggiungi la vista **[!UICONTROL Transazioni evento]** e seleziona **[!UICONTROL Salva]**.

## Introduzione all’utilizzo della vista Transazioni evento

In questa sezione, potrai acquisire familiarità con la vista Transazione evento e scoprire come utilizzarla in modo efficiente per la convalida end-to-end nei flussi di lavoro della rete Edge.

### Flusso di elaborazione degli eventi

![Vista Transazioni evento](./images/event-transactions/event-transactions-view.png)

Nella vista Transazioni evento vengono visualizzate tre colonne ordinati secondo il flusso di elaborazione degli eventi:

- **[!UICONTROL Lato client]**: questa colonna mostra gli eventi elaborati o ricevuti lato client, accessibili per l’SDK Mobile. Ciò include gli eventi creati utilizzando una chiamata API, come `Edge.sendEvent`, e gli eventuali handler di eventi di risposta ricevuti dal client dal server della rete Edge. Esempi di eventi lato client:
   - L’evento di richiesta AEP è l’evento inviato tramite l’estensione Edge che contiene i dati XDM e i dati in forma libera facoltativi.
   - La gestione evento di risposta AEP è la gestione dell’evento ricevuto dalla rete Edge in risposta a un evento di richiesta AEP. Un evento di richiesta può ricevere nessuno, uno o più handler di eventi di risposta.
   - La risposta di errore AEP può essere visualizzata in caso di errore, ad esempio se il payload XDM non può essere elaborato oppure se uno dei servizi a monte ha restituito un errore o un avviso.
- **[!UICONTROL Rete Edge]**: questa colonna mostra l’evento ricevuto lato server dalla rete Edge tramite una richiesta di rete e i dati e metadati contenuti nell’evento.
- **[!UICONTROL Upstream]**: in questa colonna vengono visualizzati gli eventi ricevuti dai servizi a monte configurati, incluse informazioni dettagliate sull’elaborazione e/o sui risultati della convalida per l’evento in arrivo.
Tieni presente che questa colonna è dinamica e può mostrare diversi tipi di informazioni a seconda di due fattori principali:
   - La configurazione dello stream di dati e i servizi in esso abilitati.
   - Il tipo di evento inviato alla rete Edge.

### Esamina eventi

Gli eventi visualizzati nella vista Transazioni evento forniscono informazioni sul formato e il contenuto dei dati elaborati in ogni stato, nonché dettagli approfonditi su eventuali avvisi o errori rilevati durante l’elaborazione dei dati a monte. La vista consente di ridurre le informazioni di debug a livello di evento/richiesta e di identificare gli errori nelle prime fasi del ciclo di sviluppo.

#### Espandi i dettagli dell’evento

Per esaminare un evento, seleziona quello desiderato dalla vista. Questa azione espande la vista **[!UICONTROL Dettagli evento]** sul lato destro dello schermo.
I dati nidificati vengono visualizzati in una struttura ad albero. Puoi esaminare i valori chiave nidificati selezionando il pulsante **+** (più) a sinistra del nome del tasto.

![Dettagli evento](./images/event-transactions/event-details.png)

#### Esamina avvisi o errori

A ogni nome dell’evento viene anteposta un’icona che indica lo stato di alto livello dell’elaborazione di quell’evento:

- Se l’evento è stato elaborato correttamente, viene visualizzato un segno di spunta verde.
- Se sono stati rilevati avvisi o errori, viene visualizzato un segnale di avviso. Seleziona l’evento correlato per ulteriori informazioni sulla causa dell’avviso o dell’errore nella vista **[!UICONTROL Dettagli evento]**.

### Impostazioni di configurazione

Per controllare l’identificatore dello stream di dati attualmente utilizzato, seleziona il suggerimento informativo accanto all’intestazione di colonna **[!UICONTROL Rete Edge]**.

![Mostra l’ID dello stream di dati](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>Quando più client si connettono alla stessa sessione di Assurance e vengono utilizzati diversi ID dello stream di dati, vengono visualizzati tutti qui. Tuttavia, questo non significa che l’implementazione corrente stia utilizzando più stream di dati. Solo l’ID dello stream di dati corrente impostato nel tag (proprietà mobile) utilizzato dall’app viene utilizzato per l’elaborazione di nuovi eventi da tale client. Quando si sottopongono a test casi d’uso più complessi con impostazioni di configurazione diverse e più client connessi, può essere utile utilizzare sessioni di Assurance separate per semplificare il processo di convalida.
