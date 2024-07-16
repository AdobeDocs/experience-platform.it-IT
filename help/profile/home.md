---
title: Panoramica del profilo cliente in tempo reale
description: Real-Time Customer Profile unisce i dati provenienti da varie origini e fornisce l’accesso a tali dati sotto forma di profili dei clienti individuali e di eventi delle serie temporali correlati. Questa funzione consente agli addetti al marketing di promuovere esperienze coordinate, coerenti e rilevanti con i propri tipi di pubblico su più canali.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 1%

---

# Panoramica di [!DNL Real-Time Customer Profile]

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con [!DNL Real-Time Customer Profile] è possibile visualizzare una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente. Questa panoramica consente di comprendere il ruolo e l&#39;utilizzo di [!DNL Real-Time Customer Profile] in [!DNL Experience Platform].

## [!DNL Profile] in Experience Platform

La relazione tra Real-Time Customer Profile e altri servizi in Experience Platform è evidenziata nel diagramma seguente:

![Relazione tra Real-Time Customer Profile e altri servizi in Adobe Experience Platform. Questo diagramma mostra che il profilo è uno dei componenti principali di Adobe Experience Platform.](images/profile-overview/profile-in-platform.png)

## Informazioni sui profili

[!DNL Real-Time Customer Profile] unisce i dati di vari sistemi aziendali e fornisce l&#39;accesso a tali dati sotto forma di profili cliente con eventi di serie temporali correlati. Questa funzione consente agli addetti al marketing di promuovere esperienze coordinate, coerenti e rilevanti con i propri tipi di pubblico su più canali. Le sezioni seguenti mettono in evidenza alcuni dei concetti fondamentali che è necessario comprendere per creare e gestire in modo efficace i profili in Platform.

### Composizione entità profilo

Un profilo cliente in tempo reale è composto da un&#39;entità principale, denominata **entità principale**, e da varie entità di supporto. Nel contesto di Experience Platform, l&#39;entità primaria è in genere un&#39;entità **profilo**, composta da caratteristiche, comportamenti e appartenenze di pubblico di una singola persona. Altre entità consentono al motore di segmentazione di utilizzare dati esterni all’entità principale del profilo e includono quanto segue:

- **Entità dimensionale**: entità utilizzata per semplificare il processo di modellazione dei dati per le informazioni condivise tra eventi o record di profilo. Questa è anche nota come entità di ricerca o entità di classificazione.
- **Entità B2B**: entità che descrivono la relazione del profilo con account e opportunità business-to-business.

![Diagramma che illustra la composizione dell&#39;entità profilo.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>Poiché le entità dimensionali e B2B esistono solo al di fuori dell’entità principale, vengono utilizzate solo per la segmentazione batch.

Le entità dimensionali e B2B sono collegate all&#39;entità primaria tramite **relazioni schema**. Per ulteriori informazioni, consulta la seguente documentazione:

- [Creare una relazione schema uno-a-uno per le entità di ricerca](../xdm/tutorials/relationship-ui.md)
- [Creare una relazione schema molti-a-uno per le entità B2B](../xdm/tutorials/relationship-b2b.md)

### Archivio dati profilo

Sebbene [!DNL Real-Time Customer Profile] elabori i dati acquisiti e utilizzi Adobe Experience Platform [!DNL Identity Service] per unire i dati correlati tramite il mapping delle identità, mantiene i propri dati nell&#39;archivio dati [!DNL Profile]. L&#39;archivio [!DNL Profile] è separato dai dati del catalogo nel data lake e dai dati [!DNL Identity Service] nel grafico delle identità.

L’archivio dei profili utilizza un’infrastruttura Microsoft Azure Cosmos DB e Platform Data Lake utilizza l’archiviazione Microsoft Azure Data Lake.

### Guardrail del profilo

L&#39;Experience Platform fornisce una serie di guardrail che consentono di evitare la creazione di [schemi Experience Data Model (XDM)](../xdm/home.md) che Real-Time Customer Profile non è in grado di supportare. Questo include limiti programmati che determineranno un deterioramento delle prestazioni e limiti rigidi che determineranno errori e interruzioni del sistema. Per ulteriori informazioni, tra cui un elenco di linee guida e casi d&#39;uso di esempio, consulta la documentazione di [Guardrail del profilo](guardrails.md).

### Dashboard profili {#profile-dashboard}

L’interfaccia utente di Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui dati del Profilo cliente in tempo reale, acquisiti durante un’istantanea giornaliera. Per informazioni su come accedere e utilizzare il dashboard [!DNL Profile] nell&#39;interfaccia utente e informazioni dettagliate sulle metriche visualizzate nel dashboard, fare riferimento alla [Guida dell&#39;interfaccia utente del dashboard del profilo](ui/profile-dashboard.md).

### Frammenti di profilo e profili uniti {#profile-fragments-vs-merged-profiles}

Ogni singolo profilo cliente è composto da più frammenti di profilo che sono stati uniti per formare un’unica vista di quel cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi a quel singolo cliente che appaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un unico profilo per quel cliente.

In altre parole, i frammenti di profilo rappresentano un&#39;identità primaria univoca e i dati [record](#record-data) o [event](#time-series-events) corrispondenti per tale ID all&#39;interno di un set di dati specificato.

Quando i dati di più set di dati sono in conflitto (ad esempio, un frammento elenca il cliente come &quot;singolo&quot;, mentre l&#39;altro lo elenca come &quot;sposato&quot;) il [criterio di unione](#merge-policies) determina quali informazioni assegnare la priorità e includere nel profilo dell&#39;utente. Pertanto, è probabile che il numero totale di frammenti di profilo in Platform sia sempre superiore al numero totale di profili uniti, in quanto ogni profilo è in genere composto da più frammenti provenienti da più set di dati.

### Registra dati {#record-data}

Un profilo è una rappresentazione di un soggetto, un’organizzazione o un individuo, composta da molti attributi (noti anche come dati record). Ad esempio, il profilo di un prodotto può includere uno SKU e una descrizione, mentre il profilo di una persona contiene informazioni come nome, cognome e indirizzo e-mail. Utilizzando [!DNL Experience Platform], puoi personalizzare i profili in modo da utilizzare dati specifici rilevanti per la tua azienda. La classe standard [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], è la classe preferita su cui creare uno schema quando si descrivono i dati dei record dei clienti e fornisce i dati integrali a molte interazioni tra i servizi Platform. Per ulteriori informazioni sull&#39;utilizzo degli schemi in [!DNL Experience Platform], leggere la [Panoramica del sistema XDM](../xdm/home.md).

### Eventi di serie temporali {#time-series-events}

I dati della serie temporale forniscono un’istantanea del sistema nel momento in cui un soggetto ha intrapreso un’azione, direttamente o indirettamente, nonché i dati che descrivono l’evento stesso. Rappresentati dalla classe di schema standard XDM ExperienceEvent, i dati delle serie temporali possono descrivere eventi come elementi aggiunti a un carrello, collegamenti su cui si fa clic e video visualizzati. I dati delle serie temporali possono essere utilizzati per basare le regole di segmentazione su e gli eventi sono accessibili singolarmente nel contesto di un profilo.

### Identità

Ogni azienda vuole comunicare con i propri clienti in modo che sia personale. Tuttavia, una delle sfide per offrire esperienze digitali rilevanti ai clienti è capire come collegare i loro dati disconnessi, che spesso è diffuso su diversi canali digitali come tablet, telefoni cellulari e laptop. [!DNL Identity Service] consente di mettere insieme il quadro completo del cliente collegando identità da più canali e creando un grafico delle identità per ciascun cliente. Per ulteriori informazioni, visita la [panoramica del servizio Identity](../identity-service/home.md).

### Criteri di unione

Quando si riuniscono frammenti di dati da più origini e li si combina per ottenere una visualizzazione completa di ciascuno dei singoli clienti, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare la priorità dei dati e i dati che verranno utilizzati per creare il profilo cliente.

In caso di dati in conflitto da più set di dati, il criterio di unione determina il modo in cui tali dati devono essere trattati e quale valore deve essere utilizzato. Tramite le API RESTful o l’interfaccia utente di, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione.

Per ulteriori informazioni sui criteri di unione e sul loro ruolo in Experience Platform, consulta la [panoramica dei criteri di unione](merge-policies/overview.md).

### Schemi di unione {#profile-fragments-and-union-schemas}

Una delle caratteristiche principali di [!DNL Real-Time Customer Profile] è la capacità di unificare dati multicanale. Quando [!DNL Real-Time Customer Profile] viene utilizzato per accedere a un&#39;entità, può fornire una vista unita di tutti i frammenti di profilo per tale entità nei set di dati, denominata &quot;vista unione&quot; e resa possibile tramite quello che è noto come schema di unione.

Per ulteriori informazioni sugli schemi di unione, tra cui come accedere agli schemi di unione nell&#39;interfaccia utente, consulta la [guida dell&#39;interfaccia utente dello schema di unione](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## Profili e pubblico

Adobe Experience Platform [!DNL Segmentation Service] produce i tipi di pubblico necessari per fornire esperienze ai singoli clienti. Quando viene creato un pubblico, l’ID di tale pubblico viene aggiunto all’elenco delle appartenenze del pubblico per tutti i profili idonei. Le regole dei segmenti vengono create e applicate ai dati [!DNL Real-Time Customer Profile] utilizzando le API RESTful e l&#39;interfaccia utente di Segment Builder. Per ulteriori informazioni sulla segmentazione, consulta la [Panoramica del servizio di segmentazione](../segmentation/home.md).

### Acquisizione e segmentazione in streaming

L’input in tempo reale è possibile tramite un processo denominato acquisizione in streaming. Al momento dell&#39;acquisizione dei dati di profilo e serie temporali, [!DNL Real-Time Customer Profile] decide automaticamente di includere o escludere tali dati dai tipi di pubblico tramite un processo continuo denominato segmentazione in streaming, prima di unirli ai dati esistenti e di aggiornare la visualizzazione unione. Di conseguenza, puoi eseguire istantaneamente i calcoli e prendere decisioni per fornire esperienze avanzate e personalizzate ai clienti mentre interagiscono con il tuo marchio. Durante l’acquisizione, i dati vengono sottoposti anche a convalida per garantirne la corretta acquisizione e la conformità allo schema su cui si basa il set di dati. Per ulteriori informazioni sulla convalida eseguita durante l&#39;acquisizione, consulta la [panoramica sulla qualità dell&#39;acquisizione dei dati](../ingestion/quality/overview.md).

## Acquisizione di dati in [!DNL Profile]

[!DNL Platform] può essere configurato per inviare dati di record e serie temporali a [!DNL Profile], supportando l&#39;acquisizione in streaming in tempo reale e l&#39;acquisizione in batch. Per ulteriori informazioni, vedere l&#39;esercitazione che illustra come [aggiungere dati al profilo cliente in tempo reale](tutorials/add-profile-data.md).

>[!NOTE]
>
>I dati raccolti tramite le soluzioni Adobe, tra cui [!DNL Analytics Cloud], [!DNL Marketing Cloud] e [!DNL Advertising Cloud], fluiscono in [!DNL Experience Platform] e vengono acquisiti in [!DNL Profile].

### Metriche di acquisizione del profilo

Observability Insights consente di esporre le metriche chiave in Adobe Experience Platform. Oltre alle statistiche sull&#39;utilizzo di [!DNL Experience Platform] e agli indicatori di prestazioni per varie funzionalità di [!DNL Platform], sono disponibili metriche specifiche relative al profilo che consentono di ottenere informazioni sulle percentuali di richieste in arrivo, sulle percentuali di acquisizione riuscite, sulle dimensioni dei record acquisiti e altro ancora. Per ulteriori informazioni, consulta la [panoramica API Observability Insights](../observability/api/overview.md). Per un elenco completo delle metriche del profilo cliente in tempo reale, consulta la documentazione sulle [metriche disponibili](../observability/api/metrics.md#available-metrics).

## Aggiorna dati archivio profili

A volte può essere necessario aggiornare i dati nell’archivio profili della tua organizzazione. Ad esempio, potrebbe essere necessario correggere i record o modificare un valore di attributo. Questa operazione può essere eseguita tramite l’acquisizione in batch e richiede un set di dati abilitato per il profilo configurato con un tag upsert. Per ulteriori informazioni su come configurare un set di dati per gli aggiornamenti degli attributi, consulta l&#39;esercitazione per [abilitare un set di dati per Profilo e upsert](../catalog/datasets/enable-upsert.md).

## Governance dei dati e [!DNL Privacy]

La governance dei dati è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati.

Per quanto riguarda l&#39;accesso ai dati, la governance dei dati svolge un ruolo chiave all&#39;interno di [!DNL Experience Platform] a vari livelli:

- Etichetta di utilizzo dei dati
- Criteri di accesso ai dati
- Controllo dell’accesso ai dati per le azioni di marketing

La governance dei dati viene gestita in diversi punti. Queste includono la decisione di quali dati vengono acquisiti in [!DNL Platform] e quali dati sono accessibili dopo l&#39;acquisizione per una determinata azione di marketing. Per ulteriori informazioni, leggere la [panoramica sulla governance dei dati](../data-governance/home.md).

### Gestione delle richieste di rinuncia e di privacy dei dati

[!DNL Experience Platform] consente ai clienti di inviare richieste di rinuncia relative all&#39;utilizzo e all&#39;archiviazione dei dati in [!DNL Real-Time Customer Profile]. Per ulteriori informazioni sulla gestione delle richieste di rinuncia, consulta la documentazione su [rispetto delle richieste di rinuncia](../segmentation/consents.md).

## Passaggi successivi e risorse aggiuntive

Per ulteriori informazioni sull&#39;utilizzo dei dati del profilo cliente in tempo reale tramite l&#39;interfaccia utente di Experience Platform o l&#39;API del profilo, leggere la [Guida dell&#39;interfaccia utente del profilo](ui/user-guide.md) o la [Guida per gli sviluppatori API](api/overview.md).
