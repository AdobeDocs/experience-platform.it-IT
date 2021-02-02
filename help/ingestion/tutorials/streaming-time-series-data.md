---
keywords: ' Experience Platform;home;popolari argomenti;streaming, assimilazione;inserimento;data delle serie temporali;data delle serie temporali;'
solution: Experience Platform
title: Streaming dei dati delle serie temporali
topic: tutorial
type: Tutorial
description: Questa esercitazione ti aiuterà a iniziare a utilizzare le API di assimilazione in streaming, parte delle API del servizio Adobe Experience Platform Data Ingestion.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 2%

---


# Trasmissione dei dati delle serie temporali ad Adobe Experience Platform

Questa esercitazione aiuterà a iniziare a utilizzare le API di assimilazione in streaming, parte delle API Adobe Experience Platform [!DNL Data Ingestion Service].

## Introduzione

Questa esercitazione richiede una buona conoscenza dei diversi servizi Adobe Experience Platform. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standard con cui  [!DNL Platform] organizzare i dati relativi all&#39;esperienza.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumo unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [Schema Guida](../../xdm/api/getting-started.md) per lo sviluppatore del Registro di sistema: Una guida completa che illustra tutti gli endpoint disponibili dell&#39; [!DNL Schema Registry] API e come effettuare chiamate a tali endpoint. Ciò include la conoscenza di `{TENANT_ID}`, che viene visualizzata nelle chiamate durante questa esercitazione, nonché la conoscenza di come creare schemi, che viene utilizzata per creare un dataset per l&#39;assimilazione.

Inoltre, questa esercitazione richiede che sia già stata creata una connessione in streaming. Per ulteriori informazioni sulla creazione di una connessione in streaming, leggere l&#39; [creazione di un&#39;esercitazione sulla connessione in streaming](./create-streaming-connection.md).

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API di assimilazione in streaming.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Comporre uno schema basato sulla classe ExperienceEvent XDM

Per creare un dataset, è innanzitutto necessario creare un nuovo schema che implementa la classe [!DNL XDM ExperienceEvent]. Per ulteriori informazioni sulla creazione di schemi, consultare la [Guida per gli sviluppatori API del Registro di sistema ](../../xdm/api/getting-started.md).

**Formato API**

```http
POST /schemaregistry/tenant/schemas
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce"
        },
        {  
         "$ref":"https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
        }
    ],
    "meta:immutableTags": [
        "union"
    ]
}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `title` | Nome da utilizzare per lo schema. Questo nome deve essere univoco. |
| `description` | Una descrizione significativa dello schema che si sta creando. |
| `meta:immutableTags` | In questo esempio, il tag `union` viene utilizzato per mantenere i dati in [[!DNL Real-time Customer Profile]](../../profile/home.md). |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli dello schema appena creato.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "{SCHEMA_VERSION}",
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent"
    ],
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "required": [
        "@id",
        "xdm:timestamp"
    ],
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/experienceevent",
        "https://ns.adobe.com/xdm/data/time-series",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "meta:registryMetadata": {
        "repo:createDate": 1551229957987,
        "repo:lastModifiedDate": 1551229957987,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:tenantNamespace": "{NAMESPACE}"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{TENANT_ID}` | Questo ID viene utilizzato per garantire che le risorse create siano correttamente denominate e contenute all’interno dell’organizzazione IMS. Per ulteriori informazioni sull&#39;ID tenant, leggere la guida del Registro di sistema [schema](../../xdm/api/getting-started.md#know-your-tenant-id). |

Prendete nota degli attributi `$id` e `version`, in quanto entrambi verranno utilizzati durante la creazione del set di dati.

## Impostare un descrittore di identità principale per lo schema

Quindi, aggiungere un [descrittore di identità](../../xdm/api/descriptors.md) allo schema creato sopra, utilizzando l&#39;attributo dell&#39;indirizzo e-mail di lavoro come identificatore principale. Ciò comporterà due modifiche:

1. L&#39;indirizzo e-mail di lavoro diventerà un campo obbligatorio. Ciò significa che i messaggi inviati senza questo campo non potranno essere convalidati e che non verranno trasferiti.

2. [!DNL Real-time Customer Profile] utilizzerà l&#39;indirizzo e-mail di lavoro come identificatore per unire più informazioni su quell&#39;individuo.

### Richiesta

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "@type":"xdm:descriptorIdentity",
    "xdm:sourceProperty":"/_experience/campaign/message/profileSnapshot/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | La `$id` ricevuta in precedenza quando si componeva lo schema. Dovrebbe assomigliare a questo: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;**Codici dello spazio dei nomi identità**
>
> Assicurarsi che i codici siano validi. Nell&#39;esempio precedente viene utilizzato &quot;email&quot;, che è uno spazio dei nomi di identità standard. Altri spazi dei nomi di identità standard comunemente utilizzati sono disponibili nelle [Domande frequenti su Servizio identità](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Per creare uno spazio nomi personalizzato, seguire i passaggi descritti nella [panoramica dello spazio nomi identità](../../identity-service/home.md).

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con informazioni sullo spazio dei nomi identità principale appena creato per lo schema.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/_experience/campaign/message/profileSnapshot/workEmail/address",
    "@id": "ec31c09e0906561861be5a71fcd964e29ebe7923b8eb0d1e",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{IMS_ORG}"
}
```

## Creare un dataset per i dati delle serie temporali

Una volta creato lo schema, sarà necessario creare un dataset per acquisire i dati del record.

>[!NOTE]
>
>Questo set di dati sarà abilitato per **[!DNL Real-time Customer Profile]** e **[!DNL Identity]** impostando i tag appropriati.

**Formato API**

```http
POST /catalog/dataSets
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
        "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 e un array contenente l&#39;ID del set di dati appena creato nel formato `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```

## Trasferimento dei dati delle serie temporali alla connessione in streaming

Con il set di dati e la connessione in streaming in posizione, è possibile assimilare record JSON in formato XDM per acquisire i dati delle serie temporali all&#39;interno di [!DNL Platform].

**Formato API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Il valore `id` della nuova connessione di streaming creata. |
| `synchronousValidation` | Un parametro di query facoltativo destinato allo sviluppo. Se impostato su `true`, può essere utilizzato per il feedback immediato per determinare se la richiesta è stata inviata correttamente. Per impostazione predefinita, questo valore è impostato su `false`. |

**Richiesta**

È possibile inserire i dati delle serie temporali in una connessione in streaming con o senza il nome di origine.

La richiesta di esempio riportata di seguito consente di inserire in Platform i dati delle serie temporali con un nome di origine mancante. Se ai dati manca il nome di origine, verrà aggiunto l&#39;ID di origine dalla definizione della connessione di streaming.

>[!NOTE]
>
>Sarà necessario generare le proprie `xdmEntity._id` e `xdmEntity.timestamp`. Per generare un ID è utile utilizzare un UUID. Inoltre, la seguente chiamata API **non** richiede intestazioni di autenticazione.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
            }
        },
        "xdmEntity":{
            "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": "2019-02-23T22:07:01Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            },
            "productListItems": [
                {
                    "SKU": "CC",
                    "name": "Fernie Snow",
                    "quantity": 30,
                    "priceTotal": 7.8
                }
            ],
            "commerce": {
                "productViews": {
                    "value": 1
                }
            },
            "_experience": {
                "campaign": {
                    "message": {
                        "profileSnapshot": {
                            "workEmail":{
                                "address": "janedoe@example.com"
                            }
                        }
                    }
                }
            }
        }
    }
}'
```

Se desiderate includere un nome di origine, l&#39;esempio seguente mostra come includerlo.

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli del nuovo streaming [!DNL Profile].

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "synchronousValidation": {
        "status": "pass"
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID della connessione di streaming creata in precedenza. |
| `xactionId` | Identificatore univoco generato sul lato server per il record appena inviato. Questo ID aiuta  Adobe a tracciare il ciclo di vita del record attraverso diversi sistemi e con il debug. |
| `receivedTimeMs`: Una marca temporale (epoch in millisecondi) che mostra l’ora in cui è stata ricevuta la richiesta. |
| `synchronousValidation.status` | Poiché il parametro di query `synchronousValidation=true` è stato aggiunto, questo valore viene visualizzato. Se la convalida ha esito positivo, lo stato sarà `pass`. |

## Recuperare i nuovi dati delle serie temporali acquisiti

Per convalidare i record acquisiti in precedenza, è possibile utilizzare il simbolo [[!DNL Profile Access API]](../../profile/api/entities.md) per recuperare i dati delle serie temporali. Questo può essere fatto utilizzando una richiesta di GET all&#39;endpoint `/access/entities` e utilizzando parametri di query facoltativi. Possono essere utilizzati più parametri, separati da e commerciale (&amp;).&quot;

>[!NOTE]
>
>Se l&#39;ID del criterio di unione non è definito e il `schema.name` o `relatedSchema.name` è `_xdm.context.profile`, [!DNL Profile Access] recupererà tutte le identità correlate **a5/>.**

**Formato API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Parametro | Descrizione |
| --------- | ----------- |
| `schema.name` | **Obbligatorio.** Nome dello schema a cui si accede. |
| `relatedSchema.name` | **Obbligatorio.** Poiché si sta effettuando l&#39;accesso a un  `_xdm.context.experienceevent`, questo valore specifica lo schema per l&#39;entità profilo a cui sono collegati gli eventi delle serie temporali. |
| `relatedEntityId` | L&#39;ID dell&#39;entità correlata. Se fornito, è necessario fornire anche lo spazio nomi entità. |
| `relatedEntityIdNS` | Spazio dei nomi dell’ID che si sta tentando di recuperare. |

**Richiesta**

```shell
curl -X GET \
  https://platform-stage.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli delle entità richieste. Come potete vedere, si tratta degli stessi dati delle serie temporali precedentemente acquisiti.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "9af5adcc-db9c-4692-b826-65d3abe68c22",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
            "entityId": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": 1582495621000,
            "entity": {
                "environment": {
                    "browserDetails": {
                        "javaScriptVersion": "1.6",
                        "cookiesEnabled": true,
                        "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
                        "acceptLanguage": "en-US",
                        "javaEnabled": true
                    },
                    "colorDepth": 32,
                    "viewportHeight": 799,
                    "viewportWidth": 414
                },
                "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Fernie Snow",
                        "quantity": 30,
                        "SKU": "CC",
                        "priceTotal": 7.8
                    }
                ],
                "_experience": {
                    "campaign": {
                        "message": {
                            "profileSnapshot": {
                                "workEmail": {
                                    "address": "janedoe@example.com"
                                }
                            }
                        }
                    }
                },
                "timestamp": "2020-02-23T22:07:01Z"
            },
            "lastModifiedAt": "2020-03-18T18:51:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Passaggi successivi

Leggendo questo documento, ora puoi capire come trasferire i dati dei record in [!DNL Platform] utilizzando le connessioni di streaming. Puoi provare a effettuare più chiamate con valori diversi e a recuperare i valori aggiornati. Inoltre, puoi iniziare a monitorare i dati acquisiti tramite l&#39;interfaccia utente [!DNL Platform]. Per ulteriori informazioni, consultare la [guida all&#39;inserimento dei dati di monitoraggio](../quality/monitor-data-ingestion.md).

Per ulteriori informazioni sull&#39;assimilazione in streaming in generale, leggere la [panoramica sull&#39;assimilazione in streaming](../streaming-ingestion/overview.md).
