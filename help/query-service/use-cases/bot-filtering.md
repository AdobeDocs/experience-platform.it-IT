---
title: Filtro bot in Query Service con apprendimento automatico
description: Questo documento fornisce una panoramica sull’utilizzo di Query Service e machine learning per determinare l’attività di bot e filtrare le loro azioni in base al traffico dei visitatori del sito web online.
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 5%

---

# Filtro bot in [!DNL Query Service] con apprendimento automatico

L’attività dei bot può influire sulle metriche di analisi e compromettere l’integrità dei dati. Adobe Experience Platform [!DNL Query Service] può essere utilizzato per mantenere la qualità dei dati attraverso il processo di filtraggio dei bot.

Il filtraggio dei bot ti consente di mantenere la qualità dei dati rimuovendo in modo ampio la contaminazione dei dati risultante dall’interazione non umana con il tuo sito web. Questo processo si ottiene attraverso la combinazione di query SQL e apprendimento automatico.

L’attività bot può essere identificata in diversi modi. L’approccio adottato in questo documento si concentra sui picchi di attività, in questo caso, il numero di azioni intraprese da un utente in un dato periodo di tempo. Inizialmente, una query SQL imposta arbitrariamente una soglia per il numero di azioni intraprese in un periodo di tempo per qualificarsi come attività bot. Questa soglia viene quindi perfezionata dinamicamente utilizzando un modello di apprendimento automatico per migliorare la precisione di questi rapporti.

Questo documento fornisce una panoramica e esempi dettagliati delle query di filtro bot SQL e dei modelli di apprendimento automatico necessari per impostare il processo nell&#39;ambiente.

## Introduzione

Come parte di questo processo richiede la formazione di un modello di apprendimento automatico, in questo documento si presuppone una conoscenza operativa di uno o più ambienti di apprendimento automatico.

Questo esempio utilizza [!DNL Jupyter Notebook] come ambiente di sviluppo. Sebbene siano disponibili molte opzioni, [!DNL Jupyter Notebook] è consigliato perché si tratta di un&#39;applicazione web open-source con requisiti di elaborazione ridotti. Può essere [scaricato dal sito ufficiale](https://jupyter.org/).

## Utilizzo [!DNL Query Service] per definire una soglia per l’attività bot

I due attributi utilizzati per estrarre i dati per il rilevamento di bot sono:

* ID visitatore di Experience Cloud (ECID, noto anche come MCID): Questo fornisce un ID universale e costante che identifica i visitatori in tutte le soluzioni Adobe.
* Timestamp: Questo fornisce l’ora e la data in formato UTC quando si è verificata un’attività sul sito web.

>[!NOTE]
>
>L&#39;uso di `mcid` si trova ancora nei riferimenti dello spazio dei nomi all’ID visitatore Experience Cloud come mostrato nell’esempio seguente.

L&#39;istruzione SQL seguente fornisce un esempio iniziale per identificare l&#39;attività bot. L&#39;istruzione presuppone che se un visitatore esegue 50 clic in un minuto, l&#39;utente è un bot.

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

L&#39;espressione filtra gli ECID (`mcid`) di tutti i visitatori che soddisfano la soglia ma non soddisfano i picchi di traffico di altri intervalli.

## Migliorare il rilevamento dei bot con l&#39;apprendimento automatico

L&#39;istruzione SQL iniziale può essere perfezionata per diventare una query di estrazione di funzionalità per l&#39;apprendimento automatico. La query migliorata dovrebbe produrre più funzionalità per una varietà di intervalli per i modelli di apprendimento automatico di formazione con alte precisione.

L’istruzione di esempio viene espansa da un minuto con fino a 60 clic, per includere periodi di cinque minuti e 30 minuti con conteggi di clic rispettivamente di 300 e 1800.

L&#39;istruzione example raccoglie il numero massimo di clic per ogni ECID (`mcid`) nelle varie durate. L’istruzione iniziale è stata espansa per includere periodi di un minuto (60 secondi), di 5 minuti (300 secondi) e di un’ora (cioè 1800 secondi).

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

Quindi, esporta il set di dati di query risultante in formato CSV e quindi importalo in [!DNL Jupyter Notebook]. Da quell&#39;ambiente, è possibile addestrare un modello di apprendimento automatico utilizzando le librerie di apprendimento automatico correnti. Per ulteriori informazioni, consulta la guida alla risoluzione dei problemi . [come esportare i dati da [!DNL Query Service] in formato CSV](../troubleshooting-guide.md#export-csv)

Le soglie di picco ad hoc inizialmente stabilite non sono basate sui dati e pertanto non sono precise. I modelli di apprendimento automatico possono essere utilizzati per addestrare i parametri come soglie. Di conseguenza, è possibile aumentare l’efficienza della query riducendo il numero di `GROUP BY` parole chiave rimuovendo le funzionalità non necessarie.

In questo esempio viene utilizzata la libreria di apprendimento automatico Scikit-Learning, installata per impostazione predefinita con [!DNL Jupyter Notebook]. La libreria pitone &quot;pandas&quot; viene importata anche per l&#39;uso qui. Vengono immessi i seguenti comandi [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

Successivamente, devi addestrare un classificatore della struttura decisionale nel set di dati e osservare la logica risultante dal modello.

La libreria &quot;Matplotlib&quot; viene utilizzata per visualizzare il classificatore della struttura decisionale nell’esempio seguente.

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

I valori restituiti da [!DNL Jupyter Notebook] per questo esempio:

```text
Model Accuracy: 0.99935
```

![Uscita statistica da [!DNL Jupyter Notebook] modello di apprendimento automatico.](../images/use-cases/jupiter-notebook-output.png)

I risultati per il modello mostrato nell&#39;esempio precedente sono accurati oltre il 99%.

Poiché il classificatore della struttura decisionale può essere addestrato utilizzando i dati di [!DNL Query Service] in caso di cadenza regolare utilizzando query pianificate, puoi garantire l’integrità dei dati filtrando l’attività bot con un elevato grado di precisione. Utilizzando i parametri derivati dal modello di apprendimento automatico, le query originali possono essere aggiornate con i parametri altamente precisi creati dal modello.

Il modello di esempio è stato determinato con un alto grado di precisione in base al quale tutti i visitatori con più di 130 interazioni in cinque minuti sono bot. Queste informazioni possono ora essere utilizzate per perfezionare le query SQL con filtro bot.

## Passaggi successivi

Leggendo questo documento, si ha una migliore comprensione di come utilizzare [!DNL Query Service] e l&#39;apprendimento automatico per determinare e filtrare l&#39;attività bot.

Altri documenti che dimostrano i vantaggi di [!DNL Query Service] le informazioni strategiche aziendali della tua organizzazione sono [caso d&#39;uso del browser abbandonato](./abandoned-browse.md) esempio.
