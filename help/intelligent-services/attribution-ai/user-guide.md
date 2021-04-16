---
keywords: Experience Platform;guida utente;ai di attribuzione;argomenti popolari;area geografica
solution: Experience Platform, Intelligent Services
title: Guida all’interfaccia utente di Attribution AI
topic: 'Guida utente '
description: Questo documento funge da guida per l’interazione con Attribution AI nell’interfaccia utente di Intelligent Services.
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
translation-type: tm+mt
source-git-commit: 013f8d99fc394477177fdbf7eb9dd9b8ce94b88f
workflow-type: tm+mt
source-wordcount: '1712'
ht-degree: 1%

---

# Guida all’interfaccia utente di Attribution AI

Nell’ambito di Intelligent Services, Attribution AI è un servizio di attribuzione algoritmica multicanale che calcola l’influenza e l’impatto incrementale delle interazioni dei clienti rispetto a risultati specifici. Con Attribution AI, gli esperti di marketing possono misurare e ottimizzare le spese di marketing e pubblicitarie comprendendo l’impatto di ogni singola interazione con i clienti in ogni fase del percorso del cliente.

Questo documento funge da guida per l’interazione con Attribution AI nell’interfaccia utente di Intelligent Services.

## Creare un’istanza

Nell’interfaccia utente di [!DNL Adobe Experience Platform], fai clic su **[!UICONTROL Services]** nel menu di navigazione a sinistra. Viene visualizzato il browser **[!UICONTROL Services]** che visualizza i servizi intelligenti di Adobe disponibili. Nel contenitore per Attribution AI, fai clic su **[!UICONTROL Open]**.

![Accesso all’istanza](./images/user-guide/open_Attribution_ai.png)

Viene visualizzata la pagina del servizio Attribution AI. In questa pagina sono elencate le istanze di servizio di Attribution AI e vengono visualizzate informazioni su di esse, tra cui il nome dell’istanza, gli eventi di conversione, la frequenza di esecuzione dell’istanza e lo stato dell’ultimo aggiornamento.

Puoi trovare la metrica **[!UICONTROL Total conversion events scored]** situata in basso a destra del contenitore **[!UICONTROL Create instance]** . Questa metrica tiene traccia del numero totale di eventi di conversione valutati per Attribution AI per l’anno solare corrente, inclusi tutti gli ambienti sandbox ed eventuali istanze di servizio eliminate.

![](./images/user-guide/total_conversions.png)

Le istanze del servizio possono essere modificate, clonate ed eliminate utilizzando i controlli sul lato destro dell’interfaccia utente. Per visualizzare questi controlli, seleziona un&#39;istanza dal tuo **[!UICONTROL Service instances]** esistente. I controlli contengono le seguenti informazioni:

- **[!UICONTROL Edit]**: La selezione  **[!UICONTROL Edit]** ti consente di modificare un’istanza di servizio esistente. Puoi modificare il nome, la descrizione, lo stato e la frequenza di punteggio dell’istanza.
- **[!UICONTROL Clone]**: Selezionando  **[!UICONTROL Clone]** copia l&#39;istanza di servizio selezionata. Puoi quindi modificare il flusso di lavoro per apportare modifiche minori e rinominarlo come nuova istanza.
- **[!UICONTROL Delete]**: Puoi eliminare un’istanza di servizio, comprese eventuali esecuzioni cronologiche.
- **[!UICONTROL Data source]**: Un collegamento al set di dati utilizzato da questa istanza.
- **[!UICONTROL Last run details]**: Viene visualizzato solo in caso di errore di un&#39;esecuzione. Informazioni sul motivo per cui l’esecuzione non riuscita, ad esempio i codici di errore, sono visualizzati qui.

![](./images/user-guide/side_panel.png)

- **[!UICONTROL Conversion events]**: Panoramica rapida degli eventi di conversione configurati per questa istanza.
- **[!UICONTROL Lookback window]**: Intervallo di tempo definito che indica quanti giorni prima dei punti di contatto dell’evento di conversione sono inclusi.
- **[!UICONTROL Touchpoints]**: Elenco di tutti i punti di contatto definiti durante la creazione dell’istanza.

![](./images/user-guide/side_panel_2.png)

Selezionare **[!UICONTROL Create instance]** per iniziare.

![Crea istanza](./images/user-guide/landing_page.png)

Viene quindi visualizzata la pagina di configurazione di Attribution AI, in cui puoi fornire informazioni di base e specificare un set di dati per l’istanza.

![pagina di configurazione](./images/user-guide/setup_attribution.png)

### Denomina l&#39;istanza

Alla voce **[!UICONTROL Basic information]**, fornisci un nome e una descrizione facoltative per la tua istanza di servizio.

![denominazione di un’istanza](./images/user-guide/naming_instance.png)

### Selezionare un set di dati

Dopo aver compilato le informazioni di base, fai clic sul menu a discesa con etichetta **Seleziona set di dati** per selezionare il set di dati. Il set di dati viene utilizzato per addestrare il modello e valutare i dati successivi che produce. Quando selezioni un set di dati dal selettore a discesa, vengono elencati solo quelli compatibili con Attribution AI e conformi allo schema Experience Data Model (XDM). Una volta scelto un set di dati, fai clic su **Successivo** nell’angolo in alto a destra per passare alla pagina degli eventi di definizione.

>[!TIP]
>
>I set di dati Adobe Analytics sono supportati tramite il connettore origine Analytics.

![pagina di configurazione](./images/user-guide/dataset_selector.png)

## Definizione degli eventi

Esistono tre diversi tipi di dati di input utilizzati per definire gli eventi:

- **Eventi di conversione:** obiettivi aziendali che identificano l’impatto delle attività di marketing, come ordini di e-commerce, acquisti in negozio e visite a siti web.
- **Intervallo di lookback:** fornisce un intervallo di tempo che indica quanti giorni prima dell’inclusione dei punti di contatto dell’evento di conversione.
- **Punti di contatto: eventi di marketing a livello di destinatario, singolo e o cookie utilizzati per valutare l’impatto numerico o basato su ricavi delle conversioni.** 

### Definire gli eventi di conversione {#define-conversion-events}

Per definire un evento di conversione, devi assegnare un nome all’evento e selezionare il tipo di evento facendo clic sul menu a discesa **Inserisci nome campo** .

![menu a discesa sì](./images/user-guide/conversion_event_2.png)

Una volta selezionato un evento, viene visualizzato un nuovo menu a discesa a destra di tale evento. Il secondo menu a discesa viene utilizzato per fornire ulteriore contesto all’evento attraverso le operazioni. Per questo evento di conversione, viene utilizzata l&#39;operazione predefinita *exists* .

>[!NOTE]
>
>Una stringa sotto il *nome conversione* viene aggiornata mentre definisci l&#39;evento.

![nessun menu a discesa](./images/user-guide/conversion_event_1.png)

I pulsanti **[!UICONTROL Add event]** e **[!UICONTROL Add Group]** vengono utilizzati per definire ulteriormente la conversione. A seconda della conversione che stai definendo, potrebbe essere necessario utilizzare i pulsanti **[!UICONTROL Add event]** e **[!UICONTROL Add group]** per fornire ulteriore contesto.

![aggiungi evento](./images/user-guide/add_event.png)

Facendo clic su **[!UICONTROL Add event]** vengono creati campi aggiuntivi che possono essere compilati utilizzando lo stesso metodo descritto in precedenza. In questo modo viene aggiunta un&#39;istruzione AND alla definizione della stringa sotto il nome di conversione. Fai clic su **x** per rimuovere un evento aggiunto.

![aggiungi menu eventi](./images/user-guide/add_event_result.png)

Facendo clic su **[!UICONTROL Add Group]** è possibile creare campi aggiuntivi separati dall’originale. Aggiungendo i gruppi, viene visualizzato un pulsante blu *And* . Facendo clic su **And** è possibile modificare il parametro in modo che contenga &quot;OR&quot;. &quot;OR&quot; viene utilizzato per definire più percorsi di conversione riusciti. &quot;And&quot; estende il percorso di conversione per includere condizioni aggiuntive.

![utilizzando e](./images/user-guide/and_or.png)

Se hai bisogno di più conversioni, fai clic su **Aggiungi conversione** per creare una nuova scheda di conversione. Puoi ripetere il processo sopra descritto per definire più conversioni.

![aggiungi conversione](./images/user-guide/add_conversion.png)

### Definisci la finestra di lookback {#lookback-window}

Dopo aver definito la conversione, devi confermare l’intervallo di lookback. Utilizzando i tasti freccia o facendo clic sul valore predefinito (56), specifica quanti giorni prima dell’evento di conversione da cui desideri includere i punti di contatto. I punti di contatto sono definiti nel passaggio successivo.

![lookback](./images/user-guide/lookback_window.png)

### Definire i punti di contatto

La definizione dei punti di contatto segue un flusso di lavoro simile a [definizione delle conversioni](#define-conversion-events). Inizialmente devi denominare il punto di contatto e selezionare un valore del punto di contatto dal menu a discesa *Inserisci nome campo* . Una volta selezionato, viene visualizzato il menu a discesa dell’operatore con il valore predefinito &quot;exists&quot; (esiste). Fai clic sul menu a discesa per visualizzare un elenco di operatori.

![operatori](./images/user-guide/operators.png)

Per questo punto di contatto, seleziona **è uguale a**.

![passaggio 1](./images/user-guide/touchpoint_step1.png)

Dopo aver selezionato un operatore per un punto di contatto, viene reso disponibile *Immetti valore campo* . I valori a discesa per *Inserisci valore campo* vengono compilati in base all’operatore e al valore del punto di contatto precedentemente selezionati. Se un valore non viene compilato nel menu a discesa, è possibile digitarlo manualmente. Fai clic sul menu a discesa e seleziona **CLIC**.

>[!NOTE]
>
>Agli operatori &quot;esiste&quot; e &quot;non esiste&quot; non sono associati valori di campo.

![elenco a discesa dei punti di contatto](./images/user-guide/touchpoint_dropdown.png)

I pulsanti *Aggiungi evento* e *Aggiungi gruppo* vengono utilizzati per definire ulteriormente il punto di contatto. A causa della complessità dei punti di contatto, non è raro che si disponga di più eventi e gruppi per un singolo punto di contatto.

Quando fai clic su , **Aggiungi evento** consente l’aggiunta di campi aggiuntivi. Fai clic su **x** per rimuovere un evento aggiunto.

![aggiungi evento](./images/user-guide/touchpoint_add_event.png)

Facendo clic su **Aggiungi gruppo** è possibile creare campi aggiuntivi separati dall&#39;originale. Aggiungendo i gruppi, viene visualizzato un pulsante blu *And* . Fai clic su **E** per modificare il parametro; il nuovo parametro &quot;OR&quot; viene utilizzato per definire più percorsi con esito positivo. Questo particolare punto di contatto ha un solo percorso di successo, quindi non è necessario &quot;O&quot;.

![panoramica dei punti di contatto](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>Utilizza la stringa in *Nome punto di contatto* per una panoramica rapida del punto di contatto. La stringa corrisponde al nome del punto di contatto.

![](./images/user-guide/touchpoint_string.png)

Per aggiungere altri punti di contatto, fai clic su **Aggiungi punto di contatto** e ripeti il processo descritto sopra.

![aggiungi punto di contatto](./images/user-guide/add_touchpoint.png)

Dopo aver definito tutti i punti di contatto necessari, scorri verso l’alto e fai clic su **Successivo** nell’angolo in alto a destra per passare al passaggio finale.

![definire finito](./images/user-guide/define_event_next.png)

## Impostazione avanzata di formazione e valutazione

La pagina finale in Attribution AI è la pagina **[!UICONTROL Advanced]** utilizzata per impostare formazione e valutazione.

![nuova pagina avanzata](./images/user-guide/advanced_settings.png)

### Formazione programmata

Utilizzando la *Pianificazione*, puoi selezionare un giorno e un&#39;ora della settimana in cui desideri eseguire il punteggio.

Fai clic sull’elenco a discesa in *Frequenza di punteggio* per selezionare un punteggio giornaliero, settimanale e mensile. Quindi, seleziona i giorni della settimana in cui desideri che si verifichi il punteggio. È possibile selezionare più giorni. Fai clic una volta al secondo per deselezionarlo.

![Formazione programmata](./images/user-guide/schedule_training.png)

Per modificare l&#39;ora del giorno in cui si desidera che si verifichi il punteggio, fare clic sull&#39;icona dell&#39;orologio. Nella nuova sovrapposizione visualizzata, immetti l’ora del giorno in cui desideri che venga effettuato il punteggio. Fai clic all’esterno della sovrapposizione per chiuderla.

>[!NOTE]
>
>Il completamento di ogni processo di punteggio può richiedere fino a 24 ore.

![icona dell&#39;orologio](./images/user-guide/time_of_day.png)

### Colonne di set di dati con punteggio aggiuntivo (facoltativo)

Per impostazione predefinita, viene creato un set di dati di punteggio per ogni istanza di servizio in uno schema standard. Puoi scegliere di aggiungere ulteriori colonne in base alle configurazioni Evento di conversione e Punto di contatto all’output del set di dati del punteggio. Per iniziare, seleziona le colonne dal set di dati di input, puoi trascinarle e rilasciarle per modificare l’ordine tenendo premuto il pulsante sinistro del mouse sull’icona hamburger.

![aggiunta a una colonna di set di dati di punteggio](./images/user-guide/Add-score-dataset.png)

### Modellazione basata su regione (opzionale) {#region-based-modeling-optional}

I comportamenti dei clienti possono variare in modo significativo a seconda del paese e dell’area geografica. Per le aziende globali, l’utilizzo di modelli basati su paesi o aree geografiche può aumentare l’accuratezza dell’attribuzione. Ogni area aggiunta crea un nuovo modello con i dati di tale area.

Per definire una nuova area, fai clic su **[!UICONTROL Add region]**. Specifica un nome per la regione nel contenitore visualizzato. Solo un valore (&quot;placeContext.geo.countryCode&quot;) viene popolato dal menu a discesa **[!UICONTROL Enter Field Name]**. Selezionare questo valore.

![Seleziona la regione in](./images/user-guide/select_region_att.png)

Quindi, seleziona un operatore.

![operatore regionale](./images/user-guide/region_operators.png)

Infine, digita il codice del paese nel menu a discesa **[!UICONTROL Enter Field Value]** .

>[!NOTE]
>
>I codici paese sono lunghi due caratteri. Un elenco completo è disponibile qui [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

![regione](./images/user-guide/region-based.png)

### Finestra di formazione {#training-window}

Per garantire che il modello sia il più accurato possibile, è importante addestrare il modello con dati storici che rappresentano la vostra attività. Per impostazione predefinita, il modello viene addestrato utilizzando 2 quarti (6 mesi) dei dati degli eventi di conversione. Seleziona il menu a discesa per modificare il valore predefinito. Puoi scegliere di allenarti con uno o quattro quarti di dati (3-12 mesi).

>[!NOTE]
>
>Una finestra di formazione più breve è più sensibile alle tendenze recenti, mentre una finestra di formazione più lunga crea un modello più robusto ed è meno sensibile alle tendenze recenti.

![finestra di formazione](./images/user-guide/training_window.png)

Dopo aver selezionato la finestra di formazione, fai clic su **[!UICONTROL Finish]** nell’angolo in alto a destra. Consentire un po&#39; di tempo per l&#39;elaborazione dei dati. Una volta completata, viene visualizzata una finestra di dialogo di attivazione che conferma il completamento della configurazione dell&#39;istanza. Fai clic su **[!UICONTROL Ok]** per essere reindirizzato alla pagina **[!UICONTROL Service instances]** in cui puoi visualizzare la tua istanza di servizio.

![configurazione completata](./images/user-guide/instance_setup_complete.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un&#39;istanza di servizio in Attribution AI. Al termine del punteggio dell&#39;istanza (consenti fino a 24 ore), puoi [scoprire informazioni sulle Attribution AI](./discover-insights.md). Inoltre, se desideri scaricare i risultati del punteggio, visita la documentazione [download scores](./download-scores.md) .

## Risorse aggiuntive

Il video seguente illustra un flusso di lavoro end-to-end per la creazione di una nuova istanza in Attribution AI.

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)
