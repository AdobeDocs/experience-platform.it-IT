---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2024
description: Note sulla versione di Adobe Experience Platform di gennaio 2024.
exl-id: d4b3c5b2-3adb-41fd-91ad-f4c0f21d2325
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: ht
source-wordcount: '1659'
ht-degree: 100%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 30 gennaio 2024**

Nuove funzioni di Adobe Experience Platform:

- [Playbook di casi d’uso](#use-case-playbooks)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Controllo degli accessi basato su attributi](#abac)
- [Preparazione dei dati](#data-prep)
- [Dashboard](#dashboards)
- [Destinazioni](#destinations)
- [Identity Service](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [Profilo cliente in tempo reale](#profile)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Playbook di casi d’uso {#use-case-playbooks}

La funzionalità [!UICONTROL Playbook di casi d’uso] è ora disponibile per tutti i clienti Real-Time CDP e Adobe Journey Optimizer. I [!UICONTROL playbook di casi d’uso] sono progettati per aiutare gli utenti a superare eventuali difficoltà quando iniziano a utilizzare Real-time Customer Data Platform o Adobe Journey Optimizer. Quando non sai da dove iniziare o come creare le risorse giuste per i casi d’uso desiderati, i playbook di casi d’uso possono fornirti l’ispirazione e creare diverse risorse da testare e importare negli ambienti di produzione quando sono pronti.

Per iniziare a utilizzare i [!UICONTROL playbook di casi d’uso], leggi le seguenti pagine della documentazione:

- Leggi la [pagina di panoramica](/help/use-case-playbooks/playbooks/overview.md) per comprendere lo scopo, le informazioni sulla disponibilità e per ottenere una dimostrazione completa del funzionamento dei playbook, dall’individuazione alla creazione di istanze, fino all’importazione di risorse generate in altri ambienti sandbox.
- Ottieni un elenco di tutti i [playbook disponibili](/help/use-case-playbooks/playbooks/playbooks-list.md), raggruppati per prodotto (Real-Time CDP o Journey Optimizer)
- Ottieni informazioni su tutte le [autorizzazioni necessarie](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) per utilizzare i playbook e le risorse generate dai playbook.
- Comprendere la [funzionalità di riconoscimento dei dati](/help/use-case-playbooks/playbooks/data-awareness.md) che consente di copiare le risorse generate in altri ambienti sandbox
- Ottieni [suggerimenti per la risoluzione dei problemi](/help/use-case-playbooks/playbooks/troubleshooting.md) in caso di errori o difficoltà durante l’utilizzo dei playbook di casi d’uso.

## Controllo degli accessi basato su attributi {#abac}

Il controllo degli accessi basato sugli attributi è una funzionalità di Adobe Experience Platform che offre ai brand attenti alla privacy una maggiore flessibilità per gestire l’accesso degli utenti. È possibile assegnare singoli oggetti, come campi e segmenti dello schema, ai ruoli utente. Questa funzione consente di concedere o revocare l’accesso a singoli oggetti per specifici utenti di Platform nell’organizzazione.

Tramite il controllo dell’accesso basato su attributi, gli amministratori dell’organizzazione possono controllare l’accesso degli utenti a dati personali sensibili (SPD), informazioni personali (PII) e altri tipi di dati personalizzati in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici che corrispondono a tali campi.

**Documentazione nuova o aggiornata**

| Aggiornamento della documentazione | Descrizione |
| --- | --- |
| Documentazione dei nuovi endpoint API per il controllo degli accessi basato su attributi | La [documentazione di riferimento API per il controllo degli accessi](https://developer.adobe.com/experience-platform-apis/references/access-control/) ora include ruoli API per il controllo degli accessi basati su attributi, criteri ed endpoint di prodotto. Questi endpoint possono essere utilizzati per recuperare ruoli, criteri e prodotti rilevanti per un utente su determinate risorse in una sandbox specifica. |

{style="table-layout:auto"}

Per ulteriori informazioni sul controllo degli accessi basato su attributi, consulta la [panoramica sul controllo degli accessi basato su attributi](../../access-control/abac/overview.md). Per una guida completa sul flusso di lavoro del controllo degli accessi basato su attributi, leggi la [guida completa per il controllo degli accessi basato su attributi](../../access-control/abac/end-to-end-guide.md).

## Preparazione dei dati {#data-prep}

La preparazione dei dati consente ai data engineer di mappare, trasformare e convalidare i dati da e per Experience Data Model (XDM).

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove funzioni di mappatura | <ul><li>`object_to_map`: utilizza la funzione `object_to_map` per creare tipi di dati di mappatura. Questa funzione supporta diverse sintassi. Per ulteriori informazioni, leggi la guida sulle [funzioni per gerarchie - oggetti](../../data-prep/functions.md#objects). </li><li>`to_map`: utilizza la funzione `to_map` per creare una mappa con coppie di nomi di campi e valori specificati utilizzando gli oggetti. Per ulteriori informazioni, leggi la guida sulle [funzioni per gerarchie - mappe](../../data-prep/functions.md#map). </li><li>`array_to_map`: utilizza la funzione `array_to_map` per creare una mappa con coppie di nomi di campi e valori specificati utilizzando array di oggetti. Per ulteriori informazioni, leggi la guida su [funzioni per gerarchie - mappe](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Per ulteriori informazioni sulla preparazione dati, leggi la [panoramica sulla preparazione dei dati](../../data-prep/home.md).

## Dashboard {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Visualizza SQL | Ora puoi visualizzare le istruzioni SQL sottostanti i profili, i tipi di pubblico, le destinazioni e le informazioni personalizzate con l’interruttore Visualizza SQL, quindi eseguire la query su richiesta tramite l’editor di query. L’accesso a SQL che alimenta le informazioni di Real-time Customer Data Platform consente di comprendere la logica alla base dell’analisi del modello dati. Questa trasparenza rende i dati Real-time CDP di Adobe più accessibili, comprensibili e di impatto per il processo decisionale.<br>Puoi trarre spunto dal codice SQL di oltre 40 insight esistenti per creare nuove query e ottenere informazioni esclusive dai dati di Platform in base alle tue specifiche esigenze di business. SQL è disponibile anche per gli approfondimenti su [Profili](../../dashboards/insights/profiles.md), [Tipi di pubblico](../../dashboards/insights/audiences.md) e [Destinazioni](../../dashboards/insights/destinations.md) nella documentazione di Experience League. Questi documenti evidenziano i casi d’uso aziendali a cui è possibile rispondere con gli approfondimenti standard. Per ulteriori informazioni, leggi la guida sulla [visualizzazione di approfondimenti SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni** {#new-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [Connessione pubmatic](../../destinations/catalog/advertising/pubmatic.md) | Utilizzare questa destinazione per inviare i dati del pubblico alla piattaforma [!DNL PubMatic Connect]. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Nuovo tipo di autenticazione del **ruolo presunto** per le destinazioni Amazon S3 | Utilizza il nuovo tipo di autenticazione del ruolo presunto per collegare Experience Platform ai bucket Amazon S3 se non desideri condividere le chiavi dell’account e le chiavi segrete con Experience Platform. Per ulteriori informazioni sul nuovo metodo di autenticazione, consulta la [sezione sull’autenticazione](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) della documentazione di Amazon S3. |

{style="table-layout:auto"}

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Identity Service {#identity-service}

Adobe Experience Platform Identity Service offre una panoramica completa della clientela e del relativo comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali ed efficaci in tempo reale.

**Documentazione nuova o aggiornata**

| Aggiornamento della documentazione | Descrizione |
| --- | --- |
| Ristrutturazione della documentazione | La documentazione dell’Identity Service è stata ristrutturata per migliorarne la presentazione e la chiarezza dei concetti:<ul><li>Visita la [pagina di panoramica di Identity Service](../../identity-service/home.md) per una guida teminologica estesa, un esempio di caso d’uso che descrive un percorso clienti tipico, un raggruppamento del modo in cui l’Identity Service collega le identità e un riepilogo del ruolo che tale servizio ricopre all’interno dell’ecosistema Experience Platform.</li><li>Leggi la guida sulla [relazione tra Identity Service e Real-Time Customer Profile](../../identity-service/identity-and-profile.md) per un riepilogo dettagliato della collaborazione tra i due servizi e per le differenze tra scopi, processi, input e output.</li><li>Fai riferimento alla [guida per la logica di collegamento dell’Identity Service](../../identity-service/features/identity-linking-logic.md) per spiegazioni e visualizzazioni sul comportamento del grafico delle identità in base a scenari e timestamp diversi.</li></ul> |

{style="table-layout:auto"}

Per ulteriori informazioni sull’Identity Service, leggi la [panoramica sull’Identity Service](../../identity-service/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Basato su Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) consente alle aziende di unire dati noti e sconosciuti per attivare i profili cliente con decisioni intelligenti in tutto il percorso del cliente. [!DNL Real-Time CDP] combina più origini dati aziendali per creare profili cliente in tempo reale. I segmenti generati da questi profili possono quindi essere inviati alle destinazioni a valle per fornire esperienze cliente personalizzate individuali su tutti i canali e i dispositivi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Aggiornamenti alla [pagina Home di Real-Time CDP](https://experience.adobe.com) | <ul><li>**Widget Profili**: ora puoi utilizzare il widget Profili per passare alla pagina panoramica dei Profili e visualizzare le metriche dei profili per la tua organizzazione.</li><li>**Scheda Metriche profilo**: la scheda Metriche profilo nella dashboard della pagina Home presenta ora il conteggio totale dei profili nell’organizzazione, a seconda del criterio di unione rispettivo.</li><li>**Widget Schemi**: ora puoi utilizzare il widget Schemi per passare al flusso di lavoro di creazione dello schema nell’interfaccia utente.</li></ul> |

{style="table-layout:auto"}

**Documentazione nuova o aggiornata**

| Aggiornamento della documentazione | Descrizione |
| --- | --- |
| Nuova pagina Home della documentazione di Real-Time CDP | Visita la [nuova pagina Home della documentazione di Real-Time CDP](/help/rtcdp/home.md) per un’occhiata alle informazioni su come iniziare a utilizzare il prodotto, guardrail, casi d’uso di esempio e molto altro. |
| Panoramica sui casi d’uso di esempio di Real-Time CDP | Visita la [nuova pagina con una panoramica sui casi d’uso di esempio](/help/rtcdp/use-case-guides/overview.md) per una raccolta di casi d’uso di esempio realizzabili con Real-Time CDP. |

{style="table-layout:auto"}

Per ulteriori informazioni su Real-Time CDP, consulta la [panoramica su Real-Time CDP](../../rtcdp/overview.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati clienti in una visualizzazione unificata che offre un account utilizzabile e dotato di marca temporale per ogni interazione con il cliente.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti alla localizzazione delle schede predefinite della dashboard del visualizzatore di profili | Le schede predefinite del profilo ora avranno nomi localizzati in modo dinamico. Le schede personalizzate del profilo possono continuare ad avere nomi personalizzati e modificabili. |

{style="table-layout:auto"}

Per ulteriori informazioni sul profilo cliente in tempo reale, leggi la [panoramica sul profilo](../../profile/home.md)

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Caricamento di pubblico generato esternamente | Il numero massimo di colonne è stato aumentato a **25**. |
| Stime di Generatore di segmenti | Le stime e i profili qualificati vengono ora visualizzati nella sezione delle proprietà del pubblico. Per ulteriori informazioni su questa modifica, consulta la [Guida dell’interfaccia utente di Generatore di segmenti](../../segmentation/ui/segment-builder.md). |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} Origini [!DNL Oracle NetSuite] | Utilizza le integrazioni [!DNL Oracle NetSuite] nel catalogo delle origini per portare in Experience Platform i dati dai tuoi account [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) e [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md). |
| [!BADGE Beta]{type=Informative} Origine [!DNL Braze Currents]  | Utilizza l’integrazione [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) nel catalogo delle origini per portare in Experience Platform i dati dal tuo account [!DNL Braze]. |
| Supporto per l’autenticazione con coppia di chiavi per l’origne batch [!DNL Snowflake] | Ora puoi utilizzare l’autenticazione con coppia di chiavi durante la creazione di un nuovo account [!DNL Snowflake] per i dati in batch. Per ulteriori informazioni, leggi la guida sulla [creazione di un account [!DNL Snowflake] tramite API](../../sources/tutorials/api/create/databases/snowflake.md) o la guida sulla [creazione di un account [!DNL Snowflake] tramite l’interfaccia utente](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sources/home.md).
