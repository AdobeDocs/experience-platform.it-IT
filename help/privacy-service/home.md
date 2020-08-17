---
keywords: Experience Platform;home;popular topics;GDPR;gdpr;ccpa:CCPA
solution: Experience Platform
title: ' Adobe Experience Platform Privacy Service'
topic: overview
translation-type: tm+mt
source-git-commit: cc81d590f308c7e2677cec000c27e8aca42437f5
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 2%

---


# Adobe Experience Platform [!DNL Privacy Service] overview

Per offrire esperienze cliente migliori, devi raccogliere e archiviare i dati personali dei clienti. Quando si utilizzano questi dati, è importante comprendere e rispettare la privacy dei clienti. Le nuove normative legali e organizzative danno agli utenti il diritto di accedere o cancellare i propri dati personali dall&#39;archivio dei dati su richiesta.

Adobe Experience Platform [!DNL Privacy Service] è stata sviluppata in risposta a un cambiamento fondamentale nel modo in cui le aziende sono tenute a gestire i dati personali dei loro clienti. Lo scopo principale di [!DNL Privacy Service] è automatizzare la conformità con le normative sulla privacy dei dati che, in caso di violazione, possono comportare gravi multe e interrompere le operazioni relative ai dati per la tua attività.

[!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutarti a gestire le richieste di dati dei clienti. Con [!DNL Privacy Service]questa opzione puoi inviare richieste di accesso ed eliminazione di dati personali dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

## Getting started with [!DNL Privacy Service] {#getting-started}

Per poter utilizzare [!DNL Privacy Service], è necessario prendere diverse decisioni chiave in termini di requisiti di privacy dell&#39;organizzazione, tipi di dati di identità raccolti dai clienti e il modo migliore per interfacciare il sistema CRM con il servizio.

Tali decisioni possono essere riassunte attraverso le seguenti domande:

1. **Quali informazioni sto raccogliendo dai miei clienti?**
   * Per utilizzare al meglio [!DNL Privacy Service], devi avere una comprensione dettagliata dei tipi di dati raccolti dai clienti e di quelli soggetti alle normative sulla privacy. Per ulteriori informazioni, consulta la sezione sulla [determinazione dei requisiti](#requirements) di privacy.
1. **Ho etichettato correttamente i miei dati?**
   * I dati devono essere etichettati correttamente affinché il servizio possa determinare quali campi accedere o eliminare durante i processi di privacy. Per ulteriori informazioni, consulta la sezione sull’ [etichettatura dei dati](#label) .
1. **So a quali ID inviare[!DNL Privacy Service]?**
   * Quando si inviano richieste di privacy, è necessario fornire ID cliente individuali specifici per specifiche applicazioni  Adobe. Per ulteriori informazioni, consulta le sezioni sulla [fornitura dei dati](#identity) di identità e sulle richieste [di](#requests) privacy.
1. **Come posso monitorare i miei lavori sulla privacy?**
   * Una volta effettuate le richieste di privacy, sono disponibili diverse opzioni per il tracciamento dello stato e dei risultati. Per ulteriori informazioni, consulta la sezione sul [monitoraggio dei processi](#monitor) di privacy.

Le sezioni seguenti forniscono indicazioni generali su questi importanti passi preliminari e forniscono anche collegamenti verso ulteriori [!DNL Privacy Service] documenti per ulteriori dettagli.

### Determinare i requisiti di privacy dell&#39;organizzazione {#requirements}

A seconda della natura della tua attività e delle giurisdizioni in cui essa opera, le tue operazioni sui dati possono essere soggette alle normative sulla privacy legali. Queste normative danno spesso ai clienti il diritto di richiedere l&#39;accesso ai dati raccolti e il diritto di richiedere l&#39;eliminazione dei dati archiviati. Tali richieste di dati personali da parte del cliente sono denominate &quot;richieste di privacy&quot; in tutta la documentazione.

Nella tabella seguente sono illustrate le normative sulla privacy legali che [!DNL Privacy Service] gestiscono le richieste, compresi i collegamenti alla documentazione per ulteriori informazioni:

| regolamento | Descrizione |
| --- | --- |
| CCPA (California) | The [!DNL California Consumer Privacy Act] (CCPA) enhances privacy rights and consumer protection for residents of California, United States. L&#39;CCPA fornisce nuovi diritti sulla privacy dei dati ai residenti della California, compreso il diritto di accedere ai loro dati personali ed eliminarli, di sapere se i loro dati personali sono venduti o divulgati (e a chi), e il diritto di non far vendere i loro dati a terzi.<br/><br/>Link per ulteriore documentazione: <ul><li>[Panoramica legale](https://oag.ca.gov/privacy/ccpa)</li><li>[Domande frequenti su CCPA](ccpa/faq.md)</li></ul> |
| GDPR (Unione europea) | The [!DNL General Data Protection Regulation] (GDPR) introduced several new data privacy rights for members of the European Union, including the **Right to Access** and the **Right to be Forgotten**. Ciò significa che qualsiasi cittadino dell’UE i cui dati personali siano stati raccolti dalla tua azienda può richiedere l’accesso ai dati o la loro cancellazione in qualsiasi momento. <br/><br/>Link per ulteriore documentazione: <ul><li>[Panoramica legale](https://gdpr-info.eu/)</li><li>[Domande frequenti su RGPD](gdpr/faq.md)</li><li>[Terminologia RGPD](gdpr/terminology.md)</li></ul> |
| PDPA_THA (Thailandia) | Il Personal Data Protection Act of Thailand (PDPA) è stato introdotto per proteggere i proprietari di dati thailandesi dalla raccolta, dall&#39;uso o dalla divulgazione illecita dei loro dati personali. Ispirandosi al GDPR dell&#39;Unione europea, il regolamento concede ai cittadini thailandesi il diritto di chiedere l&#39;accesso ai loro dati personali conservati o di eliminarli.<br/><br/>Link per ulteriore documentazione: <ul><li>[Panoramica legale](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[Domande frequenti su PDPA_THA](pdpa-tha/faq.md)</li><li>[Terminologia PDPA_THA](pdpa-tha/terminology.md)</li></ul> |

Se le operazioni relative ai dati rientrano nell&#39;ambito di applicazione di una qualsiasi delle suddette normative, rivedete la loro documentazione per informazioni importanti, quali i diritti specifici sulla privacy che offrono ai clienti e le finestre di conformità per soddisfare le richieste sulla privacy. Queste informazioni devono essere prese in considerazione quando si determina come integrare [!DNL Privacy Service] nel sistema CRM e come i clienti devono interagire con il tuo sito Web per effettuare richieste sulla privacy.

Oltre alle normative legali, nel prendere queste decisioni dovrebbero essere presi in considerazione anche tutti gli standard organizzativi o industriali applicabili alla tua organizzazione.

### Dati etichetta per richieste di privacy {#label}

A seconda delle [!DNL Experience Cloud] applicazioni in uso, è necessario etichettare i campi dati specifici a cui è necessario accedere o eliminare in risposta alle richieste di privacy. Il processo di etichettatura dei dati varia a seconda delle applicazioni. Per informazioni su come etichettare i dati per ogni applicazione  Adobe supportata, consultare il documento sulle applicazioni [](./experience-cloud-apps.md)Experience Cloud.

### Determinare i tipi di dati di identità da inviare [!DNL Privacy Service] {#identity}

Per [!DNL Privacy Service] elaborare una richiesta di privacy da parte di un cliente, nella richiesta deve essere fornito almeno un valore univoco per tale cliente. Un valore di identità univoco è costituito da qualsiasi informazione che può essere utilizzata per identificare una singola persona e i suoi dati personali memorizzati all&#39;interno dei [!DNL Experience Cloud] data store. [!DNL Privacy Service] utilizza queste informazioni di identità per individuare ed elaborare i dati personali del cliente in base alla natura della richiesta (accesso, eliminazione o rinuncia).

A seconda delle [!DNL Experience Cloud] applicazioni che il sistema CRM utilizza, il tipo e il numero di valori di identità che è necessario fornire per ogni cliente varieranno. Alcune applicazioni utilizzano i propri valori ID cliente interni (come  ID Adobe Target), mentre altre soluzioni si basano su identificatori globali provenienti dal Adobe  [!DNL Experience Cloud Identity Service] (ECID) che tengono traccia dell&#39;attività dei clienti in tutte le [!DNL Experience Cloud] applicazioni. Inoltre, le informazioni personali generiche come un indirizzo e-mail o un numero di telefono possono anche fungere da dati di identità validi.

Il documento sui dati di [identità per le richieste](./identity-data.md) di privacy fornisce informazioni più dettagliate sui tipi di informazioni di identità accettate per [!DNL Privacy Service]. Il documento fornisce inoltre indicazioni su come sfruttare  tecnologie di Adobe per recuperare efficacemente le informazioni di identità appropriate dai clienti che interagiscono con il sito Web e inviare tali dati [!DNL Privacy Service] nelle richieste API.

### Avvio delle richieste di privacy {#requests}

Una volta determinate le esigenze di privacy della tua azienda e deciso a quali valori di identità inviare, [!DNL Privacy Service]puoi iniziare a effettuare richieste di privacy. [!DNL Privacy Service] consente di inviare richieste di privacy tramite l&#39;API o l&#39;interfaccia utente.

>[!IMPORTANT]
>
>Le sezioni seguenti contengono collegamenti alla documentazione che descrive come effettuare richieste di privacy generiche nell&#39;API o nell&#39;interfaccia utente. Tuttavia, a seconda delle [!DNL Experience Cloud] applicazioni in uso, i campi che è necessario inviare nel payload della richiesta possono essere diversi dagli esempi riportati in queste guide.
>
>Seguendo le guide API o dell&#39;interfaccia utente, consulta il documento sulle applicazioni [](./experience-cloud-apps.md) Privacy Service e  Experience Cloud per ulteriori informazioni su come formattare le richieste di privacy per le [!DNL Experience Cloud] applicazioni.

#### Utilizzo dell&#39;API

Il modulo [!DNL Privacy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) fornisce diversi endpoint per la creazione e la gestione dei processi di privacy mediante chiamate RESTful API, che consentono di impostare in modo programmatico la conformità alla normativa sulla privacy per [!DNL Experience Cloud] le applicazioni. Per informazioni dettagliate sull&#39;utilizzo dell&#39;API, consultate la guida per gli sviluppatori API [Privacy Service](api/getting-started.md).

#### Utilizzo dell’interfaccia

>[!NOTE]
>
>Al momento l&#39; [!DNL Privacy Service] interfaccia utente supporta solo le richieste di accesso ed eliminazione. Tutte le richieste di rifiuto devono essere effettuate tramite l&#39;API.

L’ [!DNL Privacy Service] interfaccia utente consente di creare e monitorare i processi relativi alla privacy mediante un’interfaccia grafica. L’interfaccia utente include un **[!UICONTROL Status Report]** widget che fornisce una rappresentazione visiva dello stato di tutte le richieste attive e consente di creare nuove richieste utilizzando il predefinito **[!UICONTROL Request Builder]** o caricando file JSON. Per ulteriori informazioni sull’utilizzo dell’interfaccia utente, consultate la guida [utente](ui/overview.md)Privacy Service.

### Monitorare i processi di privacy {#monitor}

Una volta effettuati i processi relativi alla privacy, è possibile controllarne lo stato e i risultati tramite diverse opzioni:

| Metodo di monitoraggio | Descrizione |
| --- | --- |
| [!DNL Privacy Service] Interfaccia | L’ [!DNL Privacy Service] interfaccia utente fornisce una dashboard di monitoraggio che consente di visualizzare una rappresentazione visiva dello stato di tutte le richieste attive. Per ulteriori informazioni, consultate la guida [utente per i](ui/overview.md) Privacy Service. |
| [!DNL Privacy Service] API | Potete monitorare lo stato dei processi relativi alla privacy a livello di programmazione utilizzando gli endpoint di ricerca forniti dall&#39; [!DNL Privacy Service] API. Per informazioni dettagliate sull&#39;utilizzo dell&#39;API, consultate la guida [per gli sviluppatori di](./api/getting-started.md) Privacy Service. |
| [!DNL Privacy Events] | [!DNL Privacy Events] sfruttare  eventi I/O Adobe inviati a un webhook configurato per facilitare l&#39;automazione efficiente della richiesta di lavoro. Essi riducono o eliminano la necessità di eseguire il polling dell&#39; [!DNL Privacy Service] API per verificare se un processo è completo o se è stata raggiunta una determinata fase cardine all&#39;interno di un flusso di lavoro. Per ulteriori informazioni, consulta l’esercitazione sull’ [iscrizione agli eventi](./privacy-events.md) sulla privacy. |

## Passaggi successivi

Questo documento fornisce una panoramica di alto livello dei passaggi principali [!DNL Privacy Service] e principali necessari per iniziare a utilizzare le funzionalità del servizio. Per informazioni più dettagliate sui diversi aspetti dell&#39;utilizzo di [!DNL Privacy Service], consultare la documentazione collegata a tutta la panoramica.
