---
description: Configurare le opzioni di formattazione dei file per le destinazioni basate su file
title: Scopri come utilizzare Destination SDK per configurare le opzioni di formattazione per le destinazioni basate su file.
exl-id: e61c7989-1123-4b3b-9781-a6097cd0e2b4
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 1%

---

# Configurare le opzioni di formattazione dei file per le destinazioni basate su file

## Panoramica {#overview}

Destination SDK consente di regolare in modo approfondito le opzioni di formattazione e compressione dei file esportati, in base ai requisiti downstream della posizione di archiviazione.

Questa pagina descrive come utilizzare Destination SDK per configurare le opzioni di formattazione dei file per le destinazioni basate su file.

## Prerequisiti {#prerequisites}

Prima di procedere con i passaggi descritti di seguito, leggere la pagina della [guida introduttiva](../../getting-started.md) di Destination SDK per informazioni su come ottenere le credenziali di autenticazione Adobe I/O necessarie e altri prerequisiti per l&#39;utilizzo delle API Destination SDK.

L’Adobe consiglia inoltre di leggere e acquisire familiarità con la seguente documentazione prima di procedere:

* Ogni opzione di formattazione file disponibile è documentata nella sezione [configurazione di formattazione file](../../functionality/destination-server/file-formatting.md).
* Completare i passaggi per [configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md) utilizzando Destination SDK.

## Creare una configurazione di server e file {#create-server-file-configuration}

Iniziare utilizzando l&#39;endpoint `/destination-server` per determinare quali opzioni di configurazione di formattazione dei file si desidera impostare per i file esportati.

Di seguito è riportato un esempio di configurazione del server di destinazione per una destinazione [!DNL Amazon S3], con diverse opzioni di formattazione del file selezionate.

**Formato API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
{
  "name": "Amazon S3 Server with several CSV Options",
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
}
}'
```

## Aggiungi le opzioni di formattazione del file alla configurazione di destinazione {#create-destination-configuration}

>[!TIP]
>
>**Verificare l&#39;interfaccia utente di Experience Platform**. Quando configuri le opzioni di formattazione del file con le configurazioni illustrate nelle sezioni seguenti, controlla nell’interfaccia utente di Experience Platform come vengono visualizzate queste opzioni.

Dopo aver aggiunto le opzioni di formattazione del file desiderate al server di destinazione e la configurazione di formattazione del file nel passaggio precedente, ora puoi utilizzare l&#39;endpoint API `/destinations` per aggiungere i campi desiderati come campi dati del cliente alla configurazione di destinazione.

>[!IMPORTANT]
>
>Questo passaggio è facoltativo e determina solo le opzioni di formattazione del file da rendere visibili agli utenti nell’interfaccia utente di Experience Platform. Se non si impostano le opzioni di formattazione dei file come campi dati del cliente, l&#39;esportazione dei file proseguirà con i valori predefiniti configurati nel [server e nella configurazione dei file](#create-server-file-configuration).

In questo passaggio è possibile raggruppare le opzioni visualizzate in qualsiasi ordine desiderato, nonché creare raggruppamenti personalizzati, campi a discesa e raggruppamenti condizionali in base ai tipi di file selezionati. Tutte queste impostazioni sono mostrate nella registrazione e nelle sezioni seguenti.

![Registrazione dello schermo con varie opzioni di formattazione per i file batch.](../../assets/guides/batch/file-formatting-options.gif)

### Ordinare le opzioni di formattazione del file {#ordering}

L’ordine in cui aggiungi le opzioni di formattazione del file come campi dati del cliente nella configurazione di destinazione si riflette nell’interfaccia utente. Ad esempio, la configurazione seguente viene riflessa di conseguenza nell&#39;interfaccia utente, con le opzioni visualizzate nell&#39;ordine **[!UICONTROL Delimiter]**, **[!UICONTROL Quote Character]**, **[!UICONTROL Escape Character]**, **[!UICONTROL Empty Value]**, **[!UICONTROL Null Value]**.

![Immagine che mostra l&#39;ordine delle opzioni di formattazione dei file nell&#39;interfaccia utente di Experience Platform.](../../assets/guides/batch/file-formatting-order.png)

```json
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\u0000",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": ""
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
```

### Raggruppa le opzioni di formattazione del file {#grouping}

È possibile raggruppare diverse opzioni di formattazione dei file all&#39;interno di una sezione. Quando si imposta la connessione alla destinazione nell’interfaccia utente di, l’utente può visualizzare e beneficiare di un raggruppamento visivo di campi simili.

A tale scopo, utilizzare `"type": "object"` per creare il gruppo e raccogliere le opzioni di formattazione del file desiderate all&#39;interno di un parametro `properties`, come illustrato nell&#39;esempio seguente, dove il raggruppamento **[!UICONTROL Opzioni CSV]** è evidenziato.

```json {line-numbers="true" start-number="100" highlight="106-128"}
"customerDataFields":[
[...]
{
   "name":"csvOptions",
   "title":"CSV Options",
   "description":"Select your CSV options",
   "type":"object",
   "properties":[
      {
         "name":"delimiter",
         "title":"Delimiter",
         "description":"Select your Delimiter",
         "type":"string",
         "isRequired":false,
         "default":",",
         "namedEnum":[
            {
               "name":"Comma (,)",
               "value":","
            },
            {
               "name":"Tab (\\t)",
               "value":"\t"
            }
         ],
         "readOnly":false,
         "hidden":false
      },
      [...]
   ]
}
[...]
]
```

![Immagine che mostra il raggruppamento di opzioni CSV nell&#39;interfaccia utente.](../../assets/guides/batch/file-formatting-grouping.png)

### Creare selettori a discesa per le opzioni di formattazione del file {#dropdown-selectors}

Nelle situazioni in cui desideri consentire agli utenti di selezionare tra diverse opzioni, ad esempio il carattere da utilizzare per delimitare i campi nei file CSV, puoi aggiungere campi a discesa all’interfaccia utente.

A tale scopo, utilizzare l&#39;oggetto `namedEnum` come illustrato di seguito e configurare un valore `default` per le opzioni selezionabili dall&#39;utente.

```json {line-numbers="true" start-number="100" highlight="114-124"}
[...]
"customerDataFields":[
[...]
{
   "name":"csvOptions",
   "title":"CSV Options",
   "description":"Select your CSV options",
   "type":"object",
   "properties":[
      {
         "name":"delimiter",
         "title":"Delimiter",
         "description":"Select your Delimiter",
         "type":"string",
         "isRequired":false,
         "default":",",
         "namedEnum":[
            {
               "name":"Comma (,)",
               "value":","
            },
            {
               "name":"Tab (\\t)",
               "value":"\t"
            }
         ],
         "readOnly":false,
         "hidden":false
      },
      [...]
   ]
}
[...]
]
```

![Registrazione schermata che mostra un esempio di selettori a discesa creati con la configurazione mostrata sopra.](../../assets/guides/batch/dropdown-options-file-formatting.gif)

### Creare opzioni di formattazione condizionale dei file {#conditional-options}

È possibile creare opzioni di formattazione condizionale per i file, visualizzate nel flusso di lavoro di attivazione solo quando l&#39;utente seleziona un determinato tipo di file per l&#39;esportazione. Ad esempio, la configurazione seguente crea un raggruppamento condizionale per le opzioni del file CSV. Le opzioni del file CSV vengono visualizzate solo quando l’utente seleziona CSV come tipo di file desiderato per l’esportazione.

Per impostare un campo come condizionale, utilizzare il parametro `conditional` come illustrato di seguito:

```json
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            }
```

In un contesto più ampio, è possibile visualizzare il campo `conditional` utilizzato nella configurazione di destinazione seguente, insieme alla stringa `fileType` e all&#39;oggetto `csvOptions` in cui è definito.

```json
        {
            "name": "fileType",
            "title": "File Type",
            "description": "Select your file type",
            "type": "string",
            "isRequired": true,
            "enum": [
                "PARQUET",
                "CSV",
                "JSON"
            ],
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            },            
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": "\u0000"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
            ],
            "isRequired": false,
            "readOnly": false,
            "hidden": false
        }
```

Di seguito è riportata la schermata risultante dell’interfaccia utente, in base alla configurazione precedente. Quando l’utente seleziona il tipo di file CSV, nell’interfaccia utente vengono visualizzate ulteriori opzioni di formattazione relative al tipo di file CSV.

![Registrazione dello schermo che mostra l&#39;opzione di formattazione del file condizionale per i file CSV.](../../assets/guides/batch/conditional-file-formatting.gif)

### Richiesta API completa che include tutte le opzioni mostrate sopra

La richiesta API seguente combina in un’unica configurazione tutte le opzioni descritte nelle sezioni precedenti.

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
  "name": "My S3 Destination",
  "description": "Test destination",
  "status": "TEST",
  "sources": [
    "UNIFIED_PROFILE"
  ],
  "customerAuthenticationConfigurations": [
    {
      "authType": "S3"
    }
  ],
  "customerDataFields": [
    {
      "name": "bucket",
      "type": "string",
      "title": "Bucket",
      "description": "Enter your S3 Bucket",
      "isRequired": true
    },
    {
      "name": "path",
      "type": "string",
      "title": "Path",
      "description": "Enter your S3 Path",
      "isRequired": true
    },
    {
      "name": "fileType",
      "type": "string",
      "enum": [
        "CSV",
        "JSON",
        "PARQUET"
      ],
      "title": "File Type",
      "description": "Select your file type",
      "isRequired": true
    },
    {
      "name": "csvOptions",
      "type": "object",
      "title": "CSV Options",
      "description": "Select your CSV options",
      "conditional": {
        "field": "fileType",
        "operator": "EQUALS",
        "value": "CSV"
      },
      "properties": [
        {
          "name": "delimiter",
          "type": "string",
          "title": "Delimiter",
          "description": "Select your Delimiter",
          "namedEnum": [
            {
              "name": "Comma (,)",
              "value": ","
            },
            {
              "name": "Tab (\\t)",
              "value": "\t"
            }
          ],
          "default": ","
        },
        {
          "name": "quote",
          "type": "string",
          "title": "Quote Character",
          "description": "Select your Quote character",
          "namedEnum": [
            {
              "name": "Double Quotes (\")",
              "value": "\""
            },
            {
              "name": "Null Character (\\u0000)",
              "value": "\u0000"
            }
          ],
          "default": "\u0000"
        },
        {
          "name": "escape",
          "type": "string",
          "title": "Escape Character",
          "description": "Select your Escape character",
          "namedEnum": [
            {
              "name": "Back Slash (\\)",
              "value": "\\"
            },
            {
              "name": "Single Quote (')",
              "value": "'"
            }
          ],
          "default": "\\"
        },
        {
          "name": "emptyValue",
          "type": "string",
          "title": "Empty Value",
          "description": "Select the output value of blank fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": ""
        },
        {
          "name": "nullValue",
          "type": "string",
          "title": "Null Value",
          "description": "Select the output value of 'null' fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": "null"
        }
      ]
    }
  ],
  "uiAttributes": {
    "documentationLink": "https://www.adobe.com/go/aep",
    "category": "cloudStorage",
    "connectionType": "Server-to-server",
    "frequency": "Batch",
    "monitoringSupported": true,
    "flowRunsSupported": true
  },
  "schemaConfig": {
    "profileRequired": true,
    "segmentRequired": true,
    "identityRequired": true
  },
  "batchConfig": {
    "allowMandatoryFieldSelection": true,
    "allowDedupeKeyFieldSelection": true,
    "defaultExportMode": "DAILY_FULL_EXPORT",
    "allowedExportMode": [
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
    ],
    "allowedScheduleFrequency": [
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
    ],
    "defaultFrequency": "DAILY",
    "defaultStartTime": "00:00",
    "filenameConfig": {
      "allowedFilenameAppendOptions": [
        "SEGMENT_NAME",
        "DESTINATION_INSTANCE_ID",
        "DESTINATION_INSTANCE_NAME",
        "ORGANIZATION_NAME",
        "SANDBOX_NAME",
        "DATETIME",
        "CUSTOM_TEXT"
      ],
      "defaultFilenameAppendOptions": [
        "DATETIME"
      ],
      "defaultFilename": "%DESTINATION%_%SEGMENT_ID%"
    }
  },
  "destinationDelivery": [
    {
      "deliveryMatchers": [
        {
          "type": "SOURCE",
          "value": [
            "batch"
          ]
        }
      ],
      "authenticationRule": "CUSTOMER_AUTHENTICATION",
      "destinationServerId": "<server-id>"
    }
  ]
}'
```

Una risposta corretta restituisce la configurazione di destinazione, incluso l&#39;identificatore univoco (`instanceId`) della configurazione.

## Limitazioni note {#known-limitations}

Una determinata combinazione di opzioni di formattazione dei file può portare a risultati di esportazione indesiderati.
L’Adobe consiglia di non selezionare la seguente combinazione di opzioni CSV:

```
nullValue -> ""
quote -> "
emptyValue -> ""
```

Per esemplificare la limitazione, prendere in considerazione l&#39;esportazione di un file con i valori seguenti:

| nome | cognome | paese | Stato |
|---------|----------|---------|--------|
| Michael | Rosa | Stati Uniti | NY |
| James | Smith |  | null |

{style="table-layout:auto"}

Questo si tradurrebbe in un output come mostrato di seguito. Il valore null della tabella viene esportato in modo errato come virgolette di escape.

```csv
Michael,Rose,USA,NY 
James,Smith,"","\"\""
```

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, saprai come impostare le opzioni di formattazione dei file personalizzati per i file esportati utilizzando Destination SDK. Successivamente, il tuo team può utilizzare il [flusso di lavoro di attivazione per le destinazioni basate su file](../../../ui/activate-batch-profile-destinations.md) per esportare i dati nella destinazione.
