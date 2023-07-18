---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;Profilo unificato;unificato;Profilo;rtcp;XDM
title: Panoramica del profilo cliente in tempo reale
description: Real-Time Customer Profile unisce i dati provenienti da varie origini e fornisce l’accesso a tali dati sotto forma di profili dei clienti individuali e di eventi delle serie temporali correlati. Questa funzione consente agli addetti al marketing di promuovere esperienze coordinate, coerenti e rilevanti con i propri tipi di pubblico su più canali.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1990'
ht-degree: 0%

---

# Panoramica di [!DNL Real-Time Customer Profile]

Adobe Experience Platform ti consente di offrire ai tuoi clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con [!DNL Real-Time Customer Profile], puoi avere una visione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente. Questa panoramica ti aiuterà a comprendere il ruolo e l’utilizzo di [!DNL Real-Time Customer Profile] in [!DNL Experience Platform].

## [!DNL Profile] nell’Experience Platform

La relazione tra Real-Time Customer Profile e altri servizi in Experience Platform è evidenziata nel diagramma seguente:

![La relazione tra Real-Time Customer Profile e altri servizi in Adobe Experience Platform. Questo diagramma mostra che Profilo è uno dei componenti principali di Adobe Experience Platform.](images/profile-overview/profile-in-platform.png)

## Informazioni sui profili

[!DNL Real-Time Customer Profile] unisce i dati provenienti da vari sistemi aziendali e quindi fornisce l’accesso a tali dati sotto forma di profili cliente con eventi di serie temporali correlati. Questa funzione consente agli addetti al marketing di promuovere esperienze coordinate, coerenti e rilevanti con i propri tipi di pubblico su più canali. Le sezioni seguenti mettono in evidenza alcuni dei concetti fondamentali che è necessario comprendere per creare e gestire in modo efficace i profili in Platform.

### Composizione entità profilo

Un profilo cliente in tempo reale è composto da un’entità principale, denominata **entità principale** e varie entità di supporto. Nel contesto di un Experience Platform, l’entità principale è in genere un **entità profilo**, composto da caratteristiche, comportamenti e appartenenze a un pubblico di una singola persona. Altre entità consentono al motore di segmentazione di utilizzare dati esterni all’entità principale del profilo e includono quanto segue:

- **Entità dimensionale**: entità utilizzata per semplificare il processo di modellazione dei dati per le informazioni condivise tra eventi o record di profilo. Questa è anche nota come entità di ricerca o entità di classificazione.
- **Entità B2B**: entità che descrivono la relazione del profilo con i conti e le opportunità business-to-business.

![Un diagramma che spiega la composizione dell’entità profilo.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>Poiché le entità dimensionali e B2B esistono solo al di fuori dell’entità principale, vengono utilizzate solo per la segmentazione batch.

Le entità dimensionali e B2B sono collegate all&#39;entità primaria tramite **relazioni tra schemi**. Per ulteriori informazioni, consulta la seguente documentazione:

- [Creare una relazione schema uno-a-uno per le entità di ricerca](../xdm/tutorials/relationship-ui.md)
- [Creare una relazione schema molti-a-uno per le entità B2B](../xdm/tutorials/relationship-b2b.md)

### Archivio dati profilo

Anche se [!DNL Real-Time Customer Profile] elabora i dati acquisiti e utilizza Adobe Experience Platform [!DNL Identity Service] per unire i dati correlati tramite il mapping delle identità, mantiene i propri dati nel [!DNL Profile] archivio dati. Il [!DNL Profile] è separato dai dati del catalogo nel data lake e [!DNL Identity Service] dati nel grafico delle identità.

L’archivio dei profili utilizza un’infrastruttura Microsoft Azure Cosmos DB e Platform Data Lake utilizza l’archiviazione Microsoft Azure Data Lake.

### Guardrail del profilo

Experience Platform fornisce una serie di guardrail per evitare la creazione di [Schemi Experience Data Model (XDM)](../xdm/home.md) che Real-Time Customer Profile non può supportare. Questo include limiti programmati che determineranno un deterioramento delle prestazioni e limiti rigidi che determineranno errori e interruzioni del sistema. Per ulteriori informazioni, tra cui un elenco di linee guida e casi d’uso di esempio, consulta [Guardrail del profilo](guardrails.md) documentazione.

### Dashboard dei profili {#profile-dashboard}

L’interfaccia utente di Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui dati del Profilo cliente in tempo reale, acquisiti durante un’istantanea giornaliera. Per scoprire come accedere e utilizzare [!DNL Profile] nell&#39;interfaccia utente e informazioni dettagliate sulle metriche visualizzate nel dashboard, fai riferimento alla [Guida dell’interfaccia utente della dashboard del profilo](ui/profile-dashboard.md).

### Frammenti di profilo e profili uniti {#profile-fragments-vs-merged-profiles}

Ogni singolo profilo cliente è composto da più frammenti di profilo che sono stati uniti per formare un’unica vista di quel cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi a quel singolo cliente che appaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un unico profilo per quel cliente.

In altre parole, i frammenti di profilo rappresentano un’identità primaria univoca e la corrispondente [record](#record-data) o [evento](#time-series-events) dati per quell’ID all’interno di un dato set di dati.

Quando i dati di più set di dati sono in conflitto (ad esempio, un frammento elenca il cliente come &quot;singolo&quot; mentre l’altro lo elenca come &quot;sposato&quot;), la [criterio di unione](#merge-policies) determina quali informazioni assegnare la priorità e includere nel profilo per il singolo utente. Pertanto, è probabile che il numero totale di frammenti di profilo in Platform sia sempre superiore al numero totale di profili uniti, in quanto ogni profilo è in genere composto da più frammenti provenienti da più set di dati.

### Registra dati {#record-data}

Un profilo è una rappresentazione di un soggetto, un’organizzazione o un individuo, composta da molti attributi (noti anche come dati record). Ad esempio, il profilo di un prodotto può includere uno SKU e una descrizione, mentre il profilo di una persona contiene informazioni come nome, cognome e indirizzo e-mail. Utilizzo di [!DNL Experience Platform], puoi personalizzare i profili in modo da utilizzare dati specifici rilevanti per la tua azienda. Lo standard [!DNL Experience Data Model] classe (XDM), [!DNL XDM Individual Profile], è la classe preferita su cui creare uno schema quando si descrivono i dati dei record dei clienti e fornisce i dati integrati in molte interazioni tra i servizi di Platform. Per ulteriori informazioni sull’utilizzo degli schemi in [!DNL Experience Platform], iniziare leggendo il [Panoramica del sistema XDM](../xdm/home.md).

### Eventi di serie temporali {#time-series-events}

I dati della serie temporale forniscono un’istantanea del sistema nel momento in cui un soggetto ha intrapreso un’azione, direttamente o indirettamente, nonché i dati che descrivono l’evento stesso. Rappresentati dalla classe di schema standard XDM ExperienceEvent, i dati delle serie temporali possono descrivere eventi come elementi aggiunti a un carrello, collegamenti su cui si fa clic e video visualizzati. I dati delle serie temporali possono essere utilizzati per basare le regole di segmentazione su e gli eventi sono accessibili singolarmente nel contesto di un profilo.

### Identità

Ogni azienda vuole comunicare con i propri clienti in modo che sia personale. Tuttavia, una delle sfide per offrire esperienze digitali rilevanti ai clienti è capire come collegare i loro dati disconnessi, che spesso è diffuso su diversi canali digitali come tablet, telefoni cellulari e laptop. [!DNL Identity Service] consente di creare un quadro completo del cliente collegando le identità da più canali e creando un grafico delle identità per ciascun cliente. Visita il [Panoramica del servizio Identity](../identity-service/home.md) per ulteriori informazioni.

### Criteri di unione

Quando riunisci frammenti di dati da più origini e li combini per ottenere una visione completa di ciascuno dei singoli clienti, i criteri di unione sono le regole che [!DNL Platform] utilizza per determinare come assegnare la priorità ai dati e quali dati verranno utilizzati per creare il profilo cliente.

In caso di dati in conflitto da più set di dati, il criterio di unione determina il modo in cui tali dati devono essere trattati e quale valore deve essere utilizzato. Tramite le API RESTful o l’interfaccia utente di, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione.

Per ulteriori informazioni sui criteri di unione e sul loro ruolo nell’Experience Platform, consulta la sezione [panoramica dei criteri di unione](merge-policies/overview.md).

### Schemi di unione {#profile-fragments-and-union-schemas}

Una delle caratteristiche principali di [!DNL Real-Time Customer Profile] è la capacità di unificare dati multicanale. Quando [!DNL Real-Time Customer Profile] viene utilizzato per accedere a un’entità, può fornirti una vista unita di tutti i frammenti di profilo per tale entità nei diversi set di dati, denominata &quot;vista unione&quot; e resa possibile tramite quello che viene definito uno schema di unione.

Per ulteriori informazioni sugli schemi unione, tra cui come accedere agli schemi unione nell’interfaccia utente, visita [guida dell’interfaccia utente per lo schema di unione](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## Profili e pubblico

Adobe Experience Platform [!DNL Segmentation Service] produce i tipi di pubblico necessari per fornire esperienze ai singoli clienti. Quando viene creato un pubblico, l’ID di tale pubblico viene aggiunto all’elenco delle appartenenze del pubblico per tutti i profili idonei. Le regole del segmento vengono generate e applicate a [!DNL Real-Time Customer Profile] dati utilizzando le API RESTful e l’interfaccia utente di Segment Builder. Per ulteriori informazioni sulla segmentazione, consulta la sezione [Panoramica del servizio di segmentazione](../segmentation/home.md).

### Acquisizione e segmentazione in streaming

L’input in tempo reale è possibile tramite un processo denominato acquisizione in streaming. Al momento dell’acquisizione dei dati di profilo e serie temporali, [!DNL Real-Time Customer Profile] decide automaticamente di includere o escludere tali dati dai tipi di pubblico tramite un processo continuo denominato segmentazione in streaming, prima di unirli ai dati esistenti e di aggiornare la visualizzazione unione. Di conseguenza, puoi eseguire istantaneamente i calcoli e prendere decisioni per fornire esperienze avanzate e personalizzate ai clienti mentre interagiscono con il tuo marchio. Durante l’acquisizione, i dati vengono sottoposti anche a convalida per garantirne la corretta acquisizione e la conformità allo schema su cui si basa il set di dati. Per ulteriori informazioni sulla convalida eseguita durante l’acquisizione, leggi [panoramica sulla qualità dell’acquisizione dei dati](../ingestion/quality/overview.md).

## Proiezioni spigolo

Per fornire ai clienti esperienze coordinate, coerenti e personalizzate in tempo reale su più canali, i dati giusti devono essere prontamente disponibili e continuamente aggiornati in base alle modifiche apportate. Adobe Experience Platform consente questo accesso in tempo reale ai dati tramite l’utilizzo dei cosiddetti edge. Un server perimetrale è un server posizionato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. Ad Adobe, applicazioni come Adobe Target e Adobe Campaign utilizzano Edge per fornire ai clienti esperienze personalizzate in tempo reale. I dati vengono instradati a uno spigolo da una proiezione, con una destinazione di proiezione che definisce lo spigolo a cui verranno inviati i dati e una configurazione di proiezione che definisce le informazioni specifiche che saranno rese disponibili sullo spigolo. Per ulteriori informazioni e iniziare a utilizzare le proiezioni utilizzando [!DNL Real-Time Customer Profile] API, fai riferimento alla [guida degli endpoint di proiezione edge](api/edge-projections.md).

## Acquisizione di dati in [!DNL Profile]

[!DNL Platform] può essere configurato per inviare dati di record e serie temporali a [!DNL Profile], che supporta l’acquisizione in streaming in tempo reale e l’acquisizione in batch. Per ulteriori informazioni, consulta il tutorial che illustra come [aggiungere dati a Real-Time Customer Profile](tutorials/add-profile-data.md).

>[!NOTE]
>
>Dati raccolti tramite soluzioni Adobe, tra cui [!DNL Analytics Cloud], [!DNL Marketing Cloud], e [!DNL Advertising Cloud], fluisce in [!DNL Experience Platform] e viene acquisito in [!DNL Profile].

### Metriche di acquisizione del profilo

Observability Insights consente di esporre le metriche chiave in Adobe Experience Platform. Oltre a [!DNL Experience Platform] statistiche di utilizzo e indicatori di prestazioni per vari [!DNL Platform] funzionalità, esistono metriche specifiche relative al profilo che ti consentono di ottenere informazioni approfondite sulle percentuali di richieste in arrivo, sulle percentuali di acquisizione corrette, sulle dimensioni dei record acquisiti e altro ancora. Per ulteriori informazioni, consulta [Panoramica API di Observability Insights](../observability/api/overview.md), e per un elenco completo delle metriche del profilo cliente in tempo reale, consulta la documentazione su [metriche disponibili](../observability/api/metrics.md#available-metrics).

## Aggiorna dati archivio profili

A volte può essere necessario aggiornare i dati nell’archivio profili della tua organizzazione. Ad esempio, potrebbe essere necessario correggere i record o modificare un valore di attributo. Questa operazione può essere eseguita tramite l’acquisizione in batch e richiede un set di dati abilitato per il profilo configurato con un tag upsert. Per ulteriori informazioni su come configurare un set di dati per gli aggiornamenti degli attributi, consulta l’esercitazione per [abilitazione di un set di dati per Profilo e upsert](../catalog/datasets/enable-upsert.md).

## Governance dei dati e [!DNL Privacy]

La governance dei dati è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati.

In quanto riguarda l’accesso ai dati, la governance dei dati svolge un ruolo chiave nell’ambito di [!DNL Experience Platform] a vari livelli:

- Etichetta di utilizzo dei dati
- Criteri di accesso ai dati
- Controllo dell’accesso ai dati per le azioni di marketing

La governance dei dati viene gestita in diversi punti. Questi includono la decisione in quali dati vengono acquisiti [!DNL Platform] e quali dati sono accessibili dopo l’acquisizione per una determinata azione di marketing. Per ulteriori informazioni, consulta [panoramica sulla governance dei dati](../data-governance/home.md).

### Gestione delle richieste di rinuncia e di privacy dei dati

[!DNL Experience Platform] consente ai clienti di inviare richieste di rinuncia relative all’utilizzo e all’archiviazione dei propri dati in [!DNL Real-Time Customer Profile]. Per ulteriori informazioni sulla gestione delle richieste di rinuncia, consulta la documentazione su [rispetto delle richieste di rinuncia](../segmentation/consents.md).

## Passaggi successivi e risorse aggiuntive

Per ulteriori informazioni sull’utilizzo dei dati del Profilo cliente in tempo reale tramite l’interfaccia utente di Experience Platform o l’API del Profilo, consulta la sezione [Guida all’interfaccia utente del profilo](ui/user-guide.md) o [Guida per gli sviluppatori API](api/overview.md), rispettivamente.
