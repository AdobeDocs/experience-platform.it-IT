---
keywords: Experience Platform;guida per sviluppatori;Data Science Workspace;argomenti popolari;apprendimento automatico in tempo reale;riferimento nodo;
solution: Experience Platform
title: Gestire i notebook di apprendimento automatico in tempo reale
description: La guida seguente illustra i passaggi necessari per creare un’applicazione di machine learning in tempo reale in Adobe Experience Platform JupyterLab.
exl-id: 604c4739-5a07-4b5a-b3b4-a46fd69e3aeb
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 0%

---

# Gestire i notebook di apprendimento automatico in tempo reale (Alpha)

>[!IMPORTANT]
>
>Real-time Machine Learning non è ancora disponibile per tutti gli utenti. Questa funzione è in formato alfa ed è ancora in fase di test. Questo documento è soggetto a modifiche.

La guida seguente illustra i passaggi necessari per creare un’applicazione di apprendimento automatico in tempo reale. Utilizzando l’Adobe fornito **[!UICONTROL ML in tempo reale]** Modello di blocco appunti Python, questa guida descrive come addestrare un modello, creare una DSL, pubblicare una DSL su Edge e valutare la richiesta. Man mano che procedi all’implementazione del modello di apprendimento automatico in tempo reale, devi modificare il modello in base alle esigenze del set di dati.

## Creare un blocco appunti di apprendimento automatico in tempo reale

Nell’interfaccia utente di Adobe Experience Platform, seleziona **[!UICONTROL Notebook]** da entro **Data Science**. Quindi, seleziona **[!UICONTROL JupyterLab]** e lascia un po’ di tempo per caricare l’ambiente.

![apri JupyterLab](../images/rtml/open-jupyterlab.png)

Il [!DNL JupyterLab] viene visualizzato il modulo di avvio. Scorri verso il basso fino a *Apprendimento automatico in tempo reale* e seleziona la **[!UICONTROL ML in tempo reale]** notebook. Viene aperto un modello contenente celle di esempio del blocco appunti con un set di dati di esempio.

![pitone bianco](../images/rtml/authoring-notebook.png)

## Importare e individuare nodi

Inizia importando tutti i pacchetti richiesti per il modello. Assicurati che sia importato qualsiasi pacchetto che intendi utilizzare per la creazione dei nodi.

>[!NOTE]
>
>L’elenco delle importazioni potrebbe variare in base al modello che desideri effettuare. Questo elenco verrà modificato con l’aggiunta di nuovi nodi nel tempo. Consulta la sezione [guida di riferimento ai nodi](./node-reference.md) per un elenco completo dei nodi disponibili.

```python
from pprint import pprint
import pandas as pd
import numpy as np
import json
import uuid
from shutil import copyfile
from pathlib import Path
from datetime import date, datetime, timedelta
from platform_sdk.dataset_reader import DatasetReader

from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_sdk.edge.utils import EdgeUtils
from rtml_sdk.graph.utils import GraphBuilder
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.preprocessing.one_hot_encoder import OneHotEncoder
from rtml_nodelibs.nodes.standard.ml.artifact_utils import ModelUpload
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.core.datamsg import DataMsg
```

Nella cella di codice seguente viene stampato un elenco dei nodi disponibili.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![elenco di note](../images/rtml/node-list.png)

## Formazione di un modello di apprendimento automatico in tempo reale

Stai per scrivere utilizzando una delle seguenti opzioni [!DNL Python] codice per leggere, pre-elaborare e analizzare i dati. Successivamente, devi addestrare il tuo modello ML, serializzarlo in formato ONNX e caricarlo nell’archivio modelli di apprendimento automatico in tempo reale.

- [Formazione del proprio modello nei notebook JupyterLab](#training-your-own-model)
- [Caricamento del proprio modello ONNX pre-addestrato sui notebook JupyterLab](#pre-trained-model-upload)

### Formazione del proprio modello {#training-your-own-model}

Inizia caricando i dati di apprendimento.

>[!NOTE]
>
>In **ML in tempo reale** modello, il [set di dati CSV assicurazione auto](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) viene recuperato da [!DNL Github].

![Caricare i dati di apprendimento](../images/rtml/load_training.png)

Se desideri utilizzare un set di dati all’interno di Adobe Experience Platform, rimuovi il commento dalla cella sottostante. Successivamente, devi sostituire `DATASET_ID` con il valore appropriato.

![set di dati rtml](../images/rtml/rtml-dataset.png)

Per accedere a un set di dati nel [!DNL JupyterLab] blocco appunti, selezionare **Dati** nella barra di navigazione a sinistra di [!DNL JupyterLab]. Il **[!UICONTROL Set di dati]** e **[!UICONTROL Schemi]** vengono visualizzate le directory. Seleziona **[!UICONTROL Set di dati]** e fai clic con il pulsante destro del mouse, quindi seleziona la **[!UICONTROL Esplora i dati nel notebook]** dal menu a discesa del set di dati che desideri utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile. Questa cella contiene `dataset_id`.

![accesso ai set di dati](../images/rtml/access-dataset.png)

Al termine, fare clic con il pulsante destro del mouse ed eliminare la cella generata nella parte inferiore del blocco appunti.

### Proprietà di formazione

Utilizzando il modello fornito, modifica una qualsiasi delle proprietà di apprendimento in `config_properties`.

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### Prepara il modello

Utilizzo di **[!UICONTROL ML in tempo reale]** modello, è necessario analizzare, pre-elaborare, addestrare e valutare il modello ML. Questo viene fatto applicando trasformazioni di dati e creando una pipeline di formazione.

**Trasformazioni dati**

Il **[!UICONTROL ML in tempo reale]** modelli **Trasformazioni dati** è necessario modificare la cella per funzionare con il proprio set di dati. In genere, questo comporta la ridenominazione delle colonne, l’aggregazione dei dati e la preparazione dei dati/progettazione delle funzioni.

>[!NOTE]
>
>L’esempio seguente è stato condensato a scopo di leggibilità utilizzando `[ ... ]`. Visualizzare ed espandere *ML in tempo reale* sezione delle trasformazioni dei dati dei modelli per la cella del codice completo.

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid': 'ecid',
                     [ ... ]}, inplace=True)
df1 = df1[['ecid', 'km', 'cartype', 'age', 'gender', 'carbrand', 'leasing', 'city', 
       'country', 'nationality', 'primaryuser', 'purchase', 'pricequote', 'timestamp']]
print("df1 shape 1", df1.shape)
#########################################
# Data Rollup
######################################### 
df1['timestamp'] = pd.to_datetime(df1.timestamp)
df1['hour'] = df1['timestamp'].dt.hour.astype(int)
df1['dayofweek'] = df1['timestamp'].dt.dayofweek

df1.loc[(df1['purchase'] == 'yes'), 'purchase'] = 1
df1.purchase.fillna(0, inplace=True)
df1['purchase'] = df1['purchase'].astype(int)

[ ... ]

print("df1 shape 2", df1.shape)

#########################################
# Data Preparation/Feature Engineering
#########################################      

df1['carbrand'] = df1['carbrand'].str.lower()
df1['country'] = df1['country'].str.lower()
df1.loc[(df1['carbrand'] == 'vw'), 'carbrand'] = 'volkswagen'

[ ... ]

df1['age'].fillna(df1['age'].median(), inplace=True)
df1['gender'].fillna('notgiven', inplace=True)

[ ... ]

df1['city'] = df1.groupby('country')['city'].transform(lambda x: x.fillna(x.mode()))
df1.dropna(subset = ['pricequote'], inplace=True)
print("df1 shape 3", df1.shape)
print(df1)

#grouping
grouping_cols = ['carbrand', 'cartype', 'city', 'country']

for col in grouping_cols:
    df_idx = pd.DataFrame(df1[col].value_counts().head(6))

    def grouping(x):
        if x in df_idx.index:
            return x
        else:
            return "Others"
    df1[col] = df1[col].apply(lambda x: grouping(x))

def age(x):
    if x < 20:
        return "u20"
    elif x > 19 and x < 29:
    [ ... ]
    else: 
        return "Others"

df1['age'] = df1['age'].astype(int)
df1['age_bucket'] = df1['age'].apply(lambda x: age(x))

df_final = df1[['hour', 'dayofweek','age_bucket', 'gender', 'city',  
   'country', 'carbrand', 'cartype', 'leasing', 'pricequote', 'purchase']]
print("df final", df_final.shape)

cat_cols = ['age_bucket', 'gender', 'city', 'dayofweek', 'country', 'carbrand', 'cartype', 'leasing']
df_final = pd.get_dummies(df_final, columns = cat_cols)
```

Esegui la cella specificata per visualizzare un risultato di esempio. La tabella di output restituita dal `carinsurancedataset.csv` set di dati restituisce le modifiche definite.

![Esempio di trasformazione dei dati](../images/rtml/table-return.png)

**Pipeline di addestramento**

Successivamente, devi creare la pipeline di apprendimento. Sarà simile a qualsiasi altro file della pipeline di apprendimento, tranne per il fatto che è necessario convertire e generare un file ONNX.

Utilizzando le trasformazioni di dati definite nella cella precedente, modificare il modello. Il seguente codice evidenziato di seguito viene utilizzato per generare un file ONNX nella pipeline delle funzioni. Visualizzare *ML in tempo reale* modello per la cella completa del codice della pipeline.

```python
#for generating onnx
def generate_onnx_resources(self):        
    install_dir = os.path.expanduser('~/my-workspace')
    print("Generating Onnx")
        
    from skl2onnx import convert_sklearn
    from skl2onnx.common.data_types import FloatTensorType
        
    # ONNX-ification
    initial_type = [('float_input', FloatTensorType([None, self.feature_len]))]

    print("Converting Model to Onnx")
    onx = convert_sklearn(self.model, initial_types=initial_type)
             
    with open("model.onnx", "wb") as f:
        f.write(onx.SerializeToString())
            
    print("Model onnx created")
```

Dopo aver completato la pipeline di apprendimento e modificato i dati tramite trasformazioni di dati, utilizza la cella seguente per eseguire l’apprendimento.

```python
model = train(config_properties, df_final)
```

### Generare e caricare un modello ONNX

Dopo aver completato con successo l’esecuzione di un corso di formazione, devi generare un modello ONNX e caricare il modello addestrato nell’archivio modelli di apprendimento automatico in tempo reale. Dopo aver eseguito le celle seguenti, il modello ONNX viene visualizzato nella barra a sinistra insieme a tutti gli altri notebook.

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>Modificare il `model_path` valore stringa (`model.onnx`) per modificare il nome del modello.

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>La cella seguente non è modificabile o eliminabile ed è necessaria per il funzionamento dell&#39;applicazione Real-time Machine Learning.

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID: ", model_id)
```

![Modello ONNX](../images/rtml/onnx-model-rail.png)

### Caricamento del proprio modello ONNX pre-addestrato {#pre-trained-model-upload}

Utilizzando il pulsante Carica disponibile in [!DNL JupyterLab] notebook, carica il modello ONNX pre-addestrato sul [!DNL Data Science Workspace] dell&#39;ambiente notebook.

![icona di caricamento](../images/rtml/upload.png)

Quindi, modifica il `model_path` valore stringa in *ML in tempo reale* per corrispondere al nome del modello ONNX. Al termine, esegui *Imposta percorso modello* ed eseguire il comando *Carica il modello nell&#39;archivio modelli RTML* cella. La posizione del modello e l’ID del modello vengono entrambi restituiti nella risposta in caso di esito positivo.

![caricamento del proprio modello](../images/rtml/upload-own-model.png)

## Creazione DSL (Domain Specific Language)

In questa sezione viene descritta la creazione di un DSL. Stai per creare i nodi che includono eventuali pre-elaborazioni di dati insieme al nodo ONNX. Successivamente, viene creato un grafico DSL utilizzando nodi e bordi. Gli spigoli connettono i nodi utilizzando il formato basato sulla tupla (node_1, node_2). Il grafico non deve avere cicli.

>[!IMPORTANT]
>
>L’utilizzo del nodo ONNX è obbligatorio. Senza il nodo ONNX, l’applicazione non avrà esito positivo.

### Authoring dei nodi

>[!NOTE]
>
> È probabile che siano presenti più nodi in base al tipo di dati utilizzati. L&#39;esempio che segue delinea un solo nodo nel *ML in tempo reale* modello. Visualizzare *ML in tempo reale* modelli *Authoring dei nodi* per la cella del codice completo.

Il nodo Pandas di seguito utilizza `"import": "map"` per importare il nome del metodo come stringa nei parametri, seguito dall&#39;immissione dei parametri come funzione di mappa. L’esempio seguente esegue questa operazione utilizzando `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`. Dopo aver impostato la mappa, puoi impostare `inplace` as `True` o `False`. Imposta `inplace` as `True` o `False` a seconda che si desideri applicare la trasformazione sul posto o meno. Per impostazione predefinita `"inplace": False` crea una nuova colonna. Il supporto per fornire un nuovo nome di colonna è impostato per essere aggiunto in una versione successiva. Ultima riga `cols` può essere un nome di colonna singolo o un elenco di colonne. Specificare le colonne alle quali applicare la trasformazione. In questo esempio `leasing` è specificato. Per ulteriori informazioni sui nodi disponibili e su come utilizzarli, visita il [guida di riferimento ai nodi](./node-reference.md).

```python
# Renaming leasing column using Pandas Node
leasing_mapper_node = Pandas(params={'import': 'map',
                                'kwargs': {'arg': {
                                    'dataLayerNull': 'notgiven', 
                                    'no': 'no', 
                                    'yes': 'yes', 
                                    'notgiven': 'notgiven'}},
                                'inplace': True,
                                'cols': 'leasing'})
```

### Creare il grafico DSL

Una volta creati i nodi, il passaggio successivo consiste nel concatenare i nodi per creare un grafico.

Per iniziare, elenca tutti i nodi che fanno parte del grafico creando un array.

```python
nodes = [json_df_node, 
        to_datetime_node,
        hour_node,
        dayofweek_node,
        age_fillna_node,
        carbrand_fillna_node,
        country_fillna_node,
        cartype_primary_nationality_km_fillna_node,
        carbrand_mapper_node,
        cartype_mapper_node,
        country_mapper_node,
        gender_mapper_node,
        leasing_mapper_node,
        age_to_int_node,
        age_bins_node,
        dummies_node, 
        onnx_node]
```

Quindi, connetti i nodi con gli spigoli. Ogni tupla è un [!DNL Edge] connessione.

>[!TIP]
>
> Poiché i nodi sono linearmente dipendenti l’uno dall’altro (ogni nodo dipende dall’output del nodo precedente), puoi creare collegamenti utilizzando una semplice comprensione dell’elenco Python. Aggiungi le tue connessioni se un nodo dipende da più input.

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

Una volta connessi i nodi, crea il grafico. La cella seguente è obbligatoria e non può essere modificata o eliminata.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

Una volta completato, `edge` viene restituito un oggetto contenente ciascuno dei nodi e i parametri mappati ad essi.

![ritorno perimetrale](../images/rtml/edge-return.png)

## Pubblica su Edge (Hub)

>[!NOTE]
>
>Real-time Machine Learning viene temporaneamente distribuito e gestito dall’hub Adobe Experience Platform. Per ulteriori dettagli, consulta la sezione panoramica su [Architettura di apprendimento automatico in tempo reale](./home.md#architecture).

Dopo aver creato un grafico DSL, puoi distribuirlo al [!DNL Edge].

>[!IMPORTANT]
>
>Non pubblicare in [!DNL Edge] spesso questo può sovraccaricare il [!DNL Edge] nodi. Non è consigliabile pubblicare lo stesso modello più volte.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### Aggiornamento della DSL e ripubblicazione in Edge (facoltativo)

Se non è necessario aggiornare l&#39;elenco DSL, è possibile passare a [punteggio](#scoring).

>[!NOTE]
>
>Le celle seguenti sono necessarie solo se si desidera aggiornare un DSL esistente pubblicato in Edge.

È probabile che i modelli continuino a svilupparsi. Anziché creare un servizio completamente nuovo, è possibile aggiornare un servizio esistente con il nuovo modello. È possibile definire un nodo da aggiornare, assegnargli un nuovo ID, quindi ricaricare il nuovo DSL in [!DNL Edge].

Nell’esempio seguente, il nodo 0 viene aggiornato con un nuovo ID.

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![Nodo aggiornato](../images/rtml/updated-node.png)

Dopo aver aggiornato l’ID nodo, puoi ripubblicare un DSL aggiornato in Edge.

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

Viene restituito il DSL aggiornato.

![DSL aggiornato](../images/rtml/updated-dsl.png)

## Punteggio {#scoring}

Dopo la pubblicazione in [!DNL Edge], il punteggio viene eseguito da una richiesta POST da un client. In genere, questa operazione può essere eseguita da un’applicazione client che richiede punteggi ML. Puoi anche farlo da Postman. Il **[!UICONTROL ML in tempo reale]** Il modello utilizza EdgeUtils per illustrare questo processo.

>[!NOTE]
>
>È necessario un piccolo tempo di elaborazione prima dell’inizio del punteggio.

```python
# Wait for the app to come up
import time
time.sleep(20)
```

Utilizzando lo stesso schema utilizzato nell’apprendimento, vengono generati dati di punteggio di esempio. Questi dati vengono utilizzati per creare un dataframe di punteggio e quindi convertiti in un dizionario di punteggio. Visualizzare *ML in tempo reale* modello per la cella del codice completo.

![Dati punteggio](../images/rtml/generate-score-data.png)

### Punteggio rispetto al punto finale Edge

Utilizza la cella seguente all’interno di *ML in tempo reale* modello per valutare il tuo [!DNL Edge] servizio.

![Punteggio rispetto al bordo](../images/rtml/scoring-edge.png)

Una volta completato il punteggio, [!DNL Edge] URL, payload e output con punteggio da [!DNL Edge] vengono restituiti.

## Elencare le app distribuite da [!DNL Edge]

Per generare un elenco delle app attualmente distribuite sul [!DNL Edge], esegui la seguente cella di codice. Impossibile modificare o eliminare questa cella.

```python
services = edge_utils.list_deployed_services()
print(services)
```

La risposta restituita è un array dei servizi distribuiti.

```json
[
    {
        "created": "2020-05-25T19:18:52.731Z",
        "deprecated": false,
        "id": "40eq76c0-1c6f-427a-8f8f-54y9cdf041b7",
        "type": "edge",
        "updated": "2020-05-25T19:18:52.731Z"
    }
]
```

## Eliminare un ID di app o servizio distribuito da [!DNL Edge] (facoltativo)

>[!CAUTION]
>
>Questa cella viene utilizzata per eliminare l&#39;applicazione Edge distribuita. Non utilizzare la cella seguente a meno che non sia necessario eliminare una [!DNL Edge] applicazione.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Passaggi successivi

Seguendo l&#39;esercitazione precedente, hai completato l&#39;apprendimento e hai caricato un modello ONNX nell&#39;archivio modelli di apprendimento automatico in tempo reale. Inoltre, hai valutato e implementato il tuo modello di apprendimento automatico in tempo reale. Per ulteriori informazioni sui nodi disponibili per l’authoring dei modelli, visita [guida di riferimento ai nodi](./node-reference.md).
