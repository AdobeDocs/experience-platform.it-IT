---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;modello dati;modello dati;modello dati;modello dati;registro classi;registro schemi;classe;classi;classi;creazione
solution: Experience Platform
title: Endpoint API classi
description: L’endpoint /classes nell’API Schema Registry consente di gestire in modo programmatico le classi XDM all’interno dell’applicazione Experience.
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 3%

---

# Endpoint &quot;class&quot;

Tutti gli schemi Experience Data Model (XDM) devono essere basati su una classe. Una classe determina la struttura di base delle proprietà comuni che tutti gli schemi basati su tale classe devono contenere, nonché i gruppi di campi di schema idonei per l’utilizzo in tali schemi. Inoltre, la classe di uno schema determina gli aspetti comportamentali dei dati che uno schema conterrà, di cui esistono due tipi:

* **[!UICONTROL Registra]**: fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **[!UICONTROL Serie temporali]**: fornisce un’istantanea del sistema nel momento in cui un oggetto record ha eseguito un’azione, direttamente o indirettamente.

>[!NOTE]
>
>Per ulteriori informazioni sui comportamenti dei dati in termini di influenza sulla composizione dello schema, consulta [nozioni di base sulla composizione dello schema](../schema/composition.md).

Il `/classes` endpoint nella [!DNL Schema Registry] API consente di gestire in modo programmatico le classi all’interno dell’applicazione Experience.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[[!DNL Schema Registry] API di ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Prima di continuare, controlla [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recuperare un elenco di classi {#list}

Puoi elencare tutte le classi sotto `global` o `tenant` mediante una richiesta GET a `/global/classes` o `/tenant/classes`, rispettivamente.

>[!NOTE]
>
>Quando si elencano le risorse, il registro dello schema limita il set di risultati a 300 elementi. Per restituire risorse oltre questo limite, è necessario utilizzare i parametri di paging. È inoltre consigliabile utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Consulta la sezione su [parametri di query](./appendix.md#query) nel documento dell’appendice per ulteriori informazioni.

**Formato API**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore da cui desideri recuperare le classi: `global` per le classi create da Adobi o `tenant` per le classi di proprietà della tua organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query facoltativi in base ai quali filtrare i risultati. Consulta la [documento dell&#39;appendice](./appendix.md#query) per un elenco dei parametri disponibili. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera un elenco di classi da `tenant` contenitore, utilizzando un `orderby` parametro di query per ordinare le classi in base alla relativa `title` attributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende da `Accept` intestazione inviata nella richiesta. I seguenti elementi `Accept` le intestazioni sono disponibili per l&#39;elenco delle classi:

| `Accept` intestazione | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Questa è l’intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce la classe JSON completa per ogni risorsa, con originale `$ref` e `allOf` incluso. (Limite: 300) |

{style="table-layout:auto"}

**Risposta**

La richiesta precedente utilizzava `application/vnd.adobe.xed-id+json` `Accept` , pertanto la risposta include solo il `title`, `$id`, `meta:altId`, e `version` attributi per ogni classe. Utilizzo dell&#39;altro `Accept` intestazione (`application/vnd.adobe.xed+json`) restituisce tutti gli attributi di ciascuna classe. Seleziona la scheda appropriata `Accept` a seconda delle informazioni richieste nella risposta.

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

## Cercare una classe {#lookup}

Per cercare una classe specifica, devi includere l’ID della classe nel percorso di una richiesta GET.

**Formato API**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore che ospita la classe che desideri recuperare: `global` per una classe creata da un Adobe oppure `tenant` per una classe di proprietà dell’organizzazione. |
| `{CLASS_ID}` | Il `meta:altId` o con codifica URL `$id` della classe che desideri cercare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera una classe in base al suo `meta:altId` valore fornito nel percorso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende da `Accept` intestazione inviata nella richiesta. Tutte le richieste di ricerca richiedono un `version` essere inclusi nel `Accept` intestazione. I seguenti elementi `Accept` le intestazioni sono disponibili:

| `Accept` intestazione | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw con `$ref` e `allOf`, ha titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e `allOf` risolto, con titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw con `$ref` e `allOf`, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e `allOf` risolto, nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e `allOf` risolto, inclusi i descrittori. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della classe. I campi restituiti dipendono dal `Accept` intestazione inviata nella richiesta. Sperimenta con diversi `Accept` intestazioni per confrontare le risposte e determinare quale intestazione è più adatta al tuo caso d’uso.

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
  "imsOrg":"{ORG_ID}",
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

Puoi definire una classe personalizzata in `tenant` effettuando una richiesta POST.

>[!IMPORTANT]
>
>Durante la composizione di uno schema basato su una classe personalizzata definita dall’utente, non è possibile utilizzare gruppi di campi standard. Ogni gruppo di campi definisce le classi con cui sono compatibili nei `meta:intendedToExtend` attributo. Una volta iniziata la definizione dei gruppi di campi compatibili con la nuova classe (utilizzando `$id` della nuova classe in `meta:intendedToExtend` del gruppo di campi), potrai riutilizzare tali gruppi di campi ogni volta che definisci uno schema che implementa la classe definita. Consulta le sezioni relative a [creazione di gruppi di campi](./field-groups.md#create) e [creazione di schemi](./schemas.md#create) nelle rispettive guide degli endpoint per ulteriori informazioni.
>
>Se prevedi di utilizzare schemi basati su classi personalizzate in Real-Time Customer Profile, è inoltre importante tenere presente che gli schemi di unione vengono costruiti solo in base a schemi che condividono la stessa classe. Se desideri includere uno schema di classe personalizzata nell’unione per un’altra classe come [!UICONTROL Profilo individuale XDM] o [!UICONTROL XDM ExperienceEvent], è necessario stabilire una relazione con un altro schema che utilizza tale classe. Guarda il tutorial su [che stabilisce una relazione tra due schemi nell’API](../tutorials/relationship-api.md) per ulteriori informazioni.

**Formato API**

```http
POST /tenant/classes
```

**Richiesta**

La richiesta di creazione (POST) di una classe deve includere `allOf` attributo contenente un `$ref` a uno dei due valori seguenti: `https://ns.adobe.com/xdm/data/record` o `https://ns.adobe.com/xdm/data/time-series`. Questi valori rappresentano il comportamento su cui si basa la classe (rispettivamente record o serie temporali). Per ulteriori informazioni sulle differenze tra i dati dei record e i dati delle serie temporali, vedere la sezione relativa ai tipi di comportamento all&#39;interno del [nozioni di base sulla composizione dello schema](../schema/composition.md).

Quando si definisce una classe, è possibile includere anche gruppi di campi o campi personalizzati all&#39;interno della definizione della classe. In questo modo, i gruppi di campi e i campi aggiunti verrebbero inclusi in tutti gli schemi che implementano la classe. L’esempio di richiesta seguente definisce una classe denominata &quot;Property&quot; (Proprietà), che acquisisce informazioni relative a diverse proprietà possedute e gestite da un’azienda. Include un `propertyId` da includere ogni volta che viene utilizzata la classe.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `_{TENANT_ID}` | Il `TENANT_ID` dello spazio dei nomi per la tua organizzazione. Tutte le risorse create dall’organizzazione devono includere questa proprietà per evitare conflitti con altre risorse in [!DNL Schema Registry]. |
| `allOf` | Elenco di risorse le cui proprietà devono essere ereditate dalla nuova classe. Uno dei `$ref` all&#39;interno dell&#39;array definisce il comportamento della classe. In questo esempio, la classe eredita il comportamento &quot;record&quot;. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli della classe appena creata, tra cui `$id`, `meta:altId`, e `version`. Questi tre valori sono di sola lettura e sono assegnati dal [!DNL Schema Registry].

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
  "imsOrg": "{ORG_ID}",
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

Esecuzione di una richiesta di GET a [elenca tutte le classi](#list) nel `tenant` Il contenitore ora include la classe Property. È inoltre possibile [eseguire una richiesta di ricerca (GET)](#lookup) utilizzando la codifica URL `$id` per visualizzare direttamente la nuova classe.

## Aggiornare una classe {#put}

Puoi sostituire un’intera classe tramite un’operazione PUT, essenzialmente riscrivendo la risorsa. Quando si aggiorna una classe tramite una richiesta PUT, il corpo deve includere tutti i campi necessari quando [creazione di una nuova classe](#create) in una richiesta POST.

>[!NOTE]
>
>Se si desidera aggiornare solo una parte di una classe anziché sostituirla completamente, vedere la sezione relativa [aggiornamento di una parte di una classe](#patch).

**Formato API**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | Il `meta:altId` o con codifica URL `$id` della classe che si desidera riscrivere. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente riscrive una classe esistente, modificandone la `description` e `title` di uno dei suoi campi.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

In caso di esito positivo, la risposta restituisce i dettagli della classe aggiornata.

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
  "imsOrg": "{ORG_ID}",
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

È possibile aggiornare una parte di una classe utilizzando una richiesta PATCH. Il [!DNL Schema Registry] supporta tutte le operazioni Patch JSON standard, tra cui `add`, `remove`, e `replace`. Per ulteriori informazioni sulla patch JSON, vedi [Guida di base sulle API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Se desideri sostituire un’intera risorsa con nuovi valori invece di aggiornare singoli campi, consulta la sezione su [sostituzione di una classe mediante un&#39;operazione PUT](#put).

**Formato API**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | Codifica URL `$id` URI o `meta:altId` della classe che desideri aggiornare. |

{style="table-layout:auto"}

**Richiesta**

L’esempio di richiesta seguente aggiorna la `description` di una classe esistente e `title` di uno dei suoi campi.

Il corpo della richiesta è un array e ogni oggetto elencato rappresenta una modifica specifica di un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), campo in cui deve essere eseguita l&#39;operazione (`path`) e quali informazioni devono essere incluse in tale operazione (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Risposta**

La risposta mostra che entrambe le operazioni sono state eseguite correttamente. Il `description` è stato aggiornato, insieme al `title` del `propertyId` campo.

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
  "imsOrg": "{ORG_ID}",
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

A volte può essere necessario rimuovere una classe dal registro degli schemi. Questa operazione viene eseguita eseguendo una richiesta DELETE con l’ID di classe fornito nel percorso.

**Formato API**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | Codifica URL `$id` URI o `meta:altId` della classe da eliminare. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) e un corpo vuoto.

È possibile confermare l’eliminazione tentando un [richiesta di ricerca (GET)](#lookup) per la classe. Dovrai includere un `Accept` nella richiesta, ma dovrebbe ricevere lo stato HTTP 404 (Non trovato) perché la classe è stata rimossa dal registro degli schemi.
