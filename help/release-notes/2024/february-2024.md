---
title: Note sulla versione di Adobe Experience Platform - Febbraio 2024
description: Note sulla versione di Adobe Experience Platform di febbraio 2024.
exl-id: 7e4b76b7-4027-4890-b869-1dbb79670c3e
source-git-commit: aa33f7006b1a3abf7d19ffe3e0d5e5ee39fe9a5d
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 22%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 21 febbraio 2024**

Aggiornamenti alle funzioni esistenti in Experience Platform:

- [Avvisi](#alerts)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Avvisi {#alerts}

Un Experience Platform consente di abbonarti agli avvisi basati su eventi per varie attività di Platform. Puoi abbonarti a diverse regole di avviso tramite la scheda [!UICONTROL Avvisi] nell&#39;interfaccia utente di Platform e scegliere di ricevere messaggi di avviso all&#39;interno dell&#39;interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Scheda Cronologia avvisi | In qualità di amministratore di Experience Platform, puoi utilizzare la funzione di gestione degli abbonati agli avvisi per assegnare un avviso a un ID utente, un indirizzo e-mail esterno o un elenco di gruppi e-mail di Adobe. Per ulteriori informazioni, vedere la [documentazione dell&#39;interfaccia utente degli avvisi](../../observability/alerts/ui.md) per ulteriori informazioni sulla scheda della cronologia. |

{style="table-layout:auto"}

Per ulteriori informazioni sugli avvisi, leggere la [[!DNL Observability Insights] panoramica](../../observability/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [Supporto per la messaggistica Web in-app in Web SDK](../../web-sdk/personalization/web-in-app-messaging.md) | Adobe Experience Platform Web SDK ora supporta la configurazione della messaggistica in-app web per le campagne Adobe Journey Optimizer. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle raccolte dati, consulta la [panoramica sulle raccolte dati](../../tags/home.md).

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](../../data-prep/home.md). -->

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni** {#new-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [Connessione Gainsight PX](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX è una piattaforma di esperienza dei prodotti che consente ai team di prodotto di comprendere in che modo gli utenti utilizzano i loro prodotti, raccogliere feedback e creare progetti in-app, come le procedure dettagliate sui prodotti, per incentivare l’onboarding degli utenti e l’adozione dei prodotti. |
| [Connessione tag Mailchimp](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp è una piattaforma di automazione del marketing e un servizio di marketing via e-mail popolare. Puoi utilizzare il connettore Mailchimp Tags per strutturare, etichettare o categorizzare i contatti. |
| [Connessione Commerce SAP](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce è una piattaforma di e-commerce basata su cloud per le aziende B2B e B2C, disponibile come parte del portafoglio Customer Experience SAP. È possibile utilizzare questa destinazione per aggiornare i dettagli del cliente in SAP Commerce da un pubblico Experience Platform esistente. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Attiva i tipi di pubblico dell’account generalmente disponibili | La funzionalità per attivare i tipi di pubblico dell&#39;account in determinate destinazioni è ora generalmente disponibile per le aziende che acquistano le edizioni [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) e [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) di Real-time Customer Data Platform. Leggi il tutorial su [attivazione dei tipi di pubblico dell&#39;account](/help/destinations/ui/activate-account-audiences.md) per ottenere informazioni complete, incluse le destinazioni supportate. |
| Strumenti di applicazione del consenso Digital Markets Act per le destinazioni Google | Google sta rilasciando modifiche all&#39;API [Google Ads](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) e all&#39;API [Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) per supportare i requisiti relativi alla conformità e al consenso definiti nel [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) nell&#39;Unione Europea ([EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/)). L’applicazione di queste modifiche ai requisiti di consenso dovrebbe entrare in vigore a partire dal 6 marzo 2024. <br/><br/> Per aderire alla politica di consenso degli utenti dell&#39;UE e continuare a creare elenchi di pubblico per gli utenti dello Spazio economico europeo (SEE), gli inserzionisti e i partner devono assicurarsi di trasmettere il consenso dell&#39;utente finale durante il caricamento dei dati sul pubblico. In qualità di partner Google, Adobe fornisce gli strumenti necessari per soddisfare i requisiti di consenso ai sensi dell’accordo DMA nell’Unione Europea.<br/><br/>I clienti che hanno acquistato Adobe Privacy &amp; Security Shield e hanno configurato un [criterio di consenso](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) per filtrare i profili non autorizzati non devono intraprendere alcuna azione.<br/><br/>I clienti che non hanno acquistato Adobe Privacy &amp; Security Shield devono utilizzare le funzionalità di [definizione del segmento](../../segmentation/home.md#segment-definitions) all&#39;interno di [Generatore di segmenti](../../segmentation/ui/segment-builder.md) per filtrare i profili non autorizzati, al fine di continuare a utilizzare le destinazioni Real-Time CDP Google esistenti senza interruzioni. |
| [!BADGE Beta]{type=Informative} riordina i campi di mappatura per le destinazioni batch | Ora puoi modificare l&#39;ordine delle colonne nelle esportazioni CSV trascinando i campi di mappatura nel passaggio [mappatura](../../destinations/ui/activate-batch-profile-destinations.md#mapping). L’ordine dei campi mappati nell’interfaccia utente si riflette nell’ordine delle colonne nel file CSV esportato, dall’alto verso il basso, con la riga in alto che corrisponde alla colonna più a sinistra nel file CSV. <br/><br/> Questa funzionalità è in versione beta ed è disponibile solo per alcuni clienti. Per richiedere l’accesso a questa funzione, contatta il rappresentante del tuo Adobe. |
| [!BADGE Beta]{type=Informative} Pianificazioni di esportazione predefinite preselezionate per le destinazioni batch | Experience Platform ora imposta automaticamente una pianificazione predefinita per ogni esportazione di file. Per informazioni su come modificare la pianificazione predefinita, consulta la documentazione sulla [pianificazione delle esportazioni del pubblico](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). <br/><br/> Questa funzionalità è in versione beta ed è disponibile solo per alcuni clienti. Per richiedere l’accesso a questa funzione, contatta il rappresentante del tuo Adobe. |
| [!BADGE Beta]{type=Informative} Modifica in blocco le pianificazioni di attivazione del pubblico per le destinazioni batch | Ora puoi modificare la pianificazione dell&#39;attivazione per più tipi di pubblico in blocco dalla pagina [Dati attivazione](../../destinations/ui/destination-details-page.md#bulk-edit-schedule). <br/><br/> Questa funzionalità è in versione beta ed è disponibile solo per alcuni clienti. Per richiedere l’accesso a questa funzione, contatta il rappresentante del tuo Adobe. |
| [!BADGE Beta]{type=Informative} Esporta in blocco i file su richiesta nelle destinazioni batch | È ora possibile esportare i tipi di pubblico in blocco nelle destinazioni batch tramite la funzionalità [esporta file on-demand](../../destinations/ui/export-file-now.md). <br/><br/> Questa funzionalità è in versione beta ed è disponibile solo per alcuni clienti. Per richiedere l’accesso a questa funzione, contatta il rappresentante del tuo Adobe. |

{style="table-layout:auto"}

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per soddisfare questa esigenza, Experience Platform fornisce sandbox che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Strumenti sandbox | Oltre a supportare ora i tipi di oggetto per le regole di consenso e governance, utilizza gli strumenti sandbox per importare schemi senza profili unificati abilitati, verificare la presenza di attributi mancanti nella sandbox di destinazione durante l’importazione di un segmento e utilizza per impostazione predefinita il criterio di unione esistente. Per ulteriori informazioni su queste funzioni, consulta la [guida dell&#39;interfaccia utente per gli strumenti della sandbox](../../sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle sandbox, consulta la [panoramica sulle sandbox](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] consente di segmentare i dati memorizzati in [!DNL Experience Platform] che si riferiscono ai singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in tipi di pubblico. Puoi creare tipi di pubblico tramite definizioni di segmenti o altre origini dai tuoi dati di [!DNL Real-Time Customer Profile]. Questi tipi di pubblico sono configurati e gestiti centralmente in [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione Adobe.

**Nuova funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Pubblico dell’account | I tipi di pubblico dell’account sono ora generalmente disponibili. Ora puoi utilizzare la segmentazione dell’account per rendere più semplice e sofisticata l’esperienza di segmentazione del marketing, dai tipi di pubblico basati sulle persone a quelli basati sull’account, sia nelle edizioni B2B che B2P di Real-Time Customer Platform. Questa versione consente di utilizzare i tipi di pubblico basati sulle persone come predicato per i tipi di pubblico basati su account, aggiunge funzionalità di ricerca, supporta l’utilizzo di entità personalizzate ed è conforme alla governance dei dati. Per ulteriori informazioni su questa funzione, leggere la [panoramica sui tipi di pubblico dell&#39;account](../../segmentation/ui/account-audiences.md). |

{style="table-layout:auto"}

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Origine [!BADGE Beta]{type=Informative} [!DNL Acxiom] | Utilizza [[!DNL Acxiom Prospecting Data Import] source](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) per recuperare e mappare i dati da [!DNL Acxiom] prospect service ad Experience Platform. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, leggere la [panoramica delle origini](../../sources/home.md).
