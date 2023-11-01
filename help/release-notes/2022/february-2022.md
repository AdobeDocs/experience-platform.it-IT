---
title: Note sulla versione di Adobe Experience Platform - Febbraio 2022
description: Note sulla versione di Adobe Experience Platform di febbraio 2022.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 27%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 7 marzo 2022**

>[!NOTE]
>
>Questa versione è stata spostata dalla data originale del 23 febbraio al 7 marzo.

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform offre più [!DNL dashboards] attraverso cui è possibile visualizzare informazioni importanti sui dati dell&#39;organizzazione, acquisite durante le istantanee giornaliere.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuovi widget di destinazioni standard | I seguenti widget standard consentono di visualizzare diverse metriche correlate alle destinazioni.<ul><li>Segmenti attivati di recente per destinazione. Questo widget mostra i primi cinque segmenti attivati più di recente in ordine decrescente in base alla destinazione scelta.</li><li>Tendenza delle dimensioni del pubblico. Questo widget rappresenta la relazione del conteggio dei profili in un periodo di tempo per un segmento mappato su tale account di destinazione.</li><li>Segmenti non mappati per identità. Questo widget elenca i primi cinque segmenti non mappati classificati in base al conteggio delle identità decrescente per una determinata destinazione e identità.</li><li>Segmenti mappati per identità. Questo widget elenca i primi cinque segmenti mappati. I segmenti vengono ordinati da alto a basso in base al rispettivo numero di ID di origine che corrispondono all’ID di destinazione selezionato dal menu a discesa del widget.</li><li>Segmenti di pubblico comuni. Questo widget fornisce un elenco dei primi cinque segmenti attivati nell’account di destinazione scelto nella parte superiore della pagina e la destinazione selezionata nel menu a discesa del widget.</li></ul> Per ulteriori informazioni sui widget standard disponibili, vedere [documentazione del dashboard destinazioni.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#standard-widgets). |

Per ulteriori informazioni su [!DNL Dashboards], consultare il [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Flusso di lavoro dell’interfaccia utente migliorato per la configurazione dello stream di dati | Il flusso di lavoro per la creazione di un nuovo stream di dati nell’interfaccia utente di Data Collection è stato aggiornato. Quando si aggiungono servizi a un flusso di dati, nell’elenco delle opzioni verranno inclusi solo i servizi a cui hai accesso. Consulta la guida su [configurazione di uno stream di dati](../../datastreams/overview.md) per ulteriori informazioni. |
| Preparazione dei dati per la raccolta dati | Se utilizzi Adobe Experience Platform Web SDK, ora puoi sfruttare le funzionalità di preparazione dati per mappare i dati su Experience Data Model (XDM) sul lato server. Consulta la sezione su [Preparazione per la raccolta dati](../../datastreams/data-prep.md) per ulteriori informazioni, consulta la guida sugli stream di dati. |
| ID dispositivo di prime parti | Ora è possibile inviare i propri ID dispositivo alla rete Edge di Adobe Experience Platform durante la raccolta dei dati dei clienti tramite Platform Web SDK, fornendo una soluzione per le recenti restrizioni del browser sulla durata dei cookie di terze parti. Consulta la guida su [ID dispositivo di prime parti](../../edge/identity/first-party-device-ids.md) per ulteriori informazioni. |

Per ulteriori informazioni sulla raccolta dei dati in Platform, consulta la sezione [panoramica sulla raccolta dati](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| (Beta) Supporto di Destination SDK per destinazioni basate su file | [Destination SDK supporto per destinazioni basate su file](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) è attualmente in versione beta privata ed è disponibile solo per un numero selezionato di partner e clienti. La funzionalità e la documentazione associata sono soggette a modifiche prima del rilascio di disponibilità generale.<br><br>Per informazioni su come accedere alla funzione, contatta il rappresentante del tuo account di Adobe. I rappresentanti degli account interni degli Adobi devono contattare i team di prodotto e di progettazione delle destinazioni Experienci Platform per discutere i casi di utilizzo supportati. <br><br> Nella fase beta del supporto Destination SDK per le destinazioni basate su file, i partner beta e i clienti possono utilizzare [Destination SDK Experience Platform](../../destinations/destination-sdk/overview.md) per creare destinazioni private che possano usufruire delle seguenti funzionalità: <ul><li>Crea una destinazione basata su file (batch) tramite Amazon S3, server SFTP, Azure Blob, Azure Data Lake Storage e Data Landing Zone Storage.</li><li>Configura e imposta le opzioni di frequenza e pianificazione per l&#39;esportazione dei file di default.</li><li>Configura e imposta le opzioni per formattare i file CSV esportati (delimitatori, caratteri di escape e altre opzioni).</li><li>Possibilità di impostare e modificare intestazioni di file personalizzate.</li><li>Possibilità di ricevere notifiche di eventi sull’esportazione di file e segmenti.</li><li>Possibilità di esportare altri tipi di file come CSV, TSV, JSON o Parquet.</li></ul>  <br>Per iniziare a utilizzare la nuova funzionalità, leggi [(Beta) Utilizza Destination SDK per configurare una destinazione basata su file](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md). <br><br> La funzionalità per creare privati o prodotti *streaming* Le destinazioni tramite Destination SDK sono già disponibili per tutti i clienti e i partner Experienci Platform. Leggi la guida su come [utilizzare Destination SDK per configurare una destinazione di streaming](../../destinations/destination-sdk/guides/configure-destination-instructions.md) per i dettagli. |

## [!DNL Identity Service] {#identity}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Questo è reso più difficile quando i dati del cliente sono frammentati tra sistemi diversi, facendo apparire ogni singolo cliente con più &quot;identità&quot;.

Adobe Experience Platform [!DNL Identity Service] ti consente di avere una visione migliore del cliente e del suo comportamento collegando le identità tra dispositivi e sistemi, consentendoti di fornire esperienze digitali personali e di impatto in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuova autorizzazione per `view-identity-graph` | Ora puoi utilizzare la `view-identity-graph` autorizzazione per controllare se gli utenti dell’organizzazione possono visualizzare i dati del grafico delle identità. Agli utenti senza questa autorizzazione sarà vietato accedere al visualizzatore del grafico delle identità nell’interfaccia utente o durante l’accesso [!DNL Identity Service] API che restituiscono identità. Consulta la [panoramica sul controllo degli accessi](../../access-control/home.md) per ulteriori informazioni sulle autorizzazioni. |

Per informazioni più generali su [!DNL Identity Service], fare riferimento a [Panoramica del servizio Identity](../../identity-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Sorgenti beta che passano a GA | Le seguenti sorgenti sono state promosse dalla versione beta a GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).