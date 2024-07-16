---
description: Scopri come configurare le specifiche del server di destinazione in Adobe Experience Platform Destination SDK tramite l’endpoint "/authoring/destination-servers".
title: Specifiche del server per le destinazioni create con Destination SDK
exl-id: 62202edb-a954-42ff-9772-863cea37a889
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2739'
ht-degree: 2%

---

# Specifiche del server per le destinazioni create con Destination SDK

Le specifiche del server di destinazione definiscono il tipo di piattaforma di destinazione che riceverà i dati da Adobe Experience Platform e i parametri di comunicazione tra Platform e la destinazione. Ad esempio:

* Una specifica del server di destinazione [streaming](#streaming-example) definisce l&#39;endpoint del server HTTP che riceverà i messaggi HTTP da Platform. Per informazioni su come configurare la formattazione delle chiamate HTTP all&#39;endpoint, leggere la pagina delle specifiche dei [modelli](templating-specs.md).
* Una specifica del server di destinazione [Amazon S3](#s3-example) definisce il nome e il percorso del bucket [!DNL S3] in cui Platform esporterà i file.
* Una specifica del server di destinazione [SFTP](#sftp-example) definisce il nome host, la directory radice, la porta di comunicazione e il tipo di crittografia del server SFTP in cui Platform esporterà i file.

Per capire dove questo componente si inserisce in un&#39;integrazione creata con Destination SDK, consulta il diagramma nella documentazione delle [opzioni di configurazione](../configuration-options.md) oppure vedi le seguenti pagine di panoramica sulla configurazione di destinazione:

* [Utilizzare Destination SDK per configurare una destinazione di streaming](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

È possibile configurare le specifiche del server di destinazione tramite l&#39;endpoint `/authoring/destination-servers`. Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md)
* [Aggiornare una configurazione del server di destinazione](../../authoring-api/destination-server/update-destination-server.md)

Questa pagina mostra tutti i tipi di server di destinazione supportati da Destination SDK, con tutti i relativi parametri di configurazione. Quando crei la destinazione, sostituisci i valori dei parametri con i tuoi.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |

Quando [crea](../../authoring-api/destination-server/create-destination-server.md) o [aggiorna](../../authoring-api/destination-server/update-destination-server.md) un server di destinazione, utilizza una delle configurazioni del tipo di server descritte in questa pagina. A seconda dei requisiti di integrazione, assicurati di sostituire i valori dei parametri di esempio di questi esempi con i tuoi.

## Campi hardcoded e template {#templatized-fields}

Durante la creazione di un server di destinazione tramite Destination SDK, è possibile definire i valori dei parametri di configurazione codificandoli nella configurazione o utilizzando campi modello. I campi con modello consentono di leggere i valori forniti dall’utente dall’interfaccia utente di Platform.

I parametri del server di destinazione hanno due campi configurabili. Queste opzioni determinano se si utilizzano valori hardcoded o template.

| Parametro | Tipo | Descrizione |
|---|---|---|
| `templatingStrategy` | Stringa | *Obbligatorio.* Definisce se è presente un valore hardcoded fornito tramite il campo `value` o un valore configurabile dall&#39;utente nell&#39;interfaccia utente. Valori supportati: <ul><li>`NONE`: utilizzare questo valore quando si codifica il valore del parametro tramite il parametro `value` (vedere la riga successiva). Esempio:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: utilizzare questo valore quando si desidera che gli utenti forniscano un valore di parametro nell&#39;interfaccia utente. Esempio: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | Stringa | *Richiesto*. Definisce il valore del parametro. Tipi di valore supportati: <ul><li>**Valore hardcoded**: utilizza un valore hard coded (ad esempio `"value": "my-storage-bucket"`) quando non è necessario che gli utenti immettano un valore di parametro nell&#39;interfaccia utente. Quando si codifica un valore a livello di codice, `templatingStrategy` deve essere sempre impostato su `NONE`.</li><li>**Valore con modello**: utilizzare un valore con modello (ad esempio `"value": "{{customerData.bucket}}"`) quando si desidera che gli utenti forniscano un valore di parametro nell&#39;interfaccia utente. Quando si utilizzano valori con modelli, `templatingStrategy` deve essere sempre impostato su `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### Quando utilizzare campi hardcoded e campi con modelli

Sia i campi hardcoded che i campi template hanno un proprio uso nella Destination SDK, a seconda del tipo di integrazione che si sta creando.

**Connessione alla destinazione senza l&#39;input dell&#39;utente**

Quando gli utenti [si connettono alla destinazione](../../../ui/connect-destination.md) nell&#39;interfaccia utente di Platform, è possibile gestire il processo di connessione di destinazione senza l&#39;input degli utenti.

A questo scopo, puoi codificare i parametri di connessione della piattaforma di destinazione nelle specifiche del server. Quando si utilizzano valori di parametri hardcoded nella configurazione del server di destinazione, la connessione tra Adobe Experience Platform e la piattaforma di destinazione viene gestita senza alcun input da parte dell’utente.

Nell&#39;esempio seguente, un partner crea un server di destinazione Data Landing Zone con il campo `path.value` codificato.

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

Di conseguenza, quando gli utenti seguono l&#39;[esercitazione sulla connessione di destinazione](../../../ui/connect-destination.md), non visualizzeranno un [passaggio di autenticazione](../../../ui/connect-destination.md#authenticate). L’autenticazione viene invece gestita da Platform, come illustrato nell’immagine seguente.

![Immagine dell&#39;interfaccia utente che mostra la schermata di autenticazione tra Platform e una destinazione DLZ.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Connessione alla destinazione con l&#39;input dell&#39;utente**

Quando la connessione tra Platform e la destinazione deve essere stabilita in base a un input specifico dell’utente nell’interfaccia utente di Platform, ad esempio la selezione di un endpoint API o la fornitura di un valore di campo, puoi utilizzare i campi modello nelle specifiche del server per leggere l’input dell’utente e connettersi alla piattaforma di destinazione.

Nell&#39;esempio seguente, un partner crea un&#39;integrazione [in tempo reale (streaming)](#streaming-example) e il campo `url.value` utilizza il parametro `{{customerData.region}}` modello per personalizzare parte dell&#39;endpoint API in base all&#39;input dell&#39;utente.

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

Per consentire agli utenti di selezionare un valore dall&#39;interfaccia utente di Platform, il parametro `region` deve essere definito anche nella [configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md) come campo dati cliente, come illustrato di seguito:

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

Di conseguenza, quando gli utenti seguono l&#39;[esercitazione sulla connessione di destinazione](../../../ui/connect-destination.md), devono selezionare un&#39;area geografica prima di connettersi alla piattaforma di destinazione. Quando si connettono alla destinazione, il campo con modello `{{customerData.region}}` viene sostituito con il valore selezionato dall&#39;utente nell&#39;interfaccia utente, come illustrato nell&#39;immagine seguente.

![Immagine dell&#39;interfaccia utente che mostra la schermata di connessione di destinazione con un selettore di area.](../../assets/functionality/destination-server/server-spec-template-region.png)

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
| `destinationServerType` | Stringa | *Obbligatorio.* Imposta questo su `URL_BASED` per le destinazioni di streaming. |
| `templatingStrategy` | Stringa | *Obbligatorio.* <ul><li>Usa `PEBBLE_V1` se nel campo `value` utilizzi un campo con modello invece di un valore hardcoded. Utilizzare questa opzione se si dispone di un endpoint come `https://api.moviestar.com/data/{{customerData.region}}/items`, in cui gli utenti devono selezionare l&#39;area dell&#39;endpoint dall&#39;interfaccia utente di Platform. </li><li> Utilizzare `NONE` se non è necessaria alcuna trasformazione modellata sul lato Adobe, ad esempio se si dispone di un endpoint come: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Stringa | *Obbligatorio.* Inserire l&#39;indirizzo dell&#39;endpoint API a cui l&#39;Experience Platform deve connettersi. |

{style="table-layout:auto"}

## Server di destinazione [!DNL Amazon S3] {#s3-example}

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
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per esportare i file in un bucket [!DNL Amazon S3], impostarlo su `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Stringa | *Richiesto*. Impostare questo valore in base al tipo di valore utilizzato nel campo `bucket.value`.<ul><li>Se desideri che gli utenti inseriscano il proprio nome di bucket nell&#39;interfaccia utente Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario formattare il campo `value` per leggere un valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se per l&#39;integrazione utilizzi un nome di bucket hardcoded, ad esempio `"bucket.value":"MyBucket"`, imposta questo valore su `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | Stringa | Nome del bucket [!DNL Amazon S3] che deve essere utilizzato da questa destinazione. Può trattarsi di un campo modello che leggerà il valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente (come mostrato nell&#39;esempio precedente) o di un valore hardcoded, ad esempio `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | Stringa | *Richiesto*. Impostare questo valore in base al tipo di valore utilizzato nel campo `path.value`.<ul><li>Se desideri che gli utenti inseriscano il proprio percorso nell&#39;interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario formattare il campo `path.value` per leggere un valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se per l&#39;integrazione si utilizza un percorso hardcoded, ad esempio `"bucket.value":"/path/to/MyBucket"`, impostare questo valore su `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | Stringa | Percorso del bucket [!DNL Amazon S3] da utilizzare per questa destinazione. Può trattarsi di un campo modello che leggerà il valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente (come mostrato nell&#39;esempio precedente) o di un valore hardcoded, ad esempio `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## Server di destinazione [!DNL SFTP] {#sftp-example}

Questo server di destinazione consente di esportare file contenenti dati Adobe Experience Platform nel server di archiviazione [!DNL SFTP].

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
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per esportare i file in una destinazione [!DNL SFTP], impostarla su `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Stringa | *Richiesto*. Impostare questo valore in base al tipo di valore utilizzato nel campo `rootDirectory.value`.<ul><li>Se si desidera che gli utenti inseriscano il proprio percorso di directory principale nell&#39;interfaccia utente di Experience Platform, impostare questo valore su `PEBBLE_V1`. In questo caso, è necessario formattare il campo `rootDirectory.value` per leggere un valore fornito dall&#39;utente dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se per l&#39;integrazione si utilizza un percorso di directory principale hardcoded, ad esempio `"rootDirectory.value":"Storage/MyDirectory"`, impostare questo valore su `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | Stringa | Percorso della directory che ospiterà i file esportati. Può trattarsi di un campo modello che leggerà il valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente (come mostrato nell&#39;esempio precedente) o di un valore hardcoded, ad esempio `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Stringa | *Richiesto*. Impostare questo valore in base al tipo di valore utilizzato nel campo `hostName.value`.<ul><li>Se desideri che gli utenti inseriscano il proprio nome host nell&#39;interfaccia utente Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario formattare il campo `hostName.value` per leggere un valore fornito dall&#39;utente dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se per l&#39;integrazione si utilizza un nome host hardcoded, ad esempio `"hostName.value":"my.hostname.com"`, impostare questo valore su `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | Stringa | Il nome host del server SFTP. Può trattarsi di un campo modello che leggerà il valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente (come mostrato nell&#39;esempio precedente) o di un valore hardcoded, ad esempio `"hostName.value":"my.hostname.com"`. |
| `port` | Intero | Porta del file server SFTP. |
| `encryptionMode` | Stringa | Indica se utilizzare la crittografia file. Valori supportati: <ul><li>PGP</li><li>Nessuna</li></ul> |

{style="table-layout:auto"}

## Server di destinazione [!DNL Azure Data Lake Storage] ([!DNL ADLS]) {#adls-example}

Questo server di destinazione ti consente di esportare i file contenenti dati di Adobe Experience Platform nel tuo account [!DNL Azure Data Lake Storage].

Nell&#39;esempio seguente viene illustrato un esempio di configurazione del server di destinazione per una destinazione [!DNL Azure Data Lake Storage].

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
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Azure Data Lake Storage] destinazioni, impostare su `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Stringa | *Richiesto*. Impostare questo valore in base al tipo di valore utilizzato nel campo `path.value`.<ul><li>Se desideri che gli utenti inseriscano il percorso della cartella [!DNL ADLS] nell&#39;interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario formattare il campo `path.value` per leggere un valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se per l&#39;integrazione si utilizza un percorso hardcoded, ad esempio `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`, impostare questo valore su `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | Stringa | Percorso della cartella di archiviazione [!DNL ADLS]. Può trattarsi di un campo modello che leggerà il valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente (come mostrato nell&#39;esempio precedente) o di un valore hardcoded, ad esempio `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## Server di destinazione [!DNL Azure Blob Storage] {#blob-example}

Questo server di destinazione consente di esportare i file contenenti dati di Adobe Experience Platform nel contenitore [!DNL Azure Blob Storage].

Nell&#39;esempio seguente viene illustrato un esempio di configurazione del server di destinazione per una destinazione [!DNL Azure Blob Storage].

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
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Azure Blob Storage] destinazioni, impostare su `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Stringa | *Richiesto*. Impostare questo valore in base al tipo di valore utilizzato nel campo `path.value`.<ul><li>Se si desidera che gli utenti immettano il proprio [!DNL Azure Blob] [URI dell&#39;account di archiviazione](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) nell&#39;interfaccia utente di Experience Platform, impostare questo valore su `PEBBLE_V1`. In questo caso, è necessario formattare il campo `path.value` per leggere il valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se per l&#39;integrazione si utilizza un percorso hardcoded, ad esempio `"path.value": "https://myaccount.blob.core.windows.net/"`, impostare questo valore su `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | Stringa | Percorso dell&#39;archivio [!DNL Azure Blob]. Può trattarsi di un campo modello che leggerà il valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente (come mostrato nell&#39;esempio precedente) o di un valore hardcoded, ad esempio `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Stringa | *Richiesto*. Impostare questo valore in base al tipo di valore utilizzato nel campo `container.value`.<ul><li>Se desideri che gli utenti inseriscano il proprio [!DNL Azure Blob] [nome contenitore](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) nell&#39;interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario formattare il campo `container.value` per leggere il valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se per l&#39;integrazione si utilizza un nome di contenitore hardcoded, ad esempio `"path.value: myContainer"`, impostare questo valore su `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | Stringa | Nome del contenitore di archiviazione BLOB di Azure da utilizzare per questa destinazione. Può trattarsi di un campo modello che leggerà il valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente (come mostrato nell&#39;esempio precedente) o di un valore hardcoded, ad esempio `myContainer`. |

{style="table-layout:auto"}

## Server di destinazione [!DNL Data Landing Zone] ([!DNL DLZ]) {#dlz-example}

Questo server di destinazione consente di esportare i file contenenti i dati di Platform in un archivio [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md).

Nell&#39;esempio seguente viene illustrato un esempio di configurazione del server di destinazione per una destinazione [!DNL Data Landing Zone] ([!DNL DLZ]).

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
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Data Landing Zone] destinazioni, impostare su `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Stringa | *Richiesto*. Impostare questo valore in base al tipo di valore utilizzato nel campo `path.value`.<ul><li>Se desideri che gli utenti inseriscano il proprio account [!DNL Data Landing Zone] nell&#39;interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario formattare il campo `path.value` per leggere un valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se per l&#39;integrazione si utilizza un percorso hardcoded, ad esempio `"path.value": "https://myaccount.blob.core.windows.net/"`, impostare questo valore su `NONE`. |
| `fileBasedDlzDestination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |

{style="table-layout:auto"}

## Server di destinazione [!DNL Google Cloud Storage] {#gcs-example}

Questo server di destinazione ti consente di esportare i file contenenti i dati di Platform nel tuo account [!DNL Google Cloud Storage].

Nell&#39;esempio seguente viene illustrato un esempio di configurazione del server di destinazione per una destinazione [!DNL Google Cloud Storage].

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
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Google Cloud Storage] destinazioni, impostare su `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Stringa | *Richiesto*. Impostare questo valore in base al tipo di valore utilizzato nel campo `bucket.value`.<ul><li>Se desideri che gli utenti inseriscano il proprio nome di bucket [!DNL Google Cloud Storage] nell&#39;interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario formattare il campo `bucket.value` per leggere un valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se per l&#39;integrazione utilizzi un nome di bucket hardcoded, ad esempio `"bucket.value": "my-bucket"`, imposta questo valore su `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Stringa | Nome del bucket [!DNL Google Cloud Storage] che deve essere utilizzato da questa destinazione. Può trattarsi di un campo modello che leggerà il valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente (come mostrato nell&#39;esempio precedente) o di un valore hardcoded, ad esempio `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Stringa | *Richiesto*. Impostare questo valore in base al tipo di valore utilizzato nel campo `path.value`.<ul><li>Se desideri che gli utenti inseriscano il proprio percorso del bucket [!DNL Google Cloud Storage] nell&#39;interfaccia utente di Experience Platform, imposta questo valore su `PEBBLE_V1`. In questo caso, è necessario formattare il campo `path.value` per leggere un valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente. Questo caso d’uso è illustrato nell’esempio precedente.</li><li>Se per l&#39;integrazione si utilizza un percorso hardcoded, ad esempio `"path.value": "/path/to/my-bucket"`, impostare questo valore su `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | Stringa | Percorso della cartella [!DNL Google Cloud Storage] da utilizzare per questa destinazione. Può trattarsi di un campo modello che leggerà il valore dai [campi dati cliente](../destination-configuration/customer-data-fields.md) compilati dall&#39;utente (come mostrato nell&#39;esempio precedente) o di un valore hardcoded, ad esempio `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, è necessario comprendere meglio cosa è una specifica del server di destinazione e come configurarla.

Per ulteriori informazioni sugli altri componenti del server di destinazione, consulta i seguenti articoli:

* [Specifiche di modello](templating-specs.md)
* [Formato del messaggio](message-format.md)
* [Configurazione formattazione file](file-formatting.md)
