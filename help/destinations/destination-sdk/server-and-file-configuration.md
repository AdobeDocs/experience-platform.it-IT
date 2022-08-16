---
description: Le specifiche di configurazione del server e del file per le destinazioni basate su file possono essere configurate in Adobe Experience Platform Destination SDK tramite l'endpoint /destination-server.
title: (Beta) Opzioni di configurazione per specifiche del server di destinazione basate su file
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: a43bb18182ac6e591e011b585719da955ee681b7
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 13%

---

# (Beta) Configurazione del server e dei file per specifiche del server di destinazione basate su file

## Panoramica {#overview}

>[!IMPORTANT]
>
>La funzionalità per configurare e inviare destinazioni basate su file tramite Adobe Experience Platform Destination SDK è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Questa pagina descrive tutte le opzioni di configurazione del server per i server di destinazione basati su file e illustra come impostare varie opzioni di configurazione dei file per gli utenti che esportano i file dall’Experience Platform alla destinazione.

Le specifiche di configurazione del server e del file per le destinazioni basate su file possono essere configurate in Adobe Experience Platform Destination SDK tramite il `/destination-servers` punto finale. Leggi [Operazioni endpoint API del server di destinazione](./destination-server-api.md) per un elenco completo delle operazioni eseguibili sull&#39;endpoint.

## Specifiche del server di destinazione Amazon S3 basate su file {#s3-example}

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Amazon S3]imposta su `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Stringa | Nome della [!DNL Amazon S3] bucket utilizzato da questa destinazione. |
| `fileBasedS3Destination.path.templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |
| `fileConfigurations` | Oggetto | Vedi [configurazione della formattazione dei file](#file-configuration) per spiegazioni dettagliate su questa sezione. |

{style=&quot;table-layout:auto&quot;}

## Specifiche del server di destinazione SFTP basato su file {#sftp-example}

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL SFTP] destinazioni, imposta su `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | Stringa | Directory principale dell&#39;archivio di destinazione. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | Stringa | Nome host dell&#39;archivio di destinazione. |
| `port` | Intero | La porta del file server SFTP. |
| `encryptionMode` | Stringa | Indica se utilizzare la crittografia dei file. Valori supportati: <ul><li>PGP</li><li>Nessuna</li></ul> |
| `fileConfigurations` | Oggetto | Vedi [configurazione della formattazione dei file](#file-configuration) per spiegazioni dettagliate su questa sezione. |

{style=&quot;table-layout:auto&quot;}

## Basato su file [!DNL Azure Data Lake Storage] ([!DNL ADLS]) specifica del server di destinazione {#adls-example}

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Azure Data Lake Storage] destinazioni, imposta su `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |
| `fileConfigurations` | Oggetto | Vedi [configurazione della formattazione dei file](#file-configuration) per spiegazioni dettagliate su questa sezione. |

{style=&quot;table-layout:auto&quot;}

## Basato su file [!DNL Azure Blob Storage] specifica del server di destinazione {#blob-example}

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Azure Blob Storage] destinazioni, imposta su `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Stringa | Nome della [!DNL Azure Blob Storage] contenitore utilizzato da questa destinazione. |
| `fileConfigurations` | Oggetto | Vedi [configurazione della formattazione dei file](#file-configuration) per spiegazioni dettagliate su questa sezione. |

{style=&quot;table-layout:auto&quot;}

## Basato su file [!DNL Data Landing Zone] ([!DNL DLZ]) specifica del server di destinazione {#dlz-example}

```json
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Data Landing Zone] destinazioni, imposta su `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Stringa | *Obbligatorio.*  Seleziona `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |
| `fileConfigurations` | Oggetto | Vedi [configurazione della formattazione dei file](#file-configuration) per spiegazioni dettagliate su questa sezione. |

{style=&quot;table-layout:auto&quot;}

## Basato su file [!DNL Google Cloud Storage] specifica del server di destinazione {#gcs-example}

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
   "fileConfigurations":{
      // See the file formatting configuration section further below on this page
   }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Google Cloud Storage] destinazioni, imposta su `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Stringa | *Obbligatorio.*  Seleziona `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Stringa | Nome della [!DNL Google Cloud Storage] bucket utilizzato da questa destinazione. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |
| `fileConfigurations` | Oggetto | Vedi [configurazione della formattazione dei file](#file-configuration) per spiegazioni dettagliate su questa sezione. |

{style=&quot;table-layout:auto&quot;}

## Configurazione della formattazione dei file {#file-configuration}

Questa sezione descrive le impostazioni di formattazione del file per l&#39;esportazione `CSV` file. È possibile modificare diverse proprietà dei file esportati in modo che corrispondano ai requisiti del sistema di ricezione dei file sul proprio lato, al fine di leggere e interpretare in modo ottimale i file ricevuti da Experience Platform.

>[!NOTE]
>
>Le opzioni CSV sono supportate solo durante l’esportazione di file CSV. La `fileConfigurations` La sezione non è obbligatoria quando si imposta un nuovo server di destinazione. Se non trasmetti alcun valore nella chiamata API per le opzioni CSV, verranno utilizzati quelli predefiniti dalla tabella seguente.

```json
"fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        },
        "maxFileRowCount":5000000
    }
```

| Campo | Obbligatorio/facoltativo | Descrizione | Valore predefinito |
|---|---|---|---|
| `compression.value` | Facoltativo | Codec di compressione da utilizzare per il salvataggio dei dati su file. Valori supportati: `none`, `bzip2`, `gzip`, `lz4`e `snappy`. | `none` |
| `fileType.value` | Facoltativo | Specifica il formato del file di output. Valori supportati: `csv`, `parquet`e `json`. | `csv` |
| `csvOptions.quote.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta un singolo carattere utilizzato per l&#39;escape dei valori tra virgolette in cui il separatore può far parte del valore. | `null` |
| `csvOptions.quoteAll.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se tutti i valori devono sempre essere racchiusi tra virgolette. L&#39;impostazione predefinita prevede l&#39;escape solo di valori contenenti virgolette. | `false` |
| `csvOptions.escape.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta un singolo carattere utilizzato per l&#39;escape delle virgolette all&#39;interno di un valore già citato. | `\` |
| `csvOptions.escapeQuotes.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se i valori contenenti virgolette devono sempre essere racchiusi tra virgolette. L&#39;impostazione predefinita prevede l&#39;escape di tutti i valori contenenti un carattere di virgolette. | `true` |
| `csvOptions.header.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se scrivere i nomi delle colonne come prima riga. | `true` |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se tagliare i valori degli spazi vuoti iniziali. | `true` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se tagliare gli spazi bianchi finali dai valori. | `true` |
| `csvOptions.nullValue.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta la rappresentazione stringa di un valore null. | `""` |
| `csvOptions.dateFormat.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica il formato della data. | `yyyy-MM-dd` |
| `csvOptions.timestampFormat.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta la stringa che indica un formato di marca temporale. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` |
| `csvOptions.charToEscapeQuoteEscaping.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta un singolo carattere utilizzato per l&#39;escape del carattere di escape del virgolette. | `\` quando i caratteri di escape e virgolette sono diversi. `\0` quando il carattere di escape e virgolette sono gli stessi. |
| `csvOptions.emptyValue.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta la rappresentazione stringa di un valore vuoto. | `""` |
| `maxFileRowCount` | Facoltativo | Numero massimo di righe che il file esportato può contenere. Configuralo in base ai requisiti di dimensione del file della piattaforma di destinazione. | N/D |

{style=&quot;table-layout:auto&quot;}