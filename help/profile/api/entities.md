---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API entità (accesso profilo)
type: Documentation
description: Adobe Experience Platform consente di accedere ai dati del profilo cliente in tempo reale utilizzando le API RESTful o l’interfaccia utente di. Questa guida illustra come accedere alle entità, più comunemente note come "profili", utilizzando l’API di profilo.
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 2%

---

# Endpoint entità (accesso profilo)

Adobe Experience Platform consente di accedere a [!DNL Real-Time Customer Profile] dati utilizzando le API RESTful o l’interfaccia utente di. Questa guida illustra come accedere alle entità, più comunemente note come &quot;profili&quot;, utilizzando l’API. Per ulteriori informazioni sull’accesso ai profili tramite il [!DNL Platform] Interfaccia utente, fare riferimento a [Guida utente del profilo](../ui/user-guide.md).

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Prima di continuare, controlla [guida introduttiva](getting-started.md) per collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a [!DNL Experience Platform] API.

## Accedere ai dati del profilo per identità

È possibile accedere a un [!DNL Profile] effettuando una richiesta GET al `/access/entities` e fornendo l’identità dell’entità sotto forma di serie di parametri di query. Questa identità è costituita da un valore ID (`entityId`) e lo spazio dei nomi dell’identità (`entityIdNS`).

I parametri di query forniti nel percorso della richiesta specificano a quali dati accedere. Puoi includere più parametri, separati da e commerciali (&amp;). Un elenco completo dei parametri validi è fornito in [parametri di query](#query-parameters) sezione dell&#39;appendice.

**Formato API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Richiesta**

La richiesta seguente recupera l’e-mail e il nome di un cliente utilizzando un’identità:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

>[!NOTE]
>
>Se un grafico correlato collega più di 50 identità, questo servizio restituirà lo stato HTTP 422 e il messaggio &quot;Troppe identità correlate&quot;. Se ricevi questo errore, puoi aggiungere altri parametri di query per restringere la ricerca.

## Accedere ai dati del profilo per elenco di identità

Per accedere a più entità profilo in base alle loro identità, devi effettuare una richiesta POST al `/access/entities` e fornendo le identità nel payload. Queste identità sono costituite da un valore ID (`entityId`) e uno spazio dei nomi delle identità (`entityIdNS`).

**Formato API**

```http
POST /access/entities
```

**Richiesta**

La richiesta seguente recupera i nomi e gli indirizzi e-mail di diversi clienti da un elenco di identità:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.profile"
        },
        "fields":[
            "identities",
            "person.name",
            "workEmail"
        ],
        "identities":[
            {
                "entityId":"89149270342662559642753730269986316601",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316900",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316602",
                "entityIdNS":{
                    "code":"ECID"
                }
            }
        ],
        "timeFilter": {
            "startTime": 1539838505,
            "endTime": 1539838510
        },
        "limit": 10,
        "orderby": "-timestamp",
        "withCA": true
      }'
```

| Proprietà | Descrizione |
|---|---|
| `schema.name` | ***(Obbligatorio)*** Nome dello schema XDM a cui appartiene l’entità. |
| `fields` | I campi XDM da restituire, sotto forma di array di stringhe. Per impostazione predefinita, vengono restituiti tutti i campi. |
| `identities` | ***(Obbligatorio)*** Matrice contenente un elenco di identità per le entità alle quali si desidera accedere. |
| `identities.entityId` | L’ID di un’entità a cui desideri accedere. |
| `identities.entityIdNS.code` | Lo spazio dei nomi di un ID di entità a cui desideri accedere. |
| `timeFilter.startTime` | Ora di inizio del filtro dell’intervallo di tempo, incluso. Deve essere con granularità di millisecondi. Il valore predefinito, se non specificato, è l&#39;inizio del tempo disponibile. |
| `timeFilter.endTime` | Filtro di fine intervallo di tempo, escluso. Deve essere con granularità di millisecondi. Il valore predefinito, se non specificato, corrisponde alla fine del tempo disponibile. |
| `limit` | Numero di record da restituire. Applicabile solo al numero di eventi di esperienza restituiti. Valore predefinito: 1.000. |
| `orderby` | Ordinamento degli eventi esperienza recuperati per marca temporale, scritti come `(+/-)timestamp` con il valore predefinito `+timestamp`. |
| `withCA` | Flag di funzione per abilitare gli attributi calcolati per la ricerca. Impostazione predefinita: false. |

**Risposta**
In caso di esito positivo, la risposta restituisce i campi richiesti delle entità specificate nel corpo della richiesta.

```json
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## Accedere agli eventi di serie temporali per un profilo in base all’identità

Puoi accedere agli eventi delle serie temporali in base all’identità dell’entità profilo associata, effettuando una richiesta GET al `/access/entities` endpoint. Questa identità è costituita da un valore ID (`entityId`) e uno spazio dei nomi delle identità (`entityIdNS`).

I parametri di query forniti nel percorso della richiesta specificano a quali dati accedere. Puoi includere più parametri, separati da e commerciali (&amp;). Un elenco completo dei parametri validi è fornito in [parametri di query](#query-parameters) sezione dell&#39;appendice.

**Formato API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Richiesta**

La richiesta seguente trova un’entità profilo per ID e recupera i valori per le proprietà `endUserIDs`, `web`, e `channel` per tutti gli eventi di serie temporali associati all’entità.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco impaginato di eventi di serie temporali e dei campi associati specificati nei parametri di query della richiesta.

>[!NOTE]
>
>La richiesta ha specificato un limite di uno (`limit=1`), quindi il `count` nella risposta seguente è 1 e viene restituita una sola entità.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### Accedere a una pagina di risultati successiva

I risultati vengono impaginati durante il recupero degli eventi delle serie temporali. Se sono presenti pagine successive di risultati, il `_page.next` La proprietà conterrà un ID. Inoltre, il `_links.next.href` fornisce un URI di richiesta per recuperare la pagina successiva. Per recuperare i risultati, effettua un’altra richiesta GET al `/access/entities` endpoint, tuttavia devi assicurarti di sostituire `/entities` con il valore dell’URI fornito.

>[!NOTE]
>
>Assicurati di non ripetere accidentalmente `/entities/` nel percorso della richiesta. Dovrebbe apparire solo una volta come, `/access/entities?start=...`

**Formato API**

```http
GET /access/{NEXT_URI}
```

| Parametro | Descrizione |
|---|---|
| `{NEXT_URI}` | Il valore URI preso da `_links.next.href`. |

**Richiesta**

La richiesta seguente recupera la pagina successiva dei risultati utilizzando `_links.next.href` URI come percorso della richiesta.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce la pagina successiva di risultati. Questa risposta non contiene pagine successive di risultati, come indicato dai valori stringa vuoti di `_page.next` e `_links.next.href`.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Accedere agli eventi delle serie temporali per più profili in base alle identità

Per accedere agli eventi delle serie temporali da più profili associati, devi effettuare una richiesta POST al `/access/entities` e fornendo le identità di profilo nel payload. Ciascuna di queste identità è costituita da un valore ID (`entityId`) e uno spazio dei nomi delle identità (`entityIdNS`).

**Formato API**

```http
POST /access/entities
```

**Richiesta**

La richiesta seguente recupera gli ID utente, le ore locali e i codici paese per gli eventi di serie temporali associati a un elenco di identità di profilo:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.experienceevent"
    },
    "relatedSchema": {
        "name": "_xdm.context.profile"
    },
    "identities": [
        {
            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW"
        }
        {
            "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY"
        }
    ],
    "fields": [
        "endUserIDs",
        "placeContext.localTime",
        "placeContext.geo.countryCode"
    ],
    
    "timeFilter": {
        "startTime": 11539838505
        "endTime": 1539838510
    },
    "limit": 10
}'
```

| Proprietà | Descrizione |
|---|---|
| `schema.name` | **(OBBLIGATORIO)** Schema XDM dell’entità da recuperare |
| `relatedSchema.name` | Se `schema.name` è `_xdm.context.experienceevent` questo valore deve specificare lo schema per l’entità profilo a cui sono correlati gli eventi della serie temporale. |
| `identities` | **(OBBLIGATORIO)** Un array che elenca i profili da cui recuperare gli eventi della serie temporale associati. Ogni voce nell’array è impostata in uno dei due modi seguenti: 1) utilizzando un’identità completa costituita da valore ID e spazio dei nomi oppure 2) fornendo un XID. |
| `fields` | Isola i dati restituiti a un set di campi specificato. Utilizza questa opzione per filtrare quali campi schema sono inclusi nei dati recuperati. Esempio: personalEmail,person.name,person.gender |
| `mergePolicyId` | Identifica il criterio di unione in base al quale gestire i dati restituiti. Se non ne è specificato uno nella chiamata del servizio, verrà utilizzato lo schema predefinito della tua organizzazione. Se non è stato configurato alcun criterio di unione predefinito, l’impostazione predefinita è nessuna unione di profili e nessuna unione di identità. |
| `orderby` | Ordinamento degli eventi esperienza recuperati per marca temporale, scritti come `(+/-)timestamp` con il valore predefinito `+timestamp`. |
| `timeFilter.startTime` | Specifica l&#39;ora di inizio per filtrare gli oggetti della serie temporale (in millisecondi). |
| `timeFilter.endTime` | Specifica l&#39;ora di fine per filtrare gli oggetti della serie temporale (in millisecondi). |
| `limit` | Valore numerico che specifica il numero massimo di oggetti da restituire. Predefinito: 1000 |
| `withCA` | Flag di funzione per abilitare gli attributi calcolati per la ricerca. Predefinito: false |

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco impaginato di eventi di serie temporali associati ai più profili specificati nella richiesta.

```json
{
    "GkouAW-yD9aoRCPhRYROJ-TetAFW": {
        "_page": {
            "orderby": "timestamp",
            "start": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
            "count": 10,
            "next": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
                "timestamp": 1537275882000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:42Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            },
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "a9e137b4-1348-4878-8167-e308af523d8b",
                "timestamp": 1537275889000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:49Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            }
        ],
        "_links": {
            "next": {
                "href": "/entities",
                "payload": {
                    "schema": {
                        "name": "_xdm.context.experienceevent"
                    },
                    "relatedSchema": {
                        "name": "_xdm.context.profile"
                    },
                    "timeFilter": {
                        "startTime": 1537275882000
                    },
                    "fields": [
                        "endUserIDs",
                        "placeContext.localTime",
                        "placeContext.geo.countryCode"
                    ],
                    "identities": [
                        {
                            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                            "start": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
                        }
                    ],
                    "limit": 10
                }
            }
        }
    },
    "GkouAW-2u-7iWt5vQ9u2wm40JOZY": {
        "_page": {
            "orderby": "timestamp",
            "start": "2746d0db-fa64-4e29-b67e-324bec638816",
            "count": 9,
            "next": ""
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "2746d0db-fa64-4e29-b67e-324bec638816",
                "timestamp": 1537559483000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:23Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            },
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "9bf337a1-3256-431e-a38c-5c0d42d121d1",
                "timestamp": 1537559486000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:26Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            }
        ],
        "_links": {
            "next": {
                "href": ""
            }
        }
    }
}`
```

In questo esempio di risposta, il primo profilo elencato (&quot;GkouAW-yD9aoRCPhRYROJ-TetAFW&quot;) fornisce un valore per `_links.next.payload`, il che significa che ci sono pagine aggiuntive di risultati per questo profilo. Consulta la sezione seguente su [accesso a risultati aggiuntivi](#access-additional-results) per informazioni dettagliate su come accedere a tali risultati aggiuntivi.

### Accedere ai risultati aggiuntivi {#access-additional-results}

Quando si recuperano eventi di serie temporali, possono essere restituiti molti risultati, pertanto i risultati sono spesso impaginati. Se sono presenti pagine successive di risultati per un particolare profilo, il `_links.next.payload` per quel profilo conterrà un oggetto payload.

Utilizzando questo payload nel corpo della richiesta, puoi eseguire una richiesta POST aggiuntiva al `access/entities` per recuperare la pagina successiva dei dati della serie temporale per quel profilo.

## Accedere agli eventi delle serie temporali in più entità dello schema

È possibile accedere a più entità connesse tramite un descrittore di relazione. L’esempio di chiamata API seguente presuppone che sia già stata definita una relazione tra due schemi. Per ulteriori informazioni sui descrittori di relazione, consulta la sezione [!DNL Schema Registry] Guida per gli sviluppatori API [guida dell’endpoint &quot;descriptors&quot;](../../xdm/api/descriptors.md).

Puoi includere i parametri di query nel percorso della richiesta per specificare a quali dati accedere. Puoi includere più parametri, separati da e commerciali (&amp;). Un elenco completo dei parametri validi è fornito in [parametri di query](#query-parameters) sezione dell&#39;appendice.

**Formato API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Richiesta**

La richiesta seguente recupera un’entità contenente un descrittore di relazione stabilito in precedenza per accedere alle informazioni tra schemi diversi.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco impaginato di eventi di serie temporali associati alle più entità.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "GkouAW-2Xkftzer3bBtHiW8GkaFL",
            "entityId": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
            "timestamp": 1564614939000,
            "entity": {
                "environment": {
                    "browserDetails": {}
                },
                "identityMap": {
                    "CRMId": [
                        {
                            "id": "78520026455138218785449796480922109723",
                            "primary": true
                        }
                    ]
                },

                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Red shoe",
                        "quantity": 85,
                        "storesAvailableIn": [
                            "da6dced5-9574-4dda-89b5-9dc106903f80",
                            "981bb433-2ee5-4db0-a19a-449ec9dbf39f"
                        ],
                        "SKU": "8f998279-797b-4da2-9e60-88bf73a9f15a",
                        "priceTotal": 934.8
                    }
                ],
                "_id": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
                "commerce": {
                    "order": {}
                },
                "placeContext": {
                    "geo": {
                        "_schema": {}
                    }
                },
                "device": {},
                "timestamp": "2019-07-31T23:15:39Z",
                "_experience": {
                    "profile": {
                        "identityNamespaces": {
                            "/productListItems[*]/SKU": {
                                "namespace": {
                                    "code": "ECID"
                                }
                            }
                        }
                    }
                }
            },
            "lastModifiedAt": "2019-10-10T00:14:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

### Accedere a una pagina di risultati successiva

I risultati vengono impaginati durante il recupero degli eventi delle serie temporali. Se sono presenti pagine successive di risultati, il `_page.next` La proprietà conterrà un ID. Inoltre, il `_links.next.href` fornisce un URI di richiesta per recuperare la pagina successiva effettuando ulteriori richieste di GET al `access/entities` endpoint.

## Passaggi successivi

Seguendo questa guida si è effettuato l&#39;accesso [!DNL Real-Time Customer Profile] campi dati, profili e dati di serie temporali. Per scoprire come accedere ad altre risorse di dati memorizzate in [!DNL Platform], vedere [Panoramica sull’accesso ai dati](../../data-access/home.md).

## Appendice {#appendix}

La sezione seguente fornisce informazioni supplementari sull’accesso a [!DNL Profile] dati utilizzando l’API.

### Parametri di query {#query-parameters}

I seguenti parametri vengono utilizzati nel percorso per le richieste di GET a `/access/entities` endpoint. Servono a identificare l’entità profilo a cui desideri accedere e a filtrare i dati restituiti nella risposta. I parametri richiesti sono etichettati, mentre gli altri sono facoltativi.

| Parametro | Descrizione | Esempio |
|---|---|---|
| `schema.name` | **(OBBLIGATORIO)** Schema XDM dell’entità da recuperare | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | Se `schema.name` è &quot;_xdm.context.experienceevent&quot;, questo valore deve specificare lo schema per l’entità profilo a cui sono correlati gli eventi della serie temporale. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(OBBLIGATORIO)** ID dell’entità. Se il valore di questo parametro non è un XID, è necessario fornire anche un parametro dello spazio dei nomi dell’identità (vedi `entityIdNS` di seguito). | `entityId=janedoe@example.com` |
| `entityIdNS` | Se `entityId` non viene fornito come XID, questo campo deve specificare lo spazio dei nomi dell’identità. | `entityIdNE=email` |
| `relatedEntityId` | Se `schema.name` è &quot;_xdm.context.experienceevent&quot;, questo valore deve specificare lo spazio dei nomi dell’identità dell’entità profilo correlata. Questo valore segue le stesse regole di `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Se `schema.name` è &quot;_xdm.context.experienceevent&quot;, questo valore deve specificare lo spazio dei nomi dell’identità per l’entità specificata in `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtra i dati restituiti nella risposta. Utilizzare questa opzione per specificare i valori dei campi dello schema da includere nei dati recuperati. Per più campi, separa i valori con una virgola senza spazi tra | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Identifica il criterio di unione in base al quale gestire i dati restituiti. Se non ne è specificato uno nella chiamata, verrà utilizzato lo schema predefinito della tua organizzazione. Se non è stato configurato alcun criterio di unione predefinito, l’impostazione predefinita è nessuna unione di profili e nessuna unione di identità. | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | Ordinamento degli eventi esperienza recuperati per marca temporale, scritti come `(+/-)timestamp` con il valore predefinito `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Specifica l&#39;ora di inizio per filtrare gli oggetti della serie temporale (in millisecondi). | `startTime=1539838505` |
| `endTime` | Specifica l&#39;ora di fine per filtrare gli oggetti della serie temporale (in millisecondi). | `endTime=1539838510` |
| `limit` | Valore numerico che specifica il numero massimo di oggetti da restituire. Predefinito: 1000 | `limit=100` |
| `property` | Filtra per valore della proprietà. Supporta i seguenti valutatori: =, !=, &lt;, &lt;=, >, >=. Può essere utilizzato solo con eventi di esperienza, con un massimo di tre proprietà supportate. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
| `withCA` | Flag di funzione per abilitare gli attributi calcolati per la ricerca. Predefinito: false | `withCA=true` |
