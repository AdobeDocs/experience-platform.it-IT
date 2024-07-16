---
title: Creare una nuova specifica di connessione per Streaming SDK utilizzando l’API del servizio Flusso
description: Il documento seguente descrive come creare una specifica di connessione utilizzando l’API del servizio Flusso e integrare una nuova origine tramite Origini self-service.
exl-id: ad8f6004-4e82-49b5-aede-413d72a1482d
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---

# Creare una nuova specifica di connessione utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>L’SDK di streaming per origini self-service è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Una specifica di connessione rappresenta la struttura di un&#39;origine. Contiene informazioni sui requisiti di autenticazione di una sorgente, definisce come i dati sorgente possono essere esplorati e ispezionati e fornisce informazioni sugli attributi di una determinata sorgente. L&#39;endpoint `/connectionSpecs` nell&#39;API [!DNL Flow Service] consente di gestire in modo programmatico le specifiche di connessione all&#39;interno dell&#39;organizzazione.

Nel documento seguente vengono descritti i passaggi necessari per creare una specifica di connessione utilizzando l&#39;API [!DNL Flow Service] e integrare una nuova origine tramite Origini self-service (Streaming SDK).

## Introduzione

Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e per le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

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
| {your_source}-category.txt | Categoria a cui appartiene l&#39;origine, formattata come file di testo. **Nota**: se ritieni che la tua origine non rientri in nessuna delle categorie precedenti, contatta il rappresentante del tuo Adobe per discutere. | `medallia-category.txt` All&#39;interno del file, specificare la categoria dell&#39;origine, ad esempio: `streaming`. |
| {your_source}-description.txt | Breve descrizione dell’origine. | [!DNL Medallia] è l&#39;origine dell&#39;automazione di marketing che è possibile utilizzare per portare all&#39;Experience Platform [!DNL Medallia] dati. |
| {your_source}-icon.svg | Immagine da utilizzare per rappresentare la tua origine nel catalogo delle sorgenti di Experience Platform. Questa icona deve essere un file SVG. |
| {your_source}-label.txt | Il nome dell’origine così come dovrebbe essere visualizzato nel catalogo delle origini Experienci Platform. | Medallia |
| {your_source}-connectionSpec.json | Un file JSON che contiene la specifica di connessione dell’origine. Questo file non è inizialmente necessario in quanto verrà compilata la specifica di connessione durante il completamento di questa guida. | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>Durante il periodo di test della specifica di connessione, al posto dei valori chiave, è possibile utilizzare `text` nella specifica di connessione.

Dopo aver aggiunto i file necessari all’archivio Git privato, devi creare una richiesta di pull (PR), ad Adobe da rivedere. Quando la PR viene approvata e unita, riceverai un ID che può essere utilizzato per la specifica di connessione per fare riferimento all&#39;etichetta, alla descrizione e all&#39;icona della tua sorgente.

Quindi, segui i passaggi descritti di seguito per configurare le specifiche di connessione. Per ulteriori informazioni sulle diverse funzionalità che è possibile aggiungere all&#39;origine, ad esempio pianificazione avanzata, schema personalizzato o diversi tipi di impaginazione, consultare la guida alla [configurazione delle specifiche dell&#39;origine](../config/sourcespec.md).

## Copia modello di specifica di connessione

Dopo aver raccolto gli artefatti richiesti, copiare e incollare il modello di specifica di connessione seguente nell&#39;editor di testo desiderato, quindi aggiornare gli attributi tra parentesi `{}` con le informazioni relative all&#39;origine specifica.

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

Con le informazioni aggiornate sulla specifica, è possibile inviare la nuova specifica di connessione effettuando una richiesta POST all&#39;endpoint `/connectionSpecs` dell&#39;API [!DNL Flow Service].

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

In caso di esito positivo, la risposta restituisce la specifica di connessione appena creata, incluso il relativo `id` univoco.

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

Dopo aver creato una nuova specifica di connessione, è necessario aggiungerne l&#39;ID corrispondente a una specifica di flusso esistente. Per ulteriori informazioni, consulta il tutorial su [aggiornamento delle specifiche del flusso](./update-flow-specs.md).

Per apportare modifiche alla specifica di connessione creata, vedere l&#39;esercitazione [aggiornamento delle specifiche di connessione](./update-connection-specs.md).
