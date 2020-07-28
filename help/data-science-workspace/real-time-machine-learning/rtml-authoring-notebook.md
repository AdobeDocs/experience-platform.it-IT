---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: Guida utente del notebook Real-time Machine Learning
topic: Training and scoring a ML model
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1618'
ht-degree: 0%

---


# Guida utente del notebook Real-time Machine Learning (Alpha)

>[!IMPORTANT]
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in alfa e viene ancora testata. Questo documento è soggetto a modifiche.

La seguente guida illustra i passaggi necessari per creare un&#39;applicazione Real-time Machine Learning. Utilizzando il modello per notebook **[!UICONTROL Real-time ML]** Python fornito dall&#39;Adobe , questa guida illustra la formazione di un modello, la creazione di un DSL, la pubblicazione di DSL su Edge e il punteggio della richiesta. Durante l&#39;implementazione del modello di apprendimento automatico in tempo reale, si prevede di modificare il modello per adattarlo alle esigenze del set di dati.

## Creazione di un notebook Real-time Machine Learning

Nell&#39;interfaccia utente del Adobe Experience Platform , seleziona **[!UICONTROL Notebooks]** da *Data Science*. Quindi, selezionate **[!UICONTROL JupyterLab]** e lasciate che il caricamento dell&#39;ambiente abbia un po&#39; di tempo.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

Viene [!DNL JupyterLab] visualizzato il modulo di avvio. Scorri verso il basso fino a *Real-Time Machine Learning* e seleziona il **[!UICONTROL Real-time ML]** notebook. Viene aperto un modello contenente celle di blocco appunti di esempio con un set di dati di esempio.

![pitone bianco](../images/rtml/authoring-notebook.png)

## Importare e individuare i nodi

Iniziate importando tutti i pacchetti richiesti per il modello. Accertatevi che tutti i pacchetti che pianificate di utilizzare per l&#39;authoring dei nodi siano importati.

>[!NOTE]
>L&#39;elenco delle importazioni potrebbe essere diverso in base al modello che si desidera effettuare. Questo elenco verrà modificato man mano che nuovi nodi vengono aggiunti nel tempo. Per un elenco completo dei nodi disponibili, fare riferimento alla guida [di riferimento per i](./node-reference.md) nodi.

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

Nella cella di codice seguente viene visualizzato un elenco di nodi disponibili.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![elenco delle note](../images/rtml/node-list.png)

## Formazione di un modello di apprendimento automatico in tempo reale

Utilizzando una delle seguenti opzioni, si scriverà [!DNL Python] il codice per leggere, preelaborare e analizzare i dati. Successivamente, è necessario formare il proprio modello ML, serializzarlo in formato ONNX e quindi caricarlo in Real-time Machine Learning model store.

- [Formazione del proprio modello nei notebook JupyterLab](#training-your-own-model)
- [Caricamento del modello ONNX su notebook JupyterLab](#pre-trained-model-upload)

### Formazione del proprio modello {#training-your-own-model}

Iniziate caricando i dati di formazione.

>[!NOTE]
>Nel modello ML **in** tempo reale, il set di dati [CSV di assicurazione](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) auto viene preso dal [!DNL Github].

![Dati di formazione del carico](../images/rtml/load_training.png)

Se desiderate utilizzare un dataset dall&#39;interno  Adobe Experience Platform, rimuovete il commento dalla cella sottostante. Successivamente, è necessario sostituire `DATASET_ID` con il valore appropriato.

![set di dati rtml](../images/rtml/rtml-dataset.png)

Per accedere a un set di dati nel [!DNL JupyterLab] blocco appunti, seleziona la scheda **Dati** nella barra di navigazione a sinistra di [!DNL JupyterLab]. Vengono visualizzate le *[!UICONTROL Datasets]* e *[!UICONTROL Schemas]* le directory. Selezionare **[!UICONTROL Datasets]** e fare clic con il pulsante destro del mouse, quindi selezionare l&#39; **[!UICONTROL Explore Data in Notebook]** opzione dal menu a discesa del set di dati che si desidera utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile. Questa cellula ha la sua `dataset_id`.

![accesso dataset](../images/rtml/access-dataset.png)

Al termine, fare clic con il pulsante destro del mouse ed eliminare la cella generata nella parte inferiore del blocco appunti.

### Proprietà formazione

Utilizzando il modello fornito, modificate le proprietà di formazione all’interno `config_properties`.

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### Preparare il modello

Utilizzando il *[!UICONTROL Real-time ML]* modello, è necessario analizzare, pre-elaborare, formare e valutare il modello ML. A tal fine, si applicano le trasformazioni dei dati e si crea una pipeline di formazione.

**Trasformazioni dei dati**

La cella *[!UICONTROL Real-time ML]* template *Data Transformations (Trasformazioni* dati) deve essere modificata per lavorare con il set di dati personale. In genere si tratta di rinominare le colonne, il rollup dei dati e la preparazione/progettazione di funzioni.

>[!NOTE]
>L&#39;esempio seguente è stato condensato a fini di leggibilità utilizzando `[ ... ]`. Visualizzare ed espandere la sezione Trasformazioni dati dei modelli ML *in tempo* reale per l&#39;intera cella di codice.

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid' : 'ecid',
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

df1['city'] = df1.groupby('country')['city'].transform(lambda x : x.fillna(x.mode()))
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

Eseguire la cella fornita per visualizzare un risultato di esempio. La tabella di output restituita dal `carinsurancedataset.csv` dataset restituisce le modifiche definite.

![Esempio di trasformazioni di dati](../images/rtml/table-return.png)

**Canale di formazione**

Successivamente è necessario creare la pipeline di formazione. Questo avrà un aspetto simile a qualsiasi altro file della pipeline di formazione, tranne che è necessario convertire e generare un file ONNX.

Utilizzando le trasformazioni di dati definite nella cella precedente, modificate il modello. Il seguente codice evidenziato di seguito viene utilizzato per generare un file ONNX nella pipeline delle funzioni. Visualizzare il modello ML *in tempo* reale per l&#39;intera cella del codice della pipeline.

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

Dopo aver completato la pipeline di formazione e modificato i dati attraverso le trasformazioni dei dati, utilizzate la cella seguente per eseguire la formazione.

```python
model = train(config_properties, df_final)
```

### Generazione e caricamento di un modello ONNX

Dopo aver completato un&#39;esecuzione di formazione di successo, è necessario generare un modello ONNX e caricare il modello addestrato nel negozio di modelli Real-time Machine Learning. Dopo aver eseguito le celle seguenti, il modello ONNX viene visualizzato nella barra a sinistra accanto a tutti gli altri notebook.

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>Modificate il valore `model_path` stringa (`model.onnx`) per cambiare il nome del modello.

```python
model_path = "model.onnx"
```

>[!NOTE]
>La cella seguente non è modificabile o eliminabile e è necessaria per il funzionamento dell&#39;applicazione Real-time Machine Learning.

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID : ", model_id)
```

![ONNX, modello](../images/rtml/onnx-model-rail.png)

### Caricamento di un modello ONNX già preparato {#pre-trained-model-upload}

Usando il pulsante di caricamento presente nei [!DNL JupyterLab] notebook, caricate il modello ONNX già preparato nell’ambiente [!DNL Data Science Workspace] dei notebook.

![icona di caricamento](../images/rtml/upload.png)

Quindi, modificare il valore della `model_path` stringa nel blocco appunti XML *in tempo* reale in modo che corrisponda al nome del modello ONNX. Al termine, eseguite la cella del percorso *del modello* Set, quindi eseguite *Carica il modello nella cella archivio* modelli RTML. La posizione del modello e l&#39;ID del modello vengono entrambi restituiti nella risposta in caso di esito positivo.

![caricamento di un modello personalizzato](../images/rtml/upload-own-model.png)

## Creazione di un linguaggio DSL (Domain Specific Language)

In questa sezione viene illustrato come creare un DSL. Stai per creare i nodi che includono la preelaborazione dei dati insieme al nodo ONNX. Quindi, viene creato un grafico DSL utilizzando nodi e bordi. I bordi collegano i nodi utilizzando il formato basato su tuple (node_1, node_2). Il grafico non deve avere cicli.

>[!IMPORTANT]
>
>
>L&#39;utilizzo del nodo ONNX è obbligatorio. Senza il nodo ONNX, l&#39;applicazione non avrà esito positivo.

### Authoring dei nodi

>[!NOTE]
> È probabile che si abbiano più nodi in base al tipo di dati utilizzato. L&#39;esempio seguente delinea un solo nodo nel modello ML *in tempo* reale. Visualizza la sezione Creazione *di* nodi XML *in tempo* reale per l&#39;intera cella del codice.

Il nodo Pandas seguente utilizza `"import": "map"` per importare il nome del metodo come una stringa nei parametri, seguito dall&#39;inserimento dei parametri come una funzione mappa. L&#39;esempio seguente esegue questa operazione utilizzando `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`. Dopo aver posizionato la mappa, potete impostare `inplace` come `True` o `False`. Impostate `inplace` come `True` o `False` in base al fatto che desiderate applicare o meno la trasformazione al suo interno. Per impostazione predefinita `"inplace": False` crea una nuova colonna. Il supporto per fornire un nuovo nome di colonna è impostato per essere aggiunto in una versione successiva. L&#39;ultima riga `cols` può essere un nome di colonna singolo o un elenco di colonne. Specificare le colonne sulle quali si desidera applicare la trasformazione. In questo esempio `leasing` è specificato. Per ulteriori informazioni sui nodi disponibili e su come utilizzarli, consultare la guida [al riferimento ai](./node-reference.md)nodi.

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

Con i nodi creati, il passo successivo consiste nel catena i nodi per creare un grafico.

Per iniziare, elencare tutti i nodi che fanno parte del grafico, creando un array.

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

Quindi, collegare i nodi ai bordi. Ogni tupla è una [!DNL Edge] connessione.

>[!TIP]
> Poiché i nodi sono linearmente dipendenti l&#39;uno dall&#39;altro (ogni nodo dipende dall&#39;output del nodo precedente), è possibile creare collegamenti utilizzando una semplice comprensione dell&#39;elenco Python. Aggiungi le tue connessioni se un nodo dipende da più input.

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

Una volta connessi i nodi, create il grafico. La cella sottostante è obbligatoria e non può essere modificata o eliminata.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

Una volta completato, viene restituito un `edge` oggetto contenente ciascuno dei nodi e i parametri a essi associati.

![edge return](../images/rtml/edge-return.png)

## Pubblica su Edge (Hub)

>[!NOTE]
>L&#39;apprendimento automatico in tempo reale viene temporaneamente distribuito e gestito dall&#39;hub Platform Experience del Adobe . Per ulteriori dettagli, visitare la sezione panoramica sull&#39;architettura [di apprendimento automatico in tempo](./home.md#architecture)reale.

Dopo aver creato un grafico DSL, potete distribuire il grafico al [!DNL Edge].

>[!IMPORTANT]
>Non pubblicare [!DNL Edge] spesso, questo può sovraccaricare i [!DNL Edge] nodi. Non è consigliabile pubblicare lo stesso modello più volte.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### Aggiornamento del DSL e ripubblicazione in Edge (facoltativo)

Se non è necessario aggiornare il DSL, è possibile passare al [punteggio](#scoring).

>[!NOTE]
>Le celle seguenti sono necessarie solo se desiderate aggiornare un DSL esistente pubblicato in Edge.

È probabile che i vostri modelli continueranno a svilupparsi. Invece di creare un nuovo servizio, è possibile aggiornare un servizio esistente con il nuovo modello. Puoi definire un nodo da aggiornare, assegnargli un nuovo ID, quindi caricare nuovamente il nuovo DSL sul [!DNL Edge].

Nell&#39;esempio seguente, il nodo 0 viene aggiornato con un nuovo ID.

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![Nodo aggiornato](../images/rtml/updated-node.png)

Dopo aver aggiornato l’ID del nodo, potete ripubblicare un DSL aggiornato sul bordo.

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

Viene restituito il DSL aggiornato.

![DSL aggiornato](../images/rtml/updated-dsl.png)

## Punteggio {#scoring}

Dopo la pubblicazione in [!DNL Edge], il punteggio viene eseguito da una richiesta di POST da parte di un client. In genere, questo può essere fatto da un&#39;applicazione client che ha bisogno di punteggi ML. Puoi farlo anche da Postman. Il *[!UICONTROL Real-time ML]* modello utilizza EdgeUtils per illustrare questo processo.

>[!NOTE]
>Prima dell&#39;inizio del punteggio è necessario un tempo di elaborazione ridotto.

```python
# Wait for the app to come up
import time
time.sleep(20)
```

Utilizzando lo stesso schema utilizzato per la formazione, vengono generati dati di punteggio di esempio. Questi dati vengono utilizzati per creare un fotogramma dati di punteggio e quindi convertiti in un dizionario di punteggio. Visualizzare il modello ML *in tempo* reale per l&#39;intera cella del codice.

![Dati punteggio](../images/rtml/generate-score-data.png)

### Punteggio rispetto all&#39;endpoint Edge

Utilizzate la cella seguente all’interno del modello ML *in tempo* reale per eseguire il punteggio rispetto al [!DNL Edge] servizio.

![Punteggio rispetto al bordo](../images/rtml/scoring-edge.png)

Una volta completato il punteggio, vengono restituiti l’ [!DNL Edge] URL, il payload e l’output con punteggio del [!DNL Edge] .

## Elenca le app distribuite da [!DNL Edge]

Per generare un elenco delle app attualmente distribuite in [!DNL Edge], eseguite la seguente cella di codice. Impossibile modificare o eliminare la cella.

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

## Eliminare un&#39;app o un ID di servizio distribuito dal [!DNL Edge] (facoltativo)

>[!CAUTION]
>Questa cella viene utilizzata per eliminare l&#39;applicazione Edge distribuita. Non utilizzare la cella seguente a meno che non sia necessario eliminare un&#39; [!DNL Edge] applicazione distribuita.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Passaggi successivi

Seguendo l&#39;esercitazione precedente, è stato completato il training e caricato un modello ONNX nello store del modello Real-time Machine Learning. Inoltre, hai ottenuto un punteggio e implementato il modello di apprendimento automatico in tempo reale. Per ulteriori informazioni sui nodi disponibili per l&#39;authoring dei modelli, consultare la guida [di riferimento ai](./node-reference.md)nodi.