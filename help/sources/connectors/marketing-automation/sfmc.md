---
title: Panoramica Di Salesforce Marketing Cloud (V2) Source
description: Scopri come collegare Salesforce Marketing Cloud (V2) a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2025-02-02T00:00:00Z
source-git-commit: 4d47eae91711596677335b03568add9f6fbade74
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# Panoramica sull&#39;origine di [!DNL Salesforce Marketing Cloud] (V2)

>[!IMPORTANT]
>
>L&#39;origine [[!DNL Salesforce Marketing Cloud] (V1)](salesforce-marketing-cloud.md) originale è stata rimossa a gennaio 2026. Nessuna migrazione disponibile per questa origine obsoleta. È necessario implementare nuovamente i dati utilizzando la nuova origine [!DNL Salesforce Marketing Cloud] (V2).

L&#39;integrazione tra Adobe [Real-Time CDP](../../../rtcdp/overview.md) e [!DNL Salesforce Marketing Cloud] è progettata per sfruttare le estensioni dati a causa della flessibilità e del controllo che forniscono. A differenza delle tabelle di sistema standard (visualizzazioni dati e oggetti incorporati), che sono limitate a campi predefiniti e servono principalmente per il tracciamento a livello di sistema, è possibile utilizzare le estensioni dati per definire campi personalizzati, organizzare un’ampia varietà di dati specifici per l’azienda e personalizzare le strutture di dati per soddisfare requisiti specifici.

A causa di questo livello di personalizzazione e scalabilità, l&#39;integrazione tra Real-Time CDP e [!DNL Salesforce Marketing Cloud] si basa sulle estensioni dati anziché sulle tabelle di sistema standard. Questo approccio offre una base più flessibile, scalabile e integrata per la gestione dei dati, garantendo che siano in linea con gli obiettivi aziendali

È possibile utilizzare l&#39;origine [!DNL Salesforce Marketing Cloud] per connettere l&#39;account [!DNL Salesforce Marketing Cloud] a Real-Time CDP e Adobe Experience Platform. Per informazioni su come iniziare, leggi la documentazione sottostante.

## Esempi di casi d’uso {#use-case-examples}

### Personalizzazione delle campagne e-mail con i dati dei contatti

Un brand di vendita al dettaglio desidera personalizzare le campagne e-mail in base alle fasi del ciclo di vita del cliente (ad esempio, nuovo cliente, acquirente ripetuto, cliente fedele). A questo scopo, crea un’estensione per i dati di contatto in cui memorizzare le informazioni chiave del cliente, tra cui nome, e-mail, fase del ciclo di vita e comportamento di acquisto. Questi dati vengono quindi acquisiti in Experience Platform per una segmentazione e un targeting più approfonditi.

Acquisendo i dati dall’estensione Contact Data in Experience Platform, il brand può segmentare i clienti in base alla loro fase del ciclo di vita e al comportamento di acquisto. Ad esempio, possono inviare un’offerta di benvenuto ai nuovi clienti, un premio di fedeltà agli acquirenti ripetuti o persino coinvolgere nuovamente i clienti inattivi con offerte mirate. Questo approccio garantisce una comunicazione personalizzata e consente un coinvolgimento più pertinente ed efficace dei clienti.

### Acquisizione dei dati della campagna per la segmentazione personalizzata

Un team di marketing desidera ottimizzare le campagne e-mail indirizzando i clienti in base al loro coinvolgimento con le campagne precedenti. A questo scopo, crea un&#39;estensione dati di Campaign in [!DNL Salesforce Marketing Cloud] per memorizzare i dati sul coinvolgimento dei clienti, ad esempio le aperture delle e-mail, i clic e le risposte alle campagne. Questi dati vengono quindi acquisiti in Experience Platform per ulteriore segmentazione e personalizzazione.

Acquisendo questi dati dall’estensione dati di Campaign in Experience Platform, il team marketing può segmentare i clienti in base al coinvolgimento passato, ad esempio coloro che hanno fatto clic sulle offerte di prodotto o hanno risposto positivamente. I clienti che hanno partecipato possono ricevere promozioni mirate nelle e-mail future, mentre quelli che hanno risposto negativamente possono ricevere follow-up del servizio clienti. Questa integrazione con Experience Platform garantisce che il team di marketing possa fornire contenuti più personalizzati e rilevanti in base al comportamento del cliente.

### Targeting dei clienti in base ai dati delle attività

Un team di marketing desidera eseguire il targeting dei clienti in base alle loro attività, ad esempio visite al sito web, invio di moduli o interazioni con campagne e-mail precedenti. A questo scopo, crea un’estensione dati Activities per memorizzare informazioni sulle attività di coinvolgimento di ciascun cliente. Questi dati vengono quindi acquisiti in Experience Platform per ulteriore segmentazione e targeting personalizzato delle campagne.

Acquisendo i dati dall’estensione dati Activities in Experience Platform, il team marketing può segmentare i clienti in base alla cronologia del coinvolgimento. Ad esempio, ai clienti che hanno visitato di recente il sito web ma non hanno completato un acquisto possono essere inviate e-mail di promemoria con offerte speciali. Allo stesso modo, i clienti che hanno compilato un modulo possono ricevere comunicazioni di follow-up personalizzate. Questo approccio assicura che ogni cliente riceva contenuti rilevanti in base alle sue attività più recenti, migliorando i tassi di coinvolgimento e conversione.

## Prerequisiti {#prerequisites}

Leggi le sezioni seguenti per informazioni sui prerequisiti da completare per connettere l’origine ad Experience Platform.

### Imposta l&#39;applicazione per l&#39;autenticazione {#set-up-application-for-authentication}

Durante la creazione di un&#39;integrazione con [!DNL Salesforce Marketing Cloud], uno dei primi passaggi consiste nel creare un **pacchetto installato** in [!DNL Salesforce Marketing Cloud]. Il pacchetto installato genera le credenziali client necessarie per autenticare le chiamate API, definisce il tipo di integrazione e gli ambiti di autorizzazione associati. Inoltre, il pacchetto installato fornisce gli endpoint API corretti per il tenant. Funge anche da contenitore gestito per l’amministrazione, il monitoraggio e la revoca dell’accesso, garantendo che tutte le integrazioni siano sicure, verificabili e allineate al modello di autenticazione consigliato da Salesforce.

Per creare un pacchetto installato, utilizzare l&#39;interfaccia utente [!DNL Salesforce Marketing Cloud], passare a **[!DNL Setup]** > **[!DNL Apps]** > **[!DNL Installed Packages]** e selezionare **[!DNL New]**. Utilizzare l&#39;interfaccia [!DNL New Package Details] per fornire un nome e informazioni per il pacchetto. Al termine, selezionare **[!DNL Save]**.

![Nuova interfaccia pacchetto dell&#39;interfaccia utente di Salesforce Marketing Cloud.](../../images/tutorials/create/sfmc/new-package.png)

Una volta creato il nuovo pacchetto, selezionare **[!DNL Add Component]**.

![Interfaccia Aggiungi componente dell&#39;interfaccia utente di Salesforce Marketing Cloud.](../../images/tutorials/create/sfmc/add-component.png)

Seleziona **[!DNL API Integration]** come tipo di componente.

![Finestra di selezione dei componenti con &quot;Integrazione API&quot; selezionata.](../../images/tutorials/create/sfmc/api-integration.png)

Seleziona **[!DNL Server-to-Server]** come tipo di integrazione.

![Finestra di selezione del tipo di integrazione](../../images/tutorials/create/sfmc/server-to-server.png)

Infine, passare a **[!DNL Scope]** > **[!DNL Data]**. In **[!DNL Data Extensions]**, selezionare **[!DNL Read]**.

![Sezione estensioni dati dell&#39;ambito in Salesforce Marketing](../../images/tutorials/create/sfmc/data-extensions.png)

Seleziona **[!DNL Save]**, quindi copia e salva il **segreto client**. Al termine, selezionare **[!DNL Finish]**.

![Finestra di Salesforce Marketing Cloud per la generazione di un segreto client.](../../images/tutorials/create/sfmc/generate-secret.png)

Prima di uscire dall&#39;interfaccia utente [!DNL Salesforce Marketing Cloud], copiare l&#39;**ID client** e il **prefisso URI di base univoco**, in quanto verranno utilizzati entrambi i valori per creare una connessione ad Experience Platform. Per l&#39;URI di base di autenticazione, assicurarsi di rimuovere tutto dopo `.auth.marketingcloudapis.com/`

![Interfaccia dei componenti di Salesforce Marketing Cloud in cui è possibile recuperare l&#39;ID client e l&#39;URI di base univoco.](../../images/tutorials/create/sfmc/client-id-and-uri.png)

Per i passaggi dettagliati sulla creazione di un pacchetto installato, consulta la [[!DNL Salesforce] documentazione](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-developer-basics/set-up-your-developer-environment).

### Raccogli le credenziali richieste {#gather-required-credentials}

Per connettere [!DNL Salesforce Marketing Cloud] ad Experience Platform è necessario fornire i valori per le credenziali seguenti.

| Credenziali | Descrizione |
| --- | --- |
| ID client | L&#39;identificatore pubblicamente esposto utilizzato da [!DNL Salesforce Marketing Cloud] per identificare l&#39;account quando si autorizza Experience Platform. L&#39;ID client può essere recuperato dal pannello dei componenti dell&#39;interfaccia utente [!DNL Salesforce Marketing Cloud]. |
| Segreto client | Chiave riservata nota solo all&#39;applicazione client e al server di autorizzazione. Puoi generare il segreto client seguendo i [passaggi di configurazione dell&#39;applicazione descritti in precedenza](#set-up-application-for-authentication). |
| Endpoint base | Prefisso dell&#39;URI di base per l&#39;autenticazione per [!DNL Salesforce Marketing Cloud]. |

{style="table-layout:auto"}

## Connetti [!DNL Salesforce Marketing Cloud] ad Experience Platform

Procedi alla configurazione della connessione di origine [!DNL Salesforce Marketing Cloud] in Experience Platform. Per una guida dettagliata sulla configurazione della connessione tramite l&#39;interfaccia utente, consulta l&#39;[esercitazione](../../tutorials/ui/create/marketing-automation/sfmc.md). Leggi questa esercitazione per scoprire come connettere il tuo account [!DNL Salesforce Marketing Cloud], selezionare dati, mappare campi, pianificare acquisizioni e monitorare i flussi di dati.
