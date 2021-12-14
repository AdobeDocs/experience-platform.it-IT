---
keywords: Experience Platform;guida per gli sviluppatori;Data Science Workspace;argomenti comuni;Real-time Machine Learning;riferimento al nodo;
solution: Experience Platform
title: Riferimento al nodo di apprendimento automatico in tempo reale
topic-legacy: Nodes reference
description: Un nodo è l'unità fondamentale di cui si formano i grafici. Ogni nodo esegue un'attività specifica e può essere concatenato utilizzando i collegamenti per formare un grafico che rappresenta una pipeline ML. L'attività eseguita da un nodo rappresenta un'operazione sui dati di input, ad esempio una trasformazione di dati o schemi o un'inferenza di apprendimento automatico. Il nodo restituisce il valore trasformato o dedotto ai nodi successivi.
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# Riferimento del nodo di apprendimento automatico in tempo reale (Alpha)

>[!IMPORTANT]
>
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in alfa e viene ancora testata. Questo documento è soggetto a modifiche.

Un nodo è l&#39;unità fondamentale di cui si formano i grafici. Ogni nodo esegue un&#39;attività specifica e può essere concatenato utilizzando i collegamenti per formare un grafico che rappresenta una pipeline ML. L&#39;attività eseguita da un nodo rappresenta un&#39;operazione sui dati di input, ad esempio una trasformazione di dati o schemi o un&#39;inferenza di apprendimento automatico. Il nodo restituisce il valore trasformato o dedotto ai nodi successivi.

La guida seguente illustra le librerie di nodi supportate per il machine learning in tempo reale.

## Esplorazione dei nodi da utilizzare nella pipeline ML

Copia il seguente codice in un [!DNL Python] per visualizzare tutti i nodi disponibili.

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**Risposta di esempio**

```json
{'FieldOps': 'rtml_nodelibs.nodes.standard.preprocessing.fieldops.FieldOps',
 'FieldTrans': 'rtml_nodelibs.nodes.standard.preprocessing.fieldtrans.FieldTrans',
 'ModelUpload': 'rtml_nodelibs.nodes.standard.ml.artifact_utils.ModelUpload',
 'ONNXNode': 'rtml_nodelibs.nodes.standard.ml.onnx.ONNXNode',
 'Pandas': 'rtml_nodelibs.nodes.standard.preprocessing.pandasnode.Pandas',
 'Processor': 'rtml_nodelibs.nodes.standard.preprocessing.processor.Processor',
 'Receiver': 'rtml_nodelibs.nodes.standard.preprocessing.receiver.Receiver',
 'ScikitLearn': 'rtml_nodelibs.nodes.standard.ml.scikitlearn.ScikitLearn',
 'Simulator': 'rtml_nodelibs.nodes.standard.preprocessing.simulator.Simulator',
 'Split': 'rtml_nodelibs.nodes.standard.preprocessing.splitter.Split'}
```

## Nozioni standard

I nodi standard si basano su librerie open source di scienza dei dati come Pandas e ScikitLearning.

### ModelUpload

Il nodo ModelUpload è un nodo di Adobe interno che prende un percorso_modello e carica il modello dal percorso del modello locale all&#39;archivio BLOB di apprendimento automatico in tempo reale.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode è un nodo di Adobe interno che prende un ID modello per richiamare il modello ONNX pre-addestrato e lo utilizza per segnare i dati in arrivo.

>[!TIP]
>
>Specificare le colonne nello stesso ordine in cui si desidera inviare i dati al modello ONNX per ottenere il punteggio.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Panda {#pandas}

Il seguente nodo Panda consente di importare qualsiasi `pd.DataFrame` o qualsiasi funzione generale di livello superiore dei panda. Per ulteriori informazioni sui metodi Pandas, visita il [Documentazione sui metodi dei panda](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). Per ulteriori informazioni sulle funzioni di primo livello, visita il [Guida di riferimento API per i panda per le funzioni generali](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

Il nodo seguente utilizza `"import": "map"` per importare il nome del metodo come stringa nei parametri, quindi inserendo i parametri come funzione mappa. L’esempio seguente lo fa utilizzando `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Dopo aver impostato la mappa, puoi scegliere di `inplace` come `True` o `False`. Imposta `inplace` come `True` o `False` a seconda che si desideri applicare o meno la trasformazione al suo interno. Per impostazione predefinita `"inplace": False` crea una nuova colonna. Il supporto per fornire un nuovo nome di colonna deve essere impostato per essere aggiunto in una versione successiva. Ultima riga `cols` può essere un nome di colonna singolo o un elenco di colonne. Specificare le colonne alle quali si desidera applicare la trasformazione. In questo esempio `device` è specificato.

```python
#  df["device"] = df["device"].map({"Desktop":1, "Mobile":0}, na_action=0)
 
node_device_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0},
    "inplace": True,
    "cols": "device"})
 
 
# df["browser"] = df["browser"].map({"chrome": 1, "firefox": 0}, "na_action": 0})
 
node_browser_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"chrome": 1, "firefox": 0}, "na_action": 0},
    "inplace": True,
    "cols": "browser"})
```

### ScikitImpara

Il nodo ScikitLearning consente di importare qualsiasi modello o scaler di ScikitImpara ML. Utilizza la tabella seguente per ulteriori informazioni su uno dei valori utilizzati nell’esempio:

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver": 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Valore | Descrizione |
| --- | --- |
| caratteristiche | Feature di input nel modello (elenco di stringhe). <br> Ad esempio: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Nome della colonna di destinazione (stringa). |
| modalità | Treno/prova (stringa). |
| model_path | Percorso del modello di salvataggio locale in formato onnx. |
| params.model | Percorso di importazione assoluto del modello (stringa), ad esempio: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Iperparametri del modello, vedere [API sklearn (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) documentazione per ulteriori informazioni. |
| node_instance.process(data_message_from_previous_node) | Il metodo `process()` prende DataMsg dal nodo precedente e applica la trasformazione. Questo dipende dal nodo corrente utilizzato. |

### Dividere

Usa il seguente nodo per dividere il dataframe in treno e test passando `train_size` o `test_size`. Questo restituisce un dataframe con un multi-indice. È possibile accedere ai fotogrammi dati del treno e del test utilizzando l&#39;esempio seguente: `msg5.data.xs(“train”)`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Passaggi successivi

Il passaggio successivo consiste nel creare nodi da utilizzare per il punteggio di un modello di apprendimento automatico in tempo reale. Per ulteriori informazioni, visita il [Guida utente del notebook Real-time Machine Learning](./rtml-authoring-notebook.md).
