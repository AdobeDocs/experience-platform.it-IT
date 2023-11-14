---
title: Panoramica del connettore di origine di Amazon Kinesis
description: Scopri come collegare Amazon Kinesis a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# [!DNL Amazon Kinesis] sorgente

>[!IMPORTANT]
>
>Il [!DNL Amazon Kinesis] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Adobe Experience Platform fornisce connettività nativa per i provider di cloud come AWS, [!DNL Google Cloud Platform], e [!DNL Azure]. È possibile inserire i dati da questi sistemi in [!DNL Platform].

Le origini di archiviazione cloud possono inserire i tuoi dati in [!DNL Platform] senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come XDM JSON, XDM Parquet o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini. [!DNL Platform] consente di inserire dati da [!DNL Amazon Kinesis] in tempo reale.

>[!NOTE]
>
>Fattore di scala per [!DNL Kinesis] deve essere aumentata se devi acquisire dati con volumi elevati. Attualmente, il volume massimo di dati che puoi portare dal tuo [!DNL Kinesis] l’account per Platform è di 4000 record al secondo. Per aumentare e acquisire dati con volumi più elevati, contatta il rappresentante del tuo Adobe.

## Prerequisiti

La sezione seguente fornisce ulteriori informazioni sui prerequisiti necessari per la creazione di un [!DNL Kinesis] connessione sorgente.

### Configurare i criteri di accesso

A [!DNL Kinesis] per creare una connessione di origine, il flusso richiede le seguenti autorizzazioni:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Queste autorizzazioni sono organizzate tramite [!DNL Kinesis] e sono controllati da Platform dopo aver immesso le credenziali e selezionato il flusso di dati.

L’esempio seguente mostra i diritti di accesso minimi necessari per creare un [!DNL Kinesis] connessione sorgente.

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
| `kinesis:GetShardIterator` | Azione necessaria per scorrere i record. |
| `kinesis:GetRecords` | Azione necessaria per ottenere record da un ID di offset o di partizione specifico. |
| `kinesis:DescribeStream` | Azione che restituisce informazioni relative al flusso, inclusa la mappa di partizioni, necessaria per generare un ID di partizione. |
| `kinesis:ListStreams` | Azione necessaria per elencare i flussi disponibili che è possibile selezionare dall’interfaccia utente. |

Per ulteriori informazioni sul controllo dell&#39;accesso per [!DNL Kinesis] flussi di dati, vedi quanto segue [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Configura tipo di iteratore

[!DNL Kinesis] supporta i seguenti tipi di iteratore per specificare l&#39;ordine di lettura dei dati:

| Tipo di iteratore | Descrizione |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | I dati vengono letti a partire da una posizione identificata da un numero di sequenza specifico. |
| `AFTER_SEQUENCE_NUMBER` | I dati vengono letti a partire dalla posizione identificata da un numero di sequenza specifico. |
| `AT_TIMESTAMP` | I dati vengono letti a partire da una posizione identificata da una marca temporale specifica. |
| `TRIM_HORIZON` | I dati vengono letti a partire dal record di dati meno recente. |
| `LATEST` | I dati vengono letti a partire dal record di dati più recente. |

A [!DNL Kinesis] L’origine dell’interfaccia utente attualmente supporta solo `TRIM_HORIZON`, mentre l’API supporta entrambi `TRIM_HORIZON` e `LATEST` come modalità per ottenere i dati. Il valore iteratore predefinito utilizzato da Platform per [!DNL Kinesis] sorgente è `TRIM_HORIZON`.

Per ulteriori informazioni sui tipi di iteratore, vedere [[!DNL Kinesis] documento](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Connetti [!DNL Amazon Kinesis] a [!DNL Platform]

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Amazon Kinesis] a [!DNL Platform] utilizzando le API o l’interfaccia utente:

### Utilizzo delle API

- [Creare una connessione sorgente Amazon Kinesis utilizzando l’API del servizio Flusso](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Raccogliere dati in streaming utilizzando l’API del servizio Flusso](../../tutorials/api/collect/streaming.md)

### Utilizzo dell’interfaccia utente

- [Creare una connessione sorgente Amazon Kinesis nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configurare un flusso di dati per una connessione all’archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
