---
keywords: Experience Platform;home;argomenti popolari;streaming ingestion;acquisizione;streaming messaggi multipli;messaggi multipli;
solution: Experience Platform
title: Inviare più messaggi in una singola richiesta HTTP
type: Tutorial
description: Questo documento fornisce un tutorial per inviare più messaggi a Adobe Experience Platform all’interno di una singola richiesta HTTP utilizzando l’acquisizione in streaming.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 3ad5c06db07b360df255d3afb1c177cc5de613bb
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 1%

---

# Inviare più messaggi in una singola richiesta HTTP

Quando si inviano dati in streaming a Adobe Experience Platform, effettuare numerose chiamate HTTP può essere costoso. Ad esempio, invece di creare 200 richieste HTTP con payload da 1 KB, è molto più efficiente creare 1 richiesta HTTP con 200 messaggi di 1 KB ciascuno, con un singolo payload di 200 KB. Se utilizzato correttamente, il raggruppamento di più messaggi all&#39;interno di una singola richiesta è un modo eccellente per ottimizzare i dati inviati a [!DNL Experience Platform].

Questo documento fornisce un tutorial per inviare più messaggi a [!DNL Experience Platform] all&#39;interno di una singola richiesta HTTP utilizzando l&#39;acquisizione in streaming.

## Introduzione

Questo tutorial richiede una buona conoscenza di Adobe Experience Platform [!DNL Data Ingestion]. Prima di iniziare questo tutorial, consulta la seguente documentazione:

- [Panoramica sull&#39;acquisizione dei dati](../home.md): descrive i concetti fondamentali di [!DNL Experience Platform Data Ingestion], inclusi i metodi di acquisizione e i connettori dati.
- [Panoramica sull&#39;acquisizione in streaming](../streaming-ingestion/overview.md): flusso di lavoro e blocchi predefiniti per l&#39;acquisizione in streaming, ad esempio connessioni in streaming, set di dati, [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent].

Questo tutorial richiede inoltre di aver completato l&#39;esercitazione di autenticazione a Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) di [ per effettuare correttamente le chiamate alle API di [!DNL Platform]. Il completamento del tutorial sull’autenticazione fornisce il valore per l’intestazione Authorization richiesta da tutte le chiamate API in questo tutorial. L’intestazione viene visualizzata nelle chiamate di esempio come segue:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`

Tutte le richieste POST richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

## Creare una connessione in streaming

È necessario creare una connessione in streaming prima di poter avviare i dati in streaming a [!DNL Experience Platform]. Per informazioni su come creare una connessione in streaming, leggere la [guida alla creazione di una connessione in streaming](./create-streaming-connection.md).

Dopo aver registrato una connessione in streaming, in qualità di produttore di dati avrai un URL univoco che può essere utilizzato per inviare dati a Platform.

## Trasmetti a un set di dati

L’esempio seguente mostra come inviare più messaggi a un set di dati specifico all’interno di una singola richiesta HTTP. Inserisci l’ID del set di dati nell’intestazione del messaggio affinché il messaggio venga acquisito direttamente al suo interno.

È possibile ottenere l&#39;ID per un set di dati esistente utilizzando l&#39;interfaccia utente [!DNL Platform] o un&#39;operazione di elenco nell&#39;API. Per trovare l&#39;ID del set di dati in [Experience Platform](https://platform.adobe.com), vai alla scheda **[!UICONTROL Set di dati]**, fai clic sul set di dati per il quale desideri ottenere l&#39;ID e copia la stringa dal campo ID del set di dati nella scheda **[!UICONTROL Informazioni]**. Per informazioni su come recuperare i set di dati utilizzando l&#39;API, vedere [Panoramica di Catalog Service](../../catalog/home.md).

Invece di utilizzare un set di dati esistente, puoi crearne uno nuovo. Per ulteriori informazioni sulla creazione di un set di dati tramite API, leggere l&#39;esercitazione [Creare un set di dati utilizzando API](../../catalog/api/create-dataset.md).

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 207 (multistato). L’esame del corpo della risposta fornisce ulteriori dettagli sull’esito positivo o negativo di ciascun metodo eseguito nella richiesta. Viene restituita una risposta per ogni elemento della matrice dei messaggi di richiesta. Di seguito è riportato un esempio di risposta corretta senza errori di messaggio:

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

Per ulteriori informazioni sui codici di stato, vedere la tabella [codici di risposta](#response-codes) nell&#39;appendice di questa esercitazione.

## Identificare i messaggi non riusciti

Rispetto all’invio di una richiesta con un singolo messaggio, quando si invia una richiesta HTTP con più messaggi, ci sono fattori aggiuntivi da considerare, ad esempio: come identificare quando i dati non sono stati inviati, quali messaggi specifici non sono stati inviati e come è possibile recuperarli e cosa succede ai dati che hanno esito positivo quando altri messaggi nella stessa richiesta non riescono.

Prima di procedere con questa esercitazione, è consigliabile rivedere la guida [recupero dei batch non riusciti](../quality/retrieve-failed-batches.md).

### Invia payload di richiesta con messaggi validi e non validi

L’esempio seguente mostra cosa accade quando il batch include messaggi validi e non validi.

Il payload della richiesta è un array di oggetti JSON che rappresentano l’evento nello schema XDM. Per la corretta convalida del messaggio è necessario soddisfare le seguenti condizioni:
- Il campo `imsOrgId` nell&#39;intestazione del messaggio deve corrispondere alla definizione di ingresso. Se il payload della richiesta non include un campo `imsOrgId`, [!DNL Data Collection Core Service] (DCCS) aggiungerà automaticamente il campo.
- L&#39;intestazione del messaggio deve fare riferimento a uno schema XDM esistente creato nell&#39;interfaccia utente [!DNL Platform].
- Il campo `datasetId` deve fare riferimento a un set di dati esistente in [!DNL Platform] e il relativo schema deve corrispondere allo schema fornito nell&#39;oggetto `header` all&#39;interno di ogni messaggio incluso nel corpo della richiesta.

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

Il payload di risposta include uno stato per ogni messaggio insieme a un GUID in `xactionId` che può essere utilizzato per la traccia.

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

L’esempio di risposta riportato sopra mostra i messaggi di errore per la richiesta precedente. Confrontando questa risposta con la precedente risposta valida, puoi notare che la richiesta ha avuto un successo parziale, con un messaggio acquisito correttamente e tre messaggi con conseguente errore. Entrambe le risposte restituiscono il codice di stato &quot;207&quot;. Per ulteriori informazioni sui codici di stato, vedere la tabella [codici di risposta](#response-codes) nell&#39;appendice di questa esercitazione.

Il primo messaggio è stato inviato correttamente a [!DNL Platform] e non è influenzato dai risultati degli altri messaggi. Di conseguenza, quando si tenta di inviare nuovamente i messaggi non riusciti, non è necessario includere nuovamente il messaggio.

Il secondo messaggio non è riuscito perché manca il corpo del messaggio. La richiesta di raccolta prevede che gli elementi del messaggio abbiano sezioni di intestazione e corpo valide. L’aggiunta del seguente codice dopo l’intestazione nel secondo messaggio corregge la richiesta, consentendo al secondo messaggio di superare la convalida:

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

Il terzo messaggio non è riuscito a causa di un ID organizzazione non valido utilizzato nell’intestazione. L&#39;organizzazione deve corrispondere a {CONNECTION_ID} a cui si sta tentando di pubblicare. Per determinare quale ID organizzazione corrisponde alla connessione streaming in uso, è possibile eseguire una richiesta `GET inlet` utilizzando [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/). Per un esempio su come recuperare le connessioni streaming create in precedenza, vedere [recupero di una connessione streaming](./create-streaming-connection.md#get-data-collection-url).

Il quarto messaggio non è riuscito perché non ha seguito lo schema XDM previsto. I `xdmSchema` inclusi nell&#39;intestazione e nel corpo della richiesta non corrispondono allo schema XDM di `{DATASET_ID}`. La correzione dello schema nell&#39;intestazione e nel corpo del messaggio consente di superare la convalida DCCS e l&#39;invio a [!DNL Platform]. È inoltre necessario aggiornare il corpo del messaggio in modo che corrisponda allo schema XDM di `{DATASET_ID}` per consentire il passaggio della convalida in streaming su [!DNL Platform]. Per ulteriori informazioni su ciò che accade ai messaggi che vengono inviati correttamente a Platform, consulta la sezione [messaggi di conferma acquisiti](#confirm-messages-ingested) di questa esercitazione.

### Recupera messaggi non riusciti da [!DNL Platform]

I messaggi non riusciti sono identificati da un codice di stato di errore nell’array di risposta.
I messaggi non validi vengono raccolti e memorizzati in un batch di &quot;errore&quot; all&#39;interno del set di dati specificato da `{DATASET_ID}`.

Per ulteriori informazioni sul recupero dei messaggi batch non riusciti, leggere la [guida recupero dei batch non riusciti](../quality/retrieve-failed-batches.md).

## Conferma messaggi acquisiti

I messaggi che superano la convalida DCCS vengono inviati a [!DNL Platform]. Il [!DNL Platform], i messaggi batch vengono testati tramite convalida in streaming prima di essere acquisiti in [!DNL Data Lake]. Lo stato dei batch, con o senza esito positivo, viene visualizzato nel set di dati specificato da `{DATASET_ID}`.

Puoi visualizzare lo stato dei messaggi batch che hanno completato correttamente il flusso a [!DNL Platform] utilizzando la [interfaccia utente Experience Platform](https://platform.adobe.com) andando alla scheda **[!UICONTROL Set di dati]**, facendo clic sul set di dati a cui stai eseguendo il flusso e controllando la scheda **[!UICONTROL Attività set di dati]**.

I messaggi batch che superano la convalida in streaming su [!DNL Platform] vengono acquisiti in [!DNL Data Lake]. I messaggi sono quindi disponibili per l’analisi o l’esportazione.

## Passaggi successivi

Ora che sai come inviare più messaggi in un&#39;unica richiesta e verificare quando i messaggi vengono correttamente acquisiti nel set di dati di destinazione, puoi iniziare a inviare i dati in streaming a [!DNL Platform]. Per una panoramica su come eseguire query e recuperare dati acquisiti da [!DNL Platform], vedere la guida di [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md).

## Appendice

Questa sezione contiene informazioni supplementari per l’esercitazione.

### Codici di risposta

Nella tabella seguente sono riportati i codici di stato restituiti dai messaggi di risposta riusciti e non riusciti.

| Codice di stato | Descrizione |
| :---: | --- |
| 207 | Sebbene &quot;207&quot; sia utilizzato come codice di stato della risposta complessiva, il destinatario deve consultare il contenuto del corpo della risposta con più stati per ulteriori informazioni sull’esecuzione corretta o non riuscita del metodo. Il codice di risposta viene utilizzato in caso di successo parziale e anche in situazioni di errore. |
| 400 | Si è verificato un problema con la richiesta. Per un messaggio di errore più specifico, vedi il corpo della risposta (ad esempio, nel payload del messaggio mancavano campi obbligatori o il messaggio era in formato xdm sconosciuto). |
| 401 | Non autorizzato: nella richiesta manca un’intestazione di autorizzazione valida. Questa opzione viene restituita solo per gli ingressi per i quali è abilitata l’autenticazione. |
| 403 | Non autorizzato: il token di autorizzazione fornito non è valido o è scaduto. Questa opzione viene restituita solo per gli ingressi per i quali è abilitata l’autenticazione. |
| 413 | Payload troppo grande: generato quando la richiesta di payload totale è maggiore di 1 MB. |
| 429 | Troppe richieste entro la durata specificata. |
| 500 | Errore nell’elaborazione del payload. Per un messaggio di errore più specifico, vedere il corpo della risposta (ad esempio, schema di payload del messaggio non specificato o non corrispondente alla definizione XDM in [!DNL Platform]). |
| 503 | Il servizio non è attualmente disponibile. I clienti devono riprovare almeno 3 volte utilizzando una strategia di back-off esponenziale. |
