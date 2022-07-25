---
title: Note sulla versione di Adobe Experience Platform - Febbraio 2022
description: Note sulla versione di febbraio 2022 per Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 3%

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

Adobe Experience Platform fornisce più [!DNL dashboards] attraverso cui puoi visualizzare informazioni importanti sui dati della tua organizzazione, come acquisiti durante le istantanee giornaliere.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuovi widget per destinazioni standard | I seguenti widget standard consentono di visualizzare diverse metriche correlate alle destinazioni.<ul><li>Segmenti attivati di recente per destinazione. Questo widget visualizza i primi cinque segmenti attivati più di recente in ordine decrescente in base alla destinazione scelta.</li><li>Tendenza della dimensione del pubblico. Questo widget rappresenta la relazione del conteggio del profilo in un periodo di tempo per un segmento mappato a tale account di destinazione.</li><li>Segmenti non mappati per identità. Questo widget elenca i primi cinque segmenti non mappati classificati per numero di identità decrescente per una determinata destinazione e identità.</li><li>Segmenti mappati per identità. Questo widget elenca i primi cinque segmenti mappati. I segmenti sono ordinati da alti a bassi in base ai rispettivi conteggi degli ID sorgente che corrispondono all’ID di destinazione selezionato dal menu a discesa del widget.</li><li>Tipi di pubblico comuni. Questo widget fornisce un elenco dei primi cinque segmenti attivati nell’account di destinazione scelto nella parte superiore della pagina e della destinazione selezionata nel menu a discesa del widget.</li></ul> Per ulteriori informazioni sui widget standard disponibili, consulta la sezione [documentazione del dashboard delle destinazioni.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets). |

Per ulteriori informazioni su [!DNL Dashboards], vedi [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Platform fornisce una suite di tecnologie che ti consentono di raccogliere dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network, da cui arricchire, trasformare e distribuire a destinazioni Adobi o non Adobi.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Miglioramento del flusso di lavoro dell&#39;interfaccia utente per la configurazione del datastream | Il flusso di lavoro per la creazione di un nuovo datastream nell’interfaccia utente Raccolta dati è stato aggiornato. Quando aggiungi servizi a un datastream, solo i servizi a cui hai accesso verranno inclusi nell’elenco delle opzioni. Consulta la guida su [configurazione di un datastream](../../edge/datastreams/overview.md) per ulteriori informazioni. |
| Preparazione per la raccolta dati | Se utilizzi Adobe Experience Platform Web SDK, ora puoi sfruttare le funzionalità di preparazione dei dati per mappare i dati su Experience Data Model (XDM) sul lato server. Vedi la sezione su [Preparazione per la raccolta dei dati](../../edge/datastreams/data-prep.md) nella guida datastreams per ulteriori informazioni. |
| ID dispositivo di prime parti | Ora puoi inviare i tuoi ID dispositivo a Adobe Experience Platform Edge Network quando raccogli i dati dei clienti tramite l’SDK per web di Platform, fornendo una soluzione alle recenti restrizioni del browser per la durata dei cookie di terze parti. Consulta la guida su [ID dispositivo di prime parti](../../edge/identity/first-party-device-ids.md) per ulteriori informazioni. |

Per ulteriori informazioni sulla raccolta dei dati in Platform, consulta la sezione [panoramica sulla raccolta dati](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| (Beta) Supporto per Destination SDK per destinazioni basate su file | [Supporto di Destination SDK per destinazioni basate su file](../../destinations/destination-sdk/file-based-destination-configuration.md) attualmente è in versione beta privata ed è disponibile solo per un numero selezionato di partner e clienti. La funzionalità e la documentazione associata sono soggette a modifiche prima del rilascio di disponibilità generale.<br><br>Per informazioni su come accedere alla funzione, contatta il rappresentante commerciale di Adobe. I rappresentanti dell’account interno e di Adobe devono contattare i team tecnici e di prodotto delle destinazioni Experience Platform per discutere i casi d’uso supportati. <br><br> Nella fase beta del supporto Destination SDK per le destinazioni basate su file, i partner beta e i clienti possono utilizzare il [Destination SDK Experience Platform](/help/destinations/destination-sdk/overview.md) per creare destinazioni private per sfruttare le seguenti funzionalità: <ul><li>Crea una destinazione basata su file (batch) tramite Amazon S3, server SFTP, Azure Blob, Azure Data Lake Storage, archiviazione Data Landing Zone.</li><li>Configura e imposta le opzioni di pianificazione e frequenza predefinite per l’esportazione dei file.</li><li>Configura e imposta le opzioni per formattare i file CSV esportati (delimitatori, caratteri di escape e altre opzioni).</li><li>Possibilità di impostare e modificare intestazioni di file personalizzate.</li><li>Possibilità di ricevere notifiche evento sull’esportazione di file e segmenti.</li><li>Possibilità di esportare tipi di file aggiuntivi come CSV, TSV, JSON, Parquet.</li></ul>  <br>Per iniziare a utilizzare le nuove funzionalità, leggi [(Beta) Utilizza Destination SDK per configurare una destinazione basata su file](../../destinations/destination-sdk/file-based-destination-configuration.md). <br><br> Funzionalità per creare dati privati o prodotti *streaming* Le destinazioni utilizzando Destination SDK sono già disponibili per tutti i clienti e i partner di Experience Platform. Leggi la guida su come [utilizza Destination SDK per configurare una destinazione streaming](/help/destinations/destination-sdk/configure-destination-instructions.md) per i dettagli. |

## [!DNL Identity Service] {#identity}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati dei clienti sono frammentati in diversi sistemi, il che fa sì che ogni singolo cliente sembri avere più &quot;identità&quot;.

Adobe Experience Platform [!DNL Identity Service] consente di ottenere una visione migliore del cliente e del suo comportamento attraverso il collegamento delle identità tra dispositivi e sistemi, per offrire in tempo reale esperienze digitali personali di impatto.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuova autorizzazione per `view-identity-graph` | Ora puoi utilizzare la `view-identity-graph` autorizzazione per controllare se gli utenti della tua organizzazione sono in grado di visualizzare i dati del grafico delle identità. Agli utenti che non dispongono di questa autorizzazione verrà impedito di accedere al visualizzatore del grafico di identità nell’interfaccia utente o quando accederanno [!DNL Identity Service] API che restituiscono le identità. Consulta la sezione [panoramica sul controllo degli accessi](../../access-control/home.md) per ulteriori informazioni sulle autorizzazioni. |

Per informazioni più generali su [!DNL Identity Service], fare riferimento alla [Panoramica del servizio Identity](../../identity-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Sorgenti beta che si spostano in GA | Le seguenti origini sono state promosse dalla versione beta a GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).