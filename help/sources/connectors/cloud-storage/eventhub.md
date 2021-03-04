---
keywords: Experience Platform;home;argomenti popolari;hub eventi di Azure;hub eventi di Azure;hub eventi di Azure;hub eventi;hub eventi
solution: Experience Platform
title: Panoramica del connettore di origine per gli hub eventi di Azure
topic: ' - Panoramica'
description: Scopri come collegare gli hub eventi di Azure ad Adobe Experience Platform utilizzando le API o l’interfaccia utente.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# (Beta) Connettore Azure Event Hubs

>[!NOTE]
>
>Il connettore Azure Event Hubs è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../home.md#terms-and-conditions) .

Adobe Experience Platform fornisce connettività nativa per provider cloud come AWS, [!DNL Google Cloud Platform] e [!DNL Azure]. Puoi inserire i tuoi dati da questi sistemi in [!DNL Platform].

Le origini di archiviazione cloud possono inserire i tuoi dati in [!DNL Platform] senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini . [!DNL Platform] consente di inserire dati in tempo  [!DNL Azure Event Hubs] reale.

## Elenco indirizzi IP consentiti

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco di indirizzi IP un elenco di indirizzi IP consentiti . Se non aggiungi gli indirizzi IP specifici per l’area geografica all’elenco Consentiti, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Per ulteriori informazioni, consulta la pagina [Elenco indirizzi IP consentiti](../../ip-address-allow-list.md) .

## Connetti [!DNL Azure Event Hubs] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come connettersi a [!DNL Azure Event Hubs] utilizzando le API o l&#39;interfaccia utente:[!DNL Platform]

### Utilizzo delle API

- [Creare una connessione sorgente Azure Event Hubs utilizzando l’API del servizio di flusso](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Raccogliere dati in streaming utilizzando l’API del servizio di flusso](../../tutorials/api/collect/streaming.md)

### Utilizzo dell’interfaccia

- [Creare una connessione sorgente Azure Event Hubs nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configurare un flusso di dati per una connessione di archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)