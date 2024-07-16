---
keywords: Experience Platform;ottimizzare;modello;Data Science Workspace;argomenti popolari;informazioni sul modello
solution: Experience Platform
title: Ottimizzare un modello utilizzando il framework Model Insights
type: Tutorial
description: Il framework Model Insights fornisce allo scienziato dati strumenti in Data Science Workspace per effettuare scelte rapide e informate per modelli di apprendimento automatico ottimali basati sugli esperimenti.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 0%

---

# Ottimizzare un modello utilizzando il framework Model Insights

Il framework Model Insights fornisce al data scientist gli strumenti in [!DNL Data Science Workspace] per effettuare scelte rapide e informate per modelli di apprendimento automatico ottimali basati su esperimenti. Il quadro migliorerà la velocità e l&#39;efficacia del flusso di lavoro di apprendimento automatico nonché la facilità d&#39;uso per i data scientist. A tal fine, viene fornito un modello predefinito per ogni tipo di algoritmo di apprendimento automatico per facilitare l’ottimizzazione del modello. Il risultato finale consente ai data scientist e ai data scientist dei cittadini di prendere decisioni migliori in merito all’ottimizzazione dei modelli per i propri clienti finali.

## Cosa sono le metriche?

Dopo aver implementato e addestrato un modello, il passo successivo che un data scientist farebbe è trovare il livello di prestazioni del modello. Vengono utilizzate diverse metriche per determinare l’efficacia di un modello rispetto ad altri. Alcuni esempi di metriche utilizzate includono:
- Precisione della classificazione
- Area sotto la curva
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

È possibile abilitare una metrica specifica modificando il valore di `evaluation.metrics.com`. Nell’esempio seguente, la metrica F-Score è abilitata.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

Nella tabella seguente vengono indicate le metriche predefinite per ogni classe. Un utente può inoltre utilizzare i valori nella colonna `evaluation.metric` per abilitare una metrica specifica.

| `evaluator.class` | Metriche predefinite | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br>-Matrice di confusione <br>-F-Score <br>-Accuracy <br>-Caratteristiche operative del ricevitore <br>-Area sotto le caratteristiche operative del ricevitore | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Matrice di confusione <br>-F-Score <br>-Accuracy <br>-Caratteristiche operative del ricevitore <br>-Area sotto le caratteristiche operative del ricevitore | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Precisione media (MAP) <br>-Guadagno cumulativo scontato normalizzato <br>-Classificazione reciproca media <br>-Metrica K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Metriche di valutazione personalizzate per Scala

È possibile fornire un valutatore personalizzato estendendo l&#39;interfaccia di `MLEvaluator.scala` nel file `Evaluator.scala`. Nel file [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) di esempio vengono definite le funzioni personalizzate `split()` e `evaluate()`. La funzione `split()` suddivide i dati in modo casuale con un rapporto di 8:2 e la funzione `evaluate()` definisce e restituisce 3 metriche: MAPE, MAE e RMSE.

>[!IMPORTANT]
>
>Per la classe `MLMetric`, non utilizzare `"measures"` per `valueType` durante la creazione di un nuovo `MLMetric`. In caso contrario, la metrica non verrà popolata nella tabella delle metriche di valutazione personalizzata.
>  
> Esegui questa operazione: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Non questo: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Una volta definita nella ricetta, il passaggio successivo è quello di abilitarla nelle ricette. Operazione eseguita nel file [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) nella cartella `resources` del progetto. Qui `evaluation.class` è impostato sulla classe `Evaluator` definita in `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

In [!DNL Data Science Workspace], l&#39;utente potrebbe visualizzare le informazioni nella scheda &quot;Metriche di valutazione&quot; nella pagina dell&#39;esperimento.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Al momento non sono disponibili metriche di valutazione predefinite per [!DNL Python] o [!DNL Tensorflow]. Pertanto, per ottenere le metriche di valutazione per [!DNL Python] o [!DNL Tensorflow], è necessario creare una metrica di valutazione personalizzata. Questa operazione può essere eseguita implementando la classe `Evaluator`.

#### Metriche di valutazione personalizzate per [!DNL Python]

Per le metriche di valutazione personalizzate, è necessario implementare due metodi principali per il valutatore: `split()` e `evaluate()`.

Per [!DNL Python], questi metodi sono definiti in [valuator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) per la classe `Evaluator`. Segui il collegamento [valuator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) per un esempio di `Evaluator`.

La creazione delle metriche di valutazione in [!DNL Python] richiede l&#39;implementazione dei metodi `evaluate()` e `split()` da parte dell&#39;utente.

Il metodo `evaluate()` restituisce l&#39;oggetto metrica che contiene una matrice di oggetti metrici con proprietà di `name`, `value` e `valueType`.

Lo scopo del metodo `split()` è quello di immettere dati e generare un set di dati di formazione e di test. Nel nostro esempio, il metodo `split()` inserisce i dati utilizzando l&#39;SDK `DataSetReader`, quindi pulisce i dati rimuovendo colonne non correlate. A questo punto, vengono create feature aggiuntive a partire dalle feature raw esistenti nei dati.

Il metodo `split()` deve restituire un dataframe di addestramento e test che viene quindi utilizzato dai metodi `pipeline()` per addestrare e testare il modello ML.

#### Metriche di valutazione personalizzate per Tensorflow

Per [!DNL Tensorflow], simile a [!DNL Python], sarà necessario implementare i metodi `evaluate()` e `split()` nella classe `Evaluator`. Per `evaluate()`, le metriche devono essere restituite mentre `split()` restituisce il treno e i set di dati di prova.

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

Al momento non sono disponibili metriche di valutazione predefinite per R. Pertanto, per ottenere le metriche di valutazione per R, è necessario definire la classe `applicationEvaluator` come parte della ricetta.

#### Metriche di valutazione personalizzate per R

Lo scopo principale di `applicationEvaluator` è restituire un oggetto JSON contenente coppie chiave-valore di metriche.

Questo [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) può essere utilizzato come esempio. In questo esempio, `applicationEvaluator` è suddiviso in tre sezioni familiari:
- Carica dati
- Preparazione dei dati/progettazione delle funzioni
- Recupera il modello salvato e valuta

I dati vengono prima caricati in un set di dati da un&#39;origine come definito in [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). Da lì, i dati vengono puliti e progettati per adattarsi al modello di apprendimento automatico. Infine, il modello viene utilizzato per effettuare una previsione utilizzando il nostro set di dati; vengono calcolate le metriche in base ai valori previsti e ai valori effettivi. In questo caso, MAPE, MAE e RMSE sono definiti e restituiti nell&#39;oggetto `metrics`.

## Utilizzo di metriche e grafici di visualizzazione predefiniti

[!DNL Sensei Model Insights Framework] supporterà un modello predefinito per ogni tipo di algoritmo di apprendimento automatico. La tabella seguente mostra le classi di algoritmi comuni di apprendimento automatico di alto livello e le corrispondenti metriche e visualizzazioni di valutazione.

| Tipo di algoritmo ML | Metriche di valutazione | Visualizzazioni |
| --- | --- | --- |
| Regressione | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Curva di sovrapposizione dei valori previsti ed effettivi |
| Classificazione binaria | - Matrice di confusione<br>- Precisione-richiamo<br>- Precisione<br>- Punteggio F (in particolare F1 ,F2)<br>- AUC<br>- ROC | Matrice di curva ROC e di confusione |
| Classificazione di più classi | -Matrice di confusione <br>- Per ogni classe: <br>- precisione-richiamo precisione <br>- F-score (in particolare F1, F2) | Matrice di curva ROC e di confusione |
| Clustering (con verità di base) | - NMI (punteggio normalizzato per le informazioni reciproche), AMI (punteggio rettificato per le informazioni reciproche)<br>- RI (indice Rand), ARI (indice Rand rettificato)<br>- punteggio di omogeneità, punteggio di completezza e misura V<br>- FMI (indice Fowlkes-Mallows)<br>- purezza<br>- indice Jaccard | Grafico dei cluster che mostra cluster e centroidi con dimensioni relative dei cluster che riflettono i punti di dati che rientrano nel cluster |
| Clustering (senza verità di terra) | - Inerzia<br>- Coefficiente di siluetta<br>- CHI (indice Calinski-Harabaz)<br>- DBI (indice Davies-Bouldin)<br>- indice Dunn | Grafico dei cluster che mostra cluster e centroidi con dimensioni relative dei cluster che riflettono i punti di dati che rientrano nel cluster |
| Consiglio | -Precisione media (MAP) <br>-Guadagno cumulativo scontato normalizzato <br>-Classificazione reciproca media <br>-Metrica K | Da definire |
| Casi di utilizzo di TensorFlow | Analisi del modello TensorFlow (TFMA) | Confronto/visualizzazione del modello di rete neurale Deepcompare |
| Altro/meccanismo di acquisizione degli errori | Logica di metrica personalizzata (e grafici di valutazione corrispondenti) definita dall’autore del modello. Gestione corretta degli errori in caso di mancata corrispondenza del modello | Tabella con coppie chiave-valore per le metriche di valutazione |
