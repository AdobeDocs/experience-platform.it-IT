---
keywords: Experience Platform;home;argomenti popolari;RGPD;rgpd;ccpa:CCPA;pdpa;PDPA_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Panoramica di Privacy Service
description: Privacy Service consente di facilitare la conformità automatica alle normative legali sulla privacy nelle operazioni relative ai dati di Experience Cloud.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 037ea8d11bb94e3b4f71ea301a535677b3cccdbd
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 5%

---

# Panoramica di [!DNL Privacy Service]

Per offrire migliori esperienze ai clienti, devi raccogliere e archiviare i dati personali dei clienti. Quando si utilizzano questi dati, è importante comprendere e rispettare la privacy dei clienti. Nuovi regolamenti legali e organizzativi danno agli utenti il diritto di accedere ai propri dati o di cancellarli dagli archivi dati su richiesta.

Adobe Experience Platform [!DNL Privacy Service] è stato sviluppato in risposta a un cambiamento fondamentale nel modo in cui le aziende sono tenute a gestire i dati personali dei loro clienti. L&#39;obiettivo principale di [!DNL Privacy Service] automatizzare la conformità alle normative sulla privacy dei dati che, se violate, possono comportare multe elevate e interrompere le operazioni sui dati per la tua azienda.

[!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente che consentono di gestire le richieste di dati dei clienti. Con [!DNL Privacy Service], puoi inviare richieste di accesso e cancellazione dei dati personali dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

>[!IMPORTANT]
>
>Privacy Service è destinato solo alle richieste degli interessati e dei diritti dei consumatori. Qualsiasi altro utilizzo di Privacy Service per la pulizia o la manutenzione dei dati non è supportato o consentito. L&#39;Adobe ha l&#39;obbligo giuridico di adempiere tali obblighi in modo tempestivo. Di conseguenza, il test di carico su Privacy Service non è consentito in quanto si tratta di un ambiente di sola produzione e crea un backlog inutile di richieste di privacy valide.
>
>È ora disponibile un limite massimo di caricamento giornaliero per evitare abusi del servizio. Se gli utenti rilevano un abuso del sistema, l’accesso al servizio verrà disattivato. Successivamente si terrà una riunione con i Privacy Service per discutere le loro azioni e l&#39;uso accettabile di tali strumenti.

## Guida introduttiva a [!DNL Privacy Service] {#getting-started}

Al fine di utilizzare [!DNL Privacy Service], è necessario prendere diverse decisioni chiave in termini di requisiti di privacy della tua organizzazione, tipi di dati di identità raccolti dai clienti e il modo migliore per interfacciare il sistema CRM con il servizio.

Queste decisioni possono essere riassunte attraverso le seguenti domande:

1. **Quali informazioni vengono raccolte dai clienti?**
   * Per utilizzare al meglio [!DNL Privacy Service], devi conoscere in modo dettagliato i tipi di dati che raccogli dai tuoi clienti e quali di essi sono soggetti alle normative sulla privacy. Consulta la sezione su [determinazione dei requisiti di privacy](#requirements) per ulteriori informazioni.
1. **Ho etichettato correttamente i miei dati?**
   * I dati devono essere correttamente etichettati affinché il servizio possa determinare quali campi accedere o eliminare durante i processi relativi alla privacy. Consulta la sezione su [dati di etichettatura](#label) per ulteriori informazioni.
1. **So a quali ID inviare? [!DNL Privacy Service]?**
   * Quando si inviano richieste di privacy, è necessario fornire gli ID dei singoli clienti specifici per particolari applicazioni Adobi. Consulta le sezioni relative a [fornitura di dati di identità](#identity)  e [effettuare richieste di privacy](#requests) per ulteriori informazioni.
1. **Come si tiene traccia dei processi relativi alla privacy?**
   * Dopo aver effettuato le richieste di privacy, sono disponibili diverse opzioni per monitorarne lo stato e i risultati. Consulta la sezione su [monitoraggio dei processi relativi alla privacy](#monitor) per ulteriori informazioni.

Le sezioni seguenti forniscono indicazioni generali su questi importanti passaggi preliminari e collegamenti verso ulteriori [!DNL Privacy Service] per ulteriori dettagli.

### Determinare i requisiti di privacy della tua organizzazione {#requirements}

A seconda della natura della tua attività e delle giurisdizioni in cui opera, le tue operazioni sui dati possono essere soggette a normative legali sulla privacy. Tali nornmative solitamente tutelano il diritto dei clienti di richiedere l’accesso ai dati raccolti su di loro e memorizzati, e di richiederne l’eliminazione. In tutta la documentazione, queste richieste dei clienti per i propri dati personali sono denominate &quot;richieste di privacy&quot;.

Per informazioni dettagliate sulle diverse normative legali sulla privacy che [!DNL Privacy Service] gestisce le richieste di, inclusi i termini chiave e le risposte alle domande frequenti, fare riferimento a [documentazione sulle normative sulla privacy](./regulations/overview.md).

Se le operazioni sui dati rientrano nell’ambito di applicazione di una qualsiasi delle normative supportate, consulta la relativa documentazione per informazioni importanti quali i diritti specifici sulla privacy concessi ai clienti e le finestre di conformità per soddisfare le richieste di privacy. Queste informazioni dovrebbero essere prese in considerazione nel determinare come integrare [!DNL Privacy Service] nel sistema CRM e come i clienti devono interagire con il sito web per effettuare richieste di privacy.

Oltre alle normative legali, nel prendere queste decisioni è necessario tenere in considerazione anche eventuali standard organizzativi o di settore applicabili alla tua organizzazione.

### Etichettare i dati per le richieste di privacy {#label}

A seconda della [!DNL Experience Cloud] applicazioni in uso, è necessario etichettare i campi di dati specifici che devono essere accessibili o eliminati in risposta alle richieste di accesso a dati personali. Il processo di etichettatura dei dati varia a seconda delle applicazioni. Per informazioni su come etichettare i dati per ciascuna applicazione di Adobe supportata, consulta il documento su [applicazioni Experience Cloud](./experience-cloud-apps.md).

### Determinare i tipi di dati di identità da inviare a [!DNL Privacy Service] {#identity}

Per ottenere [!DNL Privacy Service] per elaborare una richiesta di accesso a dati personali da parte di un cliente, è necessario fornire almeno un valore di identità univoco per tale cliente nella richiesta stessa. Un valore di identità univoco è qualsiasi informazione che può essere utilizzata per identificare una singola persona e i suoi dati personali memorizzati all’interno del tuo [!DNL Experience Cloud] archivi dati. [!DNL Privacy Service] utilizza queste informazioni di identità per individuare ed elaborare i dati personali del cliente in base alla natura della richiesta (accesso, eliminazione o rinuncia).

A seconda della [!DNL Experience Cloud] applicazioni utilizzate dal sistema CRM, il tipo e il numero di valori di identità da fornire per ogni cliente varieranno. Alcune applicazioni utilizzano i propri valori ID cliente interni (come gli ID di Adobe Target), mentre altre soluzioni si basano su identificatori globali di Adobe [!DNL Experience Cloud Identity Service] (ECID) che tengono traccia dell’attività dei clienti in tutti [!DNL Experience Cloud] applicazioni. Inoltre, anche informazioni personali generiche come l’indirizzo e-mail o il numero di telefono possono fungere da dati di identità validi.

Il documento su [dati di identità per le richieste di privacy](./identity-data.md) fornisce informazioni più dettagliate sui tipi di informazioni di identità accettate per [!DNL Privacy Service]. Il documento fornisce anche indicazioni su come sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate dai clienti durante l’interazione con il sito web e inviare tali dati a [!DNL Privacy Service] nelle richieste API.

### Inizia ad effettuare richieste di privacy {#requests}

Una volta stabilite le esigenze di privacy della tua azienda e i valori di identità da inviare a [!DNL Privacy Service], puoi iniziare ad effettuare richieste di accesso a dati personali. [!DNL Privacy Service] consente di inviare richieste di accesso a dati personali tramite l’API o l’interfaccia utente.

>[!IMPORTANT]
>
>Le sezioni seguenti forniscono collegamenti alla documentazione che descrivono come effettuare richieste generiche di accesso a dati personali nell’API o nell’interfaccia utente. Tuttavia, a seconda della [!DNL Experience Cloud] applicazioni in uso, i campi da inviare nel payload della richiesta possono essere diversi dagli esempi mostrati in queste guide.
>
>Nel seguire le guide API o dell’interfaccia utente, consulta il documento su [Applicazioni Privacy Service e Experience Cloud](./experience-cloud-apps.md) per ulteriore documentazione su come formattare le richieste di accesso a dati personali per specifici [!DNL Experience Cloud] applicazione/i.
>
>È inoltre importante notare che le richieste di accesso ai dati personali vengono elaborate in modo asincrono tra le applicazioni Experience Cloud. Una volta ricevuta una richiesta da parte di Privacy Service, ogni applicazione può richiedere da minuti a settimane per completare la richiesta. Il tempo necessario per completare ogni richiesta è specifico per l’applicazione con cui stai lavorando e la quantità di dati da elaborare.

#### Mediante l’API

Il [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) fornisce diversi endpoint per la creazione e la gestione di processi relativi alla privacy utilizzando le chiamate API RESTful, consentendoti di approcciare in modo programmatico la conformità alle normative sulla privacy per [!DNL Experience Cloud] applicazioni. Per i passaggi dettagliati su come utilizzare l’API, consulta [Guida all’API di Privacy Service](api/overview.md).

#### Utilizzo dell’interfaccia utente

>[!NOTE]
>
>Il [!DNL Privacy Service] Al momento l’interfaccia utente supporta solo le richieste di accesso ed eliminazione. Tutte le richieste di rinuncia devono essere effettuate tramite l’API.

Il [!DNL Privacy Service] L’interfaccia utente consente di creare e monitorare i processi relativi alla privacy utilizzando un’interfaccia grafica. L’interfaccia utente include **[!UICONTROL Rapporto di stato]** widget che fornisce una rappresentazione visiva dello stato di tutte le richieste attive e consente di creare nuove richieste utilizzando **[!UICONTROL Request Builder]** o caricando file JSON. Per ulteriori informazioni sull&#39;utilizzo dell&#39;interfaccia utente, vedere [Guida utente di Privacy Service](ui/overview.md).

### Monitorare i processi relativi alla privacy {#monitor}

Dopo aver eseguito i processi relativi alla privacy, puoi monitorare lo stato e i risultati di tali processi in diverse modi:

| Metodo di monitoraggio | Descrizione |
| --- | --- |
| [!DNL Privacy Service] Interfaccia utente | Il [!DNL Privacy Service] L’interfaccia utente fornisce una dashboard di monitoraggio che consente di visualizzare una rappresentazione visiva dello stato di tutte le richieste attive. Consulta la [Guida utente di Privacy Service](ui/overview.md) per ulteriori informazioni. |
| [!DNL Privacy Service] API | Puoi monitorare in modo programmatico lo stato dei processi di Privacy utilizzando gli endpoint di ricerca forniti da [!DNL Privacy Service] API. Consulta la [Guida all’API di Privacy Service](./api/overview.md) per i passaggi dettagliati su come utilizzare l’API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] sfrutta gli eventi Adobe I/O inviati a un webhook configurato per facilitare l’automazione efficiente delle richieste di processo. Riducono o eliminano la necessità di polling [!DNL Privacy Service] API per verificare se un processo è completo o se è stata raggiunta una determinata fase cardine all’interno di un flusso di lavoro. Guarda il tutorial su [abbonamento a eventi sulla privacy](./privacy-events.md) per ulteriori informazioni. |

## Passaggi successivi

Questo documento fornisce una panoramica ad alto livello di [!DNL Privacy Service] e i passaggi principali necessari per iniziare a utilizzare le funzionalità del servizio. Per informazioni più approfondite sui vari aspetti dell&#39;utilizzo di, fare riferimento alla documentazione accessibile dal collegamento [!DNL Privacy Service].
