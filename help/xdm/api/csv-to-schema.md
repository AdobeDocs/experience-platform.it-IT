---
title: Endpoint API di conversione da modello CSV a schema
description: L’endpoint /rpc/csv2schema nell’API Schema Registry consente di utilizzare i modelli CSV per creare automaticamente gli schemi Experience Data Model (XDM).
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 5%

---

# Endpoint API di conversione da modello CSV a schema

Il `/rpc/csv2schema` endpoint nella [!DNL Schema Registry] API consente di creare automaticamente uno schema Experience Data Model (XDM) utilizzando un file CSV come modello. Utilizzando questo endpoint, puoi creare modelli per importare in blocco i campi dello schema e ridurre il lavoro manuale dell’API o dell’interfaccia utente.

## Introduzione

Il `/rpc/csv2schema` l&#39;endpoint fa parte del [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Prima di continuare, controlla [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API Adobe Experience Platform.

Il `/rpc/csv2schema` l&#39;endpoint fa parte delle chiamate di procedura remota (RPC) supportate dalla [!DNL Schema Registry]. A differenza di altri endpoint nel [!DNL Schema Registry] API, gli endpoint RPC non richiedono intestazioni aggiuntive come `Accept` o `Content-Type`, e non utilizzare un `CONTAINER_ID`. Devono invece utilizzare il `/rpc` dello spazio dei nomi, come dimostrato nelle chiamate API di seguito.

## Requisiti del file CSV

Per utilizzare questo endpoint, devi innanzitutto creare un file CSV con le intestazioni di colonna appropriate e i valori corrispondenti. Alcune colonne sono obbligatorie, mentre le altre sono facoltative. La tabella seguente descrive queste colonne e il loro ruolo nella costruzione dello schema.

| Posizione intestazione CSV | Nome intestazione CSV | Obbligatorio/facoltativo | Descrizione |
| --- | --- | --- | --- |
| 1 | `isIgnored` | Facoltativo | Se incluso e impostato su `true`, indica che il campo non è pronto per il caricamento API e deve essere ignorato. |
| 2 | `isCustom` | Obbligatorio | Indica se il campo è personalizzato o meno. |
| 3 | `fieldGroupId` | Facoltativo | ID del gruppo di campi a cui deve essere associato un campo personalizzato. |
| 4 | `fieldGroupName` | (Vedi descrizione) | Nome del gruppo di campi a cui associare il campo.<br><br>Facoltativo per i campi personalizzati che non estendono i campi standard esistenti. Se non specificato, il sistema assegnerà automaticamente il nome.<br><br>Obbligatorio per i campi standard o personalizzati che estendono gruppi di campi standard, utilizzati per eseguire query sulla proprietà `fieldGroupId`. |
| 5 | `fieldPath` | Obbligatorio | Percorso completo di notazione con punti XED per il campo. Per includere tutti i campi di un gruppo di campi standard (come indicato in `fieldGroupName`), imposta il valore su `ALL`. |
| 6 | `displayName` | Facoltativo | Titolo o nome visualizzato descrittivo del campo. Può anche essere un alias per il titolo, se presente. |
| 7 | `fieldDescription` | Facoltativo | Descrizione del campo. Può anche essere un alias per la descrizione, se presente. |
| 8 | `dataType` | (Vedi descrizione) | Indica il [tipo di dati di base](../schema/field-constraints.md#basic-types) per il campo. Obbligatorio per tutti i campi personalizzati.<br><br>Se `dataType` è impostato su `object`, sia `properties` o `$ref` deve essere definito anche per la stessa riga, ma non per entrambe. |
| 9 | `isRequired` | Facoltativo | Indica se il campo è obbligatorio per l’acquisizione dei dati. |
| 10 | `isArray` | Facoltativo | Indica se il campo è una matrice dei campi indicati `dataType`. |
| 11 | `isIdentity` | Facoltativo | Indica se il campo è un campo di identità. |
| 12 | `identityNamespace` | Obbligatorio se `isIdentity` è true | Il [spazio dei nomi delle identità](../../identity-service/features/namespaces.md) per il campo di identità. |
| 13 | `isPrimaryIdentity` | Facoltativo | Indica se il campo è l’identità primaria dello schema. |
| 14 | `minimum` | Facoltativo | (Solo per campi numerici) Il valore minimo per il campo. |
| 15 | `maximum` | Facoltativo | (Solo per campi numerici) Il valore massimo per il campo. |
| 16 | `enum` | Facoltativo | Un elenco di valori enum per il campo, espressi come matrice (ad es. `[value1,value2,value3]`). |
| 17 | `stringPattern` | Facoltativo | (Solo per i campi stringa) Pattern regex che il valore stringa deve corrispondere per passare la convalida durante l’acquisizione dei dati. |
| 18 | `format` | Facoltativo | (Solo per i campi stringa) Il formato del campo stringa. |
| 19 | `minLength` | Facoltativo | (Solo per i campi stringa) La lunghezza minima del campo stringa. |
| 20 | `maxLength` | Facoltativo | (Solo per i campi stringa) La lunghezza massima del campo stringa. |
| 21 | `properties` | (Vedi descrizione) | Obbligatorio se `dataType` è impostato su `object` e `$ref` non è definito. Definisce il corpo dell’oggetto come stringa JSON (ad esempio `{"myField": {"type": "string"}}`). |
| 22 | `$ref` | (Vedi descrizione) | Obbligatorio se `dataType` è impostato su `object` e `properties` non è definito. Questo definisce il `$id` dell&#39;oggetto di riferimento per il tipo di oggetto (ad esempio `https://ns.adobe.com/xdm/context/person`). |
| 23 | `comment` | Facoltativo | Quando `isIgnored` è impostato su `true`, questa colonna viene utilizzata per fornire le informazioni di intestazione dello schema. |

{style="table-layout:auto"}

Fai riferimento a quanto segue [Modello CSV](../assets/sample-csv-template.csv) per determinare come formattare il file CSV.

## Creare un payload di esportazione da un file CSV

Dopo aver configurato il modello CSV, puoi inviare il file al `/rpc/csv2schema` e convertirlo in un payload di esportazione.

**Formato API**

```http
POST /rpc/csv2schema
```

**Richiesta**

Il payload della richiesta deve utilizzare i dati del modulo come formato. I campi modulo richiesti sono mostrati di seguito.

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
| `schema-class-id` | Il `$id` del modello XDM [classe](../schema/composition.md#class) che questo schema utilizzerà. |
| `schema-name` | Un nome visualizzato per lo schema. |
| `schema-description` | Descrizione dello schema. |

**Risposta**

In caso di esito positivo, la risposta restituisce un payload di esportazione generato dal file CSV. Il payload assume la forma di un array e ogni elemento dell’array è un oggetto che rappresenta un componente XDM dipendente per lo schema. Seleziona la sezione seguente per visualizzare un esempio completo di payload di esportazione generato da un file CSV.

+++ Esempio di payload di risposta

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

Dopo aver generato il payload di esportazione dal file CSV, puoi inviarlo al `/rpc/import` per generare lo schema.

Consulta la [importa guida dell’endpoint](./import.md) per informazioni dettagliate su come generare schemi dai payload di esportazione.
