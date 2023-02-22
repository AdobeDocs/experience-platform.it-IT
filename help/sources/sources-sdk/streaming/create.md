---
title: Creare una nuova specifica di connessione per l’SDK Streaming utilizzando l’API del servizio di flusso
description: Il seguente documento fornisce passaggi su come creare una specifica di connessione utilizzando l’API del servizio di flusso e integrare una nuova origine tramite Origini self-service.
hide: true
hidefromtoc: true
source-git-commit: 6b78ed695bca5912c9af4371a8423fdcd7471bde
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# Crea una nuova specifica di connessione utilizzando [!DNL Flow Service] API

Una specifica di connessione rappresenta la struttura di un&#39;origine. Contiene informazioni sui requisiti di autenticazione di un&#39;origine, definisce come esplorare e ispezionare i dati di origine e fornisce informazioni sugli attributi di una determinata origine. La `/connectionSpecs` punto finale [!DNL Flow Service] L’API ti consente di gestire in modo programmatico le specifiche di connessione all’interno dell’organizzazione.

Il documento seguente illustra i passaggi necessari per creare una specifica di connessione utilizzando [!DNL Flow Service] e integra una nuova sorgente tramite Sorgenti self-service (Streaming SDK).

## Introduzione

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Raccogli artifact

Per creare una nuova origine di streaming utilizzando Origini self-service, è innanzitutto necessario coordinarsi con Adobe, richiedere un archivio Git privato e allinearsi con Adobe sui dettagli relativi all’etichetta, alla descrizione, alla categoria e all’icona della sorgente.

Una volta fornito, devi strutturare il tuo archivio Git privato come segue:

* Origini
   * {your_source}
      * Artifact
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| Artifact (nomi di file) | Descrizione | Esempio |
| --- | --- | --- |
| {your_source} | Nome della sorgente. Questa cartella deve contenere tutti gli artefatti relativi all’origine, all’interno dell’archivio Git privato. | `medallia` |
| {your_source}-category.txt | La categoria a cui appartiene l&#39;origine, formattata come file di testo. **Nota**: Se ritieni che la tua fonte non rientri in nessuna delle categorie di cui sopra, contatta il tuo rappresentante di Adobe per discutere. | `medallia-category.txt` All’interno del file, specifica la categoria della sorgente, ad esempio: `streaming`. |
| {your_source}-description.txt | Breve descrizione della fonte. | [!DNL Medallia] è una sorgente di automazione di marketing che può essere utilizzata per [!DNL Medallia] dati ad Experience Platform. |
| {your_source}-icon.svg | Immagine da utilizzare per rappresentare la tua origine nel catalogo origini Experienci Platform. Questa icona deve essere un file SVG. |
| {your_source}-label.txt | Il nome della sorgente come dovrebbe apparire nel catalogo delle sorgenti di Experience Platform. | Medallia |
| {your_source}-connectionSpec.json | Un file JSON contenente le specifiche di connessione della tua origine. Questo file non è inizialmente necessario in quanto verranno compilate le specifiche di connessione durante il completamento di questa guida. | `medallia-connectionSpec.json` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>Durante il periodo di prova della specifica di connessione, al posto dei valori chiave, è possibile utilizzare `text` nella specifica di connessione.

Dopo aver aggiunto i file necessari all’archivio Git privato, devi quindi creare una richiesta di pull (PR) da rivedere, ad Adobe. Quando il PR viene approvato e unito, ti verrà fornito un ID che può essere utilizzato per la specifica di connessione per fare riferimento all’etichetta, alla descrizione e all’icona della tua origine.

Quindi, segui i passaggi descritti di seguito per configurare le specifiche di connessione. Per ulteriori informazioni sulle diverse funzionalità che è possibile aggiungere all’origine, ad esempio la pianificazione avanzata, lo schema personalizzato o diversi tipi di impaginazione, consulta la guida in [configurazione delle specifiche di origine](../config/sourcespec.md).

## Copia modello di specifica di connessione

Una volta raccolti gli artefatti richiesti, copia e incolla il modello di specifica di connessione sottostante all’editor di testo desiderato, quindi aggiorna gli attributi tra parentesi `{}` con informazioni relative alla tua origine specifica.

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

Una volta acquisito il modello di specifica di connessione, è ora possibile iniziare a creare una nuova specifica di connessione compilando i valori appropriati corrispondenti all&#39;origine.

Una specifica di connessione può essere divisa in due parti distinte: le specifiche di origine e le specifiche di esplorazione.

Per ulteriori informazioni sulle sezioni di una specifica di connessione, vedere i documenti seguenti:

* [Configurare le specifiche di origine](../config/sourcespec.md)
* [Configurare la specifica di esplorazione](../config/explorespec.md)

Con le informazioni sulle specifiche aggiornate, puoi inviare la nuova specifica di connessione effettuando una richiesta di POST al `/connectionSpecs` punto finale [!DNL Flow Service] API.

**Formato API**

```http
POST /connectionSpecs
```

**Richiesta**

La seguente richiesta è un esempio di specifica di connessione completamente creata per una sorgente in streaming:

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

Una risposta corretta restituisce la specifica di connessione appena creata, inclusa la relativa univoca `id`.

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

Dopo aver creato una nuova specifica di connessione, è necessario aggiungere l’ID della specifica di connessione corrispondente a una specifica di flusso esistente. Guarda l’esercitazione su [aggiornamento delle specifiche di flusso](./update-flow-specs.md) per ulteriori informazioni.

Per apportare modifiche alla specifica di connessione creata, consulta l’esercitazione su [aggiornamento delle specifiche di connessione](./update-connection-specs.md).
