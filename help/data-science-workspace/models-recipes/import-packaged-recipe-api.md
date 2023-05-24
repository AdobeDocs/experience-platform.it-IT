---
keywords: Experience Platform;importare pacchetti di ricetta;Data Science Workspace;argomenti popolari;ricette;api;sensei machine learning;creare un motore;import packaged ricetta;Data Science Workspace;popular topic;recipes;api;sensei machine learning;create engine
solution: Experience Platform
title: Importare una composizione in pacchetti utilizzando l’API di apprendimento automatico di Sensei
type: Tutorial
description: Questa esercitazione utilizza l’API di apprendimento automatico di Sensei per creare un motore, noto anche come ricetta nell’interfaccia utente di.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 2%

---

# Importare una ricetta confezionata utilizzando l’API di apprendimento automatico di Sensei

Questa esercitazione utilizza [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) per creare un [Motore](../api/engines.md), nota anche come ricetta nell’interfaccia utente di.

Prima di iniziare, è importante notare che Adobe Experience Platform [!DNL Data Science Workspace] utilizza termini diversi per fare riferimento a elementi simili nell’API e nell’interfaccia utente. In questa esercitazione vengono utilizzati i termini API e la tabella seguente illustra i termini correlati:

| Termine interfaccia utente | Termine API |
| ---- | ---- |
| Ricetta | [Motore](../api/engines.md) |
| Modello | [MLInstance](../api/mlinstances.md) |
| Formazione e valutazione | [Esperimento](../api/experiments.md) |
| Servizio | [MLService](../api/mlservices.md) |

Un motore contiene algoritmi di apprendimento automatico e logica per risolvere problemi specifici. Il diagramma seguente fornisce una visualizzazione che mostra il flusso di lavoro API in [!DNL Data Science Workspace]. Questa esercitazione si concentra sulla creazione di un motore, il cervello di un modello di apprendimento automatico.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Introduzione

Questa esercitazione richiede un file di composizione in pacchetti sotto forma di URL Docker. Segui le [Creare pacchetti di file di origine in una ricetta](./package-source-files-recipe.md) esercitazione per creare un pacchetto di file di composizione o fornirne uno personalizzato.

- `{DOCKER_URL}`: indirizzo URL di un’immagine Docker di un servizio intelligente.

Questo tutorial richiede di aver completato [Tutorial sull’autenticazione per Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente chiamate a [!DNL Platform] API. Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- `{ACCESS_TOKEN}`: valore del token Bearer specifico fornito dopo l’autenticazione.
- `{ORG_ID}`: le credenziali della tua organizzazione sono state trovate nell’integrazione univoca di Adobe Experience Platform.
- `{API_KEY}`: valore chiave API specifico trovato nell’integrazione univoca di Adobe Experience Platform.

## Creare un motore

I motori possono essere creati effettuando una richiesta POST all’endpoint /engines. Il motore creato è configurato in base al formato del file Composizione da includere nella richiesta API.

### Creare un motore con un URL Docker {#create-an-engine-with-a-docker-url}

Per creare un motore con un file di composizione in pacchetto memorizzato in un contenitore Docker, è necessario fornire l’URL Docker al file di composizione in pacchetto.

>[!CAUTION]
>
> Se sta usando [!DNL Python] o R utilizza la richiesta seguente. Se utilizzi PySpark o Scala, utilizza l’esempio di richiesta PySpark/Scala che si trova sotto l’esempio Python/R.

**Formato API**

```http
POST /engines
```

**Richiedi Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `engine.name` | Il nome desiderato per il motore. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzata in [!DNL Data Science Workspace] come nome della ricetta. |
| `engine.description` | Descrizione facoltativa del motore. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzata in [!DNL Data Science Workspace] come descrizione della ricetta. Non rimuovere questa proprietà, lascia che questo valore sia una stringa vuota se scegli di non fornire una descrizione. |
| `engine.type` | Tipo di esecuzione del motore. Questo valore corrisponde al linguaggio in cui viene sviluppata l’immagine Docker. Quando viene fornito un URL Docker per creare un motore, `type` è `Python`, `R`, `PySpark`, `Spark` (Scala), oppure `Tensorflow`. |
| `artifacts.default.image.location` | Il tuo `{DOCKER_URL}` va qui. Un URL Docker completo ha la seguente struttura: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Un nome aggiuntivo per il file di immagine Docker. Non rimuovere questa proprietà, lascia che questo valore sia una stringa vuota se scegli di non fornire un nome di file immagine Docker aggiuntivo. |
| `artifacts.default.image.executionType` | Tipo di esecuzione del motore. Questo valore corrisponde al linguaggio in cui viene sviluppata l’immagine Docker. Quando viene fornito un URL Docker per creare un motore, `executionType` è `Python`, `R`, `PySpark`, `Spark` (Scala), oppure `Tensorflow`. |

**Richiedi PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Il nome desiderato per il motore. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzato nell’interfaccia utente come nome della ricetta. |
| `description` | Descrizione facoltativa del motore. La ricetta corrispondente a questo motore erediterà questo valore per essere visualizzato nell’interfaccia utente come descrizione della ricetta. Questa proprietà è obbligatoria. Se non si desidera fornire una descrizione, impostarne il valore su una stringa vuota. |
| `type` | Tipo di esecuzione del motore. Questo valore corrisponde al linguaggio in cui l’immagine Docker è generata su &quot;PySpark&quot;. |
| `mlLibrary` | Campo richiesto per la creazione di motori per le ricette PySpark e Scala. |
| `artifacts.default.image.location` | Posizione dell’immagine Docker collegata da un URL Docker. |
| `artifacts.default.image.executionType` | Tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui l’immagine Docker è generata su &quot;Spark&quot;. |

**Scala richiesta**

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
| `type` | Tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui l’immagine Docker è generata su &quot;Spark&quot;. |
| `mlLibrary` | Campo richiesto per la creazione di motori per le ricette PySpark e Scala. |
| `artifacts.default.image.location` | Posizione dell’immagine Docker collegata da un URL Docker. |
| `artifacts.default.image.executionType` | Tipo di esecuzione del motore. Questo valore corrisponde alla lingua in cui l’immagine Docker è generata su &quot;Spark&quot;. |

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli del motore appena creato, compreso il relativo identificatore univoco (`id`). L’esempio di risposta che segue è per un [!DNL Python] Motore. Il `executionType` e `type` le chiavi cambiano in base al POST fornito.

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

In caso di esito positivo, la risposta mostra un payload JSON con informazioni relative al motore appena creato. Il `id` La chiave rappresenta l’identificatore univoco del motore ed è richiesta nell’esercitazione successiva per creare un’istanza MLI. Prima di procedere con i passaggi successivi, assicurati che l’identificatore del motore sia salvato.

## Passaggi successivi {#next-steps}

Hai creato un motore utilizzando l’API ed è stato ottenuto un identificatore univoco del motore come parte del corpo della risposta. Puoi utilizzare questo identificatore del motore nel prossimo tutorial mentre scopri come [creare, addestrare e valutare un modello utilizzando l’API](./train-evaluate-model-api.md).
