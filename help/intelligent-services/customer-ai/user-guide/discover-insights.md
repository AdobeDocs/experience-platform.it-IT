---
keywords: Experience Platform;approfondimenti;customer ai;argomenti più comuni;customer ai insights
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Scopri gli approfondimenti con IA per l’analisi dei clienti
description: Questo documento funge da guida per l’interazione con le informazioni approfondite sull’istanza del servizio nell’interfaccia utente di IA per l’analisi dei clienti di Intelligent Services.
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 1%

---

# Scopri informazioni con Customer AI

IA per l’analisi dei clienti, parte di Intelligent Services offre agli esperti di marketing la possibilità di sfruttare Adobe Sensei per anticipare l’azione futura dei clienti. Customer AI viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su grande scala. Ciò avviene senza dover trasformare le esigenze aziendali in un problema di machine learning, scegliendo un algoritmo, una formazione o una distribuzione.

Questo documento funge da guida per l’interazione con le informazioni approfondite sull’istanza del servizio nell’interfaccia utente di IA per l’analisi dei clienti di Intelligent Services.

## Introduzione

Per utilizzare le informazioni per IA per l’analisi dei clienti, è necessario disporre di un’istanza del servizio con uno stato di esecuzione corretto. Per creare una nuova istanza di servizio, visita [Configurazione di un’istanza di Customer AI](./configure.md). Se di recente è stata creata un’istanza del servizio che sta ancora formando e assegnando un punteggio, attendi 24 ore prima del termine dell’esecuzione.

## Panoramica dell’istanza del servizio

In [!DNL Adobe Experience Platform] UI, seleziona **[!UICONTROL Servizi]** nel menu di navigazione a sinistra. Il *Servizi* viene visualizzato il browser e vengono visualizzati i servizi intelligenti disponibili. Nel contenitore di IA per l’analisi dei clienti, seleziona **[!UICONTROL Apri]**.

![Accesso all’istanza](../images/insights/navigate-to-service.png)

Viene visualizzata la pagina del servizio Customer AI. In questa pagina vengono elencate le istanze del servizio di IA per l’analisi dei clienti e vengono visualizzate informazioni su di esse, tra cui il nome dell’istanza, il tipo di propensione, la frequenza di esecuzione dell’istanza e lo stato dell’ultimo aggiornamento.

>[!NOTE]
>
>Solo le istanze del servizio che hanno completato le esecuzioni con punteggio di successo dispongono di approfondimenti.

![Crea istanza](../images/insights/dashboard.png)

Seleziona un nome di istanza del servizio per iniziare.

![Crea istanza](../images/insights/click-the-name.png)

Viene quindi visualizzata la pagina delle informazioni per l’istanza del servizio con l’opzione per selezionare **[!UICONTROL Punteggi più recenti]** o **[!UICONTROL Riepilogo prestazioni]**. Scheda predefinita **[!UICONTROL Punteggi più recenti]** fornisce visualizzazioni dei dati. Le visualizzazioni e ciò che puoi fare con i dati sono spiegati più dettagliatamente in questa guida.

Il **[!UICONTROL Riepilogo prestazioni]** La scheda mostra i tassi di abbandono o di conversione effettivi per ciascun periodo fisso di propensione. Per ulteriori informazioni, consulta la sezione su [metriche di riepilogo delle prestazioni](#performance-metrics).

![pagina di impostazione](../images/insights/landing_page_insights.png)

## Dettagli dell’istanza del servizio

Esistono due modi per visualizzare i dettagli dell’istanza del servizio: dal dashboard o all’interno dell’istanza del servizio.

### Dashboard istanza servizio

Per visualizzare una panoramica dei dettagli dell&#39;istanza del servizio all&#39;interno del dashboard, selezionare un contenitore dell&#39;istanza del servizio, evitando il collegamento ipertestuale associato al nome. Si apre una barra a destra che fornisce ulteriori dettagli. I controlli contengono quanto segue:

- **[!UICONTROL Modifica]**: selezione **[!UICONTROL Modifica]** consente di modificare un’istanza di servizio esistente. Puoi modificare il nome, la descrizione e la frequenza di punteggio dell’istanza.
- **[!UICONTROL Clona]**: selezione **[!UICONTROL Clona]** copia la configurazione dell&#39;istanza del servizio attualmente selezionata. Puoi quindi modificare il flusso di lavoro per apportare modifiche minori e rinominarlo come nuova istanza.
- **[!UICONTROL Elimina]**: puoi eliminare un’istanza del servizio, comprese le esecuzioni storiche.
- **[!UICONTROL Origine dati]**: collegamento al set di dati utilizzato da questa istanza.
- **[!UICONTROL Frequenza di esecuzione]**: quante volte si verifica un’esecuzione di punteggio e quando.
- **[!UICONTROL Definizione punteggio]**: panoramica rapida dell’obiettivo configurato per questa istanza.

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>Se l’esecuzione di un punteggio non riesce, viene visualizzato un messaggio di errore. Il messaggio di errore è elencato in **Dettagli ultima esecuzione** nella barra a destra, visibile solo per le esecuzioni non riuscite.

![messaggio di esecuzione non riuscita](../images/insights/failed-run.png)

### Mostra più informazioni a discesa

Il secondo modo per visualizzare ulteriori dettagli per un’istanza del servizio si trova all’interno della pagina Approfondimenti. Seleziona **[!UICONTROL Mostra altro]** in alto a destra per popolare un elenco a discesa. Vengono elencati dettagli quali la definizione del punteggio, quando è stata creata, il tipo di propensione e i set di dati utilizzati. Per ulteriori informazioni sulle proprietà elencate, visitare il sito [Configurazione di un’istanza di Customer AI](./configure.md).

![mostra altro](../images/insights/landing-show-more.png)

### Popover di anteprima del set di dati di IA per l’analisi dei clienti

Se IA per l’analisi dei clienti utilizza più di un set di dati, un collegamento ipertestuale con etichetta **[!UICONTROL Più]** seguito dal numero di set di dati tra parentesi `()` viene fornito.

![più set di dati](../images/insights/insights-multi-datasets.png)

Selezionando il collegamento più set di dati si apre il popover di anteprima del set di dati di IA per l’analisi dei clienti. Ogni colore nell’anteprima rappresenta un set di dati come mostrato dalla chiave colore a sinistra delle colonne del set di dati. In questo esempio, è possibile vedere solo **Set di dati 1** contiene `PROP1` colonna.

![mostra altro](../images/insights/dataset-preview.png)

### Modificare un’istanza

Per modificare un’istanza, seleziona **[!UICONTROL Modifica]** nella navigazione in alto a destra.

![fai clic sul pulsante modifica](../images/insights/edit-button.png)

Viene visualizzata la finestra di dialogo di modifica, che consente di modificare il nome, la descrizione, lo stato e la frequenza di punteggio dell’istanza. Per confermare le modifiche e chiudere la finestra di dialogo, seleziona **[!UICONTROL Salva]** in basso a destra.

![modifica popover](../images/insights/edit-instance.png)

### Altre azioni

Il **[!UICONTROL Altre azioni]** si trova nella navigazione in alto a destra accanto a **[!UICONTROL Modifica]**. Selezione **[!UICONTROL Altre azioni]** apre un menu a discesa che consente di selezionare una delle seguenti operazioni:

- **[!UICONTROL Clona]**: selezione **[!UICONTROL Clona]** copia la configurazione dell’istanza del servizio. Puoi quindi modificare il flusso di lavoro per apportare modifiche minori e rinominarlo come nuova istanza.
- **[!UICONTROL Elimina]**: elimina l’istanza.
- **[!UICONTROL Punteggi di accesso]**: selezione **[!UICONTROL Punteggi di accesso]** apre una finestra di dialogo che fornisce un collegamento al [download dei punteggi per IA per l’analisi dei clienti](./download-scores.md) tutorial, la finestra di dialogo fornisce anche l’id del set di dati necessario per effettuare chiamate API.
- **[!UICONTROL Visualizza cronologia di esecuzione]**: viene visualizzata una finestra di dialogo contenente un elenco di tutte le esecuzioni di punteggio associate all’istanza del servizio.

![altre azioni](../images/insights/more-actions.png)

## Riepilogo punteggio {#scoring-summary}

Il riepilogo del punteggio mostra il numero totale di profili con punteggio e li classifica in contenitori contenenti propensione alta, media e bassa. I bucket di propensione sono determinati in base all’intervallo di punteggio, il valore basso è inferiore a 24, il valore medio è compreso tra 25 e 74 e il valore alto è superiore a 74. Ogni bucket ha un colore corrispondente alla legenda.

>[!NOTE]
>
>Se si tratta di un punteggio di propensione alla conversione, i punteggi alti vengono visualizzati in verde e i punteggi bassi in rosso. Se prevedi una propensione all’abbandono, questo viene capovolto, i punteggi alti sono in rosso e i punteggi bassi in verde. Il bucket medio rimane giallo indipendentemente dal tipo di propensione scelto.

![riepilogo punteggio](../images/insights/scoring-summary.png)

Puoi passare il cursore del mouse su qualsiasi colore dell’anello per visualizzare informazioni aggiuntive, ad esempio la percentuale e il numero totale di profili appartenenti a un bucket.

![](../images/insights/scoring-ring.png)

## Distribuzione dei punteggi

Il **[!UICONTROL Distribuzione dei punteggi]** La scheda ti fornisce un riepilogo visivo della popolazione in base al punteggio. I colori visualizzati nel [!UICONTROL Distribuzione dei punteggi] rappresenta il tipo di punteggio tendenza generato. Passando il puntatore del mouse su una delle distribuzioni di punteggio, viene visualizzato il conteggio esatto che appartiene a tale distribuzione.

![distribuzione dei punteggi](../images/insights/distribution-of-scores.png)

## Fattori di influenza

Per ogni bucket di punteggio, viene generata una scheda che mostra i primi 10 fattori influenti per tale bucket. I fattori influenti forniscono ulteriori dettagli sul motivo per cui i clienti appartengono a vari bucket di punteggio.

![Fattori di influenza](../images/insights/influential-factors.png)

### Espansioni dei fattori di influenza

Passando il puntatore del mouse su uno qualsiasi dei principali fattori influenti i dati vengono ulteriormente suddivisi. Viene fornita una panoramica del motivo per cui alcuni profili appartengono a un bucket di propensione. A seconda del fattore, è possibile che vengano forniti valori numerici, categorici o booleani. L’esempio seguente visualizza i valori categorici per regione.

![schermata di approfondimento](../images/insights/drilldown.png)

Inoltre, utilizzando i drill-down, puoi confrontare un fattore di distribuzione se si verifica in due o più bucket di propensione e creare segmenti più specifici con questi valori. L’esempio seguente illustra il primo caso d’uso:

![](../images/insights/drilldown-compare.png)

Puoi notare che i profili con bassa propensione alla conversione hanno meno probabilità di aver effettuato una visita recente alle pagine web adobe.com. Il fattore &quot;Giorni dall’ultima visita web&quot; ha una copertura solo dell’8% rispetto al 26% nei profili a media propensione. Utilizzando questi numeri, puoi confrontare la distribuzione del fattore all’interno di ciascun bucket. Queste informazioni possono essere utilizzate per dedurre che l’attualità in webvisit non è influente tanto nel bucket di bassa propensione quanto nel bucket di media propensione.

### Crea un segmento

Selezione del **[!UICONTROL Crea segmento]** in qualsiasi bucket per propensione bassa, media e alta ti reindirizza al generatore di segmenti.

>[!NOTE]
>
>Il **[!UICONTROL Crea segmento]** Questo pulsante è disponibile solo se Real-Time Customer Profile è abilitato per il set di dati. Per ulteriori informazioni su come abilitare Real-Time Customer Profile, visita [Panoramica del profilo cliente in tempo reale](../../../rtcdp/overview.md).

![Fai clic su Crea segmento.](../images/insights/influential-factors-create-segment.png)

![Crea un segmento](../images/insights/create-segment.png)

Il generatore di segmenti viene utilizzato per definire un segmento. Durante la selezione **[!UICONTROL Crea segmento]** Dalla pagina Insights, IA per l’analisi dei clienti aggiunge automaticamente le informazioni sui bucket selezionati al segmento. Per completare la creazione del segmento, compila il **Nome** e **Descrizione** si trovano nella barra a destra dell’interfaccia utente di segment builder. Dopo aver assegnato al segmento un nome e una descrizione, seleziona **[!UICONTROL Salva]** in alto a destra.

>[!NOTE]
>
>Poiché i punteggi di tendenza vengono scritti nel singolo profilo, sono disponibili nel Generatore di segmenti come qualsiasi altro attributo di profilo. Quando passi al Generatore di segmenti per creare nuovi segmenti, puoi visualizzare tutti i vari punteggi di tendenza nello spazio dei nomi IA per l’analisi dei clienti.

![Segment fill in](../images/insights/segment-saving.png)

Per visualizzare il nuovo segmento nell’interfaccia utente di Platform, seleziona **[!UICONTROL Segmenti]** nel menu di navigazione a sinistra. Il **[!UICONTROL Sfoglia]** viene visualizzata la pagina, con tutti i segmenti disponibili.

![Tutti i tuoi segmenti](../images/insights/Segments-dashboard.png)

## Prestazioni storiche {#historical-performance}

Il **[!UICONTROL Riepilogo prestazioni]** La scheda mostra i tassi di abbandono o di conversione effettivi, separati in ciascuno dei bucket di propensione valutati da IA per l’analisi dei clienti.

![Scheda Riepilogo prestazioni](../images/insights/summary_tab.png)

Inizialmente vengono visualizzate solo le tariffe previste (linee tratteggiate). Le percentuali previste vengono visualizzate quando non si è verificata un’esecuzione di punteggio e i dati non sono ancora disponibili. Tuttavia, una volta superata una finestra di risultati, il tasso previsto viene sostituito con un tasso effettivo (linea continua).

Passando il puntatore del mouse sulle righe vengono visualizzati la data e il tasso effettivo/previsto per quel giorno in quel periodo fisso.

![Esempio di bucket](../images/insights/churn_tab.png)

Puoi filtrare l’intervallo di tempo per la frequenza prevista ed effettiva visualizzata. Seleziona la **icona calendario** ![icona](../images/insights/calendar_icon.png)quindi seleziona un nuovo intervallo di date. I risultati in ciascun bucket vengono aggiornati per essere visualizzati entro il nuovo intervallo di date.

![Selettore data](../images/insights/date_selector.png)

### Percentuali di esecuzione del punteggio individuale

La metà inferiore del **[!UICONTROL Riepilogo prestazioni]** Nella scheda vengono visualizzati i risultati per ogni singola esecuzione di punteggio. Seleziona la data a discesa in alto a destra per visualizzare i risultati per un’esecuzione di punteggio diversa.

A seconda che si preveda l’abbandono o la conversione, il [!UICONTROL Distribuzione dei punteggi] grafico mostra la distribuzione dei profili abbandonati/convertiti e non abbandonati/non convertiti in ogni incremento.

![punteggio individuale](../images/insights/scoring_tab.png)

## Valutazione del modello {#model-evaluation}

Oltre a tenere traccia nel tempo dei risultati previsti ed effettivi nella scheda Prestazioni storiche, gli addetti al marketing dispongono di una maggiore trasparenza sulla qualità del modello nella scheda Valutazione modello. È possibile utilizzare i grafici Incremento e Guadagno per determinare le differenze nell&#39;utilizzo di un modello predittivo rispetto al targeting casuale. Inoltre, è in grado di determinare quanti risultati positivi verrebbero acquisiti a ogni cut-off di punteggio. Ciò è utile per la segmentazione e per allineare il ritorno sull’investimento con le azioni di marketing.

### Grafico lift

![grafico lift](../images/user-guide/lift-chart.png)

Il grafico lift misura il miglioramento nell’utilizzo di un modello predittivo invece del targeting casuale.

Gli indicatori dei modelli di alta qualità includono:

- Valori elevati di incremento nei primi decili. Ciò significa che il modello è in grado di identificare gli utenti con la maggiore propensione a intraprendere l’azione di interesse.
- Valori di incremento decrescenti. Ciò significa che i clienti con punteggi più alti hanno più probabilità di intraprendere l’azione di interesse rispetto alle persone con punteggi più bassi.

### Grafico dei guadagni

![grafico guadagni](../images/user-guide/gains-chart.png)

Il grafico dei guadagni cumulativi misura la percentuale di risultati positivi rilevati con punteggi al di sopra di una certa soglia. Dopo aver ordinato i clienti in base al punteggio di tendenza da alto a basso, la popolazione è divisa in decili - 10 gruppi di uguali dimensioni. Un modello perfetto catturerebbe tutti i risultati positivi nei decili con il punteggio più alto. Un metodo di targeting casuale di base acquisisce risultati positivi in proporzione alle dimensioni del gruppo: il targeting del 30% degli utenti catturerebbe il 30% dei risultati.

Gli indicatori dei modelli di alta qualità includono:

- I guadagni cumulativi si avvicinano rapidamente al 100%.
- La curva dei guadagni cumulativi per il modello è più vicina all&#39;angolo superiore sinistro del grafico.
- Il grafico dei guadagni cumulativi può essere utilizzato per determinare i limiti di punteggio per la segmentazione e il targeting. Ad esempio, se il modello acquisisce il 70% dei risultati positivi nei primi 2 decili di punteggio, il targeting degli utenti con PercentileScore > 80 dovrebbe acquisire circa il 70% dei risultati positivi.

### AUC (area sotto la curva)

L’AUC riflette la forza della relazione tra la classificazione per punteggio e il verificarsi dell’obiettivo previsto. Un **AUC** 0,5 significa che il modello non è migliore di una stima casuale. Un **AUC** di 1 significa che il modello è in grado di prevedere perfettamente chi intraprenderà l’azione pertinente.

## Passaggi successivi

Questo documento illustra le informazioni fornite da un’istanza del servizio Customer AI. Ora puoi continuare l’esercitazione su [download di punteggi in Customer AI](./download-scores.md) o sfogliare l&#39;altro [Adobe Intelligent Services](../../home.md) guide offerte.

## Risorse aggiuntive

Il video seguente illustra come utilizzare IA per l’analisi dei clienti per visualizzare l’output dei modelli e dei fattori influenti.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)
