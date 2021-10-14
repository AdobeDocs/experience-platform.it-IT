---
keywords: Experience Platform;approfondimenti;customer ai;argomenti popolari;approfondimenti sull'ai clienti
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Scopri informazioni approfondite con Customer AI
topic-legacy: Discovering insights
description: Questo documento funge da guida per interagire con le informazioni sulle istanze del servizio nell’interfaccia utente di Intelligent Services Customer AI.
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '1632'
ht-degree: 1%

---

# Scopri informazioni approfondite con Customer AI

Customer AI, come parte di Intelligent Services, fornisce agli addetti al marketing il potere di sfruttare Adobe Sensei per anticipare quali saranno le prossime azioni dei clienti. Customer AI viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su grande scala. Ciò viene realizzato senza dover trasformare le esigenze aziendali in un problema di apprendimento automatico, scegliendo un algoritmo, una formazione o un&#39;implementazione.

Questo documento funge da guida per interagire con le informazioni sulle istanze del servizio nell’interfaccia utente di Intelligent Services Customer AI.

## Introduzione

Per utilizzare le informazioni per Customer AI, è necessario disporre di un’istanza di servizio con uno stato di esecuzione riuscito. Per creare una nuova istanza di servizio, visita [Configurazione di un&#39;istanza di Customer AI](./configure.md). Se hai creato di recente un&#39;istanza di servizio ed è ancora in fase di formazione e valutazione, ti preghiamo di consentire 24 ore per il completamento dell&#39;esecuzione.

## Panoramica dell&#39;istanza del servizio

Nell&#39;interfaccia utente [!DNL Adobe Experience Platform], fai clic su **[!UICONTROL Servizi]** nel menu di navigazione a sinistra. Viene visualizzato il browser *Servizi* e vengono visualizzati i servizi intelligenti disponibili. Nel contenitore per Customer AI, fai clic su **[!UICONTROL Apri]**.

![Accesso all’istanza](../images/insights/navigate-to-service.png)

Viene visualizzata la pagina del servizio Customer AI. In questa pagina sono elencate le istanze di servizio di Customer AI e vengono visualizzate informazioni su di esse, tra cui il nome dell’istanza, il tipo di propensione, la frequenza di esecuzione dell’istanza e lo stato dell’ultimo aggiornamento.

>[!NOTE]
>
>Solo le istanze del servizio che hanno completato con successo le esecuzioni con punteggio dispongono di informazioni approfondite.

![Crea istanza](../images/insights/dashboard.png)

Seleziona un nome di istanza del servizio da iniziare.

![Crea istanza](../images/insights/click-the-name.png)

Successivamente, viene visualizzata la pagina delle informazioni per l&#39;istanza del servizio con l&#39;opzione per selezionare **[!UICONTROL Punteggi più recenti]** o **[!UICONTROL Riepilogo delle prestazioni]**. La scheda predefinita **[!UICONTROL Ultimi punteggi]** fornisce visualizzazioni dei tuoi dati. Le visualizzazioni e le operazioni che puoi eseguire con i dati sono descritte più dettagliatamente in questa guida.

La scheda **[!UICONTROL Riepilogo prestazioni]** mostra i tassi di abbandono o di conversione effettivi per ciascun intervallo di propensione. Per ulteriori informazioni, consulta la sezione sulle [metriche di riepilogo delle prestazioni](#performance-metrics).

![pagina di configurazione](../images/insights/landing_page_insights.png)

### Dettagli istanza servizio

Esistono due modi per visualizzare i dettagli dell’istanza del servizio: dal dashboard o all&#39;interno dell&#39;istanza del servizio.

Per visualizzare una panoramica dei dettagli dell&#39;istanza del servizio all&#39;interno del dashboard, selezionare un contenitore di istanza del servizio, evitando il collegamento ipertestuale associato al nome. Viene visualizzata la barra a destra con ulteriori dettagli. I controlli contengono i seguenti elementi:

- **[!UICONTROL Modifica]**: Selezionando  **** Modifica puoi modificare un’istanza di servizio esistente. Puoi modificare il nome, la descrizione e la frequenza di punteggio dell’istanza.
- **[!UICONTROL Clona]**: Selezionando  **** Copia l&#39;istanza di servizio attualmente selezionata. Puoi quindi modificare il flusso di lavoro per apportare modifiche minori e rinominarlo come nuova istanza.
- **[!UICONTROL Elimina]**: Puoi eliminare un’istanza di servizio, comprese eventuali esecuzioni cronologiche.
- **[!UICONTROL Origine]** dati: Un collegamento al set di dati utilizzato da questa istanza.
- **[!UICONTROL Esegui frequenza]**: Con quale frequenza e quando si svolge un’esecuzione del punteggio.
- **[!UICONTROL Definizione]** punteggio: Panoramica rapida dell’obiettivo configurato per questa istanza.

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>Se un’esecuzione del punteggio non riesce, viene visualizzato un messaggio di errore. Il messaggio di errore è elencato in **Dettagli ultima esecuzione** nella barra a destra, visibile solo per le esecuzioni non riuscite.

![messaggio di esecuzione non riuscito](../images/insights/failed-run.png)

Il secondo modo per visualizzare dettagli aggiuntivi per un’istanza di servizio si trova nella pagina approfondimenti. Per compilare un elenco a discesa, fai clic su **[!UICONTROL Mostra altro]** in alto a destra. Sono elencati i dettagli, ad esempio la definizione del punteggio, la data di creazione e il tipo di propensione. Per ulteriori informazioni su una delle proprietà elencate, visita [Configurazione di un&#39;istanza di Customer AI](./configure.md).

![mostrare di più](../images/insights/landing-show-more.png)

![mostrare di più](../images/insights/show-more.png)

### Modificare un’istanza

Per modificare un&#39;istanza, fai clic su **[!UICONTROL Modifica]** nella navigazione in alto a destra.

![fai clic sul pulsante modifica](../images/insights/edit-button.png)

Viene visualizzata la finestra di dialogo di modifica, che consente di modificare il nome, la descrizione, lo stato e la frequenza di punteggio dell’istanza. Per confermare le modifiche e chiudere la finestra di dialogo, seleziona **[!UICONTROL Salva]** nell’angolo in basso a destra.

![pozzo di modifica](../images/insights/edit-instance.png)

### Altre azioni

Il pulsante **[!UICONTROL Altre azioni]** si trova nella navigazione in alto a destra accanto a **[!UICONTROL Modifica]**. Facendo clic su **[!UICONTROL Altre azioni]** si apre un menu a discesa che consente di selezionare una delle seguenti operazioni:

- **[!UICONTROL Clona]**: Selezionando  **** Copia l&#39;istanza del servizio impostata. Puoi quindi modificare il flusso di lavoro per apportare modifiche minori e rinominarlo come nuova istanza.
- **[!UICONTROL Elimina]**: Elimina l’istanza.
- **[!UICONTROL Punteggi]** di accesso: Selezionando  **[!UICONTROL i]** punteggi di accesso si apre una finestra di dialogo che fornisce un collegamento ai punteggi di  [download per l’](./download-scores.md) esercitazione di Customer AI, la finestra di dialogo fornisce anche l’ID set di dati necessario per effettuare chiamate API.
- **[!UICONTROL Visualizzare la cronologia]** di esecuzione: Viene visualizzata una finestra di dialogo contenente un elenco di tutte le esecuzioni del punteggio associate all’istanza del servizio.

![altre azioni](../images/insights/more-actions.png)

## Riepilogo del punteggio {#scoring-summary}

Riepilogo del punteggio visualizza il numero totale di profili con punteggio e li classifica in blocchi contenenti propensione alta, media e bassa. I periodi fissi di propensione sono determinati in base all’intervallo di punteggio, il valore basso è inferiore a 24, il valore medio è compreso tra 25 e 74 e il valore alto è superiore a 74. Ogni bucket ha un colore corrispondente alla legenda.

>[!NOTE]
>
>Se si tratta di un punteggio di propensione di conversione, i punteggi elevati sono visualizzati in verde e i punteggi bassi in rosso. Se prevedi la propensione di abbandono questo viene capovolto, i punteggi alti sono in rosso e i punteggi bassi sono verdi. Il bucket medio rimane giallo indipendentemente dal tipo di propensione scelto.

![riepilogo del punteggio](../images/insights/scoring-summary.png)

Passa il cursore del mouse su un colore dell’anello per visualizzare informazioni aggiuntive, ad esempio una percentuale e un numero totale di profili appartenenti a un bucket.

![](../images/insights/scoring-ring.png)

## Distribuzione dei punteggi

La scheda **[!UICONTROL Distribuzione di punteggi]** fornisce un riepilogo visivo della popolazione in base al punteggio. I colori visualizzati nella scheda [!UICONTROL Distribuzione di punteggi] rappresentano il tipo di punteggio di propensione generato. Passando il puntatore del mouse su una delle distribuzioni di punteggio, viene fornito il conteggio esatto appartenente a tale distribuzione.

![distribuzione dei punteggi](../images/insights/distribution-of-scores.png)

## Fattori influenti

Per ogni bucket di punteggio, viene generata una scheda che mostra i primi 10 fattori influenti per tale bucket. I fattori influenti ti forniscono ulteriori dettagli sul motivo per cui i tuoi clienti appartengono a vari periodi fissi di valutazione.

![Fattori influenti](../images/insights/influential-factors.png)

### Perdita di fattori influenti

Passando il puntatore del mouse su uno dei principali fattori influenti, i dati vengono ulteriormente suddivisi. Viene fornita una panoramica del motivo per cui alcuni profili appartengono a un bucket di propensione. A seconda del fattore, è possibile assegnare valori numerici, categorici o booleani. Nell’esempio seguente vengono visualizzati i valori categorici per regione.

![schermata di drilldown](../images/insights/drilldown.png)

Inoltre, utilizzando i drill-down, puoi confrontare un fattore di distribuzione se si verifica in due o più bucket di propensione e creare segmenti più specifici con questi valori. L’esempio seguente illustra il primo caso d’uso:

![](../images/insights/drilldown-compare.png)

Puoi notare che i profili con bassa propensione alla conversione hanno meno probabilità di aver effettuato una visita recente alle pagine web adobe.com. Il fattore &quot;Giorni dall’ultima visita web&quot; ha una copertura solo dell’8% rispetto al 26% nei profili di propensione medi. Utilizzando questi numeri, puoi confrontare la distribuzione all’interno di ciascun bucket per il fattore. Queste informazioni possono essere utilizzate per dedurre che la recency nella visita web non è così influente nel bucket di bassa propensione, come è nel secchio di media propensione.

### Creare un segmento

Selezionando il pulsante **[!UICONTROL Crea segmento]** in uno qualsiasi dei bucket per una propensione bassa, media e alta, si reindirizza al generatore di segmenti.

>[!NOTE]
>
>Il pulsante **[!UICONTROL Crea segmento]** è disponibile solo se per il set di dati è abilitato Profilo cliente in tempo reale. Per ulteriori informazioni su come abilitare il profilo cliente in tempo reale, visita la [Panoramica sul profilo cliente in tempo reale](../../../rtcdp/overview.md).

![Fai clic su Crea segmento](../images/insights/influential-factors-create-segment.png)

![Creare un segmento](../images/insights/create-segment.png)

Il generatore di segmenti viene utilizzato per definire un segmento. Quando selezioni **[!UICONTROL Crea segmento]** dalla pagina Approfondimenti , Customer AI aggiunge automaticamente le informazioni sui bucket selezionati al segmento. Per completare la creazione del segmento, è sufficiente compilare i contenitori *Name* e *Description* nella barra a destra dell’interfaccia utente del generatore di segmenti. Dopo aver assegnato un nome e una descrizione al segmento, fai clic su **[!UICONTROL Salva]** in alto a destra.

>[!NOTE]
>
>Poiché i punteggi di propensione sono scritti sul singolo profilo, sono disponibili nel Generatore di segmenti come qualsiasi altro attributo di profilo. Quando visiti il Generatore di segmenti per creare nuovi segmenti, puoi visualizzare tutti i vari punteggi di propensione nello spazio dei nomi Customer AI.

![Riempimento del segmento](../images/insights/segment-saving.png)

Per visualizzare il nuovo segmento nell’interfaccia utente di Platform, fai clic su **[!UICONTROL Segmenti]** nel menu di navigazione a sinistra. Viene visualizzata la pagina **[!UICONTROL Sfoglia]** che visualizza tutti i segmenti disponibili.

![Tutti i segmenti](../images/insights/Segments-dashboard.png)

## Metriche di riepilogo delle prestazioni {#performance-metrics}

La scheda **[!UICONTROL Riepilogo delle prestazioni]** mostra i tassi di abbandono o di conversione effettivi, separati in ciascuno dei periodi di tendenza valutati da Customer AI.

![Scheda Riepilogo prestazioni](../images/insights/summary_tab.png)

Inizialmente vengono visualizzate solo le percentuali previste (linee tratteggiate). Le percentuali previste vengono visualizzate quando non si è verificata un’esecuzione del punteggio e i dati non sono ancora disponibili. Tuttavia, una volta superato un intervallo di risultati, il tasso previsto viene sostituito da un tasso effettivo (linea continua).

Passando il puntatore del mouse sopra le righe viene visualizzata la data e il tasso effettivo/previsto per quel giorno nel periodo fisso.

![Esempio di bucket](../images/insights/churn_tab.png)

Puoi filtrare l’intervallo di tempo per la visualizzazione dei tassi previsti ed effettivi. Seleziona l&#39;icona **Calendario** ![icona](../images/insights/calendar_icon.png)e seleziona un nuovo intervallo di date. I risultati in ciascuno dei bucket vengono aggiornati per essere visualizzati all’interno del nuovo intervallo di date.

![Selettore data](../images/insights/date_selector.png)

### Tassi di esecuzione dei punteggi individuali

Nella parte inferiore della scheda **[!UICONTROL Riepilogo prestazioni]** vengono visualizzati i risultati per ogni singola esecuzione del punteggio. Seleziona la data a discesa in alto a destra per visualizzare i risultati di una diversa esecuzione del punteggio.

A seconda che si preveda un abbandono o una conversione, il grafico [!UICONTROL Distribuzione di punteggi] mostra la distribuzione dei profili eseguiti/convertiti e non eseguiti/non convertiti in ogni incremento.

![punteggio individuale](../images/insights/scoring_tab.png)

## Passaggi successivi

Questo documento descrive le informazioni fornite da un&#39;istanza del servizio Customer AI. È ora possibile continuare l&#39;esercitazione su [download dei punteggi in Customer AI](./download-scores.md) oppure sfogliare le altre guide [Adobe Intelligent Services](../../home.md) offerte.

## Risorse aggiuntive

Il video seguente illustra come utilizzare Customer AI per vedere l’output dei modelli e dei fattori influenti.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)
