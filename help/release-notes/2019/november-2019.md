---
title: Note sulla versione di Adobe Experience Platform novembre 2019
description: Note sulla versione di novembre 2019 per Adobe Experience Platform.
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 7%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 18 novembre 2019**

Nuove funzioni di Adobe Experience Platform:
* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Aggiornamenti alle funzioni esistenti:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Basato su Adobe Experience Platform, Real-time Customer Data Platform (Real-Time CDP) consente alle aziende di unire dati noti e sconosciuti per attivare profili cliente con decisioni intelligenti in tutto il percorso del cliente. Real-Time CDP combina più origini dati aziendali per creare profili unificati in tempo reale che possono essere utilizzati per fornire ai clienti esperienze personalizzate uno a uno su tutti i canali e i dispositivi.

[!DNL Real-Time Customer Data Platform] include strumenti per la governance dei dati, la gestione delle identità, la segmentazione avanzata e la scienza dei dati che consentono di creare profili e definire tipi di pubblico, nonché di ottenere informazioni approfondite e al tempo stesso di applicare criteri rigorosi per la governance dei dati.

Adobe si connette a un ampio ecosistema di partner, per non parlare delle integrazioni native con Adobe Experience Cloud, in modo da poter attivare facilmente questi tipi di pubblico e fornire esperienze cliente eccellenti su tutti i canali, dalla personalizzazione in sito o in-app a e-mail, media a pagamento, call center, dispositivi connessi e altro ancora.

Con Real-Time CDP è possibile:

* Ottieni una visione unica del tuo cliente con la raccolta in streaming dei dati dei clienti da tutta l’azienda.
* Gestisci in modo responsabile i profili con governance e controlli sulla privacy affidabili per gli identificatori noti e sconosciuti.
* Genera informazioni actionable e ridimensiona i tipi di pubblico con intelligenza artificiale e apprendimento automatico basati su Adobe Sensei e progettati per gli esperti di marketing.
* Distribuisci esperienze personalizzate in tempo reale su tutti i canali e le destinazioni.

Per ulteriori informazioni, consulta la [documentazione di Real-time Customer Data Platform](../../rtcdp/overview.md).

**Funzioni principali**

| Funzione | Descrizione |
|---|---|
| Destinazioni | Integrazioni predefinite con piattaforme di destinazione supportate da [!DNL Real-Time Customer Data Platform] di Adobe che attivano i dati per tali partner in modo semplice. Per ulteriori informazioni, consulta [Destinazioni](#destinations). |
| Dashboard delle metriche della home page | La pagina Home di Real-time Customer Data Platform (Real-Time CDP) include una dashboard delle metriche che mostra informazioni su profili e segmenti. La pagina Home contiene anche collegamenti ai materiali di apprendimento. Consulta la sezione sulle [metriche Real-time Customer Data Platform](#real-time-customer-data-platform-metrics) di seguito. |
| Origini | Puoi acquisire dati da diverse origini, ad esempio soluzioni Adobe, archiviazione basata su cloud, software di terze parti e CRM. Per ulteriori informazioni, consulta la sezione [Origini](#sources) di seguito. |

**[!DNL Real-Time Customer Data Platform]metriche**

Quando accedi a Real-Time CDP, viene visualizzata la home page di Real-time Customer Data Platform (Real-Time CDP), che include una dashboard delle metriche.

La home page è solo una delle posizioni in cui vengono visualizzate le schede metriche. Real-Time CDP fornisce schede di metrica per tutta la tua esperienza. Queste metriche ti informano sui dati, sul profilo e sui segmenti di pubblico nel sistema.

Se al momento dell&#39;accesso a Real-Time CDP non sono presenti dati, la dashboard nella home page non viene visualizzata. In questo caso, la pagina Home fornisce materiale di apprendimento per la prima esperienza utente. Durante la raccolta dei dati, il dashboard viene aggiornato automaticamente per visualizzare informazioni su tali dati.

Per ulteriori informazioni, consulta la [panoramica delle metriche di Real-time Customer Data Platform](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione supportate da Real-time Customer Data Platform Adobe che attivano i dati per tali partner in modo semplice. Per ulteriori informazioni, leggere l&#39;articolo [Panoramica sulle destinazioni](../../destinations/home.md).

**Destinazioni disponibili**

Con la versione di novembre, Adobe Real-time Customer Data Platform supporta le seguenti destinazioni:

* Advertising: [!DNL Google]
* E-mail marketing: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Per informazioni su ciascuna destinazione, vedere il [catalogo di destinazione](../../destinations/catalog/overview.md).

**Limitazioni note**

* Il controllo per consentire pianificazioni di attivazione personalizzate nel flusso di attivazione (passaggio Pianificazione) non è disponibile con la versione iniziale.
* Attualmente non è possibile modificare o eliminare una configurazione di destinazione. Per ovviare a questo limite, puoi abilitare o disabilitare la destinazione nell&#39;angolo in alto a destra della [pagina dei dettagli della destinazione](../../destinations/ui/destination-details-page.md).
* Al momento non è attiva alcuna convalida per i dettagli, il percorso o le credenziali dell&#39;account al momento della connessione all&#39;account di destinazione o di archiviazione. Assicurarsi di immettere le credenziali corrette e verificare la presenza di errori ortografici o errori di battitura.
* Con la versione iniziale non sono stati effettuati rinnovi delle credenziali. Una volta che un account è scaduto o deve essere aggiornato, devi creare una nuova connessione di destinazione e ripetere la mappatura dei segmenti mappati in precedenza.

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo consentire di strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Platform]. Puoi acquisire dati da diverse origini, ad esempio soluzioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di configurare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine ti consentono di eseguire l’autenticazione nei sistemi di storage e nei servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni principali**

| Funzione | Descrizione |
| ---------- | ------------ |
| Interfaccia utente origini | Nuova interfaccia utente per la creazione, la visualizzazione e la gestione delle connessioni di origine. |
| Flussi di lavoro rinnovati per i connettori CRM | Nuovo flusso di lavoro intuitivo dell&#39;interfaccia utente per la creazione e la gestione dei connettori [!DNL Microsoft Dynamics] e [!DNL Salesforce]. |
| Supporto del connettore per gli archivi basati su cloud | I connettori possono ora accedere agli archivi basati su cloud. Le nuove origini includono [!DNL Amazon S3], [!DNL Azure Blob] e server FTP/SFTP. |

**Problemi noti**

* I connettori Source per gli archivi basati su cloud non supportano l’acquisizione di file compressi.

Per ulteriori informazioni sulle origini, vedere [Panoramica delle origini](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] consente ai data scientist di generare senza problemi informazioni da dati e contenuti in applicazioni Adobe e sistemi di terze parti tramite la creazione e l&#39;operazionalizzazione di modelli di apprendimento automatico. [!DNL Data Science Workspace] è strettamente integrato con [!DNL Platform] e potenzia il ciclo di vita end-to-end della data science, inclusa l&#39;esplorazione e la preparazione dei dati XDM, seguito dallo sviluppo e dall&#39;operazionalizzazione dei modelli per arricchire automaticamente [!DNL Real-Time Customer Profile] con Machine Learning Insights.

**Nuove funzioni**

| Funzione | Descrizione |
| -----------| ---------- |
| Accesso ai dati con l&#39;SDK [!DNL Platform] | I blocchi appunti predefiniti di Ricette e modulo di avvio in [!DNL Python] ora utilizzano l&#39;SDK [!DNL Platform] per accedere ai dati. |
| Supporto per sandbox | Supporto per le future funzionalità sandbox (attualmente in versione beta), inclusa la possibilità di isolare blocchi appunti e ricette in sandbox di sviluppo o produzione. Per ulteriori informazioni, consulta la [panoramica delle sandbox](../../sandboxes/home.md). |

Per ulteriori informazioni, vedere [Panoramica di Data Science Workspace](../../data-science-workspace/home.md).

## Sistema [!DNL Experience Data Model] (XDM)  {#xdm}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da Adobe, è un tentativo di standardizzare i dati sull&#39;esperienza del cliente e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che fornisce informazioni in modo più veloce e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| ---------- | ------------ |
| Schema di notifica | Nuovo schema che rappresenta i dati di notifica inviati durante il processo di acquisizione dei dati. |
| Adobe di schemi DSP AdCloud | Sono stati aggiunti cinque nuovi schemi per rappresentare i metadati della piattaforma lato domanda (DSP) di Adobe Advertising Cloud: Posizionamento, Campagna, Pacchetto, Inserzionista, Account. |
| Gruppi di campi schema Dettagli implementazione ExperienceEvent | Nuovi gruppi di campi ExperienceEvent che aggiungono un campo standard per memorizzare informazioni sul software utilizzato per raccogliere l’evento. |
| [!DNL Profile Privacy] gruppi di campi | Nuovi gruppi di campi profilo che aggiungono campi per accettare i segnali di rinuncia generale e di vendita/condivisione per [!DNL Real-Time Customer Profile]. |
| Vincoli di formato per `xdm:alternateDisplayInfo` | I campi &quot;Titolo&quot; e &quot;Descrizione&quot; per `xdm:alternateDisplayInfo` devono essere entrambi stringhe per superare la convalida. |
| Modifica nome: XDM [!DNL Individual Profile] | Il titolo della classe &quot;XDM [!DNL Profile]&quot; è stato aggiornato a &quot;XDM [!DNL Individual Profile]&quot;. Il `$id` formale della classe non è stato modificato. |

**Problemi noti**

* Nessuno.

Per ulteriori informazioni sull&#39;utilizzo di XDM con l&#39;API [!DNL Schema Registry] e l&#39;interfaccia utente [!DNL Schema Editor], leggere la [documentazione del sistema XDM](../../xdm/home.md).

## [!DNL Real-Time Customer Profile] {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con [!DNL Real-Time Customer Profile] è possibile visualizzare una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, del sistema CRM e di terze parti. [!DNL Profile] consente di consolidare i dati disparati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| -----------| ---------- |
| Miglioramenti alla ricerca [!DNL Profile] | Gli utenti ora possono cercare profili utilizzando descrittori di riferimento ed entità correlate. |
| Pulizia dei dati per un determinato set di dati | Gli utenti possono ora eliminare i dati per un determinato set di dati o batch utilizzando l&#39;API dei processi di sistema [!DNL Profile]. |
| Miglioramenti alle query di Edge [!DNL Profile] | Le applicazioni ora possono eseguire query su Edge [!DNL Profile] in base a una qualsiasi delle identità di un determinato profilo. |
| Configurare i criteri di unione per proiezione | Le applicazioni possono ora configurare criteri di unione per ogni proiezione per generare una visualizzazione dei dati in base a un criterio di unione specifico. |
| Attributi calcolati | Gli attributi calcolati calcolano automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo per aggregare valori quali &quot;acquisto totale&quot;, &quot;valore del ciclo di vita&quot; o &quot;stato funnel&quot; in base a un evento in arrivo, a un evento in arrivo e a dati di profilo, oppure a un evento in arrivo, a dati di profilo e a eventi storici. |

**Correzioni di bug**

* Elenco semplificato delle strategie di unione degli ID disponibili nel flusso di lavoro di creazione dei criteri di unione.

**Problemi noti**

* Nessuno.

Per ulteriori informazioni su [!DNL Real-Time Customer Profile], inclusi tutorial e best practice per l&#39;utilizzo dei dati di [!DNL Profile], leggere la [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] fornisce un&#39;interfaccia utente e un&#39;API RESTful che consentono di creare segmenti e generare tipi di pubblico dai dati di [!DNL Real-Time Customer Profile]. Questi segmenti vengono configurati e gestiti centralmente in [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

| Funzione | Descrizione |
| -----------| ---------- |
| Segmentazione pianificata | Ora gli utenti possono abilitare la valutazione pianificata dei segmenti per tutti i segmenti tramite l’interfaccia utente e l’API. Una volta abilitati, tutti i segmenti verranno valutati una volta al giorno. Questo non influisce sulle funzionalità di segmentazione on-demand che continuano a funzionare come in precedenza.<br/><br/>Nota: la funzione di segmentazione pianificata non può essere utilizzata nelle sandbox con più di cinque criteri di unione per [!DNL XDM Individual Profile]. |
| Segmentazione in streaming | Il supporto per la valutazione continua dei segmenti (segmentazione in streaming) consente di valutare la maggior parte delle regole dei segmenti quando i dati passano in [!DNL Platform]. Ciò significa che l’iscrizione al segmento sarà aggiornata senza dover eseguire processi di segmentazione pianificati. Si applicano alcune eccezioni, ad esempio i segmenti che utilizzano relazioni tra più entità o con payload arricchiti. |
| Segmenti come blocchi predefiniti | Durante la creazione di segmenti tramite l’interfaccia utente del Generatore di segmenti, gli utenti possono ora utilizzare segmenti definiti in precedenza come blocchi predefiniti per altri segmenti. <ul><li>Riferimento all’iscrizione al pubblico corrente: aggiornamenti man mano che le persone si spostano all’interno e all’esterno del pubblico.</li><li>Copia logica: prendi la definizione del segmento selezionato e duplicala nel nuovo segmento.</li></ul> |
| Visualizzare l’iscrizione al segmento per spazio dei nomi ID | L’iscrizione al segmento ora può essere visualizzata per spazio dei nomi ID (e-mail, ECID e conteggio totale). |
| Supporto RBAC | Segment Builder ora fornisce supporto per controlli di accesso e autorizzazioni di base basati sul ruolo. |
| Supporto migliorato per la condivisione di tipi di pubblico esterni tra [!DNL Platform] e le soluzioni Adobe | Gli utenti possono ora inserire metadati di pubblico esterno (non [!DNL Experience Platform]) in scenari in cui il numero di tipi di pubblico è elevato o non è noto a priori. Questa versione include l&#39;accesso ai metadati [!DNL Audience Manager] per i clienti che hanno eseguito il provisioning del connettore della soluzione. Questi metadati di pubblico possono essere utilizzati in Segment Builder per creare nuovi segmenti [!DNL Experience Platform]. <br/><br/> Inoltre, i segmenti creati in [!DNL Experience Platform] saranno ora disponibili per l&#39;utilizzo in soluzioni Adobe integrate, tra cui [!DNL Audience Manager], [!DNL Target] e [!DNL Ad Cloud]. |

**Correzioni di bug**

* È stato risolto un problema che causava la restituzione da parte di Segmentazione di più entità di profili zero in caso di relazioni nidificate.
* È stato risolto un problema a causa del quale la logica di esclusione restituiva risultati fuorvianti.
* È stata migliorata la leggibilità per le cartelle con più entità. Ora mostrano il nome descrittivo della classe XDM.
* È stato risolto un problema intermittente a causa del quale venivano visualizzate più copie della stessa cartella XDM.
* La messaggistica ora viene generata per informare un utente se le stime dei segmenti non sono disponibili per il criterio di unione selezionato.

**Problemi noti**

* Nessuno.

Per ulteriori informazioni su [!DNL Segmentation Service], leggere la [Panoramica del servizio di segmentazione](../../segmentation/home.md).
