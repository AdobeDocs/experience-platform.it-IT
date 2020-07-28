---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sistema XDM (Experience Data Model)
topic: overview
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 0%

---


# Panoramica del sistema XDM

Standardizzazione e interoperabilità sono concetti chiave  Adobe Experience Platform. [!DNL Experience Data Model] (XDM), guidato da  Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione da utilizzare per comunicare con [!DNL Platform] i servizi. Aderendo agli standard XDM, tutti i dati relativi all&#39;esperienza cliente possono essere incorporati in una rappresentazione comune in grado di fornire informazioni approfondite in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti ed esprimere gli attributi del cliente a scopo di personalizzazione.

XDM è il framework fondamentale che consente a Adobe Experience Cloud, alimentato da [!DNL Experience Platform], di inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui [!DNL Experience Platform] è costruito, **XDM System**, rende operativi [!DNL Experience Data Model] gli schemi per l&#39;uso da parte dei [!DNL Platform] servizi.

Questo documento fornisce una panoramica del ruolo di XDM System all&#39;interno [!DNL Experience Platform].

## Schemi XDM

[!DNL Experience Platform] utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i diversi sistemi, diventa più semplice mantenere il significato e quindi ottenere valore dai dati.

Prima di poter inserire i dati [!DNL Platform], è necessario che uno schema sia composto per descrivere la struttura dei dati e per fornire vincoli al tipo di dati che è possibile includere all&#39;interno di ciascun campo. Gli schemi sono composti da una classe base e da zero o più mixin.

Per ulteriori informazioni sul modello di composizione dello schema, compresi i principi di progettazione e le procedure ottimali, vedere le [nozioni di base della composizione](schema/composition.md)dello schema.

### [!DNL Schema Registry] ed [!DNL Schema Library]

L&#39; **[!DNL Schema Registry]** applicazione fornisce un&#39;interfaccia utente e RESTful API da cui è possibile visualizzare e gestire tutte le risorse relative allo schema nel Adobe Experience Platform  **[!DNL Schema Library]**. Il [!DNL Schema Library] pacchetto contiene risorse standard di settore messe a vostra disposizione da  Adobe, così come risorse da parte di [!DNL Experience Platform] partner e fornitori di cui utilizzate le applicazioni. L&#39;interfaccia utente e l&#39;API del Registro di sistema dello schema possono essere utilizzate anche per creare e gestire nuovi schemi e risorse univoci per l&#39;organizzazione.

Per una guida completa alle operazioni principali disponibili in [!DNL Schema Registry], vedere la guida [per gli sviluppatori del Registro di](api/getting-started.md)schema.

## Comportamenti dei dati in XDM System {#data-behaviors}

I dati destinati all&#39;uso in [!DNL Experience Platform] sono raggruppati in due tipi di comportamento:

* **Record data**: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **Dati** serie temporali: Fornisce un&#39;istantanea del sistema al momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

Tutti gli schemi XDM descrivono i dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla **classe** dello schema, che viene assegnata a uno schema al momento della sua creazione. Le classi XDM descrivono il numero minimo di proprietà che uno schema deve contenere per rappresentare un particolare comportamento di dati.

Sebbene sia possibile definire classi personalizzate all&#39;interno di [!DNL Schema Registry], si consiglia di utilizzare rispettivamente le classi preferite **[!DNL XDM Individual Profile]** e **[!DNL XDM ExperienceEvent]** i dati di record e serie temporali. Queste classi sono descritte più dettagliatamente di seguito.

### [!DNL XDM Individual Profile]

[!DNL XDM Individual Profile] è una classe basata su record che forma una singola rappresentazione degli attributi di soggetti identificati e parzialmente identificati. I profili altamente identificati possono essere utilizzati per comunicazioni personali o per impegni mirati e possono contenere informazioni personali dettagliate come nome, sesso, data di nascita, luogo e informazioni di contatto, inclusi numeri di telefono e indirizzi e-mail.

I profili meno identificati possono essere costituiti solo da segnali comportamentali anonimi come i cookie del browser. In questo caso, i dati del profilo sparso vengono utilizzati per creare una base di informazioni in cui gli interessi e le preferenze del profilo anonimo vengono raccolti e memorizzati. Questi identificatori possono diventare più dettagliati nel tempo, in quanto l&#39;oggetto si registra per le notifiche, le sottoscrizioni, gli acquisti e così via. Questo aumento degli attributi di profilo potrebbe alla fine dare luogo a un oggetto identificato e consentire un maggiore grado di coinvolgimento mirato.

Con la crescita del profilo del consumatore, il profilo diventa un archivio affidabile delle informazioni personali, delle informazioni di identificazione, dei dati di contatto e delle preferenze di comunicazione di un individuo.

### [!DNL XDM ExperienceEvent]

XDM ExperienceEvent è una classe basata su serie temporale utilizzata per acquisire lo stato del sistema quando si verifica un evento (o un set di eventi), incluso il punto nel tempo e l&#39;identità dell&#39;oggetto interessato. Gli eventi di esperienza sono infatti record di ciò che è accaduto, quindi sono immutabili e rappresentano ciò che è accaduto senza aggregazione o interpretazione. Sono fondamentali per l&#39;analisi del dominio temporale in quanto possono essere utilizzati per analizzare le modifiche che si verificano in una determinata finestra di tempo, e per confrontare tra più finestre di tempo per monitorare le tendenze.

Gli eventi di esperienza possono essere espliciti o impliciti. Gli eventi espliciti sono azioni umane direttamente osservabili che si svolgono durante un punto di un viaggio. Gli eventi impliciti sono eventi che vengono sollevati senza un&#39;azione umana diretta, ma che si riferiscono ancora ad un individuo. Esempi di eventi impliciti possono includere l&#39;invio pianificato di newsletter via e-mail o la tensione della batteria che raggiunge una determinata soglia.

Anche se non tutti gli eventi sono facilmente organizzati per tutte le origini dati, è estremamente utile armonizzare eventi simili in tipi simili, laddove possibile per l&#39;elaborazione.

![Percorso del cliente ExperienceEvent](images/overview/experience-event-journey.png)

## schemi e [!DNL Experience Platform] servizi XDM

[!DNL Experience Platform] è agnostico dello schema, il che significa che qualsiasi schema conforme allo standard XDM è disponibile per l&#39;uso da parte dei [!DNL Platform] servizi. I modi in cui i diversi [!DNL Platform] servizi utilizzano gli schemi sono descritti più dettagliatamente di seguito.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] è il sistema di registrazione delle [!DNL Experience Platform] risorse e dei relativi schemi. [!DNL Catalog] non sono i file o le directory effettivi contenenti i dati, ma contengono i metadati e le descrizioni di tali file e directory.

[!DNL Catalog] i dati sono memorizzati in [!DNL Data Lake], un archivio dati altamente granulare contenente tutti i dati gestiti da [!DNL Platform], indipendentemente dall&#39;origine o dal formato del file.

Per iniziare a assimilare i dati in [!DNL Experience Platform], viene creato un dataset utilizzando [!DNL Catalog Service]. Il dataset fa riferimento a uno schema XDM che descrive la struttura dei dati da assimilare. Se un dataset viene creato senza uno schema, [!DNL Experience Platform] verrà derivato uno &quot;schema osservato&quot;, controllando il tipo e il contenuto dei campi di dati acquisiti. I set di dati vengono quindi tracciati [!DNL Catalog] e memorizzati [!DNL Data Lake] accanto agli schemi e agli schemi osservati su cui si basano.

Per ulteriori informazioni su [!DNL Catalog]questo argomento, consultate la panoramica [del servizio](../catalog/home.md)catalogo. Per ulteriori informazioni sullinserimento dei dati di Adobe Experience Platform, consulta la panoramica [sull&#39;inserimento dei](../ingestion/home.md)dati.

### [!DNL Query Service]

 Adobe Experience Platform [!DNL Query Service] consente di utilizzare SQL standard per eseguire query [!DNL Experience Platform] sui dati per supportare molti casi di utilizzo diversi.

Dopo la composizione di uno schema e la creazione di un set di dati che fa riferimento a tale schema, i dati vengono quindi assimilati e memorizzati nel [!DNL Data Lake]. Utilizzando [!DNL Query Service], è possibile unire qualsiasi set di dati nel modulo [!DNL Data Lake] e acquisire i risultati della query come nuovo set di dati da utilizzare nei report, nell&#39;apprendimento automatico o per l&#39;inserimento in [!DNL Real-time Customer Profile].

Per ulteriori informazioni [!DNL Query Service], consultate l&#39;introduzione [del servizio](../query-service/home.md)query.

### [!DNL Real-time Customer Profile]

Il profilo del cliente in tempo reale fornisce un profilo del consumatore centralizzato per una gestione mirata e personalizzata dell&#39;esperienza. Ogni profilo contiene dati aggregati per tutti i sistemi, nonché conti con marca temporale fruibili di eventi che coinvolgono il singolo che si sono verificati in uno dei sistemi con cui utilizzi [!DNL Experience Platform].

[!DNL Real-time Customer Profile] consuma dati in formato schema in base alle [!DNL XDM Individual Profile] [!DNL XDM ExperienceEvent] classi o e risponde alle query basate su tali dati. [!DNL Profile] non supporta l&#39;uso di schemi basati su altre classi.

[!DNL Profile] mantiene un&#39;istanza di ciascun profilo cliente, unendo i dati per formare una &quot;singola origine di verità&quot; per l&#39;individuo. Questi dati unificati vengono rappresentati utilizzando la cosiddetta &quot;visualizzazione unione&quot;. Una vista unione aggrega i campi di tutti gli schemi che implementano la stessa classe in un unico schema.  Quando si compone uno schema utilizzando l&#39;interfaccia utente o l&#39;API, è possibile abilitare lo schema da utilizzare con [!DNL Real-time Customer Profile] e assegnargli un tag da includere nella visualizzazione unione. Lo schema con tag parteciperà quindi alla definizione dello schema a cui viene inviato [!DNL Profile].

Man mano che [!DNL XDM Individual Profile] e dai [!DNL XDM ExperienceEvent] dati vengono acquisiti e gestiti da [!DNL Catalog], viene attivato [!DNL Real-time Customer Profile] l’inizio dell’assimilazione dei dati che sono stati attivati per il loro utilizzo. Più interazioni e dettagli vengono acquisiti, più solidi diventano i profili individuali.

[!DNL XDM Individual Profile] i dati aiutano a informare e a rendere più efficaci le azioni attraverso l&#39;integrazione di soluzioni per canali o  Adobi e, se associati a una ricca cronologia di dati comportamentali e interattivi, questi dati vengono utilizzati per sviluppare l&#39;apprendimento automatico. L&#39; [!DNL Real-time Customer Profile] API può essere utilizzata anche per arricchire le funzionalità di soluzioni di terze parti, CRM e soluzioni proprietarie.

Per ulteriori informazioni, consulta la panoramica [Profilo cliente](../profile/home.md) in tempo reale.

### [!DNL Data Science Workspace]

 Adobe Experience Platform [!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per acquisire informazioni dai dati memorizzati all&#39;interno [!DNL Experience Platform]. [!DNL Data Science Workspace] consente agli esperti informatici di creare ricette basate su XDM Singolo [!DNL Profile] e [!DNL XDM ExperienceEvent] dati sui clienti e sulle loro attività, facilitando previsioni come l&#39;acquisto di propensione e offerte consigliate che l&#39;individuo è probabile apprezzare e utilizzare.

Con [!DNL Data Science Workspace], gli esperti informatici possono creare facilmente API di servizi intelligenti alimentate da machine learning. Questi servizi funzionano con altre soluzioni  Adobi, inclusi  Adobe Target e Adobe Analytics Cloud, per aiutarti a automatizzare esperienze digitali personalizzate e mirate.

Per ulteriori informazioni sull’utilizzo [!DNL Experience Platform] dei dati per fornire informazioni approfondite, consulta la panoramica [di](../data-science-workspace/home.md)Data Science Workspace.

### [!DNL Decisioning Service]

[!DNL Decisioning Service] consente di configurare il processo decisionale personalizzato delle offerte nelle applicazioni [!DNL Platform]integrate. Le offerte possono essere raccomandazioni di prodotto, componenti di contenuto per un&#39;esperienza Web, script di conversazione e azioni da intraprendere.

[!DNL Decisioning Service] sfrutta [!DNL Real-time Customer Profile] i dati ed è pertanto compatibile solo con i set di dati basati su schemi che implementano la [!DNL XDM Individual Profile] classe o [!DNL XDM ExperienceEvent] .

Per ulteriori informazioni, consulta la panoramica [del servizio](../decisioning-service/home.md) Disegno.

## Passaggi successivi e risorse aggiuntive

Ora che capisci meglio il ruolo degli schemi in tutto [!DNL Experience Platform], sei pronto a comporre il tuo. Per continuare a completare l&#39;apprendimento, leggete la documentazione suggerita e guardate il video seguente.

Per apprendere i principi di progettazione e le procedure ottimali per la composizione degli schemi da utilizzare [!DNL Experience Platform], iniziare leggendo le [nozioni di base della composizione](schema/composition.md)dello schema. Per istruzioni dettagliate su come creare uno schema, vedere le esercitazioni sulla creazione di uno schema [mediante l&#39;API](tutorials/create-schema-api.md) o [l&#39;interfaccia](tutorials/create-schema-ui.md)utente.

Per comprendere meglio [!DNL XDM System] in [!DNL Experience Platform], guarda il seguente video:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

