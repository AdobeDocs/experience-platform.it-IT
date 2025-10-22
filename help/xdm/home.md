---
keywords: Experience Platform;home;argomenti popolari;XDM;sistema XDM;profilo individuale XDM;XDM ExperienceEvent;XDM ExperienceEvent;experienceEvent;evento esperienza;gruppi di campi;gruppi di campi;gruppo di campi;gruppo di campi;Evento esperienza;XDM ExperienceEvent;experienceEvent;experienceevent;XDM ExperienceEvent;Experience data model;Experience Data model;Experience Data Model;modello dati;modello dati;modello dati;modello dati;modello dati;modello dati;registro schema;registro schemi;libreria schema;schema;dati record;serie temporali
solution: Experience Platform
title: Panoramica del sistema XDM
description: La standardizzazione e l'interoperabilità sono concetti chiave alla base di Adobe Experience Platform. Experience Data Model (XDM), gestito da Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi per la gestione della customer experience.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 57981d2e4306b2245ce0c1cdd9f696065c508a1d
workflow-type: tm+mt
source-wordcount: '2440'
ht-degree: 3%

---

# Panoramica del sistema XDM

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di Adobe Experience Platform. Experience Data Model (XDM), gestito da Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni che consentono a qualsiasi applicazione di comunicare con i servizi di Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che può fornire informazioni in modo più veloce e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti ed esprimere gli attributi dei clienti a scopo di personalizzazione.

XDM è il framework fondamentale che consente a Adobe Experience Cloud, con tecnologia Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, nel momento esatto giusto. La metodologia su cui è basato Experience Platform, il sistema XDM, rende operativi gli schemi Experience Data Model per l’utilizzo da parte dei servizi Experience Platform.

Scopri il ruolo del sistema XDM in Experience Platform.

## Schemi XDM {#xdm-schemas}

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e quindi ottenere valore dai dati.

Prima che i dati possano essere acquisiti in Experience Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che possono essere contenuti all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più gruppi di campi schema.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, vedere le [nozioni di base sulla composizione dello schema](schema/composition.md).

### Componenti XDM standard {#Standard-xdm-components}

XDM fornisce una solida raccolta di gruppi di campi e tipi di dati standard, pensati per acquisire concetti e casi d’uso comuni a diversi settori. Experience Platform consente di filtrare questi componenti in base al settore e di creare schemi in modo rapido e sicuro per soddisfare al meglio le specifiche esigenze aziendali.

Durante la costruzione di schemi nell’interfaccia utente di Experience Platform, i gruppi di campi elencati vengono visualizzati con una metrica di popolarità. Questa metrica è determinata dalla frequenza con cui gli altri utenti di Experience Platform utilizzano il gruppo di campi nei loro schemi. Più alto è il numero, più popolare sarà il gruppo di campi. Per impostazione predefinita, i risultati vengono visualizzati da quelli più popolari a quelli meno popolari, per tenerti informato sulle tendenze di modellazione dei dati nel tuo settore.

![Colonna di popolarità della finestra di dialogo [!UICONTROL Add field group].](./images/overview/popularity.png)

### [!DNL Schema Library] {#schema-library}

Experience Platform fornisce un&#39;interfaccia utente e un&#39;API RESTful da cui è possibile visualizzare e gestire tutte le risorse relative allo schema in Experience Platform **[!DNL Schema Library]**. [!DNL Schema Library] contiene i componenti XDM standard resi disponibili da Adobe, nonché le risorse dei partner e dei fornitori Experience Platform di cui utilizzi le applicazioni.

Puoi anche creare e gestire nuovi schemi e risorse univoci per la tua organizzazione utilizzando [!DNL Schema Registry API] o l&#39;area di lavoro [!UICONTROL Schemas] nell&#39;interfaccia utente di Experience Platform.

Per ulteriori informazioni su come gestire e interagire con gli schemi in Experience Platform, consulta la seguente documentazione:

* [Guida all’interfaccia utente XDM](./ui/overview.md)
* [Guida API del registro dello schema](./api/overview.md)

## Comportamenti dei dati nel sistema XDM {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="Comportamenti dei dati"
>abstract="I dati da utilizzare in Experience Platform sono raggruppati secondo tre tipi di comportamento: record, serie temporali e ad hoc. Gli schemi di record forniscono informazioni sugli attributi di un oggetto. Gli schemi di serie temporali acquisiscono uno snapshot del sistema al momento dell’esecuzione di un’azione. Gli schemi ad hoc acquisiscono campi di spazi dei nomi da utilizzare solo per un singolo set di dati. Per ulteriori informazioni sui comportamenti dei dati in Experience Platform, consulta la documentazione."

I dati destinati all’utilizzo in Experience Platform sono raggruppati in tre tipi di comportamento:

* **Record**: fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **Serie temporale**: fornisce un&#39;istantanea del sistema nel momento in cui un oggetto record ha eseguito un&#39;azione direttamente o indirettamente.
* **Ad-hoc**: acquisisce i campi con namespace da usare solo per un singolo set di dati. Gli schemi ad hoc vengono utilizzati in vari flussi di lavoro di acquisizione dati per Experience Platform, tra cui l’acquisizione di file CSV e la creazione di alcuni tipi di connessioni sorgente.

Tutti gli schemi XDM descrivono dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla classe dello schema, che viene assegnata a uno schema al momento della creazione. Le classi XDM descrivono il minor numero di proprietà che uno schema deve contenere per rappresentare un particolare comportamento di dati.

Sebbene sia possibile definire classi personalizzate all&#39;interno di [!DNL Schema Registry], si consiglia di utilizzare le classi standard **[!UICONTROL XDM Individual Profile]** e **[!UICONTROL XDM ExperienceEvent]** rispettivamente per i dati di record e di serie temporali. Tali classi sono descritte più dettagliatamente di seguito.

>[!NOTE]
>
>Non esistono classi standard basate sul comportamento ad hoc. Gli schemi ad hoc vengono generati automaticamente dai processi Experience Platform che li utilizzano, ma possono anche essere [creati manualmente utilizzando l&#39;API Schema Registry](./tutorials/ad-hoc.md).

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual Profile] è una classe basata su record che costituisce una singola rappresentazione degli attributi di soggetti identificati e parzialmente identificati. I profili altamente identificati possono essere utilizzati per comunicazioni personali o impegni mirati. I profili altamente identificati possono contenere informazioni personali dettagliate come nome, genere, data di nascita, posizione e informazioni di contatto, inclusi numeri di telefono e indirizzi e-mail.

I profili meno identificati possono essere costituiti solo da segnali comportamentali anonimi come i cookie del browser. In questo caso, i dati di profilo sparsi vengono utilizzati per creare una base di informazioni in cui gli interessi e le preferenze del profilo anonimo vengono raccolti e memorizzati. Questi identificatori possono diventare più dettagliati nel tempo, man mano che il soggetto si iscrive a notifiche, abbonamenti, acquisti e così via. Questo aumento degli attributi del profilo può infine causare un soggetto identificato e consentire un livello più elevato di coinvolgimento mirato.

Man mano che un profilo continua a crescere, diventa un solido archivio di informazioni personali, informazioni di identificazione, dettagli di contatto e preferenze di comunicazione di un individuo.

Per ulteriori informazioni sulla struttura e sul caso d&#39;uso dei campi forniti dalla classe, consulta la [[!UICONTROL XDM Individual Profile] guida di riferimento](./classes/individual-profile.md).

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent è una classe basata su serie temporali utilizzata per acquisire lo stato del sistema quando si è verificato un evento (o un set di eventi), compreso il momento e l’identità del soggetto interessato. Gli Eventi di esperienza sono registrazioni fattuali e immutabili di ciò che si è verificato in quel momento, che rappresentano ciò che è accaduto senza aggregazione o interpretazione. Sono fondamentali per l’analisi del dominio temporale in quanto possono essere utilizzati per analizzare i cambiamenti che si verificano in una determinata finestra temporale e per confrontare tra più finestre temporali al fine di tracciare le tendenze.

Gli eventi esperienza possono essere espliciti o impliciti. Gli eventi espliciti sono azioni umane direttamente osservabili che si verificano durante un punto di un percorso. Gli eventi impliciti sono eventi che vengono generati senza un&#39;azione umana diretta, ma che sono comunque correlati a un individuo. Esempi di eventi impliciti possono includere l’invio pianificato di newsletter via e-mail o il raggiungimento di una determinata soglia per la tensione della batteria.

Anche se non tutti gli eventi sono facilmente categorizzati in tutte le origini dati, è estremamente utile armonizzare eventi simili in tipi simili, ove possibile per l’elaborazione.

![Un&#39;infografica del Percorso di clienti visualizzata con eventi di esperienza nel tempo.](images/overview/experience-event-journey.png)

Per ulteriori informazioni sulla struttura e sul caso d&#39;uso dei campi forniti dalla classe, consulta la [[!UICONTROL XDM ExperienceEvent] guida di riferimento](./classes/experienceevent.md).

## Schemi XDM e servizi Experience Platform {#schemas-and-platform-services}

Experience Platform è indipendente dallo schema, il che significa che qualsiasi schema conforme allo standard XDM viene reso disponibile ai servizi di Experience Platform. Di seguito sono descritti più dettagliatamente i modi in cui i diversi servizi di Experience Platform utilizzano gli schemi.

### Catalog Service, acquisizione dati e data lake {#ingestion-catalog-and-storage}

Catalog Service è il sistema di registrazione per le risorse Experience Platform e i relativi schemi. Il catalogo non contiene i file di dati o le directory effettive, ma contiene i metadati e le descrizioni di tali file e directory.

I dati del catalogo vengono memorizzati nel data lake, un archivio di dati altamente granulare contenente tutti i dati gestiti da Experience Platform, indipendentemente dall’origine o dal formato del file.

Per iniziare a acquisire dati in Experience Platform, puoi utilizzare Catalog Service per creare un set di dati. Il set di dati fa riferimento a uno schema XDM che descrive la struttura dei dati da acquisire. Se un set di dati viene creato senza uno schema, Experience Platform deriva uno &quot;schema osservato&quot; esaminando il tipo e il contenuto dei campi di dati acquisiti. I set di dati vengono quindi tracciati in Catalog Service e memorizzati nel data lake insieme agli schemi e agli schemi osservati su cui si basano.

Per ulteriori informazioni, vedere [Panoramica di Catalog Service](../catalog/home.md). Per ulteriori informazioni sull&#39;acquisizione dati di Adobe Experience Platform, consulta la [panoramica sull&#39;acquisizione dati](../ingestion/home.md).

### Data Mirror e schemi relazionali {#relational-schemas}

>[!AVAILABILITY]
>
>Data Mirror e gli schemi relazionali sono disponibili per i titolari di licenze di **Campagne orchestrate** Adobe Journey Optimizer. Sono disponibili anche come **versione limitata** per gli utenti di Customer Journey Analytics, a seconda della licenza e dell&#39;abilitazione della funzione. Contatta il tuo rappresentante Adobe per accedere.

>[!NOTE]
>
>Nelle versioni precedenti della documentazione di Adobe Experience Platform, gli schemi relazionali erano precedentemente denominati schemi basati su modelli. La funzionalità rimane invariata, solo la terminologia è cambiata per maggiore chiarezza.

Data Mirror è una funzionalità di Adobe Experience Platform che consente la sincronizzazione avanzata del database utilizzando schemi relazionali. Per una panoramica completa delle funzionalità e dei casi d&#39;uso di Data Mirror, consulta la [panoramica di Data Mirror](./data-mirror/overview.md).

Data Mirror opera attraverso schemi relazionali, progettati per modelli di dati strutturati e in stile relazionale. Applicano le chiavi primarie, supportano gli identificatori di versione e definiscono relazioni schema-schema utilizzando le chiavi primarie ed esterne. A differenza degli schemi XDM standard, non richiedono classi o gruppi di campi e sono ottimizzati per i flussi di lavoro di acquisizione dei dati di modifica.

Per informazioni dettagliate su come definire relazioni schema-schema, consulta la [documentazione dell&#39;endpoint dei descrittori](./api/descriptors.md).

Utilizza Data Mirror quando devi:

* Sincronizzare le modifiche ai dati da sistemi esterni come Snowflake, Databrick o BigQuery
* Mantenere le relazioni tra i database e applicare l’integrità dei dati durante l’acquisizione
* Supporto di analisi avanzate e orchestrazione del percorso
* Abilitare il rilevamento preciso delle modifiche con operazioni di upsert ed eliminazione

Per creare uno schema relazionale, selezionare **[!UICONTROL Relational]** durante la creazione di uno schema. Gli schemi relazionali non utilizzano classi o gruppi di campi. È invece possibile definire manualmente la struttura o caricare un file DDL. Gli schemi relazionali richiedono una chiave primaria, un identificatore di versione e, se applicabile, campi di identificazione marca temporale. Puoi quindi configurare campi aggiuntivi e definire relazioni con altri schemi.

>[!NOTE]
>
>Le colonne di controllo utilizzate durante l&#39;acquisizione (ad esempio `_change_request_type` per i flussi di lavoro di acquisizione dati di modifica) vengono lette al momento dell&#39;acquisizione e non vengono memorizzate nello schema o mappate ai campi XDM. Gli schemi relazionali sono disponibili con i diritti e le funzioni abilitate appropriati di Experience Platform.

Per i passaggi dettagliati e le linee guida sul caso d’uso, consulta:

* [Panoramica di Data Mirror](./data-mirror/overview.md) - Funzionalità, casi d&#39;uso e pianificazione dell&#39;implementazione
* [Riferimento tecnico sullo schema relazionale](./schema/relational.md) - Specifiche tecniche e vincoli
* [Esercitazione sull’interfaccia utente](./ui/resources/schemas.md#create-relational-schema)
* [Esercitazione API](./api/schemas.md#create-relational-schema)
* [Documentazione del descrittore (identificatore)](./api/descriptors.md#relationship-descriptor)
* [Abilita la modifica di acquisizione dei dati](../sources/tutorials/api/change-data-capture.md)

### Servizio query {#query-service}

È possibile utilizzare SQL standard per eseguire query sui dati di Experience Platform per supportare molti casi d’uso diversi con Adobe Experience Platform Query Service.

Dopo aver composto uno schema e creato un set di dati che fa riferimento a tale schema, i dati vengono quindi acquisiti e memorizzati nel data lake. Puoi quindi utilizzare Query Service per unire qualsiasi set di dati nel data lake e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, nell’apprendimento automatico o nell’acquisizione in Real-Time Customer Profile.

Per ulteriori informazioni sul servizio, consulta la [Panoramica di Query Service](../query-service/home.md).

### Profilo cliente in tempo reale {#real-time-customer-profile}

Real-Time Customer Profile fornisce un profilo consumer centralizzato per una gestione mirata e personalizzata delle esperienze. Ogni profilo contiene dati aggregati in tutti i sistemi e include account con marca temporale utilizzabile di eventi che coinvolgono l’oggetto del profilo. Questi eventi possono essersi verificati in qualsiasi sistema utilizzato con Experience Platform.

Real-Time Customer Profile utilizza dati in formato schema basati sulle classi [!UICONTROL XDM Individual Profile] e [!UICONTROL XDM ExperienceEvent] e risponde alle query basate su tali dati.

Il sistema gestisce un’istanza di ciascun profilo cliente, unendo i dati in modo da formare un’unica fonte di verità per l’individuo. Questi dati unificati vengono rappresentati utilizzando quello che è noto come &quot;schema di unione&quot; (a volte indicato come &quot;visualizzazione unione&quot;). Uno schema di unione aggrega i campi di tutti gli schemi che implementano la stessa classe in un singolo schema. Durante la composizione di uno schema tramite l’interfaccia utente o l’API, puoi abilitare lo schema per l’utilizzo con Real-Time Customer Profile e assegnare i tag necessari per l’inclusione nell’unione. Lo schema con tag farà quindi parte della definizione dello schema da inviare al profilo.

Quando i dati di [!UICONTROL XDM Individual Profile] e [!UICONTROL XDM ExperienceEvent] vengono acquisiti nel data lake, Real-Time Customer Profile acquisisce tutti i dati abilitati per il relativo utilizzo. Più interazioni e dettagli vengono acquisiti, più solidi saranno i singoli profili.

I dati di [!UICONTROL XDM Individual Profile] consentono di informare e abilitare le azioni su qualsiasi canale o integrazione di prodotto Adobe. Se associati a una ricca cronologia di dati comportamentali e di interazione, questi dati possono essere utilizzati per potenziare l’apprendimento automatico. L’API del profilo cliente in tempo reale può essere utilizzata anche per arricchire le funzionalità di soluzioni di terze parti, CRM e soluzioni proprietarie.

Per ulteriori informazioni, vedere [Panoramica del profilo cliente in tempo reale](../profile/home.md).

### Data Science Workspace {#data-science-workspace}

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto. Questa documentazione è destinata ai clienti esistenti che dispongono di diritti precedenti su Data Science Workspace.

Adobe Experience Platform Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per acquisire informazioni dai dati memorizzati in Experience Platform. Data Science Workspace consente ai data scientist di creare ricette basate sui dati di [!UICONTROL XDM Individual Profile] e [!UICONTROL XDM ExperienceEvent] relativi ai clienti e alle loro attività. Queste ricette facilitano le previsioni come la propensione all&#39;acquisto e le offerte consigliate che l&#39;individuo è in grado di apprezzare e utilizzare.

Con Data Science Workspace, i data scientist possono creare facilmente API di servizio intelligenti basate sull’apprendimento automatico. Questi servizi funzionano con altre soluzioni Adobe, tra cui Adobe Target e Adobe Analytics Cloud, per aiutarti ad automatizzare esperienze digitali personalizzate e mirate.

Per ulteriori informazioni sull&#39;utilizzo dei dati di Experience Platform per approfondimenti, consulta la [Panoramica di Data Science Workspace](../data-science-workspace/home.md).

## Passaggi successivi e risorse aggiuntive

Ora che hai capito meglio il ruolo degli schemi in Experience Platform, puoi iniziare a comporne di nuovi.

Per scoprire i principi di progettazione e le best practice per la composizione di schemi da utilizzare con Experience Platform, leggi le [nozioni di base sulla composizione dello schema](schema/composition.md). Per istruzioni dettagliate sulla creazione di uno schema, vedere i tutorial sulla creazione di uno schema [tramite l&#39;API](tutorials/create-schema-api.md) o [tramite l&#39;interfaccia utente](tutorials/create-schema-ui.md).

Per approfondire la tua conoscenza di [!DNL XDM System] in Experience Platform, guarda il seguente video:

>[!VIDEO](https://video.tv.adobe.com/v/38516?captions=ita&quality=12&learn=on)
