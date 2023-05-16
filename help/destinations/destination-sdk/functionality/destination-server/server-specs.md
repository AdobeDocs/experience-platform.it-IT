---
description: Scopri come configurare le specifiche del server di destinazione in Adobe Experience Platform Destination SDK tramite l’endpoint `/authoring/destination-servers`.
title: Specifiche server per le destinazioni create con Destination SDK
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 3%

---


# Specifiche server per le destinazioni create con Destination SDK

Le specifiche del server di destinazione definiscono il tipo di piattaforma di destinazione che riceverà i dati da Adobe Experience Platform e i parametri di comunicazione tra Platform e la destinazione. Per esempio:

* A [streaming](#streaming-example) la specifica del server di destinazione definisce l’endpoint del server HTTP che riceverà i messaggi HTTP da Platform. Per scoprire come configurare la formattazione delle chiamate HTTP all’endpoint, leggi la sezione [specifiche di templazione](templating-specs.md) pagina.
* Un [Amazon S3](#s3-example) specifica del server di destinazione definisce la [!DNL S3] nome e percorso del bucket in cui Platform esporterà i file.
* Un [SFTP](#sftp-example) la specifica del server di destinazione definisce il nome host, la directory principale, la porta di comunicazione e il tipo di crittografia del server SFTP in cui Platform esporterà i file.

Per capire dove si trova questo componente in un’integrazione creata con Destination SDK, consulta il diagramma nella sezione [opzioni di configurazione](../configuration-options.md) documentazione o consulta le seguenti pagine di panoramica della configurazione di destinazione:

* [Utilizza Destination SDK per configurare una destinazione di streaming](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

Puoi configurare le specifiche del server di destinazione tramite il `/authoring/destination-servers` punto finale. Per esempi dettagliati sulle chiamate API , consulta le pagine di riferimento API seguenti dove puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md)
* [Aggiornare una configurazione del server di destinazione](../../authoring-api/destination-server/update-destination-server.md)

Questa pagina mostra tutti i tipi di server di destinazione supportati da Destination SDK, con tutti i relativi parametri di configurazione. Quando crei la destinazione, sostituisci i valori dei parametri con i tuoi.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina, consulta la tabella seguente.

| Tipo di integrazione | Supporta funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |

Quando [creazione](../../authoring-api/destination-server/create-destination-server.md) o [aggiornamento](../../authoring-api/destination-server/update-destination-server.md) in un server di destinazione, utilizza una delle configurazioni del tipo di server descritte in questa pagina. A seconda dei requisiti di integrazione, sostituisci con i tuoi i valori dei parametri di esempio da questi esempi.

## Campi hardcoded rispetto a quelli templatizzati {#templatized-fields}

Quando crei un server di destinazione tramite Destination SDK, puoi definire i valori dei parametri di configurazione tramite codifica fissa nella configurazione o utilizzando campi templatizzati. I campi con modelli consentono di leggere i valori forniti dall’utente dall’interfaccia utente di Platform.

I parametri del server di destinazione hanno due campi configurabili. Queste opzioni determinano se si utilizzano valori hardcoded o templatized.

| Parametro | Tipo | Descrizione |
|---|---|---|
| `templatingStrategy` | Stringa | *Obbligatorio.* Definisce se è presente un valore hardcoded fornito tramite il `value` o un valore configurabile dall’utente nell’interfaccia utente. Valori supportati: <ul><li>`NONE`: Utilizza questo valore quando codifichi il valore del parametro tramite il `value` (vedi la riga successiva). Esempio:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: Utilizza questo valore quando desideri che gli utenti forniscano un valore di parametro nell’interfaccia utente. Esempio: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | Stringa | *Obbligatorio*. Definisce il valore del parametro. Tipi di valori supportati: <ul><li>**Valore hardcoded**: Utilizza un valore hardcoded (ad esempio `"value": "my-storage-bucket"`) se non è necessario che gli utenti immettano un valore di parametro nell’interfaccia utente. Quando si codifica un valore, `templatingStrategy` deve essere sempre impostato su `NONE`.</li><li>**Valore templatizzato**: Utilizzare un valore modello (ad esempio `"value": "{{customerData.bucket}}"`) quando desideri che gli utenti forniscano un valore di parametro nell&#39;interfaccia utente. Quando si utilizzano valori templatizzati, `templatingStrategy` deve essere sempre impostato su `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### Quando utilizzare campi hardcoded rispetto a quelli templatizzati

Sia i campi hardcoded che quelli templatizzati hanno un proprio utilizzo nella Destination SDK, a seconda del tipo di integrazione che si sta creando.

**Connessione alla destinazione senza l&#39;input dell&#39;utente**

Quando gli utenti [connettersi alla destinazione](../../../ui/connect-destination.md) nell’interfaccia utente di Platform, potresti voler gestire il processo di connessione di destinazione senza il relativo input.

A questo scopo, puoi codificare i parametri di connessione della piattaforma di destinazione nelle specifiche del server. Quando si utilizzano valori di parametro hardcoded nella configurazione del server di destinazione, la connessione tra Adobe Experience Platform e la piattaforma di destinazione viene gestita senza l’input dell’utente.

Nell’esempio seguente, un partner crea un server di destinazione Area di destinazione dati con `path.value` campo codificato.

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"NONE",
         "value":"Your/hardcoded/path/here"
      },
      "useCase": "Your use case"
   }
}
```

Di conseguenza, quando gli utenti passano attraverso il [esercitazione sulla connessione di destinazione](../../../ui/connect-destination.md), non visualizzano un [passaggio di autenticazione](../../../ui/connect-destination.md#authenticate). Al contrario, l’autenticazione viene gestita da Platform, come illustrato nell’immagine seguente.

![Immagine dell’interfaccia utente che mostra la schermata di autenticazione tra Platform e una destinazione DLZ.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Connessione alla destinazione con l&#39;input dell&#39;utente**

Quando la connessione tra Platform e la destinazione deve essere stabilita in seguito a un input utente specifico nell’interfaccia utente di Platform, ad esempio selezionando un endpoint API o fornendo un valore di campo, puoi utilizzare campi formattati nelle specifiche del server per leggere l’input dell’utente e connetterti alla piattaforma di destinazione.

Nell’esempio seguente, un partner crea un [in tempo reale (streaming)](#streaming-example) integrazione e `url.value` utilizza il parametro templatized `{{customerData.region}}` personalizzare parte dell’endpoint API in base all’input dell’utente.

```json
{
   "name":"Templatized API endpoint example",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.yourcompany.com/data/{{customerData.region}}/items"
      }
   }
}
```

Per consentire agli utenti di selezionare un valore dall’interfaccia utente di Platform, la `region` deve essere definito anche nella [configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md) come campo dati cliente, come illustrato di seguito:

```json
"customerDataFields":[
   {
      "name":"region",
      "title":"Region",
      "description":"Select an option",
      "type":"string",
      "isRequired":true,
      "readOnly":false,
      "enum":[
         "US",
         "EU"
      ]
   }
```

Di conseguenza, quando gli utenti passano attraverso il [esercitazione sulla connessione di destinazione](../../../ui/connect-destination.md), devono selezionare una regione prima di potersi connettere alla piattaforma di destinazione. Quando si collegano alla destinazione, il campo con modello `{{customerData.region}}` viene sostituito con il valore selezionato dall’utente nell’interfaccia utente, come illustrato di seguito.

![Immagine dell’interfaccia utente che mostra la schermata di connessione di destinazione con un selettore di area.](../../assets/functionality/destination-server/server-spec-template-region.png)

## Server di destinazione in tempo reale (streaming) {#streaming-example}

Questo tipo di server di destinazione consente di esportare i dati da Adobe Experience Platform alla destinazione tramite richieste HTTP. La configurazione del server contiene informazioni sul server che riceve i messaggi (il server sul tuo lato).

Questo processo distribuisce i dati utente sotto forma di serie di messaggi HTTP alla piattaforma di destinazione. I parametri seguenti formano il modello delle specifiche del server HTTP.

L’esempio seguente mostra un esempio di configurazione del server di destinazione per una destinazione in tempo reale (streaming).

```json
{
   "name":"Your destination server name",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{YOUR_API_ENDPOINT}"
      }
   }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | *Obbligatorio.* Rappresenta un nome descrittivo del server, visibile solo ad Adobe. Questo nome non è visibile ai partner o clienti. Esempio: `Moviestar destination server`. |
| `destinationServerType` | Stringa | *Obbligatorio.* Imposta questo su `URL_BASED` per le destinazioni di streaming. |
| `templatingStrategy` | Stringa | *Obbligatorio.* <ul><li>Utilizzo `PEBBLE_V1` se utilizzi un campo formattato invece di un valore hardcoded nel `value` campo . Utilizza questa opzione se disponi di un endpoint come: `https://api.moviestar.com/data/{{customerData.region}}/items`, in cui gli utenti devono selezionare la regione dell’endpoint dall’interfaccia utente di Platform. </li><li> Utilizzo `NONE` se sul lato Adobe non è necessaria alcuna trasformazione basata su modelli, ad esempio se si dispone di un endpoint come: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Stringa | *Obbligatorio.* Inserisci l’indirizzo dell’endpoint API a cui Experience Platform deve connettersi. |

{style="table-layout:auto"}

## [!DNL Amazon S3] server di destinazione {#s3-example}

Questo server di destinazione consente di esportare file contenenti dati Adobe Experience Platform nell’archivio Amazon S3.

L&#39;esempio seguente mostra un esempio di configurazione del server di destinazione per una destinazione Amazon S3.

```json
{
   "name":"Amazon S3 destination",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome del server di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per esportare i file in un [!DNL Amazon S3] secchio, imposta questo su `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `bucket.value` campo .<ul><li>Se desideri che i tuoi utenti inseriscano il loro nome di bucket nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, devi modellare il `value` per leggere un valore dal campo [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall&#39;utente. Questo caso d’uso è mostrato nell’esempio precedente.</li><li>Se utilizzi un nome di bucket codificato per l’integrazione, ad esempio `"bucket.value":"MyBucket"`quindi imposta questo valore su `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | Stringa | Nome della [!DNL Amazon S3] bucket utilizzato da questa destinazione. Può trattarsi di un campo con modello che leggerà il valore dal [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o da un valore hardcoded, come `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `path.value` campo .<ul><li>Se desideri che gli utenti inseriscano il proprio percorso nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, devi modellare il `path.value` per leggere un valore dal campo [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall&#39;utente. Questo caso d’uso è mostrato nell’esempio precedente.</li><li>Se utilizzi un percorso codificato per l’integrazione, ad esempio `"bucket.value":"/path/to/MyBucket"`quindi imposta questo valore su `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | Stringa | Il percorso del [!DNL Amazon S3] bucket utilizzato da questa destinazione. Può trattarsi di un campo con modello che leggerà il valore dal [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o da un valore hardcoded, come `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] server di destinazione {#sftp-example}

Questo server di destinazione ti consente di esportare file contenenti dati Adobe Experience Platform nel tuo [!DNL SFTP] server di storage.

L’esempio seguente mostra un esempio di configurazione del server di destinazione per una destinazione SFTP.

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port":22,
      "encryptionMode":"PGP"
   }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome del server di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per esportare i file in un [!DNL SFTP] destinazione, imposta su `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `rootDirectory.value` campo .<ul><li>Se desideri che gli utenti inseriscano il proprio percorso di directory principale nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, devi modellare il `rootDirectory.value` per leggere un valore fornito dall&#39;utente dal campo [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall&#39;utente. Questo caso d’uso è mostrato nell’esempio precedente.</li><li>Se utilizzi un percorso di directory radice hardcoded per l’integrazione, ad esempio `"rootDirectory.value":"Storage/MyDirectory"`quindi imposta questo valore su `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | Stringa | Percorso della directory che ospita i file esportati. Può trattarsi di un campo con modello che leggerà il valore dal [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o da un valore hardcoded, come `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `hostName.value` campo .<ul><li>Se desideri che i tuoi utenti inseriscano il loro nome host nell&#39;interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, devi modellare il `hostName.value` per leggere un valore fornito dall&#39;utente dal campo [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall&#39;utente. Questo caso d’uso è mostrato nell’esempio precedente.</li><li>Se utilizzi un nome host hardcoded per l&#39;integrazione, ad esempio `"hostName.value":"my.hostname.com"`quindi imposta questo valore su `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | Stringa | Il nome host del server SFTP. Può trattarsi di un campo con modello che leggerà il valore dal [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o da un valore hardcoded, come `"hostName.value":"my.hostname.com"`. |
| `port` | Intero | La porta del file server SFTP. |
| `encryptionMode` | Stringa | Indica se utilizzare la crittografia dei file. Valori supportati: <ul><li>PGP</li><li>Nessuna</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) server di destinazione {#adls-example}

Questo server di destinazione ti consente di esportare file contenenti dati Adobe Experience Platform nel tuo [!DNL Azure Data Lake Storage] conto.

L’esempio seguente mostra un esempio di configurazione di un server di destinazione per un [!DNL Azure Data Lake Storage] destinazione.

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Azure Data Lake Storage] destinazioni, imposta su `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `path.value` campo .<ul><li>Se desideri che i tuoi utenti inseriscano i loro [!DNL ADLS] percorso della cartella nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, devi modellare il `path.value` per leggere un valore dal campo [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall&#39;utente. Questo caso d’uso è mostrato nell’esempio precedente.</li><li>Se utilizzi un percorso codificato per l’integrazione, ad esempio `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`quindi imposta questo valore su `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | Stringa | Il percorso del [!DNL ADLS] cartella di archiviazione. Può trattarsi di un campo con modello che leggerà il valore dal [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o da un valore hardcoded, come `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] server di destinazione {#blob-example}

Questo server di destinazione ti consente di esportare file contenenti dati Adobe Experience Platform nel tuo [!DNL Azure Blob Storage] contenitore.

L’esempio seguente mostra un esempio di configurazione di un server di destinazione per un [!DNL Azure Blob Storage] destinazione.

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
   }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Azure Blob Storage] destinazioni, imposta su `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `path.value` campo .<ul><li>Se desideri che i tuoi utenti inseriscano i loro [!DNL Azure Blob] [URI account di archiviazione](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, devi modellare il `path.value` campo per leggere il valore dal [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall&#39;utente. Questo caso d’uso è mostrato nell’esempio precedente.</li><li>Se utilizzi un percorso codificato per l’integrazione, ad esempio `"path.value": "https://myaccount.blob.core.windows.net/"`quindi imposta questo valore su `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | Stringa | Il percorso del [!DNL Azure Blob] archiviazione. Può trattarsi di un campo con modello che leggerà il valore dal [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o da un valore hardcoded, come `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `container.value` campo .<ul><li>Se desideri che i tuoi utenti inseriscano i loro [!DNL Azure Blob] [nome del contenitore](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, devi modellare il `container.value` campo per leggere il valore dal [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall&#39;utente. Questo caso d’uso è mostrato nell’esempio precedente.</li><li>Se utilizzi un nome di contenitore hardcoded per l’integrazione, ad esempio `"path.value: myContainer"`quindi imposta questo valore su `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | Stringa | Nome del contenitore di archiviazione BLOB di Azure da utilizzare per questa destinazione. Può trattarsi di un campo con modello che leggerà il valore dal [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o da un valore hardcoded, come `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) server di destinazione {#dlz-example}

Questo server di destinazione ti consente di esportare file contenenti dati di Platform in un [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) archiviazione.

L’esempio seguente mostra un esempio di configurazione di un server di destinazione per un [!DNL Data Landing Zone] ([!DNL DLZ]).

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Data Landing Zone] destinazioni, imposta su `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `path.value` campo .<ul><li>Se desideri che i tuoi utenti inseriscano i loro [!DNL Data Landing Zone] nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, devi modellare il `path.value` per leggere un valore dal campo [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall&#39;utente. Questo caso d’uso è mostrato nell’esempio precedente.</li><li>Se utilizzi un percorso codificato per l’integrazione, ad esempio `"path.value": "https://myaccount.blob.core.windows.net/"`quindi imposta questo valore su `NONE`. |
| `fileBasedDlzDestination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] server di destinazione {#gcs-example}

Questo server di destinazione ti consente di esportare i file contenenti i dati di Platform nel tuo [!DNL Google Cloud Storage] conto.

L’esempio seguente mostra un esempio di configurazione di un server di destinazione per un [!DNL Google Cloud Storage] destinazione.

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
   }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Google Cloud Storage] destinazioni, imposta su `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `bucket.value` campo .<ul><li>Se desideri che i tuoi utenti inseriscano i loro [!DNL Google Cloud Storage] nome del bucket nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, devi modellare il `bucket.value` per leggere un valore dal campo [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall&#39;utente. Questo caso d’uso è mostrato nell’esempio precedente.</li><li>Se utilizzi un nome di bucket codificato per l’integrazione, ad esempio `"bucket.value": "my-bucket"`quindi imposta questo valore su `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Stringa | Nome della [!DNL Google Cloud Storage] bucket utilizzato da questa destinazione. Può trattarsi di un campo con modello che leggerà il valore dal [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o da un valore hardcoded, come `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `path.value` campo .<ul><li>Se desideri che i tuoi utenti inseriscano i loro [!DNL Google Cloud Storage] percorso del bucket nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, devi modellare il `path.value` per leggere un valore dal campo [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall&#39;utente. Questo caso d’uso è mostrato nell’esempio precedente.</li><li>Se utilizzi un percorso codificato per l’integrazione, ad esempio `"path.value": "/path/to/my-bucket"`quindi imposta questo valore su `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | Stringa | Il percorso del [!DNL Google Cloud Storage] cartella utilizzata da questa destinazione. Può trattarsi di un campo con modello che leggerà il valore dal [campi dati del cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o da un valore hardcoded, come `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti avere una migliore comprensione delle specifiche di un server di destinazione e di come configurarle.

Per ulteriori informazioni sugli altri componenti del server di destinazione, consulta i seguenti articoli:

* [Specifiche di templatura](templating-specs.md)
* [Formato del messaggio](message-format.md)
* [Configurazione della formattazione dei file](file-formatting.md)
