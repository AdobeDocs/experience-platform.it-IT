---
keywords: Experience Platform;home;argomenti popolari;esportare;esportare;;home;popular topic;export;Export
solution: Experience Platform
title: Gestire i processi relativi alla privacy nell’interfaccia utente di Privacy Service
description: Scopri come utilizzare l’interfaccia utente di Privacy Service per coordinare e monitorare le richieste di accesso a dati personali tra le varie applicazioni Experience Cloud.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: b960e67789acaeb27a0a39db933a2bbb7d84f4d5
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 12%

---

# Gestione dei processi relativi alla privacy nell’interfaccia utente di Privacy Service {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="Rispettare le richieste sulla privacy dell’interessato"
>abstract="<h2>Descrizione</h2><p>Adobe Experience Platform Privacy Service ti consente di creare e gestire le richieste sulla privacy per conto dei clienti che desiderano accedere o cancellare i propri dati personali in conformità alle normative legali sulla privacy.</p>"

In questo documento vengono descritti i passaggi per la creazione e la gestione delle richieste di accesso a dati personali tramite l&#39;interfaccia utente [!DNL Privacy Service].

>[!IMPORTANT]
>
>Privacy Service è destinato solo agli interessati e alle richieste dei diritti dei consumatori. Qualsiasi altro utilizzo di Privacy Service per la pulizia o la manutenzione dei dati non è supportato o consentito. Adobe ha l’obbligo legale di soddisfarli in modo tempestivo. Di conseguenza, il test di carico su Privacy Service non è consentito in quanto si tratta di un ambiente di sola produzione e crea un backlog inutile di richieste di privacy valide.
>
>È ora disponibile un limite massimo di caricamento giornaliero per evitare abusi del servizio. Se gli utenti rilevano un abuso del sistema, l’accesso al servizio verrà disattivato. Successivamente si terrà una riunione con i due partner per discutere le loro azioni e l&#39;uso accettabile di Privacy Service.

## Sfoglia il dashboard dell&#39;interfaccia utente [!DNL Privacy Service]

Il dashboard per l&#39;interfaccia utente di [!DNL Privacy Service] fornisce due widget che consentono di visualizzare lo stato dei processi di privacy: &quot;[!UICONTROL Status Report]&quot; e &quot;[!UICONTROL Job Requests]&quot;. Il dashboard visualizza anche il regolamento corrente selezionato per i job visualizzati.

![Dashboard interfaccia utente](../images/user-guide/dashboard.png)

### Tipo di regolamento

[!DNL Privacy Service] supporta le richieste di processi per diverse normative sulla privacy. Nella tabella seguente sono elencate le normative supportate e l’etichetta corrispondente, come rappresentata nell’interfaccia utente.

Consulta la [Panoramica sulle normative sulla privacy](../regulations/overview.md) per una descrizione di ogni regolamento che spiega i diritti dei consumatori e gli obblighi aziendali imposti.

>[!TIP]
>
>Il tipo di regolamento API è stato incluso per comodità generale.

| Etichetta interfaccia utente | API `regulation_type` | Regolamento |
|-------------------------------------------|-----------------------|----------------|
| [!UICONTROL APA_AUS (Australia)] | `apa_aus` | [!DNL Australia Privacy Act] |
| [!UICONTROL CCCA (California)] | `ccpa` | [!DNL California Consumer Privacy Act] (CCPA) |
| [!UICONTROL CPA_CO_USA (Colorado)] | `cpa_co_usa` | [!DNL Colorado Privacy Act] |
| [!UICONTROL CPRA_CA_USA (California)] | `cpra_ca_usa` | [!DNL California Privacy Rights Act] (CPRA) |
| [!UICONTROL CTDPA_CT_USA (Connecticut)] | `ctdpa_ct_usa` | [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL DPDPA_DE_USA (Delaware)] | `dpdpa_de_usa` | [!DNL Delaware Personal Data Privacy Act] |
| [!UICONTROL FDBR_FL_USA (Florida)] | `fdbr_fl_usa` | [!DNL Florida Digital Bill of Rights] |
| [!UICONTROL GDPR (European Union)] | `gdpr` | Il [!DNL General Data Protection Regulation] dell&#39;Unione Europea |
| [!UICONTROL HIPAA_USA (United States)] | `hipaa_usa` | [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL ICDPALIA_USA (Iowa)] | `icdpa_ia_usa` | [!DNL Iowa Consumer Data Protection Act] |
| [!UICONTROL LGPD_BRA (Brazil)] | `lgpd_bra` | Brasile: &quot;[!DNL General Data Protection Law]&quot; [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL MCDPA_MN_USA (Minnesota)] | `mcdpa_mn_usa` | [!DNL Minnesota Consumer Data Privacy Act] |
| [!UICONTROL MCDPA_MT_USA (Montana)] | `mcdpa_mt_usa` | [!DNL Montana Consumer Data Privacy Act] |
| [!UICONTROL MHMDA_WA_USA (Washington)] | `mhmda_wa_usa` | [!DNL Washington My Health My Data Act] |
| [!UICONTROL MODPA_MD_USA (Maryland)] | `modpa_md_usa` | [!DNL Maryland Online Data Privacy Act] |
| [!UICONTROL NDPA_NE_USA (Nebraska)] | `ndpa_ne_usa` | [!DNL Nebraska Data Protection Act] |
| [!UICONTROL NHPA_NH_USA (New Hampshire)] | `nhpa_nh_usa` | [!DNL New Hampshire Privacy Act] |
| [!UICONTROL NJDPA_NJ_USA (New Jersey)] | `njdpa_nj_usa` | [!DNL New Jersey Data Protection Act] |
| [!UICONTROL NZPA_NZL (New Zealand)] | `nzpa_nzl` | Nuova Zelanda: [!DNL Privacy Act] (PA) |
| [!UICONTROL OCPA_OR_USA (Oregon)] | `ocpa_or_usa` | [!DNL Oregon Consumer Privacy Act] |
| [!UICONTROL PDPA_THA (Thailand)] | `pdpa_tha` | Thailandese [!DNL Personal Data Protection Act] (PDPA) |
| [!UICONTROL PIPA_KOR (South Korea)] | `pipa_kor` | Corea del Sud [!DNL Personal Information Privacy Act] (PIPA) |
| [!UICONTROL QL25_QC_CAN (Quebec)] | `ql25_qc_can` | [!DNL Quebec Law 25] |
| [!UICONTROL TDPSA_TX_USA (Texas)] | `tdpsa_tx_usa` | [!DNL Texas Data Privacy and Security Act] |
| [!UICONTROL TIPA_TN_USA (Tennessee)] | `tipa_tn_usa` | [!DNL Tennessee Information Protection Act] |
| [!UICONTROL UCPA_UT_USA (Utah)] | `ucpa_ut_usa` | [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_VA_USA (Virginia)] | `vcdpa_va_usa` | [!DNL Virginia Consumer Data Protection Act] (VCDPA) |

{style="table-layout:auto"}

<!-- | [!UICONTROL ICDPA_IN_USA (Indiana)]       | `icdpa_in_usa` | [!DNL Indiana Consumer Data Protection Act]| NOT SUPP YET JAN 1st ### ... -->
<!-- | [!UICONTROL KCDPA_KY_USA (Kentucky)]      | `kcdpa_ky_usa`| [!DNL Kentucky Consumer Data Protection Act]|  NOT SUPP YET JAN 1st ### ... -->
<!-- | [!UICONTROL RIDTPPA_RI_USA (Rhode Island)]| `ridtppa_ri_usa` | [!DNL Rhode Island Data Transparency and Privacy Protection Act]|  NOT SUPP YET JAN 1st ### ... -->

>[!NOTE]
>
>Per ulteriori informazioni sul contesto legale di ciascun regolamento, consulta la panoramica sulle [normative sulla privacy supportate](../regulations/overview.md).

I processi per ogni tipo di regolamento vengono tracciati separatamente. Per passare da un tipo di regolamento all&#39;altro, selezionare il menu a discesa **[!UICONTROL Regulation Type]** e selezionare il regolamento desiderato dall&#39;elenco.

![Console Privacy Service con elenco a discesa Tipo di regolamento.](../images/user-guide/regulation.png)

Quando si modifica il tipo di regolamento, il dashboard viene aggiornato in modo da visualizzare tutte le operazioni, i filtri, i widget e le finestre di dialogo per la creazione di posti di lavoro che si applicano al regolamento selezionato.

![Dashboard aggiornato](../images/user-guide/dashboard-update.png)

### Rapporto di stato

Il grafico sul lato sinistro del widget Rapporto di stato tiene traccia dei processi inviati rispetto a quelli che potrebbero essere stati segnalati con errori. Il grafico sul lato destro traccia i processi che si avvicinano alla fine dell’intervallo di conformità di 30 giorni.

Seleziona uno dei due pulsanti di attivazione/disattivazione sopra il grafico per mostrare o nascondere le rispettive metriche.

![](../images/user-guide/hide-errors.png)

Puoi visualizzare il numero esatto di processi associati a qualsiasi punto dati sui grafici passando il mouse sopra il punto dati in questione.

![Punti dati da passare con il mouse](../images/user-guide/mouse-over.png)

Per visualizzare ulteriori dettagli su un dato punto dati, selezionare il punto dati in questione per visualizzare i job associati nel widget Richieste di job. Prendi nota del filtro applicato appena sopra l’elenco dei processi.

![Filtro applicato dal widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Quando è stato applicato un filtro al widget Richieste di lavoro, è possibile rimuovere il filtro selezionando **X** nella pillola del filtro. Le richieste di lavoro quindi tornano all&#39;elenco di tracciamento predefinito.

### Richieste di lavoro {#job-requests}

Nell&#39;area di lavoro [!UICONTROL Job Requests] sono elencati i dettagli relativi alle richieste di processi recenti nell&#39;organizzazione. I dettagli includono il tipo di richiesta, lo stato corrente, la data di scadenza, l’e-mail del richiedente e così via. Vengono caricati set di 100 record alla volta. Per impostazione predefinita, i processi creati più di recente vengono visualizzati nella parte superiore con più set di record caricati mentre si scorre verso il basso per sfogliare.

>[!NOTE]
>
>I dati per i processi creati in precedenza sono accessibili solo per 30 giorni dopo la data di completamento.

È possibile filtrare l&#39;elenco digitando parole chiave nella barra di ricerca sotto il titolo [!UICONTROL Job Requests]. L’elenco filtra automaticamente durante la digitazione, mostrando le richieste che contengono valori che corrispondono ai termini di ricerca. Il campo di ricerca esegue una ricerca &quot;rapida&quot; che corrisponde agli ID del processo di privacy dei processi attualmente renderizzati/caricati nell’interfaccia utente. Non è una ricerca completa di tutti i lavori inviati. Si tratta piuttosto di un filtro applicato ai risultati caricati. Utilizza l&#39;API di Privacy Service per [restituire processi in base a un regolamento specifico, intervalli di date o un singolo processo](../api/privacy-jobs.md#list).

>[!TIP]
>
>Per caricare i record nell’interfaccia utente degli ultimi 30 giorni, devi scorrere la tabella verso il basso e caricare altri batch di record.

![Sezione Richiesta processo console per la privacy con il campo di ricerca evidenziato.](../images/user-guide/job-search.png)

In alternativa, utilizza il pulsante di ricerca per eseguire una query del processo di privacy che si estende su un particolare intervallo di date. Questa azione restituisce tutti i processi relativi alla privacy inviati dall’organizzazione durante l’intervallo di tempo specificato. Selezionare il menu a discesa **[!UICONTROL Requested on]** per scegliere una data di inizio e una data di fine per la query. Le opzioni disponibili sono [!UICONTROL Today], [!UICONTROL Last 7 Days], [!UICONTROL Last 2 Weeks], [!UICONTROL Last 30 Days] o [!UICONTROL Custom]. Se utilizzata con l&#39;opzione [!UICONTROL Requested on], la funzionalità di ricerca visualizza solo le richieste di processo inviate tra gli intervalli di date selezionati.

![Sezione Richiesta processo con il campo di ricerca, il menu a discesa Richiesto e il pulsante Cerca evidenziato.](../images/user-guide/requested-on-dropdown-menu.png)

Per visualizzare i dettagli di una particolare richiesta di processo, selezionare l&#39;ID processo della richiesta dall&#39;elenco per aprire la pagina **[!UICONTROL Job Details]**.

![Dettagli processo interfaccia utente RGPD](../images/user-guide/job-details.png)

Questa finestra di dialogo contiene informazioni sullo stato di ciascuna soluzione [!DNL Experience Cloud] e del relativo stato corrente in relazione al processo complessivo. Poiché ogni processo di privacy è asincrono, la pagina visualizza la data e l’ora di comunicazione più recente (GMT) di ogni soluzione, in quanto alcune richiedono più tempo di altre per elaborare la richiesta.

Se una soluzione ha fornito dati aggiuntivi, questi sono visualizzabili in questa finestra di dialogo. Puoi visualizzare questi dati selezionando singole righe di prodotto.

Per scaricare i dati del processo completo come file CSV, seleziona **[!UICONTROL Export to CSV]** in alto a destra nella finestra di dialogo.

## Crea una nuova richiesta di processo per la privacy {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="Istruzioni"
>abstract="<ul><li>Seleziona <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=it#logging-in-from-experience-platform">Richieste</a> nel menu di navigazione a sinistra per aprire l’interfaccia utente della privacy, quindi seleziona <b>Crea richiesta</b>.</li><li>Da qui puoi utilizzare il generatore di richieste o caricare un file JSON di persone interessate.</li><li>Se utilizzi il generatore di richieste, seleziona il tipo di processo (accesso e/o eliminazione), quindi scegli il tipo di identità fornito (e-mail, ECID o AAID) oppure immetti uno spazio dei nomi di identità personalizzato. Una volta terminato, immetti i valori di identità appropriati per i clienti e seleziona <b>Crea</b>.</li><li>Se carichi un file JSON, seleziona la freccia accanto a Crea richiesta. Dall’elenco delle opzioni, seleziona <b>Carica JSON</b> e carica il file. Se non disponi di un file JSON da caricare, seleziona <b>Scarica Adobe-GDPR-Request.json</b> per scaricare un modello da poter compilare. Una volta terminato, carica il file JSON e seleziona <b>Crea</b>.</li><li>Per ulteriori informazioni su questa funzione, consulta la sezione <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=it">Guida utente di Privacy Service</a> su Experience League.</li></ul>"

>[!NOTE]
>
>Per creare una richiesta di processo per la privacy, devi fornire informazioni sull’identità per i clienti specifici i cui dati devono essere accessibili o eliminati. Rivedi il documento su [dati di identità per le richieste di privacy](../identity-data.md) prima di continuare con questa sezione.

L&#39;interfaccia utente di [!DNL Privacy Service] fornisce due metodi per creare nuove richieste di processi:

* [Utilizzare Request Builder](#request-builder)
* [Caricare un file JSON](#json)

I passaggi per l’utilizzo di ciascuno di questi metodi sono descritti nelle sezioni seguenti.

### Utilizzare Request Builder {#request-builder}

Utilizzando il Generatore di richieste, puoi creare manualmente una nuova richiesta di processo per la privacy nell’interfaccia utente. Request Builder (Generatore di richieste) è indicato per set di richieste più semplici e piccoli, perché il Generatore di richieste limita le richieste in modo che abbiano solo il tipo ID per utente. Per richieste più complesse, potrebbe essere preferibile [caricare un file JSON](#json).

Per iniziare a utilizzare il Generatore di richieste, seleziona **[!UICONTROL Create Request]** sotto il widget Rapporto di stato sul lato destro dello schermo.

![Seleziona Crea richiesta](../images/user-guide/create-request.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Create Request]**, in cui sono visualizzate le opzioni disponibili per l&#39;invio di una richiesta di processo per la privacy per il tipo di regolamento attualmente selezionato.

![](../images/user-guide/request-builder.png){width=500}

Selezionare **[!UICONTROL Job Type]** della richiesta (&quot;Elimina&quot; o &quot;Accesso&quot;) e uno o più prodotti disponibili dall&#39;elenco.

Privacy Service supporta due tipi di richieste di processi per dati personali: [!UICONTROL Access] (lettura) e/o [!UICONTROL Delete]. È possibile inviare una richiesta per ricevere tutte le informazioni contenute nel prodotto relative all&#39;oggetto della richiesta oppure richiedere la cancellazione di tutte le informazioni relative all&#39;oggetto della richiesta.

![](../images/user-guide/type-and-products.png){width=500}

In **[!UICONTROL Namespace type]**, selezionare il tipo di spazio dei nomi appropriato per gli ID cliente da inviare a [!DNL Privacy Service].

![](../images/user-guide/namespace-type.png){width=500}

Quando utilizzi il tipo di spazio dei nomi standard, seleziona uno spazio dei nomi dal menu a discesa (e-mail, ECID o AAID), quindi digita i valori ID nella casella di testo a destra, premendo **\&lt;invio>** per ogni ID per aggiungerlo all&#39;elenco.

![](../images/user-guide/standard-namespace.png){width=500}

Quando utilizzi il tipo di spazio dei nomi personalizzato, devi immettere manualmente lo spazio dei nomi prima di fornire i valori ID seguenti.

![](../images/user-guide/custom-namespace.png){width=500}

Al termine, selezionare **[!UICONTROL Create]**.

![](../images/user-guide/request-builder-create.png){width=500}

La finestra di dialogo scompare e il nuovo job (o job) viene elencato nel widget Richieste di job insieme al relativo stato di elaborazione corrente.

### Caricare un file JSON {#json}

Quando crei richieste più complicate, ad esempio quelle che utilizzano più tipi di ID per ogni persona interessata elaborata, puoi creare una richiesta caricando un file JSON.

Selezionare la freccia accanto a **[!UICONTROL Create Request]**, sotto il widget Rapporto di stato sul lato destro dello schermo. Dall&#39;elenco delle opzioni visualizzate, selezionare **[!UICONTROL Upload JSON]**.

![Opzioni di creazione richieste](../images/user-guide/create-options.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Upload JSON]**, che fornisce una finestra in cui trascinare il file JSON in.

![](../images/user-guide/upload-json.png){width=500}

Se non hai un file JSON da caricare, seleziona **[!UICONTROL Download Adobe-GDPR-Request.json]** per scaricare un modello che puoi compilare in base ai valori raccolti dalle persone interessate.


![](../images/user-guide/privacy-template.png){width=500}


Individua il file JSON sul computer e trascinalo nella finestra di dialogo. Se il caricamento ha esito positivo, il nome del file viene visualizzato nella finestra di dialogo. Puoi continuare ad aggiungere altri file JSON, se necessario, trascinandoli nella finestra di dialogo.

Al termine, selezionare **[!UICONTROL Create]**. La finestra di dialogo scompare e il nuovo job (o job) viene elencato nel widget Richieste di job insieme al relativo stato di elaborazione corrente.

### Passaggi successivi

Dopo aver letto questo documento, hai imparato a utilizzare l&#39;interfaccia utente [!DNL Privacy Service] per creare un processo di privacy, visualizzarne i dettagli, monitorarne lo stato di elaborazione e scaricare i risultati al termine del processo.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando l&#39;API [!DNL Privacy Service], fare riferimento alla [guida API](../api/overview.md).
