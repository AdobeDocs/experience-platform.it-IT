---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare uno schema ad hoc
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 2%

---


# Creare uno schema ad hoc

In circostanze specifiche, potrebbe essere necessario creare uno schema [!DNL Experience Data Model] (XDM) con campi che vengono denominati separati per l&#39;uso solo da un singolo dataset. Tale schema è denominato &quot;ad hoc&quot;. Gli schemi ad hoc vengono utilizzati in vari flussi di lavoro di assimilazione dei dati per [!DNL Experience Platform], ad esempio per acquisire file CSV e creare determinati tipi di connessioni sorgente.

Questo documento contiene i passaggi generali per la creazione di uno schema ad hoc mediante l&#39;API [del Registro di](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)schema. È destinato ad essere utilizzato insieme ad altre [!DNL Experience Platform] esercitazioni che richiedono la creazione di uno schema ad hoc come parte del flusso di lavoro. Ciascuno di questi documenti fornisce informazioni dettagliate su come configurare correttamente uno schema ad hoc per il relativo caso di utilizzo specifico.

## Introduzione

Questa esercitazione richiede una buona conoscenza del sistema [!DNL Experience Data Model] (XDM). Prima di iniziare questa esercitazione, consulta la seguente documentazione XDM:

- [Panoramica](../home.md)del sistema XDM: Panoramica di alto livello di XDM e della sua implementazione in [!DNL Experience Platform].
- [Nozioni di base sulla composizione](../schema/composition.md)dello schema: Panoramica dei componenti di base degli schemi XDM.

Prima di iniziare questa esercitazione, consulta la guida [allo](../api/getting-started.md) sviluppo per informazioni importanti da conoscere per effettuare correttamente le chiamate all&#39; [!DNL Schema Registry] API. Ciò include il vostro `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni necessarie per effettuare le richieste (con particolare attenzione all’intestazione Accetta e ai suoi possibili valori).

## Creare una classe ad hoc

Il comportamento dei dati di uno schema XDM è determinato dalla classe sottostante. Il primo passaggio nella creazione di uno schema ad hoc consiste nel creare una classe basata sul `adhoc` comportamento. Questa operazione viene eseguita eseguendo una richiesta POST all&#39; `/tenant/classes` endpoint.

**Formato API**

```http
POST /tenant/classes
```

**Richiesta**

La richiesta seguente crea una nuova classe XDM, configurata dagli attributi forniti nel payload. Fornendo una `$ref` proprietà impostata su `https://ns.adobe.com/xdm/data/adhoc` nell&#39; `allOf` array, questa classe eredita il `adhoc` comportamento. La richiesta definisce anche un `_adhoc` oggetto, che contiene i campi personalizzati per la classe.

>[!NOTE]
>
>I campi personalizzati definiti in `_adhoc` variano a seconda del caso di utilizzo dello schema ad hoc. Fate riferimento al flusso di lavoro specifico nell&#39;esercitazione appropriata per i campi personalizzati richiesti in base al caso di utilizzo.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New ad-hoc class",
        "description": "New ad-hoc class description",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/xdm/data/adhoc"
          },
          {
            "properties": {
              "_adhoc": {
                "type":"object",
                "properties": {
                  "field1": {
                    "type":"string"
                  },
                  "field2": {
                    "type":"string"
                  }
                }
              }
            }
          }
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `$ref` | Il comportamento dei dati per la nuova classe. Per le classi ad hoc, questo valore deve essere impostato su `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Un oggetto che contiene i campi personalizzati per la classe, espressi come coppie chiave-valore di nomi di campo e tipi di dati. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova classe, sostituendo il nome dell&#39; `properties._adhoc` oggetto con un GUID che è un identificatore univoco di sola lettura generato dal sistema per la classe. Anche l’ `meta:datasetNamespace` attributo viene generato automaticamente e incluso nella risposta.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:altId": "_{TENANT_ID}.classes.6395cbd58812a6d64c4e5344f7b9120f",
    "meta:resourceType": "classes",
    "version": "1.0",
    "title": "New Class",
    "description": "New class description",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/adhoc"
        },
        {
            "properties": {
                "_6395cbd58812a6d64c4e5344f7b9120f": {
                    "type": "object",
                    "properties": {
                        "field1": {
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "field2": {
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557527784822,
        "repo:lastModifiedDate": 1557527784822,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `$id` | URI che funge da identificatore univoco generato dal sistema di sola lettura per la nuova classe ad hoc. Questo valore viene utilizzato nella fase successiva della creazione di uno schema ad hoc. |

## Creare uno schema ad hoc

Dopo aver creato una classe ad hoc, è possibile creare un nuovo schema che implementa tale classe effettuando una richiesta POST all&#39; `/tenant/schemas` endpoint.

**Formato API**

```http
POST /tenant/schemas
```

**Richiesta**

La richiesta seguente crea un nuovo schema, fornendo un riferimento (`$ref`) alla classe ad hoc creata in precedenza `$id` nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New Schema",
        "description": "New schema description.",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
          }
        ]
      }'
```

**Risposta**

Una risposta corretta restituisce i dettagli del nuovo schema creato, incluso il relativo sistema generato in sola lettura `$id`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
        }
    ],
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

## Visualizza lo schema ad hoc completo

>[!NOTE]
>
>Questo passaggio è facoltativo. Se non si desidera esaminare la struttura del campo dello schema ad hoc, è possibile passare alla sezione dei passaggi [](#next-steps) successivi alla fine dell&#39;esercitazione.

Una volta creato lo schema ad hoc, è possibile effettuare una richiesta di ricerca (GET) per visualizzare lo schema nel modulo espanso. A questo scopo, utilizzate l&#39;intestazione Accetto appropriata nella richiesta GET, come illustrato di seguito.

**Formato API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | L’ `$id` URI con codifica URL o `meta:altId` dello schema ad hoc a cui si desidera accedere. |

**Richiesta**

La richiesta seguente utilizza l&#39;intestazione Accetto `application/vnd.adobe.xed-full+json; version=1`, che restituisce il modulo espanso dello schema. Durante il recupero di una risorsa specifica dall&#39;intestazione [!DNL Schema Registry], l&#39;intestazione Accetto della richiesta deve includere la versione principale della risorsa in questione.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce i dettagli dello schema, inclusi tutti i campi nidificati in `properties`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "properties": {
        "_6395cbd58812a6d64c4e5344f7b9120f": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "field1": {
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "field2": {
                    "type": "string",
                    "meta:xdmType": "string"
                }
            }
        }
    },
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "bTogM1ON2LO/F7rlcc1iOWmNVy0="
    }
}
```

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, è stato creato con successo un nuovo schema ad hoc. Se siete stati portati in questo documento come parte di un&#39;altra esercitazione, ora potete utilizzare il `$id` dello schema ad hoc per completare il flusso di lavoro come indicato.

Per ulteriori informazioni sull&#39;utilizzo dell&#39; [!DNL Schema Registry] API, consultate la guida [allo](../api/getting-started.md)sviluppo.