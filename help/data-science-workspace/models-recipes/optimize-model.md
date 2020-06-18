---
keywords: Experience Platform;optimize;model;Data Science Workspace;popular topics
solution: Experience Platform
title: Ottimizzare un modello
topic: Tutorial
translation-type: tm+mt
source-git-commit: 7dc5075d3101b4780af92897c0381e73a9c5aef0
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 0%

---


# Ottimizzare un modello utilizzando il framework Model Insights

Model Insights Framework fornisce agli esperti di dati strumenti in Data Science Workspace per effettuare scelte rapide e informate per modelli ottimali di machine learning basati su esperimenti. Il quadro migliorerà la velocità e l&#39;efficacia del flusso di lavoro di apprendimento automatico e migliorerà la facilità d&#39;uso per gli esperti in materia di dati. A tal fine, viene fornito un modello predefinito per ciascun tipo di algoritmo di machine learning per facilitare l&#39;ottimizzazione del modello. Il risultato finale consente agli esperti di data mining e ai cittadini di prendere decisioni migliori in merito all&#39;ottimizzazione dei modelli per i clienti finali.

## Cosa sono le metriche?

Dopo aver implementato e addestrato un modello, il passo successivo che uno scienziato farebbe è quello di trovare le prestazioni del modello. Varie metriche vengono utilizzate per determinare l&#39;efficacia del confronto tra un modello e gli altri. Alcuni esempi di metriche utilizzate:
- Precisione della classificazione
- Area sotto curva
- Matrice di fusione
- Report classificazione

## Configurazione del codice di ricetta

Al momento, Model Insights Framework supporta i seguenti runtime:
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

Il codice di esempio per le ricette è disponibile nell’archivio di riferimento [](https://github.com/adobe/experience-platform-dsw-reference) experience-platform-dsw in `recipes`. Per questa esercitazione verranno utilizzati riferimenti a file specifici provenienti da questo archivio.

### Scala {#scala}

Esistono due modi per inserire le metriche nelle ricette. Uno consiste nell’utilizzare le metriche di valutazione predefinite fornite dall’SDK e l’altro nel scrivere metriche di valutazione personalizzate.

#### Metriche di valutazione predefinite per Scala

Le valutazioni predefinite sono calcolate come parte degli algoritmi di classificazione. Di seguito sono riportati alcuni valori predefiniti per i valutatori attualmente implementati:

| Classe Valutatore | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEevaluate | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEevaluate | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEevaluate | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

Il valutatore può essere definito nella definizione nel file [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) nella `recipe` cartella. Di seguito `DefaultBinaryClassificationEvaluator` è riportato un esempio di codice che consente di:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Una volta attivata la classe di un valutatore, per impostazione predefinita durante la formazione vengono calcolate alcune metriche. Le metriche predefinite possono essere dichiarate esplicitamente aggiungendo la riga seguente alla `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE] Se la metrica non è definita, le metriche predefinite saranno attive.

È possibile abilitare una metrica specifica modificando il valore per `evaluation.metrics.com`. Nell&#39;esempio seguente, la metrica F-Score è abilitata.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

Nella tabella seguente sono riportate le metriche predefinite per ciascuna classe. Un utente può anche utilizzare i valori della `evaluation.metric` colonna per abilitare una metrica specifica.

| `evaluator.class` | Metriche predefinite | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | -Matrice <br>di <br>conversione di precisione <br>-F-Precisione <br>-Precisione- <br>Ricevitore Caratteristiche <br>Operative Sotto Le Caratteristiche Operative Del Ricevitore | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Matrice <br>di <br>conversione di precisione <br>-F-Precisione <br>-Precisione- <br>Ricevitore Caratteristiche <br>Operative Sotto Le Caratteristiche Operative Del Ricevitore | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Media Media di precisione (MAP) <br>normalizzata - Guadagno cumulativo <br>medio <br>metrico K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Metriche di valutazione personalizzate per Scala

Il valutatore personalizzato può essere fornito estendendo l&#39;interfaccia di `MLEvaluator.scala` nel `Evaluator.scala` file. Nel file [Evalutazione.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) di esempio, definiamo funzioni `split()` e funzioni personalizzate `evaluate()` . La nostra `split()` funzione divide i nostri dati in modo casuale con un rapporto di 8:2 e la nostra `evaluate()` funzione definisce e restituisce 3 metriche: MAPE, MAE e RMSE.

>[!IMPORTANT] Per la `MLMetric` classe, non utilizzare `"measures"` per `valueType` la creazione di un&#39;altra metrica `MLMetric` la metrica non verrà compilata nella tabella delle metriche di valutazione personalizzate.
>  
> Effettuate le seguenti operazioni: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Non questo: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Una volta definito nella ricetta, il passo successivo consiste nell&#39;attivarlo nelle ricette. Ciò viene fatto nel file [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) nella `resources` cartella del progetto. Qui `evaluation.class` è impostata sulla `Evaluator` classe definita in `Evaluator.scala`

```properties
evaluation.class=com.adobe.platform.ml.Evaluator
```

In Data Science Workspace, l&#39;utente potrebbe vedere le informazioni nella scheda &quot;Metriche di valutazione&quot; nella pagina dell&#39;esperimento.

### Python/Tensorflow {#pythontensorflow}

Al momento, non esistono metriche di valutazione predefinite per Python o Tensorflow. Pertanto, per ottenere le metriche di valutazione per Python o Tensorflow, dovrete creare una metrica di valutazione personalizzata. Questo può essere fatto implementando la `Evaluator` classe.

#### Metriche di valutazione personalizzate per Python

Per le metriche di valutazione personalizzate, è necessario implementare due metodi principali per il valutatore: `split()` e `evaluate()`.

Per Python, questi metodi sarebbero definiti in [evaluate.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) per la `Evaluator` classe. Seguite il collegamento [evaluate.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) per un esempio del `Evaluator`.

La creazione di metriche di valutazione in Python richiede l&#39;implementazione di `evaluate()` e `split()` metodi.

Il `evaluate()` metodo restituisce l&#39;oggetto della metrica che contiene un array di oggetti della metrica con proprietà di `name`, `value`e `valueType`.

Lo scopo del `split()` metodo è quello di inserire i dati e trasmettere un training e un set di dati di prova. Nel nostro esempio, il `split()` metodo immette i dati utilizzando l’ `DataSetReader` SDK e li pulisce rimuovendo le colonne non correlate. Da qui vengono create funzioni aggiuntive a partire dalle feature non elaborate esistenti nei dati.

Il `split()` metodo deve restituire un quadro di dati di formazione e di prova che viene poi utilizzato dai `pipeline()` metodi per addestrare e testare il modello ML.

#### Metriche di valutazione personalizzate per Tensorflow

Per Tensorflow, simile a Python, i metodi `evaluate()` e `split()` nella `Evaluator` classe dovranno essere implementati. Ad `evaluate()`esempio, le metriche devono essere restituite mentre `split()` restituisce i set di dati del treno e del test.

```PYTHON
from ml.runtime.python.Interfaces.AbstractEvaluator import AbstractEvaluator

class Evaluator(AbstractEvaluator):
    def __init__(self):
       print ("initiate")

    def evaluate(self, data=[], model={}, config={}):

        return metrics

    def split(self, config={}):

       return 'train', 'test'
```

### R {#r}

Al momento, non esistono metriche di valutazione predefinite per R. Pertanto, per ottenere le metriche di valutazione per R, dovrete definire la `applicationEvaluator` classe come parte della ricetta.

#### Metriche di valutazione personalizzate per R

Lo scopo principale di `applicationEvaluator` è restituire un oggetto JSON contenente coppie chiave-valore di metriche.

Questo [esempio può essere utilizzato da applicationEevaluate.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) . In questo esempio, la sezione `applicationEvaluator` è suddivisa in tre sezioni familiari:
- Carica dati
- Preparazione/progettazione di funzioni
- Recuperare il modello salvato e valutare

I dati vengono caricati per la prima volta in un dataset da un&#39;origine come definita in [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). Da qui, i dati vengono puliti e progettati per adattarsi al modello di apprendimento della macchina. Infine, il modello è utilizzato per fare una previsione utilizzando il nostro dataset e dai valori previsti e dai valori effettivi, le metriche sono calcolate. In questo caso, MAPE, MAE e RMSE sono definiti e restituiti nell&#39; `metrics` oggetto.

## Utilizzo di metriche e grafici di visualizzazione predefiniti

Sensei Model Insights Framework supporterà un modello predefinito per ciascun tipo di algoritmo di machine learning. La tabella seguente mostra le classi comuni di algoritmi di machine learning ad alto livello e le metriche di valutazione e le visualizzazioni corrispondenti.

| Tipo di algoritmo ML | Metriche di valutazione | Visualizzazioni |
--- | --- | ---
| Regressione | - RMSE<br>- MAPE<br>- MASE<br>- MASE | Curva di sovrapposizione valori previsti e valori effettivi |
| Classificazione binaria | - Matrice<br>di fusione - Precisione-richiamo<br>- Precisione<br>- punteggio F (in particolare F1,F2)<br>- AUC<br>- ROC | Curva ROC e matrice confusione |
| Classificazione multiclasse | -Matrice di conversione <br>- Per ogni classe: <br>- precisione del richiamo <br>- punteggio F (in particolare F1, F2) | Curva ROC e matrice confusione |
| Clustering (con verità a terra) | - NMI (valutazione normalizzata delle informazioni reciproche), AMI (valutazione rettificata delle informazioni reciproche)<br>- RI (indice Rand), ARI (indice Rand rettificato)<br>- punteggio di omogeneità, punteggio di completezza e misura<br>V- FMI (indice Fowlkes-Mallow)<br>- Purezza<br>- indice Jaccard | Grafico cluster che mostra cluster e centroidi con dimensioni cluster relative che riflettono i punti dati del cluster |
| Clustering (senza verità di fondo) | - Inerzia<br>- Coefficiente<br>della silhouette- CHI (indice di Calinski-Harabaz)<br>- DBI (indice di Davies-Bouldin)<br>- Indice di Dunn | Grafico cluster che mostra cluster e centroidi con dimensioni cluster relative che riflettono i punti dati del cluster |
| Consiglio | -Media Media di precisione (MAP) <br>normalizzata - Guadagno cumulativo <br>medio <br>metrico K | TBD |
| TensorFlow, casi di utilizzo | Analisi modello TensorFlow (TFMA) | Confronto tra il modello di rete neurale e la visualizzazione |
| Meccanismo di acquisizione di altri/errori | Logica metrica personalizzata (e grafici di valutazione corrispondenti) definita dall&#39;autore del modello. Gestione degli errori in caso di mancata corrispondenza del modello | Tabella con coppie chiave-valore per le metriche di valutazione |
