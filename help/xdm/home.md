---
keywords: Experience Platform;home;argomenti popolari;XDM;XDM system;XDM profilo individuale;XDM ExperienceEvent;XDM ExperienceEvent;experienceEvent;evento esperienza;gruppi di campi;gruppi di campi;gruppo di campi;gruppo di campi;Evento esperienza;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevent;Experience data model;Experience data model;Experience Data Model;modello dati;modello dati;modello dati;modello dati;modello dati;modello dati;registro schemi;registro schemi;libreria schemi;schema;schema;dati record;serie temporali
solution: Experience Platform
title: Panoramica del sistema XDM
description: La standardizzazione e l'interoperabilità sono concetti chiave alla base di Adobe Experience Platform. Experience Data Model (XDM), guidato da Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi per la gestione della customer experience.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 48caa318f0e951979db4fd2c94624a73311422d6
workflow-type: tm+mt
source-wordcount: '2101'
ht-degree: 0%

---

# Panoramica del sistema XDM

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di Adobe Experience Platform. Experience Data Model (XDM), guidato da Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni che consentono a qualsiasi applicazione di comunicare con i servizi di Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che può fornire informazioni in modo più veloce e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti ed esprimere gli attributi dei clienti a scopo di personalizzazione.

XDM è il framework fondamentale che consente a Adobe Experience Cloud, basato su Experienci Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, nel momento esatto giusto. La metodologia su cui viene creato l’Experience Platform, XDM System, rende operativi gli schemi Experience Data Model per l’utilizzo da parte dei servizi di Platform.

Scopri il ruolo del sistema XDM in Experienci Platform.

## Schemi XDM {#xdm-schemas}

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e quindi ottenere valore dai dati.

Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che possono essere contenuti all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più gruppi di campi schema.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, vedere [nozioni di base sulla composizione dello schema](schema/composition.md).

### Componenti XDM standard {#Standard-xdm-components}

XDM fornisce una solida raccolta di gruppi di campi e tipi di dati standard, pensati per acquisire concetti e casi d’uso comuni a diversi settori. Experienci Platform consente di filtrare questi componenti per settore, consentendo di creare schemi in modo rapido e sicuro che supportano al meglio le specifiche esigenze aziendali.

Durante la costruzione di schemi nell’interfaccia utente di Experienci Platform, i gruppi di campi elencati vengono visualizzati con una metrica di popolarità. Questa metrica è determinata dalla frequenza con cui altri utenti di Platform utilizzano il gruppo di campi nei loro schemi. Più alto è il numero, più popolare sarà il gruppo di campi. Per impostazione predefinita, i risultati vengono visualizzati da quelli più popolari a quelli meno popolari, per tenerti informato sulle tendenze di modellazione dei dati nel tuo settore.

![La colonna popolarità della [!UICONTROL Aggiungi gruppo di campi] .](./images/overview/popularity.png)

### [!DNL Schema Library] {#schema-library}

L’Experience Platform fornisce un’interfaccia utente e un’API RESTful da cui è possibile visualizzare e gestire tutte le risorse relative allo schema presenti nell’Experience Platform **[!DNL Schema Library]**. Il [!DNL Schema Library] contiene i componenti XDM standard resi disponibili da Adobe, nonché le risorse dei partner e dei fornitori Experienci Platform di cui utilizzi le applicazioni.

Puoi anche creare e gestire nuovi schemi e risorse specifici per la tua organizzazione utilizzando [!DNL Schema Registry API]o [!UICONTROL Schemi] nell’interfaccia utente di Platform.

Per ulteriori informazioni su come gestire e interagire con gli schemi in Platform, consulta la seguente documentazione:

* [Guida all’interfaccia utente XDM](./ui/overview.md)
* [Guida API del registro dello schema](./api/overview.md)

## Comportamenti dei dati nel sistema XDM {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="Comportamenti dei dati"
>abstract="I dati da utilizzare in Experienci Platform sono raggruppati in tre tipi di comportamento: record, serie temporali e ad hoc. Gli schemi di record forniscono informazioni sugli attributi di un soggetto, mentre gli schemi di serie temporali acquisiscono un’istantanea del sistema nel momento in cui è stata eseguita un’azione. Gli schemi ad hoc acquisiscono campi con namespace utilizzabili solo da un singolo set di dati. Consulta la documentazione per ulteriori informazioni sui comportamenti dei dati in Platform."

I dati da utilizzare in Experienci Platform sono raggruppati in tre tipi di comportamento:

* **Registra**: fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **Serie temporali**: fornisce un’istantanea del sistema nel momento in cui un oggetto record ha eseguito un’azione, direttamente o indirettamente.
* **Ad hoc**: acquisisce i campi con namespace che possono essere utilizzati solo da un singolo set di dati. Gli schemi ad hoc vengono utilizzati in vari flussi di lavoro di acquisizione dati, ad Experience Platform, l’acquisizione di file CSV e la creazione di alcuni tipi di connessioni sorgente.

Tutti gli schemi XDM descrivono dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla classe dello schema, che viene assegnata a uno schema al momento della creazione. Le classi XDM descrivono il minor numero di proprietà che uno schema deve contenere per rappresentare un particolare comportamento di dati.

Anche se è possibile definire classi personalizzate all&#39;interno del [!DNL Schema Registry], si consiglia di utilizzare le classi standard **[!UICONTROL Profilo individuale XDM]** e **[!UICONTROL XDM ExperienceEvent]** per i dati di record e di serie temporali, rispettivamente. Tali classi sono descritte più dettagliatamente di seguito.

>[!NOTE]
>
>Non esistono classi standard basate sul comportamento ad hoc. Gli schemi ad hoc vengono generati automaticamente dai processi Platform che li utilizzano, ma possono anche essere [creato manualmente utilizzando l’API Schema Registry](./tutorials/ad-hoc.md).

### [!UICONTROL Profilo individuale XDM] {#xdm-individual-profile}

[!UICONTROL Profilo individuale XDM] è una classe basata su record che costituisce una singola rappresentazione degli attributi sia dei soggetti identificati che parzialmente identificati. I profili altamente identificati possono essere utilizzati per comunicazioni personali o impegni mirati. I profili altamente identificati possono contenere informazioni personali dettagliate come nome, genere, data di nascita, posizione e informazioni di contatto, inclusi numeri di telefono e indirizzi e-mail.

I profili meno identificati possono essere costituiti solo da segnali comportamentali anonimi come i cookie del browser. In questo caso, i dati di profilo sparsi vengono utilizzati per creare una base di informazioni in cui gli interessi e le preferenze del profilo anonimo vengono raccolti e memorizzati. Questi identificatori possono diventare più dettagliati nel tempo, man mano che il soggetto si iscrive a notifiche, abbonamenti, acquisti e così via. Questo aumento degli attributi del profilo può infine causare un soggetto identificato e consentire un livello più elevato di coinvolgimento mirato.

Man mano che un profilo continua a crescere, diventa un solido archivio di informazioni personali, informazioni di identificazione, dettagli di contatto e preferenze di comunicazione di un individuo.

Consulta la [[!UICONTROL Profilo individuale XDM] guida di riferimento](./classes/individual-profile.md) per ulteriori informazioni sulla struttura e sul caso d’uso dei campi forniti dalla classe.

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent è una classe basata su serie temporali utilizzata per acquisire lo stato del sistema quando si è verificato un evento (o un set di eventi), compreso il momento e l’identità del soggetto interessato. Gli Eventi di esperienza sono registrazioni fattuali e immutabili di ciò che si è verificato in quel momento, che rappresentano ciò che è accaduto senza aggregazione o interpretazione. Sono fondamentali per l’analisi del dominio temporale in quanto possono essere utilizzati per analizzare i cambiamenti che si verificano in una determinata finestra temporale e per confrontare tra più finestre temporali al fine di tracciare le tendenze.

Gli eventi esperienza possono essere espliciti o impliciti. Gli eventi espliciti sono azioni umane direttamente osservabili che si verificano durante un punto di un percorso. Gli eventi impliciti sono eventi che vengono generati senza un&#39;azione umana diretta, ma che sono comunque correlati a un individuo. Esempi di eventi impliciti possono includere l’invio pianificato di newsletter via e-mail o il raggiungimento di una determinata soglia per la tensione della batteria.

Anche se non tutti gli eventi sono facilmente categorizzati in tutte le origini dati, è estremamente utile armonizzare eventi simili in tipi simili, ove possibile per l’elaborazione.

![Un’infografica del Percorso di clienti visualizzata con eventi di esperienza nel tempo.](images/overview/experience-event-journey.png)

Consulta la [[!UICONTROL XDM ExperienceEvent] guida di riferimento](./classes/experienceevent.md) per ulteriori informazioni sulla struttura e sul caso d’uso dei campi forniti dalla classe.

## Schemi XDM e servizi Experienci Platform {#schemas-and-platform-services}

L’Experience Platform è indipendente dallo schema, il che significa che qualsiasi schema conforme allo standard XDM viene reso disponibile ai servizi Platform. Di seguito sono descritti più dettagliatamente i modi in cui i diversi servizi Platform utilizzano gli schemi.

### Catalog Service, acquisizione dati e data lake {#ingestion-catalog-and-storage}

Catalog Service è il sistema di registrazione per le risorse Experienci Platform e i relativi schemi. Il catalogo non contiene i file di dati o le directory effettive, ma contiene i metadati e le descrizioni di tali file e directory.

I dati del catalogo vengono memorizzati nel data lake, un archivio di dati altamente granulare contenente tutti i dati gestiti da Platform, indipendentemente dall’origine o dal formato del file.

Per iniziare a acquisire i dati in Experienci Platform, puoi utilizzare Catalog Service per creare un set di dati. Il set di dati fa riferimento a uno schema XDM che descrive la struttura dei dati da acquisire. Se un set di dati viene creato senza uno schema, Experienci Platform deriva uno &quot;schema osservato&quot; esaminando il tipo e il contenuto dei campi di dati acquisiti. I set di dati vengono quindi tracciati in Catalog Service e memorizzati nel data lake insieme agli schemi e agli schemi osservati su cui si basano.

Consulta la [Panoramica di Catalog Service](../catalog/home.md) per ulteriori informazioni. Consulta la [Panoramica sull’acquisizione dei dati](../ingestion/home.md) per ulteriori informazioni su Acquisizione dati di Adobe Experience Platform.

### Servizio query {#query-service}

È possibile utilizzare SQL standard per eseguire query sui dati di Experience Platform per supportare molti casi d’uso diversi con Adobe Experience Platform Query Service.

Dopo aver composto uno schema e creato un set di dati che fa riferimento a tale schema, i dati vengono quindi acquisiti e memorizzati nel data lake. Puoi quindi utilizzare Query Service per unire qualsiasi set di dati nel data lake e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, nell’apprendimento automatico o nell’acquisizione in Real-Time Customer Profile.

Consulta la sezione [Panoramica di Query Service](../query-service/home.md) per ulteriori informazioni sul servizio.

### Profilo cliente in tempo reale {#real-time-customer-profile}

Real-Time Customer Profile fornisce un profilo consumer centralizzato per una gestione mirata e personalizzata delle esperienze. Ogni profilo contiene dati aggregati in tutti i sistemi e include account con marca temporale utilizzabile di eventi che coinvolgono l’oggetto del profilo. Questi eventi possono essersi verificati in uno qualsiasi dei sistemi utilizzati con Experienci Platform.

Real-Time Customer Profile utilizza dati in formato schema basati su [!UICONTROL Profilo individuale XDM] e [!UICONTROL XDM ExperienceEvent] e risponde alle query basate su tali dati.

Il sistema gestisce un’istanza di ciascun profilo cliente, unendo i dati in modo da formare un’unica fonte di verità per l’individuo. Questi dati unificati vengono rappresentati utilizzando quello che è noto come &quot;schema di unione&quot; (a volte indicato come &quot;visualizzazione unione&quot;). Uno schema di unione aggrega i campi di tutti gli schemi che implementano la stessa classe in un singolo schema. Durante la composizione di uno schema tramite l’interfaccia utente o l’API, puoi abilitare lo schema per l’utilizzo con Real-Time Customer Profile e assegnare i tag necessari per l’inclusione nell’unione. Lo schema con tag farà quindi parte della definizione dello schema da inviare al profilo.

As [!UICONTROL Profilo individuale XDM] e [!UICONTROL XDM ExperienceEvent] I dati vengono acquisiti nel data lake. Real-Time Customer Profile acquisisce tutti i dati abilitati per il relativo utilizzo. Più interazioni e dettagli vengono acquisiti, più solidi saranno i singoli profili.

[!UICONTROL Profilo individuale XDM] I dati di consentono di informare e abilitare le azioni su qualsiasi canale o integrazione di prodotto Adobe. Se associati a una ricca cronologia di dati comportamentali e di interazione, questi dati possono essere utilizzati per potenziare l’apprendimento automatico. L’API del profilo cliente in tempo reale può essere utilizzata anche per arricchire le funzionalità di soluzioni di terze parti, CRM e soluzioni proprietarie.

Consulta la [Panoramica del profilo cliente in tempo reale](../profile/home.md) per ulteriori informazioni.

### Data Science Workspace {#data-science-workspace}

Adobe Experience Platform Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per acquisire informazioni approfondite dai dati memorizzati in Experienci Platform. Data Science Workspace consente ai data scientist di creare ricette basate su [!UICONTROL Profilo individuale XDM] e [!UICONTROL XDM ExperienceEvent] dati sui clienti e sulle loro attività. Queste ricette facilitano le previsioni come la propensione all&#39;acquisto e le offerte consigliate che l&#39;individuo è in grado di apprezzare e utilizzare.

Con Data Science Workspace, i data scientist possono creare facilmente API di servizi intelligenti basate sull’apprendimento automatico. Questi servizi funzionano con altre soluzioni di Adobe, tra cui Adobe Target e Adobe Analytics Cloud, per aiutarti ad automatizzare esperienze digitali personalizzate e mirate.

Per ulteriori informazioni sull’utilizzo dei dati di Experienci Platform per approfondimenti, consulta [Panoramica di Data Science Workspace](../data-science-workspace/home.md).

## Passaggi successivi e risorse aggiuntive

Ora che hai capito meglio il ruolo degli schemi nell’Experience Platform, sei pronto per iniziare a comporne uno tuo.

Per scoprire i principi di progettazione e le best practice per la composizione di schemi da utilizzare con Experienci Platform, leggi [nozioni di base sulla composizione dello schema](schema/composition.md). Per istruzioni dettagliate su come creare uno schema, consulta i tutorial sulla creazione di uno schema [utilizzo dell’API](tutorials/create-schema-api.md) o [tramite l’interfaccia utente di](tutorials/create-schema-ui.md).

Per approfondire la comprensione di [!DNL XDM System] ad Experience Platform, guarda il seguente video:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
