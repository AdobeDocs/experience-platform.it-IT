---
title: 'Note sulla versione di Adobe Experience Platform '
description: Note sulla versione del Experience Platform  18 novembre 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 2%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 18 novembre 2019**

Nuove funzioni in  Adobe Experience Platform:
* [!DNL Real-time Customer Data Platform](#rtcdp)
* [!DNL Destinations](#destinations)
* [!DNL Sources](#sources)

Aggiornamenti alle funzioni esistenti:
* [!DNL Data Science Workspace](#dsw)
* [!DNL Experience Data Model (XDM) System](#xdm)
* [!DNL Real-time Customer Profile](#profile)
* [!DNL Segmentation Service](#segmentation)

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Basato  Adobe Experience Platform, il  Adobe Real-time Customer Data Platform (Real-time CDP) aiuta le aziende a mettere insieme dati noti e sconosciuti per attivare i profili dei clienti con decisioni intelligenti per tutto il percorso del cliente. CDP in tempo reale combina più origini dati aziendali per creare profili unificati in tempo reale che possono essere utilizzati per fornire esperienze cliente personalizzate uno-a-uno su tutti i canali e dispositivi.

[!DNL Real-time Customer Data Platform] include strumenti per la governance dei dati, la gestione delle identità, la segmentazione avanzata e la scienza dei dati, che consentono di creare profili e definire i tipi di pubblico, oltre a ricavare informazioni approfondite e al tempo stesso essere in grado di applicare politiche rigorose di governance dei dati.

 Adobe si collega a un ampio ecosistema di partner, per non parlare delle integrazioni native con Adobe Experience Cloud, in modo da poter attivare facilmente questi tipi di pubblico e fornire esperienze cliente straordinarie su tutti i canali, dalla personalizzazione in-sito o in-app alla posta elettronica, ai supporti a pagamento, ai call center, ai dispositivi connessi e molto altro ancora.

Con CDP in tempo reale, potete:

* Raggiungete un&#39;unica vista del cliente con la raccolta in streaming dei dati dei clienti da tutta l&#39;azienda.
* Gestire in modo responsabile i profili con governance affidabile e controlli sulla privacy per identificatori noti e sconosciuti.
* Generazione di informazioni fruibili e scalabilità del pubblico con AI e machine learning basati su  Adobe Sensei e progettati per gli esperti di marketing.
* Distribuisci esperienze personalizzate in tempo reale su tutti i canali e le destinazioni.

Per ulteriori informazioni, consulta la [documentazione](../../rtcdp/overview.md)Platform sui dati dei clienti in tempo reale.

**Funzionalità chiave**

| Funzione | Descrizione |
|---|---|
| Destinazioni | Integrazioni pre-costruite con piattaforme di destinazione supportate da  Adobe [!DNL Real-time Customer Data Platform] che attivano i dati per tali partner in modo semplice. See [Destinations](#destinations) below for more information. |
| Pannello metriche pagina iniziale | La pagina principale Platform (Real-time Customer Data, CDP) del Adobe  include un dashboard di metriche che mostra informazioni su profili e segmenti. La pagina principale contiene anche collegamenti ai materiali didattici. Consulta la sezione relativa alle metriche [Platform dei dati sui clienti in tempo](#real-time-customer-data-platform-metrics) reale riportata di seguito. |
| Origini | È possibile acquisire dati da origini diverse, come  soluzioni di Adobe, storage basato su cloud, software di terze parti e CRM. Per ulteriori informazioni, consulta la sezione [Origini](#sources) di seguito. |

**[!DNL Real-time Customer Data Platform]metriche **

La pagina principale Platform (Real-time CDP, Real-time CDP) del Adobe , che include un dashboard delle metriche, viene visualizzata quando si accede a CDP in tempo reale.

La pagina principale è solo uno dei punti in cui vengono visualizzate le schede metriche. Il CDP in tempo reale fornisce schede metriche per tutta l&#39;esperienza. Queste metriche ti informano sui dati, il profilo e il pubblico del segmento nel sistema.

Se non sono presenti dati nel sistema al momento dell&#39;accesso a CDP in tempo reale, il dashboard nella pagina principale non viene visualizzato. In questo caso, la pagina principale fornisce materiale didattico per la prima esperienza utente. Durante la raccolta dei dati, il dashboard si aggiorna automaticamente per visualizzare le informazioni su tali dati.

Per saperne di più, consulta la panoramica delle metriche Platform dei dati del cliente in tempo [reale](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni pre-costruite con piattaforme di destinazione supportate dall&#39;Platform di dati cliente in tempo reale del  Adobe che attivano i dati per tali partner in modo semplice. Per ulteriori informazioni, consulta l’articolo Panoramica [](../../rtcdp/destinations/destinations-overview.md) Destinazioni.

**Destinazioni disponibili**

Con la release di novembre,  Adobe  Real-time Customer Data Platform supporta le seguenti destinazioni:

* Pubblicità: [!DNL Google]
* Marketing e-mail:  Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua
   ]
Consultate il catalogo [di](../../rtcdp/destinations/destinations-catalog.md) destinazione per informazioni su ciascuna delle destinazioni.

**Limitazioni note**

* Il controllo per consentire le pianificazioni di attivazione personalizzate nel flusso [di](../../rtcdp/destinations/activate-destinations.md#activate-data) attivazione (passaggio Pianificazione) non è disponibile con il rilascio iniziale.
* Al momento non è possibile modificare o eliminare una configurazione di destinazione. Per ovviare a questo limite, è possibile abilitare o disabilitare la destinazione nell&#39;angolo superiore destro della pagina [dei dettagli di](../../rtcdp/destinations/destination-details-page.md)destinazione.
* Al momento non è disponibile alcuna convalida per i dettagli dell&#39;account, il percorso o le credenziali durante la connessione all&#39;account di destinazione o di archiviazione. Assicurarsi di immettere le credenziali corrette e di controllare due volte la presenza di errori di ortografia o errori di battitura.
* Nessun rinnovo delle credenziali è disponibile con il rilascio iniziale. Una volta scaduto o che è necessario aggiornare un account, dovete creare una nuova connessione di destinazione e mappare nuovamente i segmenti mappati in precedenza.

## Origini {#sources}

 Adobe Experience Platform può acquisire dati da origini esterne consentendo al contempo di strutturare, etichettare e migliorare i dati utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come  soluzioni di Adobe, storage basato su cloud, software di terze parti e il sistema CRM.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di effettuare l&#39;autenticazione ai sistemi di storage e ai servizi CRM, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ---------- | ------------ |
| Interfaccia utente Origini | Nuova interfaccia utente per la creazione, la visualizzazione e la gestione delle connessioni sorgente. |
| Flussi di lavoro aggiornati per i connettori CRM | Nuovo flusso di lavoro intuitivo dell’interfaccia utente per la creazione e la gestione [!DNL Microsoft Dynamics] e [!DNL Salesforce] dei connettori. |
| Supporto del connettore per gli storage basati su cloud | I connettori possono ora accedere agli store basati su cloud. Le nuove sorgenti includono server [!DNL Amazon S3], [!DNL Azure Blob]e server FTP/SFTP. |

**Problemi noti**

* I connettori di origine per gli archivi basati su cloud non supportano l&#39;inserimento di file compressi.

Per ulteriori informazioni sulle origini, consulta [Panoramica](../../sources/home.md)delle origini.

## [!DNL Data Science Workspace] {#dsw}

 Adobe Experience Platform [!DNL Data Science Workspace] consente agli esperti di dati di generare facilmente informazioni da dati e contenuti attraverso applicazioni  Adobe e sistemi di terze parti, creando e operando modelli di apprendimento automatico. [!DNL Data Science Workspace] è strettamente integrato con [!DNL Platform] e potenzia il ciclo di vita end-to-end della scienza dei dati, compresa l&#39;esplorazione e la preparazione di dati XDM, seguito dallo sviluppo e dall&#39;operazionalizzazione di Modelli per arricchire automaticamente [!DNL Real-time Customer Profile] con approfondimenti di apprendimento automatico.

**Nuove funzionalità**

| Funzione | Descrizione |
| -----------| ---------- |
| Accesso ai dati tramite [!DNL Platform] SDK | I notebook Recipes e launcher predefiniti in [!DNL Python] ora utilizzano [!DNL Platform] SDK per l&#39;accesso ai dati. |
| Supporto per sandbox | Supporto per la funzionalità sandbox in arrivo (attualmente in versione beta), inclusa la possibilità di isolare blocchi appunti e ricette in sandbox di sviluppo o produzione. Per ulteriori informazioni, consultate la panoramica [delle](../../sandboxes/home.md) sandbox. |

Per ulteriori informazioni, consulta la panoramica [di](../../data-science-workspace/home.md)Data Science Workspace.

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da  Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione che comunica con i servizi  Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati relativi all&#39;esperienza dei clienti possono essere incorporati in una rappresentazione comune, fornendo informazioni approfondite in modo più rapido e integrato. Puoi ricavare informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzionalità**

| Funzione | Descrizione |
| ---------- | ------------ |
| Schema di notifica | Nuovo schema che rappresenta i dati di notifica inviati durante il processo di assimilazione dei dati. |
|  schemi DSP AdCloud di Adobe | Sono stati aggiunti cinque nuovi schemi per rappresentare i metadati della piattaforma Adobe Advertising Cloud lato domanda (DSP): Posizione, Campagna, Pacchetto, Inserzionista, Account. |
| Mixin Dettagli implementazione di ExperienceEvent | Nuovo mixin ExperienceEvent che aggiunge un campo standard per memorizzare informazioni sul software utilizzato per raccogliere l&#39;evento. |
| [!DNL Profile Privacy] mixin | Nuovo mixin di profilo che aggiunge campi per accettare i segnali generali di out-out e di rinuncia alle vendite/condivisione per [!DNL Real-time Customer Profile]. |
| Vincoli di formattazione per `xdm:alternateDisplayInfo` | I campi &quot;Titolo&quot; e &quot;Descrizione&quot; per `xdm:alternateDisplayInfo` devono essere entrambi stringhe per superare la convalida. |
| Modifica del nome: XDM [!DNL Individual Profile] | Il &quot;titolo&quot; della classe &quot;XDM [!DNL Profile]&quot; è stato aggiornato a &quot;XDM [!DNL Individual Profile]&quot;. Il formale `$id` della classe non è cambiato. |

**Problemi noti**

* Nessuna.

Per ulteriori informazioni sull&#39;utilizzo di XDM tramite l&#39; [!DNL Schema Registry] API e l&#39;interfaccia [!DNL Schema Editor] utente, consulta la documentazione [di sistema](../../xdm/home.md)XDM.

## [!DNL Real-time Customer Profile] {#profile}

 Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti per i clienti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con [!DNL Real-time Customer Profile], puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi online, offline, CRM e dati di terze parti. [!DNL Profile] consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| -----------| ---------- |
| Miglioramenti alla [!DNL Profile] ricerca | Gli utenti ora possono cercare i profili utilizzando descrittori di riferimento ed entità correlate. |
| Pulizia dei dati per un dato dataset | Gli utenti ora possono eliminare i dati per un dato set di dati o un batch utilizzando l&#39;API [!DNL Profile] Processi di sistema. |
| Miglioramenti alle [!DNL Profile] query Edge | Le applicazioni ora possono eseguire una query su Edge [!DNL Profile] in base alle identità di un determinato profilo. |
| Configurare i criteri di unione per la proiezione | Le applicazioni ora possono configurare criteri di unione per proiezione per generare una visualizzazione dei dati come regolata da uno specifico criterio di unione. |
| Attributi calcolati | Gli attributi calcolati calcolano automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo per aggregare valori quali &quot;acquisto totale&quot;, &quot;valore del ciclo di vita&quot; o &quot;stato del funnel&quot; in base a un evento in arrivo, a un evento in arrivo e ai dati del profilo oppure a un evento in arrivo, ai dati del profilo e agli eventi storici. |

**Correzioni di bug**

* Elenco semplificato delle strategie di gestione degli ID disponibili nel flusso di lavoro di creazione dei criteri di unione.

**Problemi noti**

* Nessuna.

Per ulteriori informazioni [!DNL Real-time Customer Profile], comprese esercitazioni e best practice per l&#39;utilizzo dei [!DNL Profile] dati, consulta la Panoramica [sul profilo cliente in tempo](../../profile/home.md)reale.

## [!DNL Segmentation Service] {#segmentation}

 Adobe Experience Platform [!DNL Segmentation Service] fornisce un&#39;interfaccia utente e RESTful API che consente di creare segmenti e generare audience dai [!DNL Real-time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione  Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all&#39;interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

| Funzione | Descrizione |
| -----------| ---------- |
| Segmentazione pianificata | Gli utenti ora possono abilitare la valutazione pianificata dei segmenti per tutti i segmenti tramite l&#39;interfaccia utente e l&#39;API. Una volta attivato, tutti i segmenti saranno valutati una volta al giorno. Ciò non influisce sulle funzionalità di segmentazione su richiesta che continuano a funzionare come in precedenza.<br/><br/>Nota: La funzione di segmentazione pianificata non può essere utilizzata nelle sandbox con più di cinque criteri di unione per [!DNL XDM Individual Profile]. |
| Segmentazione in streaming | Il supporto per la valutazione continua dei segmenti (segmentazione in streaming) consente di valutare la maggior parte delle regole dei segmenti man mano che i dati vengono trasferiti [!DNL Platform]. Questa funzione consente di aggiornare l&#39;appartenenza al segmento senza dover eseguire processi di segmentazione pianificati. Sono applicabili alcune eccezioni, ad esempio i segmenti che utilizzano relazioni con più entità o con payload arricchiti. |
| Segmenti come blocchi di generazione | Quando si creano segmenti utilizzando l’interfaccia utente di Generatore di segmenti, gli utenti ora possono utilizzare i segmenti definiti in precedenza come elementi costitutivi per altri segmenti. <ul><li>Riferimento a appartenenza corrente all&#39;audience: si aggiorna man mano che le persone entrano ed escono dal pubblico.</li><li>Logica di copia: prendi la definizione del segmento selezionata e duplicala nel nuovo segmento.</li></ul> |
| Visualizzare l’appartenenza al segmento in base allo spazio dei nomi ID | L&#39;appartenenza al segmento può ora essere visualizzata per namespace ID (e-mail, ECID e conteggio totale). |
| Supporto RBAC | Segment Builder (Generatore di segmenti) ora fornisce il supporto per controlli e autorizzazioni di accesso basati sui ruoli di base. |
| Supporto migliorato per la condivisione di audience esterna tra soluzioni [!DNL Platform] e  Adobe | Gli utenti ora possono inserire metadati di pubblico esterni (non[!DNL Experience Platform]) in scenari in cui il numero di audience è grande o non è noto a priori. Questa release include l&#39;accesso ai [!DNL Audience Manager] metadati per i clienti che hanno eseguito il provisioning del connettore della soluzione. I metadati del pubblico possono essere utilizzati in Segment Builder (Generatore di segmenti) per creare nuovi [!DNL Experience Platform] segmenti. <br/><br/> Inoltre, i segmenti creati in [!DNL Experience Platform] saranno ora disponibili per l&#39;utilizzo in soluzioni di Adobe  integrate, tra cui [!DNL Audience Manager], [!DNL Target]e [!DNL Ad Cloud]. |

**Correzioni di bug**

* È stato risolto un problema a causa del quale la segmentazione multi-entità restituiva zero profili in caso di relazioni nidificate.
* È stato risolto un problema a causa del quale la logica di esclusione restituiva risultati fuorvianti.
* È stata migliorata la leggibilità delle cartelle con più entità. Ora vengono visualizzati i nomi descrittivi della classe XDM.
* È stato risolto un problema intermittente per il quale venivano visualizzate più copie della stessa cartella XDM.
* Ora vengono generati messaggi per informare l&#39;utente se le stime dei segmenti non sono disponibili per il criterio di unione selezionato.

**Problemi noti**

* Nessuna.

Per ulteriori informazioni [!DNL Segmentation Service], consulta la panoramica [del servizio](../../segmentation/home.md)di segmentazione.