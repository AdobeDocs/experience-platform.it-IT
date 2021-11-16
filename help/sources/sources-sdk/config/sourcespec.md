---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
title: Configurare le specifiche di autenticazione per l'SDK di Origini
topic-legacy: overview
description: Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare l'SDK di Origini.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '876'
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
        "key": "{CATEGORY}"
      },
      "icon": {
        "key": "{ICON}"
      },
      "description": {
        "key": "{DESCRIPTION}"
      },
      "label": {
        "key": "{LABEL}"
      }
    },
    "urlParams": {
      "path": "{RESOURCE_PATH}",
      "method": "{GET_or_POST}",
      "queryParams": "{QUERY_PARAMS}"
    },
    "headerParams": "{HEADER_VALUES}",
    "bodyParams": "{BODY_PARAMS_USED_IF_METHOD_IS_POST}",
    "contentPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "explodeEntityPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "paginationParams": {
      "type": "{OFFSET_OR_POINTER}",
      "limitName": "{NUMBER_OF_RECORDS_ATTRIBUTE_NAME}",
      "limitValue": "{NUMBER_OF_RECORDS_PER_PAGE}",
      "offSetName": "{OFFSET_ATTRIBUTE_NAME_REQUIRED_IN_CASE_OF_OFFSET BASED_PAGINATION}",
      "pointerName": "{POINTER_PATH_REQUIRED_IN__CASE_OF_POINTER BASED_PAGINATION}"
    },
    "scheduleParams": {
      "scheduleStartParamName": "{START_TIME_PARAMETER_NAME}",
      "scheduleEndParamName": "{END_TIME_PARAMETER_NAME}",
      "scheduleStartParamFormat": "{DATE_TIME_FORMAT_FOR_START_TIME}",
      "scheduleEndParamFormat": "{END_TIME_FORMAT_FOR_START_TIME}"
    }
  },
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define user input parameters to fetch resource values.",
    "properties": "{USER_INPUT}"
  }
}
```

| Proprietà | Descrizione | Esempio |
| --- | --- | --- |
| `sourceSpec.attributes` | Contiene informazioni sull’origine specifica dell’interfaccia utente o dell’API. |
| `sourceSpec.attributes.uiAttributes` | Visualizza informazioni sull’origine specifica dell’interfaccia utente. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Attributo booleano che indica se la sorgente richiede più feedback dai clienti per aggiungerla alla sua funzionalità. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Definisce la categoria dell&#39;origine. | <ul><li>`advertising`</li><li>`cloud storage`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li><li>`streaming`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Definisce l’icona utilizzata per il rendering dell’origine nell’interfaccia utente di Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Visualizza una breve descrizione dell’origine. |
| `sourceSpec.attributes.uiAttributes.label` | Visualizza l’etichetta da utilizzare per il rendering dell’origine nell’interfaccia utente di Platform. |
| `sourceSpec.attributes.urlParams` | Contiene informazioni sul percorso della risorsa URL, sul metodo e sui parametri di query supportati. |
| `sourceSpec.attributes.urlParams.path` | Definisce il percorso della risorsa da cui recuperare i dati. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.urlParams.method` | Definisce il metodo HTTP da utilizzare per effettuare la richiesta alla risorsa di recuperare i dati. | `GET`, `POST` |
| `sourceSpec.attributes.urlParams.queryParams` | Definisce i parametri di query supportati che possono essere utilizzati per aggiungere l’URL di origine quando si effettua una richiesta di recupero dati. I parametri della query devono essere virgola (`,`) coppie chiave-valore separate. **Nota**: Qualsiasi valore di parametro fornito dall&#39;utente deve essere formattato come segnaposto. Ad esempio: `${USER_PARAMETER}`. | `exclude_fields=emails._links,id=${id}` |
| `sourceSpec.attributes.headerParams` | Definisce la virgola (`,`) intestazioni separate che devono essere fornite nella richiesta HTTP all&#39;URL di origine durante il recupero dei dati. | `Content-Type=application/json,foo=bar&userHeader={{USER_HEADER_VALUE}}` |
| `sourceSpec.attributes.bodyParams` | Definisce i parametri del corpo richiesti. Questa proprietà viene utilizzata solo se `urlParams.method` è impostato su `POST`. |
| `sourceSpec.attributes.contentPath` | Definisce il nodo che contiene l’elenco degli elementi necessari per l’acquisizione in Platform. Questo attributo deve seguire una sintassi di percorso JSON valida e puntare a un particolare array. | Consulta la sezione [appendice](#content-path) per un esempio della risorsa contenuta in un percorso di contenuto. |
| `sourceSpec.attributes.contentPath.path` | Percorso che punta ai record di raccolta da acquisire in Platform. | `$.emails` |
| `sourceSpec.attributes.contentPath.skipAttributes` | Questa proprietà ti consente di identificare elementi specifici della risorsa identificata nel percorso del contenuto che devono essere esclusi dall’acquisizione. |
| `sourceSpec.attributes.contentPath.overrideWrapperAttribute` | Questa proprietà consente di ignorare il valore del nome dell&#39;attributo specificato in `contentPath`. |
| `sourceSpec.attributes.contentPath.keepAttributes` | Questa proprietà ti consente di specificare in modo esplicito i singoli attributi da mappare. |
| `sourceSpec.attributes.explodeEntityPath` | Questa proprietà consente di appiattire due array e trasformare i dati delle risorse in una risorsa Platform. |
| `sourceSpec.attributes.explodeEntityPath.path` | Percorso che punta ai record della raccolta che desideri appiattire. | `$.email.activity` |
| `sourceSpec.attributes.explodeEntityPath.skipAttributes` | Questa proprietà ti consente di identificare elementi specifici della risorsa identificata nel percorso dell’entità che devono essere esclusi dall’acquisizione. |
| `sourceSpec.attributes.explodeEntityPath.overrideWrapperAttribute` | Questa proprietà consente di ignorare il valore del nome dell&#39;attributo specificato in `explodeEntityPath`. |
| `sourceSpec.attributes.explodeEntityPath.keepAttributes` | Questa proprietà ti consente di specificare in modo esplicito i singoli attributi da mappare. |
| `sourceSpec.attributes.paginationParams` | Definisce i parametri o i campi che devono essere forniti per ottenere un collegamento alla pagina successiva dalla risposta della pagina corrente dell&#39;utente o durante la creazione di un URL della pagina successiva. |
| `sourceSpec.attributes.paginationParams.type` | Visualizza il tipo di impaginazione supportato per l’origine. | <ul><li>`offset`: Questo tipo di impaginazione consente di analizzare i risultati specificando un indice dal punto in cui avviare la matrice risultante e un limite al numero di risultati restituiti.</li><li>`pointer`: Questo tipo di impaginazione consente di utilizzare un `pointer` per puntare a un particolare elemento che deve essere inviato con una richiesta. L&#39;impaginazione del tipo di puntatore richiede il percorso nel payload che punta alla pagina successiva</li></ul> |
| `sourceSpec.attributes.paginationParams.limitName` | Nome del limite attraverso il quale l’API può specificare il numero di record da recuperare in una pagina. | `count` |
| `sourceSpec.attributes.paginationParams.limitValue` | Il numero di record da recuperare in una pagina. | `100` |
| `sourceSpec.attributes.paginationParams.offSetName` | Nome dell&#39;attributo di offset. Questa opzione è necessaria se il tipo di impaginazione è impostato su `offset`. | `offset` |
| `sourceSpec.attributes.paginationParams.pointerName` | Nome dell&#39;attributo del puntatore. Questo richiede il percorso json dell’attributo che indicherà la pagina successiva. Questa opzione è necessaria se il tipo di impaginazione è impostato su `pointer`. | `pointer` |
| `sourceSpec.attributes.scheduleParams` | Contiene parametri che definiscono i formati di pianificazione supportati per la sorgente. I parametri di pianificazione includono `startTime` e `endTime`, che consente di impostare intervalli di tempo specifici per le esecuzioni batch, in modo che i record recuperati in una precedente esecuzione batch non vengano recuperati di nuovo. |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamName` | Definisce il nome del parametro dell&#39;ora di inizio | `since_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamName` | Definisce il nome del parametro del tempo di fine | `before_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamFormat` | Definisce il formato supportato per il `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamFormat` | Definisce il formato supportato per il `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
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