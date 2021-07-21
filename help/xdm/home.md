---
keywords: Experience Platform;home;argomenti popolari;XDM;sistema XDM;profilo individuale XDM;ExperienceEvent XDM;evento esperienza XDM;evento esperienza;evento esperienza;gruppi di campi;gruppi di campi;gruppo di campi;evento esperienza;evento esperienza XDM;evento esperienza XDM;evento esperienza;evento esperienza;evento;esperienza;modello di dati XDM;modello di dati esperienza;modello di dati esperienza;modello di dati esperienza;modello di dati;modello di dati schema di registro;Schema di registro;libreria di schemi;libreria di schemi;schema;record di dati;serie temporali;serie temporali
solution: Experience Platform
title: Panoramica del sistema XDM
topic-legacy: overview
description: La standardizzazione e l'interoperabilità sono concetti chiave alla base di Adobe Experience Platform. Experience Data Model (XDM), basato su un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 9fda5dad7b7e29c88598ff299c26277a015277a6
workflow-type: tm+mt
source-wordcount: '1993'
ht-degree: 0%

---

# Panoramica del sistema XDM

>[!NOTE]
>
>Il termine &quot;mixin&quot; è stato aggiornato allo schema &quot;gruppo di campi&quot; per promuovere la comprensione. I gruppi di campi sono insiemi di campi riutilizzabili per supportare i casi di utilizzo aziendali. Questa modifica si riflette ora nell’API del Registro di sistema dello schema, nell’interfaccia utente di Adobe Experience Platform e in tutta la documentazione di Platform.

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di Adobe Experience Platform. [!DNL Experience Data Model] (XDM), guidato da un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare il potere delle esperienze digitali. Fornisce strutture e definizioni comuni che consentono a qualsiasi applicazione di comunicare con i servizi di Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che può fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti ed esprimere gli attributi dei clienti a scopo di personalizzazione.

XDM è il framework fondamentale che consente a Adobe Experience Cloud, basato sull&#39;Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui viene generato l’Experience Platform, XDM System, rende operativi gli schemi [!DNL Experience Data Model] per l’utilizzo da parte dei servizi Platform.

Questo documento fornisce una panoramica del ruolo del sistema XDM all&#39;interno di Experience Platform.

## Schemi XDM

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i diversi sistemi, diventa più facile mantenere il significato e quindi ottenere valore dai dati.

Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che può essere contenuto all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più gruppi di campi dello schema.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, consulta le [nozioni di base sulla composizione dello schema](schema/composition.md).

### Componenti XDM standard

XDM fornisce una raccolta affidabile di gruppi di campi e tipi di dati standard, allo scopo di acquisire concetti e casi di utilizzo comuni in diversi settori. L’Experience Platform ti consente di filtrare questi componenti per settore, consentendoti di creare in modo rapido e sicuro schemi che supportano al meglio le tue particolari esigenze aziendali.

Quando si creano schemi nell’interfaccia utente di Experience Platform, i gruppi di campi elencati vengono visualizzati con una metrica di popolarità. Questa metrica è determinata dalla frequenza con cui gli altri utenti di Platform utilizzano il gruppo di campi nei loro schemi. Maggiore è il numero, più popolare sarà il gruppo di campi. Per impostazione predefinita, i risultati vengono visualizzati dai più popolari ai meno popolari, tenendoti informato sulle tendenze di modellazione dei dati nel tuo settore.

![Popolarità del gruppo di campi](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform fornisce un’interfaccia utente e RESTful API da cui è possibile visualizzare e gestire tutte le risorse relative allo schema nell’Experience Platform **[!DNL Schema Library]**. Il [!DNL Schema Library] contiene componenti XDM standard resi disponibili per Adobe, nonché risorse di partner e fornitori di Experience Platform le cui applicazioni utilizzi.

Utilizzando l’area di lavoro [!DNL Schema Registry API] o [!UICONTROL Schemi] nell’interfaccia utente di Platform, puoi anche creare e gestire nuovi schemi e risorse esclusivi per la tua organizzazione.

Per ulteriori informazioni su come gestire e interagire con gli schemi in Platform, consulta la seguente documentazione:

* [Guida all’interfaccia utente XDM](./ui/overview.md)
* [Guida all’API del registro dello schema](./api/overview.md)

## Comportamenti dei dati nel sistema XDM {#data-behaviors}

I dati destinati ad essere utilizzati in Experience Platform sono raggruppati in due tipi di comportamento:

* **Dati** record: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **Dati** della serie temporale: Fornisce un&#39;istantanea del sistema al momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

Tutti gli schemi XDM descrivono i dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla classe dello schema, che viene assegnata a uno schema quando viene creato per la prima volta. Le classi XDM descrivono il numero minimo di proprietà che uno schema deve contenere per rappresentare un particolare comportamento di dati.

Sebbene sia possibile definire le proprie classi all&#39;interno di [!DNL Schema Registry], si consiglia di utilizzare le classi preferite **[!UICONTROL Profilo individuale XDM]** e **[!UICONTROL XDM ExperienceEvent]** rispettivamente per i dati di record e le serie temporali. Queste classi sono descritte più dettagliatamente di seguito.

### [!UICONTROL Profilo individuale XDM] {#xdm-individual-profile}

[!UICONTROL XDM Singoli ] Profileè una classe basata su record che forma una singola rappresentazione degli attributi di soggetti identificati e parzialmente identificati. I profili altamente identificati possono essere utilizzati per comunicazioni personali o per impegni mirati e possono contenere informazioni personali dettagliate come nome, genere, data di nascita, ubicazione e informazioni di contatto, compresi i numeri di telefono e gli indirizzi e-mail.

I profili meno identificati possono essere costituiti solo da segnali comportamentali anonimi come i cookie del browser. In questo caso, i dati del profilo sparso vengono utilizzati per creare una base di informazioni in cui gli interessi e le preferenze del profilo anonimo vengono raggruppati e memorizzati. Questi identificatori possono diventare più dettagliati nel tempo in quanto l’oggetto si registra per notifiche, abbonamenti, acquisti e così via. Questo aumento degli attributi del profilo può alla fine dare luogo a un soggetto identificato e consentire un maggiore grado di coinvolgimento mirato.

Man mano che un profilo cresce, diventa un solido archivio delle informazioni personali, delle informazioni di identificazione, dei dati di contatto e delle preferenze di comunicazione di un individuo.

Per ulteriori informazioni sulla struttura e il caso d’uso dei campi forniti dalla classe, consulta la [[!UICONTROL Guida di riferimento di ] XDM Singolo profilo](./classes/individual-profile.md) .

### [!UICONTROL ExperienceEvent XDM] {#xdm-experience-event}

XDM ExperienceEvent è una classe basata su serie temporale utilizzata per acquisire lo stato del sistema quando si è verificato un evento (o un set di eventi), incluso il punto nel tempo e l’identità dell’oggetto coinvolto. Gli eventi di esperienza sono documenti fattuali immutabili di ciò che si è verificato in quel momento, che rappresentano ciò che è accaduto senza aggregazione o interpretazione. Sono fondamentali per l’analisi del dominio temporale in quanto possono essere utilizzati per analizzare le modifiche che si verificano in una determinata finestra di tempo e per confrontare tra più finestre di tempo per monitorare le tendenze.

Gli eventi di esperienza possono essere espliciti o impliciti. Eventi espliciti sono azioni umane direttamente osservabili che si svolgono durante un punto in un percorso. Gli eventi impliciti sono eventi che vengono sollevati senza un&#39;azione umana diretta, ma che si riferiscono ancora ad un individuo. Esempi di eventi impliciti possono includere l&#39;invio programmato di newsletter via e-mail o tensione della batteria che raggiunge una certa soglia.

Sebbene non tutti gli eventi siano facilmente organizzati in tutte le origini dati, è estremamente utile armonizzare eventi simili in tipi simili, laddove possibile, per l’elaborazione.

![Percorso cliente ExperienceEvent](images/overview/experience-event-journey.png)

Per ulteriori informazioni sulla struttura e sul caso d’uso dei campi forniti dalla classe, consulta la [[!UICONTROL Guida di riferimento di ExperienceEvent] XDM](./classes/experienceevent.md) .

## Schemi XDM e servizi di Experience Platform

Ad Experience Platform, è indipendente dallo schema, il che significa che qualsiasi schema conforme allo standard XDM viene reso disponibile ai servizi Platform. Di seguito sono descritti più dettagliatamente i modi in cui diversi servizi di Platform utilizzano gli schemi.

### Servizio catalogo, acquisizione dati e Data Lake

Servizio catalogo è il sistema di record per le risorse di Experience Platform e i relativi schemi. Il catalogo non contiene i file o le directory di dati effettivi, ma contiene i metadati e le descrizioni di tali file e directory.

I dati del catalogo vengono memorizzati nel Data Lake, un archivio dati altamente granulare contenente tutti i dati gestiti da Platform, indipendentemente dall’origine o dal formato del file.

Per iniziare ad acquisire i dati in Experience Platform, puoi utilizzare il servizio catalogo per creare un set di dati. Il set di dati fa riferimento a uno schema XDM che descrive la struttura dei dati da acquisire. Se un set di dati viene creato senza uno schema, l’Experience Platform deriva uno &quot;schema osservato&quot; controllando il tipo e il contenuto dei campi di dati acquisiti. I set di dati vengono quindi tracciati in Catalogo e memorizzati nel Data Lake accanto agli schemi e agli schemi osservati su cui si basano.

Per ulteriori informazioni sul Catalogo, consulta la [Panoramica del servizio catalogo](../catalog/home.md). Per ulteriori informazioni sull&#39;acquisizione dei dati da parte di Adobe Experience Platform, consulta la [Panoramica sull&#39;acquisizione dei dati](../ingestion/home.md).

### Servizio query

Adobe Experience Platform Query Service consente di utilizzare SQL standard per eseguire query sui dati di Experience Platform per supportare molti casi d’uso diversi.

Una volta creato uno schema e creato un set di dati che fa riferimento a tale schema, i dati vengono quindi acquisiti e memorizzati nel Data Lake. Utilizzando Query Service, puoi unire qualsiasi set di dati nel Data Lake e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, nell’apprendimento automatico o per l’inserimento nel Profilo cliente in tempo reale.

Per ulteriori informazioni sul servizio, consulta la [Panoramica del servizio query](../query-service/home.md) .

### Profilo cliente in tempo reale

Profilo cliente in tempo reale fornisce un profilo consumatore centralizzato per una gestione delle esperienze mirata e personalizzata. Ogni profilo contiene dati aggregati in tutti i sistemi, nonché account con marca temporale utilizzabili per eventi che coinvolgono il singolo utente che si sono verificati in uno dei sistemi utilizzati con Experience Platform.

Profilo cliente in tempo reale utilizza dati formattati in base allo schema in base alle classi [!UICONTROL XDM Singolo profilo] e [!UICONTROL XDM ExperienceEvent] e risponde alle query basate su tali dati. Il profilo non supporta l’utilizzo di schemi basati su altre classi.

Il sistema mantiene un&#39;istanza di ciascun profilo cliente, unendo i dati per formare una &quot;singola fonte di verità&quot; per l&#39;individuo. Questi dati unificati vengono rappresentati utilizzando uno &quot;schema di unione&quot; (a volte denominato &quot;visualizzazione di unione&quot;). Uno schema di unione aggrega i campi di tutti gli schemi che implementano la stessa classe in un unico schema.  Quando si compone uno schema utilizzando l’interfaccia utente o l’API, è possibile abilitare lo schema per l’utilizzo con Profilo cliente in tempo reale e assegnare tag per l’inclusione nell’unione. Lo schema con tag partecipa quindi alla definizione dello schema da inviare al profilo.

Poiché i dati [!UICONTROL XDM Singolo profilo] e [!UICONTROL XDM ExperienceEvent] vengono acquisiti nel Data Lake, il Profilo cliente in tempo reale acquisisce tutti i dati abilitati per il suo utilizzo. Più interazioni e dettagli vengono acquisiti, più i profili individuali diventano solidi.

[!UICONTROL I dati ] Profiledati individuali XDM consentono di informare e abilitare le azioni su qualsiasi canale o integrazione di prodotti Adobe. Se associati a una ricca cronologia dei dati comportamentali e interattivi, questi dati possono essere utilizzati per potenziare l&#39;apprendimento automatico. L’API del profilo cliente in tempo reale può essere utilizzata anche per arricchire le funzionalità di soluzioni di terze parti, CRM e soluzioni proprietarie.

Per ulteriori informazioni, consulta la [Panoramica sul profilo cliente in tempo reale](../profile/home.md) .

### Data Science Workspace

Adobe Experience Platform Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per ottenere informazioni dai dati archiviati in Experience Platform. Data Science Workspace consente agli scienziati dei dati di creare ricette basate su [!UICONTROL Profilo individuale XDM] e [!UICONTROL XDM ExperienceEvent] dati sui clienti e le loro attività, facilitando previsioni come l&#39;acquisto di propensione e offerte consigliate che l&#39;individuo è probabile apprezzare e utilizzare.

Con Data Science Workspace, gli scienziati dei dati possono creare facilmente API di servizio intelligenti alimentate dall&#39;apprendimento automatico. Questi servizi funzionano con altre soluzioni di Adobe, tra cui Adobe Target e Adobe Analytics Cloud, per aiutarti a automatizzare esperienze digitali personalizzate e mirate.

Per ulteriori informazioni sull&#39;utilizzo dei dati di Experience Platform per fornire informazioni approfondite, consulta la [panoramica di Data Science Workspace](../data-science-workspace/home.md).

## Passaggi successivi e risorse aggiuntive

Ora che si capisce meglio il ruolo degli schemi in tutto l&#39;Experience Platform, si è pronti a iniziare a comporre il proprio.

Per conoscere i principi di progettazione e le best practice per la composizione degli schemi da utilizzare con Experience Platform, inizia leggendo le [nozioni di base della composizione dello schema](schema/composition.md). Per istruzioni dettagliate su come creare uno schema, consulta le esercitazioni sulla creazione di uno schema [utilizzando l&#39;API](tutorials/create-schema-api.md) o [utilizzando l&#39;interfaccia utente](tutorials/create-schema-ui.md).

Per approfondire la conoscenza di [!DNL XDM System] nell’Experience Platform, guarda il seguente video:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
