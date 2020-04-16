---
title: 'Note sulla versione di Adobe Experience Platform '
description: Note sulla versione della piattaforma Experience - 18 novembre 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac

---


# Note sulla versione di Adobe Experience Platform

## Data di rilascio: 18 novembre 2019

Nuove versioni:
* [Piattaforma dati cliente in tempo reale](#real-time-customer-data-platform)
* [Destinazioni](#destinations)
* [Origini](#sources)

Aggiornamenti alle funzioni esistenti:
* [Area di lavoro Data Science](#data-science-workspace)
* [Sistema XDM (Experience Data Model)](#experience-data-model-xdm-system)
* [Profilo cliente in tempo reale](#real-time-customer-profile)
* [Servizio di segmentazione](#segmentation-service)

## Piattaforma dati cliente in tempo reale

Basato su Adobe Experience Platform, la Adobe Real-time Customer Data Platform (CDP in tempo reale) consente alle aziende di mettere insieme dati noti e sconosciuti per attivare i profili dei clienti con decisioni intelligenti per tutto il percorso del cliente. CDP in tempo reale combina più origini dati aziendali per creare profili unificati in tempo reale che possono essere utilizzati per fornire esperienze cliente personalizzate uno-a-uno su tutti i canali e dispositivi.

La Piattaforma dati cliente in tempo reale include strumenti per la governance dei dati, la gestione delle identità, la segmentazione avanzata e la scienza dei dati, per creare profili e definire i tipi di pubblico, oltre a ricavare informazioni approfondite e al tempo stesso essere in grado di applicare rigorose politiche di governance dei dati.

Adobe si collega a un ampio ecosistema di partner, per non parlare delle integrazioni native con Adobe Experience Cloud, per consentirti di attivare facilmente tali tipi di pubblico e offrire esperienze cliente straordinarie su tutti i canali, dalla personalizzazione in-sito o in-app alle e-mail, ai supporti a pagamento, ai call center, ai dispositivi connessi e molto altro ancora.

Con CDP in tempo reale, potete:

* Raggiungete un&#39;unica vista del cliente con la raccolta in streaming dei dati dei clienti da tutta l&#39;azienda.
* Gestire in modo responsabile i profili con governance affidabile e controlli sulla privacy per identificatori noti e sconosciuti.
* Puoi generare informazioni fruibili e scalare i tipi di pubblico con AI e machine learning basati su Adobe Sensei, progettati per i professionisti del marketing.
* Distribuisci esperienze personalizzate in tempo reale su tutti i canali e le destinazioni.

Per ulteriori informazioni, consulta la documentazione relativa alla piattaforma dati [Adobe in tempo reale](../../rtcdp/overview.md).

### Funzioni chiave

| Funzione | Descrizione |
|---|---|
| Destinazioni | Integrazioni pre-costruite con piattaforme di destinazione supportate dalla piattaforma dati cliente in tempo reale di Adobe che attivano i dati per tali partner in modo semplice. See [Destinations](#destinations) below for more information. |
| Pannello metriche pagina iniziale | La home page di Adobe Real-time Customer Data Platform (CDP in tempo reale) include un dashboard di metriche che mostra informazioni su profili e segmenti. La pagina principale contiene anche collegamenti ai materiali didattici. Vedi la sezione relativa alle metriche [della piattaforma dati cliente in tempo](#real-time-customer-data-platform-metrics) reale riportata di seguito. |
| Origini | È possibile acquisire dati da origini diverse, come soluzioni Adobe, archiviazione basata su cloud, software di terze parti e CRM. Per ulteriori informazioni, consulta la sezione [Origini](#sources) di seguito. |

### Metriche della piattaforma dati cliente in tempo reale

La pagina principale Adobe Real-time Customer Data Platform (CDP in tempo reale), che include un dashboard delle metriche, viene visualizzata quando accedete a CDP in tempo reale.

La pagina principale è solo uno dei punti in cui vengono visualizzate le schede metriche. Il CDP in tempo reale fornisce schede metriche per tutta l&#39;esperienza. Queste metriche ti informano sui dati, il profilo e il pubblico del segmento nel sistema.

Se non sono presenti dati nel sistema al momento dell&#39;accesso a CDP in tempo reale, il dashboard nella pagina principale non viene visualizzato. In questo caso, la pagina principale fornisce materiale didattico per la prima esperienza utente. Durante la raccolta dei dati, il dashboard si aggiorna automaticamente per visualizzare le informazioni su tali dati.

Per ulteriori informazioni, consulta la panoramica delle metriche della piattaforma dati cliente in tempo [reale](../../rtcdp/home-page-dashboards.md)

## Destinazioni

Le destinazioni sono integrazioni preconfigurate con piattaforme di destinazione supportate dalla piattaforma dati cliente in tempo reale di Adobe che attivano i dati per tali partner in modo semplice. Per ulteriori informazioni, consulta l’articolo Panoramica [](../../rtcdp/destinations/destinations-overview.md) Destinazioni.

### Destinazioni disponibili

Con la release di novembre, la piattaforma dati cliente Adobe in tempo reale supporta le seguenti destinazioni:

* Pubblicità: Google
* Marketing e-mail: Adobe Campaign, Salesforce Marketing Cloud, Oracle Responsys, Oracle Eloqua

Consultate il catalogo [di](../../rtcdp/destinations/destinations-catalog.md) destinazione per informazioni su ciascuna delle destinazioni.

### Limitazioni note

* Il controllo per consentire le pianificazioni di attivazione personalizzate nel flusso [di](../../rtcdp/destinations/activate-destinations.md#activate-data) attivazione (passaggio Pianificazione) non è disponibile con il rilascio iniziale.
* Al momento non è possibile modificare o eliminare una configurazione di destinazione. Per ovviare a questo limite, è possibile abilitare o disabilitare la destinazione nell&#39;angolo superiore destro della pagina [dei dettagli di](../../rtcdp/destinations/destination-details-page.md)destinazione.
* Al momento non è disponibile alcuna convalida per i dettagli dell&#39;account, il percorso o le credenziali durante la connessione all&#39;account di destinazione o di archiviazione. Assicurarsi di immettere le credenziali corrette e di controllare due volte la presenza di errori di ortografia o errori di battitura.
* Nessun rinnovo delle credenziali è disponibile con il rilascio iniziale. Una volta scaduto o che è necessario aggiornare un account, dovete creare una nuova connessione di destinazione e mappare nuovamente i segmenti mappati in precedenza.

## Origini

Adobe Experience Platform è in grado di acquisire dati da origini esterne e allo stesso tempo di strutturarli, etichettarli e ottimizzarli tramite i servizi della piattaforma. È possibile acquisire dati da origini diverse, come soluzioni Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di effettuare l&#39;autenticazione ai sistemi di storage e ai servizi CRM, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

### Funzioni chiave

| Funzione | Descrizione |
| ---------- | ------------ |
| Interfaccia utente Origini | Nuova interfaccia utente per la creazione, la visualizzazione e la gestione delle connessioni sorgente. |
| Flussi di lavoro aggiornati per i connettori CRM | Nuovo flusso di lavoro intuitivo dell&#39;interfaccia utente per la creazione e la gestione dei connettori Microsoft Dynamics e Salesforce. |
| Supporto del connettore per gli storage basati su cloud | I connettori possono ora accedere agli store basati su cloud. Le nuove origini includono i server Amazon S3, Azure Blob e FTP/SFTP. |

### Problemi noti

* I connettori di origine per gli archivi basati su cloud non supportano l&#39;inserimento di file compressi.

Per ulteriori informazioni sulle origini, consulta [Panoramica](../../sources/home.md)delle origini.

## Area di lavoro Data Science

Adobe Experience Platform Data Science Workspace consente agli esperti di dati di generare facilmente informazioni dai dati e dai contenuti tra le applicazioni Adobe e i sistemi di terze parti, creando e operando modelli di apprendimento automatico. Data Science Workspace è strettamente integrato con la Piattaforma e migliora il ciclo di vita completo della scienza dei dati, compresa l&#39;esplorazione e la preparazione di dati XDM, seguita dallo sviluppo e dall&#39;operazionalizzazione di modelli per arricchire automaticamente il profilo cliente in tempo reale con informazioni sull&#39;apprendimento automatico.

### Nuove funzionalità

| Funzione | Descrizione |
| -----------| ---------- |
| Accesso ai dati tramite SDK piattaforma | I notebook Recipes e launcher pregenerati in Python ora utilizzano Platform SDK per l&#39;accesso ai dati. |
| Supporto per sandbox | Supporto per la funzionalità sandbox in arrivo (attualmente in versione beta), inclusa la possibilità di isolare blocchi appunti e ricette in sandbox di sviluppo o produzione. Per ulteriori informazioni, consultate la panoramica [delle](../../sandboxes/home.md) sandbox. |

Per ulteriori informazioni, consulta la panoramica [di](../../data-science-workspace/home.md)Data Science Workspace.

## Sistema XDM (Experience Data Model)

Standardizzazione e interoperabilità sono concetti chiave della piattaforma Experience. Experience Data Model (XDM), guidato da Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione che desideri comunicare con i servizi in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati relativi all&#39;esperienza dei clienti possono essere incorporati in una rappresentazione comune, fornendo informazioni approfondite in modo più rapido e integrato. Puoi ricavare informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

### Nuove funzionalità

| Funzione | Descrizione |
| ---------- | ------------ |
| Schema di notifica | Nuovo schema che rappresenta i dati di notifica inviati durante il processo di assimilazione dei dati. |
| Schemi DSP di Adobe AdCloud | Sono stati aggiunti cinque nuovi schemi per rappresentare i metadati della piattaforma DSP (Demand-side Platform) di Adobe Advertising Cloud: Posizione, Campagna, Pacchetto, Inserzionista, Account. |
| Mixin Dettagli implementazione di ExperienceEvent | Nuovo mixin ExperienceEvent che aggiunge un campo standard per memorizzare informazioni sul software utilizzato per raccogliere l&#39;evento. |
| Mixaggio sulla privacy del profilo | Nuovo mixin di profilo che aggiunge campi per accettare i segnali generali di out-out e di rinuncia alle vendite/condivisione per il profilo cliente in tempo reale. |
| Vincoli di formattazione per `xdm:alternateDisplayInfo` | I campi &quot;Titolo&quot; e &quot;Descrizione&quot; per `xdm:alternateDisplayInfo` devono essere entrambi stringhe per superare la convalida. |
| Modifica del nome: Profilo singolo XDM | Il &quot;titolo&quot; della classe &quot;Profilo XDM&quot; è stato aggiornato a &quot;Profilo singolo XDM&quot;. Il formale `$id` della classe non è cambiato. |

### Problemi noti

* None.

Per ulteriori informazioni sull&#39;utilizzo di XDM tramite l&#39;interfaccia utente API del Registro di sistema e Editor schema, consultare la documentazione [di sistema](../../xdm/home.md)XDM.

## Profilo cliente in tempo reale

Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti per i clienti, ovunque e quando interagiscono con il tuo marchio. Con il profilo cliente in tempo reale, puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| -----------| ---------- |
| Miglioramenti alla ricerca dei profili | Gli utenti ora possono cercare i profili utilizzando descrittori di riferimento ed entità correlate. |
| Pulizia dei dati per un dato dataset | Gli utenti ora possono eliminare i dati per un dato set di dati o un batch utilizzando l&#39;API Processi di sistema profilo. |
| Miglioramenti alla query profilo Edge | Le applicazioni ora possono eseguire una query su Edge Profile in base alle identità di un determinato profilo. |
| Configurare i criteri di unione per la proiezione | Le applicazioni ora possono configurare criteri di unione per proiezione per generare una visualizzazione dei dati come regolata da uno specifico criterio di unione. |
| Attributi calcolati | Gli attributi calcolati calcolano automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo per aggregare valori quali &quot;acquisto totale&quot;, &quot;valore del ciclo di vita&quot; o &quot;stato del funnel&quot; in base a un evento in arrivo, a un evento in arrivo e ai dati del profilo oppure a un evento in arrivo, ai dati del profilo e agli eventi storici. |

### Correzioni di bug

* Elenco semplificato delle strategie di gestione degli ID disponibili nel flusso di lavoro di creazione dei criteri di unione.

### Problemi noti

* None.

Per ulteriori informazioni sul profilo cliente in tempo reale, comprese esercitazioni e best practice per lavorare con i dati del profilo, consulta la panoramica [sul profilo cliente in tempo](../../profile/home.md)reale.

## Servizio di segmentazione

Il servizio di segmentazione di Adobe Experience Platform fornisce un&#39;interfaccia utente e RESTful API che consente di creare segmenti e generare audience dai dati del profilo cliente in tempo reale. Questi segmenti sono configurati e mantenuti a livello centrale sulla piattaforma, rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

Il servizio di segmentazione definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all&#39;interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

| Funzione | Descrizione |
| -----------| ---------- |
| Segmentazione pianificata | Gli utenti ora possono abilitare la valutazione pianificata dei segmenti per tutti i segmenti tramite l&#39;interfaccia utente e l&#39;API. Una volta attivato, tutti i segmenti saranno valutati una volta al giorno. Ciò non influisce sulle funzionalità di segmentazione su richiesta che continuano a funzionare come in precedenza.<br/><br/>Nota: La funzione di segmentazione pianificata non può essere utilizzata nelle sandbox con più di cinque criteri di unione per il profilo individuale XDM. |
| Segmentazione in streaming | Il supporto per la valutazione continua dei segmenti (segmentazione in streaming) consente di valutare la maggior parte delle regole dei segmenti man mano che i dati passano in Piattaforma. Questa funzione consente di aggiornare l&#39;appartenenza al segmento senza dover eseguire processi di segmentazione pianificati. Sono applicabili alcune eccezioni, ad esempio i segmenti che utilizzano relazioni con più entità o con payload arricchiti. |
| Segmenti come blocchi di generazione | Quando si creano segmenti utilizzando l’interfaccia utente di Generatore di segmenti, gli utenti ora possono utilizzare i segmenti definiti in precedenza come elementi costitutivi per altri segmenti. <ul><li>Riferimento a appartenenza corrente all&#39;audience: si aggiorna man mano che le persone entrano ed escono dal pubblico.</li><li>Logica di copia: prendi la definizione del segmento selezionata e duplicala nel nuovo segmento.</li></ul> |
| Visualizzare l’appartenenza al segmento in base allo spazio dei nomi ID | L&#39;appartenenza al segmento può ora essere visualizzata per namespace ID (e-mail, ECID e conteggio totale). |
| Supporto RBAC | Segment Builder (Generatore di segmenti) ora fornisce il supporto per controlli e autorizzazioni di accesso basati sui ruoli di base. |
| Supporto migliorato per la condivisione di audience esterna tra le soluzioni Platform e Adobe | Gli utenti ora possono importare metadati di pubblico esterni (non-Experience Platform) in scenari in cui il numero di audience è grande o non è noto a priori. Questa release include l&#39;accesso ai metadati di Audience Manager per i clienti che hanno eseguito il provisioning del connettore della soluzione. I metadati del pubblico possono essere utilizzati in Segment Builder (Generatore di segmenti) per creare nuovi segmenti della Experience Platform. <br/><br/> Inoltre, i segmenti creati in Experience Platform saranno ora disponibili per l&#39;utilizzo in soluzioni Adobe integrate, tra cui Audience Manager, Target e Ad Cloud. |

### Correzioni di bug

* È stato risolto un problema a causa del quale la segmentazione multi-entità restituiva zero profili in caso di relazioni nidificate.
* È stato risolto un problema a causa del quale la logica di esclusione restituiva risultati fuorvianti.
* È stata migliorata la leggibilità delle cartelle con più entità. Ora vengono visualizzati i nomi descrittivi della classe XDM.
* È stato risolto un problema intermittente per il quale venivano visualizzate più copie della stessa cartella XDM.
* Ora vengono generati messaggi per informare l&#39;utente se le stime dei segmenti non sono disponibili per il criterio di unione selezionato.

### Problemi noti

* None.

Per ulteriori informazioni sul servizio di segmentazione, consulta la panoramica [del servizio di](../../segmentation/home.md)segmentazione.