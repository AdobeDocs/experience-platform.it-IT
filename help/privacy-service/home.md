---
keywords: ' Experience Platform;home;argomenti popolari;GDPR;gdpr;ccpa:CCPA;PDPA;pdpa;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;'
solution: Experience Platform
title: Panoramica di  Adobe Experience Platform Privacy Service
topic: overview
description: Privacy Service consente di semplificare la conformità automatizzata alle normative sulla privacy nelle operazioni sui dati del Experience Cloud .
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '1396'
ht-degree: 0%

---


# Panoramica di Adobe Experience Platform [!DNL Privacy Service]

Per offrire esperienze cliente migliori, devi raccogliere e archiviare i dati personali dei clienti. Quando si utilizzano questi dati, è importante comprendere e rispettare la privacy dei clienti. Le nuove normative legali e organizzative danno agli utenti il diritto di accedere o cancellare i propri dati personali dall&#39;archivio dei dati su richiesta.

Adobe Experience Platform [!DNL Privacy Service] è stata sviluppata in risposta a un cambiamento fondamentale nel modo in cui le aziende sono tenute a gestire i dati personali dei loro clienti. Lo scopo principale di [!DNL Privacy Service] è quello di automatizzare la conformità alle normative sulla privacy dei dati che, in caso di violazione, può comportare multe elevate e interrompere le operazioni sui dati per la tua attività.

[!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutarti a gestire le richieste di dati dei clienti. Con [!DNL Privacy Service], puoi inviare richieste di accesso ed eliminazione di dati personali dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative sulla privacy legali e organizzative.

## Guida introduttiva a [!DNL Privacy Service] {#getting-started}

Per poter utilizzare [!DNL Privacy Service], è necessario prendere diverse decisioni chiave in termini di requisiti di privacy dell&#39;organizzazione, tipi di dati di identità raccolti dai clienti e il modo migliore per interfacciare il sistema CRM con il servizio.

Tali decisioni possono essere riassunte attraverso le seguenti domande:

1. **Quali informazioni sto raccogliendo dai miei clienti?**
   * Per utilizzare al meglio [!DNL Privacy Service], è necessario avere una conoscenza dettagliata dei tipi di dati raccolti dai clienti e di quelli soggetti alle normative sulla privacy. Per ulteriori informazioni, consulta la sezione relativa alla [determinazione dei requisiti di privacy](#requirements).
1. **Ho etichettato correttamente i miei dati?**
   * I dati devono essere etichettati correttamente affinché il servizio possa determinare quali campi accedere o eliminare durante i processi di privacy. Per ulteriori informazioni, vedere la sezione sull&#39;etichetta [data](#label).
1. **So a quali ID inviare  [!DNL Privacy Service]?**
   * Quando si inviano richieste di privacy, è necessario fornire ID cliente individuali specifici per specifiche applicazioni  Adobe. Per ulteriori informazioni, vedere le sezioni relative alla [fornitura di dati di identità](#identity) e [richiesta di privacy](#requests).
1. **Come posso monitorare i miei lavori sulla privacy?**
   * Una volta effettuate le richieste di privacy, sono disponibili diverse opzioni per il tracciamento dello stato e dei risultati. Per ulteriori informazioni, vedere la sezione sul [monitoraggio dei processi relativi alla privacy](#monitor).

Le sezioni seguenti forniscono indicazioni generali su questi importanti passaggi preliminari, nonché collegamenti verso ulteriori [!DNL Privacy Service] documenti per ulteriori dettagli.

### Determinare i requisiti di privacy dell&#39;organizzazione {#requirements}

A seconda della natura della tua attività e delle giurisdizioni in cui essa opera, le tue operazioni sui dati possono essere soggette alle normative sulla privacy legali. Queste normative danno spesso ai clienti il diritto di richiedere l&#39;accesso ai dati raccolti e il diritto di richiedere l&#39;eliminazione dei dati archiviati. Tali richieste di dati personali da parte del cliente sono denominate &quot;richieste di privacy&quot; in tutta la documentazione.

Per informazioni dettagliate sulle diverse normative sulla privacy legali per le quali [!DNL Privacy Service] gestisce le richieste, compresi i termini chiave e le risposte alle domande frequenti, fare riferimento alla [documentazione sulle normative sulla privacy](./regulations/overview.md).

Se le operazioni relative ai dati rientrano nell&#39;ambito di applicazione di una qualsiasi delle normative supportate, rivedete la loro documentazione per informazioni importanti, quali i diritti specifici sulla privacy che offrono ai clienti e le finestre di conformità per soddisfare le richieste sulla privacy. Queste informazioni devono essere prese in considerazione quando si determina come integrare [!DNL Privacy Service] nel sistema CRM, e come i clienti devono interagire con il tuo sito Web per effettuare richieste sulla privacy.

Oltre alle normative legali, nel prendere queste decisioni dovrebbero essere presi in considerazione anche tutti gli standard organizzativi o industriali applicabili alla tua organizzazione.

### Dati etichetta per richieste di privacy {#label}

A seconda delle applicazioni [!DNL Experience Cloud] in uso, è necessario etichettare i campi dati specifici a cui è necessario accedere o eliminare in risposta alle richieste di privacy. Il processo di etichettatura dei dati varia a seconda delle applicazioni. Per informazioni su come etichettare i dati per ogni applicazione  Adobe supportata, consultare il documento sulle applicazioni di  Experience Cloud [](./experience-cloud-apps.md).

### Determinare i tipi di dati di identità da inviare a [!DNL Privacy Service] {#identity}

Affinché [!DNL Privacy Service] possa elaborare una richiesta di privacy da parte di un cliente, nella richiesta deve essere fornito almeno un valore di identità univoco per tale cliente. Un valore di identità univoco è costituito da qualsiasi informazione che può essere utilizzata per identificare una singola persona e i suoi dati personali memorizzati all&#39;interno dei [!DNL Experience Cloud] archivi di dati. [!DNL Privacy Service] utilizza queste informazioni di identità per individuare ed elaborare i dati personali del cliente in base alla natura della richiesta (accesso, eliminazione o rinuncia).

A seconda delle [!DNL Experience Cloud] applicazioni che il sistema CRM utilizza, il tipo e il numero di valori di identità che è necessario fornire per ogni cliente varieranno. Alcune applicazioni utilizzano i propri valori ID cliente interni (come  ID Adobe Target), mentre altre soluzioni si basano su identificatori globali provenienti  Adobe [!DNL Experience Cloud Identity Service] (ECID) che tengono traccia dell&#39;attività dei clienti in tutte le applicazioni [!DNL Experience Cloud]. Inoltre, le informazioni personali generiche come un indirizzo e-mail o un numero di telefono possono anche fungere da dati di identità validi.

Il documento relativo ai [dati di identità per le richieste di privacy](./identity-data.md) fornisce informazioni più dettagliate sui tipi di informazioni di identità accettate per [!DNL Privacy Service]. Il documento fornisce inoltre indicazioni su come sfruttare  tecnologie di Adobe per recuperare efficacemente le informazioni di identità appropriate dai clienti durante l&#39;interazione con il sito Web, e inviare tali dati a [!DNL Privacy Service] nelle richieste API.

### Avvio delle richieste di privacy {#requests}

Dopo aver determinato le esigenze di privacy della tua azienda e deciso quali valori di identità inviare a [!DNL Privacy Service], puoi iniziare a effettuare richieste di privacy. [!DNL Privacy Service] consente di inviare richieste di privacy tramite l&#39;API o l&#39;interfaccia utente.

>[!IMPORTANT]
>
>Le sezioni seguenti contengono collegamenti alla documentazione che descrive come effettuare richieste di privacy generiche nell&#39;API o nell&#39;interfaccia utente. Tuttavia, a seconda delle [!DNL Experience Cloud] applicazioni in uso, i campi che è necessario inviare nel payload della richiesta possono essere diversi dagli esempi mostrati in queste guide.
>
>Seguendo le guide delle API o dell&#39;interfaccia utente, fare riferimento al documento relativo alle [applicazioni per Privacy Service e Experienci Cloud ](./experience-cloud-apps.md) per ulteriori informazioni su come formattare le richieste di privacy per le applicazioni [!DNL Experience Cloud].
>
>È inoltre importante notare che le richieste di privacy vengono elaborate in modo asincrono tra le applicazioni  Experience Cloud. Una volta ricevuta la richiesta dal Privacy Service, ogni applicazione può richiedere da qualche minuto a settimane per completare la richiesta. Il tempo necessario per completare ogni richiesta è specifico per l’applicazione in uso e per la quantità di dati da elaborare.

#### Utilizzo dell&#39;API

[[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) offre diversi endpoint per la creazione e la gestione di processi per la privacy mediante chiamate RESTful API, che consentono di impostare a livello di programmazione la conformità alla normativa sulla privacy per le applicazioni [!DNL Experience Cloud]. Per informazioni dettagliate sull&#39;utilizzo dell&#39;API, consultate la guida per gli sviluppatori [Privacy Service API Guide](api/getting-started.md).

#### Utilizzo dell’interfaccia

>[!NOTE]
>
>L&#39;interfaccia [!DNL Privacy Service] al momento supporta solo le richieste di accesso ed eliminazione. Tutte le richieste di rifiuto devono essere effettuate tramite l&#39;API.

L&#39;interfaccia utente [!DNL Privacy Service] consente di creare e monitorare i processi relativi alla privacy mediante un&#39;interfaccia grafica. L&#39;interfaccia utente include un widget **[!UICONTROL Status Report]** che fornisce una rappresentazione visiva dello stato di tutte le richieste attive e consente di creare nuove richieste utilizzando il **[!UICONTROL Request Builder]** incorporato o caricando file JSON. Per ulteriori informazioni sull&#39;utilizzo dell&#39;interfaccia utente, consultate la guida utente [Privacy Service](ui/overview.md).

### Monitorare i processi di privacy {#monitor}

Una volta effettuati i processi relativi alla privacy, è possibile controllarne lo stato e i risultati tramite diverse opzioni:

| Metodo di monitoraggio | Descrizione |
| --- | --- |
| [!DNL Privacy Service] Interfaccia | L&#39; [!DNL Privacy Service] interfaccia utente fornisce un dashboard di monitoraggio che consente di visualizzare una rappresentazione visiva dello stato di tutte le richieste attive. Per ulteriori informazioni, vedere la [guida utente Privacy Service](ui/overview.md). |
| [!DNL Privacy Service] API | È possibile monitorare lo stato dei processi relativi alla privacy a livello di programmazione utilizzando gli endpoint di ricerca forniti dall&#39;API [!DNL Privacy Service]. Per informazioni dettagliate sull&#39;utilizzo dell&#39;API, consultate la [guida per gli sviluppatori di Privacy Service](./api/getting-started.md). |
| [!DNL Privacy Events] | [!DNL Privacy Events] sfruttare  Adobe I/O Events inviati a un webhook configurato per facilitare l&#39;automazione efficiente della richiesta di processo. Essi riducono o eliminano la necessità di eseguire il polling dell&#39;API [!DNL Privacy Service] per verificare se un processo è completo o se è stata raggiunta una determinata fase cardine all&#39;interno di un flusso di lavoro. Per ulteriori informazioni, consulta l&#39;esercitazione su [iscrizione a Eventi sulla privacy](./privacy-events.md). |

## Passaggi successivi

Questo documento fornisce una panoramica di alto livello di [!DNL Privacy Service] e dei passaggi principali necessari per iniziare a utilizzare le funzionalità del servizio. Per informazioni più dettagliate sui vari aspetti dell&#39;utilizzo di [!DNL Privacy Service], fare riferimento alla documentazione collegata a tutta la panoramica.
