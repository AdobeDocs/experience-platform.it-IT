---
keywords: Experience Platform;guida per sviluppatori;Data Science Workspace;argomenti popolari;machine learning in tempo reale;riferimento nodo;
solution: Experience Platform
title: Riferimento nodo di apprendimento automatico in tempo reale
description: Un nodo è l'unità fondamentale di cui vengono formati i grafici. Ogni nodo esegue un’attività specifica e può essere collegato utilizzando dei collegamenti per formare un grafico che rappresenta una pipeline ML. L’attività eseguita da un nodo rappresenta un’operazione sui dati di input, ad esempio una trasformazione di dati o schemi, o un’inferenza di apprendimento automatico. Il nodo restituisce il valore trasformato o dedotto ai nodi successivi.
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# Riferimento nodo di Machine Learning in tempo reale (Alpha)

>[!IMPORTANT]
>
>Real-time Machine Learning non è ancora disponibile per tutti gli utenti. Questa funzione è in formato alfa ed è ancora in fase di test. Questo documento è soggetto a modifiche.

Un nodo è l&#39;unità fondamentale di cui vengono formati i grafici. Ogni nodo esegue un’attività specifica e può essere collegato utilizzando dei collegamenti per formare un grafico che rappresenta una pipeline ML. L’attività eseguita da un nodo rappresenta un’operazione sui dati di input, ad esempio una trasformazione di dati o schemi, o un’inferenza di apprendimento automatico. Il nodo restituisce il valore trasformato o dedotto ai nodi successivi.

La guida seguente illustra le librerie di nodi supportate per Real-time Machine Learning.

## Individuazione dei nodi da utilizzare nella pipeline ML

Copia il seguente codice in una [!DNL Python] per visualizzare tutti i nodi disponibili per l&#39;uso.

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**Esempio di risposta**

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

## Nodi standard

I nodi standard si basano su librerie open source di dati scientifici come Pandas e ScikitLearn.

### ModelUpload

Il nodo ModelUpload è un nodo di Adobe interno che utilizza un percorso_modello e carica il modello dal percorso del modello locale nell&#39;archivio BLOB di Machine Learning in tempo reale.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode è un nodo di Adobe interno che utilizza un ID modello per richiamare il modello ONNX pre-addestrato e lo utilizza per valutare i dati in arrivo.

>[!TIP]
>
>Specificare le colonne nello stesso ordine in cui si desidera inviare i dati al modello ONNX per il punteggio.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Panda {#pandas}

Il seguente nodo Pandas consente di importare qualsiasi `pd.DataFrame` o una funzione generale di livello superiore dei panda. Per ulteriori informazioni sui metodi Pandas, visitare il [Documentazione sui metodi Pandas](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). Per ulteriori informazioni sulle funzioni di primo livello, visitare il [Guida di riferimento API Pandas per funzioni generali](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

Il nodo seguente utilizza `"import": "map"` per importare il nome del metodo come stringa nei parametri, seguito dall&#39;immissione dei parametri come funzione di mappa. L’esempio seguente esegue questa operazione utilizzando `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Dopo aver impostato la mappa, puoi impostare `inplace` as `True` o `False`. Imposta `inplace` as `True` o `False` a seconda che si desideri applicare la trasformazione sul posto o meno. Per impostazione predefinita `"inplace": False` crea una nuova colonna. Il supporto per fornire un nuovo nome di colonna è impostato per essere aggiunto in una versione successiva. Ultima riga `cols` può essere un nome di colonna singolo o un elenco di colonne. Specificare le colonne alle quali applicare la trasformazione. In questo esempio `device` è specificato.

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

### ScikitLearn

Il nodo ScikitLearn consente di importare qualsiasi modello o scalatore ScikitLearn ML. Utilizza la tabella seguente per ulteriori informazioni su uno qualsiasi dei valori utilizzati nell’esempio:

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
| funzioni | Inserite le feature nel modello (elenco di stringhe). <br> Ad esempio: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Nome colonna di destinazione (stringa). |
| modalità | Treno/prova (stringa). |
| percorso_modello | Percorso del modello di salvataggio locale in formato onnx. |
| params.model | Percorso di importazione assoluto del modello (stringa), ad esempio: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | iperparametri del modello, vedere [API sklearn (mappa/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) per ulteriori informazioni. |
| node_instance.process(data_message_from_previous_node) | Il metodo `process()` prende DataMsg dal nodo precedente e applica la trasformazione. Questo dipende dal nodo corrente utilizzato. |

### Dividere

Utilizza il seguente nodo per suddividere il dataframe in treno e testare passando `train_size` o `test_size`. Questo restituisce un dataframe con più indici. È possibile accedere ai dataframe dei treni e dei test utilizzando l&#39;esempio seguente: `msg5.data.xs("train")`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Passaggi successivi

Il passaggio successivo consiste nel creare nodi da utilizzare per il punteggio di un modello di apprendimento automatico in tempo reale. Per ulteriori informazioni, visitare il [Guida utente del notebook di apprendimento automatico in tempo reale](./rtml-authoring-notebook.md).
