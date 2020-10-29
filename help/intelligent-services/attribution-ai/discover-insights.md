---
keywords: Experience Platform;insights;attribution ai;popular topics;attribution ai insights
solution: Experience Platform
title: Scoprire informazioni nelle  Attribution AI
topic: Attribution AI insights
description: Questo documento funge da guida per l'interazione con le informazioni sulle istanze del servizio nell'interfaccia utente del Adobe  Intelligent Services.
translation-type: tm+mt
source-git-commit: 69c27fc45aa9d9acaaed29c2324d02ebd471d63d
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 0%

---


# Scoprire informazioni nelle  Attribution AI

 istanze di servizi di Attribution AI forniscono informazioni utili per prendere e misurare le decisioni di marketing relative alle prestazioni di marketing e al ritorno sull&#39;investimento. La selezione di un&#39;istanza di servizio fornisce visualizzazioni e filtri per aiutarvi a comprendere l&#39;impatto di ogni interazione con il cliente in ogni fase del percorso del cliente.

Questo documento funge da guida per l&#39;interazione con le informazioni sulle istanze del servizio nell&#39;interfaccia utente del Adobe  Intelligent Services.

## Introduzione

Per utilizzare le informazioni per  Attribution AI, è necessario disporre di un&#39;istanza di servizio con uno stato di esecuzione riuscito. Per creare una nuova istanza del servizio, visita la guida [all’interfaccia utente della Attribution AI](./user-guide.md). Se avete creato di recente un&#39;istanza di servizio che continua a essere formativa e valutazione, lasciate 24 ore per completare l&#39;esecuzione.

## Panoramica delle informazioni sulle istanze del servizio

In the [!DNL Adobe Experience Platform] UI, select **[!UICONTROL Services]** in the left navigation. Il **[!UICONTROL Services]** browser viene visualizzato e  Adobe Intelligent Services. Nel contenitore per  Attribution AI, selezionare **[!UICONTROL Open]**.

![Accesso all’istanza](./images/insights/open_Attribution_ai.png)

Viene visualizzata la pagina del servizio  Attribution AI. In questa pagina sono elencate le istanze di servizio delle  Attribution AI e vengono visualizzate informazioni su di esse, incluso il nome dell&#39;istanza, gli eventi di conversione, la frequenza di esecuzione dell&#39;istanza e lo stato dell&#39;ultimo aggiornamento. Selezionate il nome di un’istanza di servizio da iniziare.

>[!NOTE]
>
>È possibile selezionare solo le istanze del servizio che hanno completato con successo l&#39;esecuzione del punteggio.

![Crea istanza](./images/insights/select-service-instance.png)

Viene quindi visualizzata la pagina delle informazioni relative all’istanza del servizio, in cui vengono fornite le visualizzazioni e una serie di filtri per interagire con i dati. Le visualizzazioni e i filtri sono descritti più dettagliatamente in questa guida.

![pagina di configurazione](./images/insights/landing-page.png)

### Dettagli dell&#39;istanza del servizio

Per visualizzare ulteriori dettagli per un’istanza di servizio, selezionate **[!UICONTROL Show more]** in alto a destra.

![mostra di più](./images/insights/show-more.png)

Viene visualizzato un elenco dettagliato. Per maggiori informazioni sulle proprietà elencate, consulta la guida [utente](./user-guide.md)Attribution AI.

![mostrare i dettagli](./images/insights/advanced-details.png)

### Modificare un’istanza

Per modificare un&#39;istanza, selezionate **[!UICONTROL Edit]** nella navigazione in alto a destra.
![fare clic sul pulsante Modifica](./images/insights/edit-button.png)

Viene visualizzata la finestra di dialogo di modifica, che consente di modificare il nome, la descrizione e la frequenza di valutazione dell’istanza. Se lo stato dell’istanza è disabilitato, non è possibile modificare la frequenza del punteggio. Per confermare le modifiche e chiudere la finestra di dialogo, selezionate **[!UICONTROL Save]** nell’angolo inferiore destro.

![edit pover](./images/insights/edit-popover.png)

### Altre azioni {#more-actions}

Il **[!UICONTROL More actions]** pulsante si trova nella barra di navigazione in alto a destra accanto a **[!UICONTROL Edit]**. Selezionando **[!UICONTROL More actions]** si apre un menu a discesa che consente di selezionare una delle operazioni seguenti:

- **[!UICONTROL Clone]**: Duplica l’istanza.
- **[!UICONTROL Delete]**: Elimina l&#39;istanza.
- **[!UICONTROL Download summary data]**: Scarica un file CSV contenente i dati di riepilogo.
- **[!UICONTROL Access scores]**: Selezionando **[!UICONTROL Access scores]** si reindirizzano ai punteggi di [accesso per  esercitazione](./download-scores.md)sulle Attribution AI.
- **[!UICONTROL View run history]**: Viene visualizzato un contenitore contenente un elenco di tutte le esecuzioni del punteggio associate all&#39;istanza del servizio.

![altre azioni](./images/insights/more-actions.png)

## Applicazione di filtri ai dati

 informazioni approfondite sulle Attribution AI consentono di filtrare i dati e aggiornare automaticamente le visualizzazioni dell&#39;interfaccia utente in base ai filtri selezionati.

### Evento di conversione

Quando create una nuova istanza in  Attribution AI, uno dei campi obbligatori è &quot;Eventi di conversione&quot;. Gli eventi di conversione sono obiettivi aziendali che identificano l&#39;impatto delle attività di marketing, come gli ordini di e-commerce, gli acquisti in-store e le visite ai siti Web.

Dall&#39;interno dell&#39;istanza, il **[!UICONTROL Conversion events]** menu a discesa consente di selezionare uno degli eventi definiti per l&#39;istanza al fine di filtrare i dati. Selezionando eventi specifici, le visualizzazioni dell&#39;interfaccia utente vengono modificate per compilare solo le conversioni appartenenti a tali eventi.

![Evento conversion](./images/insights/conversion-event.png)

### Modello di attribuzione

Selezionando **[!UICONTROL Attribution Model]** si apre un menu a discesa con tutti i diversi modelli di attribuzione disponibili. Potete selezionare più modelli per confrontare i risultati. Per ulteriori informazioni sui diversi modelli di attribuzione e sul loro funzionamento, visita la panoramica delle Attribution AI [](./overview.md) che contiene una tabella con informazioni su ciascun modello.

![modello di attribuzione](./images/insights/attribution-model.png)

### Regione

>[!NOTE]
>
>Questo filtro è presente solo se durante la creazione dell’istanza del servizio è stata eseguita la modellazione [opzionale basata sull’](./user-guide.md#region-based-modeling-optional) area di passaggio nella guida dell’interfaccia utente della Attribution AI .

Questo filtro consente di selezionare tutte le aree configurate nel processo di creazione dell&#39;istanza.

### Aggiungere filtri

Per aggiungere altri filtri, fate clic sull’icona del **filtro** per aprire il **[!UICONTROL Add filters]** puntatore. Il **[!UICONTROL Add filters]** puntatore consente di filtrare in base a Canale, Geografia, Tipo di oggetto multimediale e Prodotto. Solo i filtri applicabili per un&#39;istanza di servizio sono popolati dal puntatore. Ad esempio, se non avete fornito dati geografici o un tipo di supporto, questi attributi del filtro non saranno disponibili per l’istanza.

![filtri aggiuntivi](./images/insights/additional-filters.png)

![filtro](./images/insights/filter-popover.png)

- **[!UICONTROL Channel]:** La selezione dell&#39;attributo del canale consente di filtrare i canali di marketing disponibili. Potete selezionare più canali per confrontarli.
- **[!UICONTROL Geography]:** La selezione dell&#39;attributo geografia consente di filtrare i codici paese in base a modelli basati su regioni. A seconda dei dati, questo filtro potrebbe essere presente o meno. I codici paese sono lunghi due caratteri. Vedi l&#39;elenco completo dei codici paese [qui](https://datahub.io/core/country-list).
- **[!UICONTROL Media type]:** La selezione dell&#39;attributo del tipo di supporto consente di filtrare i tipi di supporti definiti.
- **[!UICONTROL Product]:** Selezionando l&#39;attributo product è possibile filtrare da tutti i prodotti inizialmente acquisiti per la creazione dell&#39;istanza.

### Date Range

Selezionate l&#39;icona del calendario per aprire il puntatore dell&#39;intervallo di date. Le date dell&#39;evento di conversione iniziale e finale determinano la quantità di dati compilati nell&#39;interfaccia utente. È possibile scegliere di restringere o ampliare l&#39;intervallo di date per rendere attivi o espandere la quantità di dati compilati.

![intervallo date](./images/insights/display-date-range.png)

## Panoramica dei dati

La **[!UICONTROL Overview]** scheda mostra le conversioni totali per modello di attribuzione. Il numero totale cambia in base alle specifiche ricerche effettuate utilizzando i filtri precedentemente descritti in questo documento. Selezionando più modelli, alla Panoramica vengono aggiunti altri cerchi, ciascuno dei quali ha un proprio colore corrispondente alla legenda.

![panoramica](./images/insights/Overview.png)

## Tendenze settimanali

La **[!UICONTROL Weekly trends]** scheda suddivide la conversione totale per l&#39;intervallo di date impostato durante il processo di filtraggio.

Selezionando le ellissi in alto a destra della scheda delle tendenze **** settimanali, viene visualizzato un elenco a discesa che consente di selezionare le tendenze giornaliere, settimanali o mensili.

Quando si passa il puntatore del mouse sulla riga dati di un modello di attribuzione specifico, viene creato un puntatore che mostra il numero totale di conversioni per tale data.

![trend](./images/insights/weekly-trends.png)

## Suddivisione per canale

La **[!UICONTROL Breakdown by channel]** scheda viene utilizzata per determinare il numero totale di conversioni in relazione a ciascun canale. Questa scheda può essere utilizzata per prendere decisioni sull&#39;efficacia di ogni canale e sul ritorno sull&#39;investimento.

Selezionando le ellissi in alto a destra della **[!UICONTROL Breakdown by channel]** scheda si apre un menu a discesa che consente di compilare i dati in base ai punti di contatto.

![canale di degradazione](./images/insights/channel-breakdown.png)

## Campagne principali

Nella **[!UICONTROL Top campaigns]** scheda viene visualizzata una panoramica delle campagne e delle prestazioni della campagna in ogni canale. Questa scheda può aiutare a informare il team sull&#39;efficacia di una campagna specifica per un determinato canale e fornire informazioni quali le campagne sulle quali investire ulteriormente.

![campagne principali](./images/insights/top-campaigns.png)

## Suddivisione per posizione punto di contatto

Selezionando la **[!UICONTROL Path Analysis]** scheda si caricano i **[!UICONTROL Breakdown by touchpoint position]** grafici e **[!UICONTROL Top conversion paths]** i grafici.

Il **[!UICONTROL Breakdown by touchpoint position]** grafico è una suddivisione delle conversioni attribuite per posizione del punto di contatto rispetto a tutti i percorsi di conversione. Questo grafico aiuta a capire quali punti di contatto sono più efficaci nelle diverse fasi del percorso di conversione. Le tappe sono di inizio, giocatore e più vicine.

- **Inizio:** Indica che il punto di contatto è stato il primo tocco in un percorso di conversione.
- **Lettore:** Indica che il punto di contatto non è stato il primo o l&#39;ultimo tocco che ha portato a una conversione.
- **Più vicino:** Indica che il punto di contatto è stato l’ultimo tocco prima di una conversione.

>!![NOTE]
La somma del contributo percentuale per un modello di attribuzione tra tutti i punti di contatto e le posizioni deve essere pari a 100.

![punto di contatto per analisi percorso utente](./images/insights/user-paths.png)

## Percorsi di conversione principali

Il **[!UICONTROL Top conversion paths]** grafico mostra i punteggi influenzati e algoritmici sui percorsi di conversione principali nelle aree selezionate. Questo grafico consente di visualizzare i punti di contatto che contribuiscono alle conversioni e qual è il punteggio di attribuzione per ciascun punto di contatto. Puoi utilizzare queste informazioni per visualizzare i percorsi più frequenti in una determinata area e verificare se tra i diversi set di punti di contatto emergono dei pattern.

![Percorsi utente più comuni](./images/insights/Touchpoint-paths.png)

## Efficienza punto di contatto

Selezionando la **[!UICONTROL Touchpoint Effectiveness]** scheda si carica la **[!UICONTROL Touchpoint effectiveness]** scheda. Questa scheda utilizza  distribuzione dei dati da parte delle Attribution AI per visualizzare le informazioni relative a ciascun punto di contatto. I dati per questa tabella vengono generati solo per specifici periodi di tempo, come indicato dalla **[!UICONTROL As of]** data in alto a destra della scheda.

![selezione efficacia punto di contatto](./images/insights/Touchpoint-effectiveness.png)

Potete utilizzare le informazioni sulla **[!UICONTROL Touchpoint effectiveness]** scheda per comprendere in che modo un punto di contatto contribuisce a una conversione. Puoi anche verificare l’efficacia di ciascun punto di contatto con le metriche di prestazioni seguenti:

**Percorsi toccati**: Questa metrica mostra una percentuale di percorsi che raggiungono o non raggiungono la conversione per il punto di contatto. Se il rapporto tra i percorsi (percentuale) che ottengono la conversione in percorsi che non raggiungono la conversione è elevato, verranno visualizzate conversioni con attribuzione maggiore.

![Percorsi toccati dalla metrica](./images/insights/Touchpoint-metrics.png)

**Misura** di efficienza: Questa metrica visualizza le stelle su una scala da uno a cinque. La scala indica l&#39;importanza relativa di un punto di contatto per effettuare una conversione.

>[!NOTE]
Un volume di punti di contatto più elevato non garantisce una misura di efficienza più elevata.

**Volume** totale: Il numero complessivo di volte in cui un punto di contatto è stato toccato da un utente. Ciò include i punti di contatto visualizzati su un percorso che consente di ottenere la conversione e i percorsi che non determinano una conversione.

## Passaggi successivi

Dopo aver filtrato i dati e aver visualizzato le informazioni appropriate, potete accedere ai punteggi. Per una guida dettagliata su come accedere ai punteggi, visita i punteggi di [accesso in  Attribution AI](./download-scores.md) tutorial. Inoltre, puoi scaricare i dati di riepilogo come indicato in [più azioni](#more-actions). Se selezionate &quot;Scarica dati di riepilogo&quot;, vengono scaricati i dati di riepilogo aggregati per data.

## Risorse aggiuntive

Il seguente video è stato progettato per aiutare a imparare a utilizzare la pagina di approfondimenti sulle Attribution AI  per comprendere il ROI dei canali e delle campagne di marketing.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)