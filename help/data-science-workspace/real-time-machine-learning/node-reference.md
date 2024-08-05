---
keywords: Experience Platform; guida per sviluppatori; Data Science Area di lavoro; argomenti popolari; Machine Learning in tempo reale; riferimento al nodo;
solution: Experience Platform
title: Riferimento per i nodi di Machine Learning in tempo reale
description: Un nodo è l'unità fondamentale di cui sono formati i grafici. Ogni nodo esegue un'attività specifica e possono essere concatenati utilizzando collegamenti per formare un grafico che rappresenta una pipeline ML. L'attività eseguita da un nodo rappresenta un'operazione sui dati di input, ad esempio una trasformazione di dati o schemi o un'inferenza di Machine Learning. Il nodo emette il valore trasformato o dedotto ai nodi successivi.
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 9030a5482d4ea2b54426680cef92b89e68ef5b33
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Riferimento ai nodi di Machine Learning in tempo reale (Alpha)

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

>[!IMPORTANT]
>
>L&#39;apprendimento automatico in tempo reale non è ancora disponibile per tutti gli utenti. Questa funzione è in versione alpha ed è ancora in fase di test. Questo documento è soggetto a modifiche.

Un nodo è l&#39;unità fondamentale di cui sono formati i grafici. Ogni nodo esegue un&#39;attività specifica e possono essere concatenati utilizzando collegamenti per formare un grafico che rappresenta una pipeline ML. L&#39;attività eseguita da un nodo rappresenta un&#39;operazione sui dati di input, ad esempio una trasformazione di dati o schemi o un&#39;inferenza di Machine Learning. Il nodo emette il valore trasformato o dedotto ai nodi successivi.

La guida seguente delinea i librerie di nodo supportati per l&#39;apprendimento automatico in tempo reale.

## Individuazione dei nodi da utilizzare nella pipeline ML

Copiare il codice riportato di seguito in un [!DNL Python] blocco appunti per visualizzare tutti i nodi disponibili per l&#39;uso.

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

## Nodi standard

I nodi standard versione su librerie di data science open source come Pandas e ScikitLearn.

### Caricamento modello

Il nodo ModelUpload è un nodo Adobe Systems interno che accetta un model_path e carica il modello dal percorso del modello locale al BLOB Real-time Machine Learning BLOB store.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode è un nodo Adobe Systems interno che accetta un ID modello per richiamare il modello ONNX pre-addestrato e lo utilizza per assegnare un punteggio ai dati in ingresso.

>[!TIP]
>
>Specificare le colonne nello stesso ordine in cui si desidera like i dati da inviare al modello ONNX per il punteggio.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Panda {#pandas}

Il seguente nodo Pandas consente di importare qualsiasi `pd.DataFrame` metodo o qualsiasi funzione generale di livello superiore dei panda. Per ulteriori informazioni sui metodi Pandas, visita la documentazione](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html) sui [metodi Pandas. Per ulteriori informazioni sulle funzioni di primo livello, visita la guida di riferimento API [Pandas per le funzioni](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html) generali.

Il nodo seguente viene utilizzato `"import": "map"` per importare il nome del metodo come stringa nei parametri, seguito dall&#39;immissione dei parametri come funzione mappa. L&#39;esempio seguente esegue questa operazione utilizzando `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Una volta impostata la mappa, è possibile impostarla `inplace` come `True` o `False`. Imposta `inplace` come `True` o `False` in base al fatto che desideri applicare o meno la trasformazione. Per impostazione predefinita `"inplace": False` crea una nuova colonna. Il supporto per fornire un nuovo nome di colonna è impostato per essere aggiunto in una versione successiva. L&#39;ultima riga `cols` può essere un nome di una singola colonna o un elenco di colonne. Specificare le colonne a cui applicare la trasformazione. In questo esempio `device` è specificato.

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

Il nodo ScikitLearn consente di importare qualsiasi modello o scaler ScikitLearn ML. Utilizzare la tabella seguente per ulteriori informazioni sui valori utilizzati nell&#39;esempio:

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
| tratti somatici | Funzioni di input per il modello (elenco di stringhe). <br>Ad esempio: `browser`, `device`, , `login_page`, `product_page``search_page` |
| etichetta | Target nome colonna (stringa). |
| modo | Treno/test (stringa). |
| model_path | Percorso del modello di salvataggio locale in formato onnx. |
| params.model | Percorso di importazione assoluto del modello (stringa), ad esempio: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Modellare gli iperparametri, vedere la documentazione dell&#39;API [sklearn (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) per ulteriori informazioni. |
| node_istanza.process(data_message_from_previous_node) | Il metodo `process()` accetta DataMsg dal nodo precedente e applica la trasformazione. Questo dipende dal nodo corrente utilizzato. |

### Dividi

Utilizza il seguente nodo per suddividere il frame di dati in training ed eseguire il test passando `train_size` o `test_size`. In questo modo viene restituito un frame di dati con un indice multiplo. È possibile accesso eseguire il training e testare i frame di dati utilizzando l&#39;esempio seguente, `msg5.data.xs("train")`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Passaggi successivi

Il passaggio successivo consiste nel creare nodi da utilizzare per assegnare un punteggio a un modello di Machine Learning in tempo reale. Per altre informazioni, visita la Guida](./rtml-authoring-notebook.md) all&#39;utente di [Appunti di Machine Learning in tempo reale.
