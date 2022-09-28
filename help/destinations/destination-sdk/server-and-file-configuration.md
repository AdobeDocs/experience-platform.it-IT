---
description: Le specifiche di configurazione del server e del file per le destinazioni basate su file possono essere configurate in Adobe Experience Platform Destination SDK tramite l'endpoint /destination-server.
title: Opzioni di configurazione per specifiche del server di destinazione basate su file
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 5506a938253083d3dfd657a787eae20a05b1c0a9
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 9%

---

# Configurazione del server e dei file per specifiche del server di destinazione basate su file

## Panoramica {#overview}

>[!IMPORTANT]
>
>La funzionalità per configurare e inviare destinazioni basate su file tramite Adobe Experience Platform Destination SDK è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Questa pagina descrive tutte le opzioni di configurazione del server per i server di destinazione basati su file e mostra come impostare varie opzioni di configurazione dei file per gli utenti che esportano i file dall’Experience Platform alla destinazione.

Le specifiche di configurazione del server e del file per le destinazioni basate su file possono essere configurate in Adobe Experience Platform Destination SDK tramite il `/destination-servers` punto finale. Leggi [Operazioni endpoint API del server di destinazione](./destination-server-api.md) per un elenco completo delle operazioni eseguibili sull&#39;endpoint.

Le sezioni seguenti includono le specifiche del server di destinazione specifiche per ciascun tipo di destinazione batch supportato nella Destination SDK.

## Specifiche del server di destinazione Amazon S3 basate su file {#s3-example}

L&#39;esempio seguente mostra una configurazione corretta del server di destinazione per una destinazione Amazon S3.

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

L’esempio seguente mostra una configurazione corretta del server di destinazione per una destinazione SFTP.

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

L&#39;esempio seguente mostra una configurazione corretta del server di destinazione per un [!DNL Azure Data Lake Storage] destinazione.

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

L&#39;esempio seguente mostra una configurazione corretta del server di destinazione per un [!DNL Azure Blob Storage] destinazione.

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

L&#39;esempio seguente mostra una configurazione corretta del server di destinazione per un [!DNL Data Landing Zone] ([!DNL DLZ]).

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

L&#39;esempio seguente mostra una configurazione corretta del server di destinazione per un [!DNL Google Cloud Storage] destinazione.

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
>Le opzioni CSV sono supportate solo durante l’esportazione di file CSV. La `fileConfigurations` La sezione non è obbligatoria quando si imposta un nuovo server di destinazione. Se non trasmetti alcun valore nella chiamata API per le opzioni CSV, quelli predefiniti dalla [tabella di riferimento successiva](#file-formatting-reference-and-example) verrà utilizzato.

### Configurazioni di file con le opzioni CSV e `templatingStrategy` impostato su `NONE` {#file-configuration-templating-none}

Nell’esempio di configurazione seguente, tutte le opzioni CSV sono fisse. Le impostazioni di esportazione definite in ciascuna delle `csvOptions` i parametri sono finali e gli utenti non possono modificarli.

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

### Configurazioni di file con le opzioni CSV e `templatingStrategy` impostato su `PEBBLE_V1` {#file-configuration-templating-pebble}

Nell’esempio di configurazione seguente, nessuna delle opzioni CSV è fissa. La `value` in ciascuno degli `csvOptions` è configurato in un campo dati cliente corrispondente tramite `/destinations` endpoint (ad esempio `customerData.quote` per `quote` opzione di formattazione dei file) e gli utenti possono utilizzare l&#39;interfaccia utente di Experience Platform per selezionare tra le varie opzioni configurate nel campo dati cliente corrispondente.

```json
  "fileConfigurations": {
    "compression": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
    },
    "fileType": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.fileType}}"
    },
    "csvOptions": {
      "sep": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
      },
      "quote": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
      },
      "escape": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
      },
      "nullValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
      },
      "emptyValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
      }
    }
  }
```

### Riferimento completo ed esempi delle opzioni di formattazione supportate {#file-formatting-reference-and-example}

>[!TIP]
>
>Le opzioni di formattazione del file CSV descritte di seguito sono documentate anche in [Guida di Apache Spark per file CSV](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). Le descrizioni utilizzate di seguito sono tratti dalla guida Apache Spark.

Di seguito è riportato un riferimento completo di tutte le opzioni di formattazione disponibili nella Destination SDK, insieme ad esempi di output per ogni opzione.

| Campo | Obbligatorio/facoltativo | Descrizione | Valore predefinito | Esempio di output 1 | Esempio di output 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Obbligatorio | Per ogni opzione di formattazione del file configurata, è necessario aggiungere il parametro `templatingStrategy`, che può avere due valori: <br><ul><li>`NONE`: utilizza questo valore se non intendi consentire agli utenti di scegliere tra valori diversi per una configurazione. Vedi [questa configurazione](#file-configuration-templating-none) per un esempio in cui le opzioni di formattazione dei file sono fisse.</li><li>`PEBBLE_V1`: utilizza questo valore se desideri consentire agli utenti di selezionare tra valori diversi per una configurazione. In questo caso, devi anche impostare un campo dati cliente corrispondente nel `/destination` configurazione dell’endpoint, per presentare le varie opzioni agli utenti nell’interfaccia utente. Vedi [questa configurazione](#file-configuration-templating-pebble) per un esempio in cui gli utenti possono scegliere tra diversi valori per le opzioni di formattazione dei file.</li></ul> | - | - | - |
| `compression.value` | Facoltativo | Codec di compressione da utilizzare per il salvataggio dei dati su file. Valori supportati: `none`, `bzip2`, `gzip`, `lz4`e `snappy`. | `none` | - | - |
| `fileType.value` | Facoltativo | Specifica il formato del file di output. Valori supportati: `csv`, `parquet`e `json`. | `csv` | - | - |
| `csvOptions.quote.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta un singolo carattere utilizzato per l&#39;escape dei valori tra virgolette in cui il separatore può far parte del valore. | `null` | - | - |
| `csvOptions.quoteAll.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se tutti i valori devono sempre essere racchiusi tra virgolette. L&#39;impostazione predefinita prevede l&#39;escape solo di valori contenenti virgolette. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta un separatore per ciascun campo e valore. Questo separatore può essere composto da uno o più caratteri. | `,` | `delimiter`:`,` —> `comma-separated values"` | `delimiter`:`\t` —> `tab-separated values` |
| `csvOptions.escape.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta un singolo carattere utilizzato per l&#39;escape delle virgolette all&#39;interno di un valore già citato. | `\` | `"escape"`:`"\\"` —> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` —> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se i valori contenenti virgolette devono sempre essere racchiusi tra virgolette. L&#39;impostazione predefinita prevede l&#39;escape di tutti i valori contenenti un carattere di virgolette. | `true` | - | - |
| `csvOptions.header.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se scrivere i nomi delle colonne come prima riga nel file esportato. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se tagliare i valori degli spazi vuoti iniziali. | `true` | `ignoreLeadingWhiteSpace`:`true` —> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica se tagliare gli spazi vuoti finali dai valori. | `true` | `ignoreTrailingWhiteSpace`:`true` —> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`—> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta la rappresentazione stringa di un valore null. | `""` | `nullvalue`:`""` —> `male,"",TestLastName` | `nullvalue`:`"NULL"` —> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Indica il formato della data. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` —> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` —> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta la stringa che indica un formato di marca temporale. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta un singolo carattere utilizzato per l&#39;escape del carattere di escape del virgolette. | `\` quando i caratteri di escape e virgolette sono diversi. `\0` quando il carattere di escape e virgolette sono gli stessi. | - | - |
| `csvOptions.emptyValue.value` | Facoltativo | *Solo per`"fileType.value": "csv"`*. Imposta la rappresentazione stringa di un valore vuoto. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` —> `male,empty,John` |

{style=&quot;table-layout:auto&quot;}