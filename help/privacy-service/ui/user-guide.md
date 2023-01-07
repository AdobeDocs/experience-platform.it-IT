---
keywords: Experience Platform;home;argomenti popolari;esportazione;esportazione
solution: Experience Platform
title: Gestire i processi relativi alla privacy nell’interfaccia utente di Privacy Service
description: Scopri come utilizzare l’interfaccia utente di Privacy Service per coordinare e monitorare le richieste di privacy in diverse applicazioni Experience Cloud.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 1%

---

# Gestire i processi relativi alla privacy nell’interfaccia utente di Privacy Service

Questo documento descrive i passaggi necessari per creare e gestire le richieste di accesso a dati personali tramite [!DNL Privacy Service] interfaccia utente.

## Sfoglia il [!DNL Privacy Service] Dashboard dell&#39;interfaccia utente

Il dashboard per [!DNL Privacy Service] L’interfaccia utente fornisce due widget che ti consentono di visualizzare lo stato dei processi relativi alla privacy: &quot;[!UICONTROL Rapporto sullo stato]&quot; e &quot;[!UICONTROL Richieste di lavoro]&quot;. Il dashboard visualizza anche il regolamento selezionato corrente per i lavori visualizzati.

![Dashboard dell&#39;interfaccia utente](../images/user-guide/dashboard.png)

### Tipo di regolamento

[!DNL Privacy Service] supporta le richieste di lavoro per diverse normative sulla privacy. Nella tabella seguente sono elencati i regolamenti supportati e la relativa etichetta corrispondente come rappresentata nell’interfaccia utente:

| Etichetta dell’interfaccia utente | Regolamento |
| --- | --- |
| [!UICONTROL CCPA] | Le selezioni del menu [!DNL California Consumer Privacy Act] |
| [!UICONTROL RGPD] | L&#39;Unione europea [!DNL General Data Protection Regulation] |
| [!UICONTROL PDPA_THA] | Thailandia [!DNL Personal Data Protection Act] |
| [!UICONTROL LGPD_BRA] | Brasile [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL NZPA_NZL] | Nuova Zelanda [!DNL Privacy Act] |
| [!UICONTROL VCDPA_USA] | Le selezioni del menu [!DNL Virginia Consumer Data Protection Act] |
| [!UICONTROL CPRA_USA] | Le selezioni del menu [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL APA_AUS] | Le selezioni del menu [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL HIPAA_AUS] | Le selezioni del menu [!DNL Health Insurance Portability and Accountability Act] |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Vedi la panoramica su [normative sulla privacy supportate](../regulations/overview.md) per ulteriori informazioni sul contesto giuridico di ciascun regolamento.

I lavori per ciascun tipo di regolamento sono tracciati separatamente. Per passare da un tipo di regolamento all&#39;altro, seleziona la **[!UICONTROL Tipo di regolamento]** menu a discesa e selezionare il regolamento desiderato dall&#39;elenco.

![Menu a discesa Tipo di regolamento](../images/user-guide/regulation.png)

Quando si modifica il tipo di regolamento, il dashboard viene aggiornato per mostrare tutte le operazioni, i filtri, i widget e le finestre di dialogo per la creazione di posti di lavoro che si applicano al regolamento selezionato.

![Dashboard aggiornato](../images/user-guide/dashboard-update.png)

### Rapporto sullo stato

Il grafico a sinistra del widget Rapporto di stato tiene traccia dei processi inviati rispetto a quelli che potrebbero aver segnalato errori. Il grafico a destra traccia i lavori che si avvicinano alla fine della finestra di conformità di 30 giorni.

Seleziona uno dei due pulsanti di attivazione/disattivazione sopra il grafico per mostrare o nascondere le rispettive metriche.

![](../images/user-guide/hide-errors.png)

È possibile visualizzare il numero esatto di processi associati a qualsiasi punto dati dei grafici passando il mouse sul punto dati in questione.

![Punti dati del passaggio del mouse](../images/user-guide/mouse-over.png)

Per visualizzare ulteriori dettagli su un dato punto dati, seleziona il punto dati in questione per visualizzare i processi associati nel widget Richieste di lavoro. Prendi nota del filtro applicato appena sopra l’elenco dei processi.

![Filtro applicato dal widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Quando un filtro è stato applicato al widget Richieste di lavoro, puoi rimuovere il filtro selezionando la **X** sulla pillola del filtro. Le richieste di lavoro vengono quindi riportate all’elenco di tracciamento predefinito.

### Richieste di lavoro

Il widget Richieste di lavoro elenca tutte le richieste di lavoro disponibili nell’organizzazione, inclusi dettagli quali tipo di richiesta, stato corrente, data di scadenza e e-mail del richiedente.

>[!NOTE]
>
>I dati per i processi creati in precedenza sono accessibili solo per 30 giorni dopo la data di completamento.

Puoi filtrare l’elenco digitando le parole chiave nella barra di ricerca sotto il titolo Richieste di lavoro. L’elenco filtra automaticamente durante la digitazione, mostrando le richieste contenenti valori che corrispondono ai termini di ricerca. È inoltre possibile utilizzare **[!UICONTROL Richiesto il]** menu a discesa per selezionare un intervallo di tempo per i processi elencati.

![Opzioni di ricerca per la richiesta di lavoro](../images/user-guide/job-search.png)

Per visualizzare i dettagli di una particolare richiesta di processo, seleziona l’ID del processo della richiesta dall’elenco per aprire la **[!UICONTROL Dettagli processo]** pagina.

![Dettagli sul lavoro nell’interfaccia utente RGPD](../images/user-guide/job-details.png)

Questa finestra di dialogo contiene informazioni sullo stato di ogni [!DNL Experience Cloud] la soluzione e il suo stato attuale rispetto al lavoro complessivo. Poiché ogni processo di privacy è asincrono, la pagina visualizza la data e l’ora di comunicazione più recente (GMT) da ogni soluzione, in quanto alcuni richiedono più tempo di altri per elaborare la richiesta.

Se una soluzione ha fornito dati aggiuntivi, questi possono essere visualizzati in questa finestra di dialogo. Puoi visualizzare questi dati selezionando le singole righe di prodotto.

Per scaricare come file CSV i dati completi del processo, seleziona **[!UICONTROL Esportazione in formato CSV]** in alto a destra nella finestra di dialogo.

## Crea una nuova richiesta di processo per la privacy

>[!NOTE]
>
>Per creare una richiesta di lavoro per la privacy, è necessario fornire informazioni di identità per i clienti specifici i cui dati devono essere accessibili o eliminati. Consulta il documento in [dati di identità per le richieste di privacy](../identity-data.md) prima di continuare con questa sezione.

La [!DNL Privacy Service] L’interfaccia utente fornisce due metodi per creare nuove richieste di lavoro:

* [Utilizza Request Builder](#request-builder)
* [Caricare un file JSON](#json)

I passaggi per l’utilizzo di ciascuno di questi metodi sono descritti nelle sezioni seguenti.

### Utilizza Request Builder {#request-builder}

Utilizzando Request Builder, puoi creare manualmente una nuova richiesta di processo per la privacy nell’interfaccia utente. Il Generatore di richieste viene utilizzato meglio per set di richieste semplici e più piccoli, perché il Generatore di richieste limita le richieste ad avere solo un tipo di ID per utente. Per richieste più complicate, potrebbe essere meglio [caricare un file JSON](#json) invece.

Per iniziare a utilizzare il Generatore di richieste, seleziona **[!UICONTROL Crea richiesta]** sotto il widget Rapporto di stato sul lato destro dello schermo.

![Seleziona Crea richiesta](../images/user-guide/create-request.png)

La **[!UICONTROL Crea richiesta]** viene visualizzata la finestra di dialogo con le opzioni disponibili per l&#39;invio di una richiesta di processo di privacy per il tipo di regolamento attualmente selezionato.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Seleziona la **[!UICONTROL Tipo di processo]** della richiesta (&quot;Elimina&quot; o &quot;Accesso&quot;) e di uno o più prodotti disponibili dall’elenco.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Sotto **[!UICONTROL Tipo di spazio dei nomi]**, seleziona il tipo di spazio dei nomi appropriato per gli ID cliente a cui inviare [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Quando utilizzi il tipo di spazio dei nomi standard, seleziona uno spazio dei nomi dal menu a discesa (e-mail, ECID o AAID), quindi digita i valori ID nella casella di testo a destra, premendo **\&lt;enter>** per ogni ID da aggiungere all’elenco.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Quando utilizzi il tipo di namespace personalizzato, devi digitare manualmente lo spazio dei nomi prima di fornire i valori ID seguenti.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Al termine, seleziona **[!UICONTROL Crea]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

La finestra di dialogo scompare e il nuovo processo (o processi) viene elencato nel widget Richieste di lavoro insieme al relativo stato di elaborazione corrente.

### Caricare un file JSON {#json}

Quando crei richieste più complesse, ad esempio quelle che utilizzano più tipi di ID per ogni persona interessata da elaborare, puoi creare una richiesta caricando un file JSON.

Seleziona la freccia accanto a **[!UICONTROL Crea richiesta]**, sotto il widget Rapporto di stato sul lato destro dello schermo. Dall’elenco delle opzioni visualizzate, seleziona **[!UICONTROL Carica JSON]**.

![Opzioni di creazione richieste](../images/user-guide/create-options.png)

La **[!UICONTROL Carica JSON]** viene visualizzata una finestra di dialogo in cui puoi trascinare e rilasciare il file JSON.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Se non hai un file JSON da caricare, seleziona **[!UICONTROL Scarica Adobe-GDPR-Request.json]** per scaricare un modello che è possibile compilare in base ai valori raccolti dalle persone interessate.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Individua il file JSON sul tuo computer e trascinalo nella finestra di dialogo. Se il caricamento ha esito positivo, il nome del file viene visualizzato nella finestra di dialogo. Puoi continuare ad aggiungere altri file JSON, se necessario, trascinandoli nella finestra di dialogo.

Al termine, seleziona **[!UICONTROL Crea]**. La finestra di dialogo scompare e il nuovo processo (o processi) viene elencato nel widget Richieste di lavoro insieme al relativo stato di elaborazione corrente.

### Passaggi successivi

Leggendo questo documento, hai imparato a utilizzare il [!DNL Privacy Service] Interfaccia utente per creare un processo di privacy, visualizzare i dettagli di un processo e monitorarne lo stato di elaborazione e scaricare i risultati una volta completato.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando il [!DNL Privacy Service] API, fai riferimento al [Guida all’API](../api/overview.md).
