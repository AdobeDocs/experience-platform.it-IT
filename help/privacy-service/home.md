---
keywords: Experience Platform;home;argomenti popolari;RGPD;rgpd;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Panoramica di Privacy Service
topic-legacy: overview
description: Privacy Service consente di facilitare la conformità automatica alle normative sulla privacy nelle operazioni sui dati di Experience Cloud.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 0%

---

# [!DNL Privacy Service]panoramica

Per fornire esperienze cliente migliori, devi raccogliere e archiviare i dati personali dei tuoi clienti. Quando si utilizzano questi dati, è importante comprendere e rispettare la privacy dei clienti. Nuovi regolamenti legali e organizzativi danno agli utenti il diritto di accedere o cancellare i propri dati personali dagli archivi dati su richiesta.

Adobe Experience Platform [!DNL Privacy Service] è stato sviluppato in risposta a un cambiamento fondamentale nel modo in cui le aziende sono tenute a gestire i dati personali dei propri clienti. Lo scopo principale di [!DNL Privacy Service] è quello di automatizzare la conformità alle normative sulla privacy dei dati che, in caso di violazione, possono comportare multe ingenti e interrompere le operazioni relative ai dati per la tua azienda.

[!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente per aiutarti a gestire le richieste di dati dei clienti. Con [!DNL Privacy Service] puoi inviare richieste di accesso e cancellazione dei dati dei clienti personali dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

## Guida introduttiva a [!DNL Privacy Service] {#getting-started}

Per poter utilizzare [!DNL Privacy Service], è necessario prendere diverse decisioni chiave in termini di requisiti di privacy della tua organizzazione, tipi di dati di identità raccolti dai tuoi clienti e il modo migliore per interfacciare il tuo sistema CRM con il servizio.

Tali decisioni possono essere riassunte attraverso le seguenti domande:

1. **Quali informazioni raccolgo dai miei clienti?**
   * Per utilizzare al meglio [!DNL Privacy Service], devi avere una comprensione dettagliata dei tipi di dati raccolti dai clienti e di quali sono soggetti alle normative sulla privacy. Per ulteriori informazioni, consulta la sezione su [determinazione dei requisiti di privacy](#requirements) .
1. **Ho etichettato correttamente i miei dati?**
   * I dati devono essere etichettati correttamente affinché il servizio determini quali campi accedere o eliminare durante i processi di privacy. Per ulteriori informazioni, consulta la sezione sull’ [etichettatura dei dati](#label) .
1. **So a quali ID inviare  [!DNL Privacy Service]?**
   * Quando si inviano richieste di accesso a dati personali, è necessario fornire ID cliente individuali specifici per particolari applicazioni di Adobe. Per ulteriori informazioni, consulta le sezioni su [fornire dati di identità](#identity) e [effettuare richieste di privacy](#requests) .
1. **Come posso tenere traccia dei miei lavori sulla privacy?**
   * Dopo aver effettuato le richieste di privacy, sono disponibili diverse opzioni per tracciarne lo stato e i risultati. Per ulteriori informazioni, consulta la sezione sul [monitoraggio dei processi relativi alla privacy](#monitor) .

Le sezioni seguenti forniscono indicazioni generali su questi importanti passaggi preliminari e forniscono anche collegamenti ad ulteriore documentazione [!DNL Privacy Service] per ulteriori dettagli.

### Determinare i requisiti di privacy dell&#39;organizzazione {#requirements}

A seconda della natura della tua attività e delle giurisdizioni in cui opera, le tue operazioni sui dati possono essere soggette alle normative sulla privacy legali. Questi regolamenti danno spesso ai clienti il diritto di richiedere l&#39;accesso ai dati raccolti e il diritto di richiedere l&#39;eliminazione dei dati memorizzati. Le richieste dei clienti per i loro dati personali sono denominate &quot;richieste di privacy&quot; in tutta la documentazione.

Per informazioni dettagliate sulle diverse normative legali sulla privacy che [!DNL Privacy Service] gestisce le richieste di , compresi i termini chiave e le risposte alle domande frequenti, consulta la [documentazione sulle normative sulla privacy](./regulations/overview.md).

Se le operazioni sui dati rientrano nel campo di applicazione di una qualsiasi delle normative supportate, controlla la documentazione relativa a informazioni importanti, come i diritti specifici sulla privacy che offrono ai tuoi clienti e le finestre di conformità per soddisfare le richieste sulla privacy. Queste informazioni devono essere prese in considerazione quando si determina come integrare [!DNL Privacy Service] nel sistema CRM e come i clienti devono interagire con il tuo sito web per effettuare richieste di privacy.

Oltre alle normative legali, nel prendere queste decisioni dovrebbero essere presi in considerazione anche tutti gli standard organizzativi o di settore applicabili alla tua organizzazione.

### Etichettare i dati per le richieste di privacy {#label}

A seconda delle applicazioni [!DNL Experience Cloud] in uso, è necessario etichettare i campi di dati specifici a cui è necessario accedere o eliminare in risposta alle richieste di privacy. Il processo di etichettatura dei dati varia a seconda delle applicazioni. Per informazioni su come etichettare i dati per ogni applicazione di Adobe supportata, consulta il documento sulle [applicazioni di Experience Cloud](./experience-cloud-apps.md).

### Determinare i tipi di dati di identità da inviare a [!DNL Privacy Service] {#identity}

Affinché [!DNL Privacy Service] possa elaborare una richiesta di accesso a dati personali da parte di un cliente, nella richiesta stessa deve essere fornito almeno un valore di identità univoco per tale cliente. Un valore di identità univoco è qualsiasi informazione che può essere utilizzata per identificare una singola persona e i suoi dati personali memorizzati all&#39;interno dei tuoi archivi di dati [!DNL Experience Cloud]. [!DNL Privacy Service] utilizza queste informazioni di identità per individuare ed elaborare i dati personali del cliente in base alla natura della richiesta (accesso, cancellazione o rinuncia).

A seconda delle applicazioni [!DNL Experience Cloud] utilizzate dal sistema CRM, il tipo e il numero di valori di identità che è necessario fornire per ogni cliente variano. Alcune applicazioni utilizzano i propri valori ID cliente interni (come Adobe Target ID), mentre altre soluzioni si basano su identificatori globali a partire da [!DNL Experience Cloud Identity Service] (ECID) Adobe che tengono traccia dell&#39;attività dei clienti in tutte le [!DNL Experience Cloud] applicazioni. Inoltre, le informazioni personali generiche come un indirizzo e-mail o un numero di telefono possono fungere anche da dati di identità validi.

Il documento sui [dati di identità per le richieste di privacy](./identity-data.md) fornisce informazioni più dettagliate sui tipi di informazioni di identità accettate per [!DNL Privacy Service]. Il documento fornisce inoltre indicazioni su come sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate dai clienti che interagiscono con il sito web e inviare tali dati a [!DNL Privacy Service] nelle richieste API.

### Avvio dell&#39;esecuzione di richieste di privacy {#requests}

Una volta determinate le esigenze di privacy della tua azienda e deciso quali valori di identità inviare a [!DNL Privacy Service], puoi iniziare a effettuare richieste di privacy. [!DNL Privacy Service] consente di inviare richieste di privacy tramite l’API o l’interfaccia utente.

>[!IMPORTANT]
>
>Le sezioni seguenti forniscono collegamenti alla documentazione che descrive come effettuare richieste di privacy generiche nell’API o nell’interfaccia utente. Tuttavia, a seconda delle [!DNL Experience Cloud] applicazioni che utilizzi, i campi da inviare nel payload della richiesta possono essere diversi dagli esempi mostrati in queste guide.
>
>Seguendo le guide API o dell&#39;interfaccia utente, fai riferimento al documento sulle [applicazioni Privacy Service e Experience Cloud](./experience-cloud-apps.md) per ulteriore documentazione su come formattare le richieste di privacy per le tue particolari applicazioni [!DNL Experience Cloud].
>
>È inoltre importante notare che le richieste di privacy vengono elaborate in modo asincrono nelle applicazioni Experience Cloud. Una volta ricevuta una richiesta da Privacy Service, ogni applicazione può richiedere da minuti a settimane per completare la richiesta. Il tempo necessario per completare ogni richiesta è specifico per l’applicazione con cui stai lavorando e per la quantità di dati da elaborare.

#### Utilizzo dell’API

Il [[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) fornisce diversi endpoint per la creazione e la gestione dei processi di privacy tramite le chiamate RESTful API, che consentono di approcciare programmaticamente la conformità alle normative sulla privacy per le applicazioni [!DNL Experience Cloud]. Per passaggi dettagliati sull&#39;utilizzo dell&#39;API, consulta la [Guida per gli sviluppatori dell&#39;API Privacy Service](api/getting-started.md).

#### Utilizzo dell’interfaccia

>[!NOTE]
>
>L&#39;interfaccia utente [!DNL Privacy Service] supporta attualmente solo le richieste di accesso e cancellazione. Tutte le richieste di rinuncia devono invece essere effettuate tramite l’API .

L’ [!DNL Privacy Service] interfaccia utente consente di creare e monitorare processi di privacy tramite un’interfaccia grafica. L’interfaccia utente include un widget **[!UICONTROL Status Report]** che fornisce una rappresentazione visiva dello stato di tutte le richieste attive e consente di creare nuove richieste utilizzando il **[!UICONTROL Request Builder]** integrato o caricando file JSON. Per ulteriori informazioni sull&#39;utilizzo dell&#39;interfaccia utente, consulta la [guida utente di Privacy Service](ui/overview.md).

### Monitorare i processi di privacy {#monitor}

Una volta effettuati i lavori sulla privacy, hai diverse opzioni per monitorarne lo stato e i risultati:

| Metodo di monitoraggio | Descrizione |
| --- | --- |
| [!DNL Privacy Service] Interfaccia | L’ [!DNL Privacy Service] interfaccia utente fornisce un dashboard di monitoraggio che consente di visualizzare una rappresentazione visiva dello stato di tutte le richieste attive. Per ulteriori informazioni, consulta la [guida utente di Privacy Service](ui/overview.md) . |
| [!DNL Privacy Service] API | Puoi monitorare programmaticamente lo stato dei processi Privacy utilizzando gli endpoint di ricerca forniti dall’ API [!DNL Privacy Service] . Per informazioni dettagliate sull’utilizzo dell’API, consulta la [Guida per gli sviluppatori di Privacy Service](./api/getting-started.md) . |
| [!DNL Privacy Events] | [!DNL Privacy Events] sfrutta gli eventi di Adobe I/O inviati a un webhook configurato per facilitare l’automazione efficiente delle richieste di lavoro. Essi riducono o eliminano la necessità di eseguire il polling dell’ API [!DNL Privacy Service] per verificare se un processo è stato completato o se è stata raggiunta una determinata fase cardine all’interno di un flusso di lavoro. Per ulteriori informazioni, consulta l’esercitazione su [iscrizione a Eventi di privacy](./privacy-events.md) . |

## Passaggi successivi

Questo documento fornisce una panoramica di alto livello di [!DNL Privacy Service] e dei passaggi principali necessari per iniziare a utilizzare le funzionalità del servizio. Per informazioni più approfondite sui vari aspetti dell&#39;utilizzo di [!DNL Privacy Service], consulta la documentazione collegata a in tutta la panoramica.
