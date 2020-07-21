---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Streaming dei dati dei record
topic: tutorial
translation-type: tm+mt
source-git-commit: 6a371aab5435bac97f714e5cf96a93adf4aa0303
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 2%

---


# Trasferisci dati record a  Adobe Experience Platform

Questa esercitazione ti aiuterà a iniziare a utilizzare le API di assimilazione in streaming, parte delle API del servizio di inserimento dati del Adobe Experience Platform .

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei vari servizi  Adobe Experience Platform. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Experience Data Model (XDM)](../../xdm/home.md): Framework standard con cui Platform organizza i dati relativi all&#39;esperienza.
- [Profilo](../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [Schema Guida](../../xdm/api/getting-started.md)per lo sviluppatore del Registro di sistema: Una guida completa che illustra tutti gli endpoint disponibili dell&#39;API del Registro di sistema dello schema e come effettuare chiamate a tali endpoint. Ciò include la conoscenza `{TENANT_ID}`dell&#39;utente, che viene visualizzata nelle chiamate durante questa esercitazione, nonché la conoscenza di come creare gli schemi, che viene utilizzata per creare un set di dati per l&#39;assimilazione.

Inoltre, questa esercitazione richiede che sia già stata creata una connessione in streaming. Per ulteriori informazioni sulla creazione di una connessione in streaming, consulta l’esercitazione sulla [creazione di una connessione in streaming](./create-streaming-connection.md).

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API di assimilazione in streaming.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API Platform, è prima necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Componi uno schema basato sulla classe Profilo singolo XDM

Per creare un set di dati, è innanzitutto necessario creare un nuovo schema che implementa la classe di profilo singolo XDM. Per ulteriori informazioni sulla creazione degli schemi, consultare la guida [per gli sviluppatori API del Registro di](../../xdm/api/getting-started.md)schema.

**Formato API**

```http
POST /schemaregistry/tenant/schemas
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
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
| `meta:immutableTags` | In questo esempio, il `union` tag viene utilizzato per mantenere i dati nel profilo [cliente in tempo](../../profile/home.md)reale. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli dello schema appena creato.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/cpmtext/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:immutableTags": [
        "union"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createDate": 1551376506996,
        "repo:lastModifiedDate": 1551376506996,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{TENANT_ID}` | Questo ID viene utilizzato per garantire che le risorse create siano correttamente denominate e contenute all’interno dell’organizzazione IMS. Per ulteriori informazioni sull&#39;ID tenant, consultare la guida [al Registro di sistema](../../xdm/api/getting-started.md#know-your-tenant-id)dello schema. |

Prendete nota `$id` e degli `version` attributi, in quanto entrambi verranno utilizzati per la creazione del set di dati.

## Impostare un descrittore di identità principale per lo schema

Quindi, aggiungere un descrittore [di](../../xdm/api/descriptors.md) identità allo schema creato sopra, utilizzando l&#39;attributo indirizzo e-mail di lavoro come identificatore principale. Ciò comporterà due modifiche:

1. L&#39;indirizzo e-mail di lavoro diventerà un campo obbligatorio. Ciò significa che i messaggi inviati senza questo campo non potranno essere convalidati e che non verranno trasferiti.

2. Il profilo cliente in tempo reale utilizzerà l&#39;indirizzo e-mail di lavoro come identificatore per unire più informazioni su quell&#39;individuo.

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
    "xdm:sourceProperty":"/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | L&#39;oggetto `$id` ricevuto in precedenza al momento della composizione dello schema. Dovrebbe assomigliare a questo: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; codici dei nomi di identità &#x200B;****
>
> Assicurarsi che i codici siano validi. Nell&#39;esempio precedente viene utilizzato &quot;email&quot;, che è uno spazio dei nomi di identità standard. Altri spazi dei nomi di identità standard comunemente utilizzati si trovano nelle domande frequenti relative al servizio [identità](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Se desiderate creare uno spazio nomi personalizzato, seguite i passaggi descritti nella panoramica [dello spazio nomi](../../identity-service/home.md)identità.

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con informazioni sul descrittore di identità principale appena creato per lo schema.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/workEmail/address",
    "@id": "17aaebfa382ce8fc0a40d3e43870b6470aab894e1c368d16",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{IMS_ORG}"
}
```

## Creazione di un dataset per i dati dei record

Una volta creato lo schema, sarà necessario creare un dataset per acquisire i dati del record.

>[!NOTE]
>
>Questo set di dati sarà abilitato per il profilo **cliente e il servizio** di **identità in tempo** reale.

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
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1.0"
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
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Invio di dati di record alla connessione di streaming

Con il set di dati e la connessione in streaming in posizione, è possibile assimilare record JSON in formato XDM per trasferire dati di record in Platform.

**Formato API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Il `id` valore della connessione di streaming creata in precedenza. |
| `synchronousValidation` | Un parametro di query facoltativo destinato allo sviluppo. Se impostato su `true`, può essere utilizzato per il feedback immediato per determinare se la richiesta è stata inviata correttamente. Per impostazione predefinita, questo valore è impostato su `false`. |

**Richiesta**

>[!NOTE]
>
>La seguente chiamata API **non** richiede intestazioni di autenticazione.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
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
        "xdmEntity": {
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                },
                "birthDate": "1969-03-14",
                "gender": "female"
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "type": "work",
                "status": "active"
            }
        }
    }
}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli del nuovo profilo in streaming.

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
| `xactionId` | Identificatore univoco generato sul lato server per il record appena inviato. Questo ID aiuta Adobe a tenere traccia del ciclo di vita di questo record attraverso diversi sistemi e con il debug. |
| `receivedTimeMs` | Una marca temporale (epoch in millisecondi) che mostra l’ora in cui è stata ricevuta la richiesta. |
| `synchronousValidation.status` | Poiché il parametro query `synchronousValidation=true` è stato aggiunto, questo valore verrà visualizzato. Se la convalida ha esito positivo, lo stato sarà `pass`. |

## Recuperare i dati del nuovo record acquisito

Per convalidare i record precedentemente acquisiti, potete utilizzare l&#39;API [Accesso](../../profile/api/entities.md) profilo per recuperare i dati del record.

>[!NOTE]
>
>Se l&#39;ID del criterio di unione non è definito e lo schema.</span>name or relatedSchema</span>.name is `_xdm.context.profile`, Profile Access recupererà **tutte** le identità correlate.

**Formato API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Parametro | Descrizione |
| --------- | ----------- |
| `schema.name` | **Obbligatorio.** Nome dello schema a cui si accede. |
| `entityId` | L&#39;ID dell&#39;entità. Se fornito, è necessario fornire anche lo spazio nomi entità. |
| `entityIdNS` | Spazio dei nomi dell’ID che si sta tentando di recuperare. |

**Richiesta**

Puoi esaminare i dati del record precedentemente acquisiti con la seguente richiesta GET.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli delle entità richieste. Come potete vedere, si tratta dello stesso record che è stato acquisito con successo in precedenza.

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "mergePolicy": {
            "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56"
        },
        "sources": [
            "5e30d7986c0cc218a85cee65"
        ],
        "tags": [
            "1580346827274:2478:215"
        ],
        "identityGraph": [
            "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA"
        ],
        "entity": {
            "person": {
                "name": {
                    "lastName": "Doe",
                    "middleName": "F",
                    "firstName": "Jane"
                },
                "gender": "female",
                "birthDate": "1969-03-14"
            },
            "workEmail": {
                "type": "work",
                "address": "janedoe@example.com",
                "status": "active",
                "primary": true
            },
            "identityMap": {
                "email": [
                    {
                        "id": "janedoe@example.com"
                    }
                ]
            }
        },
        "lastModifiedAt": "2020-01-30T01:13:59Z"
    }
}
```

## Passaggi successivi

Leggendo questo documento, ora puoi capire come trasferire dati di record in Platform utilizzando le connessioni di streaming. Puoi provare a effettuare più chiamate con valori diversi e a recuperare i valori aggiornati. È inoltre possibile iniziare a monitorare i dati acquisiti tramite l’interfaccia utente di Platform. Per ulteriori informazioni, consulta la guida all’inserimento dei dati di [monitoraggio](../quality/monitor-data-flows.md) .

Per ulteriori informazioni sull’assimilazione in streaming in generale, consultate la panoramica sull’assimilazione in [streaming](../streaming-ingestion/overview.md).


