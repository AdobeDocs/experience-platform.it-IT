---
keywords: Experience Platform;home;argomenti popolari;acquisizione streaming;acquisizione;streaming messaggi multipli;messaggi multipli;
solution: Experience Platform
title: Inviare più messaggi in una singola richiesta HTTP
type: Tutorial
description: Questo documento fornisce un tutorial per l’invio di più messaggi a Adobe Experience Platform all’interno di una singola richiesta HTTP utilizzando l’acquisizione in streaming.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 3ad5c06db07b360df255d3afb1c177cc5de613bb
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 1%

---

# Inviare più messaggi in una singola richiesta HTTP

Quando si inviano dati in streaming a Adobe Experience Platform, effettuare numerose chiamate HTTP può essere costoso. Ad esempio, invece di creare 200 richieste HTTP con payload da 1 KB, è molto più efficiente creare 1 richiesta HTTP con 200 messaggi da 1 KB ciascuno, con un singolo payload di 200 KB. Se utilizzato correttamente, raggruppare più messaggi all’interno di una singola richiesta è un modo eccellente per ottimizzare i dati a cui vengono inviati [!DNL Experience Platform].

Questo documento fornisce un&#39;esercitazione per l&#39;invio di più messaggi a [!DNL Experience Platform] all’interno di una singola richiesta HTTP utilizzando l’acquisizione in streaming.

## Introduzione

Questa esercitazione richiede una buona comprensione di Adobe Experience Platform [!DNL Data Ingestion]. Prima di iniziare questa esercitazione, consulta la seguente documentazione:

- [Panoramica sull’acquisizione dei dati](../home.md): Copre i concetti fondamentali di [!DNL Experience Platform Data Ingestion], compresi i metodi di acquisizione e i connettori dati.
- [Panoramica sull’acquisizione in streaming](../streaming-ingestion/overview.md): Il flusso di lavoro e gli elementi costitutivi dell’acquisizione in streaming, ad esempio connessioni in streaming, set di dati, [!DNL XDM Individual Profile]e [!DNL XDM ExperienceEvent].

Questa esercitazione richiede anche di aver completato il [Autenticazione in Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate a [!DNL Platform] API. Il completamento dell’esercitazione di autenticazione fornisce il valore per l’intestazione Autorizzazione richiesta da tutte le chiamate API in questa esercitazione. L’intestazione viene mostrata nelle chiamate di esempio come segue:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`

Tutte le richieste POST richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

## Creare una connessione in streaming

È innanzitutto necessario creare una connessione in streaming prima di poter avviare i dati in streaming su [!DNL Experience Platform]. Leggi la sezione [creare una connessione in streaming](./create-streaming-connection.md) guida per scoprire come creare una connessione in streaming.

Dopo aver registrato una connessione in streaming, in qualità di produttore dei dati, avrai a disposizione un URL univoco che può essere utilizzato per lo streaming dei dati in Platform.

## Trasmetti a un set di dati

L’esempio seguente mostra come inviare più messaggi a un set di dati specifico all’interno di una singola richiesta HTTP. Inserisci l’ID del set di dati nell’intestazione del messaggio per consentirne l’acquisizione diretta.

Puoi ottenere l’ID per un set di dati esistente utilizzando [!DNL Platform] Interfaccia utente o utilizzo di un’operazione di elenco nell’API. L’ID del set di dati si trova in [Experience Platform](https://platform.adobe.com) andando al **[!UICONTROL Set di dati]** , facendo clic sul set di dati per il quale desideri l’ID e copiando la stringa dal campo ID set di dati nel **[!UICONTROL Info]** scheda . Consulta la sezione [Panoramica del servizio catalogo](../../catalog/home.md) per informazioni su come recuperare i set di dati utilizzando l’API.

Invece di utilizzare un set di dati esistente, puoi creare un nuovo set di dati. Per piacere, leggi le [creare un set di dati utilizzando le API](../../catalog/api/create-dataset.md) per ulteriori informazioni sulla creazione di un set di dati utilizzando le API.

**Formato API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID della connessione in streaming creata. |

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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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

Una risposta corretta restituisce lo stato HTTP 207 (stato multiplo). La revisione del corpo della risposta fornisce ulteriori dettagli sul successo o il fallimento di ogni metodo eseguito nella richiesta. Viene restituita una risposta per ogni elemento della matrice dei messaggi di richiesta. Di seguito è riportato un esempio di risposta riuscita senza errori di messaggio:

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

Per ulteriori informazioni sui codici di stato, consulta la sezione [codici di risposta](#response-codes) nell’appendice di questa esercitazione.

## Identificare i messaggi non riusciti

Rispetto all’invio di una richiesta con un singolo messaggio, quando si invia una richiesta HTTP con più messaggi, ci sono fattori aggiuntivi da considerare, ad esempio: come identificare quando i dati non sono stati inviati, quali messaggi specifici non sono stati inviati e come è possibile recuperarli, e cosa succede ai dati che hanno esito positivo quando altri messaggi nella stessa richiesta non riescono.

Prima di procedere con questa esercitazione, è consigliabile rivedere prima la [recupero dei batch non riusciti](../quality/retrieve-failed-batches.md) guida.

### Invia payload di richiesta con messaggi validi e non validi

L&#39;esempio seguente mostra cosa accade quando il batch include messaggi validi e non validi.

Il payload della richiesta è un array di oggetti JSON che rappresenta l’evento nello schema XDM. Per la corretta convalida del messaggio è necessario soddisfare le seguenti condizioni:
- La `imsOrgId` nell’intestazione del messaggio deve corrispondere alla definizione di ingresso. Se il payload della richiesta non include un `imsOrgId` campo [!DNL Data Collection Core Service] (DCCS) aggiungerà il campo automaticamente.
- L&#39;intestazione del messaggio deve fare riferimento a uno schema XDM esistente creato nel [!DNL Platform] Interfaccia utente.
- La `datasetId` Il campo deve fare riferimento a un set di dati esistente in [!DNL Platform]e il relativo schema deve corrispondere allo schema fornito nel `header` all&#39;interno di ogni messaggio incluso nel corpo della richiesta.

**Formato API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID dell’entrata dati creata. |

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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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

Il payload della risposta include uno stato per ogni messaggio insieme a un GUID nel `xactionId` che può essere utilizzato per il tracciamento.

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
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        }
    ]
}
```

La risposta di esempio sopra mostra i messaggi di errore per la richiesta precedente. Confrontando questa risposta alla precedente risposta valida, puoi notare che la richiesta ha avuto un successo parziale, con un messaggio che è stato acquisito correttamente e tre messaggi che hanno causato un errore. Si noti che entrambe le risposte restituiscono un codice di stato &quot;207&quot;. Per ulteriori informazioni sui codici di stato, consulta la sezione [codici di risposta](#response-codes) nell’appendice di questa esercitazione.

Il primo messaggio è stato inviato correttamente a [!DNL Platform] e non è influenzato dai risultati degli altri messaggi. Di conseguenza, quando si tenta di inviare nuovamente i messaggi non riusciti, non è necessario includere nuovamente il messaggio.

Il secondo messaggio non è riuscito perché non era presente un corpo del messaggio. La richiesta di raccolta richiede che gli elementi del messaggio abbiano sezioni di intestazione e corpo valide. Se si aggiunge il codice seguente dopo l’intestazione nel secondo messaggio, la richiesta viene corretta e il secondo messaggio viene convalidato:

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

Il terzo messaggio non è riuscito a causa di un ID organizzazione non valido utilizzato nell&#39;intestazione. L&#39;organizzazione deve corrispondere al {CONNECTION_ID} a cui si sta tentando di inviare. Per determinare quale ID organizzazione corrisponde alla connessione in streaming che stai utilizzando, puoi eseguire una `GET inlet` richiesta utilizzando [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/). Vedi [recupero di una connessione in streaming](./create-streaming-connection.md#get-data-collection-url) per un esempio di come recuperare connessioni in streaming create in precedenza.

Il quarto messaggio non è riuscito perché non ha seguito lo schema XDM previsto. La `xdmSchema` inclusi nell’intestazione e nel corpo della richiesta non corrispondono allo schema XDM del `{DATASET_ID}`. La correzione dello schema nell’intestazione e nel corpo del messaggio consente di passare la convalida DCCS e di inviarla correttamente a [!DNL Platform]. Il corpo del messaggio deve essere aggiornato anche per corrispondere allo schema XDM del `{DATASET_ID}` per trasmettere la convalida in streaming su [!DNL Platform]. Per ulteriori informazioni su cosa accade ai messaggi che vengono correttamente inviati a Platform, consulta la sezione [conferma messaggi acquisiti](#confirm-messages-ingested) di questa esercitazione.

### Recupera messaggi non riusciti da [!DNL Platform]

I messaggi non riusciti sono identificati da un codice di stato dell’errore nell’array di risposta.
I messaggi non validi vengono raccolti e memorizzati in un batch di &quot;errore&quot; all’interno del set di dati specificato da `{DATASET_ID}`.

Leggi la sezione [recupero dei batch non riusciti](../quality/retrieve-failed-batches.md) guida per ulteriori informazioni sul recupero dei messaggi batch non riusciti.

## Conferma messaggi acquisiti

I messaggi che superano la convalida DCCS vengono trasmessi in streaming a [!DNL Platform]. On [!DNL Platform], i messaggi batch vengono testati tramite convalida in streaming prima di essere acquisiti nel [!DNL Data Lake]. Lo stato dei batch, con esito positivo o meno, viene visualizzato all’interno del set di dati specificato da `{DATASET_ID}`.

È possibile visualizzare lo stato dei messaggi batch a cui è stato eseguito il flusso [!DNL Platform] utilizzando [Interfaccia utente Experience Platform](https://platform.adobe.com) andando al **[!UICONTROL Set di dati]** , facendo clic sul set di dati a cui stai eseguendo lo streaming e controllando il **[!UICONTROL Attività set di dati]** scheda .

Messaggi in batch su cui viene passata la convalida in streaming [!DNL Platform] vengono acquisiti in [!DNL Data Lake]. I messaggi sono quindi disponibili per l’analisi o l’esportazione.

## Passaggi successivi

Ora che sai come inviare più messaggi in una singola richiesta e verificare quando i messaggi vengono correttamente acquisiti nel set di dati di destinazione, puoi iniziare a inviare in streaming i tuoi dati a [!DNL Platform]. Per una panoramica su come eseguire query e recuperare i dati acquisiti da [!DNL Platform], vedi [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) guida.

## Appendice

Questa sezione contiene informazioni supplementari per l’esercitazione.

### Codici di risposta

La tabella seguente mostra i codici di stato restituiti dai messaggi di risposta riusciti e non riusciti.

| Codice di stato | Descrizione |
| :---: | --- |
| 207 | Sebbene &#39;207&#39; sia utilizzato come codice di stato della risposta globale, il destinatario deve consultare il contenuto del corpo della risposta con più stati per ulteriori informazioni sul successo o il fallimento dell&#39;esecuzione del metodo. Il codice di risposta viene utilizzato in situazioni di successo, successo parziale e anche in situazioni di errore. |
| 400 | C&#39;è stato un problema con la richiesta. Per un messaggio di errore più specifico, consulta il corpo della risposta (ad esempio, nel payload del messaggio mancavano i campi obbligatori o il formato sconosciuto xdm del messaggio). |
| 401 | Non autorizzato: richiesta di autorizzazione mancante. Viene restituito solo per gli ingressi che hanno abilitato l’autenticazione. |
| 403 | Non autorizzato: Il token di autorizzazione fornito non è valido o è scaduto. Viene restituito solo per gli ingressi che hanno abilitato l’autenticazione. |
| 413 | Payload troppo grande : generato quando la richiesta di payload totale è maggiore di 1 MB. |
| 429 | Troppe richieste entro la durata di tempo specificata. |
| 500 | Errore durante l&#39;elaborazione del payload. Consulta il corpo della risposta per un messaggio di errore più specifico (ad esempio, schema payload del messaggio non specificato o non corrispondente alla definizione XDM in [!DNL Platform]). |
| 503 | Il servizio non è attualmente disponibile. I clienti devono riprovare almeno 3 volte utilizzando una strategia di back-off esponenziale. |
