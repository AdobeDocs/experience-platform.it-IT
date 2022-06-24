---
title: Endpoint API per conversione da modello CSV a schema
description: L’endpoint /rpc/csv2schema nell’API del Registro di sistema dello schema consente di utilizzare modelli CSV per creare automaticamente schemi Experience Data Model (XDM).
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
source-git-commit: b4c186c8c40d1372fb5011f49979523e1201fb0b
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 6%

---

# Modello CSV per endpoint API di conversione dello schema

La `/rpc/csv2schema` punto finale [!DNL Schema Registry] L’API ti consente di creare automaticamente uno schema Experience Data Model (XDM) utilizzando un file CSV come modello. Utilizzando questo endpoint, puoi creare modelli per importare in massa campi dello schema e ridurre le operazioni manuali di API o interfaccia utente.

## Introduzione

La `/rpc/csv2schema` l&#39;endpoint fa parte del [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio presenti in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API Adobe Experience Platform.

La `/rpc/csv2schema` l&#39;endpoint fa parte delle chiamate di routine remote (RPC) supportate dal [!DNL Schema Registry]. A differenza di altri endpoint nel [!DNL Schema Registry] API, gli endpoint RPC non richiedono intestazioni aggiuntive come `Accept` o `Content-Type`e non utilizzano un `CONTAINER_ID`. Invece, devono utilizzare il `/rpc` namespace, come illustrato nelle chiamate API riportate di seguito.

## Requisiti del file CSV

Per utilizzare questo endpoint, devi innanzitutto creare un file CSV con intestazioni di colonna appropriate e i valori corrispondenti. Alcune colonne sono obbligatorie, mentre le altre sono facoltative. La tabella seguente descrive queste colonne e il loro ruolo nella costruzione dello schema.

| Posizione intestazione CSV | Nome intestazione CSV | Obbligatorio/facoltativo | Descrizione |
| --- | --- | --- | --- |
| 1 | `isIgnored` | Facoltativo | Quando incluso e impostato su `true`, indica che il campo non è pronto per il caricamento dell’API e deve essere ignorato. |
| 2 | `isCustom` | Obbligatorio | Indica se il campo è un campo personalizzato o meno. |
| 3 | `fieldGroupId` | Facoltativo | L’ID del gruppo di campi a cui deve essere associato un campo personalizzato. |
| 4 | `fieldGroupName` | (Vedere descrizione) | Nome del gruppo di campi a cui associare il campo.<br><br>Facoltativo per campi personalizzati che non estendono campi standard esistenti. Se lasciato vuoto, il sistema assegna automaticamente il nome.<br><br>Obbligatorio per campi standard o campi personalizzati che estendono gruppi di campi standard, utilizzato per eseguire query sul campo `fieldGroupId`. |
| 5 | `fieldPath` | Obbligatorio | Percorso di notazione del punto XED completo per il campo. Per includere tutti i campi di un gruppo di campi standard (come indicato in `fieldGroupName`), imposta il valore su `ALL`. |
| 6 | `displayName` | Facoltativo | Titolo o nome visualizzato descrittivo per il campo. Può anche essere un alias per il titolo, se presente. |
| 7 | `fieldDescription` | Facoltativo | Descrizione del campo. Può anche essere un alias della descrizione, se presente. |
| 8 | `dataType` | (Vedere descrizione) | Indica la [tipo di dati di base](../schema/field-constraints.md#basic-types) per il campo . Obbligatorio per tutti i campi personalizzati.<br><br>Se `dataType` è impostato su `object`o `properties` o `$ref` deve essere definito anche per la stessa riga, ma non per entrambe. |
| 9 | `isRequired` | Facoltativo | Indica se il campo è obbligatorio per l’inserimento dei dati. |
| 10 | `isArray` | Facoltativo | Indica se il campo è una matrice dei relativi `dataType`. |
| 11 | `isIdentity` | Facoltativo | Indica se il campo è un campo di identità. |
| 12 | `identityNamespace` | Obbligatorio se `isIdentity` è vero | La [spazio dei nomi identità](../../identity-service/namespaces.md) per il campo identity. |
| 13 | `isPrimaryIdentity` | Facoltativo | Indica se il campo è l&#39;identità principale dello schema. |
| 14 | `minimum` | Facoltativo | (Solo per i campi numerici) Il valore minimo del campo. |
| 15 | `maximum` | Facoltativo | (Solo per i campi numerici) Il valore massimo del campo. |
| 16 | `enum` | Facoltativo | Elenco dei valori enum per il campo, espressi come matrice (ad esempio `[value1,value2,value3]`). |
| 17 | `stringPattern` | Facoltativo | (Solo per i campi stringa) Pattern regex a cui deve corrispondere il valore stringa per poter passare la convalida durante l’inserimento dei dati. |
| 18 | `format` | Facoltativo | (Solo per i campi stringa) Il formato del campo stringa. |
| 19 | `minLength` | Facoltativo | (Solo per i campi stringa) La lunghezza minima del campo stringa. |
| 20 | `maxLength` | Facoltativo | (Solo per i campi stringa) La lunghezza massima del campo stringa. |
| 21 | `properties` | (Vedere descrizione) | Obbligatorio se `dataType` è impostato su `object` e `$ref` non è definito. Definisce il corpo dell’oggetto come una stringa JSON (ad es. `{"myField": {"type": "string"}}`). |
| 22 | `$ref` | (Vedere descrizione) | Obbligatorio se `dataType` è impostato su `object` e `properties` non è definito. Definisce la `$id` dell&#39;oggetto a cui si fa riferimento per il tipo di oggetto (ad esempio `https://ns.adobe.com/xdm/context/person`). |
| 23 | `comment` | Facoltativo | Quando `isIgnored` è impostato su `true`, questa colonna viene utilizzata per fornire le informazioni di intestazione dello schema. |

{style=&quot;table-layout:auto&quot;}

Consulta quanto segue [Modello CSV](../assets/sample-csv-template.csv) per determinare come deve essere formattato il file CSV.

## Creare un payload di esportazione da un file CSV

Una volta configurato il modello CSV, puoi inviare il file al `/rpc/csv2schema` e convertirlo in un payload di esportazione.

**Formato API**

```http
POST /rpc/csv2schema
```

**Richiesta**

Il payload della richiesta deve utilizzare i dati del modulo come formato. I campi modulo richiesti sono visualizzati di seguito.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/csv2schema \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'csv-file=@"/Users/userName/Documents/sample-csv-template.csv"' \
  -F 'schema-class-id="https://ns.adobe.com/xdm/context/profile"' \
  -F 'schema-name="Example Schema"' \
  -F 'schema-description="Example schema description."'
```

| Proprietà | Descrizione |
| --- | --- |
| `csv-file` | Percorso del modello CSV memorizzato nel computer locale. |
| `schema-class-id` | La `$id` dell&#39;XDM [Classe](../schema/composition.md#class) che lo schema verrà utilizzato. |
| `schema-name` | Un nome visualizzato per lo schema. |
| `schema-description` | Una descrizione dello schema. |

**Risposta**

Una risposta corretta restituisce un payload di esportazione generato dal file CSV. Il payload si presenta come una matrice e ogni elemento array è un oggetto che rappresenta un componente XDM dipendente per lo schema. Seleziona la sezione seguente per visualizzare un esempio completo di payload di esportazione generato da un file CSV.

+++ Payload di risposta di esempio

```json
[
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "description": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "required": [
            "_ddgxdmint"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField1": {
                        "type": "string",
                        "title": "my custom field1",
                        "description": "Sample custom field1"
                    },
                    "customField2": {
                        "properties": {
                            "customerField22": {
                                "type": "string",
                                "title": "my custom field22",
                                "description": "Sample custom field22"
                            }
                        },
                        "type": "object",
                        "required": [
                            "customerField22"
                        ]
                    },
                    "customField3": {
                        "type": "number",
                        "title": "my custom field3",
                        "description": "Sample custom field3",
                        "minimum": 0,
                        "maximum": 10
                    },
                    "customField4": {
                        "type": "string",
                        "title": "my custom field4",
                        "description": "Sample custom field4",
                        "enum": [
                            "one",
                            "two",
                            "three"
                        ]
                    },
                    "customField5": {
                        "type": "array",
                        "title": "my custom field5",
                        "description": "Sample custom field5",
                        "items": {
                            "type": "string"
                        }
                    },
                    "customField6": {
                        "type": "string",
                        "title": "my custom field6",
                        "description": "Sample custom field6",
                        "format": "date"
                    }
                },
                "type": "object",
                "required": [
                    "customField1",
                    "customField2"
                ]
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "SampleFieldGroup",
        "description": "Generated field group 7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField7": {
                        "type": "object",
                        "title": "my custom field7",
                        "description": "Sample custom field7",
                        "properties": {
                            "myField": {
                                "type": "string"
                            }
                        }
                    },
                    "customField8": {
                        "type": "array",
                        "title": "my custom field8",
                        "description": "Sample custom field8",
                        "items": {
                            "type": "object",
                            "$ref": "https://ns.adobe.com/xdm/context/person"
                        }
                    }
                },
                "type": "object"
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Demographic Details:Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "description": "Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile-person-details"
        ],
        "allOf": [
            {
                "properties": {
                    "person": {
                        "properties": {
                            "name": {
                                "properties": {
                                    "_ddgxdmint": {
                                        "properties": {
                                            "nickName": {
                                                "type": "string"
                                            }
                                        },
                                        "type": "object",
                                        "required": [
                                            "nickName"
                                        ]
                                    }
                                },
                                "type": "object",
                                "required": [
                                    "_ddgxdmint"
                                ]
                            }
                        },
                        "type": "object",
                        "required": [
                            "name"
                        ]
                    }
                },
                "required": [
                    "person"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Loyalty Details:Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "description": "Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
        ],
        "allOf": [
            {
                "properties": {
                    "loyalty": {
                        "properties": {
                            "_ddgxdmint": {
                                "properties": {
                                    "joinDate": {
                                        "type": "string"
                                    }
                                },
                                "type": "object"
                            }
                        },
                        "type": "object"
                    }
                }
            },
            {
                "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "schemas",
        "title": "My Sample Schema",
        "description": "My Sample Schema",
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
                "meta:refProperty": [
                    "/person/name/firstName",
                    "/person/name/lastName",
                    "/person/name/_ddgxdmint/nickName"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241"
            }
        ]
    },
    {
        "@type": "xdm:alternateDisplayInfo",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/person/name/firstName",
        "xdm:title": {
            "en_us": "My first name"
        }
    },
    {
        "@type": "xdm:descriptorIdentity",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_ddgxdmint/customField1",
        "xdm:namespace": "email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": true
    }
]
```

+++

## Importare il payload dello schema

Dopo aver generato il payload di esportazione dal file CSV, puoi inviare tale payload al `/rpc/import` per generare lo schema.

Consulta la sezione [guida all’importazione di endpoint](./import.md) per informazioni dettagliate su come generare schemi dai payload di esportazione.
