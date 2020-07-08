---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: Scopri informazioni approfondite con l'AI del cliente
topic: Discovering insights
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 0%

---


# Scopri informazioni approfondite con l&#39;AI del cliente

L&#39;AI del cliente, come parte di Intelligent Services, fornisce agli esperti di marketing il potere di sfruttare Adobe Sensei per anticipare quali saranno le azioni future dei clienti. L&#39;AI del cliente viene utilizzata per generare punteggi di propensione personalizzati, come il churn e la conversione per i singoli profili su scala. Ciò è possibile senza dover trasformare le esigenze aziendali in un problema di machine learning, scegliendo un algoritmo, una formazione o un&#39;implementazione.

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

Esistono due modi per visualizzare i dettagli dell&#39;istanza del servizio: la prima proviene dal dashboard e la seconda dall&#39;interno dell&#39;istanza del servizio.

Per visualizzare i dettagli dall&#39;interno del dashboard, fate clic su un contenitore di istanza del servizio, evitando il collegamento ipertestuale associato al nome. Si apre una barra laterale destra che fornisce dettagli aggiuntivi come la descrizione, la frequenza del punteggio, l&#39;obiettivo di previsione e la popolazione ammissibile. Inoltre, potete scegliere di modificare ed eliminare l’istanza facendo clic **[!UICONTROL Edit]** o **[!UICONTROL Delete]**.

![barra laterale destra](../images/insights/success-run.png)

>[!NOTE]
>
>Nel caso in cui un&#39;esecuzione del punteggio non riesca, viene visualizzato un messaggio di errore. Il messaggio di errore è elencato in Dettagli *dell&#39;* ultima esecuzione nella barra a destra, visibile solo per le esecuzioni non riuscite.

![messaggio di esecuzione non riuscito](../images/insights/failed-run.png)

Il secondo modo per visualizzare i dettagli aggiuntivi per un’istanza di servizio si trova nella pagina delle informazioni. Puoi fare clic **[!UICONTROL Show more]** in alto a destra per compilare un elenco a discesa. Vengono elencati i dettagli, ad esempio la definizione del punteggio, la data di creazione e il tipo di propensione. Per ulteriori informazioni su una delle proprietà elencate, visita [Configurazione di un&#39;istanza](./configure.md)di AI del cliente.

![mostra di più](../images/insights/landing-show-more.png)

![mostra di più](../images/insights/show-more.png)

### Modificare un’istanza

Per modificare un&#39;istanza, fate clic **[!UICONTROL Edit]** nella barra di navigazione in alto a destra.

![fare clic sul pulsante Modifica](../images/insights/edit-button.png)

Viene visualizzata la finestra di dialogo di modifica, che consente di modificare la *descrizione* e la frequenza *di* punteggio dell’istanza. Per confermare le modifiche e chiudere la finestra di dialogo, fate clic **[!UICONTROL Edit]** nell’angolo in basso a destra.

![edit pover](../images/insights/edit-instance.png)

### Altre azioni

Il **[!UICONTROL More actions]** pulsante si trova nella barra di navigazione in alto a destra accanto a **[!UICONTROL Edit]**. Facendo clic **[!UICONTROL More actions]** si apre un menu a discesa che consente di selezionare una delle operazioni seguenti:

- **[!UICONTROL Delete]**: Elimina l&#39;istanza.
- **[!UICONTROL Access scores]**: Facendo clic sui punteggi *di* accesso si apre una finestra di dialogo che fornisce un collegamento ai punteggi di [scaricamento per l&#39;esercitazione AI](./download-scores.md) del cliente. La finestra di dialogo fornisce inoltre l&#39;ID del set di dati necessario per effettuare chiamate API.
- **[!UICONTROL View run history]**: Viene visualizzata una finestra di dialogo contenente un elenco di tutte le esecuzioni del punteggio associate all&#39;istanza del servizio.

![altre azioni](../images/insights/more-actions.png)

## Riepilogo punteggio {#scoring-summary}

Riepilogo punteggio visualizza il numero totale di profili con punteggio e li classifica in bucket contenenti probabilità alta, media e bassa. I periodi fissi di propensione sono determinati in base all&#39;intervallo di punteggio, il valore basso è inferiore a 24, il valore medio è compreso tra 25 e 74 e il valore massimo è superiore a 74. Ogni intervallo ha un colore corrispondente alla legenda.

>[!NOTE]
>
>Se si tratta di un punteggio di propensione alla conversione, i punteggi alti sono indicati in verde e i punteggi bassi in rosso. Se si prevede la propensione del churn questo è capovolto, i punteggi alti sono in rosso e i punteggi bassi sono in verde. Il bucket medio rimane giallo indipendentemente dal tipo di propensione scelto.

![riepilogo punteggio](../images/insights/scoring-summary.png)

## Distribuzione dei punteggi

La scheda *Distribuzione dei punteggi* fornisce un riepilogo visivo della popolazione in base al punteggio. I colori visualizzati nella scheda *Distribuzione di punteggi* rappresentano il tipo di punteggio di propensione generato.

![distribuzione dei punteggi](../images/insights/distribution-of-scores.png)

## Fattori di influenza

Per ogni intervallo di punteggio, viene generata una scheda che mostra i primi 10 fattori influenti per tale intervallo. I fattori influenti forniscono ulteriori dettagli sul motivo per cui i clienti appartengono a vari periodi fissi di valutazione.

![Fattori di influenza](../images/insights/influential-factors.png)

### Creazione di un segmento

Facendo clic sul **[!UICONTROL Create Segment]** pulsante in uno qualsiasi dei periodi fissi per Propensione bassa, Media e Alta si reindirizza al generatore di segmenti.

>[!NOTE]
>Il **[!UICONTROL Create Segment]** pulsante è disponibile solo se per il set di dati è abilitato il profilo cliente in tempo reale. Per ulteriori informazioni su come abilitare il profilo cliente in tempo reale, consulta la panoramica [sul profilo cliente in tempo](../../../rtcdp/overview.md)reale.

![Fai clic su Crea segmento](../images/insights/influential-factors-create-segment.png)

![Creazione di un segmento](../images/insights/create-segment.png)

Il generatore di segmenti viene utilizzato per definire un segmento. Quando si seleziona **[!UICONTROL Create Segment]** dalla pagina Insights (Approfondimenti), l&#39;AI cliente aggiunge automaticamente al segmento le informazioni del bucket selezionato. Per completare la creazione del segmento, è sufficiente compilare i contenitori *Nome* e *Descrizione* nella parte destra dell’interfaccia utente del generatore di segmenti. Dopo aver assegnato al segmento un nome e una descrizione, fai clic **[!UICONTROL Save]** in alto a destra.

>!![NOTE] Poiché i punteggi di propensione sono scritti nel singolo profilo, sono disponibili nel generatore di segmenti come qualsiasi altro attributo di profilo. Quando vai al generatore di segmenti per creare nuovi segmenti, puoi vedere tutti i vari punteggi di propensione nello spazio dei nomi Customer AI (AI cliente).

![Riempimento segmento in](../images/insights/segment-saving.png)

Per visualizzare il nuovo segmento nell’interfaccia utente di Platform, fai clic su **[!UICONTROL Segments]** nella barra di navigazione a sinistra. Viene visualizzata la pagina *Sfoglia* , con tutti i segmenti disponibili.

![Tutti i segmenti](../images/insights/Segments-dashboard.png)

## Passaggi successivi

Questo documento descrive le informazioni fornite da un&#39;istanza del servizio Customer AI. Ora puoi continuare a seguire l&#39;esercitazione sul [download dei punteggi in Customer AI](./download-scores.md) o consultare le altre guide dei servizi [intelligenti di](../../home.md) Adobe disponibili.

## Risorse aggiuntive

Il seguente video illustra come utilizzare l&#39;API cliente per vedere l&#39;output dei modelli e dei fattori influenti.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)