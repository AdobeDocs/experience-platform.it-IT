---
keywords: Experience Platform;home;argomenti popolari;acquisizione streaming;acquisizione;dati di record;dati di record di flusso;
solution: Experience Platform
title: Trasmetti dati di record tramite le API Streaming Ingestion
topic: tutorial
type: Tutorial
description: Questa esercitazione ti aiuterà a iniziare a utilizzare le API Streaming Ingestion, parte delle API di Adobe Experience Platform Data Ingestion Service.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 2%

---


# Trasmetti i dati dei record utilizzando le API Streaming Ingestion

Questa esercitazione ti aiuterà a iniziare a utilizzare le API Streaming Ingestion, parte delle API di Adobe Experience Platform [!DNL Data Ingestion Service].

## Introduzione

Questa esercitazione richiede una buona conoscenza dei vari servizi Adobe Experience Platform. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato tramite il quale  [!DNL Platform] organizza i dati relativi alle esperienze.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [Guida](../../xdm/api/getting-started.md) per gli sviluppatori del Registro di schema: Una guida completa che descrive ciascuno degli endpoint disponibili dell’ [!DNL Schema Registry] API e come effettuare chiamate a tali endpoint. Ciò include la conoscenza del `{TENANT_ID}`, visualizzato nelle chiamate durante questa esercitazione, e la conoscenza di come creare schemi, che viene utilizzato nella creazione di un set di dati per l’acquisizione.

Inoltre, questa esercitazione richiede che sia già stata creata una connessione in streaming. Per ulteriori informazioni sulla creazione di una connessione in streaming, leggi l&#39; [esercitazione sulla connessione in streaming](./create-streaming-connection.md).

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per effettuare correttamente le chiamate alle API di acquisizione in streaming.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- nome x-sandbox: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

## Componi uno schema basato sulla classe [!DNL XDM Individual Profile]

Per creare un set di dati, devi innanzitutto creare un nuovo schema che implementi la classe [!DNL XDM Individual Profile] . Per ulteriori informazioni sulla creazione degli schemi, consulta la [Guida per gli sviluppatori API del Registro di sistema ](../../xdm/api/getting-started.md).

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
| `meta:immutableTags` | In questo esempio, il tag `union` viene utilizzato per mantenere i dati in [[!DNL Real-time Customer Profile]](../../profile/home.md). |

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
| `{TENANT_ID}` | Questo ID viene utilizzato per garantire che le risorse create siano spaccate correttamente e contenute all’interno dell’organizzazione IMS. Per ulteriori informazioni sull&#39;ID tenant, consulta la [guida del Registro di sistema dello schema](../../xdm/api/getting-started.md#know-your-tenant-id). |

Prendi nota degli attributi `$id` e `version`, in quanto entrambi verranno utilizzati durante la creazione del set di dati.

## Imposta un descrittore di identità principale per lo schema

Quindi, aggiungi un [descrittore di identità](../../xdm/api/descriptors.md) allo schema creato sopra, utilizzando l&#39;attributo dell&#39;indirizzo e-mail di lavoro come identificatore principale. Ciò comporterà due modifiche:

1. L’indirizzo e-mail di lavoro diventerà un campo obbligatorio. Ciò significa che i messaggi inviati senza questo campo non possono essere convalidati e non verranno acquisiti.

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
| `{SCHEMA_REF_ID}` | Il `$id` ricevuto in precedenza al momento della composizione dello schema. Dovrebbe assomigliare a questo: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**Codici dello spazio dei nomi identità**
>
> Assicurati che i codici siano validi - l&#39;esempio precedente utilizza &quot;email&quot; che è uno spazio dei nomi di identità standard. Altri namespace di identità standard comunemente utilizzati si trovano nelle [Domande frequenti sul servizio Identity](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Per creare uno spazio dei nomi personalizzato, segui i passaggi descritti nella [panoramica dello spazio dei nomi di identità](../../identity-service/home.md).

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

## Creare un set di dati per la registrazione dei dati

Una volta creato lo schema, dovrai creare un set di dati per acquisire i dati dei record.

>[!NOTE]
>
>Questo set di dati verrà abilitato per **[!DNL Real-time Customer Profile]** e **[!DNL Identity Service]**.

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

## Inserire dati di record nella connessione streaming {#ingest-data}

Con il set di dati e la connessione in streaming attivo, puoi acquisire record JSON in formato XDM per acquisire dati di record in [!DNL Platform].

**Formato API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Il valore `id` della connessione streaming creata in precedenza. |
| `synchronousValidation` | Parametro di query facoltativo destinato a scopi di sviluppo. Se impostato su `true`, può essere utilizzato per un feedback immediato per determinare se la richiesta è stata inviata correttamente. Per impostazione predefinita, questo valore è impostato su `false`. |

**Richiesta**

È possibile inserire i dati di record in una connessione streaming con o senza il nome sorgente.

La richiesta di esempio riportata di seguito acquisisce un record con un nome sorgente mancante in Platform. Se un record manca il nome sorgente, aggiungerà l’ID sorgente dalla definizione della connessione in streaming.

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

Per includere un nome di origine, nell&#39;esempio seguente viene illustrato come includerlo.

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
| `{CONNECTION_ID}` | ID della connessione in streaming creata in precedenza. |
| `xactionId` | Un identificatore univoco generato lato server per il record appena inviato. Questo ID consente ad Adobe di tracciare il ciclo di vita di questo record attraverso vari sistemi e con il debug. |
| `receivedTimeMs` | Una marca temporale (epoch in millisecondi) che mostra a che ora è stata ricevuta la richiesta. |
| `synchronousValidation.status` | Poiché è stato aggiunto il parametro di query `synchronousValidation=true`, questo valore viene visualizzato. Se la convalida è riuscita, lo stato sarà `pass`. |

## Recupera i dati del record appena acquisito

Per convalidare i record precedentemente acquisiti, puoi utilizzare [[!DNL Profile Access API]](../../profile/api/entities.md) per recuperare i dati del record.

>[!NOTE]
>
>Se l&#39;ID del criterio di unione non è definito e il `schema.name` o `relatedSchema.name` è `_xdm.context.profile`, [!DNL Profile Access] recupererà le identità correlate **all**.

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

È possibile esaminare i dati dei record precedentemente acquisiti con la seguente richiesta GET.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Leggendo questo documento, ora puoi imparare a inserire dati di record in [!DNL Platform] utilizzando le connessioni di streaming. Puoi provare a effettuare più chiamate con valori diversi e recuperare i valori aggiornati. Inoltre, puoi iniziare a monitorare i dati acquisiti tramite l’ [!DNL Platform] interfaccia utente. Per ulteriori informazioni, consulta la guida [monitoring data ingestion](../quality/monitor-data-ingestion.md) .

Per ulteriori informazioni sull&#39;acquisizione in streaming in generale, consulta la [panoramica sull&#39;acquisizione in streaming](../streaming-ingestion/overview.md).


