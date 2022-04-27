---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
title: Configurare le specifiche di origine per l'SDK di Origini
topic-legacy: overview
description: Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare l'SDK di Origini.
hide: true
hidefromtoc: true
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 9727f7b0e8eaae92c85f102e5e7bea018a2ee6de
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---

# Configurare la specifica di origine per l&#39;SDK Origini

Le specifiche di origine contengono informazioni specifiche per un&#39;origine, inclusi gli attributi relativi alla categoria, allo stato beta e all&#39;icona del catalogo di un&#39;origine. Contengono inoltre utili informazioni quali parametri URL, contenuto, intestazione e pianificazione. Le specifiche di origine descrivono anche lo schema dei parametri necessari per creare una connessione di origine da una connessione di base. Lo schema è necessario per creare una connessione di origine.

Consulta la sezione [appendice](#source-spec) per un esempio di specifica di origine compilata completamente.


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "protocols"
      },
      "icon": {
        "key": "genericRestIcon"
      },
      "description": {
        "key": "genericRestDescription"
      },
      "label": {
        "key": "genericRestLabel"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "HTTP method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "The query parameters in json format",
            }
          },
          "required": [
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "The header parameters in json format",
        },
        "contentPath": {
          "type": "object",
          "description": "The parameters required for main collection content.",
          "properties": {
            "path": {
              "description": "The path to the main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "The parameters required for the sub-array content.",
          "properties": {
            "path": {
              "description": "The path to the sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the  root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "The parameters required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "The pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "The limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "The number of records to fetch per page.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "The offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "The path to pointer property",
              "example": "$.paging.next"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "The parameters required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
}
```

| Proprietà | Descrizione | Esempio |
| --- | --- | --- |
| `sourceSpec.attributes` | Contiene informazioni sull’origine specifica dell’interfaccia utente o dell’API. |
| `sourceSpec.attributes.uiAttributes` | Visualizza informazioni sull’origine specifica dell’interfaccia utente. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Attributo booleano che indica se la sorgente richiede più feedback dai clienti per aggiungerla alla sua funzionalità. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Definisce la categoria dell&#39;origine. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Definisce l’icona utilizzata per il rendering dell’origine nell’interfaccia utente di Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Visualizza una breve descrizione dell’origine. |
| `sourceSpec.attributes.uiAttributes.label` | Visualizza l’etichetta da utilizzare per il rendering dell’origine nell’interfaccia utente di Platform. |
| `sourceSpec.attributes.spec.properties.urlParams` | Contiene informazioni sul percorso della risorsa URL, sul metodo e sui parametri di query supportati. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Definisce il percorso della risorsa da cui recuperare i dati. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Definisce il metodo HTTP da utilizzare per effettuare la richiesta alla risorsa di recuperare i dati. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Definisce i parametri di query supportati che possono essere utilizzati per aggiungere l’URL di origine quando si effettua una richiesta di recupero dati. **Nota**: Qualsiasi valore di parametro fornito dall&#39;utente deve essere formattato come segnaposto. Ad esempio: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` verrà aggiunto all’URL sorgente come: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Definisce le intestazioni che devono essere fornite nella richiesta HTTP all’URL di origine durante il recupero dei dati. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.contentPath` | Definisce il nodo che contiene l’elenco degli elementi necessari per l’acquisizione in Platform. Questo attributo deve seguire una sintassi di percorso JSON valida e puntare a un particolare array. | Consulta la sezione [appendice](#content-path) per un esempio della risorsa contenuta in un percorso di contenuto. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Percorso che punta ai record di raccolta da acquisire in Platform. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Questa proprietà ti consente di identificare elementi specifici della risorsa identificata nel percorso del contenuto che devono essere esclusi dall’acquisizione. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Questa proprietà consente di specificare in modo esplicito i singoli attributi che si desidera mantenere. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Questa proprietà consente di ignorare il valore del nome dell&#39;attributo specificato in `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Questa proprietà consente di appiattire due array e trasformare i dati delle risorse in una risorsa Platform. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Percorso che punta ai record della raccolta che desideri appiattire. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Questa proprietà ti consente di identificare elementi specifici della risorsa identificata nel percorso dell’entità che devono essere esclusi dall’acquisizione. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Questa proprietà consente di specificare in modo esplicito i singoli attributi che si desidera mantenere. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Questa proprietà consente di ignorare il valore del nome dell&#39;attributo specificato in `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Definisce i parametri o i campi che devono essere forniti per ottenere un collegamento alla pagina successiva dalla risposta della pagina corrente dell&#39;utente o durante la creazione di un URL della pagina successiva. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Visualizza il tipo di impaginazione supportato per l’origine. | <ul><li>`offset`: Questo tipo di impaginazione consente di analizzare i risultati specificando un indice dal punto in cui avviare la matrice risultante e un limite al numero di risultati restituiti.</li><li>`pointer`: Questo tipo di impaginazione consente di utilizzare un `pointer` per puntare a un particolare elemento che deve essere inviato con una richiesta. L&#39;impaginazione del tipo di puntatore richiede il percorso nel payload che punta alla pagina successiva</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Nome del limite attraverso il quale l’API può specificare il numero di record da recuperare in una pagina. | `limit` oppure `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Il numero di record da recuperare in una pagina. | `limit=10` oppure `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Nome dell&#39;attributo di offset. Questa opzione è necessaria se il tipo di impaginazione è impostato su `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Nome dell&#39;attributo del puntatore. Questo richiede il percorso json dell’attributo che indicherà la pagina successiva. Questa opzione è necessaria se il tipo di impaginazione è impostato su `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Contiene parametri che definiscono i formati di pianificazione supportati per la sorgente. I parametri di pianificazione includono `startTime` e `endTime`, che consente di impostare intervalli di tempo specifici per le esecuzioni batch, in modo che i record recuperati in una precedente esecuzione batch non vengano recuperati di nuovo. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Definisce il nome del parametro dell&#39;ora di inizio | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Definisce il nome del parametro del tempo di fine | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Definisce il formato supportato per il `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Definisce il formato supportato per il `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Definisce i parametri forniti dall’utente per recuperare i valori delle risorse. | Consulta la sezione [appendice](#user-input) per un esempio di parametri immessi dall’utente per `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Appendice {#appendix}

### Esempio di percorso del contenuto {#content-path}

Di seguito è riportato un esempio del contenuto del `contentPath` in una proprietà [!DNL MailChimp Campaigns] specifica di connessione.

```json
"contentPath": {
  "path": "$.members",
  "skipAttributes": [
    "_links",
    "total_items",
    "list_id"
  ],
  "overrideWrapperAttribute": "member"
}
```

### `spec.properties` esempio di input dell&#39;utente {#user-input}

Esempio di un `spec.properties` utilizzando [!DNL MailChimp Members] specifica di connessione.

In questo esempio, `listId` è fornito come parte `urlParams.path`. Se hai bisogno di recuperare `listId` da un cliente, devi anche definirlo come parte di `spec.properties`.


```json
"urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      }
"spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
```

### Esempio di specifica origine {#source-spec}

Di seguito è riportata una specifica di origine completata utilizzando [!DNL MailChimp Members]:

```json
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "marketingAutomation"
        },
        "icon": {
          "key": "mailchimpMembersIcon"
        },
        "description": {
          "key": "mailchimpMembersDescription"
        },
        "label": {
          "key": "mailchimpMembersLabel"
        }
      },
      "urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      },
      "contentPath": {
        "path": "$.members",
        "skipAttributes": [
          "_links",
          "total_items",
          "list_id"
        ],
        "overrideWrapperAttribute": "member"
      },
      "paginationParams": {
        "type": "OFFSET",
        "limitName": "count",
        "limitValue": "100",
        "offSetName": "offset"
      },
      "scheduleParams": {
        "scheduleStartParamName": "since_last_changed",
        "scheduleEndParamName": "before_last_changed",
        "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
        "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
  }
```

## Passaggi successivi

Con le specifiche di origine compilate, puoi procedere alla configurazione delle specifiche di esplorazione per la sorgente che desideri integrare in Platform. Visualizza il documento su [configurazione delle specifiche](./explorespec.md) per ulteriori informazioni.
