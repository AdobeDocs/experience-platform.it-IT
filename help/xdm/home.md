---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sistema XDM (Experience Data Model)
topic: overview
translation-type: tm+mt
source-git-commit: 8ea3b09f86fe11ce7043f22c56ff9756b909e716
workflow-type: tm+mt
source-wordcount: '1777'
ht-degree: 0%

---


# Panoramica del sistema XDM

Standardizzazione e interoperabilità sono concetti chiave  Adobe Experience Platform. Experience Data Model (XDM), guidato da Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione da utilizzare per comunicare con i servizi Platform. Aderendo agli standard XDM, tutti i dati relativi all&#39;esperienza cliente possono essere incorporati in una rappresentazione comune in grado di fornire informazioni approfondite in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti ed esprimere gli attributi del cliente a scopo di personalizzazione.

XDM è il framework fondamentale che consente ad Adobe Experience Cloud,  Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui  Experience Platform è costruito, **XDM System**, rende operativi gli schemi dei modelli di dati esperienza per l&#39;utilizzo da parte dei servizi Platform.

Questo documento fornisce una panoramica del ruolo di XDM System in  Experience Platform.

## Schemi XDM

 Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i diversi sistemi, diventa più semplice mantenere il significato e quindi ottenere valore dai dati.

Prima di poter inserire i dati in Platform, è necessario che uno schema sia composto in modo da descrivere la struttura dei dati e da limitare il tipo di dati che è possibile includere all&#39;interno di ciascun campo. Gli schemi sono composti da una classe base e da zero o più mixin.

Per ulteriori informazioni sul modello di composizione dello schema, compresi i principi di progettazione e le procedure ottimali, vedere le [nozioni di base della composizione](schema/composition.md)dello schema.

### Registro di sistema e libreria schema

Il Registro di sistema **** dello schema fornisce un&#39;interfaccia utente e RESTful API da cui è possibile visualizzare e gestire tutte le risorse relative allo schema nella  Libreria **** schema Adobe Experience Platform. La Libreria schema contiene le risorse standard di settore messe a disposizione da Adobe, nonché le risorse  partner e fornitori Experience Platform di cui si utilizzano le applicazioni. L&#39;interfaccia utente e l&#39;API del Registro di sistema dello schema possono essere utilizzate anche per creare e gestire nuovi schemi e risorse univoci per l&#39;organizzazione.

Per una guida completa alle operazioni principali disponibili nel Registro di sistema dello schema, vedere la guida [per gli sviluppatori del Registro di](api/getting-started.md)schema.

## Comportamenti dei dati in XDM System {#data-behaviors}

I dati da utilizzare in  Experience Platform sono raggruppati in due tipi di comportamento:

* **Record data**: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **Dati** serie temporali: Fornisce un&#39;istantanea del sistema al momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

Tutti gli schemi XDM descrivono i dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla **classe** dello schema, che viene assegnata a uno schema al momento della sua creazione. Le classi XDM descrivono il numero minimo di proprietà che uno schema deve contenere per rappresentare un particolare comportamento di dati.

Sebbene sia possibile definire le proprie classi all&#39;interno del Registro di sistema dello schema, si consiglia di utilizzare rispettivamente le classi preferite **XDM Singolo profilo** e **XDM ExperienceEvent** per i dati relativi a record e serie temporali. Queste classi sono descritte più dettagliatamente di seguito.

### Profilo singolo XDM

XDM Singolo profilo è una classe basata su record che forma una rappresentazione singolare degli attributi di soggetti identificati e parzialmente identificati. I profili altamente identificati possono essere utilizzati per comunicazioni personali o per impegni mirati e possono contenere informazioni personali dettagliate come nome, sesso, data di nascita, luogo e informazioni di contatto, inclusi numeri di telefono e indirizzi e-mail.

I profili meno identificati possono essere costituiti solo da segnali comportamentali anonimi come i cookie del browser. In questo caso, i dati del profilo sparso vengono utilizzati per creare una base di informazioni in cui gli interessi e le preferenze del profilo anonimo vengono raccolti e memorizzati. Questi identificatori possono diventare più dettagliati nel tempo, in quanto l&#39;oggetto si registra per le notifiche, le sottoscrizioni, gli acquisti e così via. Questo aumento degli attributi di profilo potrebbe alla fine dare luogo a un oggetto identificato e consentire un maggiore grado di coinvolgimento mirato.

Con la crescita del profilo del consumatore, il profilo diventa un archivio affidabile delle informazioni personali, delle informazioni di identificazione, dei dati di contatto e delle preferenze di comunicazione di un individuo.

### XDM ExperienceEvent

XDM ExperienceEvent è una classe basata su serie temporale utilizzata per acquisire lo stato del sistema quando si verifica un evento (o un set di eventi), incluso il punto nel tempo e l&#39;identità dell&#39;oggetto interessato. Gli eventi di esperienza sono infatti record di ciò che è accaduto, quindi sono immutabili e rappresentano ciò che è accaduto senza aggregazione o interpretazione. Sono fondamentali per l&#39;analisi del dominio temporale in quanto possono essere utilizzati per analizzare le modifiche che si verificano in una determinata finestra di tempo, e per confrontare tra più finestre di tempo per monitorare le tendenze.

Gli eventi di esperienza possono essere espliciti o impliciti. Gli eventi espliciti sono azioni umane direttamente osservabili che si svolgono durante un punto di un viaggio. Gli eventi impliciti sono eventi che vengono sollevati senza un&#39;azione umana diretta, ma che si riferiscono ancora ad un individuo. Esempi di eventi impliciti possono includere l&#39;invio pianificato di newsletter via e-mail o la tensione della batteria che raggiunge una determinata soglia.

Anche se non tutti gli eventi sono facilmente organizzati per tutte le origini dati, è estremamente utile armonizzare eventi simili in tipi simili, laddove possibile per l&#39;elaborazione.

![Percorso del cliente ExperienceEvent](images/overview/experience-event-journey.png)

## Schemi XDM e servizi Experience Platform 

 Experience Platform è agnostico dello schema, il che significa che qualsiasi schema conforme allo standard XDM è disponibile per l&#39;uso da parte dei servizi Platform. I modi in cui i diversi servizi Platform utilizzano gli schemi sono descritti più dettagliatamente di seguito.

### Servizio Catalogo, Data Ingestion &amp; Data Lake

Catalog Service è il sistema di record per  risorse Experience Platform e i relativi schemi. Catalogo non sono i file o le directory effettivi contenenti dati, ma contiene i metadati e le descrizioni di tali file e directory.

I dati del catalogo sono memorizzati nel Data Lake, un archivio dati altamente granulare contenente tutti i dati gestiti da Platform, indipendentemente dall&#39;origine o dal formato del file.

Per iniziare a assimilare i dati in  Experience Platform, viene creato un set di dati tramite Catalog Service. Il dataset fa riferimento a uno schema XDM che descrive la struttura dei dati da assimilare. Se un dataset viene creato senza uno schema,  Experience Platform deriverà uno &quot;schema osservato&quot; controllando il tipo e il contenuto dei campi di dati acquisiti. I set di dati vengono quindi tracciati in Catalog e memorizzati nel Data Lake insieme agli schemi e agli schemi osservati su cui si basano.

Per ulteriori informazioni su Catalog, consultate la panoramica [di](../catalog/home.md)Catalog Service. Per ulteriori informazioni sullinserimento dei dati di Adobe Experience Platform, consulta la panoramica [sull&#39;inserimento dei](../ingestion/home.md)dati.

### Servizio query

 Adobe Experience Platform Query Service consente di utilizzare SQL standard per eseguire query  dati Experience Platform per supportare molti casi d&#39;uso diversi.

Dopo la composizione di uno schema e la creazione di un dataset che fa riferimento a tale schema, i dati vengono quindi assimilati e memorizzati nel Data Lake. Utilizzando Query Service, è possibile partecipare a qualsiasi set di dati nel Data Lake e acquisire i risultati della query come nuovo set di dati da utilizzare nei report, nell&#39;apprendimento automatico o per l&#39;inserimento nel profilo cliente in tempo reale.

Per ulteriori informazioni sul servizio Query, vedere l&#39;introduzione [del servizio](../query-service/home.md)Query.

### Profilo del cliente in tempo reale

Il profilo del cliente in tempo reale fornisce un profilo del consumatore centralizzato per una gestione mirata e personalizzata dell&#39;esperienza. Ogni profilo contiene dati aggregati per tutti i sistemi, nonché account con marca temporale utilizzabile di eventi che coinvolgono il singolo utente che si sono verificati in uno dei sistemi utilizzati con  Experience Platform.

Il profilo cliente in tempo reale utilizza dati formattati per lo schema in base alle classi XDM Individuale Profile o XDM ExperienceEvent, e risponde alle query basate su tali dati. Il profilo non supporta l&#39;uso di schemi basati su altre classi.

Profilo mantiene un’istanza di ciascun profilo cliente, unendo i dati per formare una &quot;singola origine di verità&quot; per l’individuo. Questi dati unificati vengono rappresentati utilizzando la cosiddetta &quot;visualizzazione unione&quot;. Una vista unione aggrega i campi di tutti gli schemi che implementano la stessa classe in un unico schema.  Quando si compone uno schema utilizzando l&#39;interfaccia utente o l&#39;API, è possibile abilitare lo schema per l&#39;uso con il profilo cliente in tempo reale e assegnargli un tag per l&#39;inclusione nella visualizzazione unione. Lo schema con tag parteciperà quindi alla definizione dello schema da inviare a Profile.

Poiché i dati XDM del profilo singolo e XDM ExperienceEvent sono assimilati e gestiti dal catalogo, il profilo cliente in tempo reale avvia l’acquisizione dei dati che sono stati attivati per il relativo utilizzo. Più interazioni e dettagli vengono acquisiti, più solidi diventano i profili individuali.

I dati del profilo individuale XDM consentono di informare e potenziare le azioni su qualsiasi canale o integrazione con le soluzioni Adobe e, se associati a una ricca cronologia di dati comportamentali e interattivi, questi dati vengono utilizzati per sviluppare l&#39;apprendimento automatico. L&#39;API del profilo cliente in tempo reale può essere utilizzata anche per arricchire le funzionalità di soluzioni, CRM e soluzioni proprietarie di terze parti.

Per ulteriori informazioni, consulta la panoramica [Profilo cliente](../profile/home.md) in tempo reale.

### Area di lavoro Data Science

 Adobe Experience Platform Data Science Workspace utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per ottenere informazioni dai dati memorizzati in  Experience Platform. Data Science Workspace consente agli esperti di analisi dei dati di creare ricette basate su Profilo singolo XDM e sui dati ExperienceEvent XDM relativi ai clienti e alle loro attività, facilitando previsioni quali l&#39;acquisto di propensione e le offerte consigliate che l&#39;individuo probabilmente apprezzerà e utilizzerà.

Con Data Science Workspace, gli esperti di dati possono creare facilmente API di servizi intelligenti basate sull&#39;apprendimento automatico. Questi servizi funzionano con altre soluzioni Adobe, inclusi  Adobe Target e Adobe  Analytics Cloud, per aiutarti a automatizzare esperienze digitali personalizzate e mirate.

Per ulteriori informazioni sull&#39;utilizzo  dati Experience Platform per fornire approfondimenti, consulta la panoramica [di](../data-science-workspace/home.md)Data Science Workspace.

### Servizio di disattivazione

Decisioning Service offre la possibilità di configurare il processo decisionale personalizzato per le offerte nelle applicazioni integrate Platform. Le offerte possono essere raccomandazioni di prodotto, componenti di contenuto per un&#39;esperienza Web, script di conversazione e azioni da intraprendere.

Il servizio di gestione delle decisioni sfrutta i dati del profilo cliente in tempo reale ed è pertanto compatibile solo con i set di dati basati sugli schemi che implementano la classe XDM Singolo profilo o XDM ExperienceEvent.

Per ulteriori informazioni, consulta la panoramica [del servizio](../decisioning-service/home.md) Disegno.

## Passaggi successivi e risorse aggiuntive

Ora che hai capito meglio il ruolo degli schemi in tutto  Experience Platform, sei pronto a iniziare a comporre il tuo. Per continuare a completare l&#39;apprendimento, leggete la documentazione suggerita e guardate il video seguente.

Per apprendere i principi di progettazione e le procedure ottimali per la composizione degli schemi da utilizzare con  Experience Platform, iniziare leggendo le [nozioni di base della composizione](schema/composition.md)dello schema. Per istruzioni dettagliate su come creare uno schema, vedere le esercitazioni sulla creazione di uno schema [mediante l&#39;API](tutorials/create-schema-api.md) o [l&#39;interfaccia](tutorials/create-schema-ui.md)utente.

Per comprendere meglio il sistema XDM in  Experience Platform, guarda il seguente video:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

