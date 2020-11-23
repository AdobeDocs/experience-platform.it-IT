---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;class registry;Schema Registry;class;Class;classes;Classes;create
solution: Experience Platform
title: Creazione di una classe
description: L'endpoint /class nell'API del Registro di sistema dello schema consente di gestire le classi XDM a livello di programmazione all'interno dell'applicazione dell'esperienza.
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 1%

---


# Endpoint delle classi

Tutti gli schemi XDM (Experience Data Model) devono essere basati su una classe. Una classe determina la struttura di base delle proprietà comuni che devono contenere tutti gli schemi basati su tale classe, nonché i mixin utilizzabili in tali schemi. Inoltre, la classe di uno schema determina gli aspetti comportamentali dei dati che uno schema conterrà, di cui esistono due tipi:

* **[!UICONTROL Record]**: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **[!UICONTROL Time-series]**: Fornisce un&#39;istantanea del sistema al momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

>[!NOTE]
>
>Per ulteriori informazioni sui comportamenti dei dati in termini di impatto sulla composizione dello schema, fare riferimento alle [nozioni di base della composizione](../schema/composition.md)dello schema.

L&#39; `/classes` endpoint nell&#39; [!DNL Schema Registry] API consente di gestire le classi a livello di programmazione all&#39;interno dell&#39;applicazione dell&#39;esperienza.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Prima di continuare, consultate la guida [](./getting-started.md) introduttiva per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API  Experience Platform.

## Recupero di un elenco di classi {#list}

È possibile elencare tutte le classi sotto il `global` contenitore o `tenant` eseguendo una richiesta di GET a `/global/classes` o, rispettivamente, `/tenant/classes`.

>[!NOTE]
>
>Quando si elencano le risorse, il Registro di sistema dello schema limita i set di risultati a 300 elementi. Per restituire risorse oltre questo limite, è necessario utilizzare i parametri di paging. È inoltre consigliabile utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Per ulteriori informazioni, consulta la sezione sui parametri [di](./appendix.md#query) query nel documento allegato.

**Formato API**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore da cui si desidera recuperare le classi: `global` per  classi create dal Adobe o `tenant` per classi di proprietà dell&#39;organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query facoltativi per filtrare i risultati per. Per un elenco dei parametri disponibili, consultare il documento [](./appendix.md#query) appendice. |

**Richiesta**

La richiesta seguente recupera un elenco di classi dal `tenant` contenitore, utilizzando un parametro di `orderby` query per ordinare le classi in base al relativo `title` attributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall’ `Accept` intestazione inviata nella richiesta. Le seguenti `Accept` intestazioni sono disponibili per le classi di elenco:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per elencare le risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce la classe JSON completa per ogni risorsa, con l&#39;originale `$ref` e `allOf` l&#39;inclusione. (Limite: 300) |

**Risposta**

La richiesta precedente ha utilizzato l&#39; `application/vnd.adobe.xed-id+json` intestazione, pertanto la risposta include solo gli `Accept` , `title`, `$id`e `meta:altId``version` gli attributi per ogni classe. Utilizzando l&#39;altra `Accept` intestazione (`application/vnd.adobe.xed+json`) vengono restituiti tutti gli attributi di ciascuna classe. Selezionate l’ `Accept` intestazione appropriata in base alle informazioni richieste nella risposta.

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

Potete cercare una classe specifica includendo l&#39;ID della classe nel percorso di una richiesta di GET.

**Formato API**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore che ospita la classe da recuperare: `global` per una classe  creata dal Adobe o `tenant` per una classe di proprietà dell&#39;organizzazione. |
| `{CLASS_ID}` | La `meta:altId` classe o l’URL codificato `$id` della classe da cercare. |

**Richiesta**

La richiesta seguente recupera una classe in base al `meta:altId` valore fornito nel percorso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall’ `Accept` intestazione inviata nella richiesta. Tutte le richieste di ricerca richiedono che `version` sia inclusa nell’ `Accept` intestazione. The following `Accept` headers are available:

| `Accept` header | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw con `$ref` e `allOf`, ha titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto, con titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw con `$ref` e `allOf`, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto, nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto, descrittori inclusi. |

**Risposta**

Una risposta corretta restituisce i dettagli della classe. I campi restituiti dipendono dall’ `Accept` intestazione inviata nella richiesta. Provate con `Accept` intestazioni diverse per confrontare le risposte e determinare quale intestazione è più adatta al caso d’uso.

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

## Creazione di una classe {#create}

Potete definire una classe personalizzata sotto il `tenant` contenitore effettuando una richiesta di POST.

>[!IMPORTANT]
>
>Quando si compone uno schema basato su una classe personalizzata definita dall&#39;utente, non sarà possibile utilizzare i mixin standard. Ciascun mixin definisce le classi con cui è compatibile nel relativo `meta:intendedToExtend` attributo. Una volta iniziata la definizione di mixin compatibili con la nuova classe (utilizzando la `$id` nuova classe nel `meta:intendedToExtend` campo del mixin), sarà possibile riutilizzare tali mixin ogni volta che si definisce uno schema che implementa la classe definita. Per ulteriori informazioni, consulta le sezioni sulla [creazione di mixin](./mixins.md#create) e sulla [creazione di schemi](./schemas.md#create) nelle rispettive guide degli endpoint.
>
>Se state pensando di utilizzare schemi basati su classi personalizzate in Real-time Customer Profile, è importante tenere presente che gli schemi di unione sono costruiti solo in base a schemi che condividono la stessa classe. Se si desidera includere uno schema di classe personalizzata nell&#39;unione per un&#39;altra classe come [!UICONTROL XDM Individual Profile] o [!UICONTROL XDM ExperienceEvent], è necessario stabilire una relazione con un altro schema che utilizza tale classe. Per ulteriori informazioni, vedete l&#39;esercitazione sulla [creazione di una relazione tra due schemi nell&#39;API](../tutorials/relationship-api.md) .

**Formato API**

```http
POST /tenant/classes
```

**Richiesta**

La richiesta di creare (POST) una classe deve includere un `allOf` attributo contenente un `$ref` massimo di due valori: `https://ns.adobe.com/xdm/data/record` o `https://ns.adobe.com/xdm/data/time-series`. Questi valori rappresentano il comportamento su cui si basa la classe (record o serie temporali, rispettivamente). Per ulteriori informazioni sulle differenze tra i dati dei record e i dati delle serie temporali, vedere la sezione sui tipi di comportamento all&#39;interno delle [nozioni di base della composizione](../schema/composition.md)dello schema.

Quando si definisce una classe, è possibile includere anche mixin o campi personalizzati nella definizione della classe. In questo modo i mixin e i campi aggiunti verranno inclusi in tutti gli schemi che implementano la classe. La seguente richiesta di esempio definisce una classe denominata &quot;Property&quot;, che acquisisce informazioni relative a diverse proprietà possedute e gestite da una società. Include un `propertyId` campo da includere ogni volta che la classe viene utilizzata.

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
| `_{TENANT_ID}` | Lo `TENANT_ID` spazio dei nomi per l&#39;organizzazione. Tutte le risorse create dall&#39;organizzazione devono includere questa proprietà per evitare conflitti con altre risorse nel [!DNL Schema Registry]. |
| `allOf` | Elenco di risorse le cui proprietà devono essere ereditate dalla nuova classe. Uno degli `$ref` oggetti all&#39;interno della matrice definisce il comportamento della classe. In questo esempio, la classe eredita il comportamento &quot;record&quot;. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli della nuova classe creata, inclusi `$id`, `meta:altId`e `version`. Questi tre valori sono di sola lettura e vengono assegnati dal [!DNL Schema Registry].

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

L&#39;esecuzione di una richiesta di GET per [elencare tutte le classi](#list) nel `tenant` contenitore ora include la classe Property. Potete anche [eseguire una richiesta](#lookup) di ricerca (GET) utilizzando l&#39;URL-encoded `$id` per visualizzare direttamente la nuova classe.

## Aggiornare una classe {#put}

È possibile sostituire un&#39;intera classe tramite un&#39;operazione PUT, in sostanza riscrivendo la risorsa. Quando si aggiorna una classe tramite una richiesta di PUT, il corpo deve includere tutti i campi che sarebbero necessari per [creare una nuova classe](#create) in una richiesta di POST.

>[!NOTE]
>
>Se si desidera aggiornare solo parte di una classe invece di sostituirla completamente, vedere la sezione sull&#39; [aggiornamento di una parte di una classe](#patch).

**Formato API**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | La `meta:altId` classe o l&#39;URL codificato `$id` della classe da riscrivere. |

**Richiesta**

La seguente richiesta riscrive una classe esistente, modificandone la proprietà `description` e la proprietà `title` di uno dei campi.

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

È possibile aggiornare una parte di una classe utilizzando una richiesta di PATCH. Supporta [!DNL Schema Registry] tutte le operazioni standard di patch JSON, inclusi `add`, `remove`e `replace`. Per ulteriori informazioni sulla patch JSON, consultate la guida [ai fondamentali](../../landing/api-fundamentals.md#json-patch)API.

>[!NOTE]
>
>Se si desidera sostituire un&#39;intera risorsa con nuovi valori invece di aggiornare i singoli campi, consultare la sezione relativa alla [sostituzione di una classe con un&#39;operazione](#put)PUT.

**Formato API**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | L’ `$id` URI con codifica URL o `meta:altId` della classe da aggiornare. |

**Richiesta**

La richiesta di esempio riportata di seguito aggiorna la `description` classe esistente e la `title` sua posizione.

Il corpo della richiesta assume la forma di una matrice, con ogni oggetto elencato che rappresenta una specifica modifica a un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), il campo sul quale deve essere eseguita l&#39;operazione (`path`) e quali informazioni devono essere incluse nell&#39;operazione (`value`).

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

La risposta indica che entrambe le operazioni sono state eseguite correttamente. Il campo `description` è stato aggiornato insieme al `title` campo `propertyId` .

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

Può essere talvolta necessario rimuovere una classe dal Registro di sistema dello schema. A tal fine, eseguite una richiesta di DELETE con l&#39;ID classe fornito nel percorso.

**Formato API**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | L’ `$id` URI con codifica URL o `meta:altId` della classe da eliminare. |

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

È possibile confermare l&#39;eliminazione tentando una richiesta [di](#lookup) ricerca (GET) per la classe. Sarà necessario includere un&#39; `Accept` intestazione nella richiesta, ma dovrebbe ricevere uno stato HTTP 404 (Non trovato) perché la classe è stata rimossa dal Registro di sistema dello schema.