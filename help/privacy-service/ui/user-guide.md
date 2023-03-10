---
keywords: Experience Platform;home;argomenti popolari;esportare;Esportare
solution: Experience Platform
title: Gestire i processi relativi alla privacy nell’interfaccia utente di Privacy Service
description: Scopri come utilizzare l’interfaccia utente di Privacy Service per coordinare e monitorare le richieste di accesso a dati personali tra le varie applicazioni Experience Cloud.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: e539b1e165227d9a888bfe12d8205e285b3ce259
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---

# Gestire i processi relativi alla privacy nell’interfaccia utente di Privacy Service {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="Descrizione"
>abstract=""

Questo documento descrive i passaggi da seguire per creare e gestire le richieste di accesso a dati personali tramite [!DNL Privacy Service] dell&#39;utente.

## Sfoglia [!DNL Privacy Service] Dashboard interfaccia utente

Dashboard per [!DNL Privacy Service] L’interfaccia utente fornisce due widget che ti consentono di visualizzare lo stato dei processi relativi alla privacy: &quot;[!UICONTROL Rapporto di stato]&quot; e &quot;[!UICONTROL Richieste di lavoro]&quot;. Il dashboard visualizza anche il regolamento corrente selezionato per i job visualizzati.

![Dashboard interfaccia utente](../images/user-guide/dashboard.png)

### Tipo di regolamento

[!DNL Privacy Service] supporta le richieste di lavoro per diverse normative sulla privacy. Nella tabella seguente sono elencate le normative supportate e l’etichetta corrispondente, come rappresentata nell’interfaccia utente:

| Etichetta interfaccia utente | Regolamento |
| --- | --- |
| [!UICONTROL CCPA] | Le selezioni del menu [!DNL California Consumer Privacy Act] |
| [!UICONTROL RGPD] | dell&#39;Unione europea [!DNL General Data Protection Regulation] |
| [!UICONTROL PDPA_THA] | thailandese [!DNL Personal Data Protection Act] |
| [!UICONTROL LGPD_BRA] | del Brasile [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL NZPA_NZL] | La Nuova Zelanda [!DNL Privacy Act] |
| [!UICONTROL VCDPA_USA] | Le selezioni del menu [!DNL Virginia Consumer Data Protection Act] |
| [!UICONTROL CPRA_USA] | Le selezioni del menu [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL APA_AUS] | Le selezioni del menu [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL HIPAA_AUS] | Le selezioni del menu [!DNL Health Insurance Portability and Accountability Act] |

{style="table-layout:auto"}

>[!NOTE]
>
>Consulta la panoramica su [normative sulla privacy supportate](../regulations/overview.md) per maggiori informazioni sul contesto giuridico di ciascun regolamento.

I processi per ogni tipo di regolamento vengono tracciati separatamente. Per passare da un tipo di regolamento all&#39;altro, selezionare **[!UICONTROL Tipo di regolamento]** e selezionare il regolamento desiderato dall&#39;elenco.

![Menu a discesa Tipo di regolamento](../images/user-guide/regulation.png)

Quando si modifica il tipo di regolamento, il dashboard viene aggiornato in modo da visualizzare tutte le operazioni, i filtri, i widget e le finestre di dialogo per la creazione di posti di lavoro che si applicano al regolamento selezionato.

![Dashboard aggiornato](../images/user-guide/dashboard-update.png)

### Rapporto di stato

Il grafico sul lato sinistro del widget Rapporto di stato tiene traccia dei processi inviati rispetto a quelli che potrebbero essere stati segnalati con errori. Il grafico sul lato destro traccia i processi che si avvicinano alla fine dell’intervallo di conformità di 30 giorni.

Seleziona uno dei due pulsanti di attivazione/disattivazione sopra il grafico per mostrare o nascondere le rispettive metriche.

![](../images/user-guide/hide-errors.png)

Puoi visualizzare il numero esatto di processi associati a qualsiasi punto dati sui grafici passando il mouse sopra il punto dati in questione.

![Punti dati passando con il mouse](../images/user-guide/mouse-over.png)

Per visualizzare ulteriori dettagli su un dato punto dati, selezionare il punto dati in questione per visualizzare i job associati nel widget Richieste di job. Prendi nota del filtro applicato appena sopra l’elenco dei processi.

![Filtro applicato da widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Quando un filtro è stato applicato al widget Richieste di lavoro, è possibile rimuoverlo selezionando il **X** sulla pillola del filtro. Le richieste di lavoro quindi tornano all&#39;elenco di tracciamento predefinito.

### Richieste di lavoro

Il widget Richieste di lavoro elenca tutte le richieste di lavoro disponibili nell&#39;organizzazione, inclusi dettagli quali il tipo di richiesta, lo stato corrente, la data di scadenza e l&#39;e-mail del richiedente.

>[!NOTE]
>
>I dati per i processi creati in precedenza sono accessibili solo per 30 giorni dopo la data di completamento.

Per filtrare l’elenco, digita le parole chiave nella barra di ricerca sotto il titolo Richieste di lavoro. L’elenco filtra automaticamente durante la digitazione, mostrando le richieste che contengono valori che corrispondono ai termini di ricerca. È inoltre possibile utilizzare **[!UICONTROL Richiesto il]** per selezionare un intervallo di tempo per i job elencati.

![Opzioni di ricerca della richiesta di lavoro](../images/user-guide/job-search.png)

Per visualizzare i dettagli di una particolare richiesta di processo, seleziona l’ID processo della richiesta dall’elenco per aprire **[!UICONTROL Dettagli processo]** pagina.

![Dettagli processo interfaccia utente RGPD](../images/user-guide/job-details.png)

Questa finestra di dialogo contiene informazioni sullo stato di ciascuna [!DNL Experience Cloud] e il suo stato attuale in relazione al lavoro complessivo. Poiché ogni processo di privacy è asincrono, la pagina visualizza la data e l’ora di comunicazione più recente (GMT) di ogni soluzione, in quanto alcune richiedono più tempo di altre per elaborare la richiesta.

Se una soluzione ha fornito dati aggiuntivi, questi sono visualizzabili in questa finestra di dialogo. Puoi visualizzare questi dati selezionando singole righe di prodotto.

Per scaricare i dati del processo completo come file CSV, seleziona **[!UICONTROL Esporta in CSV]** in alto a destra nella finestra di dialogo.

## Crea una nuova richiesta di processo per la privacy {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="Istruzioni"
>abstract=""

>[!NOTE]
>
>Per creare una richiesta di processo per la privacy, devi fornire informazioni sull’identità per i clienti specifici i cui dati devono essere accessibili o eliminati. Rivedi il documento su [dati di identità per le richieste di privacy](../identity-data.md) prima di continuare con questa sezione.

Il [!DNL Privacy Service] L’interfaccia utente fornisce due metodi per creare nuove richieste di processi:

* [Utilizzare Request Builder](#request-builder)
* [Caricare un file JSON](#json)

I passaggi per l’utilizzo di ciascuno di questi metodi sono descritti nelle sezioni seguenti.

### Utilizzare Request Builder {#request-builder}

Utilizzando il Generatore di richieste, puoi creare manualmente una nuova richiesta di processo per la privacy nell’interfaccia utente. Request Builder (Generatore di richieste) è indicato per set di richieste più semplici e piccoli, perché il Generatore di richieste limita le richieste in modo che abbiano solo il tipo ID per utente. Per richieste più complicate, potrebbe essere meglio [caricare un file JSON](#json) invece.

Per iniziare a utilizzare il Generatore di richieste, seleziona **[!UICONTROL Crea richiesta]** sotto il widget Rapporto di stato sul lato destro dello schermo.

![Seleziona Crea richiesta](../images/user-guide/create-request.png)

Il **[!UICONTROL Crea richiesta]** viene visualizzata una finestra di dialogo in cui sono visualizzate le opzioni disponibili per l’invio di una richiesta di processo di privacy per il tipo di regolamento attualmente selezionato.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Seleziona la **[!UICONTROL Tipo di processo]** della richiesta (&quot;Elimina&quot; o &quot;Accesso&quot;) e uno o più prodotti disponibili dall’elenco.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Sotto **[!UICONTROL Tipo di spazio dei nomi]**, seleziona il tipo di spazio dei nomi appropriato per gli ID cliente a cui inviare [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Quando utilizzi il tipo di spazio dei nomi standard, seleziona uno spazio dei nomi dal menu a discesa (e-mail, ECID o AAID), quindi digita i valori ID nella casella di testo a destra, premendo **\&lt;enter>** per ogni ID per aggiungerlo all’elenco.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Quando utilizzi il tipo di spazio dei nomi personalizzato, devi immettere manualmente lo spazio dei nomi prima di fornire i valori ID seguenti.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Al termine, seleziona **[!UICONTROL Crea]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

La finestra di dialogo scompare e il nuovo job (o job) viene elencato nel widget Richieste di job insieme al relativo stato di elaborazione corrente.

### Caricare un file JSON {#json}

Quando crei richieste più complicate, ad esempio quelle che utilizzano più tipi di ID per ogni persona interessata elaborata, puoi creare una richiesta caricando un file JSON.

Seleziona la freccia accanto a **[!UICONTROL Crea richiesta]**, sotto il widget Rapporto di stato sul lato destro dello schermo. Dall&#39;elenco delle opzioni visualizzate, selezionare **[!UICONTROL Carica JSON]**.

![Opzioni di creazione delle richieste](../images/user-guide/create-options.png)

Il **[!UICONTROL Carica JSON]** viene visualizzata una finestra di dialogo che consente di trascinare e rilasciare il file JSON in.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Se non hai un file JSON da caricare, seleziona **[!UICONTROL Scarica Adobe-GDPR-Request.json]** per scaricare un modello che puoi compilare in base ai valori raccolti dalle persone interessate.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Individua il file JSON sul computer e trascinalo nella finestra di dialogo. Se il caricamento ha esito positivo, il nome del file viene visualizzato nella finestra di dialogo. Puoi continuare ad aggiungere altri file JSON, se necessario, trascinandoli nella finestra di dialogo.

Al termine, seleziona **[!UICONTROL Crea]**. La finestra di dialogo scompare e il nuovo job (o job) viene elencato nel widget Richieste di job insieme al relativo stato di elaborazione corrente.

### Passaggi successivi

Dopo aver letto questo documento, hai imparato a utilizzare [!DNL Privacy Service] Interfaccia utente per creare un processo di privacy, visualizzarne i dettagli e monitorarne lo stato di elaborazione e scaricare i risultati al termine del processo.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando [!DNL Privacy Service] API, fare riferimento al [Guida API](../api/overview.md).
