---
keywords: ' Experience Platform;home;argomenti popolari;Azure Event Hubs;azure event hubs;Event Hubs;event hubs;hubs'
solution: Experience Platform
title: Connettore Azure Event Hubs
topic: overview
description: La documentazione seguente fornisce informazioni su come collegare gli hub eventi di Azure alla piattaforma utilizzando le API o l'interfaccia utente.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# (Beta) Connettore Azure Event Hubs

>[!NOTE]
>
>Il connettore Azure Event Hubs è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, vedere [Panoramica delle sorgenti](../../home.md#terms-and-conditions).

Adobe Experience Platform fornisce connettività nativa per i fornitori di cloud come AWS, [!DNL Google Cloud Platform] e [!DNL Azure]. È possibile trasferire i dati da questi sistemi in [!DNL Platform].

Le origini di archiviazione cloud possono portare i tuoi dati in [!DNL Platform] senza bisogno di scaricare, formattare o caricare. I dati ingeriti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni fase del processo è integrata nel flusso di lavoro Origini. [!DNL Platform] consente di inserire dati  [!DNL Azure Event Hubs] in tempo reale.

## Indirizzo IP  elenco consentiti

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti . Se non si aggiungono al elenco consentiti  gli indirizzi IP specifici per la regione, potrebbero verificarsi errori o prestazioni insufficienti quando si utilizzano le origini. Per ulteriori informazioni, vedere la pagina [Indirizzo IP  elenco consentiti](../../ip-address-allow-list.md).

## Connetti [!DNL Azure Event Hubs] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come connettersi [!DNL Azure Event Hubs] a [!DNL Platform] utilizzando le API o l&#39;interfaccia utente:

### Utilizzo delle API

- [Creare un connettore Azure Event Hubs utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Raccogli i dati di streaming tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/streaming.md)

### Utilizzo dell’interfaccia

- [Creare un connettore di origine Azure Event Hubs nell&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configurare un flusso di dati per un connettore di archiviazione cloud nell&#39;interfaccia utente](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)