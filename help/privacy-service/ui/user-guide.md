---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida utente Privacy Service
topic: UI guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---


# [!DNL Privacy Service] guida utente

Questo documento fornisce i passaggi per creare e gestire le richieste di privacy utilizzando l&#39;interfaccia [!DNL Privacy Service] utente.

## Sfogliare il dashboard dell&#39; [!DNL Privacy Service] interfaccia utente

Il dashboard per l’ [!DNL Privacy Service] interfaccia utente offre due widget che consentono di visualizzare lo stato dei processi di privacy: **[!UICONTROL Status Report]** e **[!UICONTROL Job Requests]**. Il dashboard visualizza anche il regolamento selezionato corrente per i processi visualizzati.

![Pannello interfaccia](../images/user-guide/dashboard.png)

### Tipo di regolamento

[!DNL Privacy Service] supporta le richieste di lavoro per tre tipi di regolamentazione:

* L&#39;Unione europea [!DNL General Data Protection Regulation] (RGPD)
* L&#39; [!DNL California Consumer Privacy Act] (CCPA)
* Thailandia [!DNL Personal Data Protection Act] (PDPA_THA)

I processi per ciascun tipo di regolamento vengono tracciati separatamente. Per passare da un tipo di regola all&#39;altro, fare clic sul **[!UICONTROL Regulation Type]** menu a discesa e selezionare la regola desiderata dall&#39;elenco.

![Tipo di regolamento, elenco a discesa](../images/user-guide/regulation.png)

Dopo aver modificato il tipo di regolazione, il dashboard si aggiorna e mostra tutte le operazioni, i filtri, i widget e le finestre di dialogo per la creazione di posti di lavoro che si applicano al regolamento selezionato.

![Pannello aggiornato](../images/user-guide/dashboard-update.png)

### Rapporto stato

Il grafico a sinistra del widget Rapporto di stato tiene traccia dei processi inviati rispetto a eventuali processi che potrebbero essere stati riportati con errori. Il grafico a destra tiene traccia dei processi che si avvicinano alla fine della finestra di conformità di 30 giorni.

Fate clic su uno dei due pulsanti di attivazione/disattivazione sopra il grafico per mostrare o nascondere le rispettive metriche.

![](../images/user-guide/hide-errors.png)

Per visualizzare il numero esatto di processi associati a qualsiasi punto dati del grafico, posizionate il puntatore del mouse sul punto di dati in questione.

![Punti dati del puntatore del mouse](../images/user-guide/mouse-over.png)

Per visualizzare ulteriori dettagli su un dato punto dati, fare clic sul punto dati in questione per visualizzare i processi associati nel widget Richieste di processo. Prendete nota del filtro applicato appena sopra l’elenco dei processi.

![Filtro applicato dal widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Quando un filtro è stato applicato al widget Richieste di processo, potete rimuovere il filtro facendo clic sul **[!UICONTROL X]** filtro nella pillola del filtro. Le richieste di processo tornano quindi all’elenco di tracciamento predefinito.

### Richieste di processo

Il widget Richieste di lavoro elenca tutte le richieste di processo disponibili nell’organizzazione, inclusi dettagli quali il tipo di richiesta, lo stato corrente, la data di scadenza e l’e-mail del richiedente.

>[!NOTE]
>
>I dati per i processi creati in precedenza sono accessibili solo per 30 giorni dopo la data di completamento.

Potete filtrare l’elenco digitando le parole chiave nella barra di ricerca sotto il titolo Richieste di processo. L’elenco filtra automaticamente durante la digitazione, mostrando le richieste contenenti valori corrispondenti ai termini di ricerca. Potete inoltre utilizzare il menu a **[!UICONTROL Requested on]** discesa per selezionare un intervallo di tempo per i processi elencati.

![Opzioni di ricerca richieste di lavoro](../images/user-guide/job-search.png)

Per visualizzare i dettagli di una particolare richiesta di processo, fate clic sull’ID processo della richiesta dall’elenco per aprire la *[!UICONTROL Job Details]* pagina.

![Dettagli processo interfaccia utente GDPR](../images/user-guide/job-details.png)

Questa finestra di dialogo contiene informazioni sullo stato di ciascuna [!DNL Experience Cloud] soluzione e sullo stato corrente in relazione al processo complessivo. Poiché ogni processo di privacy è asincrono, la pagina visualizza la data e l’ora di comunicazione più recenti (GMT) di ciascuna soluzione, in quanto alcuni richiedono più tempo di altri per elaborare la richiesta.

Se una soluzione ha fornito dati aggiuntivi, questi possono essere visualizzati in questa finestra di dialogo. Per visualizzare questi dati, fai clic sulle singole righe di prodotto.

Per scaricare i dati del processo completo come file CSV, fate clic su **[!UICONTROL Export to CSV]** in alto a destra nella finestra di dialogo.

## Creare una nuova richiesta di lavoro per la privacy

>[!NOTE]
>
>Per creare una richiesta di lavoro per la privacy, è necessario fornire informazioni sull&#39;identità per i clienti specifici i cui dati devono essere accessibili o eliminati. Prima di continuare con questa sezione, consulta il documento sui dati di [identità per le richieste](../identity-data.md) di privacy.

L’ [!DNL Privacy Service] interfaccia utente offre due metodi per creare nuove richieste di processo:

* [Utilizzare il Generatore di richieste](#request-builder)
* [Caricare un file JSON](#json)

I passaggi per utilizzare ciascuno di questi metodi sono descritti nelle sezioni seguenti.

### Utilizzare il Generatore di richieste {#request-builder}

Utilizzando Request Builder, potete creare manualmente una nuova richiesta di processo per la privacy nell’interfaccia utente. Il Generatore di richieste è indicato per set di richieste sempre più semplici, perché il Generatore di richieste limita le richieste a disporre solo di ID per utente. Per richieste più complesse, potrebbe essere meglio [caricare un file](#json) JSON.

Per iniziare a utilizzare il generatore di richieste, fate clic **[!UICONTROL Create Request]** sotto il widget Rapporto di stato sul lato destro dello schermo.

![Fate clic su Crea richiesta](../images/user-guide/create-request.png)

Viene visualizzata la *[!UICONTROL Create Request]* finestra di dialogo con le opzioni disponibili per l’invio di una richiesta di lavoro per la privacy per il tipo di regola attualmente selezionato.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Selezionate la **[!UICONTROL Job Type]** richiesta (&quot;Elimina&quot; o &quot;Accesso&quot;) e una o più richieste disponibili **[!UICONTROL Products]** dall’elenco.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

In *[!UICONTROL Namespace type]*, selezionate il tipo di spazio nomi appropriato per gli ID cliente a cui viene inviato [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Quando si utilizza il tipo di spazio dei nomi _standard_ , selezionare uno spazio dei nomi dal menu a discesa (e-mail, ECID o AAID), quindi digitare i valori ID nella casella di testo a destra, premendo **\&lt;enter>** affinché ciascun ID venga aggiunto all&#39;elenco.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Quando si utilizza il tipo di spazio dei nomi _personalizzato_ , è necessario digitare manualmente lo spazio dei nomi prima di fornire i valori ID riportati di seguito.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Al termine, fate clic **[!UICONTROL Create]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

La finestra di dialogo scompare e il nuovo processo (o i nuovi processi) sono elencati nel widget Richieste di processo insieme al relativo stato di elaborazione corrente.

### Caricare un file JSON {#json}

Quando crei richieste più complesse, ad esempio quelle che utilizzano più tipi di ID per ciascun oggetto dati in fase di elaborazione, puoi creare una richiesta caricando un file JSON.

Fate clic sulla freccia accanto a **[!UICONTROL Create Request]**, sotto il widget Rapporto stato sul lato destro dello schermo. Dall&#39;elenco delle opzioni visualizzate, selezionare **[!UICONTROL Upload JSON]**.

![Opzioni di creazione richieste](../images/user-guide/create-options.png)

Viene visualizzata una *[!UICONTROL Upload JSON]* finestra di dialogo che consente di trascinare e rilasciare il file JSON.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Se non disponi di un file JSON da caricare, fai clic **[!UICONTROL Download Adobe-GDPR-Request.json]** per scaricare un modello che puoi compilare in base ai valori raccolti dagli interessati.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Individuate il file JSON sul computer e trascinatelo nella finestra di dialogo. Se il caricamento ha esito positivo, il nome del file viene visualizzato nella finestra di dialogo. Per continuare ad aggiungere altri file JSON, trascinateli e rilasciateli nella finestra di dialogo.

Al termine, fate clic **[!UICONTROL Create]**. La finestra di dialogo scompare e il nuovo processo o i nuovi processi sono elencati nel widget Richieste _di_ processo insieme al relativo stato di elaborazione corrente.

### Passaggi successivi

Leggendo questo documento, hai imparato a utilizzare l’ [!DNL Privacy Service] interfaccia utente per creare un processo di privacy, visualizzare i dettagli di un processo e controllarne lo stato di elaborazione e scaricare i risultati al termine.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando l&#39; [!DNL Privacy Service] API, fare riferimento alla guida [per](../api/getting-started.md)gli sviluppatori.