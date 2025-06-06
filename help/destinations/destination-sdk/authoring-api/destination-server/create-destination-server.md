---
description: Questa pagina esemplifica la chiamata API utilizzata per creare un server di destinazione tramite Adobe Experience Platform Destination SDK.
title: Creare una configurazione del server di destinazione
exl-id: 5c6b6cf5-a9d9-4c8a-9fdc-f8a95ab2a971
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 5%

---

# Creare una configurazione del server di destinazione

La creazione di un server di destinazione è il primo passo per la creazione di una destinazione personalizzata con Destination SDK. Il server di destinazione include le opzioni di configurazione per le specifiche [server](../../functionality/destination-server/server-specs.md) e [modelli](../../functionality/destination-server/templating-specs.md), il [formato messaggio](../../functionality/destination-server/message-format.md) e le opzioni [formattazione file](../../functionality/destination-server/file-formatting.md) (per le destinazioni basate su file).

Questa pagina esemplifica la richiesta API e il payload che è possibile utilizzare per creare il proprio server di destinazione utilizzando l&#39;endpoint API `/authoring/destination-servers`.

Per una descrizione dettagliata delle funzionalità che puoi configurare tramite questo endpoint, leggi i seguenti articoli:

* [Specifiche server per le destinazioni create con Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Specifiche di modello per le destinazioni create con Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato del messaggio](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configurazione formattazione file](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API del server di destinazione {#get-started}

Prima di continuare, consulta la [guida introduttiva](../../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Creare una configurazione del server di destinazione {#create}

È possibile creare una nuova configurazione del server di destinazione effettuando una richiesta `POST` all&#39;endpoint `/authoring/destination-servers`.

>[!TIP]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**Formato API**

```http
POST /authoring/destination-servers
```

A seconda del tipo di destinazione creato, è necessario configurare un tipo leggermente diverso di server di destinazione.

### Creare server di destinazione con schema statico {#static-destination-servers}

Vedi nelle schede seguenti esempi di server di destinazione per destinazioni che utilizzano [schemi statici](../../functionality/destination-configuration/schema-configuration.md#attributes-schema).

I payload di esempio seguenti includono tutti i parametri supportati da ciascun tipo di server di destinazione. Non è necessario includere tutti i parametri nella richiesta. Il payload è personalizzabile in base alle tue esigenze.

Seleziona ciascuna scheda di seguito per visualizzare le richieste API corrispondenti.

>[!BEGINTABS]

>[!TAB Tempo reale (streaming)]

**Creare un server di destinazione in tempo reale (streaming)**

Quando configuri un’integrazione basata su API in tempo reale (streaming), devi creare un server di destinazione in tempo reale (streaming) simile a quello mostrato di seguito.

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| Parametro | Tipo | Descrizione |
| -------- | ----------- | ----------- |
| `name` | Stringa | *Obbligatorio.* Rappresenta un nome descrittivo del server, visibile solo ad Adobe. Questo nome non è visibile ai partner o ai clienti. Esempio `Moviestar destination server`. |
| `destinationServerType` | Stringa | *Obbligatorio.* Impostato su `URL_BASED` per le destinazioni in tempo reale (streaming). |
| `urlBasedDestination.url.templatingStrategy` | Stringa | *Obbligatorio.* <ul><li>Utilizza `PEBBLE_V1` se Adobe deve trasformare l&#39;URL nel campo `value` sottostante. Utilizzare questa opzione se si dispone di un endpoint come `https://api.moviestar.com/data/{{customerData.region}}/items`, in cui la parte `region` può differire tra i clienti. In questo caso è inoltre necessario configurare `region` come [campo dati cliente](../../functionality/destination-configuration/customer-data-fields.md) nella [configurazione di destinazione]&#x200B;(../destination-configuration/create-destination-configuration.md. </li><li> Utilizza `NONE` se non è necessaria alcuna trasformazione sul lato Adobe, ad esempio se disponi di un endpoint come: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Stringa | *Obbligatorio.* Inserire l&#39;indirizzo dell&#39;endpoint API a cui Experience Platform deve connettersi. |
| `httpTemplate.httpMethod` | Stringa | *Obbligatorio.* Il metodo che Adobe utilizzerà nelle chiamate al server. Le opzioni sono `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Stringa | *Obbligatorio.* Questa stringa è la versione con escape carattere che trasforma i dati dei clienti Experience Platform nel formato previsto dal servizio. <br> <ul><li> Per informazioni su come scrivere il modello, leggere la sezione [Utilizzo dei modelli](../../functionality/destination-server/message-format.md#using-templating). </li><li> Per ulteriori informazioni sull&#39;escape di caratteri, consulta lo standard JSON [RFC, sezione sette](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Per un esempio di semplice trasformazione, fare riferimento alla trasformazione [Attributi profilo](../../functionality/destination-server/message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | Stringa | *Obbligatorio.* Il tipo di contenuto accettato dal server. Questo valore è molto probabilmente `application/json`. |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione del server di destinazione appena creata.

+++

>[!TAB Amazon S3]

**Creare un server di destinazione Amazon S3**

Quando si configura una destinazione [!DNL Amazon S3] basata su file, è necessario creare un server di destinazione [!DNL Amazon S3] simile a quello mostrato di seguito.

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
        }
    }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Amazon S3], impostarlo su `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Stringa | Nome del bucket [!DNL Amazon S3] che deve essere utilizzato da questa destinazione. |
| `fileBasedS3Destination.path.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |
| `fileConfigurations` | N/D | Per informazioni dettagliate su come configurare queste impostazioni, vedere [configurazione formattazione file](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione del server di destinazione appena creata.

+++

>[!TAB SFTP]

**Crea un server di destinazione [!DNL SFTP]**

Quando si configura una destinazione [!DNL SFTP] basata su file, è necessario creare un server di destinazione [!DNL SFTP] simile a quello mostrato di seguito.

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      }, 
      "port": 22,
      "encryptionMode" : "PGP"
   },
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
        }
    }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL SFTP] destinazioni, impostare su `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `fileBasedSFTPDestination.rootDirectory.value` | Stringa | La directory radice dell&#39;archiviazione di destinazione. |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `fileBasedSFTPDestination.hostName.value` | Stringa | Nome host dell&#39;archiviazione di destinazione. |
| `port` | Intero | Porta del file server SFTP. |
| `encryptionMode` | Stringa | Indica se utilizzare la crittografia file. Valori supportati: <ul><li>PGP</li><li>Nessuna</li></ul> |
| `fileConfigurations` | N/D | Per informazioni dettagliate su come configurare queste impostazioni, vedere [configurazione formattazione file](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione del server di destinazione appena creata.

+++

>[!TAB Archiviazione Azure Data Lake]

**Crea un server di destinazione [!DNL Azure Data Lake Storage]**

Quando si configura una destinazione [!DNL Azure Data Lake Storage] basata su file, è necessario creare un server di destinazione [!DNL Azure Data Lake Storage] simile a quello mostrato di seguito.

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
        }
    }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Azure Data Lake Storage] destinazioni, impostare su `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |
| `fileConfigurations` | N/D | Per informazioni dettagliate su come configurare queste impostazioni, vedere [configurazione formattazione file](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione del server di destinazione appena creata.

+++

>[!TAB Archiviazione BLOB di Azure]

**Crea un server di destinazione [!DNL Azure Blob Storage]**

Quando si configura una destinazione [!DNL Azure Blob Storage] basata su file, è necessario creare un server di destinazione [!DNL Azure Blob Storage] simile a quello mostrato di seguito.

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
        }
    }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Azure Blob Storage] destinazioni, impostare su `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Stringa | Nome del contenitore [!DNL Azure Blob Storage] che deve essere utilizzato da questa destinazione. |
| `fileConfigurations` | N/D | Per informazioni dettagliate su come configurare queste impostazioni, vedere [configurazione formattazione file](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione del server di destinazione appena creata.

+++

>[!TAB Zona di destinazione dati (DLZ)]

**Crea un server di destinazione [!DNL Data Landing Zone (DLZ)]**

Quando si configura una destinazione [!DNL Data Landing Zone (DLZ)] basata su file, è necessario creare un server di destinazione [!DNL Data Landing Zone (DLZ)] simile a quello mostrato di seguito.

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
        }
    }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Data Landing Zone] destinazioni, impostare su `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |
| `fileConfigurations` | N/D | Per informazioni dettagliate su come configurare queste impostazioni, vedere [configurazione formattazione file](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione del server di destinazione appena creata.

+++

>[!TAB Google Cloud Storage]

**Crea un server di destinazione [!DNL Google Cloud Storage]**

Quando si configura una destinazione [!DNL Google Cloud Storage] basata su file, è necessario creare un server di destinazione [!DNL Google Cloud Storage] simile a quello mostrato di seguito.

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
        }
    }
}
```

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | Nome della connessione di destinazione. |
| `destinationServerType` | Stringa | Imposta questo valore in base alla piattaforma di destinazione. Per [!DNL Google Cloud Storage] destinazioni, impostare su `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Stringa | Nome del bucket [!DNL Google Cloud Storage] che deve essere utilizzato da questa destinazione. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Stringa | Percorso della cartella di destinazione che ospiterà i file esportati. |
| `fileConfigurations` | N/D | Per informazioni dettagliate su come configurare queste impostazioni, vedere [configurazione formattazione file](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione del server di destinazione appena creata.

+++

>[!ENDTABS]

### Creare server di destinazione con schema dinamico {#dynamic-schema-servers}

Gli schemi dinamici ti consentono di recuperare dinamicamente gli attributi di destinazione supportati e generare schemi in base alla tua API. Per configurare lo schema, è necessario configurare un server di destinazione per gli schemi dinamici.

Vedi nella scheda seguente un esempio di server di destinazione per le destinazioni che utilizzano [schemi dinamici](../../functionality/destination-configuration/schema-configuration.md#dynamic-schema-configuration).

Il payload di esempio seguente include tutti i parametri necessari per un server di schema dinamico.

>[!BEGINTABS]

>[!TAB Server schema dinamico]

**Creare un server di schema dinamico**

Quando configuri una destinazione che recupera lo schema del profilo dal tuo endpoint API, devi creare un server schema dinamico simile a quello mostrato di seguito. A differenza di uno schema statico, uno schema dinamico non utilizza un array `profileFields`. Gli schemi dinamici utilizzano invece un server di schema dinamico che si connette alla tua API da dove recupera la configurazione dello schema.

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Dynamic Schema Server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://YOUR_API_ENDPOINT/"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET"
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"type\":\"object\",\n    \"title\": \"Contact Schema\",\n    \"properties\": {\n        {% for setDefinition in response.body.items %}\n            \"{{setDefinition.key}}\": {\n                \"title\" : \"{{setDefinition.name.value}}\",\n                \"type\" : \"object\",\n                \"properties\": {\n                    {% for attribute in setDefinition.attributes %}\n                        \"{{attribute.key}}\": {\n                            \"title\" : \"{{attribute.name.value}}\",\n                            \"type\" : \"string\"\n                        }\n                        {% if not loop.last %},{%endif%}\n                    {% endfor %}\n                }\n            }\n            {% if not loop.last %},{%endif%}\n        {% endfor %}\n    }\n}",
         "name":"schema"
      }
   ]
}
```

| Parametro | Tipo | Descrizione |
| -------- | ----------- | ----------- |
| `name` | Stringa | *Obbligatorio.* Rappresenta un nome descrittivo del server dello schema dinamico, visibile solo ad Adobe. |
| `destinationServerType` | Stringa | *Obbligatorio.* Impostato su `URL_BASED` per i server dello schema dinamico. |
| `urlBasedDestination.url.templatingStrategy` | Stringa | *Obbligatorio.* <ul><li>Utilizza `PEBBLE_V1` se Adobe deve trasformare l&#39;URL nel campo `value` sottostante. Utilizzare questa opzione se si dispone di un endpoint come: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Utilizza `NONE` se non è necessaria alcuna trasformazione sul lato Adobe, ad esempio se disponi di un endpoint come: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Stringa | *Obbligatorio.* Inserisci l&#39;indirizzo dell&#39;endpoint API a cui Experience Platform deve connettersi e recupera i campi dello schema da compilare come campi di destinazione nel passaggio di mappatura del flusso di lavoro di attivazione. |
| `httpTemplate.httpMethod` | Stringa | *Obbligatorio.* Il metodo che Adobe utilizzerà nelle chiamate al server. Per i server con schema dinamico, utilizzare `GET`. |
| `responseFields.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `responseFields.value` | Stringa | *Obbligatorio.* Questa stringa è il modello di trasformazione con escape di carattere che trasforma la risposta ricevuta dall&#39;API partner nello schema partner che verrà visualizzato nell&#39;interfaccia utente di Experience Platform. <br> <ul><li> Per informazioni su come scrivere il modello, leggere la sezione [Utilizzo dei modelli](../../functionality/destination-server/message-format.md#using-templating). </li><li> Per ulteriori informazioni sull&#39;escape di caratteri, consulta lo standard JSON [RFC, sezione sette](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Per un esempio di semplice trasformazione, fare riferimento alla trasformazione [Attributi profilo](../../functionality/destination-server/message-format.md#attributes). </li></ul> |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione del server di destinazione appena creata.

+++


>[!ENDTABS]


### Creare server di destinazione dinamici a discesa {#dynamic-dropdown-servers}

Utilizza [elenchi a discesa dinamici](../../functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) per recuperare e popolare in modo dinamico i campi dei dati cliente a discesa, in base alla tua API. Ad esempio, puoi recuperare un elenco di account utente esistenti che desideri utilizzare per una connessione di destinazione.

Prima di poter configurare il campo dati cliente a discesa dinamico, è necessario configurare un server di destinazione per i menu a discesa dinamici.

Vedi nella scheda seguente un esempio di server di destinazione utilizzato per recuperare in modo dinamico da un’API i valori da visualizzare in un selettore a discesa.

Il payload di esempio seguente include tutti i parametri necessari per un server di schema dinamico.

>[!BEGINTABS]

>[!TAB Server a discesa dinamico]

**Creare un server a discesa dinamico**

Quando configuri una destinazione che recupera i valori di un campo dati cliente a discesa dal tuo endpoint API, devi creare un server a discesa dinamico simile a quello mostrato di seguito.

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.users}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

| Parametro | Tipo | Descrizione |
| -------- | ----------- | ----------- |
| `name` | Stringa | *Obbligatorio.* Rappresenta un nome descrittivo del server a discesa dinamico, visibile solo ad Adobe. |
| `destinationServerType` | Stringa | *Obbligatorio.* Impostato su `URL_BASED` per i server a discesa dinamici. |
| `urlBasedDestination.url.templatingStrategy` | Stringa | *Obbligatorio.* <ul><li>Utilizza `PEBBLE_V1` se Adobe deve trasformare l&#39;URL nel campo `value` sottostante. Utilizzare questa opzione se si dispone di un endpoint come: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Utilizza `NONE` se non è necessaria alcuna trasformazione sul lato Adobe, ad esempio se disponi di un endpoint come: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Stringa | *Obbligatorio.* Inserisci l&#39;indirizzo dell&#39;endpoint API a cui Experience Platform deve connettersi e recupera i valori del menu a discesa. |
| `httpTemplate.httpMethod` | Stringa | *Obbligatorio.* Il metodo che Adobe utilizzerà nelle chiamate al server. Per i server a discesa dinamici, utilizzare `GET`. |
| `httpTemplate.headers` | Oggetto | *Facoltativa.l* Includere tutte le intestazioni necessarie per connettersi al server a discesa dinamico. |
| `responseFields.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `responseFields.value` | Stringa | *Obbligatorio.* Questa stringa è il modello di trasformazione con escape di carattere che trasforma la risposta ricevuta dall&#39;API nei valori che verranno visualizzati nell&#39;interfaccia utente di Experience Platform. <br> <ul><li> Per informazioni su come scrivere il modello, leggere la sezione [Utilizzo dei modelli](../../functionality/destination-server/message-format.md#using-templating). </li><li> Per ulteriori informazioni sull&#39;escape di caratteri, consulta lo standard JSON [RFC, sezione sette](https://tools.ietf.org/html/rfc8259#section-7). |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione del server di destinazione appena creata.

+++

>[!ENDTABS]

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Experience Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come creare un nuovo server di destinazione tramite l&#39;endpoint API `/authoring/destination-servers` di Destination SDK.

Per ulteriori informazioni su cosa è possibile fare con questo endpoint, consulta i seguenti articoli:

* [Recuperare una configurazione del server di destinazione](retrieve-destination-server.md)
* [Aggiornare una configurazione del server di destinazione](update-destination-server.md)
* [Eliminare una configurazione del server di destinazione](delete-destination-server.md)

Per capire dove questo endpoint si inserisce nel processo di authoring della destinazione, vedi i seguenti articoli:

* [Utilizzare Destination SDK per configurare una destinazione di streaming](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)
