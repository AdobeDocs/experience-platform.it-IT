---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;grafici XDM
title: Panoramica del profilo cliente in tempo reale
topic-legacy: guide
description: Profilo cliente in tempo reale unisce i dati provenienti da varie fonti e fornisce l’accesso a tali dati sotto forma di profili cliente individuali ed eventi serie temporali correlati. Questa funzione consente agli esperti di marketing di promuovere esperienze coordinate, coerenti e rilevanti con i loro tipi di pubblico su più canali.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: d2182b48e21de059f12ad8923bb3b420ed87bcfc
workflow-type: tm+mt
source-wordcount: '2046'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] panoramica

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con [!DNL Real-time Customer Profile], puoi visualizzare una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente. Questa panoramica ti aiuterà a comprendere il ruolo e l’utilizzo di [!DNL Real-time Customer Profile] in [!DNL Experience Platform].

## [!DNL Profile] in Experience Platform

Il rapporto tra Profilo cliente in tempo reale e altri servizi all’interno di Experience Platform è evidenziato nel diagramma seguente:

![Il rapporto tra Profilo cliente in tempo reale e altri servizi in Adobe Experience Platform. Questo diagramma mostra che Profile è uno dei componenti core di Adobe Experience Platform.](images/profile-overview/profile-in-platform.png)

## Informazioni sui profili

[!DNL Real-time Customer Profile] unisce i dati di diversi sistemi aziendali e fornisce l’accesso a tali dati sotto forma di profili cliente con eventi relativi a serie temporali. Questa funzione consente agli esperti di marketing di promuovere esperienze coordinate, coerenti e rilevanti con i loro tipi di pubblico su più canali. Nelle sezioni seguenti sono evidenziati alcuni dei concetti fondamentali che è necessario comprendere per creare e gestire in modo efficace i profili all’interno di Platform.

### Composizione entità profilo

Un profilo cliente in tempo reale è composto da un&#39;entità principale, denominata **entità principale** e varie entità di supporto. L’entità principale è composta da caratteristiche, comportamenti e appartenenze a segmenti di un profilo. Altre entità consentono al motore di segmentazione di utilizzare dati al di fuori dell’entità primaria del profilo e includono quanto segue:

- **Entità dimensionale**: L’entità utilizzata per semplificare il processo di modellazione dei dati per le informazioni condivise tra eventi o record di profilo. Questa è nota anche come entità di ricerca o di classificazione.
- **Entità B2B**: Entità che descrivono la relazione del profilo con gli account business-to-business e le opportunità.

![Diagramma che illustra la composizione dell’entità profilo.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>Poiché le entità dimensionali e B2B esistono solo al di fuori dell’entità primaria, queste vengono utilizzate solo per la segmentazione batch.

### Archiviazione dati profilo

Nonostante [!DNL Real-time Customer Profile] elabora i dati acquisiti e utilizza Adobe Experience Platform [!DNL Identity Service] per unire i dati correlati tramite la mappatura identità, mantiene i propri dati nel [!DNL Profile] archivio dati. La [!DNL Profile] l&#39;archivio è separato dai dati del catalogo nel data lake e [!DNL Identity Service] nel grafico delle identità.

L’archivio profili utilizza un’infrastruttura del database Cosmos di Microsoft Azure e Platform Data Lake utilizza l’archiviazione Data Lake di Microsoft Azure.

### Guardrail profilo

Experience Platform fornisce una serie di protezioni per evitare di creare [Schemi Experience Data Model (XDM)](../xdm/home.md) Profilo cliente in tempo reale non supportato. Ciò include i limiti soft che si traducono in deterioramento delle prestazioni, nonché i limiti rigidi che si traducono in errori e interruzioni del sistema. Per ulteriori informazioni, tra cui un elenco di linee guida e casi d’uso esemplificativi, consulta il [Guardrail profilo](guardrails.md) documentazione.

### Dashboard dei profili {#profile-dashboard}

L’interfaccia utente di Experience Platform fornisce un dashboard tramite il quale è possibile visualizzare informazioni importanti sui dati del profilo cliente in tempo reale, acquisiti durante un’istantanea giornaliera. Per scoprire come accedere e lavorare con [!DNL Profile] nell’interfaccia utente e informazioni dettagliate sulle metriche visualizzate nel dashboard, consulta [Guida all’interfaccia utente del dashboard del profilo](ui/profile-dashboard.md).

### Frammenti di profilo e profili uniti {#profile-fragments-vs-merged-profiles}

Ogni singolo profilo cliente è composto da più frammenti di profilo che sono stati uniti per formare una singola vista del cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi al singolo cliente che compaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un singolo profilo per quel cliente.

In altre parole, i frammenti di profilo rappresentano un’identità principale univoca e il corrispondente [record](#record-data) o [event](#time-series-events) i dati per quell’ID all’interno di un dato set di dati.

Quando i dati provenienti da più set di dati sono in conflitto (ad esempio, un frammento elenca il cliente come &quot;singolo&quot;, mentre l’altro elenca il cliente come &quot;sposato&quot;) il [criterio di unione](#merge-policies) determina quali informazioni assegnare una priorità e includere nel profilo dell’utente. Pertanto, è probabile che il numero totale di frammenti di profilo all’interno di Platform sia sempre superiore al numero totale di profili uniti, in quanto ogni profilo è in genere composto da più frammenti provenienti da più set di dati.

### Registra dati {#record-data}

Un profilo è una rappresentazione di un soggetto, un’organizzazione o una persona, composta da molti attributi (noti anche come dati di record). Ad esempio, il profilo di un prodotto può includere una SKU e una descrizione, mentre il profilo di una persona contiene informazioni come nome, cognome e indirizzo e-mail. Utilizzo [!DNL Experience Platform], puoi personalizzare i profili in modo da utilizzare dati specifici rilevanti per la tua azienda. Lo standard [!DNL Experience Data Model] Classe (XDM), [!DNL XDM Individual Profile], è la classe preferita da cui creare uno schema per la descrizione dei dati dei record cliente e fornisce i dati integrali a molte interazioni tra i servizi Platform. Per ulteriori informazioni sull’utilizzo degli schemi in [!DNL Experience Platform], per favore inizia leggendo il [Panoramica del sistema XDM](../xdm/home.md).

### Eventi delle serie temporali {#time-series-events}

I dati delle serie temporali forniscono un&#39;istantanea del sistema al momento in cui un soggetto ha agito direttamente o indirettamente, nonché i dati che descrivono l&#39;evento stesso. Rappresentato dalla classe di schema standard XDM ExperienceEvent, i dati delle serie temporali possono descrivere eventi quali elementi aggiunti a un carrello, collegamenti su cui si fa clic e video visualizzati. I dati delle serie temporali possono essere utilizzati per basare le regole di segmentazione su e gli eventi sono accessibili singolarmente nel contesto di un profilo.

### Identità

Ogni azienda vuole comunicare con i propri clienti in un modo che si sente personale. Tuttavia, una delle sfide legate alla fornitura di esperienze digitali rilevanti ai clienti è capire come collegare i dati disconnessi, che spesso si diffondono tra diversi canali digitali come tablet, telefoni cellulari e laptop. [!DNL Identity Service] consente di creare un quadro completo del cliente collegando le identità di più canali e creando un grafico delle identità per ciascun cliente. Visita il [Panoramica del servizio Identity](../identity-service/home.md) per ulteriori informazioni.

### Unisci criteri

Quando si uniscono frammenti di dati da più origini e si combinano per ottenere una visualizzazione completa di ciascuno dei singoli clienti, i criteri di unione sono le regole che [!DNL Platform] utilizza per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno utilizzati per creare il profilo del cliente.

In presenza di dati in conflitto provenienti da più set di dati, il criterio di unione determina il modo in cui tali dati devono essere trattati e il valore da utilizzare. Tramite le API RESTful o l&#39;interfaccia utente è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la propria organizzazione.

Per ulteriori informazioni sui criteri di unione e sul loro ruolo all&#39;interno dell&#39;Experience Platform, si prega di iniziare leggendo il [panoramica dei criteri di unione](merge-policies/overview.md).

### Schemi dell’Unione {#profile-fragments-and-union-schemas}

Una delle caratteristiche principali di [!DNL Real-time Customer Profile] è la capacità di unificare dati multicanale. Quando [!DNL Real-time Customer Profile] viene utilizzato per accedere a un’entità, può fornire una visualizzazione unita di tutti i frammenti di profilo per tale entità tra i set di dati, detta &quot;visualizzazione unione&quot; e resa possibile tramite quello che è noto come schema di unione.

Per ulteriori informazioni sugli schemi di unione, tra cui come accedere agli schemi di unione nell’interfaccia utente, visita il [guida all’interfaccia utente per schema unione](ui/union-schema.md).

### (Alfa) Attributi calcolati

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è in alfa. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati sono funzioni utilizzate per aggregare dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione. Questi calcoli consentono di rispondere facilmente a domande relative a fattori quali il valore di acquisto a vita, il tempo tra gli acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. Per ulteriori informazioni sugli attributi calcolati, compreso il ruolo svolto dagli attributi calcolati in Adobe Experience Platform, si prega di iniziare leggendo il [panoramica degli attributi calcolati](computed-attributes/overview.md).

## Profili e segmenti

Adobe Experience Platform [!DNL Segmentation Service] produce i tipi di pubblico necessari per fornire ai singoli clienti esperienze personalizzate. Quando crei un segmento di pubblico, l’ID di quel segmento viene aggiunto all’elenco delle appartenenze al segmento per tutti i profili qualificati. Le regole del segmento vengono create e applicate a [!DNL Real-time Customer Profile] i dati che utilizzano le API RESTful e l’interfaccia utente di Generatore di segmenti. Per ulteriori informazioni sulla segmentazione, inizia leggendo il [Panoramica del servizio di segmentazione](../segmentation/home.md).

### Acquisizione in streaming e segmentazione in streaming

L’ingresso in tempo reale è possibile tramite un processo chiamato acquisizione in streaming. Quando vengono acquisiti dati di profili e serie temporali, [!DNL Real-time Customer Profile] decide automaticamente di includere o escludere tali dati dai segmenti attraverso un processo continuo denominato segmentazione in streaming, prima di unirli ai dati esistenti e di aggiornare la visualizzazione unione. Di conseguenza, puoi eseguire istantaneamente i calcoli e prendere decisioni per fornire ai clienti esperienze ottimizzate e personalizzate mentre interagiscono con il tuo marchio. Durante l’acquisizione, i dati vengono inoltre convalidati per garantirne il corretto inserimento e la conformità allo schema su cui è basato il set di dati. Per ulteriori informazioni sulle operazioni di convalida durante l’acquisizione, si prega di iniziare leggendo il [panoramica sulla qualità dell’acquisizione dei dati](../ingestion/quality/overview.md).

## Proiezioni del bordo

Al fine di promuovere in tempo reale esperienze coordinate, coerenti e personalizzate per i clienti su più canali, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano cambiamenti. Adobe Experience Platform consente l’accesso in tempo reale ai dati tramite l’utilizzo dei cosiddetti edge. Un server perimetrale è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. Ad Adobe, applicazioni come Adobe Target e Adobe Campaign utilizzano i bordi per offrire esperienze cliente personalizzate in tempo reale. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui i dati saranno inviati, e una configurazione di proiezione che definisce le informazioni specifiche che saranno rese disponibili sul bordo. Per saperne di più e iniziare a lavorare con le proiezioni utilizzando il [!DNL Real-time Customer Profile] API, fai riferimento alla [guida agli endpoint di proiezione edge](api/edge-projections.md).

## Inserimento di dati in [!DNL Profile]

[!DNL Platform] può essere configurato per l&#39;invio di dati di record e serie temporali a [!DNL Profile], che supporta l’acquisizione in streaming in tempo reale e l’acquisizione batch. Per ulteriori informazioni, consulta l’esercitazione su come [aggiungere dati a Profilo cliente in tempo reale](tutorials/add-profile-data.md).

>[!NOTE]
>
>Dati raccolti attraverso soluzioni di Adobe, tra cui [!DNL Analytics Cloud], [!DNL Marketing Cloud]e [!DNL Advertising Cloud], flussi in [!DNL Experience Platform] e viene acquisito in [!DNL Profile].

### Metriche di acquisizione del profilo

Observability Insights consente di esporre le metriche chiave in Adobe Experience Platform. Oltre a [!DNL Experience Platform] statistiche di utilizzo e indicatori di performance per vari [!DNL Platform] funzionalità, esistono metriche specifiche correlate al profilo che ti consentono di ottenere informazioni dettagliate sui tassi di richiesta in arrivo, sui tassi di acquisizione riusciti, sulle dimensioni dei record acquisiti e altro ancora. Per saperne di più, inizia leggendo il [Panoramica API di Observability Insights](../observability/api/overview.md)e per un elenco completo delle metriche Profilo cliente in tempo reale, consulta la documentazione su [metriche disponibili](../observability/api/metrics.md#available-metrics).

## Aggiorna dati archivio profili

A volte può essere necessario aggiornare i dati nell’archivio profili della tua organizzazione. Ad esempio, potrebbe essere necessario correggere i record o modificare un valore di attributo. Questo può essere fatto tramite l’acquisizione batch e richiede un set di dati abilitato per il profilo configurato con un tag upsert. Per ulteriori informazioni su come configurare un set di dati per gli aggiornamenti degli attributi, consulta l’esercitazione per [abilitazione di un set di dati per profilo e aggiornamento](../catalog/datasets/enable-upsert.md).

## Governance dei dati e [!DNL Privacy]

La governance dei dati è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e politiche applicabili all’utilizzo dei dati.

Per quanto riguarda l’accesso ai dati, la governance dei dati svolge un ruolo chiave all’interno di [!DNL Experience Platform] a vari livelli:

- Etichette per l’uso dei dati
- Criteri di accesso ai dati
- Controllo degli accessi ai dati per le azioni di marketing

La governance dei dati è gestita in diversi punti. ad esempio per decidere in quali dati acquisire [!DNL Platform] e quali dati sono accessibili dopo l’acquisizione per una determinata azione di marketing. Per ulteriori informazioni, inizia leggendo il [panoramica sulla governance dei dati](../data-governance/home.md).

### Gestione delle richieste di rinuncia e di privacy dei dati

[!DNL Experience Platform] consente ai clienti di inviare richieste di rinuncia relative all’utilizzo e all’archiviazione dei propri dati all’interno di [!DNL Real-time Customer Profile]. Per ulteriori informazioni sulla gestione delle richieste di rinuncia, consulta la documentazione su [soddisfare le richieste di rinuncia](../segmentation/consents.md).

## Passaggi successivi e risorse aggiuntive

Per ulteriori informazioni sull’utilizzo dei dati del profilo cliente in tempo reale tramite l’interfaccia utente di Experience Platform o l’API di profilo, consulta la sezione [Guida all’interfaccia utente del profilo](ui/user-guide.md) o [Guida per gli sviluppatori API](api/overview.md), rispettivamente.
