---
keywords: Experience Platform;home;popular topics;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Connettore Azure Event Hubs
topic: overview
description: La documentazione seguente fornisce informazioni su come collegare gli hub eventi di Azure alla piattaforma utilizzando le API o l'interfaccia utente.
translation-type: tm+mt
source-git-commit: e0a0b7fc28b8cc85c5140d3840e06e5c7078c307
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# (Beta) Connettore Azure Event Hubs

>[!NOTE]
>
>Il connettore Azure Event Hubs è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../home.md#terms-and-conditions) Origini.

Adobe Experience Platform fornisce connettività nativa per fornitori di cloud come AWS [!DNL Google Cloud Platform], e [!DNL Azure]. È possibile inserire i dati da questi sistemi in [!DNL Platform].

Le origini di archiviazione cloud possono importare i tuoi dati [!DNL Platform] senza bisogno di scaricare, formattare o caricare. I dati ingeriti possono essere formattati come JSON XDM, parquet XDM o delimitati. Ogni fase del processo è integrata nel flusso di lavoro Origini. [!DNL Platform] consente di inserire i dati in tempo [!DNL Azure Event Hubs] reale.

## Indirizzo IP  elenco consentiti

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti . Se non si aggiungono al elenco consentiti  gli indirizzi IP specifici per la regione, potrebbero verificarsi errori o prestazioni insufficienti quando si utilizzano le origini. Per ulteriori informazioni, vedere l&#39;indirizzo [IP  pagina di elenco consentiti](../../ip-address-allow-list.md) .

## Connetti [!DNL Azure Event Hubs] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come connettersi [!DNL Azure Event Hubs] all&#39; [!DNL Platform] utilizzo delle API o dell&#39;interfaccia utente:

### Utilizzo delle API

- [Creare un connettore Azure Event Hubs utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Esplora un sistema di archiviazione cloud utilizzando l&#39;API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Raccolta di dati di archiviazione cloud tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia

- [Creare un connettore di origine Azure Event Hubs nell&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configurare un flusso di dati per un connettore di archiviazione cloud nell&#39;interfaccia utente](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)