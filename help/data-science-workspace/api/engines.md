---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti popolari;motori;sensei machine learning api
solution: Experience Platform
title: Endpoint API per i motori
description: I motori sono le basi dei modelli di apprendimento automatico in Data Science Workspace. Contengono algoritmi di apprendimento automatico che risolvono problemi specifici, pipeline di funzioni per eseguire attività di progettazione delle funzioni o entrambi.
role: Developer
exl-id: 7c670abd-636c-47d8-bd8c-5ce0965ce82f
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 2%

---

# Endpoint &quot;engines&quot;

I motori sono le basi dei modelli di apprendimento automatico in Data Science Workspace. Contengono algoritmi di apprendimento automatico che risolvono problemi specifici, pipeline di funzioni per eseguire attività di progettazione delle funzioni o entrambi.

## Cercare il registro Docker

>[!TIP]
>
>Se non disponi di un URL Docker, visita l&#39;esercitazione [Package source files into a ricetta](../models-recipes/package-source-files-recipe.md) per una procedura dettagliata sulla creazione di un URL host Docker.

Le credenziali del Registro di sistema Docker sono necessarie per caricare un pacchetto di file di composizione, inclusi l’URL host Docker, il nome utente e la password. Per cercare queste informazioni, effettua la seguente richiesta GET:

**Formato API**

```https
GET /engines/dockerRegistry
```

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli del registro Docker, inclusi l&#39;URL Docker (`host`), il nome utente (`username`) e la password (`password`).

>[!NOTE]
>
>La password Docker viene modificata ogni volta che `{ACCESS_TOKEN}` viene aggiornato.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Creare un motore utilizzando gli URL Docker {#docker-image}

Per creare un motore, devi eseguire una richiesta POST fornendo i relativi metadati e un URL Docker che faccia riferimento a un’immagine Docker in moduli multipart.

**Formato API**

```https
POST /engines
```

**Richiedi Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "A name for this Engine",
        "description": "A description for this Engine",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Il nome desiderato per il motore. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzato nell’interfaccia utente come nome della ricetta. |
| `description` | Descrizione facoltativa del motore. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzato nell’interfaccia utente come descrizione della ricetta. Questa proprietà è obbligatoria. Se non si desidera fornire una descrizione, impostarne il valore su una stringa vuota. |
| `type` | Tipo di esecuzione del motore. Questo valore corrisponde al linguaggio su cui è basata l’immagine Docker e può essere &quot;Python&quot;, &quot;R&quot; o &quot;Tensorflow&quot;. |
| `algorithm` | Stringa che specifica il tipo di algoritmo di apprendimento automatico. I tipi di algoritmo supportati includono &quot;Classification&quot;, &quot;Regressione&quot; o &quot;Custom&quot;. |
| `artifacts.default.image.location` | Posizione dell’immagine Docker collegata da un URL Docker. |
| `artifacts.default.image.executionType` | Tipo di esecuzione del motore. Questo valore corrisponde al linguaggio su cui è basata l’immagine Docker e può essere &quot;Python&quot;, &quot;R&quot; o &quot;Tensorflow&quot;. |

**Richiedi PySpark/Scala**

Quando si effettua una richiesta per le ricette PySpark, `executionType` e `type` sono &quot;PySpark&quot;. Quando si effettua una richiesta per le ricette Scala, `executionType` e `type` sono &quot;Spark&quot;. L’esempio di ricetta Scala che segue utilizza Spark:

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "Spark retail sales recipe",
    "description": "A description for this Engine",
    "type": "Spark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "Spark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Il nome desiderato per il motore. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzato nell’interfaccia utente come nome della ricetta. |
| `description` | Descrizione facoltativa del motore. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzato nell’interfaccia utente come descrizione della ricetta. Questa proprietà è obbligatoria. Se non si desidera fornire una descrizione, impostarne il valore su una stringa vuota. |
| `type` | Tipo di esecuzione del motore. Questo valore corrisponde alla lingua su cui viene generata l’immagine Docker. Il valore può essere impostato su Spark o PySpark. |
| `mlLibrary` | Campo richiesto per la creazione di motori per le ricette PySpark e Scala. Questo campo deve essere impostato su `databricks-spark`. |
| `artifacts.default.image.location` | Percorso dell’immagine Docker. È supportato solo Azure ACR o Dockerhub pubblico (non autenticato). |
| `artifacts.default.image.executionType` | Tipo di esecuzione del motore. Questo valore corrisponde alla lingua su cui viene generata l’immagine Docker. Può essere &quot;Spark&quot; o &quot;PySpark&quot;. |

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli del motore appena creato, incluso il relativo identificatore univoco (`id`). L’esempio di risposta che segue è per un motore Python. Tutte le risposte del motore seguono questo formato:

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Creare un motore di pipeline delle funzioni utilizzando gli URL Docker {#feature-pipeline-docker}

Per creare un motore di pipeline di funzioni, devi eseguire una richiesta POST mentre fornisci i relativi metadati e un URL Docker che fa riferimento a un’immagine Docker.

**Formato API**

```https
POST /engines
```

**Richiesta**

```shell
curl -X POST \
 https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer ' \
    -H 'x-gw-ims-org-id: 20655D0F5B9875B20A495E23@AdobeOrg' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -H 'x-api-key: acp_foundation_machineLearning' \
    -H 'Content-Type: text/plain' \
    -F '{
    "type": "PySpark",
    "algorithm":"fp",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "mlLibrary": "databricks-spark",
    "artifacts": {
       "default": {
           "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
           "defaultMLInstanceConfigs": [ ...
           ]
       }
   }
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `type` | Tipo di esecuzione del motore. Questo valore corrisponde alla lingua su cui viene generata l’immagine Docker. Il valore può essere impostato su Spark o PySpark. |
| `algorithm` | Algoritmo in uso. Impostare questo valore su `fp` (pipeline delle funzionalità). |
| `name` | Il nome desiderato per il motore della pipeline di funzioni. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzato nell’interfaccia utente come nome della ricetta. |
| `description` | Descrizione facoltativa del motore. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzato nell’interfaccia utente come descrizione della ricetta. Questa proprietà è obbligatoria. Se non si desidera fornire una descrizione, impostarne il valore su una stringa vuota. |
| `mlLibrary` | Campo richiesto per la creazione di motori per le ricette PySpark e Scala. Questo campo deve essere impostato su `databricks-spark`. |
| `artifacts.default.image.location` | Percorso dell’immagine Docker. È supportato solo Azure ACR o Dockerhub pubblico (non autenticato). |
| `artifacts.default.image.executionType` | Tipo di esecuzione del motore. Questo valore corrisponde alla lingua su cui viene generata l’immagine Docker. Può essere &quot;Spark&quot; o &quot;PySpark&quot;. |
| `artifacts.default.image.packagingType` | Il tipo di imballaggio del motore. Questo valore deve essere impostato su `docker`. |
| `artifacts.default.defaultMLInstanceConfigs` | Parametri del file di configurazione `pipeline.json`. |

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli del motore di pipeline delle funzionalità appena creato, incluso il relativo identificatore univoco (`id`). La risposta di esempio seguente è per un motore di pipeline di funzioni PySpark.

```json
{
    "id": "88236891-4309-4fd9-acd0-3de7827cecd1",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "mlLibrary": "databricks-spark",
    "created": "2020-04-24T20:46:58.382Z",
    "updated": "2020-04-24T20:46:58.382Z",
    "deprecated": false,
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs3mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
        "defaultMLInstanceConfigs": [ ... ]
        }
    }
}
```

## Recuperare un elenco di motori

È possibile recuperare un elenco di motori eseguendo una singola richiesta di GET. Per filtrare i risultati, puoi specificare i parametri di query nel percorso della richiesta. Per un elenco delle query disponibili, consulta la sezione dell&#39;appendice sui [parametri di query per il recupero delle risorse](./appendix.md#query).

**Formato API**

```https
GET /engines
GET /engines?parameter_1=value_1
GET /engines?parameter_1=value_1&parameter_2=value_2
```

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di motori e dei relativi dettagli.

```json
{
    "children": [
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde31",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "PySpark",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "Python",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde33",
            "name": "Feature Pipeline Engine",
            "description": "A feature pipeline Engine",
            "type": "PySpark",
            "algorithm":"fp",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 100,
        "count": 3
    }
}
```

### Recuperare un motore specifico {#retrieve-specific}

Per recuperare i dettagli di un motore specifico, esegui una richiesta di GET che includa l’ID del motore desiderato nel percorso della richiesta.

**Formato API**

```https
GET /engines/{ENGINE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{ENGINE_ID}` | ID di un motore esistente. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli del motore desiderato.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "PySpark",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "docker"
            }
        }
    }
}
```

## Aggiornare un motore

Puoi modificare e aggiornare un motore esistente sovrascrivendo le relative proprietà tramite una richiesta PUT che include l’ID del motore di destinazione nel percorso della richiesta e fornendo un payload JSON contenente le proprietà aggiornate.

>[!NOTE]
>
>Per garantire il successo di questa richiesta PUT, si consiglia di eseguire prima una richiesta GET per [recuperare il motore per ID](#retrieve-specific). Quindi, modifica e aggiorna l’oggetto JSON restituito e applica l’intero oggetto JSON modificato come payload per la richiesta PUT.

La seguente chiamata API di esempio aggiornerà il nome e la descrizione di un motore mentre inizialmente disponi di queste proprietà:

```json
{
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

**Formato API**

```https
PUT /engines/{ENGINE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{ENGINE_ID}` | ID di un motore esistente. |

**Richiesta**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -d '{
        "name": "An updated name for this Engine",
        "description": "An updated description",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "executionType": "Python",
                    "packagingType": "docker"
                }
            }
        }
    }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli aggiornati del motore.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "An updated name for this Engine",
    "description": "An updated description",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Eliminare un motore

Puoi eliminare un motore eseguendo una richiesta DELETE mentre specifichi l’ID del motore di destinazione nel percorso della richiesta. L’eliminazione di un motore comporta l’eliminazione a catena di tutte le istanze MLI che fanno riferimento a tale motore, incluse le esecuzioni di esperimenti ed esperimenti appartenenti a tali istanze MLI.

**Formato API**

```https
DELETE /engines/{ENGINE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{ENGINE_ID}` | ID di un motore esistente. |

**Richiesta**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Engine deletion was successful"
}
```
