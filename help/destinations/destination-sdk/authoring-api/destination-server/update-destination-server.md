---
description: Questa pagina esemplifica la chiamata API utilizzata per aggiornare una configurazione del server di destinazione esistente tramite il Adobe Experience Platform Destination SDK.
title: Aggiornare una configurazione del server di destinazione
exl-id: 579d2cc1-5110-4fba-9dcc-ff4b8d259827
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 7%

---

# Aggiornare una configurazione del server di destinazione

Questa pagina esemplifica la richiesta API e il payload che è possibile utilizzare per aggiornare una configurazione del server di destinazione esistente, utilizzando l&#39;endpoint API `/authoring/destination-servers`.

>[!TIP]
>
>Qualsiasi operazione di aggiornamento sulle destinazioni pubbliche/di produzione è visibile solo dopo aver utilizzato l&#39;[API di pubblicazione](../../publishing-api/create-publishing-request.md) e aver inviato l&#39;aggiornamento per una revisione di Adobe.

Per una descrizione dettagliata delle funzionalità che puoi configurare tramite questo endpoint, leggi i seguenti articoli:

* [Specifiche del server per le destinazioni create con Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Specifiche di modello per le destinazioni create con Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato del messaggio](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configurazione formattazione file](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API del server di destinazione {#get-started}

Prima di continuare, consulta la [guida introduttiva](../../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Aggiornare una configurazione del server di destinazione {#update}

È possibile aggiornare una configurazione del server di destinazione [esistente](create-destination-server.md) effettuando una richiesta `PUT` all&#39;endpoint `/authoring/destination-servers` con il payload aggiornato.

>[!TIP]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Per ottenere una configurazione del server di destinazione esistente e i relativi `{INSTANCE_ID}`, vedere l&#39;articolo relativo al [recupero di una configurazione del server di destinazione](retrieve-destination-server.md).

**Formato API**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione del server di destinazione che desideri aggiornare. Per ottenere una configurazione del server di destinazione esistente e i relativi `{INSTANCE_ID}`, vedere [Recuperare una configurazione del server di destinazione](retrieve-destination-server.md). |

Le seguenti richieste aggiornano una configurazione del server di destinazione esistente, configurata dai parametri forniti nel payload.

Seleziona ciascuna scheda di seguito per visualizzare il payload corrispondente.

>[!BEGINTABS]

>[!TAB Tempo reale (streaming)]

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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
      "httpMethod":"PUT",
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
| `name` | Stringa | *Obbligatorio.* Rappresenta un nome descrittivo del server, visibile solo agli Adobi. Questo nome non è visibile ai partner o ai clienti. Esempio `Moviestar destination server`. |
| `destinationServerType` | Stringa | *Obbligatorio.* Impostato su `URL_BASED` per le destinazioni in tempo reale (streaming). |
| `urlBasedDestination.url.templatingStrategy` | Stringa | *Obbligatorio.* <ul><li>Utilizza `PEBBLE_V1` se Adobe deve trasformare l&#39;URL nel campo `value` di seguito. Utilizzare questa opzione se si dispone di un endpoint come: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Utilizzare `NONE` se non è necessaria alcuna trasformazione sul lato Adobe, ad esempio se si dispone di un endpoint come: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Stringa | *Obbligatorio.* Inserire l&#39;indirizzo dell&#39;endpoint API a cui l&#39;Experience Platform deve connettersi. |
| `httpTemplate.httpMethod` | Stringa | *Obbligatorio.* Il metodo che Adobe utilizzerà nelle chiamate al server. Le opzioni sono `GET`, `PUT`, `PUT`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Stringa | *Obbligatorio.* Utilizza `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Stringa | *Obbligatorio.* Questa stringa è la versione con escape carattere che trasforma i dati dei clienti di Platform nel formato previsto dal servizio. <br> <ul><li> Per informazioni su come scrivere il modello, leggere la sezione [Utilizzo dei modelli](../../functionality/destination-server/message-format.md#using-templating). </li><li> Per ulteriori informazioni sull&#39;escape di caratteri, consulta lo standard JSON [RFC, sezione sette](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Per un esempio di semplice trasformazione, fare riferimento alla trasformazione [Attributi profilo](../../functionality/destination-server/message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | Stringa | *Obbligatorio.* Il tipo di contenuto accettato dal server. Questo valore è molto probabilmente `application/json`. |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione aggiornata del server di destinazione.

+++

>[!TAB Amazon S3]

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione aggiornata del server di destinazione.

+++

>[!TAB SFTP]

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione aggiornata del server di destinazione.

+++

>[!TAB Archiviazione Azure Data Lake]

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione aggiornata del server di destinazione.

+++

>[!TAB Archiviazione BLOB di Azure]

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_D} \
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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione aggiornata del server di destinazione.

+++

>[!TAB Zona di destinazione dati (DLZ)]

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione aggiornata del server di destinazione.

+++

>[!TAB Google Cloud Storage]

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione aggiornata del server di destinazione.

+++

>[!ENDTABS]

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come aggiornare la configurazione di un server di destinazione tramite l&#39;endpoint API Destination SDK `/authoring/destination-servers`.

Per ulteriori informazioni su cosa è possibile fare con questo endpoint, consulta i seguenti articoli:

* [Creare una configurazione del server di destinazione](create-destination-server.md)
* [Recuperare una configurazione del server di destinazione](retrieve-destination-server.md)
* [Aggiornare una configurazione del server di destinazione](update-destination-server.md)
