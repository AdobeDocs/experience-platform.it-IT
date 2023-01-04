---
title: Note sulla versione di Adobe Experience Platform - Novembre 2019
description: Note sulla versione di novembre 2019 per Adobe Experience Platform.
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 2%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 18 novembre 2019**

Nuove funzioni in Adobe Experience Platform:
* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Aggiornamenti alle funzioni esistenti:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Basato su Adobe Experience Platform, Real-time Customer Data Platform (Real-Time CDP) consente alle aziende di unire dati noti e sconosciuti per attivare i profili dei clienti con decisioni intelligenti in tutto il percorso di clienti. Real-Time CDP combina più origini dati aziendali per creare in tempo reale profili unificati che possono essere utilizzati per fornire esperienze cliente personalizzate uno-a-uno su tutti i canali e dispositivi.

[!DNL Real-Time Customer Data Platform] include strumenti per la governance dei dati, la gestione delle identità, la segmentazione avanzata e la scienza dei dati, in modo da poter creare profili e definire tipi di pubblico, nonché ottenere informazioni approfondite e al tempo stesso essere in grado di applicare politiche di governance dei dati rigorose.

L’Adobe si collega a un grande ecosistema di partner, per non parlare delle integrazioni native con Adobe Experience Cloud, per consentirti di attivare facilmente questi tipi di pubblico e offrire ottime esperienze cliente su tutti i canali, dalla personalizzazione on-site o in-app a e-mail, supporti a pagamento, call center, dispositivi collegati e altro ancora.

Con Real-Time CDP puoi:

* Ottieni un&#39;unica visualizzazione del tuo cliente con una raccolta in streaming dei dati del cliente da tutta l&#39;azienda.
* Gestisci in modo responsabile i profili con governance affidabile e controlli della privacy affidabili per gli identificatori noti e sconosciuti.
* Genera informazioni fruibili e scala i tipi di pubblico con intelligenza artificiale e machine learning basati su Adobe Sensei e costruiti per gli esperti di marketing.
* Offri esperienze personalizzate in tempo reale su tutti i canali e le destinazioni.

Per ulteriori informazioni, consulta la sezione [Documentazione di Real-time Customer Data Platform](../../rtcdp/overview.md).

**Funzionalità chiave**

| Funzione | Descrizione |
|---|---|
| Destinazioni | Integrazioni predefinite con piattaforme di destinazione supportate da Adobe [!DNL Real-Time Customer Data Platform] che attivano i dati a tali partner in modo semplice. Vedi [Destinazioni](#destinations) qui sotto per ulteriori informazioni. |
| Dashboard delle metriche della pagina principale | La home page di Real-time Customer Data Platform (Real-Time CDP) include un dashboard di metriche che mostra informazioni su profili e segmenti. La home page contiene anche collegamenti ai materiali di apprendimento. Vedi la sezione su [Metriche di Real-time Customer Data Platform](#real-time-customer-data-platform-metrics) sotto. |
| Origini | È possibile acquisire dati da diverse sorgenti, come soluzioni Adobe, archiviazione basata su cloud, software di terze parti e CRM. Consulta la sezione [Origini](#sources) per ulteriori informazioni, consulta la sezione seguente. |

**[!DNL Real-Time Customer Data Platform]metrica**

Quando accedi a Real-Time CDP, viene visualizzata la home page di Real-time Customer Data Platform (Real-Time CDP), che include un dashboard delle metriche.

La home page è solo una delle posizioni in cui vengono visualizzate le schede metriche. Real-Time CDP fornisce schede metriche per tutta l’esperienza. Queste metriche ti informano sui dati, sul profilo e sui segmenti di pubblico nel sistema.

Se non sono presenti dati nel sistema quando si accede a Real-Time CDP, il dashboard nella home page non viene visualizzato. In questo caso, la home page fornisce materiale di apprendimento per una prima esperienza utente. Man mano che i dati vengono raccolti, il dashboard si aggiorna automaticamente per visualizzare le informazioni relative a tali dati.

Per ulteriori informazioni, consulta la sezione [Panoramica delle metriche di Real-time Customer Data Platform](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione supportate da Real-time Customer Data Platform di Adobe che attivano i dati per tali partner in modo semplice. Per ulteriori informazioni, consulta la sezione [Panoramica sulle destinazioni](../../destinations/home.md) articolo.

**Destinazioni disponibili**

Con la versione di novembre, Adobe Real-time Customer Data Platform supporta le seguenti destinazioni:

* Advertising: [!DNL Google]
* E-mail marketing: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Consulta la sezione [catalogo di destinazione](../../destinations/catalog/overview.md) per informazioni su ciascuna delle destinazioni.

**Limitazioni note**

* Il controllo per consentire pianificazioni di attivazione personalizzate nel flusso di attivazione (passaggio Pianificazione) non è disponibile nella versione iniziale.
* Attualmente non è possibile modificare o eliminare una configurazione di destinazione. Per aggirare questa limitazione, puoi abilitare o disabilitare la destinazione nell’angolo in alto a destra della [pagina dei dettagli della destinazione](../../destinations/ui/destination-details-page.md).
* Al momento non è disponibile alcuna convalida per i dettagli dell&#39;account, il percorso o le credenziali quando ci si connette all&#39;account di destinazione o di archiviazione. Assicurati di immettere le credenziali corrette e di verificare la presenza di errori di ortografia o errori di battitura.
* Non sono in vigore rinnovi di credenziali con la versione iniziale. Una volta scaduto o necessario aggiornare un account, devi creare una nuova connessione di destinazione e mappare nuovamente i segmenti mappati in precedenza.

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse fonti come soluzioni Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di eseguire l’autenticazione nei sistemi di storage e nei servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ---------- | ------------ |
| Interfaccia utente Origini | Nuova interfaccia utente per la creazione, la visualizzazione e la gestione delle connessioni sorgente. |
| Flussi di lavoro aggiornati per i connettori di gestione delle relazioni con i clienti | Nuovo flusso di lavoro intuitivo dell’interfaccia utente per la creazione e la gestione [!DNL Microsoft Dynamics] e [!DNL Salesforce] connettori |
| Supporto del connettore per archivi basati su cloud | I connettori possono ora accedere agli archivi basati su cloud. Le nuove fonti includono [!DNL Amazon S3], [!DNL Azure Blob]e server FTP/SFTP. |

**Problemi noti**

* I connettori di origine per gli archivi basati su cloud non supportano l’acquisizione di file compressi.

Per ulteriori informazioni sulle origini, consulta [Panoramica delle origini](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] consente agli scienziati dei dati di generare in modo semplice informazioni provenienti da dati e contenuti tra applicazioni di Adobe e sistemi di terze parti creando e operando modelli di apprendimento automatico. [!DNL Data Science Workspace] è strettamente integrato con [!DNL Platform] e potenzia il ciclo di vita completo della scienza dei dati, inclusa l&#39;esplorazione e la preparazione dei dati XDM, seguiti dallo sviluppo e dall&#39;operazionalizzazione dei modelli per arricchire automaticamente [!DNL Real-Time Customer Profile] con informazioni sull&#39;apprendimento automatico.

**Nuove funzioni**

| Funzione | Descrizione |
| -----------| ---------- |
| Accesso ai dati tramite [!DNL Platform] SDK | Notebook da incasso e da avvio precompilati in [!DNL Python] ora utilizza [!DNL Platform] SDK per l’accesso ai dati. |
| Supporto per sandbox | Supporto per le prossime funzionalità sandbox (attualmente in versione beta), inclusa la possibilità di isolare i blocchi appunti e le ricette nelle sandbox di sviluppo o produzione. Consulta la sezione [panoramica sulle sandbox](../../sandboxes/home.md) per ulteriori informazioni. |

Per ulteriori informazioni, consulta la sezione [Panoramica di Data Science Workspace](../../data-science-workspace/home.md).

## Sistema [!DNL Experience Data Model] (XDM)  {#xdm}

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base della [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare il potere delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che offre informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| ---------- | ------------ |
| Schema di notifica | Nuovo schema che rappresenta i dati di notifica inviati durante il processo di inserimento dei dati. |
| Schemi DSP di Adobe AdCloud | Sono stati aggiunti cinque nuovi schemi per rappresentare i metadati della piattaforma Adobe Advertising Cloud lato domanda (DSP): Posizionamento, campagna, pacchetto, inserzionista, account. |
| Gruppi di campi dello schema Dettagli implementazione di ExperienceEvent | Nuovi gruppi di campi ExperienceEvent che aggiungono un campo standard per memorizzare informazioni sul software utilizzato per raccogliere l&#39;evento. |
| [!DNL Profile Privacy] gruppi di campi | Nuovi gruppi di campi di profilo che aggiungono campi per accettare segnali di rinuncia generali e di vendita/condivisione per [!DNL Real-Time Customer Profile]. |
| Vincoli del formato per `xdm:alternateDisplayInfo` | I campi &quot;Titolo&quot; e &quot;Descrizione&quot; per `xdm:alternateDisplayInfo` devono essere entrambe stringhe per trasmettere la convalida. |
| Modifica del nome: XDM [!DNL Individual Profile] | Il &quot;titolo&quot; di &quot;XDM [!DNL Profile]&quot; la classe è stata aggiornata in &quot;XDM [!DNL Individual Profile]&quot;. Il formale `$id` della classe non è cambiata. |

**Problemi noti**

* Nessuna.

Per ulteriori informazioni sull’utilizzo di XDM con [!DNL Schema Registry] API e [!DNL Schema Editor] interfaccia utente, leggere [Documentazione del sistema XDM](../../xdm/home.md).

## [!DNL Real-Time Customer Profile] {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con [!DNL Real-Time Customer Profile], puoi visualizzare una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account actionable e timestamp di ogni interazione con il cliente.

| Funzione | Descrizione |
| -----------| ---------- |
| Miglioramenti apportati a [!DNL Profile] ricerca | Gli utenti ora possono cercare profili utilizzando descrittori di riferimento ed entità correlate. |
| Pulizia dei dati per un dato set di dati | Gli utenti possono ora eliminare i dati per un dato set di dati o un batch utilizzando [!DNL Profile] API dei processi di sistema. |
| Bordo [!DNL Profile] miglioramenti delle query | Le applicazioni possono ora eseguire query su Edge [!DNL Profile] da una delle identità di un determinato profilo. |
| Configura criteri di unione per proiezione | Le applicazioni possono ora configurare i criteri di unione per proiezione per generare una visualizzazione dei dati in base a un criterio di unione specifico. |
| Attributi calcolati | Gli attributi calcolati calcolano automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo per aggregare valori quali &quot;acquisto totale&quot;, &quot;valore del ciclo di vita&quot; o &quot;stato del funnel&quot; in base a un evento in arrivo, a un evento in arrivo e ai dati di profilo o a un evento in arrivo, ai dati di profilo e agli eventi storici. |

**Correzioni di bug**

* Elenco semplificato delle strategie di unione degli ID disponibili nel flusso di lavoro per la creazione dei criteri di unione .

**Problemi noti**

* Nessuna.

Per ulteriori informazioni su [!DNL Real-Time Customer Profile], incluse esercitazioni e best practice per l’utilizzo di [!DNL Profile] dati, leggere [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] fornisce un’interfaccia utente e l’API RESTful che ti consentono di creare segmenti e generare tipi di pubblico dal tuo [!DNL Real-Time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale su [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione di Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

| Funzione | Descrizione |
| -----------| ---------- |
| Segmentazione pianificata | Gli utenti possono ora abilitare la valutazione pianificata dei segmenti per tutti i segmenti tramite l’interfaccia utente e l’API. Una volta abilitato, tutti i segmenti vengono valutati una volta al giorno. Questo non influisce sulle funzionalità di segmentazione on-demand che continuano a funzionare come in precedenza.<br/><br/>Nota: La funzione di segmentazione pianificata non può essere utilizzata nelle sandbox con più di cinque criteri di unione per [!DNL XDM Individual Profile]. |
| Segmentazione streaming | Il supporto per la valutazione continua dei segmenti (segmentazione in streaming) consente di valutare la maggior parte delle regole dei segmenti mentre i dati vengono trasmessi in [!DNL Platform]. Questa funzione consente di aggiornare l’appartenenza al segmento senza dover eseguire processi di segmentazione pianificati. Sono applicabili alcune eccezioni, ad esempio i segmenti che utilizzano relazioni con più entità o con payload arricchiti. |
| Segmenti come blocchi predefiniti | Quando crei segmenti utilizzando l’interfaccia utente del Generatore di segmenti, gli utenti possono ora utilizzare segmenti definiti in precedenza come blocchi predefiniti per altri segmenti. <ul><li>Riferimento all&#39;iscrizione al pubblico corrente: viene aggiornato man mano che le persone entrano ed escono dal pubblico.</li><li>Logica copia: prendi la definizione del segmento selezionato e duplicala nel nuovo segmento.</li></ul> |
| Visualizzare l’appartenenza al segmento in base allo spazio dei nomi ID | L’appartenenza al segmento può ora essere visualizzata tramite lo spazio dei nomi ID (e-mail, ECID e conteggio totale). |
| Supporto RBAC | Il Generatore di segmenti ora fornisce il supporto per controlli e autorizzazioni di accesso basati sui ruoli di base. |
| Supporto migliorato per la condivisione di tipi di pubblico esterni tra [!DNL Platform] soluzioni di Adobe | Gli utenti possono ora importare contenuti esterni (non-[!DNL Experience Platform]) metadati del pubblico in scenari in cui il numero di tipi di pubblico è elevato o non è noto a priori. Questa versione include l&#39;accesso a [!DNL Audience Manager] metadati per i clienti che hanno eseguito il provisioning del connettore della soluzione. Questi metadati del pubblico possono essere utilizzati in Segment Builder per creare nuovi [!DNL Experience Platform] segmenti. <br/><br/> Inoltre, i segmenti creati in [!DNL Experience Platform] sarà ora disponibile per l&#39;utilizzo in soluzioni di Adobe integrate, tra cui [!DNL Audience Manager], [!DNL Target]e [!DNL Ad Cloud]. |

**Correzioni di bug**

* È stato risolto un problema a causa del quale la segmentazione di più entità restituiva zero profili in caso di relazioni nidificate.
* È stato risolto un problema a causa del quale la logica di esclusione restituiva risultati fuorvianti.
* È stata migliorata la leggibilità delle cartelle con più entità. Ora mostrano il nome descrittivo della classe XDM.
* È stato risolto un problema intermittente a causa del quale venivano visualizzate più copie della stessa cartella XDM.
* La messaggistica viene ora prodotta per informare un utente se le stime dei segmenti non sono disponibili per il criterio di unione selezionato.

**Problemi noti**

* Nessuna.

Per ulteriori informazioni [!DNL Segmentation Service], leggi la [Panoramica del servizio di segmentazione](../../segmentation/home.md).
