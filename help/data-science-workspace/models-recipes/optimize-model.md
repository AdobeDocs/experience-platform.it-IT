---
keywords: Experience Platform;ottimizzare;modello;Data Science Workspace;argomenti popolari;informazioni sul modello
solution: Experience Platform
title: Ottimizzare un modello utilizzando il Framework di informazioni sul modello
type: Tutorial
description: Il Framework di informazioni sul modello fornisce allo scienziato dei dati gli strumenti in Data Science Workspace per effettuare scelte rapide e informate per modelli di apprendimento automatico ottimali basati su esperimenti.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Ottimizzare un modello utilizzando il framework Model Insights

Il Framework di informazioni sul modello fornisce allo scienziato dati gli strumenti in [!DNL Data Science Workspace] fare scelte rapide e informate per modelli ottimali di apprendimento automatico basati su esperimenti. Il quadro migliorerà la velocità e l&#39;efficacia del flusso di lavoro di apprendimento automatico e migliorerà la facilità d&#39;uso per gli scienziati dei dati. Questo viene fatto fornendo un modello predefinito per ogni tipo di algoritmo di apprendimento automatico per assistere con la regolazione del modello. Il risultato finale consente agli scienziati dei dati e ai cittadini scienziati dei dati di prendere migliori decisioni di ottimizzazione dei modelli per i loro clienti finali.

## Cosa sono le metriche?

Dopo aver implementato e addestrato un modello, il passo successivo che uno scienziato farebbe è quello di trovare le prestazioni del modello. Varie metriche vengono utilizzate per determinare l’efficacia di un modello rispetto ad altre. Alcuni esempi di metriche utilizzate includono:
- Precisione della classificazione
- Area sotto curva
- Matrice di confusione
- Rapporto di classificazione

## Configurazione del codice di ricetta

Attualmente, il framework di Insights del modello supporta i seguenti runtime:
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

Il codice di esempio per le ricette è disponibile nella sezione [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) archivio sotto `recipes`. In questa esercitazione verrà fatto riferimento a file specifici provenienti da questo archivio.

### Scala {#scala}

Esistono due modi per inserire le metriche nelle ricette. Una consiste nell&#39;utilizzare le metriche di valutazione predefinite fornite dall&#39;SDK e l&#39;altra è quella di scrivere metriche di valutazione personalizzate.

#### Metriche di valutazione predefinite per Scala

Le valutazioni predefinite sono calcolate come parte degli algoritmi di classificazione. Di seguito sono riportati alcuni valori predefiniti per i valutatori attualmente implementati:

| Classe valutatore | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| ConsigliValutatore | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

Il valutatore può essere definito nella ricetta nel [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) nel `recipe` cartella. Codice di esempio che abilita `DefaultBinaryClassificationEvaluator` è mostrato di seguito:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Dopo che una classe di valutatore è abilitata, per impostazione predefinita verrà calcolato un certo numero di metriche durante la formazione. Le metriche predefinite possono essere dichiarate esplicitamente aggiungendo la seguente riga al `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Se la metrica non è definita, le metriche predefinite saranno attive.

Per abilitare una metrica specifica, modifica il valore di `evaluation.metrics.com`. Nell’esempio seguente, la metrica Punteggio F è abilitata.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

Nella tabella seguente sono riportate le metriche predefinite per ogni classe. Un utente può inoltre utilizzare i valori nel `evaluation.metric` per abilitare una metrica specifica.

| `evaluator.class` | Metriche predefinite | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precisione <br>-Richiama <br>- Matrice di confusione <br>Punteggio F <br>- Precisione <br>- Caratteristiche operative del ricevitore <br>- Area sotto le caratteristiche operative del ricevitore | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precisione <br>-Richiama <br>- Matrice di confusione <br>Punteggio F <br>- Precisione <br>- Caratteristiche operative del ricevitore <br>- Area sotto le caratteristiche operative del ricevitore | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Media precisione media media (MAP) <br>- Guadagno cumulativo attualizzato normalizzato <br>-Classificazione reciproca media <br>-Metrica K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Metriche di valutazione personalizzate per Scala

Il valutatore personalizzato può essere fornito estendendo l’interfaccia di `MLEvaluator.scala` nel tuo `Evaluator.scala` file. Nell’esempio [Valutatore.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) file, definiamo personalizzati `split()` e `evaluate()` funzioni. Nostro `split()` la funzione divide i nostri dati in modo casuale con un rapporto di 8:2 e `evaluate()` definisce e restituisce 3 metriche: MAPE, MAE e RMSE.

>[!IMPORTANT]
>
>Per `MLMetric` Classe, non utilizzare `"measures"` per `valueType` quando si crea una nuova `MLMetric` altrimenti la metrica non verrà compilata nella tabella delle metriche di valutazione personalizzate.
>  
> Esegui quanto segue: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Non questo: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Una volta definita nella ricetta, il passo successivo è quello di abilitarla nelle ricette. Questa operazione viene eseguita nel [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) nel `resources` cartella. Qui `evaluation.class` è impostato su `Evaluator` classe definita in `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

In [!DNL Data Science Workspace], l’utente potrebbe visualizzare le informazioni nella scheda &quot;Metriche di valutazione&quot; nella pagina dell’esperimento.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Al momento, non sono disponibili metriche di valutazione predefinite per [!DNL Python] o [!DNL Tensorflow]. Pertanto, per ottenere le metriche di valutazione per [!DNL Python] o [!DNL Tensorflow], dovrai creare una metrica di valutazione personalizzata. Questo può essere fatto implementando la `Evaluator` classe.

#### Metriche di valutazione personalizzate per [!DNL Python]

Per le metriche di valutazione personalizzate, è necessario implementare due metodi principali per il valutatore: `split()` e `evaluate()`.

Per [!DNL Python], questi metodi sono definiti in [valutator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) per `Evaluator` classe. Segui [valutator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) collegamento per un esempio di `Evaluator`.

Creazione di metriche di valutazione in [!DNL Python] richiede all&#39;utente di implementare `evaluate()` e `split()` metodi.

La `evaluate()` restituisce l&#39;oggetto metric che contiene un array di oggetti metrici con proprietà di `name`, `value`e `valueType`.

Lo scopo del `split()` il metodo è quello di inserire i dati e trasmettere un training e un set di dati di prova. Nel nostro esempio, il `split()` il metodo immette i dati utilizzando `DataSetReader` SDK e quindi pulisce i dati rimuovendo le colonne non collegate. Da lì vengono create funzionalità aggiuntive a partire dalle feature non elaborate esistenti nei dati.

La `split()` deve restituire un dataframe di formazione e test che viene poi utilizzato da `pipeline()` metodi per addestrare e testare il modello ML.

#### Metriche di valutazione personalizzate per Tensorflow

Per [!DNL Tensorflow], simile a [!DNL Python], i metodi `evaluate()` e `split()` in `Evaluator` la classe dovrà essere implementata. Per `evaluate()`, le metriche devono essere restituite mentre `split()` restituisce i set di dati del treno e delle prove.

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

A partire da ora, non ci sono metriche di valutazione predefinite per R. Pertanto, per ottenere le metriche di valutazione per R, sarà necessario definire la `applicationEvaluator` classe come parte della ricetta.

#### Metriche di valutazione personalizzate per R

Lo scopo principale del `applicationEvaluator` restituisce un oggetto JSON contenente coppie chiave-valore di metriche.

Questo [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) può essere utilizzato come esempio. In questo esempio, la `applicationEvaluator` è suddiviso in tre sezioni familiari:
- Caricare dati
- Preparazione dei dati/ingegneria delle funzioni
- Recupera modello salvato e valuta

I dati vengono caricati per la prima volta in un set di dati da un’origine come definita in [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). Da lì i dati vengono puliti e progettati per adattarsi al modello di apprendimento automatico. Infine, il modello viene utilizzato per fare una previsione utilizzando il nostro set di dati e dai valori previsti e dai valori effettivi, le metriche vengono calcolate. In questo caso, MAPE, MAE e RMSE vengono definiti e restituiti nel `metrics` oggetto.

## Utilizzo di metriche e grafici di visualizzazione predefiniti

La [!DNL Sensei Model Insights Framework] supporterà un modello predefinito per ogni tipo di algoritmo di apprendimento automatico. La tabella seguente mostra le classi comuni di algoritmi di apprendimento automatico di alto livello e le metriche di valutazione e le visualizzazioni corrispondenti.

| Tipo di algoritmo ML | Metriche di valutazione | Visualizzazioni |
| --- | --- | --- |
| Regressione | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Curva di sovrapposizione dei valori previsti e effettivi |
| Classificazione binaria | - Matrice di confusione<br>- Precisione<br>- Precisione<br>- Punteggio F (in particolare F1 ,F2)<br>- AUC<br>- ROC | Curva ROC e matrice della confusione |
| Classificazione multiclasse | - Matrice di confusione <br>- Per ogni classe: <br>- precisione del richiamo <br>- Punteggio F (nello specifico F1, F2) | Curva ROC e matrice della confusione |
| Clustering (con verità di fondo) | - NMI (punteggio di mutua informazione normalizzato), AMI (punteggio di mutua informazione corretto)<br>- RI (indice Rand), ARI (indice Rand corretto)<br>- punteggio di omogeneità, punteggio di completezza e misurazione V<br>- FMI (indice Fowlkes-Mallow)<br>- Purezza<br>- indice Jaccard | Grafico cluster che mostra cluster e centroid con dimensioni relative dei cluster che riflettono i punti dati che rientrano nel cluster |
| Clustering (senza verità) | - Inerzia<br>- Coefficiente di siluetta<br>- CHI (indice Calinski-Harabaz)<br>- DBI (indice Davies-Bouldin)<br>- Indice di Dunn | Grafico cluster che mostra cluster e centroid con dimensioni relative dei cluster che riflettono i punti dati che rientrano nel cluster |
| Consiglio | -Media precisione media media (MAP) <br>- Guadagno cumulativo attualizzato normalizzato <br>-Classificazione reciproca media <br>-Metrica K | Da definire |
| Casi d’uso di TensorFlow | Analisi del modello TensorFlow (TFMA) | Confronto profondo tra il modello di rete neurale e la visualizzazione |
| Meccanismo di acquisizione di altri/errori | Logica metrica personalizzata (e grafici di valutazione corrispondenti) definita dall’autore del modello. Gestione accurata degli errori in caso di mancata corrispondenza dei modelli | Tabella con coppie chiave-valore per le metriche di valutazione |
