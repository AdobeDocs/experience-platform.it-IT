---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Importare una ricetta in pacchetti (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 20e26c874204da75cac7e8d001770702658053f1
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 2%

---


# Importare una ricetta in pacchetti (API)

Questa esercitazione utilizza l&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei Machine Learning per creare un [motore](../api/engines.md), noto anche come Ricetta nell&#39;interfaccia utente.

Prima di iniziare, è importante notare che  Adobe Experience Platform Data Science Workspace utilizza termini diversi per fare riferimento a elementi simili all&#39;interno dell&#39;API e dell&#39;interfaccia utente. I termini API vengono utilizzati in questa esercitazione e nella tabella seguente sono riportati i termini correlati:

| Termine interfaccia utente | Termine API |
| ---- | ---- |
| Ricetta | [Motore](../api/engines.md) |
| Modello | [MLInance](../api/mlinstances.md) |
| Formazione e valutazione | [Sperimentazione](../api/experiments.md) |
| Servizio | [MLService](../api/mlservices.md) |

Un Motore contiene algoritmi di machine learning e logica per risolvere problemi specifici. Il diagramma seguente fornisce una visualizzazione del flusso di lavoro API in Data Science Workspace. Questa esercitazione si concentra sulla creazione di un Motore, il cervello di un Modello di apprendimento automatico.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Introduzione

Questa esercitazione richiede un file Recipe compresso sotto forma di URL Docker. Seguite i file sorgente del [pacchetto in un&#39;esercitazione sulla ricetta](./package-source-files-recipe.md) per creare un file Recipe in pacchetto o fornitene uno personalizzato.

- `{DOCKER_URL}`: Un indirizzo URL a un&#39;immagine Docker di un servizio intelligente.

Questa esercitazione richiede che sia stata completata l&#39; [autenticazione per &#39;esercitazione](../../tutorials/authentication.md) Adobe Experience Platform al fine di effettuare correttamente le chiamate alle API Platform. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

- `{ACCESS_TOKEN}`: Il valore del token del portatore specificato dopo l&#39;autenticazione.
- `{IMS_ORG}`: Credenziali organizzazione IMS trovate nella vostra integrazione  Adobe Experience Platform.
- `{API_KEY}`: Il valore della chiave API specifico trovato nell&#39;integrazione del Adobe Experience Platform  univoco.

## Creare un motore

I motori possono essere creati eseguendo una richiesta POST all&#39;endpoint /Engine. Il motore creato è configurato in base al modulo del file Recipe del pacchetto che deve essere incluso come parte della richiesta API.

### Creare un motore con un URL Docker {#create-an-engine-with-a-docker-url}

Per creare un Motore con un file Recipe in pacchetto memorizzato in un contenitore Docker, dovete fornire l&#39;URL Docker al file Recipe in pacchetto.

>[!CAUTION]
> Se utilizzi Python o R utilizza la richiesta riportata di seguito. Se utilizzate PySpark o Scala, usate l’esempio di richiesta PySpark/Scala, situato sotto l’esempio Python/R.

**Formato API**

```http
POST /engines
```

**Richiesta Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H `x-sandbox-name: {SANDBOX_NAME}` \
    -F 'engine={
        "name": "Retail Sales Engine Python",
        "description": "A description for Retail Sales Engine, this Engines execution type is Python",
        "type": "Python"
        "artifacts": {
            "default": {
                "image": {
                    "location": "{DOCKER_URL}",
                    "name": "retail_sales_python",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Proprietà | Descrizione |
| -------  | ----------- |
| `engine.name` | Nome desiderato per il motore. La ricetta corrispondente a questo Motore erediterà questo valore per essere visualizzato nell&#39;interfaccia utente di Data Science Workspace come nome della Ricetta. |
| `engine.description` | Una descrizione facoltativa per il motore. La ricetta corrispondente a questo motore erediterà questo valore da visualizzare nell&#39;interfaccia utente di Data Science Workspace come descrizione della ricetta. Non rimuovere questa proprietà, lasciare che questo valore sia una stringa vuota se si sceglie di non fornire una descrizione. |
| `engine.type` | Il tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui è sviluppata l&#39;immagine Docker. Quando viene fornito un URL Docker per creare un motore, `type` è `Python`, `R`, `PySpark`, `Spark` (Scala) o `Tensorflow`. |
| `artifacts.default.image.location` | La tua `{DOCKER_URL}` va qui. Un URL Docker completo ha la struttura seguente: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Un nome aggiuntivo per il file immagine Docker. Non rimuovere questa proprietà, lasciare che questo valore sia una stringa vuota se si sceglie di non fornire un nome di file immagine Docker aggiuntivo. |
| `artifacts.default.image.executionType` | Il tipo di esecuzione di questo motore. Questo valore corrisponde alla lingua in cui è sviluppata l&#39;immagine Docker. Quando viene fornito un URL Docker per creare un motore, `executionType` è `Python`, `R`, `PySpark`, `Spark` (Scala) o `Tensorflow`. |

**Richiesta PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "PySpark retail sales recipe",
    "description": "A description for this Engine",
    "type": "PySpark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "PySpark",
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
| `type` | Il tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui l&#39;immagine Docker è basata su &quot;PySpark&quot;. |
| `mlLibrary` | Campo richiesto per la creazione di motori per le ricette PySpark e Scala. |
| `artifacts.default.image.location` | Posizione dell&#39;immagine Docker collegata a un URL Docker. |
| `artifacts.default.image.executionType` | Il tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui l&#39;immagine Docker è basata su &quot;Spark&quot;. |

**Richiesta scala**

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
| `type` | Il tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui l&#39;immagine Docker è basata su &quot;Spark&quot;. |
| `mlLibrary` | Campo richiesto per la creazione di motori per le ricette PySpark e Scala. |
| `artifacts.default.image.location` | Posizione dell&#39;immagine Docker collegata a un URL Docker. |
| `artifacts.default.image.executionType` | Il tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui l&#39;immagine Docker è basata su &quot;Spark&quot;. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli del motore appena creato, incluso il relativo identificatore univoco (`id`). L’esempio di seguito illustra la risposta relativa a un motore Python. Le chiavi `executionType` e `type` le chiavi cambiano in base al POST fornito.

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

Una risposta corretta mostra un payload JSON con informazioni relative al motore appena creato. La `id` chiave rappresenta l’identificatore univoco del motore ed è necessaria nell’esercitazione successiva per creare un’istanza MLI. Prima di continuare con i passaggi successivi, assicurarsi che l’identificatore del motore sia salvato.

## Passaggi successivi {#next-steps}

Avete creato un Motore utilizzando l&#39;API ed è stato ottenuto un identificatore univoco del Motore come parte del corpo della risposta. Potete utilizzare questo identificatore del motore nell&#39;esercitazione successiva per apprendere come [creare, formare e valutare un modello utilizzando l&#39;API](./train-evaluate-model-api.md).