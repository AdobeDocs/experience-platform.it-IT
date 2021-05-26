---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di Experience Platform per il 26 maggio 2021.
doc-type: release notes
last-update: May 26, 2021
author: ens72741
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 0cef5f1a0033bed987799c26b99e71145a85c1a9
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 3%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 maggio 2021**

Nuove funzioni in Adobe Experience Platform:

- [Dashboard](#dashboards)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [Profilo cliente in tempo reale](#profile)
- [Fonti](#sources)

## Dashboard {#dashboards}

Adobe Experience Platform fornisce diverse dashboard attraverso le quali puoi visualizzare informazioni importanti sui dati dell’organizzazione, acquisiti durante le istantanee giornaliere.

| Funzione | Descrizione |
| --- | --- |
| Informazioni sul profilo | Il dashboard del profilo fornisce una panoramica giornaliera delle metriche Profilo cliente in tempo reale per ogni criterio di unione organizzativa, ad Experience Platform. Queste informazioni sul profilo sono disponibili per tutti gli utenti con la possibilità di accedere e visualizzare i dati del profilo all’interno di Platform. |
| Approfondimenti sul pubblico | Il dashboard dei segmenti fornisce informazioni relative al pubblico a tutti gli utenti con accesso per visualizzare i segmenti all’interno di Platform. Il dashboard fornisce una panoramica giornaliera delle metriche del pubblico per i tipi di pubblico creati con l’interfaccia utente di Generatore di segmenti o importati da Adobe Audience Manager. |
| Informazioni sull’attivazione | Il dashboard delle destinazioni è disponibile per tutti gli utenti con la possibilità di accedere e visualizzare le destinazioni. Il dashboard fornisce una panoramica giornaliera delle metriche di attivazione per le attivazioni in tutte le destinazioni. |
| Informazioni specifiche per l’utente | Ogni utente può personalizzare l’aspetto delle dashboard, inclusa la possibilità di modificare il layout del dashboard aggiungendo, rimuovendo, ridimensionando e ridisponendo i widget. |
| Creazione e gestione dei widget | Tutti i widget standard e personalizzati sono accessibili agli addetti al marketing in un archivio centralizzato per democratizzare la creazione e la condivisione delle informazioni:<br/><ul><li>La scheda standard contiene widget forniti da Adobe accessibili nel contesto del dashboard. </li><li>La scheda personalizzata contiene i widget personalizzati creati dall’organizzazione, inclusa un’opzione per nascondere i widget dalla visualizzazione.</li><li>Il flusso di lavoro per la creazione di widget in Profili e informazioni sul pubblico consente di modificare, selezionare, visualizzare in anteprima e pubblicare widget personalizzati.</li></ul> |
| Informazioni personalizzate | Le autorizzazioni di accesso consentono a data engineer e esperti di marketing di personalizzare gli attributi di profilo disponibili per la creazione di widget. |

Per ulteriori informazioni sulle dashboard, tra cui come concedere autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica delle dashboard](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

| Funzione | Descrizione |
| ------- | ----------- |
| Avvisi di errore lenti | I messaggi di errore di Data Prep Mapper ora saranno più lenti, fornendo avvisi invece di errori insieme a righe parzialmente trasformate. |
| Nuove funzioni | Sono state aggiunte funzioni per ottenere chiavi, aggiungere elementi a un array esistente, aggiungere elementi di più array a un array esistente, utilizzare oggetti per creare array e utilizzare il nome dell’oggetto JSON come valore letterale stringa. |

Per ulteriori informazioni, consulta la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

| Funzione | Descrizione |
| ------- | ----------- |
| Monitoraggio migliorato (versione beta) | Aumento delle funzionalità di monitoraggio delle destinazioni, comprese le informazioni per le destinazioni batch e in streaming |
| [Esportazione più rapida dei file incrementali (beta)](../../destinations/ui/activate-destinations.md#export-incremental-files) | È stata aggiunta la possibilità di esportare file incrementali nelle destinazioni ogni 3, 6, 8 o 12 ore. <br> <br>Questa funzionalità è attualmente in versione beta ed è disponibile solo per un numero selezionato di clienti. I clienti non beta possono esportare file incrementali una volta al giorno. |
| [Supporto chiave di deduplicazione (beta)](../../destinations/ui/activate-destinations.md#deduplication-keys) | È stata aggiunta la possibilità di impostare spazi dei nomi di identità o attributi di profilo come chiavi di deduplicazione. Le chiavi di deduplicazione eliminano la possibilità di avere più record dello stesso profilo in un unico file di esportazione. <br> <br>Questa funzionalità è attualmente in versione beta ed è disponibile solo per un numero selezionato di clienti. |

Per informazioni più generali sulle destinazioni, consulta la [panoramica delle destinazioni](../../destinations/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Experience Data Model (XDM) è una specifica open-source progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

| Funzione | Descrizione |
| --- | --- |
| Gruppi di campi dello schema | Il termine &quot;mixin&quot; è stato aggiornato a &quot;gruppo di campi&quot;. Questa modifica si riflette nell’interfaccia utente di Adobe Experience Platform. Inoltre, l&#39;API del Registro di sistema dello schema ha un nuovo endpoint [gruppi di campi](../../xdm/api/field-groups.md), mentre l&#39;endpoint mixins è stato dichiarato obsoleto come endpoint legacy. Per ulteriori informazioni, consulta la [documentazione XDM](../../xdm/home.md) . |

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account actionable con marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Unisci aggiornamenti del flusso di lavoro dei criteri | Durante la creazione e l’aggiornamento dei criteri di unione nell’interfaccia utente, gli utenti ora possono visualizzare in anteprima 20 profili di esempio in base allo schema dell’unione. Questo consente agli utenti di visualizzare in anteprima l&#39;aspetto dei profili dei clienti prima di salvare le configurazioni dei criteri di unione. Per ulteriori informazioni, consulta la [guida all&#39;interfaccia utente dei criteri di unione](../../profile/merge-policies/ui-guide.md). |
| Rapporto di sovrapposizione set di dati | Il rapporto di sovrapposizione dei set di dati fornisce visibilità nella composizione dell’archivio profili esponendo i set di dati che contribuiscono maggiormente al pubblico indirizzabile. Oltre a fornire informazioni approfondite sui dati di Profilo, questo rapporto consente agli utenti di intraprendere azioni per ottimizzare l’utilizzo della licenza, ad esempio per impostare un limite di vita di determinati dati. Per ulteriori informazioni, segui l’esercitazione su [generazione del rapporto di sovrapposizione dei set di dati](../../profile/tutorials/dataset-overlap-report.md). |

Per ulteriori informazioni sul Profilo del cliente in tempo reale, comprese esercitazioni e best practice per l’utilizzo dei dati [!DNL Profile], si prega di iniziare leggendo la [Panoramica del profilo del cliente in tempo reale](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto dell’interfaccia utente per l’acquisizione di file compressi | Ora puoi visualizzare in anteprima e acquisire file JSON compressi o delimitati utilizzando origini di archiviazione cloud nell’interfaccia utente. Per ulteriori informazioni, consulta l’esercitazione su [configurazione di un flusso di dati per una connessione sorgente di archiviazione cloud nell’interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Per ulteriori informazioni sulle origini, consulta la [panoramica origini](../../sources/home.md).
