---
keywords: Experience Platform;home;argomenti popolari;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Panoramica del connettore sorgente Amazon Kinesis
topic-legacy: overview
description: Scopri come collegare Amazon Kinesis a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 481f72c5c630f6dbcbbfd3eee11c91787e780f3f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] connettore

Adobe Experience Platform fornisce connettività nativa per provider cloud come AWS, [!DNL Google Cloud Platform] e [!DNL Azure]. Puoi inserire i tuoi dati da questi sistemi in [!DNL Platform].

Le origini di archiviazione cloud possono inserire i tuoi dati in [!DNL Platform] senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini . [!DNL Platform] consente di inserire dati in tempo  [!DNL Amazon Kinesis] reale.

## Prerequisiti

La sezione seguente fornisce ulteriori informazioni sulla configurazione dei prerequisiti necessaria per creare una connessione sorgente [!DNL Kinesis].

### Imposta criteri di accesso

Un flusso [!DNL Kinesis] richiede le seguenti autorizzazioni per creare una connessione sorgente:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Queste autorizzazioni vengono organizzate attraverso la console [!DNL Kinesis] e controllate da Platform una volta immesse le credenziali e selezionate il flusso di dati.

Nell&#39;esempio seguente vengono visualizzati i diritti di accesso minimi necessari per creare una connessione sorgente [!DNL Kinesis].

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:GetShardIterator",
                "kinesis:GetRecords",
                "kinesis:DescribeStream",
                "kinesis:ListStreams"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `kinesis:GetShardIterator` | Un’azione necessaria per scorrere i record. |
| `kinesis:GetRecords` | Un&#39;azione necessaria per ottenere i record da un ID offset o condiviso specifico. |
| `kinesis:DescribeStream` | Un’azione che restituisce informazioni sul flusso, inclusa la mappa condivisa, necessaria per generare un ID condiviso. |
| `kinesis:ListStreams` | Un’azione necessaria per elencare i flussi disponibili che puoi selezionare dall’interfaccia utente. |

Per ulteriori informazioni sul controllo dell&#39;accesso per i flussi di dati [!DNL Kinesis], consulta il seguente [[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Configura il tipo di iteratore

[!DNL Kinesis] supporta i seguenti tipi di iteratore per consentire di specificare l’ordine di lettura dei dati:

| Tipo di iteratore | Descrizione |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | I dati vengono letti a partire da una posizione identificata da un numero di sequenza specifico. |
| `AFTER_SEQUENCE_NUMBER` | I dati vengono letti a partire dalla posizione identificata da un numero di sequenza specifico. |
| `AT_TIMESTAMP` | I dati vengono letti a partire da una posizione identificata da un timestamp specifico. |
| `TRIM_HORIZON` | I dati vengono letti a partire dal record di dati più vecchio. |
| `LATEST` | I dati vengono letti a partire dal record di dati più recente. |

Un’origine [!DNL Kinesis] dell’interfaccia utente supporta attualmente solo `TRIM_HORIZON`, mentre l’API supporta sia le modalità `TRIM_HORIZON` che `LATEST` per ottenere i dati. Il valore iteratore predefinito utilizzato da Platform per l&#39;origine [!DNL Kinesis] è `TRIM_HORIZON`.

Per ulteriori informazioni sui tipi di iteratore, consulta il seguente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Connetti [!DNL Amazon Kinesis] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come connettersi a [!DNL Amazon Kinesis] utilizzando le API o l&#39;interfaccia utente:[!DNL Platform]

### Utilizzo delle API

- [Creare una connessione sorgente Amazon Kinesis utilizzando l’API del servizio di flusso](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Raccogliere dati in streaming utilizzando l’API del servizio di flusso](../../tutorials/api/collect/streaming.md)

### Utilizzo dell’interfaccia

- [Creare una connessione sorgente Amazon Kinesis nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configurare un flusso di dati per una connessione di archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
