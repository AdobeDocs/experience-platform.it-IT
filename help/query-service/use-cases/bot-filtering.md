---
title: Filtraggio dei bot in Query Service con Machine Learning
description: Questo documento fornisce una panoramica sull’utilizzo di Query Service e machine learning per determinare l’attività di bot e filtrare le azioni da un traffico autentico di visitatori di siti web online.
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 5%

---

# Filtro bot in [!DNL Query Service] con apprendimento automatico

L’attività dei bot può influire sulle metriche di analisi e danneggiare l’integrità dei dati. Adobe Experience Platform [!DNL Query Service] può essere utilizzato per mantenere la qualità dei dati attraverso il processo di filtro dei bot.

Il filtro bot consente di mantenere la qualità dei dati rimuovendo in generale la contaminazione dei dati derivante dall’interazione non umana con il sito web. Questo processo viene ottenuto tramite la combinazione di query SQL e machine learning.

L’attività bot può essere identificata in diversi modi. L’approccio adottato in questo documento si concentra sui picchi di attività, in questo caso il numero di azioni intraprese da un utente in un determinato periodo di tempo. Inizialmente, una query SQL imposta in modo arbitrario una soglia per il numero di azioni eseguite in un periodo di tempo per qualificarsi come attività bot. Questa soglia viene quindi perfezionata dinamicamente utilizzando un modello di apprendimento automatico per migliorare l’accuratezza di questi rapporti.

Questo documento fornisce una panoramica e alcuni esempi dettagliati delle query di filtro bot SQL e dei modelli di apprendimento automatico necessari per configurare il processo nell’ambiente.

## Introduzione

Poiché parte di questo processo richiede la formazione di un modello di apprendimento automatico, il presente documento presuppone una conoscenza operativa di uno o più ambienti di apprendimento automatico.

In questo esempio viene utilizzato [!DNL Jupyter Notebook] come ambiente di sviluppo. Sebbene siano disponibili molte opzioni, [!DNL Jupyter Notebook] è consigliato in quanto si tratta di un&#39;applicazione Web open-source con requisiti di calcolo ridotti. Può essere [scaricato dal sito ufficiale](https://jupyter.org/).

## Usa [!DNL Query Service] per definire una soglia per l&#39;attività bot

I due attributi utilizzati per estrarre i dati per il rilevamento di bot sono:

* ID visitatore Experience Cloud (ECID, noto anche come MCID): fornisce un ID universale e costante che identifica i visitatori in tutte le soluzioni Adobi.
* Timestamp: fornisce l’ora e la data in formato UTC in cui si è verificata un’attività sul sito web.

>[!NOTE]
>
>L&#39;utilizzo di `mcid` è ancora presente nei riferimenti spazio dei nomi all&#39;ID visitatore Experience Cloud, come illustrato nell&#39;esempio seguente.

L’istruzione SQL seguente fornisce un esempio iniziale per identificare l’attività bot. L’istruzione presuppone che, se un visitatore esegue 50 clic in un minuto, l’utente sia un bot.

```sql
SELECT * 
FROM   <YOUR_TABLE_NAME> 
WHERE  enduserids._experience.mcid NOT IN (SELECT enduserids._experience.mcid 
                                           FROM   <YOUR_TABLE_NAME> 
                                           GROUP  BY Unix_timestamp(timestamp) / 
                                                     60, 
                                                     enduserids._experience.mcid 
                                           HAVING Count(*) > 50);  
```

L&#39;espressione filtra gli ECID (`mcid`) di tutti i visitatori che soddisfano la soglia ma non risolve i picchi di traffico da altri intervalli.

## Migliorare il rilevamento di bot con l’apprendimento automatico

L’istruzione SQL iniziale può essere perfezionata per diventare una query di estrazione di funzionalità per l’apprendimento automatico. La query migliorata dovrebbe produrre più funzioni per una varietà di intervalli per l’apprendimento automatico di modelli con precisione elevata.

L’istruzione di esempio viene espansa da un minuto con un massimo di 60 clic, per includere periodi di cinque minuti e 30 minuti con un numero di clic rispettivamente di 300 e 1800.

L&#39;istruzione di esempio raccoglie il numero massimo di clic per ogni ECID (`mcid`) nelle varie durate. L’istruzione iniziale è stata estesa per includere periodi di un minuto (60 secondi), 5 minuti (300 secondi) e un’ora (1800 secondi).

```sql
SELECT table_count_1_min.mcid AS id, 
       count_1_min, 
       count_5_mins, 
       count_30_mins 
FROM   ( ( (SELECT mcid, 
                 Max(count_1_min) AS count_1_min 
          FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                         Count(*)                       AS count_1_min 
                  FROM 
       <YOUR_TABLE_NAME> 
                  GROUP  BY Unix_timestamp(timestamp) / 60, 
                            enduserids._experience.mcid.id) 
          GROUP BY mcid) AS table_count_1_min 
           LEFT JOIN (SELECT mcid, 
                             Max(count_5_mins) AS count_5_mins 
                      FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                     Count(*)                       AS 
                                     count_5_mins 
                              FROM 
           <YOUR_TABLE_NAME> 
                              GROUP  BY Unix_timestamp(timestamp) / 300, 
                                        enduserids._experience.mcid.id) 
                      GROUP  BY mcid) AS table_count_5_mins 
                  ON table_count_1_min.mcid = table_count_5_mins.mcid ) 
         LEFT JOIN (SELECT mcid, 
                           Max(count_30_mins) AS count_30_mins 
                    FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                   Count(*)                       AS 
                                   count_30_mins 
                            FROM 
         <YOUR_TABLE_NAME> 
                            GROUP  BY Unix_timestamp(timestamp) / 1800, 
                                      enduserids._experience.mcid.id) 
                    GROUP  BY mcid) AS table_count_30_mins 
                ON table_count_1_min.mcid = table_count_30_mins.mcid ) 
```

Il risultato di questa espressione potrebbe essere simile alla tabella fornita di seguito.

| `id` | `count_1_min` | `count_5_min` | `count_30_min` |
|---|---|---|---|
| 4833075303848917832 | 1 | 1 | 1 |
| 1469109497068938520 | 1 | 1 | 1 |
| 5045682519445554093 | 1 | 1 | 1 |
| 7148203816406620066 | 3 | 3 | 3 |
| 1013065429311352386 | 1 | 1 | 1 |
| 3077475871984695013 | 7 | 7 | 7 |
| 4151486040344674930 | 2 | 2 | 2 |
| 6563366098591762751 | 6 | 6 | 6 |
| 2403566105776993627 | 4 | 4 | 4 |
| 5710530640819698543 | 1 | 1 | 1 |
| 3675089655839425960 | 1 | 1 | 1 |
| 9091930660723241307 | 1 | 1 | 1 |

## Identificare nuove soglie di picco utilizzando l’apprendimento automatico

Esportare quindi il set di dati di query risultante in formato CSV e importarlo in [!DNL Jupyter Notebook]. Da tale ambiente, puoi addestrare un modello di apprendimento automatico utilizzando le librerie di apprendimento automatico correnti. Consulta la guida alla risoluzione dei problemi per ulteriori dettagli su [come esportare dati da [!DNL Query Service] in formato CSV](../troubleshooting-guide.md#export-csv)

Le soglie di picco ad hoc inizialmente stabilite non sono basate sui dati e quindi mancano di precisione. I modelli di apprendimento automatico possono essere utilizzati per addestrare parametri come soglie. Di conseguenza, è possibile aumentare l&#39;efficienza delle query riducendo il numero di `GROUP BY` parole chiave rimuovendo le funzionalità non necessarie.

In questo esempio viene utilizzata la libreria di apprendimento automatico Scikit-Learn installata per impostazione predefinita con [!DNL Jupyter Notebook]. Viene importata anche la libreria di pandas per utilizzarla qui. I seguenti comandi sono immessi in [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

Successivamente, devi addestrare un classificatore della struttura decisionale sul set di dati e osservare la logica risultante dal modello.

La libreria &quot;Matplotlib&quot; viene utilizzata per visualizzare il classificatore dell’albero decisionale nell’esempio seguente.

```shell
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree
from matplotlib import pyplot as plt

X = df.iloc[:,:[1,3]]
y = df.iloc[:,-1]

clf = DecisionTreeClassifier(max_leaf_nodes=2, random_state=0)
clf.fit(X,y)

print("Model Accuracy: {:.5f}".format(clf.scre(X,y)))

tree.plot_tree(clf,feature_names=X.columns)
plt.show()
```

I valori restituiti da [!DNL Jupyter Notebook] per questo esempio sono i seguenti.

```text
Model Accuracy: 0.99935
```

![Output statistico da [!DNL Jupyter Notebook] modello di apprendimento automatico.](../images/use-cases/jupiter-notebook-output.png)

I risultati per il modello mostrato nell&#39;esempio precedente sono accurati oltre il 99%.

Poiché il classificatore dell&#39;albero decisionale può essere addestrato utilizzando i dati di [!DNL Query Service] su una cadenza regolare utilizzando query pianificate, è possibile garantire l&#39;integrità dei dati filtrando le attività bot con un elevato grado di precisione. Utilizzando i parametri derivati dal modello di apprendimento automatico, le query originali possono essere aggiornate con i parametri altamente precisi creati dal modello.

Il modello di esempio ha determinato con un elevato grado di precisione che qualsiasi visitatore con più di 130 interazioni in cinque minuti è un bot. Queste informazioni possono ora essere utilizzate per perfezionare il filtro bot per le query SQL.

## Passaggi successivi

La lettura di questo documento consente di comprendere meglio come utilizzare [!DNL Query Service] e l&#39;apprendimento automatico per determinare e filtrare le attività bot.

Altri documenti che dimostrano i vantaggi di [!DNL Query Service] per le informazioni aziendali strategiche della tua organizzazione sono l&#39;esempio di [caso d&#39;uso abbandonato](./abandoned-browse.md).
