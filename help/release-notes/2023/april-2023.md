---
title: Note sulla versione di Adobe Experience Platform - Aprile 2023
description: Le note sulla versione di aprile 2023 per Adobe Experience Platform.
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: efd69011f1ba81ece0a1c270cc71b9706ab7b88f
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 4%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 aprile 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Dashboard](#dashboards)
- [Preparazione dei dati](#data-prep)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Experience Data Model](#xdm)
- [Profilo cliente in tempo reale](#profile)
- [Origini](#sources)

## Dashboard {#dashboards}

Adobe Experience Platform offre diverse dashboard attraverso le quali puoi visualizzare informazioni importanti sui dati dell’organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate** {#dashboards-new-updated-features}

| Funzione | Descrizione |
| --- | --- |
| Dashboard definiti dall&#39;utente | Ora puoi **filtrare i dati storici** dalle informazioni sui widget e utilizza dati recenti o un periodo di analisi personalizzato.<br>È inoltre possibile **duplica i widget esistenti**. Personalizzando un duplicato e modificandone gli attributi, puoi evitare di riavviare dall’inizio la creazione di un nuovo widget univoco. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere autorizzazioni di accesso e creare widget personalizzati, inizia leggendo il [panoramica delle dashboard](../../dashboards/home.md).

## Preparazione dei dati {#data-prep}

Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Aggiornamenti al periodo di backfill per Adobe Analytics nelle sandbox non di produzione. | Il periodo di backfill per Adobe Analytics nelle sandbox non di produzione è stato ridotto a tre mesi. Il backfill per le sandbox di produzione rimane invariato a 13 mesi. Questa modifica si applica solo ai nuovi flussi e non influisce sui flussi esistenti. Per ulteriori informazioni, consulta la sezione [Panoramica di Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nuova funzione di mappatura per convertire le stringhe FPID in ECID | Utilizza la `fpid_to_ecid` funzione per convertire le stringhe FPID in ECID da utilizzare nelle applicazioni Experience Platform e Experience Cloud. Per ulteriori informazioni, consulta la sezione [Guida alle funzioni di preparazione dei dati](../../data-prep/functions.md). |

{style="table-layout:auto"}

Per ulteriori informazioni su Data Prep, consulta la sezione [Panoramica sulla preparazione dei dati](../../data-prep/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che ti consentono di raccogliere i dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network dove possono essere arricchiti, trasformati e distribuiti su destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Offuscamento dell’indirizzo IP per i datastreams | È ora possibile definire opzioni di offuscamento dell’IP a livello di datastream parziali o complete nella sezione [interfaccia utente per la configurazione del datastream](../../edge/datastreams/configure.md). <br><br>L’impostazione di offuscamento dell’IP a livello di datastream ha la precedenza su qualsiasi offuscamento dell’IP configurato in Adobe Target e Audience Manager. <br><br>I dati inviati ad Adobe Analytics non sono interessati dal livello di datastream [!UICONTROL Offuscamento IP] impostazione. Al momento Adobe Analytics riceve indirizzi IP non offuscati. Affinché Analytics possa ricevere indirizzi IP offuscati, devi configurare l’offuscamento dell’IP separatamente, in Adobe Analytics. Questo comportamento verrà aggiornato nelle versioni future.<br><br> Per ulteriori dettagli sull’offuscamento dell’IP e istruzioni su come configurarlo, consulta la sezione [documentazione sulla configurazione di datastream](../../edge/datastreams/configure.md#advanced-options). |
| [Ignorare le impostazioni di configurazione del Datastream](../../edge/datastreams/overrides.md) | Ora puoi definire opzioni di configurazione aggiuntive per i datastreams, che puoi utilizzare per sostituire impostazioni specifiche, come set di dati evento, token di proprietà di Target, contenitori di sincronizzazione ID e suite di rapporti di Analytics. <br><br>L&#39;override delle configurazioni di datastream è un processo in due fasi: <ol><li>Innanzitutto, devi definire le sostituzioni della configurazione del datastream nel [pagina di configurazione di datastream](../../edge/datastreams/configure.md).</li><li>Quindi, devi inviare le sostituzioni alla rete Edge tramite un comando SDK per web o utilizzando l’SDK per web [estensione tag](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |

{style="table-layout:auto"}

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni** {#new-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] connection](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Utilizza la destinazione Coinvolgimento account Marketing Cloud Salesforce (precedentemente nota come Pardot) per acquisire, tracciare, valutare e valutare i lead. Utilizza questa destinazione per i casi d&#39;uso B2B che coinvolgono più dipartimenti e responsabili decisionali che richiedono cicli di vendita e decisionali più lunghi. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Monitoraggio del flusso di dati per [!DNL Custom Personalization] e [!DNL Adobe Commerce] destinazioni | <p> Ora puoi visualizzare le metriche di attivazione per [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md) e [Personalizzazione Personalizzata Con Attributi](../../destinations/catalog/personalization/custom-personalization.md) connessioni. </p> <p>![Immagine Adobe Commerce](/help/destinations/assets/common/adobe-commerce-metrics.png "Metriche di Adobe Commerce"){width="100" zoomable="yes"}</p>  Vedi [Monitorare i flussi di dati nell’area di lavoro Destinazioni](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) per ulteriori dettagli. |
| Nuovo **[!UICONTROL Aggiungi ID segmento al nome del segmento]** campo per [!DNL Google Ad Manager] e [!DNL Google Ad Manager 360] destinazioni | <p>Ora puoi avere il nome del segmento in [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) e [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) includi l’ID del segmento dall’Experience Platform, come segue: `Segment Name (Segment ID)`.</p><p>![Aggiungi immagine ID segmento](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Nuovo ID segmento aggiunto al campo del nome del segmento "){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}

<!--

| New **[!UICONTROL Append segment ID to segment name]** field for the [!DNL Google Ad Manager] and [!DNL Google Ad Manager 360] destinations | You can now have the segment name in [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) and [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) include the segment ID from Experience Platform, like this: `Segment Name (Segment ID)`. |
| Scheduled audience backfills | <p>For the [!DNL Google Display & Video 360] destination, the activation of audience backfills to the destination is scheduled to occur 24-48 hours after a segment is first mapped to a destination connection. This update is in response to Google's policy to wait 24 hours until ingesting data and will improve match rates between Real-time CDP and [!DNL Google Display & Video 360].</p> <p>Note that this is a backend configuration applicable to this destination only and that is unrelated to any customer-configurable scheduling options in the UI.</p> |

-->


**Correzioni e miglioramenti** {#destinations-fixes-and-enhancements}

- È stato risolto un problema nel **Identità escluse** metriche di reporting per esportazioni di destinazione basate su file. I clienti ricevevano tutti gli ID esportati dall’esportazione attivata come previsto. Tuttavia, **Identità escluse** la metrica di reporting nell’interfaccia utente mostrava erroneamente un numero elevato di identità escluse a causa di un conteggio errato delle identità che non avrebbero mai dovuto essere esportate. (PLAT-149774)
- È stato risolto un problema nel **Pianificazione** passaggio del flusso di lavoro di attivazione. Per le destinazioni che richiedono un ID di mappatura, i clienti non sono stati in grado di aggiungere un ID di mappatura per i segmenti aggiunti alle connessioni di destinazione esistenti. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Mostra/Nascondi nomi | L’Editor schema ora consente di alternare tra i nomi dei campi originali e i nomi visualizzati più leggibili. Questa flessibilità consente di migliorare la reperibilità dei campi e la modifica degli schemi. I nomi visualizzati per i gruppi di campi standard vengono generati dal sistema, ma possono anche essere personalizzati tramite l’interfaccia utente, se necessario. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Scadenza dati profilo pseudonimi | La scadenza dei dati del profilo pseudonimo è ora disponibile in generale! Questa versione rimuoverà continuamente dall’istanza di Experience Platform i profili pseudonimi non aggiornati una volta abilitati. Per saperne di più su questa funzione e su Profili pseudonimi, si prega di leggere [Guida alla scadenza dei dati di profilo pseudonimo](../../profile/pseudonymous-profiles.md). |

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e consente di strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto API per il filtraggio dei dati a livello di riga per Microsoft Dynamics, Salesforce CRM e il Marketing Cloud Salesforce | Utilizza gli operatori logici e di confronto per filtrare i dati a livello di riga per le origini di Marketing Cloud Microsoft Dynamics, Salesforce CRM e Salesforce. Leggi la guida su [filtraggio dei dati per una sorgente tramite API](../../sources/tutorials/api/filter.md) per ulteriori informazioni. |
| Disponibilità beta dello streaming Shopify | La [Shopify Streaming source](../../sources/connectors/ecommerce/shopify-streaming.md) è ora disponibile in versione beta. Utilizza l’origine Shopify Streaming per inviare ad Experience Platform i dati dall’account Shopify Partners. |
| Disponibilità generale dell&#39;integrazione OneTrust | La [Origine integrazione OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) è ora GA. Utilizza l&#39;origine di integrazione OneTrust per fornire ad Experience Platform i dati di consenso e preferenze dall&#39;account di integrazione OneTrust. |
| Disponibilità generale di Oracle Service Cloud | La [Origine Oracle Service Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md) è ora GA. Utilizza l’origine Oracle Service Cloud per riportare ad Experience Platform i dati di Oracle Service Cloud . |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md).
