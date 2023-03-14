---
keywords: Experience Platform;insights;ai attribuzione;argomenti popolari;informazioni ai attribuzione
feature: Attribution AI
title: Scopri gli Approfondimenti in Attribution AI
description: Questo documento funge da guida per l’interazione con le informazioni approfondite sull’istanza del servizio nell’interfaccia utente di Adobe Intelligent Services.
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---

# Scopri informazioni in Attribution AI

Le istanze del servizio Attribution AI forniscono informazioni che possono essere utilizzate per assistere nel prendere e misurare decisioni di marketing relative alle prestazioni di marketing e al ritorno sull’investimento. La selezione di un’istanza del servizio fornisce visualizzazioni e filtri che consentono di comprendere l’impatto di ogni interazione con il cliente in ogni fase del percorso.

Questo documento funge da guida per l’interazione con le informazioni approfondite sull’istanza del servizio nell’interfaccia utente di Adobe Intelligent Services.

## Introduzione

Per utilizzare informazioni approfondite su Attribution AI, è necessario disporre di un’istanza del servizio con stato di esecuzione corretto. Per creare una nuova istanza di servizio, visita [Guida all’interfaccia utente di Attribution AI](./user-guide.md). Se di recente è stata creata un’istanza del servizio che sta ancora formando e assegnando un punteggio, attendi 24 ore prima del termine dell’esecuzione.

## Panoramica di Service Instance Insights

In [!DNL Adobe Experience Platform] UI, seleziona **[!UICONTROL Servizi]** nel menu di navigazione a sinistra. Il **[!UICONTROL Servizi]** viene visualizzato il browser e viene visualizzato l&#39;Adobe Intelligent Services disponibile. Nel contenitore per Attribution AI, seleziona **[!UICONTROL Apri]**.

![Accesso all’istanza](./images/insights/open_Attribution_ai.png)

Viene visualizzata la pagina Servizio di Attribution AI. Questa pagina elenca le istanze di servizio di Attribution AI e visualizza informazioni su di esse, tra cui il nome dell’istanza, gli eventi di conversione, la frequenza di esecuzione dell’istanza e lo stato dell’ultimo aggiornamento. Seleziona un nome di istanza del servizio per iniziare.

>[!NOTE]
>
>È possibile selezionare solo le istanze del servizio che hanno completato le esecuzioni con punteggio di successo.

![Crea istanza](./images/insights/select-service-instance.png)

Viene quindi visualizzata la pagina delle informazioni per l’istanza del servizio, in cui sono disponibili visualizzazioni e diversi filtri per interagire con i dati. Le visualizzazioni e i filtri sono illustrati più dettagliatamente in questa guida.

![pagina di impostazione](./images/insights/landing-page.png)

### Dettagli dell’istanza del servizio

Per visualizzare ulteriori dettagli su un’istanza del servizio, seleziona **[!UICONTROL Mostra altro]** in alto a destra.

![mostra altro](./images/insights/show-more.png)

Viene visualizzato un elenco dettagliato. Per ulteriori informazioni su una delle proprietà elencate, visitare il [Guida utente di Attribution AI](./user-guide.md).

![mostra dettagli](./images/insights/advanced-details.png)

### Modificare un’istanza

Per modificare un’istanza, seleziona **[!UICONTROL Modifica]** nella navigazione in alto a destra.
![fai clic sul pulsante modifica](./images/insights/edit-button.png)

Viene visualizzata la finestra di dialogo Modifica, che consente di modificare il nome, la descrizione e la frequenza di punteggio dell’istanza. Se lo stato dell’istanza è disabilitato, non è possibile modificare la frequenza di punteggio. Per confermare le modifiche e chiudere la finestra di dialogo, seleziona **[!UICONTROL Salva]** in basso a destra.

![modifica popover](./images/insights/edit-popover.png)

### Altre azioni {#more-actions}

Il **[!UICONTROL Altre azioni]** si trova nella navigazione in alto a destra accanto a **[!UICONTROL Modifica]**. Selezione **[!UICONTROL Altre azioni]** apre un menu a discesa che consente di selezionare una delle seguenti operazioni:

- **[!UICONTROL Clona]**: clona l’istanza.
- **[!UICONTROL Elimina]**: elimina l’istanza.
- **[!UICONTROL Scarica dati di riepilogo]**: scarica un file CSV contenente i dati di riepilogo.
- **[!UICONTROL Punteggi di accesso]**: selezione **[!UICONTROL Punteggi di accesso]** ti reindirizza a [esercitazione sui punteggi di accesso per Attribution AI](./download-scores.md).
- **[!UICONTROL Visualizza cronologia di esecuzione]**: viene visualizzato un popover contenente un elenco di tutte le esecuzioni di punteggio associate all’istanza del servizio.

![altre azioni](./images/insights/more-actions.png)

## Filtrare i dati

Attribution AI Insights ti consente di filtrare i dati e di aggiornare automaticamente gli elementi visivi dell’interfaccia utente in base ai filtri selezionati.

### Evento di conversione

Quando crei una nuova istanza in Attribution AI, uno dei campi obbligatori è &quot;Eventi di conversione&quot;. Gli eventi di conversione sono obiettivi aziendali che identificano l’impatto delle attività di marketing, come ordini di e-commerce, acquisti in-store e visite al sito web.

Dall’interno dell’istanza, il **[!UICONTROL Eventi di conversione]** Il menu a discesa consente di selezionare uno qualsiasi degli eventi definiti per l’istanza per filtrare i dati. La selezione di eventi specifici cambia le visualizzazioni dell’interfaccia utente in modo da popolare solo le conversioni appartenenti a tali eventi.

![evento di conversione](./images/insights/conversion-event.png)

### Modello di attribuzione

Selezione **[!UICONTROL Modello di attribuzione]** apre un menu a discesa con tutti i diversi modelli di attribuzione disponibili. Puoi selezionare più modelli per confrontare i risultati. Per ulteriori informazioni sui diversi modelli di attribuzione e sul loro funzionamento, visita [Attribution AI](./overview.md) panoramica che contiene una tabella con informazioni su ciascun modello.

![modello di attribuzione](./images/insights/attribution-model.png)

### Area geografica

>[!NOTE]
>
>Questo filtro è presente solo se hai eseguito il passaggio facoltativo [modellazione basata su regione](./user-guide.md#region-based-modeling-optional) nella guida dell’interfaccia utente di Attribution AI durante la creazione dell’istanza di servizio.

Questo filtro consente di selezionare qualsiasi area impostata nel processo di creazione dell’istanza.

### Aggiungere filtri

Puoi aggiungere altri filtri selezionando la **filter** per aprire **[!UICONTROL Aggiungere filtri]** popover. Il **[!UICONTROL Aggiungere filtri]** Il popover consente di filtrare per canale, area geografica, tipo di elemento multimediale e prodotto. Solo i filtri applicabili per un’istanza del servizio vengono compilati dal popover. Ad esempio, se non hai fornito dati geografici o un tipo di file multimediale, questi attributi di filtro non saranno disponibili per la tua istanza.

![filtri aggiuntivi](./images/insights/additional-filters.png)

![popover del filtro](./images/insights/filter-popover.png)

- **[!UICONTROL Canale]:** Selezionando l’attributo del canale puoi filtrare uno qualsiasi dei canali di marketing disponibili. Puoi selezionare più canali per confrontarli.
- **[!UICONTROL Geografia]:** La selezione dell’attributo relativo alla geografia consente di filtrare i codici paese in base ai modelli basati sulla regione. A seconda dei dati, questo filtro può essere presente o meno. I codici di paese hanno una lunghezza di due caratteri. Si veda l&#39;elenco completo dei codici paese [qui](https://datahub.io/core/country-list).
- **[!UICONTROL Tipo di file multimediale]:** Selezionando l’attributo del tipo di file multimediale puoi filtrare qualsiasi tipo di file multimediale definito.
- **[!UICONTROL Prodotto]:** Selezionando l’attributo del prodotto puoi filtrare da tutti i prodotti inizialmente acquisiti nella creazione dell’istanza.

### Date Range

Seleziona l’icona del calendario per aprire il popover dell’intervallo di date. Le date dell’evento di conversione iniziale e finale determinano la quantità di dati popolati nell’interfaccia utente. Puoi scegliere di restringere o ampliare l’intervallo di date per concentrare o espandere la quantità di dati popolati.

![intervallo date](./images/insights/display-date-range.png)

## Panoramica dei dati

Il **[!UICONTROL Panoramica]** mostra le conversioni totali per modello di attribuzione. Il numero totale cambia in base a quanto specifico è stata effettuata la ricerca utilizzando i filtri descritti in precedenza in questo documento. Selezionando più modelli si aggiungono ulteriori cerchi alla Panoramica, ciascuno con il proprio colore corrispondente alla legenda.

![panoramica](./images/insights/Overview.png)

## Tendenze settimanali

Il **[!UICONTROL Tendenze settimanali]** La scheda suddivide la conversione totale in base all’intervallo di date impostato durante il processo di filtraggio.

Selezione dei puntini di sospensione in alto a destra del **Tendenze settimanali** La scheda mostra un elenco a discesa che consente di selezionare le tendenze giornaliere, settimanali o mensili.

Passando il cursore del mouse sulla riga di dati di un modello di attribuzione specifico, viene creato un elemento a comparsa che mostra il numero totale di conversioni per tale data.

![tendenze](./images/insights/weekly-trends.png)

## Raggruppamento per canale

Il **[!UICONTROL Raggruppamento per canale]** La scheda viene utilizzata per determinare il numero totale di conversioni in relazione a ciascun canale. Questa scheda può essere utilizzata per prendere decisioni sull&#39;efficacia di ciascun canale e sul ritorno sull&#39;investimento.

Selezione dei puntini di sospensione in alto a destra del **[!UICONTROL Raggruppamento per canale]** apre un menu a discesa che consente di popolare i dati in base ai punti di contatto.

![canale di suddivisione](./images/insights/channel-breakdown.png)

## Campagne principali

Il **[!UICONTROL Campagne principali]** mostra una panoramica delle campagne e delle prestazioni della campagna in ciascun canale. Questa scheda può aiutare a informare il team dell’efficacia di una campagna specifica per un determinato canale e fornire informazioni quali le campagne in cui investire ulteriormente.

![campagne principali](./images/insights/top-campaigns.png)

## Suddivisione per posizione punto di contatto

Selezione del **[!UICONTROL Analisi percorso]** scheda carica il **[!UICONTROL Suddivisione per posizione punto di contatto]** e **[!UICONTROL Percorsi di conversione principali]** grafici.

Il **[!UICONTROL Suddivisione per posizione punto di contatto]** il grafico è una suddivisione delle conversioni attribuite per posizione del punto di contatto confrontato tra tutti i percorsi di conversione. Questo grafico consente di comprendere quali punti di contatto sono più efficaci nelle diverse fasi del percorso di conversione. Gli stadi sono starter, player e closer.

- **Starter:** Indica che il punto di contatto è stato il primo contatto in un percorso di conversione.
- **Lettore:** Indica che il punto di contatto non è stato il primo o l’ultimo contatto che ha portato a una conversione.
- **Più vicino:** Indica che il punto di contatto è stato l’ultimo contatto prima di una conversione.

>!![NOTE]
La somma del contributo in percentuale per un modello di attribuzione in tutti i punti di contatto e le posizioni deve essere pari a 100.

![punto di contatto di suddivisione percorso utente](./images/insights/user-paths.png)

## Percorsi di conversione principali

Il **[!UICONTROL Percorsi di conversione principali]** il grafico mostra i punteggi algoritmici e influenzati sui percorsi di conversione principali nelle aree selezionate. Questo grafico consente di visualizzare quale punto di contatto contribuisce alle conversioni e qual è il punteggio di attribuzione per ciascun punto di contatto. Puoi utilizzare queste informazioni per visualizzare i percorsi più frequenti in una determinata area e vedere se emergono pattern tra i diversi set di punti di contatto.

![Percorsi utente più comuni](./images/insights/Touchpoint-paths.png)

## Efficacia dei punti di contatto

Selezione del **[!UICONTROL Efficacia dei punti di contatto]** scheda carica il **[!UICONTROL Efficacia dei punti di contatto]** Card. Questa scheda utilizza la distribuzione dei dati di Attribution AI per visualizzare le informazioni per ogni punto di contatto. I dati per questa tabella vengono generati solo per specifici periodi di tempo come indicato dalla **[!UICONTROL A partire da]** data in alto a destra nella scheda.

![selezione dell’efficacia del punto di contatto](./images/insights/Touchpoint-effectiveness.png)

È possibile utilizzare **[!UICONTROL Efficacia dei punti di contatto]** informazioni sulla scheda per comprendere in che modo un punto di contatto contribuisce a una conversione. Puoi anche vedere l’efficacia di ogni punto di contatto con le seguenti metriche delle prestazioni:

**Percorsi toccati**: questa metrica visualizza la percentuale di percorsi che raggiungono o non raggiungono la conversione per il punto di contatto. Se il rapporto tra percorsi (percentuale) che ottengono la conversione e percorsi che non raggiungono la conversione è elevato, si noteranno più conversioni attribuite.

![Metrica Percorsi toccati](./images/insights/Touchpoint-metrics.png)

**Misura di efficienza**: questa metrica visualizza le stelle su una scala da uno a cinque. La scala indica l’importanza relativa di un punto di contatto per effettuare una conversione.

>[!NOTE]
Un volume di punti di contatto più elevato non garantisce una misura di efficienza più elevata.

**Volume totale**: numero aggregato di volte in cui un punto di contatto è stato toccato da un utente. Sono inclusi i punti di contatto visualizzati su un percorso che raggiunge la conversione e i percorsi che non determinano una conversione.

## Passaggi successivi

Dopo aver filtrato i dati e aver visualizzato le informazioni appropriate, puoi accedere ai punteggi. Per una guida approfondita su come accedere ai punteggi, visita il [punteggi di accesso in Attribution AI](./download-scores.md) esercitazione. Inoltre, puoi scaricare i dati di riepilogo come indicato in [altre azioni](#more-actions). Selezionando &quot;Scarica dati di riepilogo&quot; si scaricano i dati di riepilogo aggregati per date.

## Risorse aggiuntive

Il video seguente è progettato per aiutarti ad imparare a utilizzare la pagina Approfondimenti di Attribution AI per comprendere il ROI dei canali e delle campagne di marketing.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
