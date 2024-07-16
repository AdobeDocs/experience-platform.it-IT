---
title: Panoramica del connettore Source di Amazon Kinesis
description: Scopri come collegare Amazon Kinesis a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Origine [!DNL Amazon Kinesis]

>[!IMPORTANT]
>
>L&#39;origine [!DNL Amazon Kinesis] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Adobe Experience Platform fornisce connettività nativa per i provider di cloud come AWS, [!DNL Google Cloud Platform] e [!DNL Azure]. È possibile inserire i dati da questi sistemi in [!DNL Platform].

Le origini di archiviazione cloud possono inserire i tuoi dati in [!DNL Platform] senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come XDM JSON, XDM Parquet o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini. [!DNL Platform] consente di inserire dati da [!DNL Amazon Kinesis] in tempo reale.

>[!NOTE]
>
>Il fattore di scala per [!DNL Kinesis] deve essere aumentato se è necessario acquisire dati di volume elevato. Attualmente, il volume massimo di dati che puoi portare dal tuo account [!DNL Kinesis] a Platform è di 4000 record al secondo. Per aumentare e acquisire dati con volumi più elevati, contatta il rappresentante del tuo Adobe.

## Prerequisiti

Nella sezione seguente vengono fornite ulteriori informazioni sui prerequisiti necessari per creare una connessione di origine [!DNL Kinesis].

### Configurare i criteri di accesso

Un flusso [!DNL Kinesis] richiede le seguenti autorizzazioni per creare una connessione di origine:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Queste autorizzazioni sono organizzate tramite la console [!DNL Kinesis] e vengono verificate da Platform dopo aver immesso le credenziali e selezionato il flusso di dati.

Nell&#39;esempio seguente vengono visualizzati i diritti di accesso minimi necessari per creare una connessione di origine [!DNL Kinesis].

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

Per ulteriori informazioni sul controllo dell&#39;accesso per [!DNL Kinesis] flussi di dati, vedere il seguente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Configura tipo di iteratore

[!DNL Kinesis] supporta i seguenti tipi di iteratore per consentire di specificare l&#39;ordine di lettura dei dati:

| Tipo di iteratore | Descrizione |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | I dati vengono letti a partire da una posizione identificata da un numero di sequenza specifico. |
| `AFTER_SEQUENCE_NUMBER` | I dati vengono letti a partire dalla posizione identificata da un numero di sequenza specifico. |
| `AT_TIMESTAMP` | I dati vengono letti a partire da una posizione identificata da una marca temporale specifica. |
| `TRIM_HORIZON` | I dati vengono letti a partire dal record di dati meno recente. |
| `LATEST` | I dati vengono letti a partire dal record di dati più recente. |

Un&#39;origine dell&#39;interfaccia utente [!DNL Kinesis] attualmente supporta solo `TRIM_HORIZON`, mentre l&#39;API supporta sia `TRIM_HORIZON` che `LATEST` come modalità per ottenere i dati. Il valore predefinito dell&#39;iteratore utilizzato da Platform per l&#39;origine [!DNL Kinesis] è `TRIM_HORIZON`.

Per ulteriori informazioni sui tipi di iteratore, vedere il [[!DNL Kinesis] documento](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax) seguente.

## Connetti [!DNL Amazon Kinesis] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come connettere [!DNL Amazon Kinesis] a [!DNL Platform] tramite API o l&#39;interfaccia utente:

### Utilizzo delle API

- [Creare una connessione sorgente Amazon Kinesis utilizzando l’API del servizio Flusso](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Raccogliere dati in streaming utilizzando l’API del servizio Flusso](../../tutorials/api/collect/streaming.md)

### Utilizzo dell’interfaccia utente

- [Creare una connessione sorgente Amazon Kinesis nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configurare un flusso di dati per una connessione all’archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
