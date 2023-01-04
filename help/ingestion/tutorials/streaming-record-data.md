---
keywords: Experience Platform;home;argomenti popolari;streaming ingestion;ingestion;record data;stream record data;
solution: Experience Platform
title: Trasmetti dati di record tramite le API Streaming Ingestion
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione ti aiuterà a iniziare a utilizzare le API Streaming Ingestion, parte delle API del servizio Adobe Experience Platform Data Ingestion.
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 3%

---


# Trasmetti i dati dei record utilizzando le API Streaming Ingestion

Questa esercitazione ti aiuterà a iniziare a utilizzare le API Streaming Ingestion, parte di Adobe Experience Platform [!DNL Data Ingestion Service] API.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei vari servizi Adobe Experience Platform. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati dell’esperienza.
   - [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/getting-started.md): Una guida completa che copre ciascuno degli endpoint disponibili [!DNL Schema Registry] API e modalità di effettuazione delle chiamate. Ciò include la conoscenza del `{TENANT_ID}`, che viene visualizzato nelle chiamate durante questa esercitazione, oltre a sapere come creare schemi, che viene utilizzato nella creazione di un set di dati per l’acquisizione.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../landing/api-guide.md).

## Componi uno schema basato su [!DNL XDM Individual Profile] Classe

Per creare un set di dati, devi innanzitutto creare un nuovo schema che implementi il [!DNL XDM Individual Profile] classe. Per ulteriori informazioni sulla creazione degli schemi, consulta la sezione [Guida per gli sviluppatori API del Registro di sistema dello schema](../../xdm/api/getting-started.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `meta:immutableTags` | In questo esempio, la `union` viene utilizzato per mantenere i dati in [[!DNL Real-Time Customer Profile]](../../profile/home.md). |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli del nuovo schema creato.

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
    "imsOrg": "{ORG_ID}",
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
| `{TENANT_ID}` | Questo ID viene utilizzato per garantire che le risorse create siano spaccate correttamente e contenute all’interno dell’organizzazione IMS. Per ulteriori informazioni sull’ID tenant, consulta la sezione [guida al registro di sistema dello schema](../../xdm/api/getting-started.md#know-your-tenant-id). |

Si prega di prendere nota del `$id` nonché `version` attributi, in quanto entrambi verranno utilizzati durante la creazione del set di dati.

## Imposta un descrittore di identità principale per lo schema

Quindi, aggiungi un [descrittore di identità](../../xdm/api/descriptors.md) allo schema creato in precedenza, utilizzando l’attributo dell’indirizzo e-mail di lavoro come identificatore principale. Ciò comporterà due modifiche:

1. L’indirizzo e-mail di lavoro diventerà un campo obbligatorio. Ciò significa che i messaggi inviati senza questo campo non possono essere convalidati e non verranno acquisiti.

2. [!DNL Real-Time Customer Profile] utilizzerà l&#39;indirizzo e-mail di lavoro come identificatore per unire più informazioni su quell&#39;individuo.

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
| `{SCHEMA_REF_ID}` | La `$id` ricevuto in precedenza al momento della composizione dello schema. Dovrebbe assomigliare a questo: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**Codici dello spazio dei nomi identità**
>
> Assicurati che i codici siano validi - l&#39;esempio precedente utilizza &quot;email&quot; che è uno spazio dei nomi di identità standard. Altri namespace di identità standard comunemente utilizzati si trovano all’interno di [Domande frequenti sul servizio Identity](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Per creare uno spazio dei nomi personalizzato, segui i passaggi descritti in [panoramica dello spazio dei nomi identità](../../identity-service/home.md).

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
    "imsOrg": "{ORG_ID}"
}
```

## Creare un set di dati per la registrazione dei dati

Una volta creato lo schema, dovrai creare un set di dati per acquisire i dati dei record.

>[!NOTE]
>
>Questo set di dati verrà abilitato per **[!DNL Real-Time Customer Profile]** e **[!DNL Identity Service]**.

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
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
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
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Creare una connessione in streaming

Dopo aver creato lo schema e il set di dati, puoi creare una connessione in streaming

Per ulteriori informazioni sulla creazione di una connessione in streaming, leggere il [creare un&#39;esercitazione sulla connessione in streaming](./create-streaming-connection.md).

## Inserire dati di record nella connessione streaming {#ingest-data}

Con il set di dati e la connessione in streaming in essere, è possibile acquisire record JSON in formato XDM per acquisire dati di record in [!DNL Platform].

**Formato API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | La `inletId` valore della connessione in streaming creata in precedenza. |
| `syncValidation` | Parametro di query facoltativo destinato a scopi di sviluppo. Se impostato su `true`, può essere utilizzato per un feedback immediato per determinare se la richiesta è stata inviata correttamente. Per impostazione predefinita, questo valore è impostato su `false`. Se imposti questo parametro di query su `true` che la richiesta sia limitata a 60 volte al minuto `CONNECTION_ID`. |

**Richiesta**

È possibile inserire i dati di record in una connessione streaming con o senza il nome sorgente.

La richiesta di esempio riportata di seguito acquisisce un record con un nome sorgente mancante in Platform. Se un record manca il nome sorgente, aggiungerà l’ID sorgente dalla definizione della connessione in streaming.

>[!NOTE]
>
>La seguente chiamata API **not** richiede eventuali intestazioni di autenticazione.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "flowId": "{FLOW_ID}",
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
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
| `{CONNECTION_ID}` | ID della connessione in streaming creata in precedenza. |
| `xactionId` | Un identificatore univoco generato lato server per il record appena inviato. Questo ID consente ad Adobe di tracciare il ciclo di vita di questo record attraverso vari sistemi e con il debug. |
| `receivedTimeMs` | Una marca temporale (epoch in millisecondi) che mostra a che ora è stata ricevuta la richiesta. |
| `syncValidation.status` | Dal parametro della query `syncValidation=true` è stato aggiunto, verrà visualizzato questo valore. Se la convalida ha avuto esito positivo, lo stato sarà `pass`. |

## Recupera i dati del record appena acquisito

Per convalidare i record precedentemente acquisiti, puoi utilizzare la funzione [[!DNL Profile Access API]](../../profile/api/entities.md) per recuperare i dati del record.

>[!NOTE]
>
>Se l&#39;ID del criterio di unione non è definito e il valore `schema.name` o `relatedSchema.name` è `_xdm.context.profile`, [!DNL Profile Access] recupererà **tutto** identità correlate.

**Formato API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Parametro | Descrizione |
| --------- | ----------- |
| `schema.name` | **Obbligatorio.** Nome dello schema a cui si accede. |
| `entityId` | ID dell’entità. Se fornito, è necessario fornire anche lo spazio dei nomi dell’entità. |
| `entityIdNS` | Spazio dei nomi dell&#39;ID che si sta tentando di recuperare. |

**Richiesta**

Puoi esaminare i dati dei record precedentemente acquisiti con la seguente richiesta di GET.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli delle entità richieste. Come puoi vedere, si tratta dello stesso record acquisito in precedenza con successo.

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

Leggendo questo documento, ora si capisce come inserire dati di record in [!DNL Platform] utilizzo di connessioni in streaming. Puoi provare a effettuare più chiamate con valori diversi e recuperare i valori aggiornati. Inoltre, puoi iniziare a monitorare i dati acquisiti tramite [!DNL Platform] Interfaccia utente. Per ulteriori informazioni, leggere il [monitoraggio dell’acquisizione dei dati](../quality/monitor-data-ingestion.md) guida.

Per ulteriori informazioni sull’acquisizione in streaming in generale, consulta la sezione [panoramica sull’acquisizione in streaming](../streaming-ingestion/overview.md).
