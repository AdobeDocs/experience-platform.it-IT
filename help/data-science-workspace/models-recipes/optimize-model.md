---
keywords: Experience Platform; ottimizzare; modello; Data Science Area di lavoro; argomenti popolari; Informazioni sul modello
solution: Experience Platform
title: Ottimizzare un modello utilizzando Model Insights Framework
type: Tutorial
description: Il Model Insights Framework fornisce al data scientist gli strumenti in Data Science Area di lavoro per effettuare scelte rapide e informate per modelli di machine learning ottimali basati su esperimenti.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 0%

---

# Ottimizzare un modello utilizzando il framework di Insights del modello

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

Il Model Insights Framework fornisce al data scientist gli strumenti per [!DNL Data Science Workspace] effettuare scelte rapide e informate per modelli di machine learning ottimali basati su esperimenti. Il framework migliorerà la velocità e l&#39;efficacia del workflow di apprendimento automatico, oltre a migliorare la facilità d&#39;uso per i data scientist. Questo viene fatto fornendo un modello predefinito per ogni tipo di algoritmo di Machine Learning per facilitare l&#39;ottimizzazione del modello. Il risultato finale consente ai data scientist e ai citizen data scientist di prendere decisioni migliori sull&#39;ottimizzazione dei modelli per i loro clienti finali.

## Cosa sono le metriche?

Dopo aver implementato e training un modello, il passaggio successivo che un data scientist farebbe è scoprire le prestazioni del modello. Vengono utilizzate varie metriche per determinare l&#39;efficacia di un modello rispetto ad altri. Alcuni esempi di metriche utilizzate includono:
- Accuratezza della classificazione
- Area sotto curva
- Matrice di confusione
- Rapporto di classificazione

## Configurazione del codice ricetta

Attualmente, Model Insights Framework supporta i seguenti runtime:
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

Il codice di esempio per le ricette si trova nell&#39;archivio [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) in `recipes`. In questa esercitazione verrà fatto riferimento a file specifici da questo archivio.

### Scala {#scala}

Esistono due modi per inserire le metriche nelle ricette. Una consiste nell’utilizzare le metriche di valutazione predefinite fornite dall’SDK e l’altra consiste nel scrivere metriche di valutazione personalizzate.

#### Metriche di valutazione predefinite per Scala

Le valutazioni predefinite vengono calcolate come parte degli algoritmi di classificazione. Di seguito sono riportati alcuni valori predefiniti per i valutatori attualmente implementati:

| Classe valutatore | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| Valutatore consigli | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

Il valutatore può essere definito nella ricetta nel file [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) nella cartella `recipe`. Di seguito è riportato un esempio di codice che abilita `DefaultBinaryClassificationEvaluator`:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Per impostazione predefinita, dopo l’abilitazione di una classe di valutatore, durante l’apprendimento viene calcolata una serie di metriche. Le metriche predefinite possono essere dichiarate esplicitamente aggiungendo la seguente riga al tuo `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Se la metrica non è definita, le metriche predefinite saranno attive.

È possibile abilitare una metrica specifica modificando il valore di `evaluation.metrics.com`. Nell&#39;esempio seguente, la metrica F-Score è abilitata.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

Nella tabella seguente sono riportate le metriche predefinite per ogni classe. Un utente può anche utilizzare i valori nella `evaluation.metric` colonna per abilitare una metrica specifica.

| `evaluator.class` | Metriche predefinite | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precisione <br>-Richiamo <br>-Matrice <br>di confusione -F-Score <br>-Accuratezza <br>-Caratteristiche <br>operative del ricevitore -Area sotto le caratteristiche operative del ricevitore | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>- -`ROC` <br>`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Matrice di confusione <br>-F-Score <br>-Accuracy <br>-Caratteristiche operative del ricevitore <br>-Area sotto le caratteristiche operative del ricevitore | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Precisione media media (MAP) <br>-guadagno cumulativo scontato normalizzato -rango <br><br>reciproco medio -metrico k | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>- -`MRR` <br>`METRIC_K` |


#### Metriche di valutazione personalizzate per Scala

È possibile fornire un valutatore personalizzato estendendo l&#39;interfaccia di `MLEvaluator.scala` nel file `Evaluator.scala`. Nel file [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) di esempio vengono definite le funzioni personalizzate `split()` e `evaluate()`. La funzione `split()` suddivide i dati in modo casuale con un rapporto di 8:2 e la funzione `evaluate()` definisce e restituisce 3 metriche: MAPE, MAE e RMSE.

>[!IMPORTANT]
>
>Per la classe `MLMetric`, non utilizzare `"measures"` per `valueType` durante la creazione di un nuovo `MLMetric`. In caso contrario, la metrica non verrà popolata nella tabella delle metriche di valutazione personalizzata.
>  
> Esegui questa operazione: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Non questo: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Una volta definita nella ricetta, il passaggio successivo è quello di abilitarla nelle ricette. Questa operazione viene eseguita nel [file applicazione.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) nella cartella del `resources` progetto. Qui è `evaluation.class` impostato sulla `Evaluator` classe definita in `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

[!DNL Data Science Workspace]In , il utente sarebbe in grado di vedere gli approfondimenti nella scheda &quot;Metriche di valutazione&quot; nella pagina dell&#39;esperimento.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Al momento, non esistono metriche di valutazione predefinite per [!DNL Python] o [!DNL Tensorflow]. Pertanto, per ottenere le metriche di valutazione per [!DNL Python] o [!DNL Tensorflow], sarà necessario creare una metrica di valutazione personalizzata. Questo può essere fatto implementando la `Evaluator` classe.

#### Metriche di valutazione personalizzate per [!DNL Python]

Per le metriche di valutazione personalizzate, esistono due metodi principali che devono essere implementati per il valutatore: `split()` e `evaluate()`.

Per [!DNL Python], questi metodi sarebbero definiti in [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) per la `Evaluator` classe. Seguire il [collegare evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) per un esempio di `Evaluator`.

La creazione di metriche di valutazione richiede [!DNL Python] che il utente implementare i `evaluate()` metodi and `split()` .

Il `evaluate()` metodo restituisce l&#39;oggetto metrico che contiene una matrice di oggetti metrici con proprietà di `name`, `value`, e `valueType`.

Lo scopo del metodo è quello di inserire dati e generare un training e un set di `split()` dati di test. Nel nostro esempio, il `split()` metodo immette i dati utilizzando l&#39;SDK `DataSetReader` e quindi pulisce i dati rimuovendo le colonne non correlate. Da lì, vengono create funzionalità aggiuntive dalle funzionalità non elaborate esistenti nei dati.

Il `split()` metodo deve restituire un frame di dati di training e test che viene quindi utilizzato dai `pipeline()` metodi per addestrare e testare il modello ML.

#### Metriche di valutazione personalizzate per Tensorflow

Per [!DNL Tensorflow], simile a [!DNL Python], i metodi `evaluate()` e `split()` nella `Evaluator` classe dovranno essere implementati. Per `evaluate()`, le metriche devono essere restituite mentre `split()` restituisce il treno e i set di dati di prova.

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

Al momento, non esistono metriche di valutazione predefinite per R. Pertanto, per ottenere le metriche di valutazione per R, è necessario definire la `applicationEvaluator` classe come parte della ricetta.

#### Metriche di valutazione personalizzate per R

Lo scopo principale del `applicationEvaluator` è restituire un oggetto JSON contenente coppie chiave-valore di metriche.

Questa [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) può essere utilizzata come esempio. In questo esempio, la è suddivisa in `applicationEvaluator` tre sezioni familiari:
- Carica dati
- Preparazione dei dati/progettazione delle funzioni
- Recupera il modello salvato e valuta

I dati vengono prima caricati in un set di dati da un&#39;origine come definito in [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). Da lì, i dati vengono puliti e progettati per adattarsi al modello di apprendimento automatico. Infine, il modello viene utilizzato per effettuare una previsione utilizzando il nostro set di dati; vengono calcolate le metriche in base ai valori previsti e ai valori effettivi. In questo caso, MAPE, MAE e RMSE sono definiti e restituiti nell&#39;oggetto `metrics`.

## Utilizzo di metriche e grafici di visualizzazione predefiniti

[!DNL Sensei Model Insights Framework] supporterà un modello predefinito per ogni tipo di algoritmo di apprendimento automatico. La tabella seguente mostra le classi di algoritmi comuni di apprendimento automatico di alto livello e le corrispondenti metriche e visualizzazioni di valutazione.

| Tipo di algoritmo ML | Metriche di valutazione | Visualizzazioni |
| --- | --- | --- |
| Regressione | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Valori previsti vs effettivi sovrapposizione curva |
| binario classificazione | - Matrice<br> di confusione- Precisione-richiamo<br>- Accuratezza- F-score<br> (in particolare F1, F2)<br>- AUC<br>- ROC | Curva ROC e matrice di confusione |
| Classificazione multiclasse | -Matrice di confusione <br>- Per ogni classe: <br>- precisione-richiamo precisione <br>- F-score (in particolare F1, F2) | Matrice di curva ROC e di confusione |
| Clustering (con verità di base) | - NMI (punteggio normalizzato per le informazioni reciproche), AMI (punteggio rettificato per le informazioni reciproche)<br>- RI (indice Rand), ARI (indice Rand rettificato)<br>- punteggio di omogeneità, punteggio di completezza e misura V<br>- FMI (indice Fowlkes-Mallows)<br>- purezza<br>- indice Jaccard | Grafico dei cluster che mostra cluster e centroidi con dimensioni relative dei cluster che riflettono i punti di dati che rientrano nel cluster |
| Clustering (senza verità di terra) | - Inerzia<br>- Coefficiente di siluetta<br>- CHI (indice Calinski-Harabaz)<br>- DBI (indice Davies-Bouldin)<br>- indice Dunn | Grafico dei cluster che mostra cluster e centroidi con dimensioni relative dei cluster che riflettono i punti di dati che rientrano nel cluster |
| Consiglio | -Precisione media (MAP) <br>-Guadagno cumulativo scontato normalizzato <br>-Classificazione reciproca media <br>-Metrica K | Da definire |
| Casi di utilizzo di TensorFlow | Analisi del modello TensorFlow (TFMA) | Confronto/visualizzazione del modello di rete neurale Deepcompare |
| Altro/meccanismo di acquisizione degli errori | Logica metrica personalizzata (e grafici di valutazione corrispondenti) definita dall&#39;autore del modello. Gestione agevole degli errori in caso di mancata corrispondenza del modello | Tabella con coppie chiave-valore per le metriche di valutazione |
