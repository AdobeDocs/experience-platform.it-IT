---
title: Note sulla versione di Adobe Experience Platform - Agosto 2021
description: Note sulla versione di agosto 2021 per Adobe Experience Platform.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 35%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 25 agosto 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Destinazioni](#destinations)
- [Observability Insights](#observability)
- [Profilo cliente in tempo reale](#profile)
- [Origini](#sources)

## Destinazioni {#destinations}

Le destinazioni sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione fluida dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | La destinazione Airship Attributes, precedentemente in versione beta, è ora generalmente disponibile. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | La destinazione Airship Tags, precedentemente in versione beta, è ora generalmente disponibile. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | La destinazione Braze, precedentemente in versione beta, è ora generalmente disponibile. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | Con la destinazione Elenco clienti di Pinterest, puoi creare tipi di pubblico dagli elenchi dei clienti, da persone che hanno visitato il tuo sito o che hanno già interagito con i tuoi contenuti su Pinterest. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Effettua il targeting dei tuoi follower e clienti esistenti nel Twitter e crea campagne di remarketing rilevanti attivando i tipi di pubblico incorporati in Adobe Experience Platform. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX è un’infrastruttura aggregata Verizon Media/Yahoo che ospita vari componenti che consentono a Verizon Media/Yahoo di scambiare dati con i propri partner esterni in modo sicuro, automatizzato e scalabile. |

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK è una suite di API di configurazione che consente di configurare i modelli di integrazione delle destinazioni, ad Experience Platform per fornire dati di pubblico e profilo all’endpoint, in base ai dati e ai formati di autenticazione scelti. Le configurazioni sono memorizzate in Experience Platform e possono essere recuperate tramite API per ulteriori aggiornamenti. |
| [Miglioramenti di usabilità per le destinazioni](../../destinations/ui/activation-overview.md) | I miglioramenti a livello di usabilità per le destinazioni consentono agli addetti al marketing di attivare facilmente i segmenti nelle destinazioni esistenti. |

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Observability Insights {#observability}

Observability Insights consente di monitorare le attività di Platform tramite l’utilizzo di metriche statistiche e notifiche di eventi.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Avvisi | Ora è possibile attivare importanti avvisi relativi ai flussi di lavoro in esecuzione su Platform. Dopo esserti iscritto a specifiche regole di avviso, riceverai notifiche ed e-mail nell’interfaccia utente quando si verifica un evento importante del ciclo di vita (ad esempio, l’acquisizione corretta dei dati) o se sono presenti problemi che richiedono la tua attenzione (ad esempio, un errore del flusso di acquisizione o un processo di segmentazione che richiede più tempo del previsto). Per ulteriori informazioni, vedere [panoramica avvisi](../../observability/alerts/overview.md). |

Per ulteriori informazioni sul servizio, consulta la [Panoramica di Observability Insights](../../observability/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati clienti in una visualizzazione unificata che offre un account utilizzabile e dotato di marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Sfogliare i profili per criterio di unione o identità | In Experience Platform, quando esplori i profili, ora puoi sfogliare per criterio di unione per visualizzare in anteprima 20 profili di esempio in base al criterio di unione selezionato. Puoi anche sfogliare per identità per cercare un profilo specifico utilizzando uno spazio dei nomi dell’identità e il relativo valore di identità. Per ulteriori informazioni, consulta la [Guida all&#39;interfaccia utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md). |

Per ulteriori informazioni sul Profilo cliente in tempo reale, inclusi tutorial e best practice per l’utilizzo dei dati del profilo, inizia consultando la [Panoramica sul Profilo cliente in tempo reale](../../profile/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

| Funzione | Descrizione |
| ------- | ----------- |
| Connettore di origine per il caricamento di file locali | La categoria di acquisizione dei file è stata rinominata nel sistema locale, consentendo di portare i file locali direttamente in Platform utilizzando il connettore di caricamento file locale. I dati acquisiti tramite questo connettore possono essere monitorati tramite il dashboard di monitoraggio. Per ulteriori informazioni, vedere [panoramica origine caricamento file locale](../../sources/connectors/local-system/local-file-upload.md). |

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
