---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connettore Azure Data Lake Storage Gen2
topic: overview
translation-type: tm+mt
source-git-commit: 4d3899e8a91d15da7e40523a03285f3ccec27191
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Connettore Azure Data Lake Storage Gen2

 Adobe Experience Platform offre connettività nativa per fornitori di cloud come AWS [!DNL Google Cloud Platform], e [!DNL Azure], consentendo di portare i dati da questi sistemi.

Le origini di archiviazione cloud possono importare i tuoi dati [!DNL Platform] senza bisogno di scaricare, formattare o caricare. I dati ingeriti possono essere formattati come JSON XDM, parquet XDM o delimitati. Ogni fase del processo è integrata nel flusso di lavoro Origini. [!DNL Platform] consente di inserire i dati da [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2) attraverso i batch.

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

## Connetti [!DNL Azure Data Lake Storage Gen2] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come connettersi [!DNL Azure Data Lake Storage Gen2] all&#39; [!DNL Platform] utilizzo delle API o dell&#39;interfaccia utente:

### Utilizzo delle API

- [Creare un connettore ADLS-Gen2 utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Esplora un sistema di archiviazione cloud utilizzando l&#39;API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Raccolta di dati di archiviazione cloud tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

## Utilizzo dell’interfaccia

- [Creare un connettore di origine ADLS-Gen2 nell&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Configurare un flusso di dati per un connettore di archiviazione cloud nell&#39;interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)