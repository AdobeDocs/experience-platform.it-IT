---
description: Il servizio Destinazioni in Adobe Experience Platform utilizza modelli di configurazione per diversi componenti che creano la funzionalità Destinazioni. Combinati, questi componenti consentono ad Experience Platform di connettersi ai partner di destinazione, inviare messaggi personalizzati e attivare i dati di profilo nell’ecosistema digitale.
title: Opzioni di configurazione in Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 1%

---

# Opzioni di configurazione in Destination SDK

## Panoramica {#overview}

Il servizio Destinazioni in Adobe Experience Platform utilizza modelli di configurazione per diversi componenti che creano la funzionalità Destinazioni. Combinati, questi componenti consentono ad Experience Platform di connettersi ai partner di destinazione, inviare messaggi personalizzati e attivare i dati di profilo nell’ecosistema digitale. I modelli utilizzati in Adobe Experience Platform sono:

* **Configurazione della destinazione**: Contiene informazioni di base sulla destinazione. Questa configurazione include i tipi di identità supportati dalla destinazione e vari attributi dell&#39;interfaccia utente per la scheda di destinazione nell&#39;interfaccia utente di Adobe Experience Platform.
* **Specifiche del server e del modello**: Collega le informazioni sulle specifiche del server e sul modello utilizzato da Adobe per distribuire i payload alla destinazione.
   * **Specifiche del server**: Un modello che memorizza i dettagli dell’endpoint.
   * **Specifiche dei modelli**: In questo modello, puoi definire come trasformare i campi dell’attributo di profilo tra lo schema XDM e il formato supportato dalla piattaforma. Per informazioni approfondite sui linguaggi di template supportati, sui formati dei messaggi e sulle informazioni richieste da Adobe per configurare l&#39;integrazione con la piattaforma, consulta [Formato del messaggio](./message-format.md).
* **Configurazione dell’autenticazione**: Queste impostazioni definiscono il modo in cui gli utenti Adobe Experience Platform si connettono alla tua destinazione.
* **Configurazione dei metadati del pubblico**: Questo modello ti consente di configurare il modo in cui i tipi di pubblico/segmenti vengono creati, aggiornati o eliminati a livello di programmazione nella destinazione.

![Destination SDK modelli e configurazioni](./assets/self-service-configuration.png)

## Collegamenti correlati {#related-links}

Le pagine seguenti forniscono ulteriori dettagli sulle funzionalità e sulle opzioni di configurazione disponibili in Destination SDK e sulle operazioni API corrispondenti che puoi eseguire.

| Descrizione funzionalità | Riferimento API |
|--- |--- |
| [Configurazione della destinazione](./destination-configuration.md) | [Operazioni degli endpoint API delle destinazioni](./destination-configuration-api.md) |
| [Specifiche del server e del modello](./server-and-template-configuration.md) | [Operazioni endpoint API server di destinazione](./destination-server-api.md) |
| [Configurazione dell’autenticazione](./authentication-configuration.md) | [Operazioni API per l’endpoint delle credenziali](./credentials-configuration-api.md) |
| [Gestione dei metadati del pubblico](./audience-metadata-management.md) | [Operazioni API per l’endpoint dei metadati del pubblico](./audience-metadata-api.md) |
| [Configurazione OAuth 2](./oauth2-authentication.md) | Configura utilizzando `customerAuthenticationConfigurations` nel [endpoint API /Destinazioni](./destination-configuration-api.md). |
| [Formato del messaggio](./message-format.md) | - |
| [Test di destinazione](./test-destination.md) | [Operazioni API per il test di destinazione](./destination-testing-api.md) |
| [Pubblicazione destinazione](./configure-destination-instructions.md#publish-destination) | [Operazioni API di pubblicazione della destinazione](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}
