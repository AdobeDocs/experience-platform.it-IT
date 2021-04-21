---
keywords: Experience Platform;insights;attribution ai;argomenti popolari;approfondimenti di attribuzione ai
solution: Intelligent Services, Experience Platform
title: Scopri informazioni approfondite in Attribution AI
topic-legacy: Attribution AI insights
description: Questo documento funge da guida per interagire con le informazioni sulle istanze del servizio nell’interfaccia utente di Adobe Intelligent Services.
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1584'
ht-degree: 0%

---

# Scopri le informazioni in Attribution AI

Le istanze del servizio Attribution AI forniscono informazioni utili per prendere e misurare le decisioni di marketing relative alle prestazioni di marketing e al ritorno sull’investimento. La selezione di un’istanza di servizio fornisce visualizzazioni e filtri che ti aiutano a comprendere l’impatto di ogni interazione con il cliente in ogni fase del percorso di clienti.

Questo documento funge da guida per interagire con le informazioni sulle istanze del servizio nell’interfaccia utente di Adobe Intelligent Services.

## Introduzione

Per utilizzare le informazioni per Attribution AI, è necessario disporre di un’istanza di servizio con uno stato di esecuzione riuscito. Per creare una nuova istanza del servizio, visita la [guida all&#39;interfaccia utente Attribution AI](./user-guide.md). Se hai creato di recente un&#39;istanza di servizio ed è ancora in fase di formazione e valutazione, ti preghiamo di consentire 24 ore per il completamento dell&#39;esecuzione.

## Panoramica delle informazioni sulle istanze del servizio

Nell’interfaccia utente [!DNL Adobe Experience Platform] , seleziona **[!UICONTROL Services]** nel menu di navigazione a sinistra. Viene visualizzato il browser **[!UICONTROL Services]** che visualizza l&#39;Adobe di Intelligent Services disponibile. Nel contenitore per Attribution AI, seleziona **[!UICONTROL Open]**.

![Accesso all’istanza](./images/insights/open_Attribution_ai.png)

Viene visualizzata la pagina del servizio Attribution AI. In questa pagina sono elencate le istanze di servizio di Attribution AI e vengono visualizzate informazioni su di esse, tra cui il nome dell’istanza, gli eventi di conversione, la frequenza di esecuzione dell’istanza e lo stato dell’ultimo aggiornamento. Seleziona un nome di istanza del servizio da iniziare.

>[!NOTE]
>
>È possibile selezionare solo le istanze del servizio che hanno completato con successo le esecuzioni dei punteggi.

![Crea istanza](./images/insights/select-service-instance.png)

Viene quindi visualizzata la pagina delle informazioni relative all’istanza del servizio, in cui vengono fornite le visualizzazioni e una serie di filtri per interagire con i dati. Le visualizzazioni e i filtri sono descritti più dettagliatamente in questa guida.

![pagina di configurazione](./images/insights/landing-page.png)

### Dettagli istanza servizio

Per visualizzare ulteriori dettagli su un’istanza di servizio, seleziona **[!UICONTROL Show more]** in alto a destra.

![mostrare di più](./images/insights/show-more.png)

Viene visualizzato un elenco dettagliato. Per ulteriori informazioni su una delle proprietà elencate, visita la [Guida utente alle Attribution AI](./user-guide.md).

![mostra dettagli](./images/insights/advanced-details.png)

### Modificare un’istanza

Per modificare un’istanza, seleziona **[!UICONTROL Edit]** nella navigazione in alto a destra.
![fai clic sul pulsante modifica](./images/insights/edit-button.png)

Viene visualizzata la finestra di dialogo di modifica, che consente di modificare il nome, la descrizione e la frequenza di punteggio dell’istanza. Se lo stato dell’istanza è disabilitato, non è possibile modificare la frequenza di punteggio. Per confermare le modifiche e chiudere la finestra di dialogo, seleziona **[!UICONTROL Save]** nell’angolo in basso a destra.

![pozzo di modifica](./images/insights/edit-popover.png)

### Altre azioni {#more-actions}

Il pulsante **[!UICONTROL More actions]** si trova nella navigazione in alto a destra accanto a **[!UICONTROL Edit]**. Selezionando **[!UICONTROL More actions]** viene aperto un menu a discesa che consente di selezionare una delle operazioni seguenti:

- **[!UICONTROL Clone]**: Duplica l&#39;istanza.
- **[!UICONTROL Delete]**: Elimina l’istanza.
- **[!UICONTROL Download summary data]**: Scarica un file CSV contenente i dati di riepilogo.
- **[!UICONTROL Access scores]**: La selezione  **[!UICONTROL Access scores]** reindirizza ai punteggi di  [accesso per l’esercitazione](./download-scores.md) Attribution AI.
- **[!UICONTROL View run history]**: Viene visualizzato un pover contenente un elenco di tutte le esecuzioni del punteggio associate all’istanza del servizio.

![altre azioni](./images/insights/more-actions.png)

## Filtrare i dati

Le informazioni di Attribution AI ti consentono di filtrare i dati e aggiornare automaticamente le visualizzazioni dell’interfaccia utente in base ai filtri selezionati.

### Evento di conversione

Quando crei una nuova istanza in Attribution AI, uno dei campi obbligatori è &quot;Eventi di conversione&quot;. Gli eventi di conversione sono obiettivi aziendali che identificano l’impatto delle attività di marketing, come ordini di e-commerce, acquisti in-store e visite a siti web.

Dall’interno dell’istanza, il menu a discesa **[!UICONTROL Conversion events]** ti consente di selezionare uno degli eventi definiti per l’istanza al fine di filtrare i dati. Quando si selezionano eventi specifici, le visualizzazioni dell’interfaccia utente vengono modificate per compilare solo le conversioni appartenenti a tali eventi.

![evento di conversione](./images/insights/conversion-event.png)

### Modello di attribuzione

Selezionando **[!UICONTROL Attribution Model]** viene aperto un menu a discesa con tutti i diversi modelli di attribuzione disponibili. Puoi selezionare più modelli per confrontare i risultati. Per ulteriori informazioni sui diversi modelli di attribuzione e sul loro funzionamento, visita la panoramica [Attribution AI](./overview.md) che contiene una tabella con informazioni su ciascun modello.

![modello di attribuzione](./images/insights/attribution-model.png)

### Regione

>[!NOTE]
>
>Questo filtro è presente solo se hai eseguito il passaggio facoltativo [modeling basato su regione](./user-guide.md#region-based-modeling-optional) nella guida all&#39;interfaccia utente di Attribution AI durante la creazione dell&#39;istanza di servizio.

Questo filtro consente di selezionare le aree configurate nel processo di creazione delle istanze.

### Aggiungere filtri

Per aggiungere altri filtri, seleziona l’icona **filter** per aprire il puntatore **[!UICONTROL Add filters]**. Il puntatore **[!UICONTROL Add filters]** ti consente di filtrare per canale, posizione geografica, tipo di file multimediali e prodotto. Solo i filtri applicabili per un&#39;istanza di servizio sono compilati dal proxy. Ad esempio, se non hai fornito dati geografici o un tipo di supporto, questi attributi di filtro non saranno disponibili per la tua istanza.

![filtri aggiuntivi](./images/insights/additional-filters.png)

![pover filtro](./images/insights/filter-popover.png)

- **[!UICONTROL Channel]:** seleziona l’attributo del canale per filtrare tutti i canali di marketing disponibili. Puoi selezionare più canali per confrontarli.
- **[!UICONTROL Geography]:** seleziona l’attributo geografia per filtrare i codici paese in base ai modelli basati su regione. A seconda dei dati, questo filtro potrebbe essere presente o meno. I codici paese sono lunghi due caratteri. Vedi l&#39;elenco completo dei codici paese [qui](https://datahub.io/core/country-list).
- **[!UICONTROL Media type]:** seleziona l’attributo tipo di file multimediale per filtrare i tipi di file multimediali definiti.
- **[!UICONTROL Product]:** selezionando l’attributo di prodotto puoi filtrare da tutti i prodotti che sono stati inizialmente acquisiti nella creazione della tua istanza.

### Date Range

Seleziona l’icona del calendario per aprire l’intervallo di date. Le date dell’evento di conversione iniziale e finale determinano la quantità di dati compilati nell’interfaccia utente. È possibile scegliere di restringere o ampliare l’intervallo di date per attivare o espandere la quantità di dati compilati.

![intervallo date](./images/insights/display-date-range.png)

## Panoramica dei dati

La scheda **[!UICONTROL Overview]** mostra le conversioni totali per modello di attribuzione. Il numero totale cambia in base alla specifica ricerca effettuata utilizzando i filtri precedentemente descritti in questo documento. Selezionando più modelli, vengono aggiunti ulteriori cerchi alla Panoramica, ciascuno con il proprio colore corrispondente alla legenda.

![panoramica](./images/insights/Overview.png)

## Tendenze settimanali

La scheda **[!UICONTROL Weekly trends]** suddivide la conversione totale in base all’intervallo di date impostato durante il processo di filtraggio.

Selezionando i puntini di sospensione in alto a destra della scheda **Tendenze settimanali** viene visualizzato un elenco a discesa che consente di selezionare le tendenze giornaliere, settimanali o mensili.

Passando il puntatore del mouse sulla riga dati di un modello di attribuzione specifico si crea un puntatore che mostra il numero totale di conversioni per tale data.

![trend](./images/insights/weekly-trends.png)

## Suddivisione per canale

La scheda **[!UICONTROL Breakdown by channel]** viene utilizzata per determinare il numero totale di conversioni in relazione a ciascun canale. Questa scheda può essere utilizzata per prendere decisioni sull&#39;efficacia di ogni canale e sul ritorno sull&#39;investimento.

Selezionando i puntini di sospensione in alto a destra della scheda **[!UICONTROL Breakdown by channel]** viene visualizzato un menu a discesa che consente di popolare i dati in base ai punti di contatto.

![canale di rottura](./images/insights/channel-breakdown.png)

## Campagne principali

La scheda **[!UICONTROL Top campaigns]** presenta una panoramica delle campagne e delle prestazioni della campagna in ciascun canale. Questa scheda può aiutare a informare il tuo team dell’efficacia di una campagna specifica per un dato canale e fornire informazioni quali le campagne in cui investire ulteriormente.

![campagne principali](./images/insights/top-campaigns.png)

## Suddivisione per posizione punto di contatto

Selezionando la scheda **[!UICONTROL Path Analysis]** vengono caricati i grafici **[!UICONTROL Breakdown by touchpoint position]** e **[!UICONTROL Top conversion paths]**.

Il grafico **[!UICONTROL Breakdown by touchpoint position]** è una suddivisione delle conversioni attribuite in base alla posizione del punto di contatto rispetto a tutti i percorsi di conversione. Questo grafico ti aiuta a comprendere quali punti di contatto sono più efficaci nelle diverse fasi del percorso di conversione. Le tappe sono di inizio, giocatore e più vicino.

- **Starter:** indica che il punto di contatto è stato il primo contatto in un percorso di conversione.
- **Lettore:** indica che il punto di contatto non è stato il primo o l’ultimo contatto che ha portato a una conversione.
- **Più vicino:** indica che il punto di contatto è stato l’ultimo contatto prima di una conversione.

>!![NOTE]
La somma del contributo percentuale per un modello di attribuzione per tutti i punti di contatto e le posizioni deve essere pari a 100.

![punto di contatto di suddivisione del percorso utente](./images/insights/user-paths.png)

## Percorsi di conversione principali

Il grafico **[!UICONTROL Top conversion paths]** mostra i punteggi algoritmici e influenzati sui principali percorsi di conversione nelle aree selezionate. Questo grafico ti consente di visualizzare cosa i punti di contatto contribuiscono alle conversioni e qual è il punteggio di attribuzione per ogni punto di contatto. Puoi utilizzare queste informazioni per visualizzare i percorsi più frequenti in una determinata area e vedere se emergono dei pattern tra i diversi set di punti di contatto.

![Percorsi utente più comuni](./images/insights/Touchpoint-paths.png)

## Efficienza dei punti di contatto

Selezionando la scheda **[!UICONTROL Touchpoint Effectiveness]** viene caricata la scheda **[!UICONTROL Touchpoint effectiveness]** . Questa scheda utilizza la distribuzione dei dati da parte di Attribution AI per visualizzare le informazioni per ogni punto di contatto. I dati per questa tabella vengono generati solo per periodi di tempo specifici, come indicato dalla data **[!UICONTROL As of]** in alto a destra della scheda.

![selezione dell’efficacia del punto di contatto](./images/insights/Touchpoint-effectiveness.png)

Puoi usare le informazioni sulla scheda **[!UICONTROL Touchpoint effectiveness]** per comprendere in che modo un punto di contatto contribuisce a una conversione. Puoi anche vedere l’efficacia di ogni punto di contatto con le seguenti metriche di prestazioni:

**Percorsi toccati**: Questa metrica mostra una percentuale di percorsi che raggiungono o meno la conversione per il punto di contatto. Vedrai conversioni attribuite più elevate se il rapporto di percorsi (percentuale) che raggiungono la conversione in percorsi che non raggiungono la conversione è alto.

![Percorsi toccati dalla metrica](./images/insights/Touchpoint-metrics.png)

**Misura** di efficienza: Questa metrica mostra le stelle su una scala da uno a cinque. La scala indica l’importanza relativa di un punto di contatto per effettuare una conversione.

>[!NOTE]
Un volume più elevato dei punti di contatto non garantisce una maggiore efficienza.

**Volume** totale: Il numero aggregato di volte in cui un punto di contatto è stato toccato da un utente. Questo include i punti di contatto che vengono visualizzati su un percorso che raggiunge la conversione e i percorsi che non determinano una conversione.

## Passaggi successivi

Una volta completato il filtraggio dei dati e in grado di visualizzare le informazioni appropriate, puoi accedere ai punteggi. Per una guida dettagliata su come accedere ai punteggi, visita il tutorial [punteggi di accesso in Attribution AI](./download-scores.md) . Inoltre, puoi scaricare i dati di riepilogo come indicato in [altre azioni](#more-actions). Selezionando &quot;Scarica dati di riepilogo&quot; vengono scaricati i dati di riepilogo aggregati per date.

## Risorse aggiuntive

Il video seguente è stato progettato per aiutare nell’apprendimento dell’utilizzo della pagina Informazioni sulle Attribution AI per comprendere il ROI dei canali e delle campagne di marketing.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
