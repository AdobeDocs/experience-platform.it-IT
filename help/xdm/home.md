---
keywords: Experience Platform;home;argomenti popolari;XDM;sistema XDM;profilo individuale XDM;XDM ExperienceEvent;XDM ExperienceEvent;experienceEvent;evento esperienza;mixin;mixin;mixin;evento esperienza;evento esperienza XDM;evento esperienza XDM;evento esperienza;evento esperienza;evento esperienza;XDM Experienceevenet;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati dati;dati Modello;schema di registro;Schema di registro;libreria di schemi;libreria di schemi;schema;record di dati;serie temporali;serie temporali
solution: Experience Platform
title: Panoramica del sistema XDM
topic-legacy: overview
description: La standardizzazione e l'interoperabilità sono concetti chiave alla base di Adobe Experience Platform. Experience Data Model (XDM), basato su un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 0%

---

# Panoramica del sistema XDM

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di Adobe Experience Platform. [!DNL Experience Data Model] (XDM), guidato da un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare il potere delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione da utilizzare per comunicare con i servizi [!DNL Platform]. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che può fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti ed esprimere gli attributi dei clienti a scopo di personalizzazione.

XDM è il framework fondamentale che consente a Adobe Experience Cloud, basato su [!DNL Experience Platform], di inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui è costruito [!DNL Experience Platform], XDM System, rende operativi gli schemi [!DNL Experience Data Model] utilizzabili dai servizi [!DNL Platform].

Questo documento fornisce una panoramica del ruolo del sistema XDM all&#39;interno di [!DNL Experience Platform].

## Schemi XDM

[!DNL Experience Platform] utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i diversi sistemi, diventa più facile mantenere il significato e quindi ottenere valore dai dati.

Prima di poter acquisire i dati in [!DNL Platform], è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che è possibile contenere all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più mixin.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, consulta le [nozioni di base sulla composizione dello schema](schema/composition.md).

### [!DNL Schema Registry] e [!DNL Schema Library]

**[!DNL Schema Registry]** fornisce un&#39;interfaccia utente e RESTful API da cui è possibile visualizzare e gestire tutte le risorse relative allo schema in Adobe Experience Platform **[!DNL Schema Library]**. Il [!DNL Schema Library] contiene risorse standard di settore messe a tua disposizione per Adobe, nonché risorse di [!DNL Experience Platform] partner e fornitori le cui applicazioni utilizzi. L’interfaccia utente e l’API del Registro di sistema dello schema possono inoltre essere utilizzati per creare e gestire nuovi schemi e risorse univoci per la tua organizzazione.

Per una guida completa alle operazioni principali disponibili in [!DNL Schema Registry], consulta la [Guida per gli sviluppatori del Registro di sistema dello schema](api/getting-started.md).

## Comportamenti dei dati nel sistema XDM {#data-behaviors}

I dati destinati a essere utilizzati in [!DNL Experience Platform] sono raggruppati in due tipi di comportamento:

* **Dati** record: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **Dati** delle serie temporali: Fornisce un&#39;istantanea del sistema al momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

Tutti gli schemi XDM descrivono i dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla classe dello schema, che viene assegnata a uno schema quando viene creato per la prima volta. Le classi XDM descrivono il numero minimo di proprietà che uno schema deve contenere per rappresentare un particolare comportamento di dati.

Sebbene sia possibile definire le proprie classi all&#39;interno di [!DNL Schema Registry], si consiglia di utilizzare rispettivamente le classi preferite **[!DNL XDM Individual Profile]** e **[!DNL XDM ExperienceEvent]** per i dati di record e serie temporali. Queste classi sono descritte più dettagliatamente di seguito.

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] è una classe basata su record che forma una singola rappresentazione degli attributi di soggetti identificati e parzialmente identificati. I profili altamente identificati possono essere utilizzati per comunicazioni personali o per impegni mirati e possono contenere informazioni personali dettagliate come nome, genere, data di nascita, ubicazione e informazioni di contatto, compresi i numeri di telefono e gli indirizzi e-mail.

I profili meno identificati possono essere costituiti solo da segnali comportamentali anonimi come i cookie del browser. In questo caso, i dati del profilo sparso vengono utilizzati per creare una base di informazioni in cui gli interessi e le preferenze del profilo anonimo vengono raggruppati e memorizzati. Questi identificatori possono diventare più dettagliati nel tempo in quanto l’oggetto si registra per notifiche, abbonamenti, acquisti e così via. Questo aumento degli attributi del profilo può alla fine dare luogo a un soggetto identificato e consentire un maggiore grado di coinvolgimento mirato.

Man mano che il profilo del consumatore continua a crescere, diventa un solido archivio delle informazioni personali, delle informazioni di identificazione, dei dati di contatto e delle preferenze di comunicazione di un individuo.

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent è una classe basata su serie temporale utilizzata per acquisire lo stato del sistema quando si è verificato un evento (o un set di eventi), incluso il punto nel tempo e l’identità dell’oggetto coinvolto. Gli eventi di esperienza sono registrazioni di fatti di ciò che è accaduto, quindi sono immutabili e rappresentano ciò che è accaduto senza aggregazione o interpretazione. Sono fondamentali per l’analisi del dominio temporale in quanto possono essere utilizzati per analizzare le modifiche che si verificano in una determinata finestra di tempo e per confrontare tra più finestre di tempo per monitorare le tendenze.

Gli eventi di esperienza possono essere espliciti o impliciti. Eventi espliciti sono azioni umane direttamente osservabili che si svolgono durante un punto in un percorso. Gli eventi impliciti sono eventi che vengono sollevati senza un&#39;azione umana diretta, ma che si riferiscono ancora ad un individuo. Esempi di eventi impliciti possono includere l&#39;invio programmato di newsletter via e-mail o tensione della batteria che raggiunge una certa soglia.

Sebbene non tutti gli eventi siano facilmente organizzati in tutte le origini dati, è estremamente utile armonizzare eventi simili in tipi simili, laddove possibile, per l’elaborazione.

![Percorso cliente ExperienceEvent](images/overview/experience-event-journey.png)

## Schemi XDM e servizi [!DNL Experience Platform]

[!DNL Experience Platform] è indipendente dallo schema, il che significa che qualsiasi schema conforme allo standard XDM è disponibile per l’utilizzo da parte  [!DNL Platform] dei servizi. Di seguito sono descritti più dettagliatamente i modi in cui i diversi servizi [!DNL Platform] utilizzano gli schemi.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] è il sistema di registrazione delle  [!DNL Experience Platform] risorse e dei relativi schemi. [!DNL Catalog] non sono i file o le directory effettivi contenenti i dati, ma contengono i metadati e le descrizioni di tali file e directory.

[!DNL Catalog] i dati vengono memorizzati in  [!DNL Data Lake], un archivio dati altamente granulare contenente tutti i dati gestiti da  [!DNL Platform], indipendentemente dall’origine o dal formato del file.

Per iniziare a acquisire i dati in [!DNL Experience Platform], viene creato un set di dati utilizzando [!DNL Catalog Service]. Il set di dati fa riferimento a uno schema XDM che descrive la struttura dei dati da acquisire. Se un set di dati viene creato senza uno schema, [!DNL Experience Platform] deriva uno &quot;schema osservato&quot; controllando il tipo e il contenuto dei campi di dati acquisiti. I set di dati vengono quindi tracciati in [!DNL Catalog] e memorizzati in [!DNL Data Lake] accanto agli schemi e agli schemi osservati su cui si basano.

Per ulteriori informazioni su [!DNL Catalog], consulta la [Panoramica del servizio catalogo](../catalog/home.md). Per ulteriori informazioni sull&#39;acquisizione dei dati da parte di Adobe Experience Platform, consulta la [Panoramica sull&#39;acquisizione dei dati](../ingestion/home.md).

### [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] consente di utilizzare SQL standard per eseguire query sui dati [!DNL Experience Platform] per supportare molti casi d&#39;uso diversi.

Dopo aver composto uno schema e aver creato un set di dati che fa riferimento a tale schema, i dati vengono quindi acquisiti e memorizzati in [!DNL Data Lake]. Utilizzando [!DNL Query Service], puoi unire qualsiasi set di dati in [!DNL Data Lake] e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, nell’apprendimento automatico o per l’acquisizione in [!DNL Real-time Customer Profile].

Per ulteriori informazioni su [!DNL Query Service], consulta l’ [Introduzione al servizio query](../query-service/home.md).

### [!DNL Real-time Customer Profile]

Profilo cliente in tempo reale fornisce un profilo consumatore centralizzato per una gestione delle esperienze mirata e personalizzata. Ogni profilo contiene dati aggregati su tutti i sistemi, nonché account con marca temporale utilizzabili per eventi che coinvolgono l’utente che si sono verificati in uno dei sistemi utilizzati con [!DNL Experience Platform].

[!DNL Real-time Customer Profile] consuma dati formattati in base allo schema in base alle  [!DNL XDM Individual Profile] classi  [!DNL XDM ExperienceEvent] o e risponde alle query basate su tali dati. [!DNL Profile] non supporta l’uso di schemi basati su altre classi.

[!DNL Profile] mantiene un&#39;istanza di ciascun profilo cliente, unendo i dati per formare una &quot;singola fonte di verità&quot; per l&#39;individuo. Questi dati unificati vengono rappresentati utilizzando la cosiddetta &quot;visualizzazione unione&quot;. Una vista unione aggrega i campi di tutti gli schemi che implementano la stessa classe in un unico schema.  Quando si compone uno schema utilizzando l&#39;interfaccia utente o l&#39;API, è possibile abilitare lo schema per l&#39;utilizzo con [!DNL Real-time Customer Profile] e assegnare tag per l&#39;inclusione nella visualizzazione unione. Lo schema con tag parteciperà quindi alla definizione dello schema da inviare a [!DNL Profile].

Poiché i dati [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent] vengono acquisiti e gestiti da [!DNL Catalog], si attiva [!DNL Real-time Customer Profile] per iniziare a acquisire i dati abilitati per l’utilizzo. Più interazioni e dettagli vengono acquisiti, più i profili individuali diventano solidi.

[!DNL XDM Individual Profile] i dati consentono di informare e abilitare le azioni su qualsiasi canale o integrazione di soluzioni di Adobe e, se associati a una ricca cronologia di dati comportamentali e di interazione, questi dati vengono utilizzati per potenziare l&#39;apprendimento automatico. L’ API [!DNL Real-time Customer Profile] può anche essere utilizzata per arricchire le funzionalità di soluzioni di terze parti, CRM e soluzioni proprietarie.

Per ulteriori informazioni, consulta la [Panoramica sul profilo cliente in tempo reale](../profile/home.md) .

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per ottenere informazioni dai dati memorizzati all&#39;interno di [!DNL Experience Platform]. [!DNL Data Science Workspace] consente ai data scientist di creare ricette basate su XDM Individuale  [!DNL Profile] e  [!DNL XDM ExperienceEvent] dati sui clienti e le loro attività, facilitando previsioni come l&#39;acquisto di propensione e offerte raccomandate che l&#39;individuo è probabile apprezzare e utilizzare.

Con [!DNL Data Science Workspace], gli scienziati dei dati possono creare facilmente API di servizi intelligenti basate sull’apprendimento automatico. Questi servizi funzionano con altre soluzioni di Adobe, tra cui Adobe Target e Adobe Analytics Cloud, per aiutarti a automatizzare esperienze digitali personalizzate e mirate.

Per ulteriori informazioni sull&#39;utilizzo dei dati [!DNL Experience Platform] per fornire informazioni approfondite, consulta la [Panoramica di Data Science Workspace](../data-science-workspace/home.md).

## Passaggi successivi e risorse aggiuntive

Ora che hai capito meglio il ruolo degli schemi in [!DNL Experience Platform], sei pronto per iniziare a comporre il tuo. Per continuare a completare il tuo apprendimento, inizia leggendo la documentazione suggerita e guarda il video seguente.

Per scoprire i principi di progettazione e le best practice per la composizione degli schemi da utilizzare con [!DNL Experience Platform], inizia leggendo le [nozioni di base della composizione dello schema](schema/composition.md). Per istruzioni dettagliate su come creare uno schema, consulta le esercitazioni sulla creazione di uno schema [utilizzando l&#39;API](tutorials/create-schema-api.md) o [utilizzando l&#39;interfaccia utente](tutorials/create-schema-ui.md).

Per comprendere meglio [!DNL XDM System] in [!DNL Experience Platform], guarda il seguente video:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
