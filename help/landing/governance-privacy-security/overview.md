---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Panoramica su governance, privacy e sicurezza
topic: overview
description: Adobe Experience Platform offre diversi servizi e strumenti che consentono di controllare in modo sicuro i dati sulle esperienze raccolti al fine di rispettare le prassi aziendali, gli obblighi legali e il processo di sviluppo.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---


# Governance, privacy e sicurezza in Adobe Experience Platform

Adobe Experience Platform consente di assimilare, analizzare, ottimizzare e intervenire sui dati per migliorare notevolmente le esperienze dei clienti. Questi dati sono vasti, complessi e incredibilmente preziosi. A seconda della natura delle operazioni sui dati, delle giurisdizioni legali in cui opera la tua azienda e delle politiche organizzative relative all&#39;utilizzo dei dati, devi controllare e monitorare attentamente la raccolta e l&#39;utilizzo dei dati relativi all&#39;esperienza cliente al fine di proteggere i tuoi interessi commerciali.

 Experience Platform offre diversi servizi e strumenti che consentono di controllare in modo sicuro i dati relativi all&#39;esperienza raccolti al fine di rispettare le prassi aziendali, gli obblighi legali e i processi di sviluppo. Le sezioni seguenti forniscono un&#39;introduzione a ciascuno di questi servizi, insieme ai link alla documentazione per ulteriori informazioni.

I servizi possono essere suddivisi in tre domini:

* [Governance dei dati](#governance)
* [Privacy](#privacy)
* [Sicurezza](#security)

## Gestione dei dati {#governance}

La governance dei dati è un concetto essenziale che si intreccia con tutte le capacità  Experience Platform. La governance dei dati rappresenta la capacità di controllare e comprendere i dati in tutto il percorso attraverso la piattaforma. Ciò comporta il mantenimento della qualità dei dati, della linea di dati, della catalogazione dei dati e altro ancora.

### Governance dei dati Adobe Experience Platform {#data-governance}

Come servizio della piattaforma, Adobe Experience Platform Data Governance consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all&#39;uso dei dati. Esso svolge un ruolo chiave all&#39;interno  Experience Platform a vari livelli, tra cui l&#39;etichettatura dell&#39;uso dei dati, i criteri di utilizzo dei dati, l&#39;applicazione dei criteri e la linea di dati.

Per ulteriori informazioni, vedere [Panoramica sulla governance dei dati](../../data-governance/home.md).

### Catalogo e set di dati {#catalog}

Catalog Service è il sistema di record per la posizione dei dati e la linea di collegamento all&#39;interno della piattaforma. Mentre tutti i dati acquisiti  Experience Platform vengono memorizzati nel Data Lake come file e directory, Catalog contiene i metadati e la descrizione di tali file e directory a scopo di ricerca e monitoraggio.

Catalog organizza i dati acquisiti in set di dati, con ogni dataset contenente metadati che possono essere utilizzati per etichettare e classificare i dati in esso contenuti.

Per ulteriori informazioni sul servizio, vedere [Panoramica del servizio Catalogo](../../catalog/home.md). Per informazioni su come gestire i set di dati in  Experience Platform, vedere la [panoramica dei set di dati](../../catalog/datasets/overview.md).

## Privacy {#privacy}

La privacy è un problema critico per il vostro business, legislatori e i vostri clienti. Poiché i dati personali raccolti dai clienti sono al centro di quasi tutti i flussi di lavoro  Experience Platform, Platform fornisce servizi per supportare queste iniziative.

###  Adobe Experience Platform Privacy Service {#privacy-service}

Le norme sulla privacy legale, come il Regolamento generale sulla protezione dei dati (General Data Protection Regulation, GDPR) dell&#39;Unione Europea e il California Consumer Privacy Act (CCPA), concedono ai cittadini all&#39;interno delle loro giurisdizioni il diritto di accedere ed eliminare i dati personali raccolti e conservati da loro.

 Adobe Experience Platform Privacy Service fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutare a gestire queste richieste. Con Privacy Service, puoi inviare richieste di accesso o eliminazione di dati di clienti privati o personali dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative sulla privacy legali e organizzative.

Per ulteriori informazioni, vedere [Privacy Service overview](../../privacy-service/home.md).

### Raccolta di consenso {#consent}

Molte normative legali sulla privacy hanno introdotto requisiti per il consenso attivo e specifico quando si tratta di raccolta di dati, personalizzazione e altri casi di utilizzo del marketing. Per soddisfare questi requisiti,  Experience Platform consente di acquisire le informazioni sul consenso nei profili dei clienti individuali e di utilizzare tali preferenze come fattore determinante per l&#39;utilizzo dei dati di ciascun cliente nei flussi di lavoro della piattaforma a valle.

Per informazioni su come raccogliere ed elaborare i dati di consenso dei clienti in conformità con lo IAB Transparency and Consent Framework (TCF) 2.0, vedere la panoramica sul supporto di [IAB TCF 2.0 in Platform](./consent/iab/overview.md).

<!-- For more information on the consent collection process using the Adobe standard, see the [consent collection overview]. -->

## Sicurezza {#security}

L&#39;integrità e la sicurezza dei dati sono indispensabili per la tua attività e questo rischio richiede capacità di sicurezza leader del settore. Per affrontare questa sfida, Platform offre diversi strumenti per la salvaguardia delle operazioni sui dati.

### Controllo degli accessi {#access-control}

 Experience Platform utilizza l&#39;Adobe Admin Console per fornire un controllo dell&#39;accesso basato sui ruoli a varie funzionalità della piattaforma. Questa funzionalità sfrutta i profili di prodotto in  Admin Console, che collegano gli utenti con autorizzazioni e sandbox.

Per ulteriori informazioni, vedere la [panoramica sul controllo degli accessi](../../access-control/home.md).

### Sandbox {#sandboxes}

 Experience Platform è stato creato per arricchire le applicazioni per esperienze digitali su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e all&#39;implementazione di tali applicazioni, garantendo al contempo la conformità operativa.

Per rispondere alla necessità di flessibilità di sviluppo,  Experience Platform fornisce sandbox che dividono una singola istanza della piattaforma in ambienti virtuali separati per aiutarvi a sviluppare le vostre applicazioni di esperienza digitale basate sul vostro ciclo di vita di sviluppo.

Per ulteriori informazioni, consultate la [panoramica sulle sandbox](../../sandboxes/home.md).

## Passaggi successivi

Questo documento fornisce una panoramica dei vari servizi e strumenti della Piattaforma relativi a governance dei dati, privacy e sicurezza. Per ulteriori informazioni su queste funzionalità, consulta la documentazione collegata a questa guida.