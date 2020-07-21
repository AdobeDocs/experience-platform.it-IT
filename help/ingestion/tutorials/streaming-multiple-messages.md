---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Streaming di più messaggi in una singola richiesta HTTP
topic: tutorial
translation-type: tm+mt
source-git-commit: 6a371aab5435bac97f714e5cf96a93adf4aa0303
workflow-type: tm+mt
source-wordcount: '1504'
ht-degree: 1%

---


# Invio di più messaggi in una singola richiesta HTTP

Durante lo streaming dei dati  Adobe Experience Platform, effettuare numerose chiamate HTTP può essere costoso. Ad esempio, invece di creare 200 richieste HTTP con payload da 1 KB, è molto più efficiente creare 1 richiesta HTTP con 200 messaggi da 1 KB ciascuno, con un singolo payload di 200 KB. Se utilizzati correttamente, il raggruppamento di più messaggi all’interno di una singola richiesta è un metodo eccellente per ottimizzare i dati inviati a  Experience Platform.

Questo documento fornisce un’esercitazione per l’invio di più messaggi ad  Experience Platform all’interno di una singola richiesta HTTP tramite l’assimilazione in streaming.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dell&#39;inserimento dei dati  Adobe Experience Platform. Prima di iniziare questa esercitazione, consulta la seguente documentazione:

- [Panoramica sull](../home.md)’inserimento dei dati: Vengono trattati i concetti fondamentali di &#39;inserimento dei dati Experience Platform, compresi i metodi di caricamento e i connettori dati.
- [Panoramica sull](../streaming-ingestion/overview.md)’assimilazione dello streaming: Il flusso di lavoro e gli elementi costitutivi dell&#39;assimilazione dei flussi di lavoro, ad esempio connessioni di streaming, set di dati, XDM Singolo profilo e XDM ExperienceEvent.

Questa esercitazione richiede anche di completare l&#39; [autenticazione per  l&#39;esercitazione sul Adobe Experience Platform](../../tutorials/authentication.md) al fine di effettuare correttamente le chiamate alle API Platform. Completando l&#39;esercitazione sull&#39;autenticazione viene fornito il valore per l&#39;intestazione Autorizzazione richiesto da tutte le chiamate API in questa esercitazione. L’intestazione è mostrata nelle chiamate di esempio come segue:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`

Tutte le richieste POST richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Creare una connessione in streaming

Prima di avviare lo streaming dei dati su  Experience Platform, è necessario creare una connessione di streaming. Leggi la guida [per la creazione di una connessione](./create-streaming-connection.md) in streaming.

Dopo la registrazione di una connessione di streaming, l&#39;utente, in qualità di produttore di dati, avrà un URL univoco che può essere utilizzato per lo streaming dei dati ad Platform.

## Trasmissione a un dataset

L&#39;esempio seguente mostra come inviare più messaggi a uno specifico dataset all&#39;interno di una singola richiesta HTTP. Inserire l&#39;ID del set di dati nell&#39;intestazione del messaggio per consentirne l&#39;inserimento diretto.

Potete ottenere l&#39;ID per un set di dati esistente utilizzando l&#39;interfaccia utente di Platform o un&#39;operazione di elenco nell&#39;API. L&#39;ID del set di dati si trova in [Experience Platform](https://platform.adobe.com) andando alla scheda **Set** dati, facendo clic sul set di dati per il quale si desidera utilizzare l&#39;ID e copiando la stringa dal campo ID **del** set di dati nella scheda **Informazioni** . Consultate la panoramica [del servizio](../../catalog/home.md) catalogo per informazioni su come recuperare i set di dati tramite l’API.

Invece di utilizzare un dataset esistente, potete creare un nuovo dataset. Per ulteriori informazioni sulla creazione di un set di dati tramite API [, consultate l&#39;esercitazione](../../catalog/api/create-dataset.md) Create a dataset using API (Creazione di un set di dati tramite API).

**Formato API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID della connessione di streaming creata. |

**Richiesta**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
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
                  "workEmail": {
                    "address": "gregdorcey@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "7af6adcc-dc9e-4692-b826-55d2abe68c11",
          "timestamp": "2019-02-23T22:07:31Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
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
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
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
                  "workEmail": {
                    "address": "emilyong@example.com"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Risposta**

Una risposta corretta restituisce uno stato HTTP 207 (stato multiplo). La revisione del corpo della risposta fornisce ulteriori dettagli sull&#39;esito positivo o negativo di ciascun metodo eseguito nella richiesta. Viene restituita una risposta per ogni elemento dell’array dei messaggi di richiesta. Di seguito è riportato un esempio di risposta positiva senza errori di messaggio:

```json
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565628583792:1485:153",
    "receivedTimeMs": 1565628583854,
    "responses": [
        {
            "xactionId": "1565628583792:1485:153:0"
        },
        {
            "xactionId": "1565628583792:1485:153:1"
        }
    ]
}
```

Per ulteriori informazioni sui codici di stato, consulta la tabella dei codici [di](#response-codes) risposta nell’appendice di questa esercitazione.

## Identificare i messaggi non riusciti

Rispetto all&#39;invio di una richiesta con un singolo messaggio, quando si invia una richiesta HTTP con più messaggi, è necessario tenere in considerazione altri fattori, quali: come identificare quando i dati non sono stati inviati, quali messaggi specifici non sono stati inviati e come possono essere recuperati, e cosa accade ai dati che hanno esito positivo quando altri messaggi nella stessa richiesta non arrivano a destinazione.

Prima di continuare con questa esercitazione, è consigliabile rivedere la guida al [recupero dei batch](../quality/retrieve-failed-batches.md) non riusciti.

### Invia payload di richiesta con messaggi validi e non validi

L&#39;esempio seguente mostra cosa accade quando il batch include messaggi validi e non validi.

Il payload della richiesta è un array di oggetti JSON che rappresenta l&#39;evento nello schema XDM. Per la corretta convalida del messaggio è necessario rispettare le seguenti condizioni:
- Il `imsOrgId` campo nell’intestazione del messaggio deve corrispondere alla definizione di ingresso. Se il payload della richiesta non include un `imsOrgId` campo, il servizio di base per la raccolta dati (DCCS) aggiungerà il campo automaticamente.
- L&#39;intestazione del messaggio deve fare riferimento a uno schema XDM esistente creato nell&#39;interfaccia utente di Platform.
- Il `datasetId` campo deve fare riferimento a un dataset esistente in Platform e il relativo schema deve corrispondere allo schema fornito nell&#39; `header` oggetto all&#39;interno di ciascun messaggio incluso nel corpo della richiesta.

**Formato API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID dell’ingresso dati creato. |

**Richiesta**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
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
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
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
                  "workEmail": {
                    "address": "rogerkanagawa@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
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
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
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
                  "workEmail": {
                    "address": "mohandeewar@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
   {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
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
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          }
        }
      }
    },
    {
      "header": {
        "msgType": "xdmEntityCreate",
        "msgId": "79d2e715-f25f-4c36",
        "xdmSchema": {
          "name": "_xdm.context.experienceevent"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "xdmSchema": {
            "name": "_xdm.context.experienceevent"
          }
        },
        "xdmEntity": {
          "_id": "abc",
          "dataSource": {
            "_id": "http://abc.com/abc"
          },
          "timestamp": "2018-05-18T15:28:25Z",
          "endUserIDs": {
            "_vendor": {
              "adobe": {
                "experience": {
                  "mcId": {
                    "id": "http://abc.com/abc"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Risposta**

Il payload di risposta include uno stato per ciascun messaggio insieme a un GUID nel `xactionId` quale è possibile utilizzare il tracciamento.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        }
    ]
}
```

La risposta di esempio riportata sopra mostra i messaggi di errore per la richiesta precedente. Confrontando questa risposta alla precedente risposta valida, potete osservare che la richiesta ha avuto esito positivo, con un messaggio che è stato acquisito correttamente e tre messaggi che hanno avuto esito negativo. Si noti che entrambe le risposte restituiscono un codice di stato &#39;207&#39;. Per ulteriori informazioni sui codici di stato, consulta la tabella dei codici [di](#response-codes) risposta nell’appendice di questa esercitazione.

Il primo messaggio è stato inviato correttamente ad Platform e non viene influenzato dai risultati degli altri messaggi. Di conseguenza, quando si tenta di inviare nuovamente i messaggi non riusciti, non è necessario includere nuovamente il messaggio.

Il secondo messaggio non è riuscito perché mancava un corpo del messaggio. La richiesta di raccolta prevede che gli elementi del messaggio abbiano sezioni di intestazione e corpo valide. Se si aggiunge il codice seguente dopo l’intestazione del secondo messaggio, la richiesta viene corretta e il secondo messaggio viene convalidato:

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

Il terzo messaggio non è riuscito a causa di un ID organizzazione IMS non valido utilizzato nell&#39;intestazione. L&#39;organizzazione IMS deve corrispondere al {CONNECTION_ID} a cui si sta tentando di inviare. Per determinare quale ID organizzazione IMS corrisponde alla connessione di streaming in uso, potete eseguire una `GET inlet` richiesta utilizzando l&#39;API [di inserimento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)dati. Consultate [il recupero di una connessione](./create-streaming-connection.md#get-data-collection-url) in streaming per un esempio di come recuperare le connessioni in streaming create in precedenza.

Il quarto messaggio non è riuscito perché non seguiva lo schema XDM previsto. L&#39;elemento `xdmSchema` incluso nell&#39;intestazione e nel corpo della richiesta non corrisponde allo schema XDM del `{DATASET_ID}`. La correzione dello schema nell&#39;intestazione e nel corpo del messaggio consente di superare la convalida DCCS e di inviarlo ad Platform. È inoltre necessario aggiornare il corpo del messaggio in modo che corrisponda allo schema XDM dell&#39; `{DATASET_ID}` applicazione per il passaggio della convalida in streaming su Platform. Per ulteriori informazioni sugli eventi dei messaggi che sono stati inviati correttamente ad Platform, consulta la sezione [Conferma messaggi acquisiti](#confirm-messages-ingested) in questa esercitazione.

### Recupero di messaggi non riusciti da Platform

I messaggi con errore vengono identificati da un codice di stato dell&#39;errore nell&#39;array di risposte.
I messaggi non validi vengono raccolti e memorizzati in un batch di &quot;errore&quot; all&#39;interno del set di dati specificato da `{DATASET_ID}`.

Leggere la guida [al recupero dei batch](../quality/retrieve-failed-batches.md) non riusciti per ulteriori informazioni sul recupero dei messaggi batch non riusciti.

## Conferma messaggi inviati

I messaggi che superano la convalida DCCS vengono inviati in streaming ad Platform. Su Platform, i messaggi batch vengono testati mediante convalida in streaming prima di essere trasferiti nel lago di dati. Lo stato dei batch, con esito positivo o meno, viene visualizzato all&#39;interno del set di dati specificato da `{DATASET_ID}`.

È possibile visualizzare lo stato dei messaggi batch che sono stati inviati correttamente ad Platform utilizzando l&#39;interfaccia utente [Experience Platform](https://platform.adobe.com) andando alla scheda **Set** dati, facendo clic sul set di dati a cui si sta eseguendo lo streaming e selezionando la scheda Attività **** DataSet.

I messaggi batch che superano la convalida dello streaming su Platform vengono trasferiti nel lago dati. I messaggi sono quindi disponibili per l’analisi o l’esportazione.

## Passaggi successivi

Ora che sai come inviare più messaggi in una singola richiesta e quando i messaggi vengono correttamente inseriti nel set di dati di destinazione, puoi iniziare a inviare in streaming i tuoi dati ad Platform. Per una panoramica su come eseguire query e recuperare dati acquisiti da Platform, consultate la guida [Accesso](../../data-access/tutorials/dataset-data.md) ai dati.

## Appendice

Questa sezione contiene informazioni supplementari per l&#39;esercitazione.

### Codici di risposta

Nella tabella seguente sono riportati i codici di stato restituiti dai messaggi di risposta riusciti e non riusciti.

| Codice di stato | Descrizione |
| :---: | --- |
| 207 | Anche se &#39;207&#39; viene utilizzato come codice di stato della risposta globale, il destinatario deve consultare il contenuto del corpo di risposta multistato per ulteriori informazioni sull&#39;esito positivo o negativo dell&#39;esecuzione del metodo. Il codice di risposta viene utilizzato in caso di esito positivo o parziale e anche in situazioni di fallimento. |
| 400 | C&#39;è stato un problema con la richiesta. Vedere il corpo della risposta per un messaggio di errore più specifico (ad esempio, payload di messaggi mancavano i campi obbligatori oppure Messaggio era in formato xdm sconosciuto). |
| 401 | Non autorizzato: nella richiesta manca un&#39;intestazione di autorizzazione valida. Viene restituito solo per le insenature con autenticazione abilitata. |
| 403 | Non autorizzato:  Il token di autorizzazione fornito non è valido o è scaduto. Viene restituito solo per le insenature con autenticazione abilitata. |
| 413 | Payload troppo grande - generato quando la richiesta di payload totale è maggiore di 1 MB. |
| 429 | Troppe richieste entro la durata specificata. |
| 500 | Errore durante l&#39;elaborazione del payload. Vedere il corpo della risposta per un messaggio di errore più specifico (ad esempio, schema di payload del messaggio non specificato o non corrispondente alla definizione XDM in Platform). |
| 503 | Il servizio non è attualmente disponibile. I client devono riprovare almeno 3 volte utilizzando una strategia di back-off esponenziale. |