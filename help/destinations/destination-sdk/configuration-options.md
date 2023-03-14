---
description: Il servizio delle destinazioni in Adobe Experience Platform utilizza endpoint di configurazione per diversi componenti che creano la funzionalità delle destinazioni. La combinazione di questi componenti consente ad Experience Platform di connettersi ai partner di destinazione, inviare messaggi personalizzati e attivare i dati del profilo nell’ecosistema digitale.
title: Opzioni di configurazione in Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# Opzioni di configurazione in Destination SDK

## Panoramica {#overview}

Il servizio delle destinazioni in Adobe Experience Platform utilizza endpoint di configurazione per diversi componenti che creano la funzionalità delle destinazioni. La combinazione di questi componenti consente ad Experience Platform di connettersi alle piattaforme di destinazione, inviare messaggi personalizzati, esportare file personalizzati e attivare i dati del profilo nell’ecosistema digitale. Le configurazioni utilizzate in Adobe Experience Platform Destination SDK sono:

* **Configurazione della destinazione**: contiene informazioni di base sulla destinazione. Questa configurazione include i tipi di identità che la destinazione può supportare, il formato desiderato dei file esportati (per le destinazioni basate su file) e vari attributi dell’interfaccia utente per la scheda di destinazione nell’interfaccia utente di Adobe Experience Platform.
* **Specifiche di server, file e modelli**: collega le informazioni sulle specifiche del server e i modelli utilizzati da Adobe per distribuire i payload alla destinazione. Per le destinazioni basate su file, questa configurazione include anche i formati di formattazione e compressione file supportati per la destinazione.
   * **Specifiche del server**: modello di configurazione che contiene informazioni sulla posizione di archiviazione o sull’endpoint HTTP a cui vengono inviati i dati.&quot;
   * **Specifiche dei file**: modello di configurazione che include le opzioni di formattazione e compressione del file per la destinazione batch.
   * **Specifiche modello**: in questo modello, puoi definire come trasformare i campi dell’attributo del profilo tra lo schema XDM e il formato supportato dalla tua piattaforma. Per informazioni approfondite sui linguaggi di template supportati, i formati di messaggio e le informazioni richieste dall’Adobe per configurare l’integrazione con la piattaforma, leggi [Formato del messaggio](./message-format.md).
* **Configurazione dell’autenticazione**: queste impostazioni definiscono il modo in cui gli utenti di Adobe Experience Platform si connettono alla destinazione.
* **Configurazione dei metadati del pubblico**: questo endpoint di configurazione consente di configurare il modo in cui i tipi di pubblico e i segmenti vengono creati, aggiornati o eliminati a livello di programmazione nella destinazione. Per le destinazioni batch, consente di impostare una notifica ogni volta che i file vengono consegnati correttamente alla destinazione.

![Diagramma che mostra gli endpoint di configurazione della Destination SDK e come vengono utilizzati insieme.](./assets/self-service-configuration.png)

## Collegamenti correlati {#related-links}

Le pagine seguenti forniscono ulteriori dettagli sulle funzionalità e le opzioni di configurazione disponibili in Destination SDK, nonché sulle operazioni API corrispondenti che è possibile eseguire.

| Descrizione della funzionalità (destinazioni di streaming) | Descrizione della funzionalità (destinazioni batch) | Riferimento API |
|--- |--- |--- |
| [Opzioni di configurazione della destinazione](./destination-configuration.md) | [Opzioni di configurazione delle destinazioni basate su file](/help/destinations/destination-sdk/file-based-destination-configuration.md) | [Operazioni degli endpoint API per le destinazioni](./destination-configuration-api.md) |
| [Specifiche del server e del modello](./server-and-template-configuration.md) | [Specifiche di configurazione del server e dei file](/help/destinations/destination-sdk/server-and-file-configuration.md) | [Operazioni degli endpoint API dei server di destinazione](./destination-server-api.md) |
| [Configurazione dell’autenticazione](./authentication-configuration.md) | Come per le destinazioni di streaming. | È possibile configurare le informazioni di autenticazione per la destinazione tramite `customerAuthenticationConfigurations` parametri di `/destinations` endpoint. Ulteriori informazioni per [streaming](/help/destinations/destination-sdk/destination-configuration.md#customer-authentication-configurations) e [batch](/help/destinations/destination-sdk/file-based-destination-configuration.md#customer-authentication-configurations) destinazioni. |
| [Gestione dei metadati del pubblico](./audience-metadata-management.md) | Come per lo streaming. Consulta [esempio basato su file](/help/destinations/destination-sdk/audience-metadata-management.md#example-file-based) per capire come i metadati del pubblico possono essere utilizzati in un contesto di destinazione batch. | [Operazioni API per endpoint metadati pubblico](./audience-metadata-api.md) |
| [Configurazione OAuth 2](./oauth2-authentication.md) | Come per le destinazioni di streaming | Configurare utilizzando `customerAuthenticationConfigurations` parametro in [Endpoint API /destinations](./destination-configuration-api.md). |
| [Formato del messaggio](./message-format.md) | - | - |
| [Strumenti di prova per le destinazioni di streaming](./test-destination.md) | [Strumenti di test per destinazioni basate su file](/help/destinations/destination-sdk/file-based-destination-testing-overview.md) | [Operazioni API di test della destinazione](./destination-testing-api.md) |
| [Pubblicazione della destinazione](./configure-destination-instructions.md#publish-destination) | Come per le destinazioni di streaming | [Operazioni API di pubblicazione della destinazione](./destination-publish-api.md) |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, avrai una panoramica generale delle funzionalità fornite da Destination SDK e delle pagine da leggere per ulteriori informazioni su configurazioni specifiche. Quindi, puoi leggere le guide che includono tutti i passaggi per [configurare uno streaming](/help/destinations/destination-sdk/configure-destination-instructions.md) o un [destinazione basata su file](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) utilizzando Destination SDK.
