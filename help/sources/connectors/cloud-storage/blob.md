---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connettore BLOB di Azure
topic: overview
translation-type: tm+mt
source-git-commit: 8e39cc206efa3fc314ae689845c88f0923ac1743
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Connettore BLOB di Azure

Adobe Experience Platform fornisce connettività nativa per fornitori di cloud come AWS [!DNL Google Cloud Platform], e [!DNL Azure]. È possibile inserire i dati da questi sistemi in [!DNL Platform].

Le origini di archiviazione cloud possono importare i tuoi dati [!DNL Platform] senza bisogno di scaricare, formattare o caricare. I dati ingeriti possono essere formattati come JSON XDM, parquet XDM o delimitati. Ogni fase del processo è integrata nel flusso di lavoro Origini. [!DNL Platform] consente di inserire dati da [!DNL Azure Blob] batch.

## Indirizzo IP  elenco consentiti

I seguenti indirizzi IP devono essere aggiunti a un elenco consentiti  prima di utilizzare i connettori di origine. Se non si aggiungono al elenco consentiti  gli indirizzi IP specifici per la regione, potrebbero verificarsi errori o prestazioni insufficienti quando si utilizzano le origini.

### Regione degli Stati Uniti d&#39;America

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Europa occidentale

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australia Est

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

La documentazione seguente fornisce informazioni su come collegare Azure Blob alla piattaforma utilizzando le API o l&#39;interfaccia utente:

## Connessione [!DNL Azure Blob] all&#39; [!DNL Platform] utilizzo delle API

- [Creare un connettore BLOB di Azure utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/cloud-storage/blob.md)
- [Esplora un sistema di archiviazione cloud utilizzando l&#39;API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Raccolta di dati di archiviazione cloud tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

## Collegare [!DNL Blob] e utilizzare S3 all&#39; [!DNL Platform] interfaccia utente

- [Creare un connettore di origine Azure Blob nell&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/blob.md)
- [Configurare un flusso di dati per un connettore di archiviazione cloud nell&#39;interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)