---
title: Note sulla versione di Adobe Experience Platform - Agosto 2021
description: Note sulla versione di agosto 2021 per Adobe Experience Platform.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '712'
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

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | La destinazione Attributi dell&#39;aeromobile, precedentemente in versione beta, è ora generalmente disponibile. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | La destinazione dei tag di bordo, precedentemente in versione beta, è ora generalmente disponibile. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | La destinazione Braze, precedentemente in versione beta, è ora generalmente disponibile. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | Con la destinazione Elenco clienti Pinterest, puoi creare tipi di pubblico dalle liste di clienti, da persone che hanno visitato il tuo sito o da persone che hanno già interagito con i tuoi contenuti su Pinterest. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Esegui il targeting dei tuoi follower e clienti esistenti in Twitter e crea campagne di ricommercializzazione pertinenti attivando i tuoi tipi di pubblico generati in Adobe Experience Platform. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX è un’infrastruttura globale Verizon Media/Yahoo che ospita vari componenti che consentono a Verizon Media/Yahoo di scambiare dati con i suoi partner esterni in modo sicuro, automatizzato e scalabile. |

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK è una suite di API di configurazione che ti consentono di configurare modelli di integrazione di destinazione, ad Experience Platform per distribuire i dati di pubblico e profilo all’endpoint, in base ai dati e ai formati di autenticazione scelti. Le configurazioni sono memorizzate in Experience Platform e possono essere recuperate tramite API per ulteriori aggiornamenti. |
| [Miglioramenti a livello di usabilità delle destinazioni](../../destinations/ui/activation-overview.md) | I miglioramenti a livello di usabilità per le destinazioni consentono agli addetti al marketing di attivare facilmente i segmenti sulle destinazioni esistenti. |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Informazioni sull’osservabilità {#observability}

Observability Insights consente di monitorare le attività di Platform tramite l’utilizzo di metriche statistiche e notifiche di eventi.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Avvisi | ora è possibile attivare importanti avvisi relativi ai flussi di lavoro in esecuzione su Platform. Dopo aver effettuato l’abbonamento a regole di avviso specifiche, riceverai notifiche ed e-mail nell’interfaccia utente quando si verifica un evento importante sul ciclo di vita (ad esempio l’inserimento di dati con esito positivo) o in caso di problemi che richiedono attenzione (ad esempio un errore nel flusso di acquisizione o un processo di segmento che richiede più tempo del previsto). Per ulteriori informazioni, consulta la sezione [panoramica degli avvisi](../../observability/alerts/overview.md). |

Consulta la sezione [Panoramica di Observability Insights](../../observability/home.md) per ulteriori informazioni sul servizio.

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Sfoglia i profili in base a criteri di unione o identità | Durante l’esplorazione dei profili in Experience Platform, ora è possibile sfogliare i criteri di unione per visualizzare in anteprima 20 profili di esempio in base al criterio di unione selezionato. È inoltre possibile sfogliare in base all’identità per cercare un profilo specifico utilizzando uno spazio dei nomi identità e il relativo valore di identità. Per ulteriori informazioni, consulta la sezione [Guida all’interfaccia utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md). |

Per ulteriori informazioni sul Profilo del cliente in tempo reale, compresi tutorial e best practice per l’utilizzo dei dati del profilo, consulta la sezione [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| ------- | ----------- |
| Connettore sorgente di caricamento file locale | La categoria di acquisizione dei file è stata rinominata nel sistema locale e consente di portare i file locali direttamente in Platform utilizzando il connettore di caricamento file locale. I dati acquisiti tramite questo connettore possono essere monitorati tramite il dashboard di monitoraggio. Consulta la sezione [panoramica dell’origine di caricamento file locale](../../sources/connectors/local-system/local-file-upload.md) per ulteriori informazioni. |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
