---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2024
description: Note sulla versione di Adobe Experience Platform di gennaio 2024.
source-git-commit: 88dc2fc84002ae4400e4a11370ac3354cd38cd0e
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 40%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: mercoledì 30 gennaio 2024**

Nuove funzioni di Adobe Experience Platform:

- [Playbook di casi d’uso](#use-case-playbooks)

Aggiornamenti alle funzioni esistenti in Experienci Platform:

- [Dashboard](#dashboards)
- [Preparazione dei dati](#data-prep)
- [Destinazioni](#destinations)
- [Real-Time Customer Data Platform](#rtcdp)
- [Profilo cliente in tempo reale](#profile)
- [Origini](#sources)

## Playbook di casi d’uso {#use-case-playbooks}

Il [!UICONTROL Playbook di casi d’uso] Questa funzionalità è ora generalmente disponibile per tutti i clienti Real-Time CDP e Adobe Journey Optimizer. [!UICONTROL Playbook di casi d’uso] sono progettati per aiutare gli utenti a superare le sfide quando iniziano con Real-time Customer Data Platform o Adobe Journey Optimizer. Quando non sai da dove iniziare o come creare le risorse giuste per i casi d’uso desiderati, i playbook basati su casi d’uso ti forniscono ispirazione e creano diverse risorse da testare e importare negli ambienti di produzione quando sono pronti.

Per iniziare a utilizzare [!UICONTROL Playbook di casi d’uso], leggi le seguenti pagine della documentazione:

- Leggi le [pagina panoramica](/help/use-case-playbooks/playbooks/overview.md) per comprendere lo scopo, le informazioni sulla disponibilità e per ottenere una dimostrazione end-to-end del funzionamento dei playbook, dall’individuazione alla creazione di istanze, fino all’importazione di risorse generate in altri ambienti sandbox.
- Ottieni un elenco di tutti [playbook disponibili](/help/use-case-playbooks/playbooks/playbooks-list.md), raggruppati per prodotto (Real-Time CDP o Journey Optimizer)
- Ottieni informazioni su tutte le [autorizzazioni richieste](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) per utilizzare i playbook e le risorse generate dai playbook.
- Comprendere la [funzionalità di riconoscimento dei dati](/help/use-case-playbooks/playbooks/data-awareness.md) che consente di copiare le risorse generate in altri ambienti sandbox
- Ottenere [suggerimenti per la risoluzione dei problemi](/help/use-case-playbooks/playbooks/troubleshooting.md) se si verificano errori o difficoltà durante l&#39;utilizzo dei playbook di Use Case.

## Preparazione dei dati {#data-prep}

La preparazione dei dati consente ai data engineer di mappare, trasformare e convalidare i dati da e per Experience Data Model (XDM).

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove funzioni di mappatura | <ul><li>`object_to_map`: utilizza `object_to_map` funzione per creare tipi di dati mappa. Questa funzione supporta diverse sintassi. Per ulteriori informazioni, consulta la guida su [funzioni per gerarchie - oggetti](../../data-prep/functions.md#objects). </li><li>`to_map`: utilizza `to_map` per creare una mappa con le coppie di nome campo e valore specificate utilizzando gli oggetti. Per ulteriori informazioni, consulta la guida su [funzioni per gerarchie - mappe](../../data-prep/functions.md#objects). </li><li>`array_to_map`: utilizza `array_to_map` funzione per creare una mappa con coppie di nome campo e valore specificate utilizzando matrici di oggetti. Per ulteriori informazioni, consulta la guida su [funzioni per gerarchie - mappe](../../data-prep/functions.md#objects). |

{style="table-layout:auto"}

Per ulteriori informazioni sulla preparazione dati, consulta [Panoramica sulla preparazione dati](../../data-prep/home.md).

## Dashboard {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Visualizza SQL | Ora puoi visualizzare le istruzioni SQL sottostanti i profili, i tipi di pubblico, le destinazioni e le informazioni personalizzate, quindi eseguire la query su richiesta tramite l’editor delle query. Ispirati all’SQL di oltre 40 informazioni esistenti per creare nuove query che derivano informazioni univoche dai dati di Platform in base alle esigenze aziendali. Per ulteriori informazioni, consulta la guida su [visualizzazione di insight SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni** {#new-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [Connessione pubblica](../../destinations/catalog/advertising/pubmatic.md) | Utilizza questa destinazione per inviare i dati del pubblico a [!DNL PubMatic Connect] piattaforma. |

{style="table-layout:auto"}

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Basato su Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) consente alle aziende di unire dati noti e sconosciuti per attivare i profili cliente con decisioni intelligenti in tutto il percorso del cliente. [!DNL Real-Time CDP] combina più origini dati aziendali per creare profili cliente in tempo reale. I segmenti generati da questi profili possono quindi essere inviati alle destinazioni a valle per fornire esperienze cliente personalizzate individuali su tutti i canali e i dispositivi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Aggiornamenti a [Home page di Real-Time CDP](https://experience.adobe.com) | <ul><li>**Widget profili**: ora puoi utilizzare il widget Profili per passare alla pagina Panoramica profili e visualizzare le metriche Profilo della tua organizzazione.</li><li>**Scheda delle metriche del profilo**: la scheda Metriche profilo nel dashboard della pagina principale ora visualizza il conteggio totale dei profili nell’organizzazione, a seconda del rispettivo criterio di unione.</li><li>**Widget schemi**: ora puoi utilizzare il widget schemi per passare al flusso di lavoro di creazione dello schema nell’interfaccia utente.</li></ul> |

Per ulteriori informazioni su Real-Time CDP, consulta [Panoramica di Real-Time CDP](../../rtcdp/overview.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati clienti in una visualizzazione unificata che offre un account utilizzabile e dotato di marca temporale per ogni interazione con il cliente.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Sono stati apportati miglioramenti alla localizzazione delle schede dashboard predefinite del visualizzatore di profili | Le schede di profilo predefinite ora avranno nomi localizzati in modo dinamico. Le schede di profilo personalizzate possono continuare ad avere nomi personalizzati che possono essere modificati. |

{style="table-layout:auto"}

Per ulteriori informazioni su Real-Time Customer Profile, consulta [Panoramica del profilo](../../profile/home.md)

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL Oracle NetSuite] sorgenti | Utilizza il [!DNL Oracle NetSuite] integrazioni nel catalogo sorgenti per estrarre i dati dalla [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) e [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) account di Experience Platform. |
| [!BADGE Beta]{type=Informative}[!DNL Braze Currents] sorgente | Utilizza il [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) nel catalogo delle origini per importare i dati dal [!DNL Braze] da Experience Platform. |
| Supporto per l’autenticazione con coppia di chiavi [!DNL Snowflake] origine batch | È ora possibile utilizzare l’autenticazione con coppia di chiavi durante la creazione di una nuova [!DNL Snowflake] conto per i dati batch. Per ulteriori informazioni, consulta la guida su [creazione di [!DNL Snowflake] account tramite l’API](../../sources/tutorials/api/create/databases/snowflake.md) oppure la guida su [creazione di [!DNL Snowflake] account tramite l’interfaccia utente](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sources/home.md).