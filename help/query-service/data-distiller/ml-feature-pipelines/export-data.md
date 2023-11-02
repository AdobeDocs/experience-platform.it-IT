---
title: Esportare dati in ambienti ML esterni
description: Scopri come condividere un set di dati di formazione preparato, creato con Data Distiller, in una posizione di archiviazione cloud che il tuo ambiente di apprendimento può leggere per la formazione e il punteggio del modello.
exl-id: 75022acf-fafd-41d6-8dfa-ff3fd4c4fa7e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 3%

---

# Esportare dati in ambienti ML esterni

Questo documento illustra come condividere un set di dati di formazione preparato creato con Data Distiller in una posizione di archiviazione cloud che l’ambiente di apprendimento può leggere per l’apprendimento e il punteggio del modello. L’esempio esporta il set di dati di formazione in [Data Landing Zone (DLZ)](../../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md). È possibile modificare la destinazione di archiviazione in base alle esigenze per lavorare con l&#39;ambiente di apprendimento automatico.

Il [Servizio di flusso per le destinazioni](https://developer.adobe.com/experience-platform-apis/references/destinations/) viene utilizzato per completare la pipeline delle funzioni inviando un set di dati di funzioni calcolate in una posizione di archiviazione cloud appropriata.

## Creare la connessione di origine {#create-source-connection}

La connessione di origine è responsabile della configurazione della connessione al set di dati Adobe Experience Platform in modo che il flusso risultante sappia esattamente dove cercare i dati e in quale formato.

```python
from aepp import flowservice
flow_conn = flowservice.FlowService()

training_dataset_id = <YOUR_TRAINING_DATASET_ID>

source_res = flow_conn.createSourceConnectionDataLake(
    name=f"[CMLE] Featurized Dataset source connection created by {username}",
    dataset_ids=[training_dataset_id],
    format="parquet"
)
source_connection_id = source_res["id"]
```

## Creare la connessione di destinazione {#create-target-connection}

La connessione di destinazione è responsabile della connessione al file system di destinazione. A tal fine è necessario innanzitutto creare una connessione di base all’account di archiviazione cloud (la Data Landing Zone in questo esempio) e quindi una connessione di destinazione a un percorso di file specifico con opzioni di compressione e formato specificate.

Le destinazioni di archiviazione cloud disponibili sono identificate ciascuna da un ID della specifica di connessione:

| Tipo di archiviazione cloud | ID specifica di connessione |
|-----------------------|--------------------------------------|
| Amazon S3 | 4fce964d-3f37-408f-9778-e597338a21ee |
| Archiviazione BLOB di Azure | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |
| Azure Data Lake | be2c3209-53bc-47e7-ab25-145db8b873e1 |
| Data Landing Zone | 10440537-2a7b-4583-ac39-ed38d4b848e8 |
| Archiviazione cloud Google | c5d93acb-ea8b-4b14-8f53-02138444ae99 |
| SFTP | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

```python
connection_spec_id = "10440537-2a7b-4583-ac39-ed38d4b848e8"
base_connection_res = flow_conn.createConnection(data={
    "name": "Base Connection to DLZ created by",
    "auth": None,
    "connectionSpec": {
        "id": connection_spec_id,
        "version": "1.0"
    }
})
base_connection_id = base_connection_res["id"]

target_res = flow_conn.createTargetConnection(
    data={
        "name": "Data Landing Zone target connection",
        "baseConnectionId": base_connection_id,
        "params": {
            "mode": "Server-to-server",
            "compression": config.get("Cloud", "compression_type"),
            "datasetFileType": config.get("Cloud", "data_format"),
            "path": config.get("Cloud", "export_path")
        },
        "connectionSpec": {
            "id": connection_spec_id,
            "version": "1.0"
        }
    }
)
target_connection_id = target_res["id"]
```

## Creare il flusso di dati {#create-data-flow}

Il passaggio finale consiste nel creare un flusso di dati tra il set di dati specificato nella connessione di origine e il percorso del file di destinazione specificato nella connessione di destinazione.

Ogni tipo di archiviazione cloud disponibile è identificato da un ID della specifica di flusso:

| Tipo di archiviazione cloud | ID specifica flusso |
|-----------------------|--------------------------------------|
| Amazon S3 | 269ba276-16fc-47db-92b0-c1049a3c131f |
| Archiviazione BLOB di Azure | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| Azure Data Lake | 17be2013-2549-41ce-96e7-a70363bec293 |
| Data Landing Zone | cd2fc47e-e838-4f38-a581-8fff2f99b63a |
| Archiviazione cloud Google | 585c15c4-6cbf-4126-8f87-e26bff78b657 |
| SFTP | 354d6aad-4754-46e4-a576-1b384561c440 |

Il codice seguente crea un flusso di dati con una pianificazione impostata per iniziare molto in futuro. Questo consente di attivare flussi ad hoc durante lo sviluppo del modello. Una volta creato un modello addestrato, è possibile aggiornare la pianificazione del flusso di dati per condividere il set di dati della feature sulla pianificazione desiderata.

```python
import time

on_schedule = False
if on_schedule:
    schedule_params = {
        "interval": 3,
        "timeUnit": "hour",
        "startTime": int(time.time())
    }
else:
    schedule_params = {
        "interval": 1,
        "timeUnit": "day",
        "startTime": int(time.time() + 60*60*24*365) # Start the schedule far in the future
    }

flow_spec_id = "cd2fc47e-e838-4f38-a581-8fff2f99b63a"
flow_obj = {
    "name": "Flow for Feature Dataset to DLZ",
    "flowSpec": {
        "id": flow_spec_id,
        "version": "1.0"
    },
    "sourceConnectionIds": [
        source_connection_id
    ],
    "targetConnectionIds": [
        target_connection_id
    ],
    "transformations": [],
    "scheduleParams": schedule_params
}
flow_res = flow_conn.createFlow(
    obj = flow_obj,
    flow_spec_id = flow_spec_id
)
dataflow_id = flow_res["id"]
```

Una volta creato il flusso di dati, ora puoi attivare un’esecuzione di flusso ad hoc per condividere il set di dati della funzione su richiesta:

```python
from aepp import connector

connector = connector.AdobeRequest(
  config_object=aepp.config.config_object,
  header=aepp.config.header,
  loggingEnabled=False,
  logger=None,
)

endpoint = aepp.config.endpoints["global"] + "/data/core/activation/disflowprovider/adhocrun"

payload = {
    "activationInfo": {
        "destinations": [
            {
                "flowId": dataflow_id, 
                "datasets": [
                    {"id": created_dataset_id}
                ]
            }
        ]
    }
}

connector.header.update({"Accept":"application/vnd.adobe.adhoc.dataset.activation+json; version=1"})
activation_res = connector.postData(endpoint=endpoint, data=payload)
activation_res
```

## Condivisione semplificata nella Data Landing Zone

Per condividere un set di dati nell’area di destinazione dati in modo più semplice, la `aepp` la libreria fornisce `exportDatasetToDataLandingZone` funzione che esegue i passaggi precedenti in una singola chiamata di funzione:

```python
from aepp import exportDatasetToDataLandingZone

export = exportDatasetToDataLandingZone.ExportDatasetToDataLandingZone()

dataflow_id = export.createDataFlowRunIfNotExists(
    dataset_id = created_dataset_id,
    data_format = data_format, 
    export_path= export_path, 
    compression_type = compression_type, 
    on_schedule = False, 
    config_path = config_path, 
    entity_name = "Flow for Featurized Dataset to DLZ"
)
```

Questo codice crea la connessione di origine, la connessione di destinazione e il flusso di dati in base ai parametri forniti ed esegue un’esecuzione ad hoc del flusso di dati in un singolo passaggio.
