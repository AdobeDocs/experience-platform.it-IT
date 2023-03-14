---
title: Determinare Un Punteggio Di Propensione Utilizzando Un Modello Predittivo Generato Dall’Apprendimento Automatico
description: Scopri come utilizzare Query Service per applicare il modello predittivo ai dati di Platform. Questo documento illustra come utilizzare i dati di Platform per prevedere la propensione di un cliente all’acquisto per ogni visita.
exl-id: 29587541-50dd-405c-bc18-17947b8a5942
source-git-commit: 40c27a52fdae2c7d38c5e244a6d1d6ae3f80f496
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 0%

---

# Determinare un punteggio di tendenza utilizzando un modello predittivo generato dall’apprendimento automatico

Query Service consente di sfruttare modelli predittivi, come i punteggi di propensione, basati sulla piattaforma di apprendimento automatico per analizzare i dati di Experience Platform.

Questa guida spiega come utilizzare Query Service per inviare dati alla piattaforma di machine learning per addestrare un modello in un blocco appunti computazionale. Il modello addestrato può essere applicato ai dati utilizzando SQL per prevedere la propensione di un cliente ad acquistare per ogni visita.

## Introduzione

Poiché parte di questo processo richiede la formazione di un modello di apprendimento automatico, il presente documento presuppone una conoscenza operativa di uno o più ambienti di apprendimento automatico.

Questo esempio utilizza [!DNL Jupyter Notebook] come ambiente di sviluppo. Sebbene siano disponibili molte opzioni, [!DNL Jupyter Notebook] è consigliata in quanto si tratta di un&#39;applicazione web open-source con requisiti di calcolo ridotti. Può essere [scaricato dal sito ufficiale](https://jupyter.org/).

Se non lo hai già fatto, segui i passaggi per [connetti [!DNL Jupyter Notebook] con Adobe Experience Platform Query Service](../clients/jupyter-notebook.md) prima di continuare con questa guida.

Le librerie utilizzate in questo esempio includono:

```console
python=3.6.7
psycopg2
sklearn
pandas
matplotlib
numpy
tqdm
```

## Importare tabelle di analisi da Platform in [!DNL Jupyter Notebook] {#import-analytics-tables}

Per generare un modello di punteggio tendenza, è necessario importare in una proiezione dei dati di analisi memorizzati in Platform [!DNL Jupyter Notebook]. Da un [!DNL Python] 3 [!DNL Jupyter Notebook] connessi a Query Service, i seguenti comandi importano un set di dati sul comportamento del cliente da Luma, un negozio di abbigliamento fittizio. Poiché i dati di Platform vengono memorizzati utilizzando il formato Experience Data Model (XDM), è necessario generare un oggetto JSON di esempio conforme alla struttura dello schema. Consulta la documentazione per istruzioni su come [genera l’oggetto JSON campione](../../xdm/ui/sample.md).

![Il [!DNL Jupyter Notebook] dashboard con diversi comandi evidenziati.](../images/use-cases/jupyter-commands.png)

L’output mostra una vista in forma di tabella di tutte le colonne del set di dati comportamentali di Luma all’interno del [!DNL Jupyter Notebook] dashboard.

![L’output tabularizzato del set di dati del comportamento del cliente importato di Luma in [!DNL Jupyter Notebook].](../images/use-cases/behavioural-dataset-results.png)

## Prepara i dati per l’apprendimento automatico {#prepare-data-for-machine-learning}

Per addestrare un modello di apprendimento automatico è necessario identificare una colonna target. Poiché la propensione all’acquisto è l’obiettivo per questo caso d’uso, il `analytic_action` viene scelta come colonna di destinazione dai risultati Luma. Il valore `productPurchase` è l’indicatore di un acquisto di un cliente. Il `purchase_value` e `purchase_num` Le colonne vengono rimosse anche in quanto sono direttamente correlate all’azione di acquisto del prodotto.

I comandi per eseguire queste azioni sono i seguenti:

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

Successivamente, i dati del set di dati Luma devono essere trasformati in rappresentazioni appropriate. Sono necessari due passaggi:

1. Trasforma le colonne che rappresentano i numeri in colonne numeriche. Per eseguire questa operazione, convertire esplicitamente il tipo di dati in `dataframe`.
1. Trasforma anche le colonne categoriche in colonne numeriche.

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

Una tecnica denominata *una codifica a caldo* viene utilizzato per convertire le variabili di dati per categoria da utilizzare con algoritmi di apprendimento automatico e profondo. Ciò a sua volta migliora le previsioni e la precisione di classificazione di un modello. Utilizza il `Sklearn` per rappresentare ogni valore di categoria in una colonna separata.

```python
from sklearn.preprocessing import OneHotEncoder

#get the categorical columns
cat_columns = list(set(df.columns) - set(num_cols + ['target']))

#get the dataframe with categorical columns only
df_cat = df.loc[:,cat_columns]

#initialize sklearn's OneHotEncoder
enc = OneHotEncoder(handle_unknown='ignore')

#fit the data into the encoder
enc.fit(df_cat)

#define OneHotEncoder's columns names
ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
ohc_columns = [item for sublist in ohc_columns for item in sublist]

#finalize the data input to the ML models
X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                 columns =  ohc_columns + num_cols)

#define target column
y = df['target']
```

I dati definiti come `X` è tabulato e compare come segue:

![L’output tabularizzato di X in [!DNL Jupyter Notebook].](../images/use-cases/x-output-table.png)


Ora che i dati necessari per l’apprendimento automatico sono disponibili, può adattarsi ai modelli di apprendimento automatico preconfigurati in [!DNL Python]di `sklearn` libreria. [!DNL Logistics Regression] viene utilizzato per addestrare il modello di propensione e consente di visualizzare l’accuratezza dei dati di test. In questo caso, è di circa l&#39;85%.

Il [!DNL Logistic Regression] l’algoritmo e il metodo di suddivisione della prova del treno, utilizzati per stimare le prestazioni degli algoritmi di apprendimento automatico, sono importati nel blocco di codice seguente:

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

La precisione dei dati di prova è 0,8518518518518519.

Utilizzando la regressione logistica, puoi visualizzare i motivi di un acquisto e ordinare le funzioni che determinano la propensione in base alla loro importanza classificata in ordine decrescente. Le prime colonne denotano una causalità più elevata che determina il comportamento di acquisto. Queste ultime colonne indicano fattori che non determinano un comportamento di acquisto.

Il codice per visualizzare i risultati come due grafici a barre è il seguente:

```python
from matplotlib import pyplot as plt

#get feature importance as a sorted list of columns
feature_importance = np.argsort(-clf.coef_[0])
top_10_features_purchase_names = X.columns[feature_importance[:10]]
top_10_features_purchase_values = clf.coef_[0][feature_importance[:10]]
top_10_features_not_purchase_names = X.columns[feature_importance[-10:]]
top_10_features_not_purchase_values = clf.coef_[0][feature_importance[-10:]]

#plot the figures
fig, (ax1, ax2) = plt.subplots(1, 2,figsize=(10,5))

ax1.bar(np.arange(10),top_10_features_purchase_values)
ax1.set_xticks(np.arange(10))
ax1.set_xticklabels(top_10_features_purchase_names,rotation = 90)
ax1.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax1.set_title("Top 10 features to define \n a propensity to purchase")

ax2.bar(np.arange(10),top_10_features_not_purchase_values, color='#E15750')
ax2.set_xticks(np.arange(10))
ax2.set_xticklabels(top_10_features_not_purchase_names,rotation = 90)
ax2.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax2.set_title("Top 10 features to define \n a propensity to NOT purchase")

plt.show()
```

Di seguito è riportata una visualizzazione con grafico a barre verticale dei risultati:

![La visualizzazione delle 10 funzioni principali che definiscono la propensione all’acquisto o a non acquistare.](../images/use-cases/visualized-results.png)

Dal grafico a barre è possibile individuare diversi pattern. Gli argomenti POS (Point of Sale) e Call del canale come rimborso sono i fattori più importanti che determinano un comportamento di acquisto. Mentre gli argomenti della chiamata come reclami e fatture sono ruoli importanti per definire il comportamento di non acquisto. Si tratta di informazioni quantificabili e actionable che gli esperti di marketing possono sfruttare per condurre campagne di marketing volte a gestire la propensione all’acquisto di questi clienti.

## Utilizzare Query Service per applicare il modello addestrato {#use-query-service-to-apply-trained-model}

Dopo la creazione del modello addestrato, questo deve essere applicato ai dati contenuti in Experience Platform. A questo scopo, la logica della pipeline di machine learning deve essere convertita in SQL. I due componenti chiave di questa transizione sono i seguenti:

- Innanzitutto, SQL deve sostituire [!DNL Logistics Regression] modulo per ottenere la probabilità di un’etichetta di previsione. Il modello creato dalla regressione logistica ha prodotto il modello di regressione `y = wX + c`  dove pesi `w` e intercetta `c` sono l’output del modello. Le funzionalità SQL possono essere utilizzate per moltiplicare i pesi per ottenere una probabilità.

- In secondo luogo, il processo di progettazione [!DNL Python] con una codifica a caldo deve essere incorporata anche in SQL. Ad esempio, nel database originale sono presenti `geo_county` colonna in cui memorizzare la provincia ma in cui viene convertita la colonna `geo_county=Bexar`, `geo_county=Dallas`, `geo_county=DeKalb`. L&#39;istruzione SQL seguente esegue la stessa trasformazione, dove `w1`, `w2`, e `w3` possono essere sostituiti con i pesi appresi dal modello in [!DNL Python]:

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

Per le funzionalità numeriche, è possibile moltiplicare direttamente le colonne con i pesi, come illustrato nell&#39;istruzione SQL riportata di seguito.

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

Una volta ottenuti i numeri, possono essere portati a una funzione sigmoidea in cui l&#39;algoritmo di regressione logistica produce le previsioni finali. Nella dichiarazione seguente, `intercept` è il numero dell&#39;intercetta nella regressione.
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```
 
### Un esempio end-to-end

In una situazione in cui sono presenti due colonne (`c1` e `c2`), se `c1` dispone di due categorie, [!DNL Logistic Regression] l’algoritmo viene addestrato con la seguente funzione:
 

```python
y = 0.1 * "c1=category 1"+ 0.2 * "c1=category 2" +0.3 * c2+0.4
```
 
L&#39;equivalente in SQL è il seguente:

```sql
SELECT
  CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + FLOAT(0.4)))) > 0.5 THEN 1 ELSE 0 END AS Prediction
FROM
  (
    SELECT
      CASE WHEN c1 = 'Cateogry 1' THEN FLOAT(0.1) ELSE 0 END AS f1,
      CASE WHEN c1 = 'Cateogry 2' THEN FLOAT(0.2) ELSE 0 END AS f2,
      FLOAT(c2) * FLOAT(0.3) AS f3
    FROM TABLE
  )
```
 
Il [!DNL Python] il codice per automatizzare il processo di traduzione è il seguente:

```python
def generate_lr_inference_sql(ohc_columns, num_cols, clf, db):
    features_sql = []
    category_sql_text = "case when {col} = '{val}' then float({coef}) else 0 end as f{name}"
    numerical_sql_text = "float({col}) * float({coef}) as f{name}"
    for i, (column, coef) in enumerate(zip(ohc_columns+num_cols, clf.coef_[0])):
        if i < len(ohc_columns):
            col,val = column.split('=')
            val = val.replace("'","%''%")
            sql = category_sql_text.format(col=col,val=val,coef=coef,name=i+1)
        else:
            sql = numerical_sql_text.format(col=column,coef=coef,name=i+1)
        features_sql.append(sql)
    features_sum = '+'.join(['f{}'.format(i) for i in range(1,len(features_sql)+1)])
    final_sql = '''
    select case when 1/(1 + EXP(-({features} + float({intercept})))) > 0.5 then 1 else 0 end as Prediction
    from
        (select {cols}
        from {db})
    '''.format(features=features_sum,cols=",".join(features_sql),intercept=clf.intercept_[0],db=db)
    return final_sql
```

Quando SQL viene utilizzato per dedurre il database, l&#39;output è il seguente:

```python
sql = generate_lr_inference_sql(ohc_columns, num_cols, clf, "fdu_luma_raw")
cur.execute(sql)    
samples = [r for r in cur]
colnames = [desc[0] for desc in cur.description]
pd.DataFrame(samples,columns=colnames)
```

I risultati tabulari mostrano la propensione all’acquisto per ogni sessione del cliente con `0` che significa nessuna propensione ad acquistare e `1` il che significa una confermata propensione all&#39;acquisto.

![I risultati tabulari dell’inferenza del database utilizzando SQL.](../images/use-cases/inference-results.png)

## Lavori sui dati campionati: Bootstrapping {#working-on-sampled-data}

Nel caso in cui le dimensioni dei dati siano troppo grandi per consentire al computer locale di memorizzare i dati per l’apprendimento dei modelli, puoi prelevare campioni invece dei dati completi da Query Service. Per sapere quanti dati sono necessari per campionare da Query Service, puoi applicare una tecnica denominata bootstrapping. A questo proposito, l&#39;avvio comporta l&#39;addestramento del modello più volte con vari campioni e l&#39;ispezione della varianza delle accuratezze del modello tra i diversi campioni. Per regolare l’esempio del modello di propensione riportato sopra, in primo luogo, incapsula l’intero flusso di lavoro di apprendimento automatico in una funzione. Il codice è il seguente:

```python
def end_to_end_pipeline(df):
    
    #define the target label for prediction
    df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
    #remove columns that are dependent on the label
    df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
    
    num_cols = ['purchase_num','value_cart','value_lifetime']
    df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
    
    #get the categorical columns
    cat_columns = list(set(df.columns) - set(num_cols + ['target']))

    #get the dataframe with categorical columns only
    df_cat = df.loc[:,cat_columns]

    #initialize sklearn's One Hot Encoder
    enc = OneHotEncoder(handle_unknown='ignore')

    #fit the data into the encoder
    enc.fit(df_cat)

    #define one hot encoder's columns names
    ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
    ohc_columns = [item for sublist in ohc_columns for item in sublist]

    #finalize the data input to the ML models
    X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                     columns =  ohc_columns + num_cols)

    #define target column
    y = df['target']
    
    X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

    clf = LogisticRegression(max_iter=2000,random_state=0).fit(X_train, y_train)

    return clf.score(X_test, y_test)
```

Questa funzione può quindi essere eseguita più volte in un ciclo, ad esempio 10 volte. La differenza rispetto al codice precedente è che ora il campione non viene estratto dall&#39;intera tabella, ma solo da un campione di righe. Ad esempio, il codice di esempio seguente accetta solo 1000 righe. È possibile memorizzare le accuratezze di ogni iterazione.

```python
from tqdm import tqdm

bootstrap_accuracy = []
for i in tqdm(range(100)):
    
    #sample data from QS
    cur.execute('''SELECT *
    FROM fdu_luma_raw
    ORDER BY random()
    LIMIT 1000
    ''')    
    samples = [r for r in cur]
    colnames = [desc[0] for desc in cur.description]
    df_samples = pd.DataFrame(samples,columns=colnames)
    df_samples.fillna(0,inplace=True)
    
    #train the propensity model with sampled data and output its accuracy
    bootstrap_accuracy.append(end_to_end_pipeline(df_samples))
    
bootstrap_accuracy = np.sort(bootstrap_accuracy)
```

Le precisioni del modello avviato vengono quindi ordinate. Dopo di che, il decimo e il novantesimo quantile della precisione del modello diventano un intervallo di affidabilità del 95% per la precisione del modello con la dimensione del campione specificata.

![Il comando print per visualizzare l’intervallo di affidabilità del punteggio tendenza.](../images/use-cases/confidence-interval.png)

La figura precedente indica che se si utilizzano solo 1000 righe per addestrare i modelli, è possibile prevedere che la precisione diminuirà tra circa l’84% e l’88%. È possibile regolare `LIMIT` clausola nelle query di Query Service in base alle esigenze per garantire le prestazioni dei modelli.
