---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Motori
topic: Developer guide
translation-type: tm+mt
source-git-commit: f2a7300d4ad75e3910abbdf2ecc2946a2dfe553c
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 3%

---


# Motori

I motori sono le basi per i modelli di apprendimento automatico in Data Science Workspace. Contengono algoritmi di machine learning che risolvono problemi specifici, oleodotti per eseguire la progettazione di funzionalità o entrambi.

## Cerca il tuo registro di Docker

>[!TIP]
>Se non disponete di un URL Docker, visitate i file sorgente del [pacchetto in un&#39;esercitazione di ricetta](../models-recipes/package-source-files-recipe.md) per una dettagliata procedura per la creazione di un URL host Docker.

Le credenziali del Registro di sistema del Docker sono necessarie per caricare un file Recipe incluso l&#39;URL host Docker, il nome utente e la password. Potete cercare queste informazioni eseguendo la seguente richiesta GET:

**Formato API**

```https
GET /engines/dockerRegistry
```

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli del Registro di sistema del Docker, inclusi l’URL (`host`), il nome utente (`username`) e la password (`password`) del Docker.

>[!NOTE]
>La password del Docker cambia ogni volta che `{ACCESS_TOKEN}` viene aggiornato.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Creare un motore utilizzando gli URL Docker {#docker-image}

È possibile creare un motore eseguendo una richiesta POST fornendo i relativi metadati e un URL Docker che fa riferimento a un&#39;immagine Docker in più moduli.

**Formato API**

```https
POST /engines
```

**Richiesta Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
                    "location": "{DOCKER_URL}",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome desiderato per il motore. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzata nell&#39;interfaccia utente come nome della ricetta. |
| `description` | Una descrizione facoltativa per il motore. La ricetta corrispondente a questo motore erediterà il valore che verrà visualizzato nell&#39;interfaccia utente come descrizione della ricetta. Questa proprietà è obbligatoria. Se non si desidera fornire una descrizione, impostare il relativo valore su una stringa vuota. |
| `type` | Il tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui è basata l&#39;immagine Docker e può essere &quot;Python&quot;, &quot;R&quot; o &quot;Tensorflow&quot;. |
| `algorithm` | Una stringa che specifica il tipo di algoritmo di machine learning. I tipi di algoritmo supportati includono &quot;Classification&quot;, &quot;Regression&quot; o &quot;Custom&quot;. |
| `artifacts.default.image.location` | Posizione dell&#39;immagine Docker collegata a un URL Docker. |
| `artifacts.default.image.executionType` | Il tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui è basata l&#39;immagine Docker e può essere &quot;Python&quot;, &quot;R&quot; o &quot;Tensorflow&quot;. |

**Richiesta PySpark/Scala**

Quando si fa una richiesta per le ricette PySpark, il `executionType` ed `type` è &quot;PySpark&quot;. Quando si fa una richiesta per ricette Scala, il `executionType` ed `type` è &quot;Spark&quot;. Nell&#39;esempio di ricetta Scala riportato di seguito viene utilizzato Spark:

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Nome desiderato per il motore. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzata nell&#39;interfaccia utente come nome della ricetta. |
| `description` | Una descrizione facoltativa per il motore. La ricetta corrispondente a questo motore erediterà il valore che verrà visualizzato nell&#39;interfaccia utente come descrizione della ricetta. Questa proprietà è obbligatoria. Se non si desidera fornire una descrizione, impostare il relativo valore su una stringa vuota. |
| `type` | Il tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui è basata l&#39;immagine Docker. Il valore può essere impostato su Spark o PySpark. |
| `mlLibrary` | Campo richiesto per la creazione di motori per le ricette PySpark e Scala. Questo campo deve essere impostato su `databricks-spark`. |
| `artifacts.default.image.location` | Posizione dell&#39;immagine Docker. È supportato solo Azure ACR o Public (non autenticato) Dockerhub. |
| `artifacts.default.image.executionType` | Il tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui è basata l&#39;immagine Docker. Può essere &quot;Spark&quot; o &quot;PySpark&quot;. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli del motore appena creato, incluso il relativo identificatore univoco (`id`). L’esempio di seguito illustra la risposta relativa a un motore Python. Tutte le risposte del motore seguono questo formato:

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "{DOCKER_URL}",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Creare un motore di pipeline delle funzioni utilizzando gli URL Docker {#feature-pipeline-docker}

Potete creare un motore di pipeline delle funzioni eseguendo una richiesta POST fornendo i relativi metadati e un URL Docker che fa riferimento a un&#39;immagine Docker.

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
           "defaultMLInstanceConfigs": [
           ]
       }
   }
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `type` | Il tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui è basata l&#39;immagine Docker. Il valore può essere impostato su Spark o PySpark. |
| `algorithm` | L&#39;algoritmo utilizzato, imposta questo valore su `fp` (pipeline delle caratteristiche). |
| `name` | Il nome desiderato per il motore della pipeline delle feature. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzata nell&#39;interfaccia utente come nome della ricetta. |
| `description` | Una descrizione facoltativa per il motore. La ricetta corrispondente a questo motore erediterà il valore che verrà visualizzato nell&#39;interfaccia utente come descrizione della ricetta. Questa proprietà è obbligatoria. Se non si desidera fornire una descrizione, impostare il relativo valore su una stringa vuota. |
| `mlLibrary` | Campo richiesto per la creazione di motori per le ricette PySpark e Scala. Questo campo deve essere impostato su `databricks-spark`. |
| `artifacts.default.image.location` | Posizione dell&#39;immagine Docker. È supportato solo Azure ACR o Public (non autenticato) Dockerhub. |
| `artifacts.default.image.executionType` | Il tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui è basata l&#39;immagine Docker. Può essere &quot;Spark&quot; o &quot;PySpark&quot;. |
| `artifacts.default.image.packagingType` | Tipo di imballaggio del motore. Questo valore deve essere impostato su `docker`. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli del motore di pipeline delle funzionalità appena creato, incluso il relativo identificatore univoco (`id`). La risposta di esempio seguente è per un motore di pipeline delle funzionalità PySpark.

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
            }
        }
    }
}
```

## Recupero di un elenco di motori

È possibile recuperare un elenco di motori eseguendo una singola richiesta GET. Per facilitare il filtraggio dei risultati, potete specificare i parametri di query nel percorso di richiesta. Per un elenco delle query disponibili, consultate la sezione appendice sui parametri delle [query per il recupero](./appendix.md#query)delle risorse.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di motori e relativi dettagli.

```json
{
    "children": [
        {
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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

Potete recuperare i dettagli di un Motore specifico eseguendo una richiesta GET che include l&#39;ID del Motore desiderato nel percorso della richiesta.

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
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli del motore desiderato.

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/{ENGINE_ID}/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## Aggiornamento di un motore

Potete modificare e aggiornare un motore esistente sovrascrivendone le proprietà tramite una richiesta PUT che include l&#39;ID del motore di destinazione nel percorso della richiesta e fornendo un payload JSON contenente le proprietà aggiornate.

>[!NOTE] Per garantire il successo di questa richiesta PUT, si consiglia prima di eseguire una richiesta GET per [recuperare il Motore per ID](#retrieve-specific). Quindi, modificate e aggiornate l&#39;oggetto JSON restituito e applicate l&#39;intero oggetto JSON modificato come payload per la richiesta PUT.

La seguente chiamata API di esempio aggiornerà il nome e la descrizione di un motore, pur avendo inizialmente queste proprietà:

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
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Una risposta corretta restituisce un payload contenente i dettagli aggiornati del motore.

```json
{
    "id": "{ENGINE_ID}",
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

Potete eliminare un motore eseguendo una richiesta DELETE mentre specificate l&#39;ID del motore di destinazione nel percorso della richiesta. L&#39;eliminazione di un motore comporta l&#39;eliminazione a cascata di tutte le istanze MLI che fanno riferimento a tale motore, compresi gli esperimenti e gli esperimenti eseguiti appartenenti a tali istanze MLI.

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
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
