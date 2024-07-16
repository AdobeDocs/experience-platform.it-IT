---
keywords: Experience Platform;home;argomenti popolari;streaming ingestion;acquisizione;dati record;stream record data;
solution: Experience Platform
title: Trasmettere i dati dei record utilizzando le API Streaming Ingestion
type: Tutorial
description: Questa esercitazione ti aiuterà a iniziare a utilizzare le API Streaming Ingestion, che fanno parte delle API Adobe Experience Platform Data Ingestion Service.
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 3%

---


# Trasmettere i dati dei record utilizzando le API Streaming Ingestion

Questo tutorial ti aiuterà a iniziare a utilizzare le API Streaming Ingestion, parte delle API Adobe Experience Platform [!DNL Data Ingestion Service].

## Introduzione

Questo tutorial richiede una conoscenza operativa di vari servizi Adobe Experience Platform. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati dell&#39;esperienza.
   - [Guida per gli sviluppatori del Registro di schema](../../xdm/api/getting-started.md): guida completa che descrive ogni endpoint disponibile dell&#39;API [!DNL Schema Registry] e spiega come effettuare chiamate a tali endpoint. Ciò include la conoscenza di `{TENANT_ID}`, che viene visualizzato nelle chiamate in tutto questo tutorial, e di come creare schemi, utilizzati nella creazione di un set di dati per l’acquisizione.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato in tempo reale basato su dati aggregati provenienti da più origini.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../landing/api-guide.md).

## Componi uno schema basato sulla classe [!DNL XDM Individual Profile]

Per creare un set di dati, è innanzitutto necessario creare un nuovo schema che implementi la classe [!DNL XDM Individual Profile]. Per ulteriori informazioni su come creare schemi, leggere la [Guida per gli sviluppatori API del registro degli schemi](../../xdm/api/getting-started.md).

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
| `description` | Descrizione significativa dello schema che si sta creando. |
| `meta:immutableTags` | In questo esempio, il tag `union` viene utilizzato per mantenere i dati in [[!DNL Real-Time Customer Profile]](../../profile/home.md). |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 con i dettagli dello schema appena creato.

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
| `{TENANT_ID}` | Questo ID viene utilizzato per garantire che le risorse create abbiano uno spazio dei nomi corretto e siano contenute all’interno dell’organizzazione. Per ulteriori informazioni sull&#39;ID tenant, leggere la [guida del Registro di sistema dello schema](../../xdm/api/getting-started.md#know-your-tenant-id). |

Prendere nota degli attributi `$id` e `version`, poiché entrambi verranno utilizzati durante la creazione del set di dati.

## Impostare un descrittore di identità primaria per lo schema

Quindi, aggiungi un [descrittore di identità](../../xdm/api/descriptors.md) allo schema creato in precedenza, utilizzando l&#39;attributo dell&#39;indirizzo e-mail di lavoro come identificatore primario. Questa operazione comporterà due modifiche:

1. L’indirizzo e-mail aziendale diventerà un campo obbligatorio. Ciò significa che i messaggi inviati senza questo campo non supereranno la convalida e non verranno acquisiti.

2. [!DNL Real-Time Customer Profile] utilizzerà l&#39;indirizzo e-mail di lavoro come identificatore per unire più informazioni sull&#39;utente.

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
| `{SCHEMA_REF_ID}` | `$id` precedentemente ricevuti durante la composizione dello schema. Deve essere simile al seguente: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**Codici spazio dei nomi identità**
>
> Verifica che i codici siano validi. Nell’esempio precedente viene utilizzato &quot;e-mail&quot;, che è uno spazio dei nomi di identità standard. Altri spazi dei nomi di identità standard comunemente utilizzati si trovano nelle [Domande frequenti sul servizio Identity](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Se desideri creare uno spazio dei nomi personalizzato, segui i passaggi descritti nella [panoramica dello spazio dei nomi delle identità](../../identity-service/home.md).

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 con informazioni sul descrittore di identità primaria appena creato per lo schema.

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

## Creare un set di dati per i dati del record

Dopo aver creato lo schema, dovrai creare un set di dati per acquisire i dati del record.

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 e un array contenente l’ID del set di dati appena creato in formato `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Creare una connessione in streaming

Dopo aver creato lo schema e il set di dati, puoi creare una connessione in streaming

Per ulteriori informazioni sulla creazione di una connessione in streaming, leggere l&#39;esercitazione [creare una connessione in streaming](./create-streaming-connection.md).

## Acquisire dati di record nella connessione streaming {#ingest-data}

Con il set di dati e la connessione in streaming attivi, puoi acquisire record JSON formattati XDM per acquisire i dati dei record in [!DNL Platform].

**Formato API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Il valore `inletId` della connessione streaming creata in precedenza. |
| `syncValidation` | Parametro di query facoltativo destinato allo sviluppo. Se è impostato su `true`, può essere utilizzato per un feedback immediato per determinare se la richiesta è stata inviata correttamente. Per impostazione predefinita, questo valore è impostato su `false`. Tieni presente che se imposti questo parametro di query su `true`, la frequenza della richiesta sarà limitata a 60 volte al minuto per `CONNECTION_ID`. |

**Richiesta**

L’inserimento di dati record in una connessione in streaming può essere eseguito con o senza il nome dell’origine.

L’esempio di richiesta seguente acquisisce in Platform un record con un nome di origine mancante. Se a un record manca il nome dell’origine, questo aggiungerà l’ID di origine dalla definizione della connessione in streaming.

>[!NOTE]
>
>La seguente chiamata API **not** richiede intestazioni di autenticazione.

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

Se si desidera includere un nome di origine, nell&#39;esempio seguente viene illustrato come includerlo.

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del nuovo flusso [!DNL Profile].

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
| `xactionId` | Un identificatore univoco generato lato server per il record appena inviato. Questo ID aiuta gli Adobi a tracciare il ciclo di vita di questo record attraverso vari sistemi e con il debug. |
| `receivedTimeMs` | Un timestamp (epoca in millisecondi) che mostra l’ora in cui è stata ricevuta la richiesta. |
| `syncValidation.status` | Poiché è stato aggiunto il parametro di query `syncValidation=true`, verrà visualizzato questo valore. Se la convalida ha esito positivo, lo stato sarà `pass`. |

## Recupera i dati del record appena acquisiti

Per convalidare i record acquisiti in precedenza, è possibile utilizzare [[!DNL Profile Access API]](../../profile/api/entities.md) per recuperare i dati del record.

>[!NOTE]
>
>Se l&#39;ID del criterio di unione non è definito e `schema.name` o `relatedSchema.name` è `_xdm.context.profile`, [!DNL Profile Access] recupererà **tutte** le identità correlate.

**Formato API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Parametro | Descrizione |
| --------- | ----------- |
| `schema.name` | **Obbligatorio.** Nome dello schema a cui si sta effettuando l&#39;accesso. |
| `entityId` | ID dell’entità. Se fornito, devi anche fornire lo spazio dei nomi delle entità. |
| `entityIdNS` | Lo spazio dei nomi dell’ID che stai tentando di recuperare. |

**Richiesta**

Puoi rivedere i dati dei record acquisiti in precedenza con la seguente richiesta GET.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli delle entità richieste. Come puoi vedere, si tratta dello stesso record che è stato acquisito correttamente in precedenza.

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

Dopo aver letto questo documento, sarai in grado di acquisire i dati dei record in [!DNL Platform] utilizzando connessioni in streaming. Puoi provare a effettuare più chiamate con valori diversi e a recuperare i valori aggiornati. Inoltre, puoi iniziare a monitorare i dati acquisiti tramite l&#39;interfaccia utente [!DNL Platform]. Per ulteriori informazioni, consulta la [guida al monitoraggio dell&#39;acquisizione dei dati](../quality/monitor-data-ingestion.md).

Per ulteriori informazioni sull&#39;acquisizione in streaming in generale, consulta la [panoramica sull&#39;acquisizione in streaming](../streaming-ingestion/overview.md).
