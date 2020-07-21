---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connettore HDFS
topic: overview
translation-type: tm+mt
source-git-commit: 340f5d0611e9e9eb4676018ee10c8a8aa08dbb2d
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# (Beta) Connettore [!DNL Apache] HDFS

>[!NOTE]
>Il connettore Apache HDFS è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../home.md#terms-and-conditions) Origini.

 Adobe Experience Platform offre connettività nativa per fornitori di cloud come AWS [!DNL Google Cloud Platform], e [!DNL Azure], consentendo di portare i dati da questi sistemi. I dati contenuti possono essere formattati come JSON, parquet o delimitati. Il supporto per i fornitori di archiviazione cloud include [!DNL Apache] HDFS.

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

La documentazione seguente fornisce informazioni su come collegare [!DNL Apache] HDFS all’ [!DNL Platform] utilizzo delle API o dell’interfaccia utente:

## Collegare [!DNL Apache] HDFS a [!DNL Platform] mediante le API

- [Creare un connettore HDFS utilizzando l&#39;API di servizio di flusso](../../tutorials/api/create/cloud-storage/hdfs.md)
- [Esplora un sistema di archiviazione cloud utilizzando l&#39;API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Raccolta di dati di archiviazione cloud tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

## Collegare [!DNL Apache] HDFS all’ [!DNL Platform] interfaccia utente

- [Creare un connettore sorgente Apache HDFS nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [Configurare un flusso di dati per un connettore di archiviazione cloud nell&#39;interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)