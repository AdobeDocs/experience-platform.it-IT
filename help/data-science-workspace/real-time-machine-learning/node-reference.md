---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real-time Machine Learning;node reference;
solution: Experience Platform
title: Guida di riferimento ai nodi di apprendimento automatico in tempo reale
topic: Nodes reference
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---


# Guida di riferimento ai nodi di apprendimento automatico in tempo reale (Alpha)

>[!IMPORTANT]
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in alfa e viene ancora testata. Questo documento è soggetto a modifiche.

Un nodo è l&#39;unità fondamentale di cui si formano i grafici. Ogni nodo esegue un&#39;attività specifica e può essere concatenato utilizzando i collegamenti per creare un grafico che rappresenta una pipeline ML. L&#39;attività eseguita da un nodo rappresenta un&#39;operazione sui dati di input, ad esempio una trasformazione di dati o schema, o un&#39;inferenza di apprendimento di una macchina. Il nodo genera il valore trasformato o dedotto nei nodi successivi.

La seguente guida illustra le librerie di nodi supportate per l&#39;apprendimento automatico in tempo reale.

## Individuazione di nodi da utilizzare nella pipeline ML

Copiare il codice seguente in un [!DNL Python] blocco appunti per visualizzare tutti i nodi disponibili per l&#39;uso.

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

I nodi standard si basano su librerie open source di scienza dei dati come Pandas e ScikitLearn.

### ModelUpload

Il nodo ModelUpload è un nodo di Adobe  interno che prende un percorso_modello e carica il modello dal percorso del modello locale all&#39;archivio BLOB di apprendimento automatico in tempo reale.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode è un nodo di Adobe  interno che richiede un ID modello per il pulling del modello ONNX preformato e lo utilizza per il punteggio sui dati in arrivo.

>[!TIP]
>Specificare le colonne nello stesso ordine in cui si desidera inviare i dati al modello ONNX per la valutazione.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Panda {#pandas}

Il seguente nodo Pandas consente di importare qualsiasi `pd.DataFrame` metodo o qualsiasi funzione di primo livello generale panda. Per ulteriori informazioni sui metodi Pandas, consulta la documentazione sui metodi [Pandas](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). Per ulteriori informazioni sulle funzioni di primo livello, consultate la guida di riferimento API [Pandas per le funzioni](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html)generali.

Il nodo seguente utilizza `"import": "map"` per importare il nome del metodo come una stringa nei parametri, seguito dall&#39;inserimento dei parametri come una funzione mappa. L&#39;esempio seguente esegue questa operazione utilizzando `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Dopo aver posizionato la mappa, potete impostare `inplace` come `True` o `False`. Impostate `inplace` come `True` o `False` in base al fatto che desiderate applicare o meno la trasformazione al suo interno. Per impostazione predefinita `"inplace": False` crea una nuova colonna. Il supporto per fornire un nuovo nome di colonna è impostato per essere aggiunto in una versione successiva. L&#39;ultima riga `cols` può essere un nome di colonna singolo o un elenco di colonne. Specificare le colonne sulle quali si desidera applicare la trasformazione. In questo esempio `device` è specificato.

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

Il nodo ScikitLearn consente di importare qualsiasi modello o scalatore di ScikitLearn ML. Utilizzate la tabella seguente per ulteriori informazioni su uno dei valori utilizzati nell&#39;esempio:

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver" : 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Valore | Descrizione |
| --- | --- |
| funzionalità | Inserire le feature nel modello (elenco di stringhe). <br> Ad esempio: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Nome colonna Target (stringa). |
| mode | Treno/prova (stringa). |
| model_path | Percorso del modello di salvataggio locale in formato onnx. |
| params.model | Percorso di importazione assoluto del modello (stringa), ad esempio: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Per ulteriori informazioni, vedete la documentazione API [sklearn (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) . |
| node_instance.process(data_message_from_previous_node) | Il metodo `process()` prende DataMsg dal nodo precedente e applica la trasformazione. Dipende dal nodo corrente in uso. |

### Dividere

Utilizzate il seguente nodo per suddividere il dataframe in treno e verificare passando `train_size` o `test_size`. Questo restituisce un fotogramma dati con un indice multiplo. Potete accedere ai frame di dati del treno e del test utilizzando l&#39;esempio seguente `msg5.data.xs(“train”)`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Passaggi successivi

Il passaggio successivo consiste nel creare nodi da utilizzare per il punteggio di un modello di apprendimento automatico in tempo reale. Per ulteriori informazioni, consultare la guida [utente del notebook](./rtml-authoring-notebook.md)Real-time Machine Learning.
