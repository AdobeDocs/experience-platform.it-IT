---
keywords: Experience Platform;insights;attribution ai;popular topics
solution: Experience Platform
title: Scopri informazioni approfondite in Attribution AI
topic: Attribution AI insights
translation-type: tm+mt
source-git-commit: 0ea96de956adb5a6c5286433a547772118c43aee
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 1%

---


# Scopri informazioni approfondite in Attribution AI

Le istanze del servizio AI di attribuzione forniscono informazioni utili per prendere e misurare le decisioni di marketing relative alle prestazioni di marketing e al ritorno sull&#39;investimento. La selezione di un&#39;istanza di servizio fornisce visualizzazioni e filtri per aiutarvi a comprendere l&#39;impatto di ogni interazione con il cliente in ogni fase del percorso del cliente.

Questo documento funge da guida per l’interazione con le informazioni sulle istanze del servizio nell’interfaccia utente di Adobe Intelligent Services.

## Introduzione

Per utilizzare le informazioni per l&#39;analisi dell&#39;attribuzione AI, è necessario disporre di un&#39;istanza di servizio con uno stato di esecuzione riuscito. Per creare una nuova istanza del servizio, visita la guida [all’interfaccia utente](./user-guide.md)AI di attribuzione. Se avete creato di recente un&#39;istanza di servizio che continua a essere formativa e valutazione, lasciate 24 ore per completare l&#39;esecuzione.

## Panoramica delle informazioni sulle istanze del servizio

Nell’ [!DNL Adobe Experience Platform] interfaccia utente, fai clic su **Servizi** nella barra di navigazione a sinistra. Viene visualizzato il browser *Servizi* , che presenta i servizi intelligenti Adobe. Nel contenitore per l&#39;AI di attribuzione, fate clic su **Apri**.

![Accesso all’istanza](./images/insights/open_Attribution_ai.png)

Viene visualizzata la pagina del servizio AI di attribuzione. In questa pagina sono elencate le istanze del servizio di Attribution AI e vengono visualizzate informazioni su di esse, incluso il nome dell&#39;istanza, gli eventi di conversione, la frequenza di esecuzione dell&#39;istanza e lo stato dell&#39;ultimo aggiornamento. Fate clic sul nome di un&#39;istanza di servizio per iniziare.

>[!NOTE] È possibile selezionare solo le istanze del servizio che hanno completato con successo l&#39;esecuzione del punteggio.

![Crea istanza](./images/insights/select-service-instance.png)

Viene quindi visualizzata la pagina delle informazioni relative all’istanza del servizio, in cui vengono fornite le visualizzazioni e una serie di filtri per interagire con i dati. Le visualizzazioni e i filtri sono descritti più dettagliatamente in questa guida.

![pagina di configurazione](./images/insights/landing-page.png)

### Dettagli dell&#39;istanza del servizio

Per visualizzare ulteriori dettagli per un’istanza di servizio, fate clic su **Mostra più** informazioni in alto a destra.

![mostra di più](./images/insights/show-more.png)

Viene visualizzato un elenco dettagliato. Per maggiori informazioni sulle proprietà elencate, consulta la guida [utente](./user-guide.md)Attribution AI.

![mostrare i dettagli](./images/insights/advanced-details.png)

### Modificare un’istanza

Per modificare un’istanza, fate clic su *Modifica* nella barra di navigazione in alto a destra.
![fare clic sul pulsante Modifica](./images/insights/edit-button.png)

Viene visualizzata la finestra di dialogo di modifica, che consente di modificare la descrizione e la frequenza del punteggio dell’istanza. Per confermare le modifiche e chiudere la finestra di dialogo, fate clic su *Modifica* nell’angolo in basso a destra.

![edit pover](./images/insights/edit-popover.png)

### Altre azioni {#more-actions}

Il pulsante *Altre azioni* si trova nella barra di navigazione in alto a destra accanto a *Modifica*. Facendo clic su **Altre azioni** si apre un menu a discesa che consente di selezionare una delle operazioni seguenti:

- **Elimina**: Elimina l&#39;istanza.
- **Scarica dati** di riepilogo: Scarica un file CSV contenente i dati di riepilogo.
- **Punti** di accesso: Facendo clic sui punteggi *di* Access si ottengono i punteggi di [accesso per l&#39;esercitazione](./download-scores.md)AI di Attribution.
- **Visualizza cronologia** di esecuzione: Viene visualizzato un contenitore contenente un elenco di tutte le esecuzioni del punteggio associate all&#39;istanza del servizio.

![altre azioni](./images/insights/more-actions.png)

## Applicazione di filtri ai dati

Le informazioni approfondite sull&#39;interfaccia utente Attribution consentono di filtrare i dati e aggiornare automaticamente le visualizzazioni dell&#39;interfaccia utente in base ai filtri selezionati.

>[!NOTE] Per impostazione predefinita, ogni filtro è impostato su &quot;All&quot; (Tutti) tranne il filtro del modello ** Attribution, che è impostato su &quot;Incremental and Influenzted Assign Conversion&quot; (Conversioni attribuite incrementali e influenzate).

### Evento di conversione

Quando create una nuova istanza in Attribution AI, uno dei campi obbligatori è &quot;Conversion events&quot; (Eventi di conversione). Gli eventi di conversione sono obiettivi aziendali che identificano l&#39;impatto delle attività di marketing, come gli ordini di e-commerce, gli acquisti in-store e le visite ai siti Web.

Dall&#39;interno dell&#39;istanza, il menu a discesa Eventi *di* conversione consente di selezionare uno degli eventi definiti per l&#39;istanza al fine di filtrare i dati. Selezionando eventi specifici, le visualizzazioni dell&#39;interfaccia utente vengono modificate per compilare solo le conversioni appartenenti a tali eventi.

![Evento conversion](./images/insights/conversion-event.png)

### Modello di attribuzione

Facendo clic su *Attribuzione modello* si apre un menu a discesa con tutti i diversi modelli di attribuzione disponibili. Potete selezionare più modelli per confrontare i risultati. Per ulteriori informazioni sui diversi modelli di attribuzione e sul loro funzionamento, visita la panoramica AI [di](./overview.md) attribuzione, che contiene una tabella con informazioni su ciascun modello.

![modello di attribuzione](./images/insights/attribution-model.png)

### Prodotto

Il filtro *Prodotto* consente di selezionare tra tutti i prodotti che sono stati inizialmente ingeriti nella creazione dell’istanza. Fai clic sul menu a discesa e usa la funzione di ricerca per selezionare rapidamente tutti i prodotti da confrontare.

![products filter](./images/insights/product-filter.png)

### Geografia

Il filtro *Geografia* popola i codici paese in base ai modelli basati su regioni. A seconda dei dati, questo filtro potrebbe essere presente o meno.

>[!NOTE] I codici paese sono lunghi due caratteri. Un elenco completo è disponibile qui [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

### Regione

>[!NOTE] Questo filtro è presente solo se durante la creazione dell’istanza del servizio avete eseguito la modellazione [opzionale basata sull’](./user-guide.md#region-based-modeling-optional) area di passaggio nella guida dell’interfaccia utente AI di Attribution.

Questo filtro consente di selezionare tutte le aree configurate nel processo di creazione dell&#39;istanza.

### Canale

Facendo clic sul filtro *Canale* viene visualizzato un elenco a discesa contenente tutti i canali di marketing disponibili. Potete selezionare più canali per confrontarli.

![Canale](./images/insights/channel.png)

### Intervallo date

Fate clic sull&#39;icona del calendario per aprire il puntatore dell&#39;intervallo di date. Le date dell&#39;evento di conversione iniziale e finale determinano la quantità di dati compilati nell&#39;interfaccia utente. È possibile scegliere di restringere o ampliare l&#39;intervallo di date per rendere attivi o espandere la quantità di dati compilati.

![intervallo date](./images/insights/display-date-range.png)

## Panoramica dei dati

La scheda *Panoramica* mostra le conversioni totali per modello di attribuzione. Il numero totale cambia in base alle specifiche ricerche effettuate utilizzando i filtri precedentemente descritti in questo documento. Selezionando più modelli, alla Panoramica vengono aggiunti altri cerchi, ciascuno dei quali ha un proprio colore corrispondente alla legenda.

![panoramica](./images/insights/Overview.png)

## Tendenze settimanali

La scheda *Tendenze* settimanali suddivide la conversione totale per l&#39;intervallo di date impostato durante il processo di filtraggio.

![trend](./images/insights/weekly-trends.png)

Facendo clic sulle ellissi in alto a destra della scheda delle tendenze ** settimanali viene visualizzato un elenco a discesa che consente di selezionare le tendenze giornaliere, settimanali o mensili.

Quando si passa il puntatore del mouse sulla riga dati di un modello di attribuzione specifico, viene creato un puntatore che mostra il numero totale di conversioni per tale data.

![tendenza](./images/insights/weekly-trend-hover.png)

## Suddivisione per canale

La scheda *Suddivisione per canale* viene utilizzata per determinare il numero totale di conversioni in relazione a ciascun canale. Questa scheda può essere utilizzata per prendere decisioni sull&#39;efficacia di ogni canale e sul ritorno sull&#39;investimento.

![canale di degradazione](./images/insights/channel-breakdown.png)

Facendo clic sulle ellissi in alto a destra della scheda *Suddivisione per canale* , si apre un elenco a discesa che consente di compilare i dati in base ai punti di contatto.

![punti di contatto](./images/insights/breakdown-by-touchpoints.png)

## Campagne principali

La scheda *Campagne* principali visualizza una panoramica delle campagne e delle prestazioni della campagna in ogni canale. Questa scheda può aiutare a informare il team sull&#39;efficacia di una campagna specifica per un determinato canale e fornire indicazioni su dove investire ulteriormente.

![campagne principali](./images/insights/top-campaigns.png)

## Passaggi successivi

Dopo aver filtrato i dati e aver visualizzato le informazioni appropriate, potete accedere ai punteggi. Per una guida dettagliata su come accedere ai punteggi, consulta i punteggi di [accesso nell’esercitazione AI](./download-scores.md) di attribuzione. Inoltre, puoi scaricare i dati di riepilogo come indicato in [più azioni](#more-actions). Se selezionate &quot;Scarica dati di riepilogo&quot;, vengono scaricati i dati di riepilogo aggregati per data.

## Risorse aggiuntive

Il seguente video è stato progettato per aiutare a imparare a utilizzare la pagina di approfondimenti di Attribution AI per comprendere il ROI dei canali e delle campagne di marketing.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)