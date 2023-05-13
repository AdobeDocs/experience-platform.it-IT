---
title: Note sulla versione di Adobe Experience Platform
description: Le note sulla versione di aprile 2023 per Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e3fc587d924b2183806918f91e5ae3aa3fee52f3
workflow-type: tm+mt
source-wordcount: '2094'
ht-degree: 4%

---

# Note sulla versione di Adobe Experience Platform

>[!IMPORTANT]
>
>A partire dal 15 maggio 2023, il `Existing` lo stato verrà rimosso dalla mappa dell’appartenenza al segmento per rimuovere la ridondanza nel ciclo di vita dell’appartenenza al segmento. Dopo questa modifica, i profili qualificati in un segmento verranno rappresentati come `Realized` e i profili squalificati continueranno a essere rappresentati come `Exited`. Per ulteriori dettagli su questa modifica, consulta la sezione [Sezione Servizio di segmentazione](#segmentation).

**Data di rilascio: 26 aprile 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Dashboard](#dashboards)
- [Preparazione dei dati](#data-prep)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Experience Data Model](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [Profilo cliente in tempo reale](#profile)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Dashboard {#dashboards}

Adobe Experience Platform offre diverse dashboard attraverso le quali puoi visualizzare informazioni importanti sui dati dell’organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate** {#dashboards-new-updated-features}

| Funzione | Descrizione |
| --- | --- |
| Dashboard definiti dall&#39;utente | Ora puoi **filtrare i dati storici** dalle informazioni sui widget e utilizza dati recenti o un periodo di analisi personalizzato. Consulta la sezione [guida alle dashboard definite dall&#39;utente](../../dashboards/user-defined-dashboards.md#filter-historical-data) per ulteriori informazioni.<br>È inoltre possibile **duplica i widget esistenti**. Personalizzando un duplicato e modificandone gli attributi, puoi evitare di riavviare dall’inizio la creazione di un nuovo widget univoco. Leggi la sezione [guida alla duplicazione dei widget](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) per saperne di più. |

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
| Segreto JWT OAuth | La [Segreto JWT OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) consente ai clienti di utilizzare token Adobe e Google Service per supportare le interazioni server-to-server in Event Forwarding. |
| [!DNL Pinterest Conversions API] Estensione | La [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) l’estensione di inoltro eventi consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e inviarli a [!DNL Pinterest] sotto forma di eventi lato server che utilizzano [!DNL Pinterest Conversions API]. |

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
| Backfill pianificati del pubblico | <p>Per [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) destinazione , l’attivazione dei backfills del pubblico alla destinazione è pianificata per 24-48 ore dopo che un segmento è stato mappato per la prima volta a una connessione di destinazione. Questo aggiornamento risponde al criterio di Google di attendere 24 ore fino all’acquisizione dei dati e migliorerà i tassi di corrispondenza tra Real-time CDP e [!DNL Google Display & Video 360].</p> <p>Si tratta di una configurazione back-end applicabile solo a questa destinazione e non correlata a nessuna opzione di pianificazione configurabile dal cliente nell’interfaccia utente.</p> |

{style="table-layout:auto"}

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
| Mostra/Nascondi nomi | L’Editor schema ora consente di alternare tra i nomi dei campi originali e i nomi visualizzati più leggibili.<br>![L’Editor schema con il nome visualizzato evidenziato.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Icona dell’Editor di schema"){width="100" zoomable="yes"}<br>Questa flessibilità consente di migliorare la reperibilità dei campi e la modifica degli schemi. I nomi visualizzati per i gruppi di campi standard vengono generati dal sistema, ma possono anche essere personalizzati tramite l’interfaccia utente, se necessario. Per piacere, leggi le [documentazione di attivazione/disattivazione nome visualizzato](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) per saperne di più. |

{style="table-layout:auto"}

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Schema | [[!UICONTROL Campi di classificazione Adobe Target]](https://github.com/adobe/xdm/pull/1719/files) | Un nuovo schema XDM per i set di dati di classificazione di Target contenente un set di campi di metadati per classificare attività ed esperienze di Target. |

{style="table-layout:auto"}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [[!UICONTROL Estensione dell’unione dell’account del servizio di profilo unificato di Adobe]](https://github.com/adobe/xdm/pull/1696/files) | È stato aggiunto un gruppo di campi di estensione dell’account per Profilo cliente in tempo reale che consente agli utenti di aggiungere l’iscrizione al segmento nell’unione account. |
| Schema | [[!UICONTROL Schema di sistema degli attributi calcolati]](https://github.com/adobe/xdm/pull/1696/files) | Il gruppo di campi Attributi calcolati utilizzato da Profilo cliente in tempo reale è stato aggiornato a uno schema globale di sola lettura del sistema. |
| Gruppo di campi | Multipli | Sono stati aggiunti diversi eventi come campi per [[!UICONTROL Schema della serie temporale]](https://github.com/adobe/xdm/pull/1718/files). |
| Gruppo di campi | Dettagli fedeltà profilo | [È stato corretto il titolo](https://github.com/adobe/xdm/pull/1717/files) per `xdm:upgradeDate` da &quot;Nome programma&quot; a &quot;Data di aggiornamento&quot;. |
| Gruppo di campi | Multipli | Diversi campi da [[!UICONTROL Elemento decisionale]](https://github.com/adobe/xdm/pull/1714/files) sono stati aggiornati per rimuovere la gerarchia nidificata doppia. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Real-Time Customer Data Platform

Basato su Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) consente alle aziende di unire dati noti e sconosciuti per attivare i profili dei clienti con decisioni intelligenti in tutto il percorso di clienti. [!DNL Real-Time CDP] combina più origini dati aziendali per creare profili cliente in tempo reale. I segmenti generati da questi profili possono quindi essere inviati a destinazioni downstream per fornire esperienze cliente personalizzate uno-a-uno su tutti i canali e dispositivi.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Home page Real-Time CDP ottimizzata | La [Home page di Real-Time CDP](https://experience.adobe.com) è stato migliorato con un aspetto rinfrescato e prestazioni migliorate. La home page ora è consapevole delle autorizzazioni e presenterà widget relativi alle funzioni a cui hai accesso. Per ulteriori informazioni, consulta la sezione [Panoramica del dashboard della pagina Home di Real-Time CDP](../../rtcdp/home-page-dashboards.md). |
| Sondaggio di autoidentificazione | Il sondaggio di identificazione automatica è un breve questionario presentato nella home page dell’interfaccia utente di Adobe Experience Platform. Utilizza il sondaggio di auto-identificazione per creare il tuo profilo personale Experience Platform e ricevere linee guida personalizzate in base alle tue selezioni. Per ulteriori informazioni, consulta la sezione [panoramica del sondaggio di identificazione automatica](../../landing/self-identification.md). |

Per ulteriori informazioni su [!DNL Real-Time CDP], vedi [[!DNL Real-Time CDP] panoramica](../../rtcdp/overview.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Scadenza dati profilo pseudonimi | La scadenza dei dati del profilo pseudonimo è ora disponibile in generale! Questa versione rimuoverà continuamente dall’istanza di Experience Platform i profili pseudonimi non aggiornati una volta abilitati. Per saperne di più su questa funzione e su Profili pseudonimi, si prega di leggere [Guida alla scadenza dei dati di profilo pseudonimo](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Mappa di appartenenza al segmento | In seguito all’annuncio precedente del 15 febbraio 2023, il `Existing` lo stato verrà rimosso dalla mappa dell’appartenenza al segmento per rimuovere la ridondanza nel ciclo di vita dell’appartenenza al segmento. Dopo questa modifica, i profili qualificati in un segmento verranno rappresentati come `Realized` e i profili squalificati continueranno a essere rappresentati come `Exited`.<br/><br/> Questa modifica potrebbe interessarti se utilizzi [destinazioni aziendali](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) e potrebbero avere in atto processi downstream automatizzati basati su `Existing` stato. Se questo è il caso per te, controlla le tue integrazioni downstream. Se sei interessato a identificare i nuovi profili qualificati oltre un certo periodo di tempo, considera l&#39;utilizzo di una combinazione dei `Realized` lo stato e `lastQualificationTime` nella mappa di appartenenza al segmento. Per ulteriori informazioni, contatta il tuo rappresentante Adobe. |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], vedi [Panoramica sulla segmentazione](../../segmentation/home.md).

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