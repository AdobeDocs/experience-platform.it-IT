---
keywords: Experience Platform;home;argomenti popolari;RGPD;rgpd;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Panoramica di Privacy Service
description: Privacy Service consente di facilitare la conformità automatica alle normative sulla privacy nelle operazioni sui dati di Experience Cloud.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: e09f0598e1d8dc007d0fdfcf13da11d5cad94c54
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 5%

---

# Panoramica di [!DNL Privacy Service]

>[!IMPORTANT]
>
>Le autorizzazioni per Adobe Experience Platform Privacy Service sono state migliorate per aumentarne il livello di granularità. Queste modifiche consentono agli amministratori dell’organizzazione di concedere a più utenti l’accesso con il ruolo e il livello di autorizzazione desiderati. Gli utenti dell’account tecnico devono aggiornare le proprie autorizzazioni Privacy Service in quanto questo aggiornamento imminente rappresenta una modifica temporanea per loro. L&#39;applicazione di questa modifica delle autorizzazioni avrà luogo il **28 marzo 2023**.
>
>Gli account tecnici sono disponibili per i clienti aziendali e creati tramite Adobe Developers Console. L’Adobe ID di un titolare di account tecnico termina in `@techacct.adobe.com`. Se non sei sicuro di essere un titolare di account tecnico, contatta l’amministratore dell’organizzazione.

Per fornire esperienze cliente migliori, devi raccogliere e archiviare i dati personali dei tuoi clienti. Quando si utilizzano questi dati, è importante comprendere e rispettare la privacy dei clienti. Nuovi regolamenti legali e organizzativi danno agli utenti il diritto di accedere ai propri dati o di cancellarli dagli archivi dati su richiesta.

Adobe Experience Platform [!DNL Privacy Service] è stato sviluppato in risposta a un cambiamento fondamentale nel modo in cui le aziende sono tenute a gestire i dati personali dei loro clienti. Scopo centrale [!DNL Privacy Service] è quello di automatizzare la conformità alle normative sulla privacy dei dati che, in caso di violazione, possono comportare gravi multe e interrompere le operazioni sui dati per la tua azienda.

[!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente per aiutarti a gestire le richieste di dati dei clienti. Con [!DNL Privacy Service], puoi inviare richieste di accesso e cancellazione dei dati dei clienti personali dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

>[!IMPORTANT]
>
>Privacy Service è destinato solo alle richieste relative ai dati interessati e ai diritti dei consumatori. Qualsiasi altro utilizzo di Privacy Service per la pulizia o la manutenzione dei dati non è supportato o consentito. L&#39;Adobe ha l&#39;obbligo giuridico di rispettarli in tempo utile. Di conseguenza, il test di caricamento su Privacy Service non è consentito in quanto si tratta di un ambiente di sola produzione e crea un backlog inutile di richieste di privacy valide.
>
>È ora disponibile un limite di caricamento giornaliero per evitare abusi del servizio. Gli utenti che hanno riscontrato abusi del sistema avranno disattivato l’accesso al servizio. In seguito si terrà una riunione successiva con le parti interessate per discutere le loro azioni e l&#39;uso accettabile di Privacy Service.

## Guida introduttiva a [!DNL Privacy Service] {#getting-started}

Per utilizzare [!DNL Privacy Service], è necessario prendere diverse decisioni chiave in termini di requisiti di privacy della tua organizzazione, tipi di dati di identità raccolti dai tuoi clienti e il modo migliore per interfacciare il tuo sistema CRM con il servizio.

Tali decisioni possono essere riassunte attraverso le seguenti domande:

1. **Quali informazioni raccolgo dai miei clienti?**
   * Utilizzare al meglio [!DNL Privacy Service], devi avere una comprensione dettagliata dei tipi di dati raccolti dai tuoi clienti e di quali sono soggetti alle normative sulla privacy. Vedi la sezione su [determinazione dei requisiti di privacy](#requirements) per ulteriori informazioni.
1. **Ho etichettato correttamente i miei dati?**
   * I dati devono essere etichettati correttamente affinché il servizio determini quali campi accedere o eliminare durante i processi di privacy. Vedi la sezione su [dati di etichettatura](#label) per ulteriori informazioni.
1. **So a quali ID inviare? [!DNL Privacy Service]?**
   * Quando si inviano richieste di accesso a dati personali, è necessario fornire ID cliente individuali specifici per particolari applicazioni di Adobe. Consulta le sezioni [fornitura di dati di identità](#identity)  e [effettuare richieste di privacy](#requests) per ulteriori informazioni.
1. **Come posso tenere traccia dei miei lavori sulla privacy?**
   * Dopo aver effettuato le richieste di privacy, sono disponibili diverse opzioni per tracciarne lo stato e i risultati. Vedi la sezione su [monitoraggio dei processi di privacy](#monitor) per ulteriori informazioni.

Le sezioni seguenti forniscono orientamenti generali su queste importanti fasi preliminari e forniscono anche collegamenti verso ulteriori [!DNL Privacy Service] documentazione per maggiori dettagli.

### Determinare i requisiti di privacy dell’organizzazione {#requirements}

A seconda della natura della tua attività e delle giurisdizioni in cui opera, le tue operazioni sui dati possono essere soggette a normative legali sulla privacy. Tali nornmative solitamente tutelano il diritto dei clienti di richiedere l’accesso ai dati raccolti su di loro e memorizzati, e di richiederne l’eliminazione. Le richieste dei clienti per i loro dati personali sono denominate &quot;richieste di privacy&quot; in tutta la documentazione.

Per informazioni dettagliate sulle diverse normative legali sulla privacy che [!DNL Privacy Service] gestisce le richieste di , compresi i termini chiave e le risposte alle domande più frequenti, fai riferimento al [documentazione sulla privacy](./regulations/overview.md).

Se le operazioni sui dati rientrano nel campo di applicazione di una qualsiasi delle normative supportate, controlla la documentazione relativa a informazioni importanti, come i diritti specifici sulla privacy che offrono ai tuoi clienti e le finestre di conformità per soddisfare le richieste sulla privacy. Queste informazioni devono essere prese in considerazione al momento di determinare come integrare [!DNL Privacy Service] nel tuo sistema CRM e come i clienti devono interagire con il tuo sito web per effettuare richieste sulla privacy.

Oltre alle normative legali, nel prendere queste decisioni dovrebbero essere presi in considerazione anche tutti gli standard organizzativi o di settore applicabili alla tua organizzazione.

### Etichettare i dati per le richieste di privacy {#label}

A seconda del [!DNL Experience Cloud] applicazioni in uso, è necessario etichettare i campi dati specifici a cui è necessario accedere o eliminare in risposta alle richieste di privacy. Il processo di etichettatura dei dati varia a seconda delle applicazioni. Per informazioni su come etichettare i dati per ogni applicazione Adobe supportata, consulta il documento su [Applicazioni di Experience Cloud](./experience-cloud-apps.md).

### Determinare i tipi di dati di identità da inviare [!DNL Privacy Service] {#identity}

Per [!DNL Privacy Service] per elaborare una richiesta di accesso a dati personali da parte di un cliente, nella richiesta deve essere fornito almeno un valore di identità univoco per quel cliente. Un valore di identità univoco è qualsiasi informazione che può essere utilizzata per identificare una singola persona e i suoi dati personali memorizzati all&#39;interno del tuo [!DNL Experience Cloud] memorizza i dati. [!DNL Privacy Service] utilizza queste informazioni di identità per individuare ed elaborare i dati personali del cliente in base alla natura della richiesta (accesso, cancellazione o rinuncia).

A seconda del [!DNL Experience Cloud] applicazioni utilizzate dal sistema CRM, il tipo e il numero di valori di identità che è necessario fornire per ogni cliente variano. Alcune applicazioni utilizzano i propri valori ID cliente interni (come Adobe Target ID), mentre altre soluzioni si basano su identificatori globali derivati da Adobe [!DNL Experience Cloud Identity Service] (ECID) che tiene traccia dell’attività del cliente in tutti [!DNL Experience Cloud] applicazioni. Inoltre, le informazioni personali generiche come un indirizzo e-mail o un numero di telefono possono fungere anche da dati di identità validi.

Il documento su [dati di identità per le richieste di privacy](./identity-data.md) fornisce informazioni più dettagliate sui tipi di informazioni di identità accettati per [!DNL Privacy Service]. Il documento fornisce inoltre indicazioni su come sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate dai clienti durante l’interazione con il sito web e per inviare tali dati a [!DNL Privacy Service] nelle richieste API.

### Avvio dell&#39;elaborazione delle richieste di privacy {#requests}

Una volta determinate le esigenze di privacy della tua azienda e deciso a quali valori di identità inviare [!DNL Privacy Service], puoi iniziare a effettuare richieste sulla privacy. [!DNL Privacy Service] consente di inviare richieste di privacy tramite l’API o l’interfaccia utente.

>[!IMPORTANT]
>
>Le sezioni seguenti forniscono collegamenti alla documentazione che descrive come effettuare richieste di privacy generiche nell’API o nell’interfaccia utente. Tuttavia, a seconda del [!DNL Experience Cloud] applicazioni in uso, i campi che è necessario inviare nel payload della richiesta possono essere diversi dagli esempi mostrati in queste guide.
>
>Seguendo le guide API o dell’interfaccia utente, consulta il documento su [Applicazioni Privacy Service e Experience Cloud](./experience-cloud-apps.md) per ulteriore documentazione su come formattare le richieste di privacy per il tuo particolare [!DNL Experience Cloud] domande.
>
>È inoltre importante notare che le richieste di privacy vengono elaborate in modo asincrono nelle applicazioni Experience Cloud. Una volta ricevuta una richiesta da Privacy Service, ogni applicazione può richiedere da minuti a settimane per completare la richiesta. Il tempo necessario per completare ogni richiesta è specifico per l’applicazione con cui stai lavorando e per la quantità di dati da elaborare.

#### Mediante l’API

La [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) fornisce diversi endpoint per la creazione e la gestione dei processi relativi alla privacy tramite le chiamate RESTful API, che consentono di approcciare programmaticamente la conformità alla normativa sulla privacy per il tuo [!DNL Experience Cloud] applicazioni. Per i passaggi dettagliati sull’utilizzo dell’API, consulta [Guida all’API di Privacy Service](api/overview.md).

#### Utilizzo dell’interfaccia

>[!NOTE]
>
>La [!DNL Privacy Service] L’interfaccia utente supporta attualmente solo le richieste di accesso e di cancellazione. Tutte le richieste di rinuncia devono invece essere effettuate tramite l’API .

La [!DNL Privacy Service] L’interfaccia utente consente di creare e monitorare i processi relativi alla privacy tramite un’interfaccia grafica. L’interfaccia utente include un **[!UICONTROL Rapporto sullo stato]** widget che fornisce una rappresentazione visiva dello stato di tutte le richieste attive e consente di creare nuove richieste utilizzando il **[!UICONTROL Request Builder]** o caricando file JSON. Per ulteriori informazioni sull’utilizzo dell’interfaccia utente, consulta la [Guida utente di Privacy Service](ui/overview.md).

### Monitorare i processi di privacy {#monitor}

Una volta effettuati i lavori sulla privacy, hai diverse opzioni per monitorarne lo stato e i risultati:

| Metodo di monitoraggio | Descrizione |
| --- | --- |
| [!DNL Privacy Service] Interfaccia utente | La [!DNL Privacy Service] L’interfaccia utente fornisce un dashboard di monitoraggio che consente di visualizzare una rappresentazione visiva dello stato di tutte le richieste attive. Consulta la sezione [Guida utente di Privacy Service](ui/overview.md) per ulteriori informazioni. |
| [!DNL Privacy Service] API | Puoi monitorare programmaticamente lo stato dei processi Privacy utilizzando gli endpoint di ricerca forniti dalla [!DNL Privacy Service] API. Consulta la sezione [Guida all’API di Privacy Service](./api/overview.md) per passaggi dettagliati su come utilizzare l’API . |
| [!DNL Privacy Events] | [!DNL Privacy Events] sfrutta gli eventi di Adobe I/O inviati a un webhook configurato per facilitare l’automazione efficiente delle richieste di lavoro. Ridurre o eliminare la necessità di sondaggi [!DNL Privacy Service] API per verificare se un processo è stato completato o se è stata raggiunta una determinata fase cardine all’interno di un flusso di lavoro. Guarda l’esercitazione su [iscrizione agli eventi sulla privacy](./privacy-events.md) per ulteriori informazioni. |

## Passaggi successivi

Questo documento ha fornito una panoramica di alto livello di [!DNL Privacy Service] e i passaggi principali necessari per iniziare a utilizzare le funzionalità del servizio. Per informazioni più approfondite sui vari aspetti dell&#39;utilizzo dei [!DNL Privacy Service].
