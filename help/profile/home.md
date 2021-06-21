---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;grafici XDM
title: Panoramica del profilo cliente in tempo reale
topic-legacy: guide
description: Profilo cliente in tempo reale è un archivio di entità di ricerca generico che unisce i dati da varie risorse di dati aziendali e fornisce l’accesso a tali dati sotto forma di profili cliente individuali ed eventi serie temporali correlati. Questa funzione consente agli esperti di marketing di promuovere esperienze coordinate, coerenti e rilevanti con i loro tipi di pubblico su più canali.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: f193787ac27e30c69d25418656ae9c59c89622dc
workflow-type: tm+mt
source-wordcount: '1813'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile]panoramica

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con [!DNL Real-time Customer Profile] puoi visualizzare una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente. Questa panoramica ti aiuterà a comprendere il ruolo e l’utilizzo di [!DNL Real-time Customer Profile] in [!DNL Experience Platform].

## [!DNL Profile] in Experience Platform

Il rapporto tra Profilo cliente in tempo reale e altri servizi all’interno di Experience Platform è evidenziato nel diagramma seguente:

![](images/profile-overview/profile-in-platform.png)

## Informazioni sui profili

[!DNL Real-time Customer Profile] unisce i dati di diversi sistemi aziendali e fornisce l’accesso a tali dati sotto forma di profili cliente con eventi relativi a serie temporali. Questa funzione consente agli esperti di marketing di promuovere esperienze coordinate, coerenti e rilevanti con i loro tipi di pubblico su più canali. Nelle sezioni seguenti sono evidenziati alcuni dei concetti fondamentali che è necessario comprendere per creare e gestire in modo efficace i profili all’interno di Platform.

### Archiviazione dati profilo

Anche se [!DNL Real-time Customer Profile] elabora i dati acquisiti e utilizza Adobe Experience Platform [!DNL Identity Service] per unire i dati correlati tramite la mappatura dell&#39;identità, mantiene i propri dati nell&#39;archivio dati [!DNL Profile]. L&#39;archivio [!DNL Profile] è separato dai dati del catalogo nel data lake e dai dati [!DNL Identity Service] nel grafico delle identità.

L’archivio profili utilizza un’infrastruttura database Cosmos di Microsoft Azure e Platform Data Lake utilizza l’archiviazione Data Lake di Microsoft Azure.

### Guardrail profilo

Experience Platform fornisce una serie di protezioni per evitare di creare schemi [Experience Data Model (XDM)](../xdm/home.md) che non possono essere supportati dal Profilo cliente in tempo reale. Ciò include i limiti soft che si traducono in deterioramento delle prestazioni, nonché i limiti rigidi che si traducono in errori e interruzioni del sistema. Per ulteriori informazioni, tra cui un elenco di linee guida e casi di utilizzo di esempio, consulta la documentazione [Profile guardrails](guardrails.md) .

### (Beta) Dashboard del profilo {#profile-dashboard}

>[!IMPORTANT]
>
>La funzionalità del dashboard è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

L’interfaccia utente di Experience Platform fornisce un dashboard tramite il quale è possibile visualizzare informazioni importanti sui dati del profilo cliente in tempo reale, acquisiti durante un’istantanea giornaliera. Per informazioni su come accedere e lavorare con il dashboard [!DNL Profile] nell’interfaccia utente e sulle metriche visualizzate nel dashboard, consulta la [Guida all’interfaccia utente del dashboard del profilo](ui/profile-dashboard.md) .

### Frammenti di profilo e profili uniti {#profile-fragments-vs-merged-profiles}

Ogni singolo profilo cliente è composto da più frammenti di profilo che sono stati uniti per formare una singola vista del cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi al singolo cliente che compaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un singolo profilo per quel cliente.

Quando i dati provenienti da più origini sono in conflitto (ad esempio, un frammento elenca il cliente come &quot;singolo&quot;, mentre l&#39;altro elenca il cliente come &quot;sposato&quot;), il [criterio di unione](#merge-policies) determina quali informazioni dare la priorità e includere nel profilo dell&#39;individuo. Pertanto, è probabile che il numero totale di frammenti di profilo all’interno di Platform sia sempre superiore al numero totale di profili uniti, in quanto ogni profilo è composto da più frammenti.

### Registra dati

Un profilo è una rappresentazione di un soggetto, un’organizzazione o una persona, composta da molti attributi (noti anche come dati di record). Ad esempio, il profilo di un prodotto può includere una SKU e una descrizione, mentre il profilo di una persona contiene informazioni come nome, cognome e indirizzo e-mail. Utilizzando [!DNL Experience Platform], puoi personalizzare i profili in modo da utilizzare dati specifici rilevanti per la tua azienda. La classe [!DNL Experience Data Model] (XDM) standard, [!DNL XDM Individual Profile], è la classe preferita da cui creare uno schema per descrivere i dati dei record cliente e fornisce i dati integrali a molte interazioni tra i servizi Platform. Per ulteriori informazioni sull&#39;utilizzo degli schemi in [!DNL Experience Platform], iniziare leggendo la [Panoramica del sistema XDM](../xdm/home.md).

### Eventi delle serie temporali

I dati delle serie temporali forniscono un&#39;istantanea del sistema al momento in cui un soggetto ha agito direttamente o indirettamente, nonché i dati che descrivono l&#39;evento stesso. Rappresentato dalla classe di schema standard XDM ExperienceEvent, i dati delle serie temporali possono descrivere eventi quali elementi aggiunti a un carrello, collegamenti su cui si fa clic e video visualizzati. I dati delle serie temporali possono essere utilizzati per basare le regole di segmentazione su e gli eventi sono accessibili singolarmente nel contesto di un profilo.

### Identità

Ogni azienda vuole comunicare con i propri clienti in un modo che si sente personale. Tuttavia, una delle sfide legate alla fornitura di esperienze digitali rilevanti ai clienti è capire come collegare i dati disconnessi, che spesso si diffondono tra diversi canali digitali come tablet, telefoni cellulari e laptop. [!DNL Identity Service] consente di creare un quadro completo del cliente collegando le identità di più canali e creando un grafico delle identità per ciascun cliente. Per ulteriori informazioni, visita la [panoramica del servizio Identity](../identity-service/home.md) .

### Unisci criteri

Quando si uniscono frammenti di dati da più origini e si combinano per visualizzare una visualizzazione completa di ciascuno dei singoli clienti, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare come assegnare la priorità ai dati e quali saranno i dati utilizzati per creare il profilo cliente.

In presenza di dati in conflitto provenienti da più set di dati, il criterio di unione determina il modo in cui tali dati devono essere trattati e il valore da utilizzare. Tramite le API RESTful o l&#39;interfaccia utente è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la propria organizzazione.

Per ulteriori informazioni sui criteri di unione e sul loro ruolo all&#39;interno dell&#39;Experience Platform, leggere la [panoramica dei criteri di unione](merge-policies/overview.md).

### Schemi dell’Unione {#profile-fragments-and-union-schemas}

Una delle caratteristiche principali di [!DNL Real-time Customer Profile] è la capacità di unificare i dati multicanale. Quando [!DNL Real-time Customer Profile] viene utilizzato per accedere a un’entità, può fornirti una visualizzazione unita di tutti i frammenti di profilo per tale entità nei set di dati, detta &quot;visualizzazione unione&quot;, e resa possibile tramite quello che è noto come schema di unione.

Per ulteriori informazioni sugli schemi di unione, tra cui come accedere agli schemi di unione nell&#39;interfaccia utente, visita la [guida all&#39;interfaccia utente dello schema di unione](ui/union-schema.md).

### (Alfa) Attributi calcolati

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è in alfa. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati sono funzioni utilizzate per aggregare dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione. Questi calcoli consentono di rispondere facilmente a domande relative a fattori quali il valore di acquisto a vita, il tempo tra gli acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. Per ulteriori informazioni sugli attributi calcolati, compreso il ruolo svolto dagli attributi calcolati in Adobe Experience Platform, iniziare leggendo la [panoramica sugli attributi calcolati](computed-attributes/overview.md).

## Profili e segmenti

Adobe Experience Platform [!DNL Segmentation Service] produce i tipi di pubblico necessari per sviluppare esperienze personalizzate per i singoli clienti. Quando crei un segmento di pubblico, l’ID di quel segmento viene aggiunto all’elenco delle appartenenze al segmento per tutti i profili qualificati. Le regole dei segmenti vengono create e applicate ai dati [!DNL Real-time Customer Profile] utilizzando le API RESTful e l’interfaccia utente di Generatore di segmenti. Per ulteriori informazioni sulla segmentazione, inizia leggendo la [Panoramica del servizio di segmentazione](../segmentation/home.md).

### Acquisizione in streaming e segmentazione in streaming

L’ingresso in tempo reale è possibile tramite un processo chiamato acquisizione in streaming. Man mano che i dati relativi a profili e serie temporali vengono acquisiti, [!DNL Real-time Customer Profile] decide automaticamente di includere o escludere tali dati dai segmenti attraverso un processo continuo denominato segmentazione in streaming, prima di unirli ai dati esistenti e di aggiornare la visualizzazione unione. Di conseguenza, puoi eseguire istantaneamente i calcoli e prendere decisioni per fornire ai clienti esperienze ottimizzate e personalizzate mentre interagiscono con il tuo marchio. Durante l’acquisizione, i dati vengono inoltre convalidati per garantirne il corretto inserimento e la conformità allo schema su cui è basato il set di dati. Per ulteriori informazioni sulle operazioni di convalida durante l&#39;acquisizione, leggere la [panoramica sulla qualità dell&#39;acquisizione dei dati](../ingestion/quality/overview.md).

## Proiezioni del bordo

Al fine di promuovere in tempo reale esperienze coordinate, coerenti e personalizzate per i clienti su più canali, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano cambiamenti. Adobe Experience Platform consente l’accesso in tempo reale ai dati tramite l’utilizzo dei cosiddetti edge. Un server perimetrale è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. Ad Adobe, applicazioni come Adobe Target e Adobe Campaign utilizzano i bordi per offrire esperienze cliente personalizzate in tempo reale. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui i dati saranno inviati, e una configurazione di proiezione che definisce le informazioni specifiche che saranno rese disponibili sul bordo. Per ulteriori informazioni e iniziare a lavorare con le proiezioni utilizzando l&#39;API [!DNL Real-time Customer Profile], consulta la [guida agli endpoint di proiezione edge](api/edge-projections.md) .

## Acquisizione di dati in [!DNL Profile]

[!DNL Platform] può essere configurato per inviare dati di record e serie temporali a  [!DNL Profile], supportare l’acquisizione in streaming in tempo reale e l’acquisizione batch. Per ulteriori informazioni, consulta l’esercitazione su come [aggiungere dati al profilo cliente in tempo reale](tutorials/add-profile-data.md).

>[!NOTE]
>
>I dati raccolti attraverso le soluzioni di Adobe, compresi [!DNL Analytics Cloud], [!DNL Marketing Cloud] e [!DNL Advertising Cloud], scorrono in [!DNL Experience Platform] e vengono acquisiti in [!DNL Profile].

### Metriche di acquisizione del profilo

Observability Insights consente di esporre le metriche chiave in Adobe Experience Platform. Oltre alle statistiche di utilizzo e agli indicatori di prestazioni [!DNL Experience Platform] per varie funzionalità [!DNL Platform], sono disponibili metriche specifiche relative al profilo che consentono di ottenere informazioni dettagliate sui tassi di richiesta in arrivo, sui tassi di acquisizione riusciti, sulle dimensioni dei record acquisiti e altro ancora. Per ulteriori informazioni, inizia leggendo la [panoramica API di Registri di osservazione](../observability/api/overview.md) e per un elenco completo delle metriche Profilo cliente in tempo reale, consulta la documentazione sulle [metriche disponibili](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] e [!DNL Privacy]

[!DNL Data governance] è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e politiche applicabili all’utilizzo dei dati.

Per quanto riguarda l’accesso ai dati, la governance dei dati svolge un ruolo chiave all’interno di [!DNL Experience Platform] a vari livelli:
* Etichette per l’uso dei dati
* Criteri di accesso ai dati
* Controllo degli accessi ai dati per le azioni di marketing

[!DNL Data governance] è gestito in diversi punti. tra cui decidere quali dati vengono acquisiti in [!DNL Platform] e quali dati sono accessibili dopo l’acquisizione per una determinata azione di marketing. Per ulteriori informazioni, inizia leggendo la [panoramica sulla governance dei dati](../data-governance/home.md).

### Gestione delle richieste di rinuncia e di privacy dei dati

[!DNL Experience Platform] consente ai clienti di inviare richieste di rinuncia relative all’utilizzo e all’archiviazione dei propri dati all’interno di  [!DNL Real-time Customer Profile]. Per ulteriori informazioni su come vengono gestite le richieste di rinuncia, consulta la documentazione su [onorare le richieste di rinuncia](../segmentation/consents.md).

## Passaggi successivi e risorse aggiuntive

Per ulteriori informazioni sull’utilizzo dei dati [!DNL Real-time Customer Profile] tramite l’interfaccia utente di Experience Platform o l’API di profilo, inizia leggendo rispettivamente la [Guida per gli sviluppatori dell’interfaccia utente di profilo](ui/user-guide.md) o la [Guida per gli sviluppatori API](api/overview.md) .
