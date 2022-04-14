---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro classi;registro schema;classe;classi;creare
solution: Experience Platform
title: Endpoint API per le classi
description: L’endpoint /classes nell’API del Registro di sistema dello schema consente di gestire in modo programmatico le classi XDM all’interno dell’applicazione di esperienza.
topic-legacy: developer guide
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 74ef1b3abb90ab3ca24690c88c073083f02a2f1b
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 4%

---

# Endpoint delle classi

Tutti gli schemi Experience Data Model (XDM) devono essere basati su una classe . Una classe determina la struttura di base delle proprietà comuni che devono contenere tutti gli schemi basati su tale classe, nonché i gruppi di campi dello schema idonei all&#39;utilizzo in tali schemi. Inoltre, la classe di uno schema determina gli aspetti comportamentali dei dati contenuti in uno schema, di cui esistono due tipi:

* **[!UICONTROL Record]**: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **[!UICONTROL Serie temporali]**: Fornisce un&#39;istantanea del sistema al momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

>[!NOTE]
>
>Per ulteriori classi di informazioni sui comportamenti dei dati in termini di come influiscono sulla composizione dello schema, consulta [nozioni di base sulla composizione dello schema](../schema/composition.md).

La `/classes` punto finale [!DNL Schema Registry] L’API ti consente di gestire le classi a livello di programmazione all’interno dell’applicazione di esperienza.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[[!DNL Schema Registry] API di ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di classi {#list}

È possibile elencare tutte le classi nella sezione `global` o `tenant` effettuando una richiesta GET a `/global/classes` o `/tenant/classes`, rispettivamente.

>[!NOTE]
>
>Quando si elencano le risorse, il Registro di sistema dello schema limita i set di risultati a 300 elementi. Per restituire le risorse oltre questo limite, è necessario utilizzare i parametri di paging. Si consiglia inoltre di utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Vedi la sezione su [parametri di query](./appendix.md#query) nel documento di appendice per ulteriori informazioni.

**Formato API**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore da cui si desidera recuperare le classi: `global` per classi create da Adobi o `tenant` per le classi di proprietà della tua organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query opzionali per filtrare i risultati in base a. Consulta la sezione [documento appendice](./appendix.md#query) per un elenco dei parametri disponibili. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente recupera un elenco di classi dalla `tenant` contenitore, utilizzando un `orderby` parametro di query per ordinare le classi in base alle rispettive `title` attributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dal `Accept` intestazione inviata nella richiesta. I seguenti `Accept` le intestazioni sono disponibili per le classi di elenco:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce la classe JSON completa per ogni risorsa, con originale `$ref` e `allOf` incluso. (Limite: 300) |

{style=&quot;table-layout:auto&quot;}

**Risposta**

La richiesta di cui sopra ha utilizzato il `application/vnd.adobe.xed-id+json` `Accept` , quindi la risposta include solo l’ `title`, `$id`, `meta:altId`e `version` attributi per ogni classe. Utilizzo dell&#39;altro `Accept` header (`application/vnd.adobe.xed+json`) restituisce tutti gli attributi di ogni classe. Selezionare il `Accept` a seconda delle informazioni richieste nella risposta.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
      "meta:altId": "_{TENANT_ID}.classes.01b7b1745e8ac4ed1e8784ec91b6afa7",
      "version": "1.0",
      "title": "Hotel"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/d43b86253676af50da3f671ecdd26ff9",
      "meta:altId": "_{TENANT_ID}.classes.d43b86253676af50da3f671ecdd26ff9",
      "version": "1.1",
      "title": "Property"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/366f015dbfea802455fbc46c3b27f771",
      "meta:altId": "_{TENANT_ID}.classes.366f015dbfea802455fbc46c3b27f771",
      "version": "1.0",
      "title": "Subscription"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/classes"
    }
  }
}
```

## Cerca una classe {#lookup}

Puoi cercare una classe specifica includendo l’ID della classe nel percorso di una richiesta GET.

**Formato API**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore che ospita la classe da recuperare: `global` per una classe creata da un Adobe o `tenant` per una classe di proprietà della tua organizzazione. |
| `{CLASS_ID}` | La `meta:altId` o con codifica URL `$id` della classe che si desidera cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente recupera una classe dalla relativa `meta:altId` nel percorso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dal `Accept` intestazione inviata nella richiesta. Tutte le richieste di ricerca richiedono un `version` sono inclusi nella `Accept` intestazione. I seguenti `Accept` le intestazioni sono disponibili:

| `Accept` header | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw con `$ref` e `allOf`, include titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e `allOf` risolto, con titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw con `$ref` e `allOf`, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e `allOf` risolto, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e `allOf` risolti, descrittori inclusi. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli della classe. I campi restituiti dipendono dal `Accept` intestazione inviata nella richiesta. Esperimento con diversi `Accept` intestazioni per confrontare le risposte e determinare quale intestazione è migliore per il tuo caso d’uso.

```json
{
  "$id":"https://ns.adobe.com/{TENANT_ID}/classes/f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:altId":"_{TENANT_ID}.classes.f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:resourceType":"classes",
  "version":"1.1",
  "title":"Hotel",
  "type":"object",
  "description":"Base class for the Hotels schema",
  "definitions":{
    "customFields":{
      "type":"object",
      "properties":{
        "_{TENANT_ID}":{
          "type":"object",
          "properties":{
            "Address":{
              "title":"Address",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/common/address",
              "type":"object",
              "meta:xdmType":"object"
            },
            "phoneNumber":{
              "title":"Phone Number",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/context/phonenumber",
              "type":"object",
              "meta:xdmType":"object"
            },
            "brand":{
              "title":"Brand",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            },
            "hotelId":{
              "title":"Hotel ID",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            }
          },
          "meta:xdmType":"object"
        }
      },
      "meta:xdmType":"object"
    }
  },
  "allOf":[
    {
      "$ref":"https://ns.adobe.com/xdm/data/record",
      "type":"object",
      "meta:xdmType":"object"
    },
    {
      "$ref":"#/definitions/customFields",
      "type":"object",
      "meta:xdmType":"object"
    }
  ],
  "imsOrg":"{IMS_ORG}",
  "meta:extensible":true,
  "meta:abstract":true,
  "meta:extends":[
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:xdmType":"object",
  "meta:registryMetadata":{
    "repo:createdDate":1593643258779,
    "repo:lastModifiedDate":1597246362579,
    "xdm:createdClientId":"{CLIENT_ID}",
    "xdm:lastModifiedClientId":"{CLIENT_ID}",
    "xdm:createdUserId":"{USER_ID}",
    "xdm:lastModifiedUserId":"{USER_ID}",
    "eTag":"502f89ee16b8ab2e6b4ea09ecf0ab1e5614907db755051c1f3c65a273001d725",
    "meta:globalLibVersion":"1.15.4"
  },
  "meta:containerId":"tenant",
  "meta:tenantNamespace":"_{TENANT_ID}"
}
```

## Creare una classe {#create}

È possibile definire una classe personalizzata sotto la `tenant` effettuando una richiesta di POST.

>[!IMPORTANT]
>
>Quando si compone uno schema basato su una classe personalizzata definita dall&#39;utente, non è possibile utilizzare gruppi di campi standard. Ogni gruppo di campi definisce le classi con le quali è compatibile `meta:intendedToExtend` attributo. Una volta iniziato a definire gruppi di campi compatibili con la nuova classe, utilizzando `$id` della tua nuova classe `meta:intendedToExtend` campo del gruppo di campi), sarà possibile riutilizzare tali gruppi di campi ogni volta che si definisce uno schema che implementa la classe definita. Consulta le sezioni [creazione di gruppi di campi](./field-groups.md#create) e [creazione di schemi](./schemas.md#create) nelle rispettive guide dei punti finali per ulteriori informazioni.
>
>Se prevedi di utilizzare schemi basati su classi personalizzate in Profilo cliente in tempo reale, è anche importante tenere presente che gli schemi di unione sono costruiti solo in base a schemi che condividono la stessa classe. Se si desidera includere uno schema di classe personalizzato nell&#39;unione per un&#39;altra classe come [!UICONTROL Profilo individuale XDM] o [!UICONTROL ExperienceEvent XDM], è necessario stabilire una relazione con un altro schema che utilizza tale classe. Guarda l’esercitazione su [creazione di una relazione tra due schemi nell’API](../tutorials/relationship-api.md) per ulteriori informazioni.

**Formato API**

```http
POST /tenant/classes
```

**Richiesta**

La richiesta di creazione di una classe (POST) deve includere un `allOf` attributo contenente `$ref` a uno dei due valori seguenti: `https://ns.adobe.com/xdm/data/record` o `https://ns.adobe.com/xdm/data/time-series`. Questi valori rappresentano il comportamento su cui si basa la classe (record o serie temporali, rispettivamente). Per ulteriori informazioni sulle differenze tra i dati dei record e i dati delle serie temporali, consulta la sezione sui tipi di comportamento all&#39;interno della [nozioni di base sulla composizione dello schema](../schema/composition.md).

Quando si definisce una classe, è anche possibile includere gruppi di campi o campi personalizzati nella definizione della classe. In questo modo i gruppi di campi e i campi aggiunti verranno inclusi in tutti gli schemi che implementano la classe. La richiesta di esempio seguente definisce una classe denominata &quot;Property&quot;, che acquisisce informazioni relative a proprietà diverse possedute e gestite da un&#39;azienda. Include un `propertyId` campo da includere ogni volta che la classe viene utilizzata.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `_{TENANT_ID}` | La `TENANT_ID` spazio dei nomi per la tua organizzazione. Tutte le risorse create dall&#39;organizzazione devono includere questa proprietà per evitare conflitti con altre risorse nel [!DNL Schema Registry]. |
| `allOf` | Elenco di risorse le cui proprietà devono essere ereditate dalla nuova classe. Uno dei `$ref` gli oggetti all&#39;interno della matrice definiscono il comportamento della classe. In questo esempio, la classe eredita il comportamento &quot;record&quot;. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli della nuova classe creata, tra cui `$id`, `meta:altId`e `version`. Questi tre valori sono di sola lettura e sono assegnati dal [!DNL Schema Registry].

```JSON
{
  "title": "Property",
  "description": "Properties owned and operated by the company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property Identification Number",
                  "type": "string",
                  "description": "Unique Property identification number",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

Esecuzione di una richiesta GET a [elenco tutte le classi](#list) in `tenant` Il contenitore ora include la classe Property . È inoltre possibile [eseguire una richiesta di ricerca (GET)](#lookup) utilizzando l’URL-encoded `$id` per visualizzare direttamente la nuova classe.

## Aggiornare una classe {#put}

È possibile sostituire un&#39;intera classe tramite un&#39;operazione PUT, essenzialmente riscrivendo la risorsa. Quando si aggiorna una classe tramite una richiesta di PUT, il corpo deve includere tutti i campi necessari quando [creazione di una nuova classe](#create) in una richiesta POST.

>[!NOTE]
>
>Se si desidera aggiornare solo parte di una classe anziché sostituirla completamente, vedere la sezione in [aggiornamento di una parte di una classe](#patch).

**Formato API**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | La `meta:altId` o con codifica URL `$id` della classe che si desidera riscrivere. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta riscrive una classe esistente, modificandone la relativa `description` e `title` di uno dei suoi campi.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property",
        "description": "Base class for properties operated by a company.",
        "type": "object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property ID",
                        "type": "string",
                        "description": "Unique Property ID string."
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

**Risposta**

Una risposta corretta restituisce i dettagli della classe aggiornata.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Aggiornare una parte di una classe {#patch}

È possibile aggiornare una parte di una classe utilizzando una richiesta PATCH. La [!DNL Schema Registry] supporta tutte le operazioni standard di patch JSON, tra cui `add`, `remove`e `replace`. Per ulteriori informazioni sulla patch JSON, consulta la sezione [Guida di base sulle API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Per sostituire un’intera risorsa con nuovi valori anziché aggiornare singoli campi, consulta la sezione [sostituzione di una classe utilizzando un’operazione PUT](#put).

**Formato API**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | L’URL è codificato `$id` URI o `meta:altId` della classe da aggiornare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta di esempio riportata di seguito aggiorna la `description` di una classe esistente e `title` di uno dei suoi campi.

Il corpo della richiesta assume la forma di una matrice, con ogni oggetto elencato che rappresenta una modifica specifica a un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), su quale campo deve essere eseguita l&#39;operazione (`path`) e quali informazioni dovrebbero essere incluse in tale operazione (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Risposta**

La risposta indica che entrambe le operazioni sono state eseguite correttamente. La `description` è stato aggiornato insieme al `title` del `propertyId` campo .

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Eliminare una classe {#delete}

Talvolta può essere necessario rimuovere una classe dal Registro di sistema dello schema. A tal fine, esegui una richiesta DELETE con l’ID classe fornito nel percorso .

**Formato API**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | L’URL è codificato `$id` URI o `meta:altId` della classe da eliminare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

Puoi confermare l&#39;eliminazione tentando un [richiesta di ricerca (GET)](#lookup) per la classe. Sarà necessario includere un `Accept` intestazione nella richiesta, ma deve ricevere uno stato HTTP 404 (Non trovato) perché la classe è stata rimossa dal Registro di sistema dello schema.
