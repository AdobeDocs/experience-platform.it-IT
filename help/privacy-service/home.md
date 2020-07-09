---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Adobe Experience Platform Privacy Service '
topic: overview
translation-type: tm+mt
source-git-commit: d358b200d574ca8de77ee2274836c03f7cc84c40
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 5%

---


# Panoramica del Adobe Experience Platform Privacy Service 

Per offrire esperienze cliente migliori, devi raccogliere e archiviare i dati personali dei clienti. Quando si utilizzano questi dati, è importante comprendere e rispettare la privacy dei clienti. Le nuove normative legali e organizzative danno agli utenti il diritto di accedere o cancellare i propri dati personali dall&#39;archivio dei dati su richiesta.

 Adobe Experience Platform Privacy Service è stato sviluppato in risposta a un cambiamento fondamentale nel modo in cui le aziende sono tenute a gestire i dati personali dei loro clienti. Lo scopo principale di Privacy Service è automatizzare la conformità alle normative sulla privacy dei dati che, in caso di violazione, possono comportare multe elevate e interrompere le operazioni relative ai dati per la tua attività.

Privacy Service fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutarti a gestire le richieste di dati dei clienti. Con Privacy Service, puoi inviare richieste di accesso ed eliminazione di dati personali dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative sulla privacy legali e organizzative.

## Guida introduttiva ad Privacy Service {#getting-started}

Per poter utilizzare Privacy Service, è necessario prendere diverse decisioni chiave in termini di requisiti di privacy dell&#39;organizzazione, tipi di dati di identità raccolti dai clienti e il modo migliore per interfacciare il sistema CRM con il servizio.

Tali decisioni possono essere riassunte attraverso le seguenti domande:

1. **Quali informazioni sto raccogliendo dai miei clienti?**
   * Per sfruttare al meglio Privacy Service, devi avere una conoscenza dettagliata dei tipi di dati raccolti dai tuoi clienti e quali sono soggetti alle normative sulla privacy. Per ulteriori informazioni, consulta la sezione sulla [determinazione dei requisiti](#requirements) di privacy.
1. **Ho etichettato correttamente i miei dati?**
   * I dati devono essere etichettati correttamente affinché il servizio possa determinare quali campi accedere o eliminare durante i processi di privacy. Per ulteriori informazioni, consulta la sezione sull’ [etichettatura dei dati](#label) .
1. **So quali ID inviare ad Privacy Service?**
   * Quando si inviano richieste di privacy, è necessario fornire ID cliente individuali specifici per determinate applicazioni Adobe. Per ulteriori informazioni, consulta le sezioni sulla [fornitura dei dati](#identity) di identità e sulle richieste [di](#requests) privacy.
1. **Come posso monitorare i miei lavori sulla privacy?**
   * Una volta effettuate le richieste di privacy, sono disponibili diverse opzioni per il tracciamento dello stato e dei risultati. Per ulteriori informazioni, consulta la sezione sul [monitoraggio dei processi](#monitor) di privacy.

Le sezioni riportate di seguito forniscono indicazioni generali su questi importanti passaggi preliminari e collegamenti verso ulteriori documenti Privacy Service per ulteriori dettagli.

### Determinare i requisiti di privacy dell&#39;organizzazione {#requirements}

A seconda della natura della tua attività e delle giurisdizioni in cui essa opera, le tue operazioni sui dati possono essere soggette alle normative sulla privacy legali. Queste normative danno spesso ai clienti il diritto di richiedere l&#39;accesso ai dati raccolti e il diritto di richiedere l&#39;eliminazione dei dati archiviati. Tali richieste di dati personali da parte del cliente sono denominate &quot;richieste di privacy&quot; in tutta la documentazione.

Nella tabella seguente sono illustrate le normative sulla privacy legali per le quali Privacy Service gestisce le richieste, compresi i collegamenti alla documentazione per ulteriori informazioni:

| regolamento | Descrizione |
| --- | --- |
| CCPA (California) | Il California Consumer Privacy Act (CCPA) migliora i diritti alla privacy e la protezione dei consumatori per i residenti in California, Stati Uniti. L&#39;CCPA fornisce nuovi diritti sulla privacy dei dati ai residenti della California, compreso il diritto di accedere ai loro dati personali ed eliminarli, di sapere se i loro dati personali sono venduti o divulgati (e a chi), e il diritto di non far vendere i loro dati a terzi.<br/><br/>Link per ulteriore documentazione: <ul><li>[Panoramica legale](https://oag.ca.gov/privacy/ccpa)</li><li>[Domande frequenti su CCPA](ccpa/faq.md)</li></ul> |
| GDPR (Unione europea) | Il Regolamento generale sulla protezione dei dati (RGPD) ha introdotto diversi nuovi diritti riguardanti la privacy dei dati per i membri dell’Unione europea, tra cui il **diritto di accesso** e il **diritto all’oblio**. Ciò significa che qualsiasi cittadino dell’UE i cui dati personali siano stati raccolti dalla tua azienda può richiedere l’accesso ai dati o la loro cancellazione in qualsiasi momento. <br/><br/>Link per ulteriore documentazione: <ul><li>[Panoramica legale](https://gdpr-info.eu/)</li><li>[Domande frequenti su RGPD](gdpr/faq.md)</li><li>[Terminologia RGPD](gdpr/terminology.md)</li></ul> |
| PDPA_THA (Thailandia) | Il Personal Data Protection Act of Thailand (PDPA) è stato introdotto per proteggere i proprietari di dati thailandesi dalla raccolta, dall&#39;uso o dalla divulgazione illecita dei loro dati personali. Ispirandosi al GDPR dell&#39;Unione europea, il regolamento concede ai cittadini thailandesi il diritto di chiedere l&#39;accesso ai loro dati personali conservati o di eliminarli.<br/><br/>Link per ulteriore documentazione: <ul><li>[Panoramica legale](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[Domande frequenti su PDPA_THA](pdpa-tha/faq.md)</li><li>[Terminologia PDPA_THA](pdpa-tha/terminology.md)</li></ul> |

Se le operazioni relative ai dati rientrano nell&#39;ambito di applicazione di una qualsiasi delle suddette normative, rivedete la loro documentazione per informazioni importanti, quali i diritti specifici sulla privacy che offrono ai clienti e le finestre di conformità per soddisfare le richieste sulla privacy. Queste informazioni devono essere prese in considerazione quando si stabilisce come integrare Privacy Service nel sistema CRM e come i clienti devono interagire con il tuo sito Web per effettuare richieste sulla privacy.

Oltre alle normative legali, nel prendere queste decisioni dovrebbero essere presi in considerazione anche tutti gli standard organizzativi o industriali applicabili alla tua organizzazione.

### Dati etichetta per richieste di privacy {#label}

A seconda delle applicazioni Experience Cloud  in uso, è necessario etichettare i campi dati specifici a cui è necessario accedere o eliminare in risposta alle richieste di privacy. Il processo di etichettatura dei dati varia a seconda delle applicazioni. Per informazioni su come etichettare i dati per ciascuna applicazione Adobe supportata, consultare il documento [applicazioni](./experience-cloud-apps.md)Experience Cloud.

### Determinare i tipi di dati di identità da inviare ad Privacy Service {#identity}

Affinché Privacy Service possa elaborare una richiesta di privacy da parte di un cliente, nella richiesta deve essere fornito almeno un valore univoco per tale cliente. Un valore di identità univoco è costituito da qualsiasi informazione che può essere utilizzata per identificare una singola persona e i suoi dati personali memorizzati negli archivi di dati Experience Cloud . Privacy Service utilizza queste informazioni di identità per individuare ed elaborare i dati personali del cliente in base alla natura della richiesta (accesso, eliminazione o rinuncia).

A seconda delle applicazioni Experience Cloud  utilizzate dal sistema CRM, il tipo e il numero di valori di identità che è necessario fornire a ciascun cliente varieranno. Alcune applicazioni utilizzano valori ID cliente interni (come  ID Adobe Target), mentre altre soluzioni si basano su identificatori globali di Adobe Experience Cloud Identity Service (ECID) che tengono traccia dell’attività dei clienti in tutte  applicazioni Experience Cloud. Inoltre, le informazioni personali generiche come un indirizzo e-mail o un numero di telefono possono anche fungere da dati di identità validi.

Il documento sui dati di [identità per le richieste](./identity-data.md) di privacy fornisce informazioni più dettagliate sui tipi di informazioni di identità accettate per Privacy Service. Il documento fornisce inoltre indicazioni su come sfruttare le tecnologie Adobe per recuperare efficacemente le informazioni di identità appropriate dai clienti durante l&#39;interazione con il sito Web e inviare tali dati ad Privacy Service nelle richieste API.

### Avvio delle richieste di privacy {#requests}

Dopo aver determinato le esigenze di privacy della tua azienda e deciso quali valori di identità inviare ad Privacy Service, puoi iniziare a effettuare richieste di privacy. Privacy Service consente di inviare richieste di privacy tramite l&#39;API o l&#39;interfaccia utente.

>[!IMPORTANT]
>
>Le sezioni seguenti contengono collegamenti alla documentazione che descrive come effettuare richieste di privacy generiche nell&#39;API o nell&#39;interfaccia utente. Tuttavia, a seconda delle applicazioni Experience Cloud  utilizzate, i campi che è necessario inviare nel payload della richiesta possono essere diversi dagli esempi riportati in queste guide.
>
>Seguendo le guide API o dell&#39;interfaccia utente, consulta il documento sulle applicazioni [](./experience-cloud-apps.md) Privacy Service e  Experience Cloud per ulteriori informazioni su come formattare le richieste di privacy per le specifiche applicazioni  Experience Cloud.

#### Utilizzo dell&#39;API

L&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) Privacy Service fornisce diversi endpoint per la creazione e la gestione di processi relativi alla privacy mediante chiamate RESTful API, consentendo di impostare a livello di programmazione la conformità alla normativa sulla privacy per le applicazioni Experience Cloud . Per i passaggi dettagliati su come utilizzare l&#39;API, consultate la guida [per gli sviluppatori di](api/getting-started.md)Privacy Service API.

#### Utilizzo dell’interfaccia

>[!NOTE]
>
>L&#39;interfaccia utente di Privacy Service al momento supporta solo le richieste di accesso ed eliminazione. Tutte le richieste di rifiuto devono essere effettuate tramite l&#39;API.

L’interfaccia utente di Privacy Service consente di creare e monitorare i processi relativi alla privacy mediante un’interfaccia grafica. L’interfaccia utente include un widget per report **di** stato che fornisce una rappresentazione visiva dello stato di tutte le richieste attive e consente di creare nuove richieste utilizzando il **Generatore** di richieste incorporato o caricando file JSON. Per ulteriori informazioni sull’utilizzo dell’interfaccia utente, consultate la guida [utente di](ui/overview.md)Privacy Service.

### Monitorare i processi di privacy {#monitor}

Una volta effettuati i processi relativi alla privacy, è possibile controllarne lo stato e i risultati tramite diverse opzioni:

| Metodo di monitoraggio | Descrizione |
| --- | --- |
| Interfaccia utente Privacy Service | L’interfaccia utente di Privacy Service fornisce una dashboard di monitoraggio che consente di visualizzare una rappresentazione visiva dello stato di tutte le richieste attive. Per ulteriori informazioni, consultate la guida [utente di](ui/overview.md) Privacy Service. |
| API Privacy Service | Potete monitorare lo stato dei processi relativi alla privacy a livello di programmazione utilizzando gli endpoint di ricerca forniti dall&#39;API di Privacy Service. Consultate la guida [per gli sviluppatori di](./api/getting-started.md) Privacy Service per i passaggi dettagliati sull&#39;utilizzo dell&#39;API. |
| Eventi sulla privacy | Gli eventi sulla privacy sfruttano gli eventi di I/O di Adobe inviati a un webhook configurato per facilitare l’automazione efficiente della richiesta di lavoro. Essi riducono o eliminano la necessità di eseguire il polling dell’API Privacy Service per verificare se un processo è completo o se è stata raggiunta una determinata fase cardine all’interno di un flusso di lavoro. Per ulteriori informazioni, consulta l’esercitazione sull’ [iscrizione agli eventi](./privacy-events.md) sulla privacy. |

## Passaggi successivi

Questo documento fornisce una panoramica di alto livello di Privacy Service e dei passaggi principali necessari per iniziare a utilizzare le funzionalità del servizio. Per informazioni più approfondite sui diversi aspetti dell&#39;utilizzo di Privacy Service, consultate la documentazione allegata alla panoramica.
