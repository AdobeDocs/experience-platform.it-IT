---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Panoramica su governance, privacy e sicurezza
description: Adobe Experience Platform offre diversi servizi e strumenti che ti consentono di controllare in modo affidabile i dati delle esperienze raccolte al fine di rispettare le pratiche aziendali, gli obblighi legali e il processo di sviluppo.
feature: Data Governance,Privacy
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 7%

---

# Governance, privacy e sicurezza in Adobe Experience Platform

Adobe Experience Platform consente di acquisire, analizzare, ottimizzare e intervenire sui dati per migliorare notevolmente le esperienze dei clienti. Questi dati sono vasti, complessi e di incredibile valore. A seconda della natura delle operazioni sui dati, delle giurisdizioni legali in cui opera l’azienda e delle politiche organizzative relative all’utilizzo dei dati, è necessario controllare e monitorare attentamente la raccolta e l’utilizzo dei dati sull’esperienza del cliente per proteggere i propri interessi aziendali.

Experience Platform offre diversi servizi e strumenti che ti consentono di controllare in modo affidabile i dati sull’esperienza raccolti al fine di rispettare le pratiche aziendali, gli obblighi legali e i processi di sviluppo. Le sezioni seguenti forniscono un’introduzione a ciascuno di questi servizi, insieme ai collegamenti alla documentazione per ulteriori informazioni.

I servizi possono essere suddivisi in tre domini:

* [Governance dei dati](#governance)
* [Privacy](#privacy)
* [Sicurezza](#security)

## Governance dei dati {#governance}

La governance dei dati è un concetto essenziale che si intreccia con ogni funzionalità di Experience Platform. La governance dei dati rappresenta la capacità di controllare e comprendere i dati in tutto il percorso tramite Platform. Ciò implica mantenere la qualità dei dati, la derivazione dei dati, la catalogazione dei dati e altro ancora.

### Governance dei dati Adobe Experience Platform {#data-governance}

In qualità di servizio di Platform, la governance dei dati di Adobe Experience Platform consente di gestire i dati dei clienti e garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati. Svolge un ruolo chiave all’interno di Experience Platform a vari livelli, tra cui l’etichettatura dell’utilizzo dei dati, i criteri di utilizzo dei dati, l’applicazione dei criteri e la derivazione dei dati.

Per ulteriori informazioni, vedere [Panoramica sulla governance dei dati](../../data-governance/home.md).

### Catalogo e set di dati {#catalog}

Catalog Service è il sistema di registrazione per la posizione e la derivazione dei dati in Platform. Mentre tutti i dati acquisiti in Experience Platform vengono memorizzati nel data lake come file e directory, il servizio Catalog contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca e monitoraggio.

Il catalogo organizza i dati acquisiti in set di dati, con ogni set di dati contenente metadati che possono essere utilizzati per etichettare e classificare i dati in esso contenuti.

Per ulteriori informazioni sul servizio, vedere [Panoramica del servizio catalogo](../../catalog/home.md). Per informazioni su come gestire i set di dati in Experience Platform, consulta la [panoramica dei set di dati](../../catalog/datasets/overview.md).

## Privacy {#privacy}

La privacy è un problema critico per il tuo business, legislatori e clienti. Poiché i dati personali raccolti dai clienti sono al centro di quasi tutti i flussi di lavoro Experienci Platform, Platform fornisce servizi a supporto di queste iniziative.

### Adobe Experience Platform Privacy Service {#privacy-service}

Le normative legali sulla privacy, come il Regolamento generale sulla protezione dei dati (RGPD) dell’Unione Europea e il California Consumer Privacy Act (CCPA), concedono ai cittadini all’interno delle loro giurisdizioni il diritto di accesso e cancellazione dei dati personali che raccogli e archivi da loro.

Adobe Experience Platform Privacy Service fornisce un’API RESTful e un’interfaccia utente per facilitare la gestione di queste richieste. Con Privacy Service puoi inviare richieste di accesso o cancellazione di dati privati o personali dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

Per ulteriori informazioni, consulta la [panoramica di Privacy Service](../../privacy-service/home.md).

### Elaborazione del consenso {#consent}

Molte normative legali sulla privacy hanno introdotto requisiti per il consenso attivo e specifico in materia di raccolta dati, personalizzazione e altri casi d’uso di marketing. Al fine di soddisfare questi requisiti, Experience Platform consente di acquisire informazioni sul consenso nei profili dei singoli clienti e di utilizzare tali preferenze come fattore determinante nel modo in cui i dati di ciascun cliente vengono utilizzati nei flussi di lavoro della piattaforma a valle.

Per informazioni su come elaborare i dati relativi al consenso e alle preferenze del cliente utilizzando Adobe Standard, consulta la panoramica sull&#39;elaborazione del consenso [nell&#39;Experience Platform](./consent/adobe/overview.md).

Per informazioni su come elaborare i dati sul consenso dei clienti in conformità con IAB Transparency and Consent Framework (TCF) 2.0, consulta la panoramica sul supporto di [IAB TCF 2.0 in Platform](./consent/iab/overview.md).

## Sicurezza {#security}

L&#39;integrità e la sicurezza dei dati sono indispensabili per l&#39;azienda e questo rischio richiede funzionalità di sicurezza leader del settore. Per risolvere questo problema, Platform fornisce diversi strumenti per contribuire a salvaguardare le operazioni sui dati.

### Crittografia dei dati

Tutti i dati di Platform sono crittografati in transito e a riposo. Per ulteriori informazioni, consulta il documento sulla crittografia dei dati [ in Platform](./encryption.md).

### Controllo degli accessi {#access-control}

Experience Platform utilizza Adobe Admin Console per fornire il controllo dell’accesso basato sui ruoli per varie funzionalità di Platform. Questa funzionalità sfrutta i profili di prodotto di Admin Console, che collegano gli utenti con autorizzazioni e sandbox.

Per ulteriori informazioni, vedere [panoramica sul controllo degli accessi](../../access-control/home.md).

### Sandbox {#sandboxes}

Experience Platform è stato sviluppato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

Per soddisfare la necessità di flessibilità di sviluppo, Experience Platform fornisce sandbox che suddividono una singola istanza Platform in ambienti virtuali separati, utili per sviluppare le applicazioni di esperienza digitale in base al proprio ciclo di vita di sviluppo.

Per ulteriori informazioni, consulta la [panoramica delle sandbox](../../sandboxes/home.md).

## Passaggi successivi

Questo documento fornisce una panoramica dei vari servizi e strumenti di Platform coinvolti nella governance dei dati, nella privacy e nella sicurezza. Per ulteriori informazioni su queste funzionalità, consulta la documentazione accessibile dai collegamenti presenti in questa guida.
