---
description: Scopri come monitorare i flussi di dati per le destinazioni utilizzando l’interfaccia utente di Experience Platform.
solution: Experience Platform
title: Monitorare i flussi di dati per le destinazioni nell’interfaccia utente
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 25dc27d890cb2e0e23f8fa797ac9edea929164fd
workflow-type: tm+mt
source-wordcount: '3639'
ht-degree: 9%

---

# Monitorare i flussi di dati per le destinazioni nell’interfaccia utente

Utilizza le varie destinazioni nel catalogo di Experienci Platform per attivare i tuoi dati da Platform a innumerevoli partner esterni. Platform semplifica il processo di tracciamento del flusso di dati nelle destinazioni fornendo trasparenza con i flussi di dati.

La dashboard di monitoraggio offre una rappresentazione visiva del percorso di un flusso di dati, inclusa la destinazione in cui vengono attivati i dati, il tipo di dati che stai visualizzando, i dati esportati per ogni esecuzione del flusso di dati e molto altro.

Questa esercitazione fornisce istruzioni su come monitorare i flussi di dati direttamente nell’area di lavoro delle destinazioni o utilizzare il dashboard di monitoraggio per monitorare i flussi di dati per le destinazioni utilizzando l’interfaccia utente di Experience Platform.

## Introduzione {#getting-started}

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Flussi dati](../home.md): i flussi dati sono una rappresentazione dei processi di dati che spostano i dati in Platform. I flussi di dati sono configurati tra servizi diversi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, a [!DNL Identity] e [!DNL Profile] e a [!DNL Destinations].
   - [Esecuzioni flusso di dati](../../sources/notifications.md): le esecuzioni del flusso di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
- [Destinazioni](../../destinations/home.md): le destinazioni sono integrazioni predefinite con applicazioni di uso comune che consentono l&#39;attivazione diretta dei dati da Platform per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d&#39;uso.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Monitorare i flussi di dati nell’area di lavoro Destinazioni {#monitor-dataflows-in-the-destinations-workspace}

Nell&#39;area di lavoro **[!UICONTROL Destinazioni]** nell&#39;interfaccia utente di Platform, passa alla scheda **[!UICONTROL Sfoglia]** e seleziona il nome di una destinazione da visualizzare.

![Selezionare la vista di destinazione con una connessione di destinazione evidenziata](../assets/ui/monitor-destinations/select-destination.png)

Viene visualizzato un elenco dei flussi di dati esistenti. In questa pagina è riportato un elenco di flussi di dati visualizzabili, con informazioni sulla destinazione, il nome utente, il numero di flussi di dati e lo stato.

Per ulteriori informazioni sugli stati, consulta la tabella seguente:

| Stato | Descrizione |
| ------ | ----------- |
| Abilitata | Lo stato `Enabled` indica che un flusso di dati è attivo ed esporta i dati in base alla pianificazione fornita. |
| Disabilitata | Lo stato `Disabled` indica che un flusso di dati è inattivo e non esporta alcun dato. |
| Elaborazione | Lo stato `Processing` indica che un flusso di dati non è ancora attivo. Questo stato si verifica spesso subito dopo la creazione di un nuovo flusso di dati. |
| Errore | Lo stato `Error` indica che il processo di attivazione di un flusso di dati è stato interrotto. |

### Esecuzioni del flusso di dati per le destinazioni di streaming {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="Dettagli dell’esecuzione del flusso di dati"
>abstract="I dettagli di esecuzione del flusso di dati di destinazione contengono informazioni sullo stato di attivazione di un pubblico e metriche estratte dal Profilo cliente in tempo reale per generare identità univoche. Per ulteriori informazioni, rivedi la guida alle definizioni delle metriche."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="Profili ricevuti"
>abstract="Numero totale di profili ricevuti nel flusso di dati. Questo valore viene aggiornato ogni 60 minuti."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="Identità attivate"
>abstract="Conteggio delle singole identità di profilo attivate correttamente nella destinazione selezionata. Questa metrica include le identità create, aggiornate e rimosse dai tipi di pubblico esportati."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="Identità escluse"
>abstract="Conteggio dei singoli record di profilo esclusi dall’attivazione per la destinazione selezionata in base agli attributi mancanti e alla violazione del consenso."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="Identità non riuscite"
>abstract="Conteggio delle singole identità di profilo non riuscite per la destinazione selezionata. Per informazioni, controlla la diagnostica degli errori."

Per le destinazioni di streaming, la scheda [!UICONTROL Esecuzioni flusso di dati] fornisce un aggiornamento orario per i dati delle metriche sulle esecuzioni del flusso di dati. Le statistiche più importanti etichettate sono per le identità.

Le identità rappresentano i diversi facet di un profilo. Ad esempio, se un profilo contiene sia un numero di telefono che un indirizzo e-mail, tale profilo ha due identità.

Viene visualizzato un elenco di singole esecuzioni e delle relative metriche specifiche, insieme ai seguenti totali per le identità:

- **[!UICONTROL Identità attivate]**: numero totale di identità di profilo attivate correttamente nella destinazione selezionata. Questa metrica include le identità create, aggiornate e rimosse dai tipi di pubblico esportati.
- **[!UICONTROL Identità escluse]**: numero totale di identità di profilo ignorate per l&#39;attivazione in base ad attributi mancanti e violazioni del consenso.
- **[!UICONTROL Identità non riuscite]**: numero totale di identità di profilo non attivate nella destinazione a causa di errori.

![Il flusso di dati esegue i dettagli per le destinazioni di streaming.](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Ogni singola esecuzione del flusso di dati mostra i seguenti dettagli:

- **[!UICONTROL Inizio esecuzione flusso di dati]**: ora di inizio dell&#39;esecuzione del flusso di dati. Per le esecuzioni di flussi di dati in streaming, Experience Platform acquisisce metriche basate sull’inizio dell’esecuzione del flusso di dati, sotto forma di metriche orarie. Ciò significa che per l’esecuzione del flusso di dati in streaming, se un flusso di dati viene avviato, ad esempio, alle 22:30, la metrica mostra l’ora di inizio come 22:00 nell’interfaccia utente.
- **[!UICONTROL Tempo di elaborazione]**: tempo necessario all&#39;elaborazione del flusso di dati.
   - Per le esecuzioni di **[!UICONTROL completed]**, la metrica del tempo di elaborazione mostra sempre un&#39;ora.
   - Per le esecuzioni di flussi di dati che si trovano ancora in uno stato di **[!UICONTROL elaborazione]**, la finestra per acquisire tutte le metriche rimane aperta per più di un&#39;ora, per elaborare tutte le metriche che corrispondono all&#39;esecuzione del flusso di dati. Ad esempio, un’esecuzione di un flusso di dati avviata alle 09:30 potrebbe rimanere in uno stato di elaborazione per un’ora e trenta minuti per acquisire ed elaborare tutte le metriche. Quindi, una volta che la finestra di elaborazione si chiude e lo stato dell&#39;esecuzione del flusso di dati diventa **completato**, il tempo di elaborazione visualizzato viene modificato in un&#39;ora.
- **[!UICONTROL Profili ricevuti]**: numero totale di profili ricevuti nel flusso di dati.
- **[!UICONTROL Identità attivate]**: numero totale di identità di profilo attivate correttamente nella destinazione selezionata durante l&#39;esecuzione del flusso di dati. Questa metrica include le identità create, aggiornate e rimosse dai tipi di pubblico esportati.
- **[!UICONTROL Identità escluse]**: numero totale di identità di profilo escluse dall&#39;attivazione in base ad attributi mancanti e alla violazione del consenso.
- **[!UICONTROL Identità non riuscite]** Il numero totale di identità di profilo non attivate nella destinazione a causa di errori.

  >[!IMPORTANT]
  >
  > A partire da ottobre 2024, Adobe sta implementando un aggiornamento per aumentare la precisione dei rapporti per le destinazioni di streaming. Questo miglioramento garantisce un migliore allineamento tra il reporting dell’Experience Platform e quello delle piattaforme di destinazione.
  >
  > Prima di questo aggiornamento, **[!UICONTROL Identità non riuscite]** includeva tutti i tentativi di attivazione. Dopo questo aggiornamento, nel conteggio totale viene incluso solo l’ultimo tentativo di attivazione.
  > 
  > Questo miglioramento si applica attualmente alla [destinazione Customer Match di Google](../../destinations/catalog/advertising/google-customer-match.md), ma verrà introdotto gradualmente in altre destinazioni di streaming di Experienci Platform.
  > In seguito a questo miglioramento, gli utenti della [destinazione Customer Match di Google](../../destinations/catalog/advertising/google-customer-match.md) potrebbero notare un calo previsto nel conteggio di **[!UICONTROL Identità non riuscite]**.


- **[!UICONTROL Tasso di attivazione]**: percentuale di identità ricevute attivate o ignorate. La formula seguente illustra come viene calcolato questo valore:
  ![Formula del tasso di attivazione.](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Stato]**: rappresenta lo stato in cui si trova il flusso di dati: [!UICONTROL Completato] o [!UICONTROL Elaborazione]. [!UICONTROL Completato] significa che tutte le identità per l&#39;esecuzione del flusso di dati corrispondente sono state esportate entro il periodo di un&#39;ora. [!UICONTROL Elaborazione] indica che l&#39;esecuzione del flusso di dati non è ancora terminata.

Per visualizzare i dettagli di una particolare esecuzione del flusso di dati, seleziona l’ora di inizio dell’esecuzione dall’elenco.

La pagina dei dettagli per un’esecuzione del flusso di dati contiene informazioni aggiuntive, ad esempio il numero di profili ricevuti, il numero di identità attivate, il numero di identità non riuscite e il numero di identità escluse.

![Dettagli del flusso di dati per le destinazioni di streaming.](../assets/ui/monitor-destinations/dataflow-details-stream.png)

Nella pagina dei dettagli viene inoltre visualizzato un elenco di identità con errori e di identità escluse. Vengono visualizzate informazioni sia per le identità non riuscite che per quelle escluse, inclusi il codice di errore, il conteggio delle identità e la descrizione. Per impostazione predefinita, nell’elenco vengono visualizzate le identità con errori. Per visualizzare le identità ignorate, seleziona l&#39;opzione **[!UICONTROL Identità escluse]**.

![Record di flusso di dati per le destinazioni di streaming con un messaggio di errore evidenziato.](../assets/ui/monitor-destinations/dataflow-records-stream.png)

#### (Beta) Monitoraggio dell’esecuzione dei flussi di dati a livello di pubblico per le destinazioni di streaming {#audience-level-dataflow-runs-for-streaming-destinations}

Puoi visualizzare informazioni sulle identità attivate, escluse o non riuscite suddivise a livello di pubblico, per ogni pubblico che fa parte del flusso di dati. Il monitoraggio a livello di pubblico per le destinazioni di streaming è attualmente disponibile solo per la [[!DNL Google Customer Match + Display & Video 360] destinazione](/help/destinations/catalog/advertising/google-customer-match-dv360.md).

![Monitoraggio a livello di pubblico per le destinazioni di streaming.](/help/dataflows/assets/ui/monitor-destinations/audience-level-monitoring-streaming.png)

>[!NOTE]
>
>Il numero di **[!UICONTROL profili ricevuti]** nella scheda **[!UICONTROL Tipi di pubblico]** potrebbe non corrispondere sempre al numero di profili ricevuti per l&#39;esecuzione del flusso di dati. Questo perché un dato profilo potrebbe far parte di più tipi di pubblico attivati nell’esecuzione del flusso di dati.

### Il flusso di dati viene eseguito per le destinazioni di batch {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="Dettagli dell’esecuzione del flusso di dati"
>abstract="I dettagli di esecuzione del flusso di dati di destinazione contengono informazioni sullo stato di attivazione di un pubblico e metriche estratte dal Profilo cliente in tempo reale per generare identità univoche. Per ulteriori informazioni, rivedi la guida alle definizioni delle metriche."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html?lang=it#dataflow-runs-for-streaming-destinations" text="Esecuzioni del flusso di dati per le destinazioni di streaming"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="Profili ricevuti"
>abstract="Numero totale di profili ricevuti nel flusso di dati. Questo valore viene aggiornato ogni 60 minuti."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="Identità attivate"
>abstract="Conteggio delle singole identità di profilo attivate correttamente nella destinazione selezionata. Questa metrica include le identità create, aggiornate e rimosse dai tipi di pubblico esportati."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="Identità escluse"
>abstract="Conteggio dei singoli record di profilo esclusi dall’attivazione per la destinazione selezionata in base agli attributi mancanti e alla violazione del consenso."

Per le destinazioni batch, la scheda [!UICONTROL Flussi di dati in esecuzione] fornisce i dati delle metriche sulle esecuzioni dei flussi di dati. Viene visualizzato un elenco di singole esecuzioni e delle relative metriche specifiche, insieme ai seguenti totali per le identità:

- **[!UICONTROL Identità attivate]**: numero totale di identità di profilo attivate correttamente nella destinazione selezionata. Questa metrica include le identità create, aggiornate e rimosse dai tipi di pubblico esportati.
- **[!UICONTROL Identità escluse]**: il conteggio delle singole identità di profilo escluse dall&#39;attivazione per la destinazione selezionata, in base agli attributi mancanti e alla violazione del consenso.

![Il flusso di dati esegue la visualizzazione per le destinazioni batch.](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Ogni singola esecuzione del flusso di dati mostra i seguenti dettagli:

- **[!UICONTROL Inizio esecuzione flusso di dati]**: ora di inizio dell&#39;esecuzione del flusso di dati.
- **[!UICONTROL Pubblico]**: il nome del pubblico associato a ogni esecuzione del flusso di dati.
- **[!UICONTROL Tempo di elaborazione]**: tempo necessario per l&#39;elaborazione del flusso di dati.
- **[!UICONTROL Profili ricevuti]**: numero totale di profili ricevuti nel flusso di dati. Questo valore viene aggiornato ogni 60 minuti.
- **[!UICONTROL Identità attivate]**: numero totale di identità di profilo attivate correttamente nella destinazione selezionata durante l&#39;esecuzione del flusso di dati. Questa metrica include le identità create, aggiornate e rimosse dai tipi di pubblico esportati.
- **[!UICONTROL Identità escluse]**: numero totale di identità di profilo escluse dall&#39;attivazione in base ad attributi mancanti e alla violazione del consenso.
- **[!UICONTROL Stato]**: rappresenta lo stato del flusso di dati. Può essere uno dei tre stati seguenti: [!UICONTROL Operazione completata], [!UICONTROL Operazione non riuscita] e [!UICONTROL Elaborazione]. [!UICONTROL Operazione completata] significa che il flusso di dati è attivo ed esporta i dati in base alla pianificazione specificata. [!UICONTROL Non riuscito] significa che l&#39;attivazione dei dati è stata sospesa a causa di errori. [!UICONTROL Elaborazione] significa che il flusso di dati non è ancora attivo e si verifica generalmente durante la creazione di un nuovo flusso di dati.

Per visualizzare i dettagli di un’esecuzione specifica del flusso di dati, seleziona l’ora di inizio dell’esecuzione dall’elenco.

>[!NOTE]
>
>Le esecuzioni del flusso di dati vengono generate in base alla frequenza di pianificazione del flusso di dati di destinazione. Viene eseguito un flusso di dati separato per ogni [criterio di unione](../../profile/merge-policies/overview.md) applicato a un pubblico.

La pagina dei dettagli di un flusso di dati, oltre ai dettagli riportati nell’elenco dei flussi di dati, visualizza informazioni più specifiche su di esso:

- **[!UICONTROL Dimensione dei dati]**: dimensione del flusso di dati in fase di esportazione.
- **[!UICONTROL File totali]**: numero totale di file esportati nel flusso di dati.
- **[!UICONTROL Ultimo aggiornamento]**: ora dell&#39;ultimo aggiornamento del flusso di dati.

![Dettagli di esecuzione del flusso di dati per le destinazioni batch.](../assets/ui/monitor-destinations/dataflow-batch.png)

Nella pagina dei dettagli viene inoltre visualizzato un elenco di identità con errori e di identità escluse. Vengono visualizzate le informazioni sia per le identità non riuscite che per quelle escluse, inclusi il codice di errore e la descrizione. Per impostazione predefinita, nell’elenco vengono visualizzate le identità con errori. Per visualizzare le identità escluse, seleziona l&#39;opzione **[!UICONTROL Identità escluse]**.

![Record di flusso di dati per destinazioni batch con un messaggio di errore evidenziato.](../assets/ui/monitor-destinations/dataflow-records-batch.png)

### Visualizza nel monitoraggio {#view-in-monitoring}

Puoi anche scegliere di visualizzare informazioni dettagliate su un determinato flusso di dati e il relativo flusso di dati viene eseguito nel dashboard di monitoraggio. Per visualizzare informazioni su un flusso di dati nel dashboard di monitoraggio:

1. Passa a **[!UICONTROL Connessioni]** > **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** scheda
2. Passa al flusso di dati che desideri ispezionare.
3. Seleziona il simbolo di puntini di sospensione e l&#39;![icona di monitoraggio](/help/images/icons/monitoring.png) **[!UICONTROL Visualizza nel monitoraggio]**.

![Per ottenere ulteriori informazioni su un flusso di dati, seleziona Visualizza nel monitoraggio nel flusso di lavoro delle destinazioni.](/help/dataflows/assets/ui/monitor-destinations/view-in-monitoring.png)

>[!SUCCESS]
>
>Ora puoi visualizzare le informazioni sul flusso di dati e sul flusso di dati associato che viene eseguito nel dashboard di monitoraggio. Per ulteriori informazioni, consulta la sezione seguente.

## Dashboard di monitoraggio delle destinazioni {#monitoring-destinations-dashboard}

>[!NOTE]
>
>La funzionalità di monitoraggio delle destinazioni è attualmente supportata per tutte le destinazioni nell&#39;Experience Platform *eccetto* le destinazioni [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) e [Personalizzazione personalizzata](/help/destinations/catalog/personalization/custom-personalization.md).

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Activation"
>abstract="La vista Attivazione della destinazione contiene informazioni sullo stato di attivazione di un pubblico e metriche prelevate dal profilo cliente in tempo reale per generare identità univoche."

Per accedere al dashboard [!UICONTROL Monitoraggio], seleziona **[!UICONTROL Monitoraggio]** (![icona monitoraggio](/help/images/icons/monitoring.png)) nel menu di navigazione a sinistra. Nella pagina [!UICONTROL Monitoraggio], seleziona [!UICONTROL Destinazioni]. Il dashboard [!UICONTROL Monitoraggio] contiene metriche e informazioni sui processi di esecuzione di destinazione.

Utilizza il dashboard [!UICONTROL Destinazioni] per avere un&#39;idea generale dello stato dei flussi di attivazione. Inizia ottenendo informazioni su un livello aggregato per tutte le destinazioni di batch e streaming, quindi approfondisci le viste dettagliate per i flussi di dati, le esecuzioni dei flussi di dati e i tipi di pubblico attivati, per una panoramica approfondita dei dati di attivazione. Le schermate nel dashboard [!UICONTROL Monitoraggio] forniscono informazioni fruibili tramite metriche e descrizioni degli errori per aiutarti a risolvere eventuali problemi che potrebbero verificarsi negli scenari di attivazione.

Puoi filtrare le informazioni visualizzate per tipo di dati: clienti, account (solo per Adobe Real-Time CDP B2B edition), potenziali clienti e arricchimento dell’account. Ulteriori informazioni su queste opzioni sono disponibili nella [guida del dashboard di monitoraggio](/help/dataflows/ui/monitor.md#monitoring-dashboard-overview).

![Filtro del tipo di dati evidenziato nella visualizzazione del dashboard di monitoraggio.](/help/dataflows/assets/ui/monitor-destinations/add-data-filter.png)

Al centro del dashboard si trova il pannello [!UICONTROL Activation], che contiene metriche e grafici che visualizzano i dati sulla velocità di attivazione dei dati esportati nelle destinazioni di streaming, nonché sul flusso di dati batch non riuscito eseguito nelle destinazioni batch.

![Grafici di streaming e attivazione batch evidenziati nella visualizzazione di monitoraggio.](../assets/ui/monitor-destinations/dashboard-graph.png)


Per impostazione predefinita, i dati visualizzati contengono le informazioni di attivazione delle ultime 24 ore. Seleziona **[!UICONTROL Ultime 24 ore]** per regolare l&#39;intervallo di tempo dei record visualizzati. Le opzioni disponibili includono **[!UICONTROL Ultime 24 ore]**, **[!UICONTROL Ultimi 7 giorni]** e **[!UICONTROL Ultimi 30 giorni]**. In alternativa, è possibile selezionare le date nella finestra a comparsa del calendario visualizzata. Dopo aver selezionato le date, selezionare **[!UICONTROL Applica]** per modificare l&#39;intervallo di tempo delle informazioni visualizzate.

>[!NOTE]
>
>La schermata seguente mostra il tasso di attivazione e il flusso di dati batch eseguiti per gli ultimi 30 giorni invece delle ultime 24 ore. È possibile modificare l&#39;intervallo di tempo selezionando **[!UICONTROL Ultimi 30 giorni]**.

![Controllo dell&#39;intervallo di date di lookback delle modifiche evidenziato per le destinazioni attivate](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Utilizza l&#39;icona freccia (![icona freccia](/help/images/icons/chevron-up.png)) per espandere o chiudere le schede nella parte superiore dello schermo, che mostrano immediatamente informazioni sui dettagli di attivazione, in base al tipo di destinazione - streaming o batch:

- **[!UICONTROL Frequenza di attivazione streaming]**: rappresenta la percentuale di identità ricevute attivate o ignorate correttamente. La formula utilizzata per calcolare questa percentuale è descritta più avanti in questa pagina, nella sezione [Esecuzioni del flusso di dati per le destinazioni di streaming](#dataflow-runs-for-streaming-destinations).
- **[!UICONTROL Il flusso di dati batch non riuscito viene eseguito]**: rappresenta il numero di esecuzioni del flusso di dati non riuscite nell&#39;intervallo di tempo selezionato.

![Mostra o rimuovi le schede all&#39;inizio della pagina.](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

Il grafico **[!UICONTROL Activation]** viene visualizzato per impostazione predefinita ed è possibile disattivarlo per espandere l&#39;elenco di destinazioni di seguito. Seleziona l&#39;interruttore **[!UICONTROL Metriche e grafici]** per disabilitare i grafici.

Il pannello **[!UICONTROL Activation]** visualizza un elenco di destinazioni che contengono almeno un account esistente. Questo elenco include anche informazioni sui profili ricevuti, identità attivate, identità non riuscite, identità escluse, tasso di attivazione, flussi di dati totali non riusciti e la data dell’ultimo aggiornamento per queste destinazioni. Non tutte le metriche sono disponibili per tutti i tipi di destinazione. La tabella seguente illustra le metriche e le informazioni disponibili per tipo di destinazione.

| Metrica | Tipo di destinazione |
|--------------------------------------|-----------------------|
| **[!UICONTROL Record ricevuti]** | Streaming e batch |
| **[!UICONTROL Record attivati]** | Streaming e batch |
| **[!UICONTROL Record non riusciti]** | Streaming |
| **[!UICONTROL Record ignorati]** | Streaming e batch |
| **[!UICONTROL Tipo di dati]** | Streaming e batch |
| **[!UICONTROL Tasso di attivazione]** | Streaming |
| **[!UICONTROL Totale flussi di dati non riusciti]** | Batch |
| **[!UICONTROL Ultimo aggiornamento]** | Streaming e batch |

{style="table-layout:auto"}

![Dashboard di monitoraggio con tutte le destinazioni attivate evidenziate.](../assets/ui/monitor-destinations/dashboard-destinations.png)

Puoi anche filtrare l’elenco delle destinazioni per visualizzare solo la categoria di destinazioni selezionata. Seleziona il menu a discesa **[!UICONTROL Destinazioni personali]** e la [categoria di destinazione](/help/destinations/destination-types.md#categories) a cui vuoi filtrare.

![Filtra le destinazioni tramite il selettore a discesa](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

Inoltre, puoi immettere una destinazione nella barra di ricerca per isolarla in una singola destinazione. Se desideri visualizzare i flussi di dati della destinazione, puoi selezionare il filtro ![filter](/help/images/icons/filter-add.png) accanto per visualizzare un elenco dei relativi flussi di dati attivi.

![Filtra le destinazioni utilizzando la barra di ricerca evidenziata nella visualizzazione di monitoraggio.](../assets/ui/monitor-destinations/filtered-destinations.png)

Se desideri visualizzare tutti i flussi di dati esistenti in tutte le destinazioni, seleziona **[!UICONTROL Flussi di dati]**.

Viene visualizzato un elenco di flussi di dati, ordinati in base all’ultima esecuzione del flusso di dati. Per visualizzare ulteriori dettagli per un flusso di dati specifico, individua la destinazione da monitorare, seleziona il filtro ![filter](/help/images/icons/filter-add.png) accanto e quindi seleziona il filtro ![filter](/help/images/icons/filter-add.png) accanto al flusso di dati di cui desideri ulteriori informazioni.

![Tutti i flussi di dati sono evidenziati nel dashboard di monitoraggio.](../assets/ui/monitor-destinations/dashboard-dataflows.png)

Dopo aver selezionato un flusso di dati per un’ulteriore ispezione, la pagina dei dettagli del flusso di dati contiene un interruttore che consente di visualizzare i dati attivati nel flusso di dati, suddivisi per esecuzioni di flussi di dati o tipi di pubblico.

### Visualizzazione esecuzioni flusso di dati {#dataflow-runs-view}

Quando viene selezionato **[!UICONTROL Flusso di dati]**, è possibile visualizzare un elenco di flussi di dati eseguiti per il flusso di dati selezionato e ulteriori informazioni su ciascuna esecuzione.

>[!INFO]
>
>Per i flussi di dati verso le destinazioni di streaming, un’esecuzione dei flussi di dati viene suddivisa in finestre orarie. Ogni finestra oraria genera un ID esecuzione flusso di dati corrispondente.
>
>Per i flussi di dati verso destinazioni batch, ogni pubblico ha una corrispondente esecuzione di flusso di dati generata, in base alla frequenza pianificata di attivazione del pubblico. Ad esempio, se imposti un’attivazione pianificata giornaliera per cinque tipi di pubblico nello stesso flusso di dati di destinazione, ogni giorno verranno generati cinque flussi di dati separati.

![Il flusso di dati esegue il pannello evidenziando diverse esecuzioni.](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

Utilizza l&#39;interruttore **[!UICONTROL Mostra solo errori]** per visualizzare solo le esecuzioni non riuscite per un flusso di dati.

![Il flusso di dati esegue la visualizzazione con l&#39;opzione Mostra errori evidenziata](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### Visualizzazione a livello di pubblico {#segment-level-view}

Quando **[!UICONTROL Tipi di pubblico]** è selezionato, viene visualizzato un elenco dei tipi di pubblico attivati nel flusso di dati selezionato, all&#39;interno dell&#39;intervallo di tempo selezionato. Questa schermata include informazioni a livello di pubblico sui record attivati, sui record esclusi, nonché sullo stato e sull’ora dell’ultima esecuzione del flusso di dati. Esaminando le metriche per i record esclusi e attivati, puoi verificare se un pubblico è stato attivato correttamente o meno.

Ad esempio, stai attivando un pubblico denominato &quot;Membri fedeltà in California&quot; in una destinazione Amazon S3 &quot;Membri fedeltà California December&quot;. Supponiamo che nel pubblico selezionato siano presenti 100 profili, ma solo 80 record su 100 contengono gli attributi dell&#39;ID fedeltà e che le regole di mappatura dell&#39;esportazione siano state definite come `loyalty.id` obbligatorie. In questo caso, a livello di pubblico, vedrai 80 record attivati e 20 record esclusi.

>[!IMPORTANT]
>
>Tieni presente le limitazioni correnti relative alle metriche a livello di pubblico:
>- La visualizzazione a livello di pubblico è attualmente disponibile solo per le destinazioni batch (basate su file) e per la destinazione di streaming [Google Customer Match DV 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md). Il rollout è pianificato per ulteriori destinazioni di streaming.
>- Per le destinazioni batch, le metriche a livello di pubblico sono attualmente registrate solo per l’esecuzione corretta del flusso di dati. Non vengono registrati per le esecuzioni dei flussi di dati non riuscite e i record esclusi. Per l’esecuzione del flusso di dati su destinazioni di streaming, le metriche vengono acquisite e visualizzate per i record attivati ed esclusi.

![Tipi di pubblico evidenziati nel pannello del flusso di dati.](../assets/ui/monitor-destinations/dashboard-segments-view.png)

Nella vista a livello di pubblico, le metriche sono aggregate tra più flussi di dati eseguiti all’interno dell’intervallo di tempo selezionato. In presenza di più esecuzioni del flusso di dati, puoi approfondire la ricerca dal livello di pubblico per visualizzare il raggruppamento di ogni esecuzione del flusso di dati, filtrato in base al pubblico selezionato.
Utilizza il pulsante filtro ![filter](/help/images/icons/filter-add.png) per analizzare in profondità il flusso di dati e la visualizzazione eseguita per ogni pubblico nel flusso di dati.

### Pagina di esecuzione del flusso di dati {#dataflow-runs-page}

La pagina Esecuzioni flusso di dati visualizza informazioni sulle esecuzioni del flusso di dati, tra cui l’ora di inizio dell’esecuzione del flusso di dati, il tempo di elaborazione, i record ricevuti, i record attivati, i record esclusi, i record con errore, il tasso di attivazione e lo stato.

Quando esegui il drill-down nella pagina del flusso di dati dalla [visualizzazione a livello di pubblico](#segment-level-view), puoi filtrare il flusso di dati eseguito in base alle seguenti opzioni:

- **[!UICONTROL Il flusso di dati viene eseguito con record non riusciti]**: per il pubblico selezionato, questa opzione elenca tutte le esecuzioni del flusso di dati non riuscite per l&#39;attivazione. Per verificare il motivo per cui i record in una determinata esecuzione del flusso di dati non sono riusciti, vedere la [pagina dei dettagli di esecuzione del flusso di dati](#dataflow-run-details-page) per tale esecuzione.
- **[!UICONTROL Il flusso di dati viene eseguito con record esclusi]**: per il pubblico selezionato, questa opzione elenca tutte le esecuzioni del flusso di dati in cui alcuni record non sono stati completamente attivati e alcuni profili sono stati saltati. Per verificare il motivo per cui i record in una determinata esecuzione del flusso di dati sono stati ignorati, vedere la [pagina dei dettagli dell&#39;esecuzione del flusso di dati](#dataflow-run-details-page) per tale esecuzione.
- **[!UICONTROL Il flusso di dati viene eseguito con record attivati]**: per il pubblico selezionato, questa opzione elenca tutte le esecuzioni del flusso di dati con record attivati correttamente.

![Pulsanti di opzione che mostrano come filtrare il flusso di dati per i tipi di pubblico.](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

Per visualizzare ulteriori dettagli su un&#39;esecuzione specifica del flusso di dati, seleziona il filtro ![filter](/help/images/icons/filter-add.png) accanto all&#39;ora di inizio dell&#39;esecuzione del flusso di dati per visualizzare la pagina dei dettagli dell&#39;esecuzione del flusso di dati.

![Il flusso di dati esegue il filtro nel dashboard di monitoraggio per eseguire il drill-in di ulteriori informazioni per una determinata esecuzione del flusso di dati.](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### Pagina dei dettagli dell’esecuzione del flusso di dati {#dataflow-run-details-page}

La pagina dei dettagli di esecuzione del flusso di dati, oltre ai dettagli riportati nell’elenco dei flussi di dati eseguiti, visualizza informazioni più specifiche sul flusso di dati:

- **[!UICONTROL ID esecuzione flusso di dati]**: ID del flusso di dati.
- **[!UICONTROL ID organizzazione IMS]**: organizzazione a cui appartiene il flusso di dati.
- **[!UICONTROL Ultimo aggiornamento]**: ora dell&#39;ultimo aggiornamento del flusso di dati.

La pagina dei dettagli dispone anche di un interruttore per passare dagli errori di esecuzione del flusso di dati ai tipi di pubblico e viceversa. Questa opzione è disponibile solo per il flusso di dati eseguito in destinazioni batch e per la destinazione di streaming [Google Customer Match DV 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md).

Nella visualizzazione errori di esecuzione del flusso di dati viene visualizzato un elenco di record con errori e di record ignorati. Vengono visualizzate informazioni sia per i record con errori che per quelli ignorati, inclusi il codice di errore, il conteggio delle identità e la descrizione. Per impostazione predefinita, nell&#39;elenco vengono visualizzati i record con errori. Per visualizzare i record ignorati, selezionare l&#39;opzione **[!UICONTROL Record ignorati]**.

![Le identità escluse vengono evidenziate nella visualizzazione di monitoraggio](../assets/ui/monitor-destinations/identities-excluded.png)

Quando **[!UICONTROL Tipi di pubblico]** è selezionato, viene visualizzato un elenco dei tipi di pubblico attivati nell&#39;esecuzione del flusso di dati selezionato. Questa schermata include informazioni a livello di pubblico sui record attivati, sui record esclusi, nonché sullo stato e sull’ora dell’ultima esecuzione del flusso di dati.

![Visualizzazione tipi di pubblico nella schermata dei dettagli di esecuzione del flusso di dati.](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## Passaggi successivi {#next-steps}

Seguendo questa guida, ora sai come monitorare i flussi di dati sia per le destinazioni batch che per quelle in streaming, incluse tutte le informazioni rilevanti come il tempo di elaborazione, il tasso di attivazione e lo stato. Per ulteriori informazioni sui flussi di dati in Platform, consulta la [panoramica sui flussi di dati](../home.md). Per ulteriori informazioni sulle destinazioni, leggere la [panoramica sulle destinazioni](../../destinations/home.md).