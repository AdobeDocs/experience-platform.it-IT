---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;modello dati;modello dati;modello dati;modello dati;registro classi;registro schemi;classe;classi;classi;creazione
solution: Experience Platform
title: Endpoint API classi
description: L’endpoint /classes nell’API Schema Registry consente di gestire in modo programmatico le classi XDM all’interno dell’applicazione Experience.
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 2%

---

# Endpoint &quot;class&quot;

Tutti gli schemi Experience Data Model (XDM) devono essere basati su una classe. Una classe determina la struttura di base delle proprietà comuni che tutti gli schemi basati su tale classe devono contenere, nonché i gruppi di campi di schema idonei per l’utilizzo in tali schemi. Inoltre, la classe di uno schema determina gli aspetti comportamentali dei dati che uno schema conterrà, di cui esistono due tipi:

* **[!UICONTROL Record]**: fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **[!UICONTROL Serie temporale]**: fornisce un&#39;istantanea del sistema nel momento in cui un oggetto record ha eseguito un&#39;azione direttamente o indirettamente.

>[!NOTE]
>
>Per ulteriori informazioni sui comportamenti dei dati in termini di impatto sulla composizione dello schema, fare riferimento alle [nozioni di base sulla composizione dello schema](../schema/composition.md).

L&#39;endpoint `/classes` nell&#39;API [!DNL Schema Registry] consente di gestire in modo programmatico le classi all&#39;interno dell&#39;applicazione Experience.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39;[[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e per le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recuperare un elenco di classi {#list}

È possibile elencare tutte le classi nel contenitore `global` o `tenant` effettuando una richiesta GET rispettivamente a `/global/classes` o `/tenant/classes`.

>[!NOTE]
>
>Quando si elencano le risorse, il registro dello schema limita il set di risultati a 300 elementi. Per restituire risorse oltre questo limite, è necessario utilizzare i parametri di paging. È inoltre consigliabile utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Per ulteriori informazioni, vedere la sezione relativa ai [parametri di query](./appendix.md#query) nel documento dell&#39;appendice.

**Formato API**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Contenitore da cui recuperare le classi: `global` per le classi create dall&#39;Adobe o `tenant` per le classi appartenenti all&#39;organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query facoltativi in base ai quali filtrare i risultati. Per un elenco dei parametri disponibili, vedere il [documento di appendice](./appendix.md#query). |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera un elenco di classi dal contenitore `tenant`, utilizzando un parametro di query `orderby` per ordinare le classi in base al relativo attributo `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall&#39;intestazione `Accept` inviata nella richiesta. Le seguenti intestazioni `Accept` sono disponibili per l&#39;elenco delle classi:

| Intestazione `Accept` | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Questa è l’intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce la classe JSON completa per ogni risorsa, inclusi `$ref` e `allOf` originali. (Limite: 300) |

{style="table-layout:auto"}

**Risposta**

La richiesta precedente ha utilizzato l&#39;intestazione `application/vnd.adobe.xed-id+json` `Accept`, pertanto la risposta include solo gli attributi `title`, `$id`, `meta:altId` e `version` per ogni classe. L&#39;utilizzo dell&#39;altra intestazione `Accept` (`application/vnd.adobe.xed+json`) restituisce tutti gli attributi di ciascuna classe. Selezionare l&#39;intestazione `Accept` appropriata in base alle informazioni richieste nella risposta.

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
| `{CONTAINER_ID}` | Il contenitore che ospita la classe che si desidera recuperare: `global` per una classe creata da un Adobe o `tenant` per una classe di proprietà dell&#39;organizzazione. |
| `{CLASS_ID}` | `meta:altId` o `$id` con codifica URL della classe che si desidera cercare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera una classe in base al valore `meta:altId` fornito nel percorso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall&#39;intestazione `Accept` inviata nella richiesta. Tutte le richieste di ricerca richiedono l&#39;inclusione di `version` nell&#39;intestazione `Accept`. Sono disponibili le seguenti `Accept` intestazioni:

| Intestazione `Accept` | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw con `$ref` e `allOf`, con titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e `allOf` risolti, con titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw con `$ref` e `allOf`, nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e `allOf` risolti, nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e `allOf` risolti, descrittori inclusi. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della classe. I campi restituiti dipendono dall&#39;intestazione `Accept` inviata nella richiesta. Prova a confrontare le risposte con intestazioni `Accept` diverse e a determinare quale sia il migliore per il tuo caso d&#39;uso.

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

È possibile definire una classe personalizzata nel contenitore `tenant` effettuando una richiesta POST.

>[!IMPORTANT]
>
>Durante la composizione di uno schema basato su una classe personalizzata definita dall’utente, non è possibile utilizzare gruppi di campi standard. Ogni gruppo di campi definisce le classi con cui sono compatibili nel loro attributo `meta:intendedToExtend`. Una volta iniziata la definizione dei gruppi di campi compatibili con la nuova classe (utilizzando `$id` della nuova classe nel campo `meta:intendedToExtend` del gruppo di campi), sarà possibile riutilizzare tali gruppi di campi ogni volta che si definisce uno schema che implementa la classe definita. Per ulteriori informazioni, consulta le sezioni su [creazione di gruppi di campi](./field-groups.md#create) e [creazione di schemi](./schemas.md#create) nelle rispettive guide degli endpoint.
>
>Se prevedi di utilizzare schemi basati su classi personalizzate in Real-Time Customer Profile, è inoltre importante tenere presente che gli schemi di unione vengono costruiti solo in base a schemi che condividono la stessa classe. Se si desidera includere uno schema di classe personalizzata nell&#39;unione per un&#39;altra classe, ad esempio [!UICONTROL XDM Individual Profile] o [!UICONTROL XDM ExperienceEvent], è necessario stabilire una relazione con un altro schema che utilizza tale classe. Per ulteriori informazioni, consulta il tutorial su [stabilire una relazione tra due schemi nell&#39;API](../tutorials/relationship-api.md).

**Formato API**

```http
POST /tenant/classes
```

**Richiesta**

La richiesta di creazione (POST) di una classe deve includere un attributo `allOf` contenente un valore `$ref` in uno dei due valori seguenti: `https://ns.adobe.com/xdm/data/record` o `https://ns.adobe.com/xdm/data/time-series`. Questi valori rappresentano il comportamento su cui si basa la classe (rispettivamente record o serie temporali). Per ulteriori informazioni sulle differenze tra i dati dei record e i dati delle serie temporali, vedere la sezione sui tipi di comportamento all&#39;interno delle [nozioni di base sulla composizione dello schema](../schema/composition.md).

Quando si definisce una classe, è possibile includere anche gruppi di campi o campi personalizzati all&#39;interno della definizione della classe. In questo modo, i gruppi di campi e i campi aggiunti verrebbero inclusi in tutti gli schemi che implementano la classe. L’esempio di richiesta seguente definisce una classe denominata &quot;Property&quot; (Proprietà), che acquisisce informazioni relative a diverse proprietà possedute e gestite da un’azienda. Include un campo `propertyId` da includere ogni volta che la classe viene utilizzata.

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
| `_{TENANT_ID}` | Lo spazio dei nomi `TENANT_ID` per la tua organizzazione. Tutte le risorse create dall&#39;organizzazione devono includere questa proprietà per evitare conflitti con altre risorse in [!DNL Schema Registry]. |
| `allOf` | Elenco di risorse le cui proprietà devono essere ereditate dalla nuova classe. Uno degli oggetti `$ref` nell&#39;array definisce il comportamento della classe. In questo esempio, la classe eredita il comportamento &quot;record&quot;. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli della classe appena creata, inclusi `$id`, `meta:altId` e `version`. Questi tre valori sono di sola lettura e sono assegnati da [!DNL Schema Registry].

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

L&#39;esecuzione di una richiesta di GET per [elencare tutte le classi](#list) nel contenitore `tenant` includerebbe ora la classe Property. È inoltre possibile [eseguire una richiesta di ricerca (GET)](#lookup) utilizzando l&#39;URL codificato `$id` per visualizzare direttamente la nuova classe.

## Aggiornare una classe {#put}

Puoi sostituire un’intera classe tramite un’operazione PUT, essenzialmente riscrivendo la risorsa. Quando si aggiorna una classe tramite una richiesta PUT, il corpo deve includere tutti i campi necessari per [la creazione di una nuova classe](#create) in una richiesta POST.

>[!NOTE]
>
>Se si desidera aggiornare solo una parte di una classe invece di sostituirla completamente, vedere la sezione relativa all&#39;aggiornamento di una parte di una classe](#patch).[

**Formato API**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | `meta:altId` o `$id` con codifica URL della classe che si desidera riscrivere. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente riscrive una classe esistente, modificandone `description` e `title` di uno dei suoi campi.

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

È possibile aggiornare una parte di una classe utilizzando una richiesta PATCH. [!DNL Schema Registry] supporta tutte le operazioni Patch JSON standard, inclusi `add`, `remove` e `replace`. Per ulteriori informazioni sulla patch JSON, consulta la [guida delle API fondamentali](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Se si desidera sostituire un&#39;intera risorsa con nuovi valori invece di aggiornare singoli campi, vedere la sezione relativa alla [sostituzione di una classe mediante un&#39;operazione PUT](#put).

**Formato API**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | URI `$id` con codifica URL o `meta:altId` della classe da aggiornare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta di esempio seguente aggiorna il `description` di una classe esistente e il `title` di uno dei suoi campi.

Il corpo della richiesta è un array e ogni oggetto elencato rappresenta una modifica specifica di un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), il campo in cui deve essere eseguita l&#39;operazione (`path`) e le informazioni da includere nell&#39;operazione (`value`).

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

La risposta mostra che entrambe le operazioni sono state eseguite correttamente. `description` è stato aggiornato insieme a `title` del campo `propertyId`.

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
| `{CLASS_ID}` | URI `$id` con codifica URL o `meta:altId` della classe che si desidera eliminare. |

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

È possibile confermare l&#39;eliminazione tentando una [richiesta di ricerca (GET)](#lookup) per la classe. È necessario includere un&#39;intestazione `Accept` nella richiesta, ma dovrebbe ricevere lo stato HTTP 404 (Non trovato) perché la classe è stata rimossa dal registro degli schemi.
