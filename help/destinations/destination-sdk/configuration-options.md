---
description: Il servizio Destinazioni in Adobe Experience Platform utilizza gli endpoint di configurazione per diversi componenti che generano la funzionalità Destinazioni. Combinati, questi componenti consentono ad Experience Platform di connettersi ai partner di destinazione, inviare messaggi personalizzati e attivare i dati di profilo nell’ecosistema digitale.
title: Opzioni di configurazione in Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---

# Opzioni di configurazione in Destination SDK

## Panoramica {#overview}

Il servizio Destinazioni in Adobe Experience Platform utilizza gli endpoint di configurazione per diversi componenti che generano la funzionalità Destinazioni. Combinati, questi componenti consentono ad Experience Platform di connettersi alle piattaforme di destinazione, inviare messaggi personalizzati, esportare file personalizzati e attivare i dati di profilo nell’ecosistema digitale. Le configurazioni utilizzate in Adobe Experience Platform Destination SDK sono:

* **Configurazione della destinazione**: Contiene informazioni di base sulla destinazione. Questa configurazione include i tipi di identità supportati dalla destinazione, il formato desiderato per i file esportati (per le destinazioni basate su file) e vari attributi dell&#39;interfaccia utente per la scheda di destinazione nell&#39;interfaccia utente di Adobe Experience Platform.
* **Specifiche di server, file e modelli**: Collega le informazioni sulle specifiche del server e sul modello utilizzato da Adobe per distribuire i payload alla destinazione. Per le destinazioni basate su file, questa configurazione include anche i formati di formattazione e compressione supportati per la destinazione.
   * **Specifiche del server**: Un modello di configurazione che contiene informazioni sulla posizione di archiviazione o sull&#39;endpoint HTTP a cui vengono inviati i dati.&quot;
   * **Specifiche dei file**: Un modello di configurazione che include le opzioni di formattazione e compressione del file per la destinazione batch.
   * **Specifiche dei modelli**: In questo modello, puoi definire come trasformare i campi dell’attributo di profilo tra lo schema XDM e il formato supportato dalla piattaforma. Per informazioni approfondite sui linguaggi di template supportati, sui formati dei messaggi e sulle informazioni richieste da Adobe per configurare l&#39;integrazione con la piattaforma, consulta [Formato del messaggio](./message-format.md).
* **Configurazione dell’autenticazione**: Queste impostazioni definiscono il modo in cui gli utenti Adobe Experience Platform si connettono alla tua destinazione.
* **Configurazione dei metadati del pubblico**: Questo endpoint di configurazione ti consente di configurare il modo in cui i tipi di pubblico/segmenti vengono creati, aggiornati o eliminati a livello di programmazione nella destinazione. Per le destinazioni batch, ti consente di impostare una notifica ogni volta che i file vengono consegnati correttamente alla tua destinazione.

![Diagramma che mostra gli endpoint di configurazione della Destination SDK e il modo in cui questi vengono utilizzati insieme.](./assets/self-service-configuration.png)

## Collegamenti correlati {#related-links}

Le pagine seguenti forniscono ulteriori dettagli sulle funzionalità e sulle opzioni di configurazione disponibili in Destination SDK e sulle operazioni API corrispondenti che puoi eseguire.

| Descrizione delle funzionalità (destinazioni di streaming) | Descrizione delle funzionalità (destinazioni batch) | Riferimento API |
|--- |--- |--- |
| [Opzioni di configurazione della destinazione](./destination-configuration.md) | [Opzioni di configurazione della destinazione basata su file](/help/destinations/destination-sdk/file-based-destination-configuration.md) | [Operazioni degli endpoint API delle destinazioni](./destination-configuration-api.md) |
| [Specifiche del server e del modello](./server-and-template-configuration.md) | [Specifiche di configurazione del server e del file](/help/destinations/destination-sdk/server-and-file-configuration.md) | [Operazioni endpoint API server di destinazione](./destination-server-api.md) |
| [Configurazione dell’autenticazione](./authentication-configuration.md) | Come per le destinazioni di streaming. | Puoi configurare le informazioni di autenticazione per la tua destinazione tramite `customerAuthenticationConfigurations` dei parametri `/destinations` punto finale. Ulteriori informazioni [streaming](/help/destinations/destination-sdk/destination-configuration.md#customer-authentication-configurations) e [batch](/help/destinations/destination-sdk/file-based-destination-configuration.md#customer-authentication-configurations) destinazioni. |
| [Gestione dei metadati del pubblico](./audience-metadata-management.md) | Come per lo streaming. Vedi [esempio basato su file](/help/destinations/destination-sdk/audience-metadata-management.md#example-file-based) per comprendere come utilizzare i metadati del pubblico in un contesto di destinazione batch. | [Operazioni API per l’endpoint dei metadati del pubblico](./audience-metadata-api.md) |
| [Configurazione OAuth 2](./oauth2-authentication.md) | Come per le destinazioni di streaming | Configura utilizzando `customerAuthenticationConfigurations` nel [endpoint API /Destinazioni](./destination-configuration-api.md). |
| [Formato del messaggio](./message-format.md) | - | - |
| [Verifica degli strumenti per le destinazioni di streaming](./test-destination.md) | [Test degli strumenti per le destinazioni basate su file](/help/destinations/destination-sdk/file-based-destination-testing-overview.md) | [Operazioni API per il test di destinazione](./destination-testing-api.md) |
| [Pubblicazione destinazione](./configure-destination-instructions.md#publish-destination) | Come per le destinazioni di streaming | [Operazioni API di pubblicazione della destinazione](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}

## Passaggi successivi {#next-steps}

Leggendo questo articolo, disponi ora di una panoramica generale delle funzionalità fornite da Destination SDK e delle pagine da leggere per ulteriori informazioni sulle configurazioni specifiche. Successivamente, puoi leggere le guide che includono tutti i passaggi per [configurare uno streaming](/help/destinations/destination-sdk/configure-destination-instructions.md) o [destinazione basata su file](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) utilizzando la Destination SDK.
