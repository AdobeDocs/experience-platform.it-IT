---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: Punteggio di un modello di apprendimento automatico in tempo reale
topic: Scoring a ML model
translation-type: tm+mt
source-git-commit: dd2c9714c410d00ef2ba06e9f9728747fc6f989a
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# Punteggio di un modello di apprendimento automatico in tempo reale

>[!IMPORTANT]
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in alfa e viene ancora testata. Questo documento è soggetto a modifiche.

Questa esercitazione mostra come utilizzare i nodi Real-time Machine Learning per preelaborare i dati in arrivo e segnarli rispetto al modello ONNX.

>[!IMPORTANT]
> - Le funzioni utilizzate nei nodi non possono essere serializzate. Ad esempio, una funzione lambda utilizzata in un nodo panda.
> - Dopo l’implementazione manuale dei margini, è possibile tenere una sospensione di 60 secondi. Questo può essere trasferito al metodo score_edge di EdgeUtils.


>[!NOTE]
>Per segnare un modello da utilizzare in Real-time Machine Learning, è necessario aver completato l&#39;esercitazione precedente sulla [formazione di un modello per l&#39;apprendimento automatico in tempo reale](./training-ml-model.md)

## Creare un nuovo blocco appunti

Nell’interfaccia utente di Adobe Experience Platform, seleziona **[!UICONTROL Notebooks]** da *Data Science*. Quindi, selezionate **[!UICONTROL JupyterLab]** e lasciate che il caricamento dell&#39;ambiente abbia un po&#39; di tempo.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

Per iniziare, seleziona il notebook **Python 3** vuoto dall&#39;avvio di JupyterLab.

![pitone bianco](../images/rtml/python-blank.png)

## Importare e individuare i nodi

Iniziate importando tutti i pacchetti richiesti per il modello. Accertatevi che tutti i pacchetti che pianificate di utilizzare per l&#39;authoring dei nodi siano importati.

>[!NOTE]
>L’elenco delle importazioni potrebbe essere diverso in base al modello che avete creato.

```python
from pprint import pprint
import json
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_sdk.graph.utils import GraphBuilder
from rtml_sdk.edge.utils import EdgeUtils

from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_nodelibs.core.datamsg import DataMsg
import uuid
```

Per visualizzare l&#39;elenco dei nodi disponibili, copiare e incollare l&#39;esempio seguente nel blocco appunti.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

La risposta ricevuta è un elenco di nodi.

![elenco delle note](../images/rtml/node-list.png)

## Authoring dei nodi per il punteggio dei bordi

Successivamente, è necessario definire e creare un nodo per il punteggio dei bordi. Sostituite l’elemento `model_id` nell’esempio con l’ID modello ricevuto per completare la formazione nell’esercitazione [](./training-ml-model.md)precedente. In questo esempio viene utilizzato il nodo Pandas per importare un metodo pd.DataDrame o una funzione di primo livello generale panda. La funzione mappa viene importata e utilizzata per creare due nodi. Per ulteriori informazioni sui nodi disponibili e su come utilizzarli, consultare la guida [al riferimento ai](./node-reference.md)nodi.

```python
model_id = '{your_model_id}' # Get Model ID from Training Notebook.

data = {'sepal_length': {0: 5.8},
        'sepal_width': {0: 2.8},
        'petal_length': {0: 5.1},
        'petal_width': {0: 2.4}}

json2DF_node = JsonToDataframe(params={"json_payload":json.dumps(data)})
fill_na_node = Pandas(params={"import": "fillna", "kwargs":{"value":0}})
model_score_node = ONNXNode(params={"features": ['sepal_length', 'sepal_width', 'petal_length', 'petal_width'],
                                    "model_id": model_id})
```

## DSL grafico di generazione

Con i nodi creati, il passo successivo consiste nel catena i nodi per creare un grafico.

Per iniziare, elencare tutti i nodi che fanno parte del grafico.

```python
nodes = [node_device_apply, node_browser_apply, node_model_score]
```

Quindi, collegare i nodi ai bordi. Ogni tupla è una connessione a un bordo.

```python
edges = [ (node_device_apply, node_browser_apply), (node_browser_apply, node_model_score)]
```

Una volta connessi i nodi, create il grafico.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
```

## Pubblica sul bordo

Ora che avete creato un grafico potete implementare il grafico sul bordo.

>[!IMPORTANT]
>Se non si esegue spesso la pubblicazione su edge, i nodi edge potrebbero essere sovraccarichi. Non è consigliabile pubblicare lo stesso modello più volte.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
```

## Edge Client

Dopo la pubblicazione in edge, il punteggio viene eseguito da una richiesta POST di un client. In genere, questo può essere fatto da un&#39;applicazione client che ha bisogno di punteggi ML. Puoi farlo anche da Postman. In questo caso, EdgeUtils viene utilizzato per illustrare il processo.

```python
import time
time.sleep(600)
```

```python
data = {"sepal_length": {0: 5.8}, "sepal_width": {0: 2.8}, "petal_length": {0: 5.1}, "petal_width": {0: 2.4}}
```

```python
scored_output = edge_utils.score_edge(edge_location=edge_location,
                              service_id=service_id,
                              scoring_data=data)
print(f'Scored Output from Edge: {scored_output}')
```

Una volta completato il punteggio, vengono restituiti l’URL del margine, il payload e l’output del punteggio dal margine.

![punteggio completo](../images/rtml/scoring-complete.png)

## Eliminazione di un&#39;app distribuita dal bordo (facoltativo)

>!![CAUTION]
Questa cella viene utilizzata per eliminare l&#39;applicazione edge distribuita. Non utilizzare la cella seguente a meno che non sia necessario eliminare un&#39;applicazione edge distribuita.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Passaggi successivi

Seguendo l&#39;esercitazione precedente, hai ottenuto un punteggio e distribuito correttamente il modello di apprendimento automatico in tempo reale. Per ulteriori informazioni sui nodi disponibili per l&#39;authoring dei modelli, consultare la guida [di riferimento ai](./node-reference.md)nodi.



