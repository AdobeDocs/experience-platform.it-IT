---
keywords: Experience Platform;home;argomenti popolari;esportare;Esportare
solution: Experience Platform
title: Gestire i processi relativi alla privacy nell’interfaccia utente di Privacy Service
description: Scopri come utilizzare l’interfaccia utente di Privacy Service per coordinare e monitorare le richieste di accesso a dati personali tra le varie applicazioni Experience Cloud.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 8ba06a5d572310e2822a5b3c9f82ff0721540f69
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 12%

---

# Gestione dei processi relativi alla privacy nell’interfaccia utente di Privacy Service {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="Rispettare le richieste sulla privacy dell’interessato"
>abstract="<h2>Descrizione</h2><p>Adobe Experience Platform Privacy Service ti consente di creare e gestire le richieste sulla privacy per conto dei clienti che desiderano accedere o cancellare i propri dati personali in conformità alle normative legali sulla privacy.</p>"

Questo documento descrive i passaggi da seguire per creare e gestire le richieste di accesso a dati personali tramite [!DNL Privacy Service] dell&#39;utente.

>[!IMPORTANT]
>
>Privacy Service è destinato solo alle richieste degli interessati e dei diritti dei consumatori. Qualsiasi altro utilizzo di Privacy Service per la pulizia o la manutenzione dei dati non è supportato o consentito. L&#39;Adobe ha l&#39;obbligo giuridico di adempiere tali obblighi in modo tempestivo. Di conseguenza, il test di carico su Privacy Service non è consentito in quanto si tratta di un ambiente di sola produzione e crea un backlog inutile di richieste di privacy valide.
>
>È ora disponibile un limite massimo di caricamento giornaliero per evitare abusi del servizio. Se gli utenti rilevano un abuso del sistema, l’accesso al servizio verrà disattivato. Successivamente si terrà una riunione con i Privacy Service per discutere le loro azioni e l&#39;uso accettabile di tali strumenti.

## Sfoglia [!DNL Privacy Service] Dashboard interfaccia utente

Dashboard per [!DNL Privacy Service] L’interfaccia utente fornisce due widget che ti consentono di visualizzare lo stato dei processi relativi alla privacy: &quot;[!UICONTROL Rapporto di stato]&quot; e &quot;[!UICONTROL Richieste di lavoro]&quot;. Il dashboard visualizza anche il regolamento corrente selezionato per i job visualizzati.

![Dashboard interfaccia utente](../images/user-guide/dashboard.png)

### Tipo di regolamento

[!DNL Privacy Service] supporta le richieste di lavoro per diverse normative sulla privacy. Nella tabella seguente sono elencate le normative supportate e l’etichetta corrispondente, come rappresentata nell’interfaccia utente:

| Etichetta interfaccia utente | Regolamento |
| --- | --- |
| [!UICONTROL APA_AUS] | [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL CPA] | [!DNL Colorado Privacy Act] |
| [!UICONTROL CCPA] | [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPRA_USA] | [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA] | [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL RGPD] | dell&#39;Unione europea [!DNL General Data Protection Regulation] |
| [!UICONTROL HIPAA_AUS] | [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL LGPD_BRA] | del Brasile [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL MHMDA] | [!DNL Washington My Health My Data Act] |
| [!UICONTROL NZPA_NZL] | La Nuova Zelanda [!DNL Privacy Act] |
| [!UICONTROL PDPA_THA] | thailandese [!DNL Personal Data Protection Act] |
| [!UICONTROL UCPA] | [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA] | [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

<!--Not released yet:
| [!UICONTROL PDPA_VNM] | Vietnam's [!DNL Personal Data Protection Decree] |
 -->

>[!NOTE]
>
>Consulta la panoramica su [normative sulla privacy supportate](../regulations/overview.md) per maggiori informazioni sul contesto giuridico di ciascun regolamento.

I processi per ogni tipo di regolamento vengono tracciati separatamente. Per passare da un tipo di regolamento all&#39;altro, selezionare **[!UICONTROL Tipo di regolamento]** e selezionare il regolamento desiderato dall&#39;elenco.

![La console Privacy Service con il menu a discesa Tipo di regolamento.](../images/user-guide/regulation.png)

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

### Richieste di lavoro {#job-requests}

Il [!UICONTROL Richieste di lavoro] workspace elenca i dettagli relativi alle richieste di job recenti nell&#39;organizzazione. I dettagli includono il tipo di richiesta, lo stato corrente, la data di scadenza, l’e-mail del richiedente e così via. Vengono caricati set di 100 record alla volta. Per impostazione predefinita, i processi creati più di recente vengono visualizzati nella parte superiore con più set di record caricati mentre si scorre verso il basso per sfogliare.

>[!NOTE]
>
>I dati per i processi creati in precedenza sono accessibili solo per 30 giorni dopo la data di completamento.

È possibile filtrare l&#39;elenco digitando parole chiave nella barra di ricerca sotto [!UICONTROL Richieste di lavoro] titolo. L’elenco filtra automaticamente durante la digitazione, mostrando le richieste che contengono valori che corrispondono ai termini di ricerca. Il campo di ricerca esegue una ricerca &quot;rapida&quot; che corrisponde agli ID del processo di privacy dei processi attualmente renderizzati/caricati nell’interfaccia utente. Non è una ricerca completa di tutti i lavori inviati. Si tratta piuttosto di un filtro applicato ai risultati caricati. Utilizza l’API Privacy Service per: [restituire i processi in base a una normativa specifica, intervalli di date o un singolo processo](../api/privacy-jobs.md#list).

>[!TIP]
>
>Per caricare i record nell’interfaccia utente degli ultimi 30 giorni, devi scorrere la tabella verso il basso e caricare altri batch di record.

![La sezione Richiesta processo di Privacy Console con il campo di ricerca evidenziato.](../images/user-guide/job-search.png)

In alternativa, utilizza il pulsante di ricerca per eseguire una query del processo di privacy che si estende su un particolare intervallo di date. Questa azione restituisce tutti i processi relativi alla privacy inviati dall’organizzazione durante l’intervallo di tempo specificato. Seleziona la **[!UICONTROL Richiesto il]** per scegliere una data di inizio e una data di fine per la query. Le opzioni disponibili includono [!UICONTROL Oggi], [!UICONTROL Ultimi 7 giorni], [!UICONTROL Ultime 2 settimane], [!UICONTROL Ultimi 30 giorni], o [!UICONTROL Personalizzato]. Se utilizzato con [!UICONTROL Richiesto il] , la funzione di ricerca visualizza solo le richieste di lavoro inviate tra gli intervalli di date scelti.

![La sezione Richiesta di lavoro con il campo di ricerca, il menu a discesa Richiesto e il pulsante Cerca evidenziato.](../images/user-guide/requested-on-dropdown-menu.png)

Per visualizzare i dettagli di una particolare richiesta di processo, seleziona l’ID processo della richiesta dall’elenco per aprire **[!UICONTROL Dettagli processo]** pagina.

![Dettagli processo interfaccia utente RGPD](../images/user-guide/job-details.png)

Questa finestra di dialogo contiene informazioni sullo stato di ciascuna [!DNL Experience Cloud] e il suo stato attuale in relazione al lavoro complessivo. Poiché ogni processo di privacy è asincrono, la pagina visualizza la data e l’ora di comunicazione più recente (GMT) di ogni soluzione, in quanto alcune richiedono più tempo di altre per elaborare la richiesta.

Se una soluzione ha fornito dati aggiuntivi, questi sono visualizzabili in questa finestra di dialogo. Puoi visualizzare questi dati selezionando singole righe di prodotto.

Per scaricare i dati del processo completo come file CSV, seleziona **[!UICONTROL Esporta in CSV]** in alto a destra nella finestra di dialogo.

## Crea una nuova richiesta di processo per la privacy {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="Istruzioni"
>abstract="<ul><li>Seleziona <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=it#logging-in-from-experience-platform">Richieste</a> nel menu di navigazione a sinistra per aprire l’interfaccia utente della privacy, quindi seleziona <b>Crea richiesta</b>.</li><li>Da qui puoi utilizzare il generatore di richieste o caricare un file JSON di persone interessate.</li><li>Se utilizzi il generatore di richieste, seleziona il tipo di processo (accesso e/o eliminazione), quindi scegli il tipo di identità fornito (e-mail, ECID o AAID) oppure immetti uno spazio dei nomi di identità personalizzato. Una volta terminato, immetti i valori di identità appropriati per i clienti e seleziona <b>Crea</b>.</li><li>Se carichi un file JSON, seleziona la freccia accanto a Crea richiesta. Dall’elenco delle opzioni, seleziona <b>Carica JSON</b> e carica il file. Se non disponi di un file JSON da caricare, seleziona <b>Scarica Adobe-GDPR-Request.json</b> per scaricare un modello da poter compilare. Una volta terminato, carica il file JSON e seleziona <b>Crea</b>.</li><li>Per ulteriori informazioni su questa funzione, consulta la sezione <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=it">Guida utente di Privacy Service</a> su Experience League.</li></ul>"

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

Privacy Service supporta due tipi di richieste di lavoro per dati personali: [!UICONTROL Accesso] (leggi) e/o [!UICONTROL Elimina]. È possibile inviare una richiesta per ricevere tutte le informazioni contenute nel prodotto relative all&#39;oggetto della richiesta oppure richiedere la cancellazione di tutte le informazioni relative all&#39;oggetto della richiesta.

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
