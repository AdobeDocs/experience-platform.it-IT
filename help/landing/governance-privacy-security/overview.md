---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Panoramica su governance, privacy e sicurezza
description: Adobe Experience Platform offre diversi servizi e strumenti che ti consentono di controllare in modo affidabile i dati relativi all’esperienza raccolti per rispettare le tue pratiche commerciali, gli obblighi legali e il processo di sviluppo.
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 7%

---

# Governance, privacy e sicurezza in Adobe Experience Platform

Adobe Experience Platform consente di acquisire, analizzare, ottimizzare e intervenire sui dati per migliorare notevolmente l’esperienza dei clienti. Questi dati sono vasti, complessi e incredibilmente preziosi. A seconda della natura delle operazioni sui dati, delle giurisdizioni legali in cui opera la tua azienda e delle politiche organizzative relative all’utilizzo dei dati, devi controllare e monitorare attentamente la raccolta e l’utilizzo dei dati sulla customer experience al fine di proteggere i tuoi interessi aziendali.

Experience Platform offre diversi servizi e strumenti che ti consentono di controllare in modo sicuro i dati relativi all’esperienza raccolti per rispettare le tue pratiche commerciali, gli obblighi legali e i processi di sviluppo. Le sezioni seguenti forniscono un’introduzione a ciascuno di questi servizi, insieme a collegamenti alla documentazione per ulteriori informazioni.

I servizi possono essere suddivisi in tre domini:

* [Governance dei dati](#governance)
* [Privacy](#privacy)
* [Sicurezza](#security)

## Governance dei dati {#governance}

La governance dei dati è un concetto essenziale che si intreccia con ogni funzionalità di Experience Platform. La governance dei dati rappresenta la tua capacità di controllare e comprendere i tuoi dati in tutto il percorso tramite Platform. Ciò comporta il mantenimento della qualità dei dati, della derivazione dei dati, della catalogazione dei dati e altro ancora.

### Governance dei dati di Adobe Experience Platform {#data-governance}

In qualità di servizio Platform, la governance dei dati di Adobe Experience Platform ti consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. svolge un ruolo chiave all’interno di Experience Platform a vari livelli, tra cui l’etichettatura dell’utilizzo dei dati, le politiche di utilizzo dei dati, l’applicazione delle regole e la derivazione dei dati.

Consulta la sezione [Panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni.

### Catalogo e set di dati {#catalog}

Catalog Service è il sistema di registrazione per la posizione e la derivazione dei dati in Platform. Mentre tutti i dati acquisiti in Experience Platform vengono memorizzati nel data lake come file e directory, il servizio Catalog contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca e monitoraggio.

Il catalogo organizza i dati acquisiti nei set di dati, con ogni set di dati contenente i metadati che possono essere utilizzati per etichettare e classificare i dati in esso contenuti.

Consulta la sezione [Panoramica del servizio catalogo](../../catalog/home.md) per ulteriori informazioni sul servizio. Per scoprire come gestire i set di dati in Experience Platform, consulta la sezione [panoramica dei set di dati](../../catalog/datasets/overview.md).

## Privacy {#privacy}

La privacy è un problema critico per il tuo business, legislatori e i tuoi clienti. Poiché i dati personali raccolti dai clienti sono al centro di quasi tutti i flussi di lavoro di Experience Platform, Platform fornisce servizi per supportare queste iniziative.

### Adobe Experience Platform Privacy Service {#privacy-service}

Le normative sulla privacy legale, come il Regolamento generale sulla protezione dei dati (RGPD) dell&#39;Unione Europea e il California Consumer Privacy Act (CCPA), concedono ai cittadini all&#39;interno delle loro giurisdizioni il diritto di accedere e cancellare i dati personali raccolti e memorizzati da essi.

Adobe Experience Platform Privacy Service fornisce un’API RESTful e un’interfaccia utente per gestire queste richieste. Con Privacy Service puoi inviare richieste di accesso o cancellazione di dati di clienti privati o personali da applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

Consulta la sezione [Panoramica di Privacy Service](../../privacy-service/home.md) per ulteriori informazioni.

### Elaborazione del consenso {#consent}

Molte normative legali sulla privacy hanno introdotto requisiti per il consenso attivo e specifico in relazione alla raccolta dei dati, alla personalizzazione e ad altri casi d’uso del marketing. Per soddisfare questi requisiti, l’Experience Platform ti consente di acquisire le informazioni sul consenso nei profili dei singoli clienti e di utilizzarle come fattore determinante per l’utilizzo dei dati di ciascun cliente nei flussi di lavoro della piattaforma a valle.

Per informazioni su come elaborare i dati sul consenso e sulle preferenze dei clienti utilizzando lo standard Adobe, consulta la panoramica su [elaborazione del consenso in Experience Platform](./consent/adobe/overview.md).

Per informazioni su come elaborare i dati di consenso dei clienti in conformità con IAB Transparency and Consent Framework (TCF) 2.0, consulta la panoramica su [Supporto IAB TCF 2.0 in Platform](./consent/iab/overview.md).

## Sicurezza {#security}

L’integrità e la sicurezza dei dati sono indispensabili per la tua attività e questo rischio richiede funzionalità di sicurezza leader del settore. Per soddisfare questa sfida, Platform offre diversi strumenti per la protezione delle operazioni sui dati.

### Crittografia dei dati

Tutti i dati della piattaforma sono crittografati in transito e a riposo. Visualizza il documento in [crittografia dei dati in Platform](./encryption.md) per ulteriori informazioni.

### Controllo degli accessi {#access-control}

Experience Platform utilizza Adobe Admin Console per fornire un controllo degli accessi basato sui ruoli a varie funzionalità di Platform. Questa funzionalità sfrutta i profili di prodotto in Admin Console, che collegano gli utenti con autorizzazioni e sandbox.

Consulta la sezione [panoramica sul controllo degli accessi](../../access-control/home.md) per ulteriori informazioni.

### Sandbox {#sandboxes}

Experience Platform è progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e alla distribuzione di queste applicazioni, garantendo al contempo la conformità operativa.

Al fine di soddisfare la necessità di flessibilità di sviluppo, Experience Platform fornisce sandbox che suddividono una singola istanza Platform in ambienti virtuali separati per consentire di sviluppare le applicazioni di esperienza digitale in base al proprio ciclo di vita di sviluppo.

Consulta la sezione [panoramica sulle sandbox](../../sandboxes/home.md) per ulteriori informazioni.

## Passaggi successivi

Questo documento fornisce una panoramica dei vari servizi e strumenti di Platform che riguardano la governance dei dati, la privacy e la sicurezza. Per ulteriori informazioni su queste funzionalità, consulta la documentazione collegata a in questa guida.
