---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di Experience Platform per il 25 agosto 2021.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
source-git-commit: b1dca51264582788ccbde005b063c57e2f3edc8f
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 8%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 25 agosto 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Destinazioni](#destinations)
- [Observability Insights](#observability)
- [Profilo cliente in tempo reale](#profile)
- [Fonti](#sources)

## Destinazioni {#destinations}

Le destinazioni sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| [Miglioramenti a livello di usabilità delle destinazioni](../../destinations/ui/activation-overview.md) | I miglioramenti a livello di usabilità per le destinazioni consentono agli addetti al marketing di attivare facilmente i segmenti sulle destinazioni esistenti. |

Per informazioni più generali sulle destinazioni, consulta la [panoramica delle destinazioni](../../destinations/home.md).

## Informazioni sull’osservabilità {#observability}

Observability Insights consente di monitorare le attività di Platform tramite l’utilizzo di metriche statistiche e notifiche di eventi.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Avvisi | Ora puoi abbonarti a importanti avvisi relativi ai flussi di lavoro in esecuzione su Platform. Dopo aver effettuato l’abbonamento a regole di avviso specifiche, riceverai notifiche ed e-mail nell’interfaccia utente quando si verifica un evento importante sul ciclo di vita (ad esempio l’inserimento di dati con esito positivo) o in caso di problemi che richiedono attenzione (ad esempio un errore nel flusso di acquisizione o un processo di segmento che richiede più tempo del previsto). Per ulteriori informazioni, consulta la [panoramica degli avvisi](../../observability/alerts/overview.md). |

Per ulteriori informazioni sul servizio, consulta la [Panoramica di Observability Insights](../../observability/home.md) .

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Sfoglia i profili in base a criteri di unione o identità | Durante l’esplorazione dei profili in Experience Platform, ora è possibile sfogliare i criteri di unione per visualizzare in anteprima 20 profili di esempio in base al criterio di unione selezionato. È inoltre possibile sfogliare in base all’identità per cercare un profilo specifico utilizzando uno spazio dei nomi identità e il relativo valore di identità. Per ulteriori informazioni, consulta la [Guida all’interfaccia utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md). |

Per ulteriori informazioni sul Profilo del cliente in tempo reale, compresi tutorial e best practice per l’utilizzo dei dati di profilo, inizia leggendo la [Panoramica del profilo del cliente in tempo reale](../../profile/home.md).

## Fonti {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| ------- | ----------- |
| Connettore sorgente di caricamento file locale | La categoria di acquisizione dei file è stata rinominata nel sistema locale e consente di portare i file locali direttamente in Platform utilizzando il connettore di caricamento file locale. I dati acquisiti tramite questo connettore possono essere monitorati tramite il dashboard di monitoraggio. Per ulteriori informazioni, consulta la [panoramica sull’origine del caricamento dei file locali](../../sources/connectors/local-system/local-file-upload.md) . |

Per ulteriori informazioni sulle origini, consulta la [panoramica origini](../../sources/home.md).
