---
keywords: Experience Platform;insights;customer ai;popular topics;customer ai insights
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Scopri informazioni approfondite con l'AI del cliente
topic: Discovering insights
description: Questo documento funge da guida per l'interazione con le informazioni sulle istanze del servizio nell'interfaccia utente AI del cliente di Servizi intelligenti.
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 1%

---


# Scopri informazioni approfondite con l&#39;AI del cliente

L&#39;AI del cliente, come parte di Intelligent Services, fornisce agli esperti di marketing la possibilità di sfruttare  Adobe Sensei per anticipare quali saranno le prossime azioni da intraprendere per i clienti. Customer AI viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su grande scala. Ciò è possibile senza dover trasformare le esigenze aziendali in un problema di machine learning, scegliendo un algoritmo, una formazione o un&#39;implementazione.

Questo documento funge da guida per l&#39;interazione con le informazioni sulle istanze del servizio nell&#39;interfaccia utente AI del cliente di Servizi intelligenti.

## Introduzione

Per utilizzare le informazioni per l&#39;AI cliente, è necessario disporre di un&#39;istanza di servizio con uno stato di esecuzione riuscito. Per creare una nuova istanza di servizio, visita [Configurazione di un&#39;istanza](./configure.md)di AI cliente. Se avete creato di recente un&#39;istanza di servizio che continua a essere formativa e valutazione, lasciate 24 ore per completare l&#39;esecuzione.

## Panoramica dell’istanza del servizio

Nell’ [!DNL Adobe Experience Platform] interfaccia utente, fate clic **[!UICONTROL Services]** nel menu di navigazione a sinistra. Viene visualizzato il browser *Servizi* , che presenta i servizi intelligenti disponibili. Nel contenitore per l&#39;API cliente, fate clic su **[!UICONTROL Open]**.

![Accesso all’istanza](../images/insights/navigate-to-service.png)

Viene visualizzata la pagina del servizio AI del cliente. In questa pagina sono elencate le istanze di servizio dell&#39;API cliente e vengono visualizzate informazioni su di esse, incluso il nome dell&#39;istanza, il tipo di propensione, la frequenza di esecuzione dell&#39;istanza e lo stato dell&#39;ultimo aggiornamento.

>[!NOTE]
>
>Sono disponibili informazioni approfondite solo le istanze del servizio che hanno completato con successo l’esecuzione del punteggio.

![Crea istanza](../images/insights/dashboard.png)

Fate clic sul nome di un&#39;istanza di servizio per iniziare.

![Crea istanza](../images/insights/click-the-name.png)

Viene quindi visualizzata la pagina delle informazioni relative all’istanza del servizio in cui vengono fornite le visualizzazioni dei dati. Le visualizzazioni e le operazioni che puoi eseguire con i dati sono descritte più dettagliatamente in questa guida.

![pagina di configurazione](../images/insights/landing-page.png)


### Dettagli dell&#39;istanza del servizio

Esistono due modi per visualizzare i dettagli dell’istanza del servizio: dal dashboard o all&#39;interno dell&#39;istanza del servizio.

Per visualizzare una panoramica dei dettagli dell&#39;istanza del servizio all&#39;interno del dashboard, selezionate un contenitore di istanza del servizio, evitando il collegamento ipertestuale associato al nome. Si apre una barra laterale destra con dettagli aggiuntivi. I controlli contengono le seguenti informazioni:

- **[!UICONTROL Edit]**: La selezione **[!UICONTROL Edit]** consente di modificare un&#39;istanza di servizio esistente. Potete modificare il nome, la descrizione e la frequenza di punteggio dell’istanza.
- **[!UICONTROL Clone]**: Selezionando **[!UICONTROL Clone]** copia l&#39;istanza di servizio attualmente selezionata. Potete quindi modificare il flusso di lavoro per apportare modifiche minori e rinominarlo come nuova istanza.
- **[!UICONTROL Delete]**: È possibile eliminare un&#39;istanza di servizio, comprese eventuali esecuzioni cronologiche.
- **[!UICONTROL Data source]**: Un collegamento al set di dati utilizzato da questa istanza.
- **[!UICONTROL Run Frequency]**: Con quale frequenza si svolge e quando viene eseguito un punteggio.
- **[!UICONTROL Score definition]**: Panoramica rapida dell’obiettivo configurato per l’istanza.

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>Nel caso in cui un&#39;esecuzione del punteggio non riesca, viene visualizzato un messaggio di errore. Il messaggio di errore è elencato in Dettagli **dell&#39;** ultima esecuzione nella barra a destra, visibile solo per le esecuzioni non riuscite.

![messaggio di esecuzione non riuscito](../images/insights/failed-run.png)

Il secondo modo per visualizzare i dettagli aggiuntivi per un’istanza di servizio si trova nella pagina delle informazioni. Puoi fare clic **[!UICONTROL Show more]** in alto a destra per compilare un elenco a discesa. Vengono elencati i dettagli, ad esempio la definizione del punteggio, la data di creazione e il tipo di propensione. Per ulteriori informazioni su una delle proprietà elencate, visita [Configurazione di un&#39;istanza](./configure.md)di AI del cliente.

![mostra di più](../images/insights/landing-show-more.png)

![mostra di più](../images/insights/show-more.png)

### Modificare un’istanza

Per modificare un&#39;istanza, fate clic **[!UICONTROL Edit]** nella barra di navigazione in alto a destra.

![fare clic sul pulsante Modifica](../images/insights/edit-button.png)

Viene visualizzata la finestra di dialogo di modifica, che consente di modificare il nome, la descrizione, lo stato e la frequenza di punteggio dell’istanza. Per confermare le modifiche e chiudere la finestra di dialogo, selezionate **[!UICONTROL Save]** nell’angolo inferiore destro.

![edit pover](../images/insights/edit-instance.png)

### Altre azioni

Il **[!UICONTROL More actions]** pulsante si trova nella barra di navigazione in alto a destra accanto a **[!UICONTROL Edit]**. Facendo clic **[!UICONTROL More actions]** si apre un menu a discesa che consente di selezionare una delle operazioni seguenti:

- **[!UICONTROL Clone]**: Selezionando **[!UICONTROL Clone]** copia la configurazione dell&#39;istanza del servizio. Potete quindi modificare il flusso di lavoro per apportare modifiche minori e rinominarlo come nuova istanza.
- **[!UICONTROL Delete]**: Elimina l&#39;istanza.
- **[!UICONTROL Access scores]**: Selezionando **[!UICONTROL Access scores]** si apre una finestra di dialogo che fornisce un collegamento ai punteggi di [download per l&#39;esercitazione AI](./download-scores.md) del cliente, la finestra di dialogo fornisce anche l&#39;ID del set di dati necessario per effettuare chiamate API.
- **[!UICONTROL View run history]**: Viene visualizzata una finestra di dialogo contenente un elenco di tutte le esecuzioni del punteggio associate all&#39;istanza del servizio.

![altre azioni](../images/insights/more-actions.png)

## Riepilogo punteggio {#scoring-summary}

Il riepilogo del punteggio visualizza il numero totale di profili con punteggio e li classifica in bucket contenenti propensione alta, media e bassa. I periodi fissi di propensione sono determinati in base all&#39;intervallo di punteggio, il valore basso è inferiore a 24, il valore medio è compreso tra 25 e 74 e il valore massimo è superiore a 74. Ogni intervallo ha un colore corrispondente alla legenda.

>[!NOTE]
>
>Se si tratta di un punteggio di propensione alla conversione, i punteggi alti sono visualizzati in verde e i punteggi bassi in rosso. Se si prevede la propensione del churn questo è capovolto, i punteggi alti sono in rosso e i punteggi bassi sono in verde. Il bucket medio rimane giallo indipendentemente dal tipo di propensione scelto.

![riepilogo punteggio](../images/insights/scoring-summary.png)

Puoi passare il cursore del mouse su un colore dell&#39;anello per visualizzare informazioni aggiuntive, ad esempio una percentuale e un numero totale di profili appartenenti a un bucket.

![](../images/insights/scoring-ring.png)

## Distribuzione dei punteggi

La **[!UICONTROL Distribution of Scores]** scheda fornisce un riepilogo visivo della popolazione in base al punteggio. I colori visualizzati nella [!UICONTROL Distribution of Scores] scheda rappresentano il tipo di punteggio di propensione generato. Quando si passa il puntatore del mouse su una delle distribuzioni del punteggio, viene visualizzato il conteggio esatto che appartiene a tale distribuzione.

![distribuzione dei punteggi](../images/insights/distribution-of-scores.png)

## Fattori di influenza

Per ogni intervallo di punteggio, viene generata una scheda che mostra i primi 10 fattori influenti per tale intervallo. I fattori influenti forniscono ulteriori dettagli sul motivo per cui i clienti appartengono a vari periodi fissi di valutazione.

![Fattori di influenza](../images/insights/influential-factors.png)

### Perdite di fattori influenti

Passando il puntatore del mouse su uno dei principali fattori influenti, i dati vengono ulteriormente suddivisi. Viene fornita una panoramica del motivo per cui alcuni profili appartengono a un intervallo di propensione. A seconda del fattore, è possibile assegnare valori numerici, categorici o booleani. Nell&#39;esempio seguente vengono visualizzati i valori categorici per regione.

![screenshot](../images/insights/drilldown.png)

Inoltre, utilizzando le drilldowns, puoi confrontare un fattore di distribuzione se si verifica in due o più bucket di propensione e creare segmenti più specifici con questi valori. L’esempio seguente illustra il primo caso di utilizzo:

![](../images/insights/drilldown-compare.png)

Potete vedere che i profili con bassa propensione alla conversione hanno meno probabilità di aver effettuato una visita recente alle pagine Web adobe.com. Il fattore &quot;Giorni dall&#39;ultima visita Web&quot; ha una copertura solo dell&#39;8% rispetto al 26% nei profili di probabilità media. Utilizzando questi numeri, è possibile confrontare la distribuzione all&#39;interno di ciascun bucket per il fattore. Queste informazioni possono essere utilizzate per dedurre che la recency in webvisit non è così influente nel periodo fisso di bassa propensione, come è nel periodo fisso di media propensione.

### Creazione di un segmento

Se si seleziona il **[!UICONTROL Create Segment]** pulsante in uno dei periodi fissi per una propensione bassa, media e alta, si viene reindirizzati al generatore di segmenti.

>[!NOTE]
>
>Il **[!UICONTROL Create Segment]** pulsante è disponibile solo se per il set di dati è abilitato il profilo cliente in tempo reale. Per ulteriori informazioni su come abilitare il profilo cliente in tempo reale, consulta la panoramica [sul profilo cliente in tempo](../../../rtcdp/overview.md)reale.

![Fai clic su Crea segmento](../images/insights/influential-factors-create-segment.png)

![Creazione di un segmento](../images/insights/create-segment.png)

Il generatore di segmenti viene utilizzato per definire un segmento. Quando si seleziona **[!UICONTROL Create Segment]** dalla pagina Insights (Approfondimenti), l&#39;AI cliente aggiunge automaticamente al segmento le informazioni del bucket selezionato. Per completare la creazione del segmento, è sufficiente compilare i contenitori *Nome* e *Descrizione* nella parte destra dell’interfaccia utente del generatore di segmenti. Dopo aver assegnato al segmento un nome e una descrizione, fai clic **[!UICONTROL Save]** in alto a destra.

>[!NOTE]
>
>Poiché i punteggi di propensione sono scritti nel singolo profilo, sono disponibili nel generatore di segmenti come qualsiasi altro attributo di profilo. Quando vai al generatore di segmenti per creare nuovi segmenti, puoi vedere tutti i vari punteggi di propensione nello spazio dei nomi Customer AI (AI cliente).

![Riempimento segmento in](../images/insights/segment-saving.png)

Per visualizzare il nuovo segmento nell’interfaccia utente della piattaforma, fai clic su **[!UICONTROL Segments]** nella barra di navigazione a sinistra. Viene visualizzata **[!UICONTROL Browse]** la pagina e vengono visualizzati tutti i segmenti disponibili.

![Tutti i segmenti](../images/insights/Segments-dashboard.png)

## Passaggi successivi

Questo documento descrive le informazioni fornite da un&#39;istanza del servizio Customer AI. Ora puoi continuare a seguire l&#39;esercitazione sul [download dei punteggi in Customer AI](./download-scores.md) o consultare le altre guide dei servizi [intelligenti](../../home.md) Adobe disponibili.

## Risorse aggiuntive

Il seguente video illustra come utilizzare l&#39;API cliente per vedere l&#39;output dei modelli e dei fattori influenti.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)