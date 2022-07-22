---
keywords: Experience Platform;home;argomenti popolari;acquisizione streaming;acquisizione;dati sulle serie temporali;dati sulle serie temporali in streaming;
solution: Experience Platform
title: Trasmetti dati serie temporale tramite API Streaming Ingestion
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione ti aiuterà a iniziare a utilizzare le API Streaming Ingestion, parte delle API del servizio Adobe Experience Platform Data Ingestion.
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
source-git-commit: cedc53b78ea8eb8f3e93178b60ebe49b90c11650
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 2%

---

# Trasmetti dati della serie temporale utilizzando le API Streaming Ingestion

Questa esercitazione ti aiuterà a iniziare a utilizzare le API Streaming Ingestion, parte di Adobe Experience Platform [!DNL Data Ingestion Service] API.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei vari servizi Adobe Experience Platform. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati dell’esperienza.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/getting-started.md): Una guida completa che copre ciascuno degli endpoint disponibili [!DNL Schema Registry] API e modalità di effettuazione delle chiamate. Ciò include la conoscenza del `{TENANT_ID}`, che viene visualizzato nelle chiamate durante questa esercitazione, oltre a sapere come creare schemi, che viene utilizzato nella creazione di un set di dati per l’acquisizione.

Inoltre, questa esercitazione richiede che sia già stata creata una connessione in streaming. Per ulteriori informazioni sulla creazione di una connessione in streaming, leggere il [creare un&#39;esercitazione sulla connessione in streaming](./create-streaming-connection.md).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../landing/api-guide.md).

## Componi uno schema basato sulla classe ExperienceEvent XDM

Per creare un set di dati, devi innanzitutto creare un nuovo schema che implementi il [!DNL XDM ExperienceEvent] classe. Per ulteriori informazioni sulla creazione degli schemi, consulta la sezione [Guida per gli sviluppatori API del Registro di sistema dello schema](../../xdm/api/getting-started.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `meta:immutableTags` | In questo esempio, la `union` viene utilizzato per mantenere i dati in [[!DNL Real-time Customer Profile]](../../profile/home.md). |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli del nuovo schema creato.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1",
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
    "imsOrg": "{ORG_ID}",
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
    "imsOrg": "{ORG_ID}",
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
| `{TENANT_ID}` | Questo ID viene utilizzato per garantire che le risorse create siano spaccate correttamente e contenute all’interno dell’organizzazione IMS. Per ulteriori informazioni sull’ID tenant, consulta la sezione [guida al registro di sistema dello schema](../../xdm/api/getting-started.md#know-your-tenant-id). |

Si prega di prendere nota del `$id` nonché `version` attributi, in quanto entrambi verranno utilizzati durante la creazione del set di dati.

## Imposta un descrittore di identità principale per lo schema

Quindi, aggiungi un [descrittore di identità](../../xdm/api/descriptors.md) allo schema creato in precedenza, utilizzando l’attributo dell’indirizzo e-mail di lavoro come identificatore principale. Ciò comporterà due modifiche:

1. L’indirizzo e-mail di lavoro diventerà un campo obbligatorio. Ciò significa che i messaggi inviati senza questo campo non possono essere convalidati e non verranno acquisiti.

2. [!DNL Real-time Customer Profile] utilizzerà l&#39;indirizzo e-mail di lavoro come identificatore per unire più informazioni su quell&#39;individuo.

### Richiesta

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `{SCHEMA_REF_ID}` | La `$id` ricevuto in precedenza al momento della composizione dello schema. Dovrebbe assomigliare a questo: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;**Codici dello spazio dei nomi identità**
>
> Assicurati che i codici siano validi - l&#39;esempio precedente utilizza &quot;email&quot; che è uno spazio dei nomi di identità standard. Altri namespace di identità standard comunemente utilizzati si trovano all’interno di [Domande frequenti sul servizio Identity](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Per creare uno spazio dei nomi personalizzato, segui i passaggi descritti in [panoramica dello spazio dei nomi identità](../../identity-service/home.md).

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con informazioni sullo spazio dei nomi di identità principale appena creato per lo schema.

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
    "imsOrg": "{ORG_ID}"
}
```

## Creare un set di dati per i dati delle serie temporali

Una volta creato lo schema, dovrai creare un set di dati per acquisire i dati dei record.

>[!NOTE]
>
>Questo set di dati verrà abilitato per **[!DNL Real-time Customer Profile]** e **[!DNL Identity]** impostando i tag appropriati.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
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


## Creare una connessione in streaming

Dopo aver creato lo schema e il set di dati, dovrai creare una connessione in streaming per acquisire i dati.

Per ulteriori informazioni sulla creazione di una connessione in streaming, leggere il [creare un&#39;esercitazione sulla connessione in streaming](./create-streaming-connection.md).

## Inserire dati della serie temporale nella connessione streaming

Con il set di dati, la connessione in streaming e il flusso di dati creati, puoi acquisire record JSON in formato XDM per acquisire dati di serie temporali all’interno di [!DNL Platform].

**Formato API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | La `id` valore della nuova connessione in streaming. |
| `syncValidation` | Parametro di query facoltativo destinato a scopi di sviluppo. Se impostato su `true`, può essere utilizzato per un feedback immediato per determinare se la richiesta è stata inviata correttamente. Per impostazione predefinita, questo valore è impostato su `false`. Se imposti questo parametro di query su `true` che la richiesta sia limitata a 60 volte al minuto `CONNECTION_ID`. |

**Richiesta**

È possibile inserire dati di serie temporali in una connessione streaming con o senza il nome sorgente.

La richiesta di esempio riportata di seguito acquisisce i dati delle serie temporali con un nome sorgente mancante in Platform. Se ai dati manca il nome sorgente, aggiungerà l’ID sorgente dalla definizione della connessione in streaming.

Entrambi `xdmEntity._id` e `xdmEntity.timestamp` sono campi obbligatori per i dati relativi alle serie temporali. La `xdmEntity._id` l&#39;attributo rappresenta un identificatore univoco per il record stesso, **not** un ID univoco della persona o del dispositivo di cui è il record.

Sarà necessario generare il proprio `xdmEntity._id` e `xdmEntity.timestamp` per il record in modo che rimanga coerente se il record dovesse essere riacquisito. Idealmente, il sistema di origine conterrà questi valori. Se un ID non è disponibile, considera la concatenazione di valori di altri campi nel record per creare un valore univoco che può essere rigenerato in modo coerente dal record al momento della riacquisizione.

>[!NOTE]
>
>La seguente chiamata API **not** richiede eventuali intestazioni di autenticazione.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "flowId": "{FLOW_ID}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            },
        "identityMap": {
                "Email": [
                  {
                    "id": "acme_user@gmail.com",
                    "primary": true
                  }
                ]
              },
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

Per includere un nome di origine, nell&#39;esempio seguente viene illustrato come includerlo.

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
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
    "syncValidation": {
        "status": "pass"
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{CONNECTION_ID}` | La `inletId` della connessione in streaming creata in precedenza. |
| `xactionId` | Un identificatore univoco generato lato server per il record appena inviato. Questo ID consente ad Adobe di tracciare il ciclo di vita di questo record attraverso vari sistemi e con il debug. |
| `receivedTimeMs`: Una marca temporale (epoch in millisecondi) che mostra a che ora è stata ricevuta la richiesta. |
| `syncValidation.status` | Dal parametro della query `syncValidation=true` è stato aggiunto, verrà visualizzato questo valore. Se la convalida ha avuto esito positivo, lo stato sarà `pass`. |

## Recupera i nuovi dati della serie temporale acquisiti

Per convalidare i record precedentemente acquisiti, puoi utilizzare la funzione [[!DNL Profile Access API]](../../profile/api/entities.md) per recuperare i dati delle serie temporali. Questa operazione può essere eseguita utilizzando una richiesta GET al `/access/entities` e utilizzando parametri di query facoltativi. È possibile utilizzare più parametri, separati da e commerciale (&amp;).&quot;

>[!NOTE]
>
>Se l&#39;ID del criterio di unione non è definito e il valore `schema.name` o `relatedSchema.name` è `_xdm.context.profile`, [!DNL Profile Access] recupererà **tutto** identità correlate.

**Formato API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Parametro | Descrizione |
| --------- | ----------- |
| `schema.name` | **Obbligatorio.** Nome dello schema a cui si accede. |
| `relatedSchema.name` | **Obbligatorio.** Poiché si accede a un `_xdm.context.experienceevent`, questo valore specifica lo schema per l&#39;entità profilo a cui sono correlati gli eventi delle serie temporali. |
| `relatedEntityId` | ID dell’entità correlata. Se fornito, è necessario fornire anche lo spazio dei nomi dell’entità. |
| `relatedEntityIdNS` | Spazio dei nomi dell&#39;ID che si sta tentando di recuperare. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli delle entità richieste. Come puoi vedere, si tratta degli stessi dati della serie temporale precedentemente acquisiti.

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

Leggendo questo documento, ora si capisce come inserire dati di record in [!DNL Platform] utilizzo di connessioni in streaming. Puoi provare a effettuare più chiamate con valori diversi e recuperare i valori aggiornati. Inoltre, puoi iniziare a monitorare i dati acquisiti tramite [!DNL Platform] Interfaccia utente. Per ulteriori informazioni, leggere il [monitoraggio dell’acquisizione dei dati](../quality/monitor-data-ingestion.md) guida.

Per ulteriori informazioni sull’acquisizione in streaming in generale, consulta la sezione [panoramica sull’acquisizione in streaming](../streaming-ingestion/overview.md).
