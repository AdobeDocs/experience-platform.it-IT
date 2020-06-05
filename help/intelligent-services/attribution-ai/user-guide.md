---
keywords: Experience Platform;user guide;attribution ai;popular topics
solution: Experience Platform
title: Guida utente AI per attribuzione
topic: User guide
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---


# Guida utente AI per attribuzione

Attribution AI, come parte di Intelligent Services è un servizio di attribuzione algoritmica multicanale che calcola l&#39;influenza e l&#39;impatto incrementale delle interazioni dei clienti rispetto a determinati risultati. Con Attribution AI, gli addetti al marketing possono misurare e ottimizzare le spese di marketing e pubblicitarie comprendendo l&#39;impatto di ogni singola interazione con i clienti in ogni fase dei viaggi dei clienti.

Questo documento funge da guida per l&#39;interazione con Attribution AI nell&#39;interfaccia utente di Intelligent Services.

## Creare un&#39;istanza

Nell’ [!DNL Adobe Experience Platform] interfaccia utente, fai clic su **Servizi** nella barra di navigazione a sinistra. Viene visualizzato il browser *Servizi* , con i servizi intelligenti Adobe disponibili. Nel contenitore per l&#39;AI di attribuzione, fate clic su **Apri**.

![Accesso all’istanza](./images/user-guide/open_Attribution_ai.png)

Viene visualizzata la pagina del servizio AI di attribuzione. In questa pagina sono elencate le istanze del servizio di Attribution AI e vengono visualizzate informazioni su di esse, incluso il nome dell&#39;istanza, gli eventi di conversione, la frequenza di esecuzione dell&#39;istanza e lo stato dell&#39;ultimo aggiornamento. Fate clic su **Crea istanza** per iniziare.

![Crea istanza](./images/user-guide/landing_page.png)

Viene quindi visualizzata la pagina di configurazione per l&#39;AI di attribuzione, in cui è possibile fornire informazioni di base e specificare un set di dati per l&#39;istanza.

![pagina di configurazione](./images/user-guide/setup_attribution.png)

### Denominate l’istanza

In *Informazioni* di base, fornite un nome e una descrizione facoltativa per l’istanza del servizio.

![denominazione di un&#39;istanza](./images/user-guide/naming_instance.png)

### Selezionare un dataset

Dopo aver compilato le informazioni di base, fai clic sul menu a discesa **Seleziona set** di dati per selezionare il set di dati. Il dataset viene utilizzato per formare il modello e segnare i dati successivi che produce. Quando si seleziona un set di dati dal selettore a discesa, vengono elencati solo quelli compatibili con l&#39;API di attribuzione e conformi allo schema Experience Data Model (XDM). Una volta scelto un set di dati, fate clic su **Avanti** nell&#39;angolo in alto a destra per passare alla pagina degli eventi di definizione.

![pagina di configurazione](./images/user-guide/initial_creation_attribution.png)

## Definizione degli eventi

Esistono tre tipi diversi di dati di input utilizzati per definire gli eventi:

- **Eventi di conversione:** Obiettivi aziendali che identificano l&#39;impatto delle attività di marketing, come ordini di e-commerce, acquisti in-store e visite ai siti web.
- **Finestra di ricerca:** Fornisce un intervallo di tempo che indica quanti giorni prima dei punti di contatto dell&#39;evento di conversione devono essere inclusi.
- **Punti di contatto:** eventi di marketing a livello di destinatari, singoli e o cookie utilizzati per valutare l&#39;impatto numerico o basato sulle entrate delle conversioni.

### Definizione degli eventi di conversione

Per definire un evento di conversione, è necessario assegnare all&#39;evento un nome e selezionare il tipo di evento facendo clic sul menu a discesa **Inserisci nome** campo.

![sì, elenco a discesa](./images/user-guide/conversion_event_2.png)

Una volta selezionato un evento, viene visualizzato un nuovo menu a discesa a destra. Il secondo menu a discesa viene utilizzato per fornire ulteriore contesto all&#39;evento attraverso l&#39;utilizzo di operazioni. Per questo evento di conversione, *esiste* l&#39;operazione predefinita.

>[!NOTE] Una stringa sotto il nome *di* conversione viene aggiornata mentre definite l&#39;evento.

![nessun menu a discesa](./images/user-guide/conversion_event_1.png)

I pulsanti *Aggiungi evento* e *Aggiungi gruppo* vengono utilizzati per definire ulteriormente la conversione. A seconda della conversione che si sta definendo, potrebbe essere necessario utilizzare i pulsanti *Aggiungi evento* e *Aggiungi gruppo* per fornire ulteriore contesto.

![add, evento](./images/user-guide/add_event.png)

Facendo clic su **Aggiungi evento** vengono creati altri campi che possono essere compilati con lo stesso metodo descritto sopra. In questo modo viene aggiunta un&#39;istruzione *AND* alla definizione della stringa sotto il nome *di* conversione. Fate clic sulla **x** per rimuovere un evento aggiunto.

![add event, menu](./images/user-guide/add_event_result.png)

Facendo clic su **Aggiungi gruppo** potete creare altri campi separati dall’originale. Con l’aggiunta di gruppi, viene visualizzato un pulsante blu *E* . Facendo clic su **And** (E) è possibile modificare il parametro in modo che contenga &quot;OR&quot;. &quot;OR&quot; viene utilizzato per definire più percorsi di conversione con esito positivo. &quot;And&quot; estende il percorso di conversione per includere condizioni aggiuntive.

![e](./images/user-guide/and_or.png)

Se è necessaria più di una conversione, fare clic su **Aggiungi conversione** per creare una nuova scheda di conversione. Potete ripetere il processo sopra descritto per definire più conversioni.

![add conversion](./images/user-guide/add_conversion.png)

### Definisci finestra di lookback

Dopo aver definito la conversione, è necessario confermare la finestra di lookback. Utilizzando i tasti freccia o facendo clic sul valore predefinito (56), specificate quanti giorni prima dell’evento di conversione da cui desiderate includere i punti di contatto. I punti di contatto sono definiti nel passaggio successivo.

![lookback](./images/user-guide/lookback_window.png)

### Definire i punti di contatto

La definizione dei punti di contatto segue un flusso di lavoro simile a quello della [definizione delle conversioni](#define-conversion-events). Inizialmente devi assegnare un nome al punto di contatto e selezionare un valore per il punto di contatto dal menu a discesa *Inserisci nome* campo. Una volta selezionato, il menu a discesa dell&#39;operatore viene visualizzato con il valore predefinito &quot;exists&quot; (esiste). Fare clic sul menu a discesa per visualizzare un elenco di operatori.

![operator](./images/user-guide/operators.png)

Per questo punto di contatto, seleziona **uguale a**.

![step 1](./images/user-guide/touchpoint_step1.png)

Dopo aver selezionato un operatore per un punto di contatto, *Inserisci valore* campo è disponibile. I valori a discesa per *Immettere il valore* del campo vengono compilati in base all&#39;operatore e al valore del punto di contatto precedentemente selezionati. Se un valore non viene compilato nel menu a discesa, è possibile digitarlo manualmente. Fate clic sul menu a discesa e selezionate **CLIC**.

>[!NOTE] Agli operatori &quot;esiste&quot; e &quot;non esiste&quot; non sono associati valori di campo.

![touchpoint, elenco a discesa](./images/user-guide/touchpoint_dropdown.png)

I pulsanti *Aggiungi evento* e *Aggiungi gruppo* vengono utilizzati per definire ulteriormente il punto di contatto. A causa della natura complessa che circonda i punti di contatto, non è raro avere più eventi e gruppi per un singolo punto di contatto.

Quando un utente fa clic su **Aggiungi evento** , è possibile aggiungere altri campi. Fate clic sulla **x** per rimuovere un evento aggiunto.

![add, evento](./images/user-guide/touchpoint_add_event.png)

Facendo clic su **Aggiungi gruppo** potete creare altri campi separati dall’originale. Con l’aggiunta di gruppi, viene visualizzato un pulsante blu *E* . Fate clic su **E** per cambiare il parametro. Il nuovo parametro &quot;OR&quot; viene usato per definire più percorsi con esito positivo. Questo particolare punto di contatto ha un solo percorso di successo, pertanto &quot;OR&quot; non è necessario.

![panoramica dei punti di contatto](./images/user-guide/add_group_touchpoint.png)

>[!NOTE] Usa la stringa sotto Nome *punto di* contatto per una panoramica rapida del punto di contatto. La stringa corrisponde al nome del punto di contatto.

![](./images/user-guide/touchpoint_string.png)

Per aggiungere altri punti di contatto, fai clic su **Aggiungi punto di contatto** e ripeti la procedura descritta sopra.

![aggiungi punto di contatto](./images/user-guide/add_touchpoint.png)

Dopo aver definito tutti i punti di contatto necessari, scorri verso l’alto e fai clic su **Avanti** nell’angolo in alto a destra per passare al passaggio finale.

![definizione finita](./images/user-guide/define_event_next.png)

## Configurazione avanzata della formazione e del punteggio

La pagina finale in Attribution AI (Attribuzione AI) è la pagina *Advanced* utilizzata per impostare formazione e punteggio.

![nuova pagina avanzata](./images/user-guide/advanced_settings.png)

### Pianificazione formazione

Utilizzando la *pianificazione*, potete selezionare un giorno e un&#39;ora della settimana in cui eseguire il punteggio.

Fai clic sul menu a discesa sotto Frequenza ** punteggio per selezionare tra il punteggio giornaliero, settimanale e mensile. Quindi, selezionare i giorni della settimana in cui si desidera che venga eseguito il punteggio. È possibile selezionare più giorni. Fate clic una volta al giorno per deselezionare la relativa opzione.

![Pianificazione formazione](./images/user-guide/schedule_training.png)

Per modificare l&#39;ora del giorno in cui si desidera che venga eseguito il punteggio, fare clic sull&#39;icona dell&#39;orologio. Nella nuova sovrapposizione che viene visualizzata, inserite l’ora del giorno in cui si desidera che venga eseguito il punteggio. Fate clic all’esterno della sovrapposizione per chiuderla.

>[!NOTE] Il completamento di ogni processo di punteggio può richiedere fino a 24 ore.

![icona orologio](./images/user-guide/time_of_day.png)

### Modellazione basata sulle regioni (facoltativo)

I comportamenti dei clienti possono essere significativamente diversi per paese e area geografica. Per le aziende globali, l&#39;utilizzo di modelli basati su paesi o regioni può aumentare la precisione di attribuzione. Ogni area aggiunta crea un nuovo modello con i dati di tale regione.

Per definire una nuova area, fare clic su **Aggiungi area**. Nel contenitore visualizzato, specificate un nome per la regione. Un solo valore (&quot;placeContext.geo.countryCode&quot;) viene compilato dall&#39;elenco a discesa *Immettere il nome* del campo. Selezionare questo valore.

![Seleziona regione in](./images/user-guide/select_region_att.png)

Quindi, selezionare un operatore.

![operatore regionale](./images/user-guide/region_operators.png)

Infine, digitare il codice del paese nel menu a discesa *Inserisci valore* campo.

>[!NOTE] I codici paese sono lunghi due caratteri. Un elenco completo è disponibile qui [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

![regione](./images/user-guide/region-based.png)

### Finestra Formazione

Per garantire che si ottenga il modello più accurato possibile, è importante formare il modello con dati storici che rappresentano il business. Per impostazione predefinita, il modello viene addestrato utilizzando 2 quarti (6 mesi) di dati. Selezionate il menu a discesa per modificare il valore predefinito. È possibile scegliere di allenarsi con uno o quattro quarti di dati (3-12 mesi).

>[!NOTE] Una finestra di formazione più breve è più sensibile alle tendenze recenti, mentre una finestra di formazione più lunga crea un modello più robusto ed è meno sensibile alle tendenze recenti.

![finestra di formazione](./images/user-guide/training_window.png)

Dopo aver selezionato la finestra di formazione, fate clic su **Fine** nell’angolo in alto a destra. Consentire l&#39;elaborazione dei dati entro un certo periodo di tempo. Al termine, viene visualizzata una finestra di dialogo di conferma del completamento dell’impostazione dell’istanza. Fate clic su **OK** per reindirizzare la pagina delle istanze *del* servizio in cui è possibile visualizzare l&#39;istanza del servizio.

![configurazione completata](./images/user-guide/instance_setup_complete.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata creata correttamente un&#39;istanza di servizio in Attribution AI. Una volta che l&#39;istanza ha terminato il punteggio (fino a 24 ore), è possibile [scoprire informazioni](./discover-insights.md)sull&#39;analisi dell&#39;attribuzione. Inoltre, se desideri scaricare i risultati del punteggio, consulta la documentazione [sul download dei punteggi](./download-scores.md) non elaborati.

## Risorse aggiuntive

Il seguente video illustra un flusso di lavoro end-to-end per la creazione di una nuova istanza in Attribution AI.

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)