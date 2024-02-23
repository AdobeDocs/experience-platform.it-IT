---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di Adobe Experience Platform di gennaio 2024.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 3c0b7c4eee7c790a8ffae95c05a8db6ba7c3b285
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 22%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 21 febbraio 2024**

Aggiornamenti alle funzioni esistenti in Experienci Platform:

- [Avvisi](#alerts)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Avvisi {#alerts}

Un Experience Platform consente di abbonarti agli avvisi basati su eventi per varie attività di Platform. È possibile abbonarsi a diverse regole di avviso tramite [!UICONTROL Avvisi] nell’interfaccia utente di Platform e può scegliere di ricevere messaggi di avviso all’interno dell’interfaccia utente stessa o tramite notifiche e-mail.
**Funzioni nuove o aggiornate**
| Funzionalità | Descrizione | | — | — | | Scheda Cronologia avvisi | In qualità di amministratore di Experienci Platform, puoi utilizzare la funzione di gestione degli abbonati agli avvisi per assegnare un avviso a un ID utente, un indirizzo e-mail esterno o un elenco di gruppi e-mail di Adobe. Per ulteriori informazioni, vedere [documentazione dell’interfaccia utente avvisi](../../observability/alerts/ui.md) per ulteriori informazioni sulla scheda cronologia. |



Per ulteriori informazioni sugli avvisi, leggere [[!DNL Observability Insights] panoramica](../../observability/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [Supporto per la messaggistica Web in-app in Web SDK](../../edge/personalization/web-in-app-messaging.md) | Adobe Experience Platform Web SDK ora supporta la configurazione della messaggistica in-app web per le campagne Adobe Journey Optimizer. |

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
| [Connessione PX Gainsight](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX è una piattaforma di esperienza dei prodotti che consente ai team di prodotto di comprendere in che modo gli utenti utilizzano i loro prodotti, raccogliere feedback e creare progetti in-app, come le procedure dettagliate sui prodotti, per incentivare l’onboarding degli utenti e l’adozione dei prodotti. |
| [Connessione tag Mailchimp](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp è una piattaforma di automazione del marketing e un servizio di marketing via e-mail popolare. Puoi utilizzare il connettore Mailchimp Tags per strutturare, etichettare o categorizzare i contatti. |
| [Connessione SAP Commerce](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce è una soluzione di piattaforma e-commerce basata su cloud per le aziende B2B e B2C, disponibile come parte del portafoglio SAP Customer Experience. È possibile utilizzare questa destinazione per aggiornare i dettagli dei clienti in SAP Commerce da un pubblico Experience Platform esistente. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Attiva i tipi di pubblico dell’account generalmente disponibili | La funzionalità di attivazione del pubblico dell’account per determinate destinazioni è ora generalmente disponibile per le aziende che acquistano [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) e [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) edizioni Real-time Customer Data Platform. Leggi l’esercitazione su [attivazione del pubblico dell’account](/help/destinations/ui/activate-account-audiences.md) per ottenere informazioni complete, incluse le destinazioni supportate. |
| Strumenti di applicazione del consenso Digital Markets Act per le destinazioni Google | Google sta rilasciando modifiche al [API di Google Ads](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)e [API Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) al fine di garantire la conformità e i requisiti relativi al consenso definiti [Legge sui mercati digitali](https://digital-markets-act.ec.europa.eu/index_en) (DMA) nell&#39;Unione europea ([Politica di consenso degli utenti UE](https://www.google.com/about/company/user-consent-policy/)). L’applicazione di queste modifiche ai requisiti di consenso dovrebbe entrare in vigore a partire dal 6 marzo 2024. <br/><br/> Per aderire alla politica di consenso degli utenti dell’UE e continuare a creare elenchi di pubblico per gli utenti dello Spazio economico europeo (SEE), gli inserzionisti e i partner devono assicurarsi di trasmettere il consenso degli utenti finali durante il caricamento dei dati sul pubblico. In qualità di partner Google, Adobe fornisce gli strumenti necessari per soddisfare i requisiti di consenso ai sensi dell’accordo DMA nell’Unione Europea.<br/><br/>Clienti che hanno acquistato Adobe Privacy &amp; Security Shield e hanno configurato un [criterio di consenso](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) per filtrare i profili non autorizzati non è necessario eseguire alcuna azione.<br/><br/>I clienti che non hanno acquistato Adobe Privacy &amp; Security Shield devono utilizzare [definizione del segmento](../../segmentation/home.md#segment-definitions) funzionalità di [Generatore di segmenti](../../segmentation/ui/segment-builder.md) per filtrare i profili non autorizzati, in modo da continuare a utilizzare senza interruzioni le destinazioni Real-Time CDP Google esistenti. |
| [!BADGE Beta]{type=Informative} Riordina i campi di mappatura per le destinazioni batch | Ora puoi modificare l’ordine delle colonne nelle esportazioni CSV trascinando e rilasciando i campi di mappatura nella sezione [mappatura](../../destinations/ui/activate-batch-profile-destinations.md#mapping) passaggio. L’ordine dei campi mappati nell’interfaccia utente si riflette nell’ordine delle colonne nel file CSV esportato, dall’alto verso il basso, con la riga in alto che corrisponde alla colonna più a sinistra nel file CSV. <br/><br/> Questa funzione è in versione beta ed è disponibile solo per alcuni clienti. Per richiedere l’accesso a questa funzione, contatta il rappresentante del tuo Adobe. |
| [!BADGE Beta]{type=Informative} Programmi di esportazione predefiniti preselezionati per destinazioni batch | Experienci Platform ora imposta automaticamente una pianificazione predefinita per ogni esportazione di file. Consulta la documentazione su [programmazione delle esportazioni del pubblico](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) per informazioni su come modificare la pianificazione predefinita. <br/><br/> Questa funzione è in versione beta ed è disponibile solo per alcuni clienti. Per richiedere l’accesso a questa funzione, contatta il rappresentante del tuo Adobe. |
| [!BADGE Beta]{type=Informative} Modifiche in blocco delle pianificazioni di attivazione del pubblico per le destinazioni batch | Ora puoi modificare la pianificazione di attivazione per più tipi di pubblico in blocco, dalla sezione [Dati di attivazione](../../destinations/ui/destination-details-page.md#bulk-edit-schedule) pagina. <br/><br/> Questa funzione è in versione beta ed è disponibile solo per alcuni clienti. Per richiedere l’accesso a questa funzione, contatta il rappresentante del tuo Adobe. |
| [!BADGE Beta]{type=Informative} Esportazione in blocco di file su richiesta in destinazioni batch | Ora puoi esportare i tipi di pubblico in blocco nelle destinazioni batch, tramite [esportazione di file on-demand](../../destinations/ui/export-file-now.md) funzionalità. <br/><br/> Questa funzione è in versione beta ed è disponibile solo per alcuni clienti. Per richiedere l’accesso a questa funzione, contatta il rappresentante del tuo Adobe. |

{style="table-layout:auto"}

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per soddisfare questa esigenza, Experienci Platform fornisce sandbox che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Strumenti sandbox | Oltre a supportare ora i tipi di oggetto per le regole di consenso e governance, utilizza gli strumenti sandbox per importare schemi senza profili unificati abilitati, verificare la presenza di attributi mancanti nella sandbox di destinazione durante l’importazione di un segmento e utilizza per impostazione predefinita il criterio di unione esistente. Per ulteriori informazioni su queste funzioni, vedere [guida dell’interfaccia utente per gli strumenti della sandbox](../../sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle sandbox, consulta [panoramica sulle sandbox](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] consente di segmentare i dati memorizzati in [!DNL Experience Platform] che si riferiscono ai singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in tipi di pubblico. Puoi creare tipi di pubblico tramite definizioni di segmenti o altre origini dai tuoi dati di [!DNL Real-Time Customer Profile]. Questi tipi di pubblico sono configurati e gestiti centralmente in [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione Adobe.

**Nuova funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Pubblico dell’account | I tipi di pubblico dell’account sono ora generalmente disponibili. Ora puoi utilizzare la segmentazione dell’account per rendere più semplice e sofisticata l’esperienza di segmentazione del marketing, dai tipi di pubblico basati sulle persone a quelli basati sull’account, sia nelle edizioni B2B che B2P di Real-Time Customer Platform. Questa versione consente di utilizzare i tipi di pubblico basati sulle persone come predicato per i tipi di pubblico basati su account, aggiunge funzionalità di ricerca, supporta l’utilizzo di entità personalizzate ed è conforme alla governance dei dati. Per ulteriori informazioni su questa funzione, leggere [panoramica sui tipi di pubblico dell’account](../../segmentation/ui/account-audiences.md). |

{style="table-layout:auto"}

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom] sorgente | Utilizza il [[!DNL Acxiom Prospecting Data Import] sorgente](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) per recuperare e mappare i dati da [!DNL Acxiom] Experience Platform del servizio prospect. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, leggere [panoramica sulle origini](../../sources/home.md).
