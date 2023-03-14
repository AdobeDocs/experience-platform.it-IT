---
title: Creare una nuova specifica di connessione per Streaming SDK utilizzando l’API del servizio Flusso
description: Il documento seguente descrive come creare una specifica di connessione utilizzando l’API del servizio Flusso e integrare una nuova origine tramite Origini self-service.
hide: true
hidefromtoc: true
source-git-commit: 6b78ed695bca5912c9af4371a8423fdcd7471bde
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 1%

---

# Creare una nuova specifica di connessione utilizzando [!DNL Flow Service] API

Una specifica di connessione rappresenta la struttura di un&#39;origine. Contiene informazioni sui requisiti di autenticazione di una sorgente, definisce come i dati sorgente possono essere esplorati e ispezionati e fornisce informazioni sugli attributi di una determinata sorgente. Il `/connectionSpecs` endpoint nella [!DNL Flow Service] API consente di gestire in modo programmatico le specifiche di connessione all’interno dell’organizzazione.

Nel documento seguente vengono descritti i passaggi necessari per creare una specifica di connessione utilizzando [!DNL Flow Service] e integrano una nuova origine tramite Origini self-service (Streaming SDK).

## Introduzione

Prima di continuare, controlla [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Raccogli artefatti

Per creare una nuova origine di streaming con Origini self-service, devi prima coordinarti con Adobe, richiedere un archivio Git privato e allinearti con Adobe sui dettagli relativi all’etichetta, alla descrizione, alla categoria e all’icona per la tua origine.

Una volta fornito, devi strutturare l’archivio Git privato nel modo seguente:

* Origini
   * {your_source}
      * Artefatti
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| Artefatti (nomi file) | Descrizione | Esempio |
| --- | --- | --- |
| {your_source} | Nome della sorgente. Questa cartella deve contenere tutti gli artefatti relativi alla tua origine, all’interno dell’archivio Git privato. | `medallia` |
| {your_source}-category.txt | Categoria a cui appartiene l&#39;origine, formattata come file di testo. **Nota**: se ritieni che la tua sorgente non rientri in nessuna delle categorie precedenti, contatta il rappresentante del tuo Adobe per discutere. | `medallia-category.txt` All’interno del file, specifica la categoria dell’origine, ad esempio: `streaming`. |
| {your_source}-description.txt | Breve descrizione dell’origine. | [!DNL Medallia] è l’origine dell’automazione di marketing che puoi utilizzare per portare [!DNL Medallia] dati di Experience Platform. |
| {your_source}-icon.svg | Immagine da utilizzare per rappresentare la tua origine nel catalogo delle sorgenti di Experience Platform. Questa icona deve essere un file SVG. |
| {your_source}-label.txt | Il nome dell’origine così come dovrebbe essere visualizzato nel catalogo delle origini Experienci Platform. | Medallia |
| {your_source}-connectionSpec.json | Un file JSON che contiene la specifica di connessione dell’origine. Questo file non è inizialmente necessario in quanto verrà compilata la specifica di connessione durante il completamento di questa guida. | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>Durante il periodo di test della specifica di connessione, al posto dei valori chiave, puoi utilizzare `text` nella specifica di connessione.

Dopo aver aggiunto i file necessari all’archivio Git privato, devi creare una richiesta di pull (PR), ad Adobe da rivedere. Quando la PR viene approvata e unita, riceverai un ID che può essere utilizzato per la specifica di connessione per fare riferimento all&#39;etichetta, alla descrizione e all&#39;icona della tua sorgente.

Quindi, segui i passaggi descritti di seguito per configurare le specifiche di connessione. Per ulteriori informazioni sulle diverse funzionalità che è possibile aggiungere all’origine, come la pianificazione avanzata, lo schema personalizzato o diversi tipi di impaginazione, consulta la guida su [configurazione delle specifiche di origine](../config/sourcespec.md).

## Copia modello di specifica di connessione

Dopo aver raccolto gli artefatti richiesti, copia e incolla il modello di specifica di connessione riportato di seguito nell’editor di testo desiderato, quindi aggiorna gli attributi tra parentesi `{}` con informazioni rilevanti per la tua origine specifica.

```json
{
  "name": "generic-streaming",
  "type": "generic-streaming",
  "description": "{DESCRIPTION}",
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "version": "1.0",
  "attributes": {
    "category": "Streaming",
    "isSource": true,
    "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
    "uiAttributes": {
      "apiFeatures": {
        "updateSupported": false
      }
    }
  },
  "authSpec": [],
  "name": "generic-streaming",
  "permissionsInfo": {
    "view": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "sourceSpec": {
    "attributes": {
      "authRequired": false,
      "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
        "isSource": true,
        "monitoringSupported": false,
        "category": {
          "key": "streaming"
        },
        "icon": {
          "key": "generic"
        },
        "description": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "label": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "frequency": {
          "text": "Generic Streaming"
        }
      }
    }
  },
  "exploreSpec": {
    "type": "StreamingConnection"
  }
}
```

## Creare una specifica di connessione {#create}

Dopo aver acquisito il modello di specifica di connessione, è ora possibile iniziare a creare una nuova specifica di connessione inserendo i valori appropriati che corrispondono all&#39;origine.

Una specifica di connessione può essere divisa in due parti distinte: le specifiche di origine e le specifiche di esplorazione.

Per ulteriori informazioni sulle sezioni di una specifica di connessione, vedere i seguenti documenti:

* [Configurare le specifiche di origine](../config/sourcespec.md)
* [Configurare le specifiche di esplorazione](../config/explorespec.md)

Con le informazioni aggiornate sulla specifica, è possibile sottomettere la nuova specifica di connessione effettuando una richiesta POST al `/connectionSpecs` endpoint del [!DNL Flow Service] API.

**Formato API**

```http
POST /connectionSpecs
```

**Richiesta**

La seguente richiesta è un esempio di specifica di connessione completamente creata per un’origine di streaming:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "generic-streaming",
      "type": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "attributes": {
          "category": "Streaming",
          "isSource": true,
          "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
          "uiAttributes": {
            "apiFeatures": {
              "updateSupported": false
            }
          }
        },
        "authSpec": [],
        "name": "generic-streaming",
        "permissionsInfo": {
          "view": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "read"
              ]
            }
          ],
          "manage": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "write"
              ]
            }
          ]
        },
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "sourceSpec": {
          "attributes": {
            "uiAttributes": {
              "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
              "isSource": true,
              "monitoringSupported": false,
              "category": {
                "key": "streaming"
              },
              "icon": {
                "key": "Generic-Streaming"
              },
              "description": {
                "text": "Generic Streaming Connector"
              },
              "label": {
                "text": "Generic"
              },
              "frequency": {
                "text": "streaming"
              }
            }
          }
        },
        "exploreSpec": {
          "type": "StreamingConnection"
          },
        "type": "generic-streaming",
        "version": "1.0"
      }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce la specifica di connessione appena creata, inclusa la relativa specifica univoca `id`.

```json
{
  "items": [
    {
      "id": "bdb5b792-451b-42de-acf8-15f3195821de",
      "createdAt": 1667536504101,
      "updatedAt": 1667536504101,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{CREATED_CLIENT}",
      "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName": "prod",
      "imsOrgId": "{ORG_ID}",
      "name": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "type": "generic-streaming",
      "sourceSpec": {
        "attributes": {
          "authRequired": false,
          "uiAttributes": {
            "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
            "isSource": true,
            "monitoringSupported": false,
            "category": {
              "key": "streaming"
            },
            "icon": {
              "key": "Generic-Streaming"
            },
            "description": {
              "text": "Generic Streaming Connector"
            },
            "label": {
              "text": "Generic"
            },
            "frequency": {
              "text": "streaming"
            }
          }
        }
      },
      "exploreSpec": {
        "type": "StreamingConnection"
      },
      "attributes": {
        "category": "Streaming",
        "isSource": true,
        "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": false
          }
        }
      },
      "permissionsInfo": {
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "read"
            ]
          }
        ],
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ]
      }
    }
  ]
}
```

## Passaggi successivi

Dopo aver creato una nuova specifica di connessione, è necessario aggiungerne l&#39;ID corrispondente a una specifica di flusso esistente. Guarda il tutorial su [aggiornamento delle specifiche di flusso](./update-flow-specs.md) per ulteriori informazioni.

Per apportare modifiche alla specifica di connessione creata, vedere l&#39;esercitazione su [aggiornamento delle specifiche di connessione](./update-connection-specs.md).
