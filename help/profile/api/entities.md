---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API entità (accesso profilo)
type: Documentation
description: Adobe Experience Platform consente di accedere ai dati del profilo cliente in tempo reale utilizzando le API RESTful o l’interfaccia utente di. Questa guida illustra come accedere alle entità, più comunemente note come "profili", utilizzando l’API di profilo.
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 40400ab8cc87a6c8d6d37f1a20eaf96ab49aabf7
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 3%

---

# Endpoint entità (accesso profilo)

Adobe Experience Platform consente di accedere ai dati di [!DNL Real-Time Customer Profile] utilizzando le API RESTful o l&#39;interfaccia utente. Questa guida illustra come accedere alle entità, più comunemente note come &quot;profili&quot;, utilizzando l’API. Per ulteriori informazioni sull&#39;accesso ai profili tramite l&#39;interfaccia utente di [!DNL Experience Platform], fare riferimento alla [Guida utente del profilo](../ui/user-guide.md).

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte di [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Prima di continuare, consulta la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

>[!BEGINSHADEBOX]

## Risoluzione entità

Come parte dell’aggiornamento dell’architettura, Adobe sta introducendo la risoluzione delle entità per account e opportunità, utilizzando la corrispondenza degli ID deterministici basata sui dati più recenti. Il processo di risoluzione delle entità viene eseguito quotidianamente durante la segmentazione batch, prima di valutare tipi di pubblico con più entità con attributi B2B.

Questo miglioramento consente ad Experience Platform di identificare e unificare più record che rappresentano la stessa entità, migliorando la coerenza dei dati e consentendo una segmentazione del pubblico più accurata.

In precedenza, Account e opportunità si basavano su una risoluzione basata su un grafico di identità che collegava le identità, incluse tutte le acquisizioni storiche. Nel nuovo approccio di risoluzione delle entità, le identità sono collegate solo in base ai dati più recenti

### Come funziona la risoluzione delle entità?

- **Prima**: se è stato utilizzato un numero DUNS (Data Universal Numbering System) come identità aggiuntiva e il numero DUNS dell&#39;account è stato aggiornato in un sistema di origine come CRM, l&#39;ID account è collegato sia ai numeri DUNS vecchi che a quelli nuovi.
- **Dopo**: se il numero DUNS è stato utilizzato come identità aggiuntiva e il numero DUNS dell&#39;account è stato aggiornato in un sistema di origine come CRM, l&#39;ID account viene collegato solo al nuovo numero DUNS, riflettendo in tal modo lo stato corrente dell&#39;account in modo più accurato.

In seguito a questo aggiornamento, l&#39;API [!DNL Profile Access] riflette ora la visualizzazione del profilo di unione più recente dopo il completamento di un processo di risoluzione entità. Inoltre, i dati coerenti forniscono casi di utilizzo come segmentazione, attivazione e analisi con una maggiore precisione e coerenza dei dati.

>[!ENDSHADEBOX]

## Recuperare un’entità {#retrieve-entity}

>[!IMPORTANT]
>
>Le seguenti entità B2B non sono più supportate per le richieste di ricerca tramite l&#39;API: **Relazione account-persona, Relazione opportunità-persona, Campagna, Membro della campagna, Elenco marketing e Membro dell&#39;elenco marketing**.
>
>Il supporto per queste entità è stato dichiarato obsoleto. Se disponi di integrazioni o flussi di lavoro esistenti che si basano sull’accesso a tali entità, aggiornali per utilizzare i tipi di entità supportati per garantire funzionalità continue.

È possibile recuperare un&#39;entità profilo effettuando una richiesta GET all&#39;endpoint `/access/entities` insieme ai parametri di query richiesti.

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

Per recuperare più entità profilo, devi eseguire una richiesta POST all&#39;endpoint `/access/entities` e fornire le identità nel payload.

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

I risultati vengono impaginati durante il recupero degli eventi delle serie temporali. Se sono presenti pagine successive di risultati, la proprietà `_page.next` conterrà un ID. Inoltre, la proprietà `_links.next.href` fornisce un URI di richiesta per recuperare la pagina successiva. Per recuperare i risultati, eseguire un&#39;altra richiesta GET all&#39;endpoint `/access/entities` e sostituire `/entities` con il valore dell&#39;URI specificato.

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

>[!IMPORTANT]
>
>Le richieste di eliminazione per le seguenti entità B2B sono diventate obsolete:
>
>- Account
>- Relazione account-persona
>- Opportunità
>- Relazione opportunità-persona
>- Campaign
>- Membro della campagna
>- Elenco marketing
>- Membri di elenco marketing

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

Seguendo questa guida hai effettuato l&#39;accesso a [!DNL Real-Time Customer Profile] campi dati, profili e dati di serie temporali. Per informazioni su come accedere ad altre risorse di dati archiviate in [!DNL Experience Platform], vedere la [panoramica sull&#39;accesso ai dati](../../data-access/home.md).

## Appendice {#appendix}

La sezione seguente fornisce informazioni supplementari sull&#39;accesso ai dati di [!DNL Profile] tramite l&#39;API.

### Parametri della query {#query-parameters}

I seguenti parametri vengono utilizzati nel percorso per le richieste GET all&#39;endpoint `/access/entities`. Servono a identificare l’entità profilo a cui desideri accedere e a filtrare i dati restituiti nella risposta. I parametri richiesti sono etichettati, mentre gli altri sono facoltativi.

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `schema.name` | **(Obbligatorio)** Il nome dello schema XDM dell&#39;entità. | `schema.name=_xdm.context.profile` |
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
