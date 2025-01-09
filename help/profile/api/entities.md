---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API entità (accesso profilo)
type: Documentation
description: Adobe Experience Platform consente di accedere ai dati del profilo cliente in tempo reale utilizzando le API RESTful o l’interfaccia utente di. Questa guida illustra come accedere alle entità, più comunemente note come "profili", utilizzando l’API di profilo.
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 9f9823a23c488e63b8b938cb885f050849836e36
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 4%

---

# Endpoint entità (accesso profilo)

Adobe Experience Platform consente di accedere ai dati di [!DNL Real-Time Customer Profile] utilizzando le API RESTful o l&#39;interfaccia utente. Questa guida illustra come accedere alle entità, più comunemente note come &quot;profili&quot;, utilizzando l’API. Per ulteriori informazioni sull&#39;accesso ai profili tramite l&#39;interfaccia utente di [!DNL Platform], fare riferimento alla [Guida utente del profilo](../ui/user-guide.md).

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte di [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Prima di continuare, consulta la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Recuperare un’entità {#retrieve-entity}

È possibile recuperare un&#39;entità profilo o i relativi dati di serie temporali effettuando una richiesta di GET all&#39;endpoint `/access/entities` insieme ai parametri di query richiesti.

>[!BEGINTABS]

>[!TAB Entità profilo]

**Formato API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

I parametri di query forniti nel percorso della richiesta specificano a quali dati accedere. Puoi includere più parametri, separati da e commerciali (&amp;).

Per accedere a un&#39;entità profilo, **devi** fornire i seguenti parametri di query:

- `schema.name`: nome dello schema XDM dell&#39;entità. In questo caso d&#39;uso, `schema.name=_xdm.context.profile`.
- `entityId`: ID dell&#39;entità da recuperare.
- `entityIdNS`: spazio dei nomi dell&#39;entità che si sta tentando di recuperare. Questo valore deve essere fornito se `entityId` è **not** un XID.

Un elenco completo dei parametri validi è fornito nella sezione [parametri di query](#query-parameters) dell&#39;appendice.

**Richiesta**

La richiesta seguente recupera l’e-mail e il nome di un cliente utilizzando un’identità.

+++ Richiesta di esempio per recuperare un’entità utilizzando un’identità

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con l’entità richiesta.

+++ Risposta di esempio contenente l’entità richiesta

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
                    "id": "johnsmith@example.com",
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

+++

>[!NOTE]
>
>Se un grafico correlato collega più di 50 identità, questo servizio restituirà lo stato HTTP 422 e il messaggio &quot;Troppe identità correlate&quot;. Se ricevi questo errore, puoi aggiungere altri parametri di query per restringere la ricerca.

>[!TAB Evento serie temporali]

**Formato API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

I parametri di query forniti nel percorso della richiesta specificano a quali dati accedere. Puoi includere più parametri, separati da e commerciali (&amp;).

Per accedere ai dati degli eventi della serie temporale, **devi** fornire i seguenti parametri di query:

- `schema.name`: nome dello schema XDM dell&#39;entità. In questo caso d&#39;uso, il valore è `schema.name=_xdm.context.experienceevent`.
- `relatedSchema.name`: nome dello schema correlato. Poiché il nome dello schema è Evento esperienza, il valore di **deve** essere `relatedSchema.name=_xdm.context.profile`.
- `relatedEntityId`: ID dell&#39;entità correlata.
- `relatedEntityIdNS`: spazio dei nomi dell&#39;entità correlata. Questo valore deve essere fornito se `relatedEntityId` è **not** un XID.

Un elenco completo dei parametri validi è fornito nella sezione [parametri di query](#query-parameters) dell&#39;appendice.

**Richiesta**

La richiesta seguente trova un&#39;entità profilo per ID e recupera i valori per le proprietà `endUserIDs`, `web` e `channel` per tutti gli eventi di serie temporali associati all&#39;entità.

+++ Richiesta di esempio per recuperare gli eventi di serie temporali associati a un’entità

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco impaginato degli eventi delle serie temporali e dei campi associati specificati nei parametri di query della richiesta.

>[!NOTE]
>
>La richiesta ha specificato un limite di uno (`limit=1`), pertanto `count` nella risposta seguente è 1 e viene restituita una sola entità.

+++ Una risposta di esempio che contiene i dati degli eventi della serie temporale richiesti

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

+++

>[!TAB Account B2B]

**Formato API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

I parametri di query forniti nel percorso della richiesta specificano a quali dati accedere. Puoi includere più parametri, separati da e commerciali (&amp;).

Per accedere ai dati dell&#39;account B2B, **devi** fornire i seguenti parametri di query:

- `schema.name`: nome dello schema XDM dell&#39;entità. In questo caso d&#39;uso, il valore è `schema.name=_xdm.context.account`.
- `entityId`: ID dell&#39;entità da recuperare.
- `entityIdNS`: spazio dei nomi dell&#39;entità che si sta tentando di recuperare. Questo valore deve essere fornito se `entityId` è **not** un XID.

Un elenco completo dei parametri validi è fornito nella sezione [parametri di query](#query-parameters) dell&#39;appendice.

**Richiesta**

+++ Una richiesta di esempio per recuperare un account B2B

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.account&entityIdNs=b2b_account&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con l’entità richiesta.

+++ Risposta di esempio contenente l’entità richiesta

```json
{
    "GuQ-AUFjgjaeIw": {
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "{SOURCE_ID}",
                    "sourceKey": "{SOURCE_KEY}",
                    "sourceInstanceID": "{SOURCE_INSTANCE_ID}",
                    "sourceType": "{SOURCE_TYPE}"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "{SOURCE_ID}"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!TAB Opportunità B2B]

**Formato API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

I parametri di query forniti nel percorso della richiesta specificano a quali dati accedere. Puoi includere più parametri, separati da e commerciali (&amp;).

Per accedere a un&#39;entità opportunità B2B, **devi** fornire i seguenti parametri di query:

- `schema.name`: nome dello schema XDM dell&#39;entità. In questo caso d&#39;uso, `schema.name=_xdm.context.opportunity`.
- `entityId`: ID dell&#39;entità da recuperare.
- `entityIdNS`: spazio dei nomi dell&#39;entità che si sta tentando di recuperare. Questo valore deve essere fornito se `entityId` è **not** un XID.

Un elenco completo dei parametri validi è fornito nella sezione [parametri di query](#query-parameters) dell&#39;appendice.

**Richiesta**

+++ Richiesta di esempio per recuperare un’entità opportunità B2B

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.opportunity&entityIdNs=b2b_opportunity&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con l’entità richiesta.

+++ Risposta di esempio contenente l’entità richiesta

```json
{
  "Ggw_AUFjgjaeIw": {
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

## Recuperare più entità {#retrieve-entities}

Per recuperare più entità profilo o eventi di serie temporali, devi eseguire una richiesta POST all&#39;endpoint `/access/entities` e fornire le identità nel payload.

>[!BEGINTABS]

>[!TAB Entità profilo]

**Formato API**

```http
POST /access/entities
```

**Richiesta**

La richiesta seguente recupera i nomi e gli indirizzi e-mail di diversi clienti da un elenco di identità.

+++Una richiesta di esempio per recuperare più entità

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
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
        "orderby": "-timestamp"
      }'
```

| Proprietà | Tipo | Descrizione |
| -------- |----- | ----------- |
| `schema.name` | Stringa | **(Obbligatorio)** Il nome dello schema XDM a cui appartiene l&#39;entità. |
| `fields` | Array | I campi XDM da restituire, sotto forma di array di stringhe. Per impostazione predefinita, vengono restituiti tutti i campi. |
| `identities` | Array | **(Obbligatorio)** Matrice contenente un elenco di identità per le entità alle quali si desidera accedere. |
| `identities.entityId` | Stringa | L’ID di un’entità a cui desideri accedere. |
| `identities.entityIdNS.code` | Stringa | Lo spazio dei nomi di un ID di entità a cui desideri accedere. |
| `timeFilter.startTime` | Intero | Specifica l&#39;ora di inizio per filtrare le entità profilo (in millisecondi). Per impostazione predefinita, questo valore viene impostato come inizio del tempo disponibile. |
| `timeFilter.endTime` | Intero | Specifica l&#39;ora di fine per filtrare le entità profilo (in millisecondi). Per impostazione predefinita, questo valore viene impostato come fine del tempo disponibile. |
| `limit` | Intero | Numero massimo di record da restituire. Per impostazione predefinita, questo valore è impostato su 1000. |
| `orderby` | Stringa | Ordinamento degli eventi esperienza recuperati per marca temporale, scritti come `(+/-)timestamp` con valore predefinito `+timestamp`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i campi richiesti delle entità specificate nel corpo della richiesta.

+++ Risposta di esempio contenente le entità richieste

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

+++

>[!TAB Eventi di serie temporali]

**Formato API**

```http
POST /access/entities
```

**Richiesta**

La richiesta seguente recupera ID utente, ora locale e codici paese per gli eventi di serie temporali associati a un elenco di identità di profilo.

+++ Richiesta di esempio per recuperare i dati di serie temporali

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
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
    "limit": 10,
    "orderby": "-timestamp"
}'
```

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| `schema.name` | Stringa | **(Obbligatorio)** Il nome dello schema XDM a cui appartiene l&#39;entità. |
| `relatedSchema.name` | Stringa | Se `schema.name` è `_xdm.context.experienceevent` questo valore deve specificare lo schema per l&#39;entità profilo a cui sono correlati gli eventi della serie temporale. |
| `identities` | Array | **(Obbligatorio)** Un elenco array di profili da cui recuperare gli eventi della serie temporale associati. Ogni voce nell&#39;array è impostata in uno dei due modi seguenti: <ol><li>Utilizzo di un’identità completa costituita da valore ID e spazio dei nomi</li><li>Fornitura di un XID</li></ol> |
| `fields` | Stringa | I campi XDM da restituire, sotto forma di array di stringhe. Per impostazione predefinita, vengono restituiti tutti i campi. |
| `orderby` | Stringa | Ordinamento degli eventi esperienza recuperati per marca temporale, scritti come `(+/-)timestamp` con valore predefinito `+timestamp`. |
| `timeFilter.startTime` | Intero | Specifica l&#39;ora di inizio per filtrare gli oggetti della serie temporale (in millisecondi). Per impostazione predefinita, questo valore viene impostato come inizio del tempo disponibile. |
| `timeFilter.endTime` | Intero | Specifica l&#39;ora di fine per filtrare gli oggetti della serie temporale (in millisecondi). Per impostazione predefinita, questo valore viene impostato come fine del tempo disponibile. |
| `limit` | Intero | Numero massimo di record da restituire. Per impostazione predefinita, questo valore è impostato su 1.000. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco impaginato di eventi di serie temporali associati ai più profili specificati nella richiesta.

+++ Risposta di esempio contenente gli eventi della serie temporale

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

+++

>[!NOTE]
>
>In questo esempio di risposta, il primo profilo elencato (&quot;GkouAW-yD9aoRCPhRYROJ-TetAFW&quot;) fornisce un valore per `_links.next.payload`, il che significa che ci sono pagine aggiuntive di risultati per questo profilo.
>
>Per accedere a questi risultati, è possibile eseguire una richiesta POST aggiuntiva all&#39;endpoint `/access/entities` con il payload elencato come corpo della richiesta.

>[!TAB Account B2B]

**Formato API**

```http
POST /access/entities
```

**Richiesta**

La richiesta seguente recupera gli account B2B richiesti.

+++Una richiesta di esempio per recuperare più entità

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.account"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            }
        ]
    }'
```

| Proprietà | Tipo | Descrizione |
| -------- |----- | ----------- |
| `schema.name` | Stringa | **(Obbligatorio)** Il nome dello schema XDM a cui appartiene l&#39;entità. |
| `identities` | Array | **(Obbligatorio)** Matrice contenente un elenco di identità per le entità alle quali si desidera accedere. |
| `identities.entityId` | Stringa | L’ID di un’entità a cui desideri accedere. |
| `identities.entityIdNS.code` | Stringa | Lo spazio dei nomi di un ID di entità a cui desideri accedere. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con le entità richieste.

+++ Risposta di esempio contenente le entità richieste

```json
{
    "GuQ-AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjeeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjmeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
            "b2b_account": [
                {
                    "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                },
                {
                    "id": "2334265"
                }
            ]
        },
        "isDeleted": false,
        "accountKey": {
            "sourceID": "2334265",
            "sourceKey": "2334265",
            "sourceInstanceID": "2334265",
            "sourceType": "Random"
        }
    }
}
```

+++

>[!TAB Opportunità B2B]

**Formato API**

```http
POST /access/entities
```

**Richiesta**

La richiesta seguente recupera le opportunità B2B richieste.

+++ Una richiesta di esempio per recuperare più entità

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.opportunity"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334265",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            }
        ]
    }'
```

| Proprietà | Tipo | Descrizione |
| -------- |----- | ----------- |
| `schema.name` | Stringa | **(Obbligatorio)** Il nome dello schema XDM a cui appartiene l&#39;entità. |
| `identities` | Array | **(Obbligatorio)** Matrice contenente un elenco di identità per le entità alle quali si desidera accedere. |
| `identities.entityId` | Stringa | L’ID di un’entità a cui desideri accedere. |
| `identities.entityIdNS.code` | Stringa | Lo spazio dei nomi di un ID di entità a cui desideri accedere. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con le entità richieste.

+++ Risposta di esempio contenente le entità richieste

```json
{
    "Ggw_AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjieIw": {
        "requestedIdentity": {
            "entityId": "2334264",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjieIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334264",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334264"
                    },
                    {
                        "id": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334264",
                "sourceKey": "2334264",
                "sourceInstanceID": "2334264",
                "sourceType": "Salesforce"
            }
        }
    },
    "Ggw_AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjeeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjmeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334265"
                    },
                    {
                        "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334265",
                "sourceKey": "2334265",
                "sourceInstanceID": "2334265",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

### Accedere a una pagina di risultati successiva

I risultati vengono impaginati durante il recupero degli eventi delle serie temporali. Se sono presenti pagine successive di risultati, la proprietà `_page.next` conterrà un ID. Inoltre, la proprietà `_links.next.href` fornisce un URI di richiesta per recuperare la pagina successiva. Per recuperare i risultati, eseguire un&#39;altra richiesta di GET all&#39;endpoint `/access/entities` e sostituire `/entities` con il valore dell&#39;URI specificato.

>[!NOTE]
>
>Assicurarsi di non ripetere accidentalmente `/entities/` nel percorso della richiesta. Deve apparire solo una volta come, `/access/entities?start=...`

**Formato API**

```http
GET /access/{NEXT_URI}
```

| Parametro | Descrizione |
|---|---|
| `{NEXT_URI}` | Valore URI preso da `_links.next.href`. |

**Richiesta**

La richiesta seguente recupera la pagina successiva dei risultati utilizzando l&#39;URI `_links.next.href` come percorso della richiesta.

+++ Una richiesta di esempio per accedere alla pagina successiva dei risultati

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce la pagina successiva di risultati. Questa risposta non contiene pagine successive di risultati, come indicato dai valori stringa vuoti di `_page.next` e `_links.next.href`.

+++ Risposta di esempio contenente la pagina successiva di entità

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

+++

## Eliminare un’entità {#delete-entity}

È possibile eliminare un&#39;entità dall&#39;archivio profili effettuando una richiesta DELETE all&#39;endpoint `/access/entities` insieme ai parametri di query richiesti.

**Formato API**

```http
DELETE /access/entities?{QUERY_PARAMETERS}
```

I parametri di query forniti nel percorso della richiesta specificano a quali dati accedere. Puoi includere più parametri, separati da e commerciali (&amp;).

Per eliminare un&#39;entità, **devi** fornire i seguenti parametri di query:

- `schema.name`: nome dello schema XDM dell&#39;entità. In questo caso d&#39;uso, puoi **solo** usare `schema.name=_xdm.context.profile`.
- `entityId`: ID dell&#39;entità da recuperare.
- `entityIdNS`: spazio dei nomi dell&#39;entità che si sta tentando di recuperare. Questo valore deve essere fornito se `entityId` è **not** un XID.
- `mergePolicyId`: ID del criterio di unione dell&#39;entità. Il criterio di unione contiene informazioni sull’unione di identità e l’unione di oggetti XDM chiave-valore. Se questo valore non viene fornito, verrà utilizzato il criterio di unione predefinito.

**Richiesta**

La richiesta seguente elimina l’entità specificata.

+++ Richiesta di esempio per eliminare un’entità

```shell
curl -X DELETE 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 con un corpo di risposta vuoto.

## Passaggi successivi

Seguendo questa guida hai effettuato l&#39;accesso a [!DNL Real-Time Customer Profile] campi dati, profili e dati di serie temporali. Per informazioni su come accedere ad altre risorse di dati archiviate in [!DNL Platform], vedere la [panoramica sull&#39;accesso ai dati](../../data-access/home.md).

## Appendice {#appendix}

La sezione seguente fornisce informazioni supplementari sull&#39;accesso ai dati di [!DNL Profile] tramite l&#39;API.

### Parametri della query {#query-parameters}

I seguenti parametri vengono utilizzati nel percorso per le richieste GET all&#39;endpoint `/access/entities`. Servono a identificare l’entità profilo a cui desideri accedere e a filtrare i dati restituiti nella risposta. I parametri richiesti sono etichettati, mentre gli altri sono facoltativi.

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `schema.name` | **(Obbligatorio)** Il nome dello schema XDM dell&#39;entità. | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | Se `schema.name` è `_xdm.context.experienceevent`, questo valore **deve** specificare lo schema per l&#39;entità profilo a cui sono correlati gli eventi della serie temporale. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(Obbligatorio)** ID dell&#39;entità. Se il valore di questo parametro non è un XID, è necessario fornire anche un parametro dello spazio dei nomi dell&#39;identità (`entityIdNS`). | `entityId=janedoe@example.com` |
| `entityIdNS` | Se `entityId` non viene fornito come XID, il campo **deve** specificare lo spazio dei nomi dell&#39;identità. | `entityIdNS=email` |
| `relatedEntityId` | Se `schema.name` è `_xdm.context.experienceevent`, questo valore **deve** specificare l&#39;ID dell&#39;entità profilo correlata. Questo valore segue le stesse regole di `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Se `schema.name` è &quot;_xdm.context.experienceevent&quot;, questo valore deve specificare lo spazio dei nomi identità per l&#39;entità specificata in `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtra i dati restituiti nella risposta. Utilizzare questa opzione per specificare i valori dei campi dello schema da includere nei dati recuperati. Per più campi, separa i valori con una virgola senza spazi tra. | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Identifica il criterio di unione in base al quale gestire i dati restituiti. Se non ne è specificato uno nella chiamata, verrà utilizzato lo schema predefinito della tua organizzazione. Se non è stato configurato alcun criterio di unione predefinito, l’impostazione predefinita è nessuna unione di profili e nessuna unione di identità. | `mergePolicyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | Ordinamento delle entità recuperate per marca temporale. Scritto come `(+/-)timestamp`, il valore predefinito è `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Specifica l&#39;ora di inizio per filtrare le entità (in millisecondi). | `startTime=1539838505` |
| `endTime` | Specifica l&#39;ora di fine per filtrare le entità (in millisecondi). | `endTime=1539838510` |
| `limit` | Specifica il numero massimo di entità da restituire. Per impostazione predefinita, questo valore è impostato su 1000. | `limit=100` |
| `property` | Filtra per valore della proprietà. Questo parametro di query supporta i seguenti valutatori: =, !=, &lt;, &lt;=, >, >=. Questa può essere utilizzata solo con eventi di esperienza, con un massimo di tre proprietà supportate. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
