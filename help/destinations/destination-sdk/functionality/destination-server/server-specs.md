---
description: Scopri come configurare le specifiche del server di destinazione in Adobe Experience Platform Destination SDK tramite l’endpoint "/authoring/destination-servers".
title: Specifiche del server per le destinazioni create con Destination SDK
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 3%

---


# Specifiche del server per le destinazioni create con Destination SDK

Le specifiche del server di destinazione definiscono il tipo di piattaforma di destinazione che riceverà i dati da Adobe Experience Platform e i parametri di comunicazione tra Platform e la destinazione. Ad esempio:

* A [streaming](#streaming-example) La specifica del server di destinazione definisce l’endpoint del server HTTP che riceverà i messaggi HTTP da Platform. Per informazioni su come configurare la formattazione delle chiamate HTTP all’endpoint, leggi [specifiche modelli](templating-specs.md) pagina.
* Un [Amazon S3](#s3-example) specifica del server di destinazione definisce [!DNL S3] nome del bucket e percorso in cui Platform esporterà i file.
* Un [SFTP](#sftp-example) La specifica del server di destinazione definisce il nome host, la directory principale, la porta di comunicazione e il tipo di crittografia del server SFTP in cui Platform esporta i file.

Per capire dove questo componente si inserisce in un’integrazione creata con Destination SDK, consulta il diagramma riportato di seguito. [opzioni di configurazione](../configuration-options.md) oppure consulta le seguenti pagine di panoramica sulla configurazione di destinazione:

* [Utilizzare Destination SDK per configurare una destinazione di streaming](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

È possibile configurare le specifiche del server di destinazione tramite `/authoring/destination-servers` endpoint. Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md)
* [Aggiornare una configurazione del server di destinazione](../../authoring-api/destination-server/update-destination-server.md)

Questa pagina mostra tutti i tipi di server di destinazione supportati da Destination SDK, con tutti i relativi parametri di configurazione. Quando crei la destinazione, sostituisci i valori dei parametri con i tuoi.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione maiuscole/minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |

Quando [creazione](../../authoring-api/destination-server/create-destination-server.md) o [aggiornamento](../../authoring-api/destination-server/update-destination-server.md) un server di destinazione, utilizza una delle configurazioni del tipo di server descritte in questa pagina. A seconda dei requisiti di integrazione, assicurati di sostituire i valori dei parametri di esempio di questi esempi con i tuoi.

## Campi hardcoded e template {#templatized-fields}

Durante la creazione di un server di destinazione tramite Destination SDK, è possibile definire i valori dei parametri di configurazione codificandoli nella configurazione o utilizzando campi modello. I campi con modello consentono di leggere i valori forniti dall’utente dall’interfaccia utente di Platform.

I parametri del server di destinazione hanno due campi configurabili. Queste opzioni determinano se si utilizzano valori hardcoded o template.

| Parametro | Tipo | Descrizione |
|---|---|---|
| `templatingStrategy` | Stringa | *Obbligatorio.* Definisce se è presente un valore hardcoded fornito tramite il `value` o un valore configurabile dall’utente nell’interfaccia utente. Valori supportati: <ul><li>`NONE`: utilizza questo valore quando esegui la codifica fissa del valore del parametro tramite `value` (vedere la riga successiva). Esempio:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: utilizza questo valore quando desideri che gli utenti forniscano un valore per il parametro nell’interfaccia utente. Esempio: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | Stringa | *Obbligatorio*. Definisce il valore del parametro. Tipi di valore supportati: <ul><li>**Valore hardcoded**: utilizza un valore hardcoded (ad esempio `"value": "my-storage-bucket"`) quando non è necessario che gli utenti immettano un valore di parametro nell&#39;interfaccia utente. Quando si codifica un valore, `templatingStrategy` deve essere sempre impostato su `NONE`.</li><li>**Valore modellato**: utilizza un valore modellato (ad esempio `"value": "{{customerData.bucket}}"`) quando desideri che gli utenti forniscano un valore di parametro nell&#39;interfaccia utente. Quando si utilizzano i valori con modelli, `templatingStrategy` deve essere sempre impostato su `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### Quando utilizzare campi hardcoded e campi con modelli

Sia i campi hardcoded che i campi template hanno un proprio uso nella Destination SDK, a seconda del tipo di integrazione che si sta creando.

**Connessione alla destinazione senza input dell&#39;utente**

Quando gli utenti [connettersi alla destinazione](../../../ui/connect-destination.md) nell’interfaccia utente di Platform, potrebbe essere utile gestire il processo di connessione della destinazione senza il relativo input.

A questo scopo, puoi codificare i parametri di connessione della piattaforma di destinazione nelle specifiche del server. Quando si utilizzano valori di parametri hardcoded nella configurazione del server di destinazione, la connessione tra Adobe Experience Platform e la piattaforma di destinazione viene gestita senza alcun input da parte dell’utente.

Nell’esempio seguente, un partner crea un server di destinazione Data Landing Zone con il `path.value` campo in codifica fissa.

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

Di conseguenza, quando gli utenti passano attraverso [tutorial sulla connessione di destinazione](../../../ui/connect-destination.md), non visualizzeranno un [passaggio di autenticazione](../../../ui/connect-destination.md#authenticate). L’autenticazione viene invece gestita da Platform, come illustrato nell’immagine seguente.

![Immagine dell’interfaccia utente che mostra la schermata di autenticazione tra Platform e una destinazione DLZ.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Connessione alla destinazione con l&#39;input dell&#39;utente**

Quando la connessione tra Platform e la destinazione deve essere stabilita in base a un input specifico dell’utente nell’interfaccia utente di Platform, ad esempio la selezione di un endpoint API o la fornitura di un valore di campo, puoi utilizzare i campi modello nelle specifiche del server per leggere l’input dell’utente e connettersi alla piattaforma di destinazione.

Nell’esempio seguente, un partner crea un’ [tempo reale (streaming)](#streaming-example) integrazione e `url.value` utilizza il parametro di modello `{{customerData.region}}` per personalizzare parte dell’endpoint API in base all’input dell’utente.

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

Per consentire agli utenti di selezionare un valore dall’interfaccia utente di Platform, l’opzione `region` Il parametro deve essere definito anche nel [configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md) come campo dati cliente, come illustrato di seguito:

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

Di conseguenza, quando gli utenti passano attraverso [tutorial sulla connessione di destinazione](../../../ui/connect-destination.md), devono selezionare un’area geografica prima di connettersi alla piattaforma di destinazione. Quando si connettono alla destinazione, il campo modello `{{customerData.region}}` viene sostituito con il valore selezionato dall’utente nell’interfaccia utente, come illustrato nell’immagine seguente.

![Immagine dell&#39;interfaccia utente che mostra la schermata di connessione di destinazione con un selettore di regione.](../../assets/functionality/destination-server/server-spec-template-region.png)

## Server di destinazione in tempo reale (streaming) {#streaming-example}

Questo tipo di server di destinazione ti consente di esportare dati da Adobe Experience Platform alla destinazione tramite richieste HTTP. La configurazione del server contiene informazioni sul server che riceve i messaggi (il server sul lato dell’utente).

Questo processo distribuisce i dati utente come una serie di messaggi HTTP alla piattaforma di destinazione. I parametri seguenti costituiscono il modello delle specifiche del server HTTP.

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
| `name` | Stringa | *Obbligatorio.* Rappresenta un nome descrittivo del server, visibile solo agli Adobi. Questo nome non è visibile ai partner o ai clienti. Esempio: `Moviestar destination server`. |
| `destinationServerType` | Stringa | *Obbligatorio.* Imposta su `URL_BASED` per le destinazioni di streaming. |
| `templatingStrategy` | Stringa | *Obbligatorio.* <ul><li>Utilizzare `PEBBLE_V1` se utilizzi un campo con modello invece di un valore hardcoded nel `value` campo. Utilizza questa opzione se disponi di un endpoint come: `https://api.moviestar.com/data/{{customerData.region}}/items`, in cui gli utenti devono selezionare l’area dell’endpoint dall’interfaccia utente di Platform. </li><li> Utilizzare `NONE` se non è necessaria alcuna trasformazione modellata sul lato Adobe, ad esempio se si dispone di un endpoint come: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Stringa | *Obbligatorio.* Inserisci l’indirizzo dell’endpoint API a cui l’Experience Platform deve connettersi. |

{style="table-layout:auto"}

## [!DNL Amazon S3] server di destinazione {#s3-example}

Questo server di destinazione ti consente di esportare i file contenenti dati di Adobe Experience Platform nell’archiviazione Amazon S3.

L’esempio seguente mostra un esempio di configurazione del server di destinazione per una destinazione Amazon S3.

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
| `name` | Stringa | Il nome del server di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per esportare i file in una [!DNL Amazon S3] bucket, imposta su `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `bucket.value` campo.<ul><li>Se desideri che gli utenti inseriscano il proprio nome di bucket nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario creare un modello per `value` per leggere un valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se utilizzi un nome di bucket hardcoded per l’integrazione, ad esempio `"bucket.value":"MyBucket"`, quindi imposta questo valore su `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | Stringa | Il nome del [!DNL Amazon S3] bucket da utilizzare per questa destinazione. Può essere un campo con modello che leggerà il valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o un valore hardcoded, come `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `path.value` campo.<ul><li>Se desideri che gli utenti inseriscano il proprio percorso nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario creare un modello per `path.value` per leggere un valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se utilizzi un percorso hardcoded per l’integrazione, ad esempio `"bucket.value":"/path/to/MyBucket"`, quindi imposta questo valore su `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | Stringa | Percorso del [!DNL Amazon S3] bucket da utilizzare per questa destinazione. Può essere un campo con modello che leggerà il valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o un valore hardcoded, come `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] server di destinazione {#sftp-example}

Questo server di destinazione ti consente di esportare i file contenenti dati di Adobe Experience Platform nel [!DNL SFTP] server di archiviazione.

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
| `name` | Stringa | Il nome del server di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per esportare i file in una [!DNL SFTP] destinazione, imposta su `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `rootDirectory.value` campo.<ul><li>Se desideri che gli utenti inseriscano il proprio percorso di directory principale nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario creare un modello per `rootDirectory.value` per leggere un valore fornito dall&#39;utente dal [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se utilizzi un percorso di directory principale hardcoded per l’integrazione, ad esempio `"rootDirectory.value":"Storage/MyDirectory"`, quindi imposta questo valore su `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | Stringa | Percorso della directory che ospiterà i file esportati. Può essere un campo con modello che leggerà il valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o un valore hardcoded, come `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `hostName.value` campo.<ul><li>Se desideri che gli utenti inseriscano il proprio nome host nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario creare un modello per `hostName.value` per leggere un valore fornito dall&#39;utente dal [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se utilizzi un nome host hardcoded per l’integrazione, ad esempio `"hostName.value":"my.hostname.com"`, quindi imposta questo valore su `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | Stringa | Il nome host del server SFTP. Può essere un campo con modello che leggerà il valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o un valore hardcoded, come `"hostName.value":"my.hostname.com"`. |
| `port` | Intero | Porta del file server SFTP. |
| `encryptionMode` | Stringa | Indica se utilizzare la crittografia file. Valori supportati: <ul><li>PGP</li><li>Nessuna</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) server di destinazione {#adls-example}

Questo server di destinazione ti consente di esportare i file contenenti dati di Adobe Experience Platform nel [!DNL Azure Data Lake Storage] account.

L’esempio seguente mostra un esempio di configurazione del server di destinazione per un [!DNL Azure Data Lake Storage] destinazione.

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
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Azure Data Lake Storage] destinazioni, impostalo su `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `path.value` campo.<ul><li>Se desideri che gli utenti immettano il [!DNL ADLS] nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario creare un modello per `path.value` per leggere un valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se utilizzi un percorso hardcoded per l’integrazione, ad esempio `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`, quindi imposta questo valore su `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | Stringa | Il percorso del [!DNL ADLS] cartella di archiviazione. Può essere un campo con modello che leggerà il valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o un valore hardcoded, come `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] server di destinazione {#blob-example}

Questo server di destinazione ti consente di esportare i file contenenti dati di Adobe Experience Platform nel [!DNL Azure Blob Storage] contenitore.

L’esempio seguente mostra un esempio di configurazione del server di destinazione per un [!DNL Azure Blob Storage] destinazione.

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
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Azure Blob Storage] destinazioni, impostalo su `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `path.value` campo.<ul><li>Se desideri che gli utenti inseriscano i propri [!DNL Azure Blob] [URI dell&#39;account di archiviazione](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario creare un modello per `path.value` campo da cui leggere il valore [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se utilizzi un percorso hardcoded per l’integrazione, ad esempio `"path.value": "https://myaccount.blob.core.windows.net/"`, quindi imposta questo valore su `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | Stringa | Il percorso del [!DNL Azure Blob] archiviazione. Può essere un campo con modello che leggerà il valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o un valore hardcoded, come `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `container.value` campo.<ul><li>Se desideri che gli utenti inseriscano i propri [!DNL Azure Blob] [nome contenitore](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario creare un modello per `container.value` campo da cui leggere il valore [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se per l’integrazione utilizzi un nome di contenitore hardcoded, ad esempio `"path.value: myContainer"`, quindi imposta questo valore su `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | Stringa | Nome del contenitore di archiviazione BLOB di Azure da utilizzare per questa destinazione. Può essere un campo con modello che leggerà il valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o un valore hardcoded, come `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) server di destinazione {#dlz-example}

Questo server di destinazione ti consente di esportare i file contenenti i dati di Platform in una [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) archiviazione.

L’esempio seguente mostra un esempio di configurazione del server di destinazione per un [!DNL Data Landing Zone] ([!DNL DLZ]) destinazione.

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
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Data Landing Zone] destinazioni, impostalo su `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `path.value` campo.<ul><li>Se desideri che gli utenti inseriscano i propri [!DNL Data Landing Zone] nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario creare un modello per `path.value` per leggere un valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se utilizzi un percorso hardcoded per l’integrazione, ad esempio `"path.value": "https://myaccount.blob.core.windows.net/"`, quindi imposta questo valore su `NONE`. |
| `fileBasedDlzDestination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] server di destinazione {#gcs-example}

Questo server di destinazione ti consente di esportare i file contenenti i dati di Platform nel [!DNL Google Cloud Storage] account.

L’esempio seguente mostra un esempio di configurazione del server di destinazione per un [!DNL Google Cloud Storage] destinazione.

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
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Google Cloud Storage] destinazioni, impostalo su `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `bucket.value` campo.<ul><li>Se desideri che gli utenti inseriscano i propri [!DNL Google Cloud Storage] nome del bucket nell’interfaccia utente Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario creare un modello per `bucket.value` per leggere un valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se utilizzi un nome di bucket hardcoded per l’integrazione, ad esempio `"bucket.value": "my-bucket"`, quindi imposta questo valore su `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Stringa | Il nome del [!DNL Google Cloud Storage] bucket da utilizzare per questa destinazione. Può essere un campo con modello che leggerà il valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o un valore hardcoded, come `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Stringa | *Obbligatorio*. Imposta questo valore in base al tipo di valore utilizzato nel `path.value` campo.<ul><li>Se desideri che gli utenti inseriscano i propri [!DNL Google Cloud Storage] nell’interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario creare un modello per `path.value` per leggere un valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se utilizzi un percorso hardcoded per l’integrazione, ad esempio `"path.value": "/path/to/my-bucket"`, quindi imposta questo valore su `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | Stringa | Percorso del [!DNL Google Cloud Storage] cartella da utilizzare per questa destinazione. Può essere un campo con modello che leggerà il valore da [campi dati cliente](../destination-configuration/customer-data-fields.md) compilato dall’utente (come mostrato nell’esempio precedente), o un valore hardcoded, come `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, è necessario comprendere meglio cosa è una specifica del server di destinazione e come configurarla.

Per ulteriori informazioni sugli altri componenti del server di destinazione, consulta i seguenti articoli:

* [Specifiche di modello](templating-specs.md)
* [Formato del messaggio](message-format.md)
* [Configurazione formattazione file](file-formatting.md)
