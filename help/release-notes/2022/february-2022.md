---
title: Note sulla versione di Adobe Experience Platform - Febbraio 2022
description: Note sulla versione di Adobe Experience Platform di febbraio 2022.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 18%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: martedì 7 marzo 2022**

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

Adobe Experience Platform fornisce più [!DNL dashboards] tramite i quali è possibile visualizzare informazioni importanti sui dati dell&#39;organizzazione acquisiti durante le istantanee giornaliere.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuovi widget di destinazioni standard | I seguenti widget standard consentono di visualizzare diverse metriche correlate alle destinazioni.<ul><li>Segmenti attivati di recente per destinazione. Questo widget mostra i primi cinque segmenti attivati più di recente in ordine decrescente in base alla destinazione scelta.</li><li>Tendenza dimensione pubblico. Questo widget rappresenta la relazione del conteggio dei profili in un periodo di tempo per un segmento mappato su tale account di destinazione.</li><li>Segmenti non mappati per identità. Questo widget elenca i primi cinque segmenti non mappati classificati per conteggio di identità decrescente per una determinata destinazione e identità.</li><li>Segmenti mappati per identità. Questo widget elenca i primi cinque segmenti mappati. I segmenti vengono ordinati da alto a basso in base al rispettivo numero di ID di origine che corrispondono all’ID di destinazione selezionato dal menu a discesa del widget.</li><li>Pubblico comune. Questo widget fornisce un elenco dei primi cinque segmenti attivati nell’account di destinazione scelto nella parte superiore della pagina e nella destinazione selezionata nel menu a discesa del widget.</li></ul> Per ulteriori informazioni sui widget standard disponibili, consulta la documentazione del dashboard [destinazioni.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=it#standard-widgets). |

Per ulteriori informazioni su [!DNL Dashboards], consulta la [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli all’Edge Network di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Flusso di lavoro dell’interfaccia utente migliorato per la configurazione dello stream di dati | Il flusso di lavoro per la creazione di un nuovo stream di dati nell’interfaccia utente di Data Collection è stato aggiornato. Quando si aggiungono servizi a un flusso di dati, nell’elenco delle opzioni verranno inclusi solo i servizi a cui hai accesso. Per ulteriori informazioni, consulta la guida sulla [configurazione di uno stream di dati](../../datastreams/overview.md). |
| Preparazione dei dati per la raccolta dati | Se utilizzi Adobe Experience Platform Web SDK, ora puoi sfruttare le funzionalità di preparazione dati per mappare i dati su Experience Data Model (XDM) sul lato server. Per ulteriori informazioni, consulta la sezione sulla [preparazione dati per la raccolta dati](../../datastreams/data-prep.md) nella guida sugli stream di dati. |
| ID dispositivo di prime parti | Ora è possibile inviare i propri ID dispositivo all’Edge Network di Adobe Experience Platform durante la raccolta dei dati dei clienti tramite Experience Platform Web SDK, fornendo una soluzione per le recenti restrizioni del browser sulla durata dei cookie di terze parti. Per ulteriori informazioni, consulta la guida su [ID dispositivo di prime parti](../../web-sdk/identity/first-party-device-ids.md). |

Per ulteriori informazioni sulla raccolta dati in Experience Platform, consulta la [panoramica sulla raccolta dati](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| (Beta) Supporto di Destination SDK per destinazioni basate su file | [Il supporto di Destination SDK per le destinazioni basate su file](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) è attualmente in versione beta privata ed è disponibile solo per un numero selezionato di partner e clienti. La funzionalità e la documentazione associata sono soggette a modifiche prima del rilascio di disponibilità generale.<br><br>Per informazioni su come accedere alla funzione, contatta il rappresentante del tuo account Adobe. I rappresentanti degli account interni di Adobe devono contattare i team di prodotto e ingegneri delle destinazioni Experience Platform per discutere dei casi di utilizzo supportati. <br><br> Nella fase beta del supporto di Destination SDK per le destinazioni basate su file, i partner beta e i clienti possono utilizzare [Experience Platform Destination SDK](../../destinations/destination-sdk/overview.md) per creare destinazioni private e usufruire delle seguenti funzionalità: <ul><li>Crea una destinazione basata su file (batch) tramite Amazon S3, server SFTP, Azure Blob, Azure Data Lake Storage e Data Landing Zone Storage.</li><li>Configura e imposta le opzioni di frequenza e pianificazione per l&#39;esportazione dei file di default.</li><li>Configura e imposta le opzioni per formattare i file CSV esportati (delimitatori, caratteri di escape e altre opzioni).</li><li>Possibilità di impostare e modificare intestazioni di file personalizzate.</li><li>Possibilità di ricevere notifiche di eventi sull’esportazione di file e segmenti.</li><li>Possibilità di esportare altri tipi di file come CSV, TSV, JSON o Parquet.</li></ul>  <br>Per iniziare a utilizzare la nuova funzionalità, leggere [(Beta) Utilizzare Destination SDK per configurare una destinazione basata su file](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md). <br><br> La funzionalità per creare destinazioni *streaming* private o prodotte utilizzando Destination SDK è già disponibile per tutti i clienti e i partner Experience Platform. Per informazioni dettagliate, consulta la guida su come [utilizzare Destination SDK per configurare una destinazione di streaming](../../destinations/destination-sdk/guides/configure-destination-instructions.md). |

## [!DNL Identity Service] {#identity}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Questo è reso più difficile quando i dati del cliente sono frammentati tra sistemi diversi, facendo apparire ogni singolo cliente con più &quot;identità&quot;.

Adobe Experience Platform [!DNL Identity Service] consente di ottenere una migliore visualizzazione dei clienti e del loro comportamento collegando le identità tra dispositivi e sistemi, consentendo di fornire esperienze digitali personali e di impatto in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuova autorizzazione per `view-identity-graph` | È ora possibile utilizzare l&#39;autorizzazione `view-identity-graph` per controllare se gli utenti dell&#39;organizzazione possono visualizzare i dati del grafico delle identità. Agli utenti che non dispongono di questa autorizzazione sarà vietato accedere al visualizzatore del grafo delle identità nell&#39;interfaccia utente o alle API [!DNL Identity Service] che restituiscono identità. Per ulteriori informazioni sulle autorizzazioni, vedere la [panoramica sul controllo degli accessi](../../access-control/home.md). |

Per ulteriori informazioni generali su [!DNL Identity Service], consulta [Panoramica del servizio Identity](../../identity-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi di Experience Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Sorgenti Beta che passano a GA | Le seguenti sorgenti sono state promosse dalla versione beta a GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li></ul> |

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).