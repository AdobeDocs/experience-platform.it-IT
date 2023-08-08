---
title: Note sulla versione di Adobe Experience Platform - Aprile 2023
description: Note sulla versione di Adobe Experience Platform di aprile 2023.
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 100%

---

# Note sulla versione di Adobe Experience Platform

>[!IMPORTANT]
>
>A partire dal 15 maggio 2023, lo stato `Existing` verrà rimosso dalla mappa di appartenenza al segmento per rimuovere la ridondanza nel ciclo di vita dell’appartenenza al segmento. Dopo questa modifica, i profili qualificati in un segmento verranno rappresentati come `Realized` e i profili non qualificati continueranno a essere rappresentati come `Exited`. Per ulteriori informazioni su questa modifica, consulta la [sezione sul Servizio di segmentazione](#segmentation).

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

Adobe Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate** {#dashboards-new-updated-features}

| Funzione | Descrizione |
| --- | --- |
| Dashboard definite dall’utente | Ora puoi **filtrare i dati storici** dalle informazioni approfondite sul widget e utilizzare i dati recenti o un periodo di analisi personalizzato. Per ulteriori informazioni, consulta la [guida per le dashboard definite dall’utente](../../dashboards/user-defined-dashboards.md#filter-historical-data).<br>Ora puoi anche **duplicare i widget esistenti**. Personalizzando un duplicato e modificandone gli attributi, puoi evitare di ricominciare dall’inizio durante la creazione di un nuovo widget specifico. Per ulteriori informazioni, consulta la [guida sulla duplicazione dei widget](../../dashboards/user-defined-dashboards.md#duplicate-a-widget). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Preparazione dei dati {#data-prep}

La preparazione dei dati consente ai data engineer di mappare, trasformare e convalidare i dati da e per Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Aggiornamenti al periodo di retrocompilazione per Adobe Analytics nelle sandbox non di produzione | Il periodo di retrocompilazione per Adobe Analytics nelle sandbox non di produzione è stato ridotto a tre mesi. La retrocompilazione per le sandbox di produzione rimane di 13 mesi. Questa modifica si applica solo ai nuovi flussi e non influirà sui flussi esistenti. Per ulteriori informazioni, consulta la [Panoramica su Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nuova funzione di mappatura per convertire le stringhe FPID in ECID | Utilizza la funzione `fpid_to_ecid` per convertire le stringhe FPID in ECID e utilizzarle in applicazioni Experience Platform e Experience Cloud. Per ulteriori informazioni, consulta la [Guida alle funzioni di preparazione dati](../../data-prep/functions.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulla preparazione dati, consulta la [Panoramica sulla preparazione dati](../../data-prep/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Offuscamento dell’indirizzo IP per gli stream di dati | Ora puoi definire le opzioni di offuscamento parziale o completo dell’IP a livello di dati nell’[interfaccia utente per la configurazione dello stream di dati](../../datastreams/configure.md). <br><br>L’impostazione di offuscamento dell’IP a livello di stream di dati ha la precedenza su qualsiasi offuscamento dell’IP configurato in Adobe Target e Audience Manager. <br><br>I dati inviati ad Adobe Analytics non sono influenzati dall’impostazione dell’[!UICONTROL Offuscamento IP] a livello di stream di dati. Adobe Analytics attualmente riceve indirizzi IP non offuscati. Affinché Analytics possa ricevere indirizzi IP offuscati, l’offuscamento dell’IP deve essere configurato separatamente in Adobe Analytics. Questo comportamento verrà aggiornato nelle versioni future.<br><br> Per ulteriori dettagli sull’offuscamento dell’IP e istruzioni su come configurarlo, consulta la [documentazione sulla configurazione dello stream di dati](../../datastreams/configure.md#advanced-options). |
| [Override della configurazione dello stream di dati](../../datastreams/overrides.md) | Ora puoi definire opzioni di configurazione aggiuntive per i flussi di dati, che puoi utilizzare per ignorare impostazioni specifiche, ad esempio set di dati evento, il token di proprietà Target, i contenitori di sincronizzazione ID e la suite di rapporti Analytics. <br><br>L’override delle configurazioni dello stream di dati è un processo in due fasi: <ol><li>Innanzitutto, devi definire gli override della configurazione dello stream di dati nella [pagina di configurazione dello stream di dati](../../datastreams/configure.md).</li><li>Quindi, devi inviare gli override alla rete Edge tramite un comando Web SDK o utilizzando l’[estensione tag](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) di Web SDK.</li></ol> |
| Segreto JWT OAuth  | Il [Segreto JWT OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=it) consente di utilizzare i token di servizio Adobe e Google per supportare le interazioni da server a server nell’inoltro degli eventi. |
| Estensione [!DNL Pinterest Conversions API] | L’estensione per l’inoltro degli eventi [[!DNL Pinterest Conversions API]](ttps://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=it) consente di sfruttare i dati acquisiti nella rete Edge di Adobe Experience Platform e di inviarli a [!DNL Pinterest] in forma di eventi lato server che utilizzano [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni** {#new-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] connessione](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Utilizza la destinazione Marketing Cloud Account Engagement (precedentemente nota come Pardot) per acquisire, tracciare, dare un punteggio e valutare i lead. Utilizza questa destinazione per i casi d’uso B2B che coinvolgono più dipartimenti e decision maker e che richiedono cicli di vendita e decisionali più lunghi. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Monitoraggio del flusso di dati per le destinazioni [!DNL Custom Personalization] e [!DNL Adobe Commerce] | <p> Ora puoi visualizzare le metriche di attivazione per le connessioni di [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md) e [Personalizzazione personalizzata con attributi](../../destinations/catalog/personalization/custom-personalization.md). </p> <p>![Immagine di Adobe Commerce](/help/destinations/assets/common/adobe-commerce-metrics.png "Metriche di Adobe Commerce"){width="100" zoomable="yes"}</p>  Per ulteriori informazioni, consulta [Monitorare i flussi di dati nell’area di lavoro Destinazioni](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace). |
| Nuovo campo **[!UICONTROL Aggiungi ID segmento al nome del segmento]** per le destinazioni [!DNL Google Ad Manager] e [!DNL Google Ad Manager 360] | <p>Ora il nome del segmento in [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) e [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) può includere l’ID di segmento da Experience Platform, come segue: `Segment Name (Segment ID)`.</p><p>![Aggiungi immagine a ID segmento](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Nuovo campo Aggiungi ID segmento al nome del segmento "){width="100" zoomable="yes"}</p> |
| Retrocompilazioni del pubblico pianificate | <p>Per la destinazione [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics), l’attivazione delle retrocompilazioni del pubblico alla destinazione è programmata per verificarsi 24-48 ore dopo che un segmento è stato mappato per la prima volta a una connessione di destinazione. Questo aggiornamento risponde ai criteri di Google di attendere 24 ore prima dell’acquisizione dei dati e migliorerà le percentuali di corrispondenza tra Real-time CDP e [!DNL Google Display & Video 360].</p> <p>Tieni presente che si tratta di una configurazione back-end applicabile solo a questa destinazione e che non è correlata ad alcuna opzione di pianificazione configurabile dalla clientela nell’interfaccia utente.</p> |

{style="table-layout:auto"}

**Correzioni di problemi e miglioramenti** {#destinations-fixes-and-enhancements}

- È stato risolto un problema nelle metriche di reporting **Identità escluse** per esportazioni di destinazioni basate su file. La clientela riceveva tutti gli ID esportati dall’esportazione attivata come previsto. Tuttavia, la metrica di reporting **Identità escluse** nell’interfaccia utente mostrava erroneamente un numero elevato di identità escluse a causa di un conteggio errato di identità che non dovevano mai essere esportate. (PLAT-149774)
- È stato risolto un problema nel passaggio **Pianificazione** del flusso di lavoro di attivazione. Per le destinazioni che richiedono un ID di mappatura, la clientela non era in grado di aggiungere un ID di mappatura per i segmenti aggiunti alle connessioni di destinazione esistenti. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Attivare/disattivare nomi visualizzati | L’Editor di schema ora fornisce un’opzione per passare dai nomi di campo originali a quelli in forma leggibile.<br>![Editor di schema con l’attivazione/disattivazione del nome visualizzato evidenziata.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Attivazione/disattivazione nome visualizzato nell’Editor schema"){width="100" zoomable="yes"}<br>Questa flessibilità migliora l’individuazione del campo e la modifica degli schemi. I nomi visualizzati per i gruppi di campi standard sono generati dal sistema, ma possono anche essere personalizzati tramite l’interfaccia utente, se necessario. Per ulteriori informazioni, consulta la [documentazione sull’attivazione/disattivazione del nome visualizzato](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=it#display-name-toggle). |

{style="table-layout:auto"}

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Schema | [[!UICONTROL Campi di classificazione Adobe Target]](https://github.com/adobe/xdm/pull/1719/files) | Un nuovo schema XDM per i set di dati di classificazione di Target contenente un set di campi di metadati per classificare le attività ed esperienze di Target. |

{style="table-layout:auto"}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [[!UICONTROL Estensione di unione degli account del servizio profili unificato di Adobe]](https://github.com/adobe/xdm/pull/1696/files) | È stato aggiunto un gruppo di campi di estensione account per il Profilo cliente in tempo reale che consente agli utenti di aggiungere l’appartenenza al segmento nell’unione account. |
| Schema | [[!UICONTROL Schema di sistema per attributi calcolati]](https://github.com/adobe/xdm/pull/1696/files) | Il gruppo di campi Attributi calcolati utilizzato dal Profilo cliente in tempo reale è stato aggiornato a uno schema globale del sistema di sola lettura. |
| Gruppo di campi | Multiplo | Sono stati aggiunti diversi eventi come campi per lo [[!UICONTROL Schema della serie temporale]](https://github.com/adobe/xdm/pull/1718/files). |
| Gruppo di campi | Dettagli fedeltà profilo | [È stato corretto il titolo](https://github.com/adobe/xdm/pull/1717/files) per `xdm:upgradeDate` da “Nome programma” a “Data aggiornamento”. |
| Gruppo di campi | Multiplo | Diversi campi dell’[[!UICONTROL Elemento decisione]](https://github.com/adobe/xdm/pull/1714/files) sono stati aggiornati per rimuovere la doppia gerarchia nidificata. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la [Panoramica sul sistema XDM](../../xdm/home.md).

## Real-Time Customer Data Platform

Basato su Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) consente alle aziende di unire dati noti e sconosciuti per attivare i profili cliente con decisioni intelligenti in tutto il percorso del cliente. [!DNL Real-Time CDP] combina più origini dati aziendali per creare profili cliente in tempo reale. I segmenti generati da questi profili possono quindi essere inviati alle destinazioni a valle per fornire esperienze cliente personalizzate individuali su tutti i canali e i dispositivi.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Pagina Home di Real-Time CDP migliorata | La [pagina Home di Real-Time CDP](https://experience.adobe.com) è stata migliorata con un aspetto aggiornato e prestazioni migliorate. La pagina Home è ora in grado di riconoscere le autorizzazioni e presenterà i widget relativi alle funzioni a cui hai accesso. Per ulteriori informazioni, consulta la [Panoramica della dashboard della pagina Home di Real-Time CDP](../../rtcdp/home-page-dashboards.md). |
| Sondaggio di auto-identificazione | Il sondaggio di auto-identificazione è un breve questionario presentato nella pagina Home dell’interfaccia utente di Adobe Experience Platform. Utilizza il sondaggio di auto-identificazione per creare il tuo profilo personale di Experience Platform e ricevere linee guida personalizzate in base alle tue selezioni. Per ulteriori informazioni, consulta la [panoramica sul sondaggio di auto-identificazione](../../landing/self-identification.md). |

Per ulteriori informazioni su [!DNL Real-Time CDP], consulta la [[!DNL Real-Time CDP] panoramica](../../rtcdp/overview.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati clienti in una visualizzazione unificata che offre un account utilizzabile e dotato di marca temporale per ogni interazione con il cliente.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Scadenza dati profilo identificato da pseudonimo | La scadenza dei dati del profilo identificato da pseudonimo è ora generalmente disponibile. Una volta abilitata, questa versione rimuoverà continuamente dall’istanza di Experience Platform i profili identificati da pseudonimi non aggiornati. Per ulteriori informazioni su questa funzione e sui profili identificati da pseudonimi, consulta la [Guida alla scadenza dei dati del profilo identificato da pseudonimo](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Mappa di appartenenza al segmento | In seguito al precedente annuncio di febbraio, il 15 maggio 2023 lo stato `Existing` verrà rimosso dalla mappa di appartenenza al segmento per rimuovere la ridondanza nel ciclo di vita dell’appartenenza al segmento. Dopo questa modifica, i profili qualificati in un segmento verranno rappresentati come `Realized` e i profili non qualificati continueranno a essere rappresentati come `Exited`.<br/><br/> Se utilizzi le [destinazioni Enterprise](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Hub eventi Azure, API HTTP) e potresti disporre di processi a valle automatizzati basati sullo stato `Existing`, questa modifica potrebbe interessarti. In questo caso, rivedi le tue integrazioni a valle. Se ti interessa identificare profili nuovi e qualificati oltre un certo periodo di tempo, puoi utilizzare una combinazione di stato `Realized` e `lastQualificationTime` nella mappa di appartenenza al segmento. Per ulteriori informazioni, contatta il rappresentante Adobe. |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e consente di strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto API per filtrare i dati a livello di riga per l’origine del sistema CRM Salesforce. | Utilizza gli operatori logici e di confronto per filtrare i dati a livello di riga per l’origine CRM di Salesforce. Per ulteriori informazioni, consulta la guida su come [filtrare i dati per un’origine utilizzando l’API](../../sources/tutorials/api/filter.md). |
| Disponibilità in versione beta di Shopify Streaming | L’[origine Shopify Streaming](../../sources/connectors/ecommerce/shopify-streaming.md) è ora disponibile in versione beta. Utilizza l’origine Shopify Streaming per inviare dati dall’account dei partner di Shopify a Experience Platform. |
| Disponibilità generale dell’integrazione OneTrust | L’[origine dell’integrazione OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) è ora disponibile per tutti. Utilizza l’origine dell’integrazione OneTrust per portare a Experience Platform i dati di consenso e preferenze dall’account dell’integrazione di OneTrust. |
| Disponibilità generale del servizio Oracle Cloud | L’[origine del servizio Oracle Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md) è ora disponibile per tutti. Utilizza l’origine del servizio Oracle Cloud per portare i dati di tale servizio su Experience Platform. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sources/home.md).