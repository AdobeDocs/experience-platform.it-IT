---
keywords: Experience Platform;home;argomenti popolari;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Panoramica del connettore sorgente Amazon Kinesis
topic-legacy: overview
description: Scopri come collegare Amazon Kinesis a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 5f4355a9d3ef39ee63581fc70dbf0f6e7d674814
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] connettore

Adobe Experience Platform fornisce connettività nativa per fornitori di cloud come AWS, [!DNL Google Cloud Platform]e [!DNL Azure]. È possibile inserire i dati di questi sistemi in [!DNL Platform].

Le origini di archiviazione cloud possono importare i tuoi dati [!DNL Platform] senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini . [!DNL Platform] consente di inserire dati da [!DNL Amazon Kinesis] in tempo reale.

>[!NOTE]
>
>Fattore di scala per [!DNL Kinesis] deve essere aumentato se è necessario acquisire dati con volumi elevati. Attualmente, il volume massimo di dati che puoi ottenere dal tuo [!DNL Kinesis] L’account a Platform è di 4000 record al secondo. Per ingrandire e acquisire dati di volume più elevati, contattare il rappresentante di Adobe.

## Prerequisiti

La sezione seguente fornisce ulteriori informazioni sulla configurazione dei prerequisiti necessaria per creare un [!DNL Kinesis] connessione di origine.

### Imposta criteri di accesso

A [!DNL Kinesis] per creare una connessione di origine, lo streaming richiede le seguenti autorizzazioni:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Queste autorizzazioni sono organizzate tramite [!DNL Kinesis] e vengono controllati da Platform una volta immesse le credenziali e selezionate il flusso di dati.

Nell’esempio seguente vengono visualizzati i diritti di accesso minimi necessari per creare un [!DNL Kinesis] connessione di origine.

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

Per ulteriori informazioni sul controllo dell&#39;accesso per [!DNL Kinesis] flussi di dati, vedi [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Configura il tipo di iteratore

[!DNL Kinesis] supporta i seguenti tipi di iteratore per consentire di specificare l’ordine di lettura dei dati:

| Tipo di iteratore | Descrizione |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | I dati vengono letti a partire da una posizione identificata da un numero di sequenza specifico. |
| `AFTER_SEQUENCE_NUMBER` | I dati vengono letti a partire dalla posizione identificata da un numero di sequenza specifico. |
| `AT_TIMESTAMP` | I dati vengono letti a partire da una posizione identificata da un timestamp specifico. |
| `TRIM_HORIZON` | I dati vengono letti a partire dal record di dati più vecchio. |
| `LATEST` | I dati vengono letti a partire dal record di dati più recente. |

A [!DNL Kinesis] L&#39;origine dell&#39;interfaccia attualmente supporta solo `TRIM_HORIZON`, mentre l’API supporta entrambi `TRIM_HORIZON` e `LATEST` come modalità per ottenere i dati. Il valore iteratore predefinito utilizzato da Platform per la [!DNL Kinesis] source `TRIM_HORIZON`.

Per ulteriori informazioni sui tipi di iteratore, consulta quanto segue [[!DNL Kinesis] documento](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Connetti [!DNL Amazon Kinesis] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come connettersi [!DNL Amazon Kinesis] a [!DNL Platform] utilizzando le API o l’interfaccia utente:

### Utilizzo delle API

- [Creare una connessione sorgente Amazon Kinesis utilizzando l’API del servizio di flusso](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Raccogliere dati in streaming utilizzando l’API del servizio di flusso](../../tutorials/api/collect/streaming.md)

### Utilizzo dell’interfaccia

- [Creare una connessione sorgente Amazon Kinesis nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configurare un flusso di dati per una connessione di archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
