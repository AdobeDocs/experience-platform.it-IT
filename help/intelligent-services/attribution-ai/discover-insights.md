---
keywords: Experience Platform;insights;ai attribuzione;argomenti popolari;informazioni ai attribuzione
feature: Attribution AI
title: Scopri gli approfondimenti in IA per l’attribuzione
description: Questo documento funge da guida per l’interazione con le informazioni approfondite sull’istanza del servizio nell’interfaccia utente di Adobe Intelligent Services.
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1583'
ht-degree: 0%

---

# Scopri informazioni in IA per l’attribuzione

Le istanze del servizio Attribution AI forniscono informazioni che possono essere utilizzate per assistere l’utente nell’assumere e misurare decisioni di marketing relative alle prestazioni di marketing e al ritorno sull’investimento. La selezione di un’istanza del servizio fornisce visualizzazioni e filtri che consentono di comprendere l’impatto di ogni interazione con il cliente in ogni fase del percorso.

Questo documento funge da guida per l’interazione con le informazioni approfondite sull’istanza del servizio nell’interfaccia utente di Adobe Intelligent Services.

## Introduzione

Per utilizzare le informazioni di Attribution AI, è necessario disporre di un’istanza del servizio con stato di esecuzione corretto. Per creare una nuova istanza del servizio, visita la [Guida all&#39;interfaccia utente di IA per l&#39;attribuzione](./user-guide.md). Se di recente è stata creata un’istanza del servizio per la quale si sta ancora eseguendo l’apprendimento e il punteggio, attendi 24 ore per il completamento dell’esecuzione.

## Panoramica di Service Instance Insights

Nell&#39;interfaccia utente di [!DNL Adobe Experience Platform], selezionare **[!UICONTROL Services]** nel menu di navigazione a sinistra. Verrà visualizzato il browser **[!UICONTROL Services]** in cui sono visualizzati i servizi intelligenti di Adobe disponibili. Nel contenitore di IA per l&#39;attribuzione, selezionare **[!UICONTROL Open]**.

![Accesso all&#39;istanza](./images/insights/open_Attribution_ai.png)

Viene visualizzata la pagina del servizio di Attribution AI. Questa pagina elenca le istanze del servizio di IA per l’attribuzione e visualizza informazioni su di esse, tra cui il nome dell’istanza, gli eventi di conversione, la frequenza di esecuzione dell’istanza e lo stato dell’ultimo aggiornamento. Seleziona un nome di istanza del servizio per iniziare.

>[!NOTE]
>
>È possibile selezionare solo le istanze del servizio che hanno completato le esecuzioni con punteggio di successo.

![Crea istanza](./images/insights/select-service-instance.png)

Viene quindi visualizzata la pagina delle informazioni per l’istanza del servizio, in cui sono disponibili visualizzazioni e diversi filtri per interagire con i dati. Le visualizzazioni e i filtri sono illustrati più dettagliatamente in questa guida.

![pagina installazione](./images/insights/landing-page.png)

### Dettagli dell’istanza del servizio

Per visualizzare ulteriori dettagli per un&#39;istanza del servizio, selezionare **[!UICONTROL Show more]** in alto a destra.

![mostra altro](./images/insights/show-more.png)

Viene visualizzato un elenco dettagliato. Per ulteriori informazioni sulle proprietà elencate, visita la [Guida utente di IA per l&#39;attribuzione](./user-guide.md).

![mostra dettagli](./images/insights/advanced-details.png)

### Modificare un’istanza

Per modificare un&#39;istanza, selezionare **[!UICONTROL Edit]** nella navigazione in alto a destra.
![fare clic sul pulsante Modifica](./images/insights/edit-button.png)

Viene visualizzata la finestra di dialogo Modifica, che consente di modificare il nome, la descrizione e la frequenza di punteggio dell’istanza. Se lo stato dell’istanza è disabilitato, non è possibile modificare la frequenza di punteggio. Per confermare le modifiche e chiudere la finestra di dialogo, seleziona **[!UICONTROL Save]** nell&#39;angolo in basso a destra.

![modifica popover](./images/insights/edit-popover.png)

### Altre azioni {#more-actions}

Il pulsante **[!UICONTROL More actions]** si trova nella navigazione in alto a destra accanto a **[!UICONTROL Edit]**. Selezionando **[!UICONTROL More actions]** si apre un menu a discesa che consente di selezionare una delle seguenti operazioni:

- **[!UICONTROL Clone]**: clona l&#39;istanza.
- **[!UICONTROL Delete]**: elimina l&#39;istanza.
- **[!UICONTROL Download summary data]**: scarica un file CSV contenente i dati di riepilogo.
- **[!UICONTROL Access scores]**: la selezione di **[!UICONTROL Access scores]** ti reindirizza ai [punteggi di accesso per l&#39;esercitazione di IA per l&#39;attribuzione](./download-scores.md).
- **[!UICONTROL View run history]**: viene visualizzato un popover contenente un elenco di tutte le esecuzioni di punteggio associate all&#39;istanza del servizio.

![altre azioni](./images/insights/more-actions.png)

## Filtrare i dati

Le informazioni di Attribution AI ti consentono di filtrare i dati e aggiornare automaticamente gli elementi visivi dell’interfaccia utente in base ai filtri selezionati.

### Evento di conversione

Quando crei una nuova istanza in IA per l’attribuzione, uno dei campi obbligatori è &quot;Eventi di conversione&quot;. Gli eventi di conversione sono obiettivi aziendali che identificano l’impatto delle attività di marketing, come ordini di e-commerce, acquisti in-store e visite al sito web.

Dall&#39;interno dell&#39;istanza, il menu a discesa **[!UICONTROL Conversion events]** consente di selezionare qualsiasi evento definito per l&#39;istanza per filtrare i dati. La selezione di eventi specifici cambia le visualizzazioni dell’interfaccia utente in modo da popolare solo le conversioni appartenenti a tali eventi.

![evento di conversione](./images/insights/conversion-event.png)

### Modello di attribuzione

Selezionando **[!UICONTROL Attribution Model]** si apre un menu a discesa con tutti i diversi modelli di attribuzione disponibili. Puoi selezionare più modelli per confrontare i risultati. Per ulteriori informazioni sui diversi modelli di attribuzione e sul loro funzionamento, visita la panoramica di [IA per l&#39;attribuzione](./overview.md) contenente una tabella con informazioni su ciascun modello.

![modello di attribuzione](./images/insights/attribution-model.png)

### Area geografica

>[!NOTE]
>
>Questo filtro è presente solo se durante la creazione dell&#39;istanza del servizio è stato eseguito il passaggio facoltativo [modellazione basata su area](./user-guide.md#region-based-modeling-optional) nella guida dell&#39;interfaccia utente di IA per l&#39;attribuzione.

Questo filtro consente di selezionare qualsiasi area impostata nel processo di creazione dell’istanza.

### Aggiungere filtri

Per aggiungere altri filtri, seleziona l&#39;icona **filter** per aprire il popover **[!UICONTROL Add filters]**. Il popover **[!UICONTROL Add filters]** consente di filtrare per canale, area geografica, tipo di file multimediale e prodotto. Solo i filtri applicabili per un’istanza del servizio vengono compilati dal popover. Ad esempio, se non hai fornito dati geografici o un tipo di file multimediale, questi attributi di filtro non saranno disponibili per la tua istanza.

![filtri aggiuntivi](./images/insights/additional-filters.png)

![popover filtro](./images/insights/filter-popover.png)

- **[!UICONTROL Channel]:** Selezionando l&#39;attributo di canale puoi filtrare uno qualsiasi dei canali di marketing disponibili. Puoi selezionare più canali per confrontarli.
- **[!UICONTROL Geography]:** La selezione dell&#39;attributo Geografia consente di filtrare i codici paese in base ai modelli basati su aree geografiche. A seconda dei dati, questo filtro può essere presente o meno. I codici di paese hanno una lunghezza di due caratteri. Vedi l&#39;elenco completo dei codici paese [qui](https://datahub.io/core/country-list).
- **[!UICONTROL Media type]:** La selezione dell&#39;attributo del tipo di supporto consente di filtrare qualsiasi tipo di supporto definito.
- **[!UICONTROL Product]:** La selezione dell&#39;attributo di prodotto consente di filtrare da qualsiasi prodotto acquisito inizialmente nella creazione dell&#39;istanza.

### Date Range

Seleziona l’icona del calendario per aprire il popover dell’intervallo di date. Le date dell’evento di conversione iniziale e finale determinano la quantità di dati popolati nell’interfaccia utente. Puoi scegliere di restringere o ampliare l’intervallo di date per concentrare o espandere la quantità di dati popolati.

![intervallo di date](./images/insights/display-date-range.png)

## Panoramica dei dati

La scheda **[!UICONTROL Overview]** mostra le conversioni totali per modello di attribuzione. Il numero totale cambia in base a quanto specifico è stata effettuata la ricerca utilizzando i filtri descritti in precedenza in questo documento. Selezionando più modelli si aggiungono ulteriori cerchi alla Panoramica, ciascuno con il proprio colore corrispondente alla legenda.

![panoramica](./images/insights/Overview.png)

## Tendenze settimanali

La scheda **[!UICONTROL Weekly trends]** suddivide la conversione totale in base all&#39;intervallo di date impostato durante il processo di filtraggio.

Selezionando i puntini di sospensione in alto a destra della scheda **Tendenze settimanali** viene visualizzato un elenco a discesa che consente di selezionare le tendenze giornaliere, settimanali o mensili.

Passando il cursore del mouse sulla riga di dati di un modello di attribuzione specifico, viene creato un elemento a comparsa che mostra il numero totale di conversioni per tale data.

![tendenze](./images/insights/weekly-trends.png)

## Raggruppamento per canale

La scheda **[!UICONTROL Breakdown by channel]** viene utilizzata per determinare il numero totale di conversioni in relazione a ciascun canale. Questa scheda può essere utilizzata per prendere decisioni sull&#39;efficacia di ciascun canale e sul ritorno sull&#39;investimento.

Selezionando i puntini di sospensione in alto a destra della scheda **[!UICONTROL Breakdown by channel]** si apre un menu a discesa che consente di popolare i dati in base ai punti di contatto.

![canale di suddivisione](./images/insights/channel-breakdown.png)

## Campagne principali

La scheda **[!UICONTROL Top campaigns]** mostra una panoramica delle campagne e delle prestazioni della campagna in ogni canale. Questa scheda può aiutare a informare il team dell’efficacia di una campagna specifica per un determinato canale e fornire informazioni quali le campagne in cui investire ulteriormente.

![campagne principali](./images/insights/top-campaigns.png)

## Suddivisione per posizione punto di contatto

Selezionando la scheda **[!UICONTROL Path Analysis]** vengono caricati i grafici **[!UICONTROL Breakdown by touchpoint position]** e **[!UICONTROL Top conversion paths]**.

Il grafico **[!UICONTROL Breakdown by touchpoint position]** è una suddivisione delle conversioni attribuite per posizione del punto di contatto confrontato tra tutti i percorsi di conversione. Questo grafico consente di comprendere quali punti di contatto sono più efficaci nelle diverse fasi del percorso di conversione. Gli stadi sono starter, player e closer.

- **Starter:** indica che il punto di contatto è stato il primo contatto in un percorso di conversione.
- **Lettore:** indica che il punto di contatto non è stato il primo o l&#39;ultimo contatto che ha portato a una conversione.
- **Più vicino:** indica che il punto di contatto è stato l&#39;ultimo contatto prima di una conversione.

>[!NOTE]
>
>La somma del contributo in percentuale per un modello di attribuzione in tutti i punti di contatto e le posizioni deve essere pari a 100.

![punto di contatto di suddivisione percorso utente](./images/insights/user-paths.png)

## Percorsi di conversione principali

Il grafico **[!UICONTROL Top conversion paths]** mostra i punteggi algoritmici e influenzati sui percorsi di conversione principali nelle aree selezionate. Questo grafico consente di visualizzare quale punto di contatto contribuisce alle conversioni e qual è il punteggio di attribuzione per ciascun punto di contatto. Puoi utilizzare queste informazioni per visualizzare i percorsi più frequenti in una determinata area e vedere se emergono pattern tra i diversi set di punti di contatto.

![Percorsi utente più comuni](./images/insights/Touchpoint-paths.png)

## Efficacia dei punti di contatto

Selezionando la scheda **[!UICONTROL Touchpoint Effectiveness]** si carica la scheda **[!UICONTROL Touchpoint effectiveness]**. Questa scheda utilizza la distribuzione di dati di IA per l’attribuzione per visualizzare le informazioni per ogni punto di contatto. I dati per questa tabella vengono generati solo per specifici periodi di tempo come indicato dalla data **[!UICONTROL As of]** in alto a destra nella scheda.

![selezione efficacia punto di contatto](./images/insights/Touchpoint-effectiveness.png)

È possibile utilizzare le informazioni sulla scheda **[!UICONTROL Touchpoint effectiveness]** per comprendere in che modo un punto di contatto contribuisce a una conversione. Puoi anche vedere l’efficacia di ogni punto di contatto con le seguenti metriche delle prestazioni:

**Percorsi toccati**: questa metrica visualizza la percentuale di percorsi che hanno raggiunto o meno la conversione per il punto di contatto. Se il rapporto tra percorsi (percentuale) che ottengono la conversione e percorsi che non raggiungono la conversione è elevato, si noteranno più conversioni attribuite.

![Metrica percorsi toccati](./images/insights/Touchpoint-metrics.png)

**Misura di efficienza**: questa metrica visualizza le stelle su una scala da uno a cinque. La scala indica l’importanza relativa di un punto di contatto per effettuare una conversione.

>[!NOTE]
>
>Un volume di punti di contatto più elevato non garantisce una misura di efficienza più elevata.

**Volume totale**: il numero aggregato di volte in cui un punto di contatto è stato toccato da un utente. Sono inclusi i punti di contatto visualizzati su un percorso che raggiunge la conversione e i percorsi che non determinano una conversione.

## Passaggi successivi

Dopo aver filtrato i dati e aver visualizzato le informazioni appropriate, puoi accedere ai punteggi. Per una guida approfondita su come accedere ai punteggi, consulta l&#39;esercitazione [access scores in Attribution AI](./download-scores.md). Inoltre, puoi scaricare i dati di riepilogo come indicato in [altre azioni](#more-actions). Selezionando &quot;Scarica dati di riepilogo&quot; si scaricano i dati di riepilogo aggregati per date.

## Risorse aggiuntive

Il video seguente è progettato per aiutarti ad imparare a utilizzare la pagina delle informazioni di Attribution AI per comprendere il ROI dei canali e delle campagne di marketing.

>[!VIDEO](https://video.tv.adobe.com/v/345101?captions=ita&learn=on&quality=12)
