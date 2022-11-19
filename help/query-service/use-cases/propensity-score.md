---
title: Determinare Un Punteggio Di Propensione Utilizzando Un Modello Predittivo Generato Dall’Apprendimento Automatico
description: Scopri come utilizzare Query Service per applicare il modello predittivo ai dati di Platform. Questo documento illustra come utilizzare i dati di Platform per prevedere la propensione di un cliente all’acquisto in ogni visita.
source-git-commit: af1c8f94d1758b3a4e7ea00c46b0f9a71a01c6be
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# Determinare un punteggio di propensione utilizzando un modello predittivo generato da machine-learning

Utilizzando Query Service, puoi sfruttare i dati di Experience Platform nelle piattaforme di apprendimento automatico per generare modelli predittivi come i punteggi di propensione. Questa guida spiega come utilizzare Query Service per inviare dati alla piattaforma di apprendimento automatico al fine di addestrare un modello in un blocco appunti computazionale. Il modello addestrato può essere applicato ai dati utilizzando SQL per prevedere la propensione di un cliente all&#39;acquisto per ogni visita.

## Introduzione

Come parte di questo processo richiede la formazione di un modello di apprendimento automatico, in questo documento si presuppone una conoscenza operativa di uno o più ambienti di apprendimento automatico.

Questo esempio utilizza [!DNL Jupyter Notebook] come ambiente di sviluppo. Sebbene siano disponibili molte opzioni, [!DNL Jupyter Notebook] è consigliato perché si tratta di un&#39;applicazione web open-source con requisiti di elaborazione ridotti. Può essere [scaricato dal sito ufficiale](https://jupyter.org/).

Se non lo hai già fatto, segui i passaggi per [connect [!DNL Jupyter Notebook] con Adobe Experience Platform Query Service](../clients/jupyter-notebook.md) prima di continuare con questa guida.

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

Per generare un modello di punteggio tendenza, è necessario importare una proiezione dei dati di analisi memorizzati in Platform in [!DNL Jupyter Notebook]. Da un [!DNL Python] 3 [!DNL Jupyter Notebook] collegato a Query Service, i seguenti comandi importano un set di dati sul comportamento del cliente da Luma, un negozio di abbigliamento fittizio. Poiché i dati di Platform vengono memorizzati utilizzando il formato Experience Data Model (XDM), è necessario generare un oggetto JSON di esempio conforme alla struttura dello schema. Consulta la documentazione per le istruzioni su come [generare l’oggetto JSON di esempio](../../xdm/ui/sample.md).

![La [!DNL Jupyter Notebook] dashboard con diversi comandi evidenziati.](../images/use-cases/jupyter-commands.png)

L’output visualizza una visualizzazione tabularizzata di tutte le colonne del set di dati comportamentali di Luma all’interno del [!DNL Jupyter Notebook] dashboard.

![Output tabularizzato del set di dati sul comportamento dei clienti importato da Luma all’interno di [!DNL Jupyter Notebook].](../images/use-cases/behavioural-dataset-results.png)

## Preparare i dati per l’apprendimento automatico {#prepare-data-for-machine-learning}

Per formare un modello di apprendimento automatico è necessario identificare una colonna bersaglio. Poiché la propensione all’acquisto è l’obiettivo per questo caso d’uso, la `analytic_action` come colonna di destinazione dai risultati Luma. Il valore `productPurchase` è l&#39;indicatore di un acquisto da parte del cliente. La `purchase_value` e `purchase_num` vengono rimosse anche in quanto sono direttamente correlate all’azione di acquisto del prodotto.

I comandi per eseguire queste azioni sono i seguenti:

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

Successivamente, i dati del set di dati Luma devono essere trasformati in rappresentazioni appropriate. Sono necessari due passaggi:

1. Trasforma le colonne che rappresentano i numeri in colonne numeriche. A tal fine, convertire esplicitamente il tipo di dati nel `dataframe`.
1. Trasforma anche le colonne categoriche in colonne numeriche.

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

Una tecnica denominata *una codifica a caldo* viene utilizzato per convertire le variabili di dati categoriche da utilizzare con gli algoritmi di machine e deep learning. Ciò a sua volta migliora le previsioni e la precisione di classificazione di un modello. Utilizza la `Sklearn` per rappresentare ogni valore categorico in una colonna separata.

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

I dati definiti come `X` è tabularizzato e compare come segue:

![Uscita tabularizzata di X [!DNL Jupyter Notebook].](../images/use-cases/x-output-table.png)


Ora che i dati necessari per l&#39;apprendimento automatico sono disponibili, può adattarsi ai modelli di apprendimento automatico preconfigurati in [!DNL Python]s `sklearn` libreria. [!DNL Logistics Regression] viene utilizzato per addestrare il modello di propensione e consente di vedere la precisione dei dati del test. In questo caso, l’85% circa.

La [!DNL Logistic Regression] l&#39;algoritmo e il metodo di suddivisione del test del treno, utilizzato per stimare le prestazioni degli algoritmi di apprendimento automatico, vengono importati nel blocco di codice seguente:

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

La precisione dei dati di prova è 0,8518518518518519.

Utilizzando la Regressione Logistica, puoi visualizzare le ragioni di un acquisto e ordinare le caratteristiche che determinano la propensione in base alla loro importanza classificata negli ordini discendenti. Le prime colonne indicano una causa maggiore che porta al comportamento di acquisto. Le ultime colonne indicano i fattori che non portano al comportamento di acquisto.

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

Di seguito è riportata una visualizzazione grafico a barre verticale dei risultati:

![La visualizzazione delle 10 caratteristiche principali che definiscono una propensione ad acquistare o a non comprare.](../images/use-cases/visualized-results.png)

È possibile distinguere diversi pattern dal grafico a barre. Gli argomenti relativi ai punti vendita (POS) e alle chiamate come rimborso sono i fattori più importanti che determinano il comportamento di acquisto. Mentre gli argomenti della chiamata come reclami e fatture sono ruoli importanti per definire il comportamento di non acquisto. Si tratta di informazioni quantificabili e fruibili che gli addetti al marketing possono sfruttare per condurre campagne di marketing per affrontare la propensione all’acquisto di questi clienti.

## Utilizzare Query Service per applicare il modello addestrato {#use-query-service-to-apply-trained-model}

Una volta creato, il modello addestrato deve essere applicato ai dati contenuti nell&#39;Experience Platform. A questo scopo, la logica della pipeline di apprendimento automatico deve essere convertita in SQL. I due elementi chiave di questa transizione sono i seguenti:

- In primo luogo, SQL deve sostituire [!DNL Logistics Regression] modulo per ottenere la probabilità di un&#39;etichetta di previsione. Il modello creato da Regressione logistica ha prodotto il modello di regressione `y = wX + c`  dove pesi `w` e intercettare `c` sono l&#39;output del modello. Le funzionalità SQL possono essere utilizzate per moltiplicare i pesi per ottenere una probabilità.

- In secondo luogo, il processo di ingegneria realizzato [!DNL Python] con una codifica a caldo deve essere incorporato anche in SQL. Per esempio, nel database originale, abbiamo `geo_county` per memorizzare la contea, ma la colonna viene convertita in `geo_county=Bexar`, `geo_county=Dallas`, `geo_county=DeKalb`. L&#39;istruzione SQL seguente esegue la stessa trasformazione, dove `w1`, `w2`e `w3` possono essere sostituiti con i pesi tratti dal modello in [!DNL Python]:

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

Per le funzioni numeriche, è possibile moltiplicare direttamente le colonne con i pesi, come illustrato nell&#39;istruzione SQL riportata di seguito.

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

Una volta ottenuti i numeri, è possibile portarli a una funzione sigmoide in cui l&#39;algoritmo di regressione logistica produce le previsioni finali. Nell&#39;istruzione seguente, `intercept` è il numero dell&#39;intersezione nella regressione.
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```
 
### Un esempio end-to-end

In una situazione in cui sono presenti due colonne (`c1` e `c2`), se `c1` ha due categorie, [!DNL Logistic Regression] viene addestrato con la seguente funzione:
 

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
 
La [!DNL Python] codice per automatizzare il processo di traduzione:

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

Quando si utilizza SQL per dedurre il database, l&#39;output è il seguente:

```python
sql = generate_lr_inference_sql(ohc_columns, num_cols, clf, "fdu_luma_raw")
cur.execute(sql)    
samples = [r for r in cur]
colnames = [desc[0] for desc in cur.description]
pd.DataFrame(samples,columns=colnames)
```

I risultati tabularizzati mostrano la propensione ad acquistare per ogni sessione del cliente con `0` che significa nessuna propensione all&#39;acquisto e `1` che significa una propensione confermata all&#39;acquisto.

![Risultati tabularizzati dell&#39;inferenza del database utilizzando SQL.](../images/use-cases/inference-results.png)

## Lavorare sui dati campionati: Bootstrap {#working-on-sampled-data}

Nel caso in cui le dimensioni dei dati siano troppo grandi per consentire al computer locale di memorizzare i dati per la formazione sul modello, è possibile prelevare campioni invece dei dati completi da Query Service. Per sapere quanti dati sono necessari per il campionamento da Query Service, puoi applicare una tecnica chiamata bootstrapping. A questo proposito, per &quot;bootstrapping&quot; si intende che il modello viene addestrato più volte con diversi campioni e viene esaminata la varianza delle precisioni del modello tra i diversi campioni. Per regolare l&#39;esempio di modello di propensione riportato sopra, prima di tutto, incapsulare l&#39;intero flusso di lavoro di apprendimento automatico in una funzione. Il codice è il seguente:

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

Questa funzione può quindi essere eseguita più volte in un ciclo, ad esempio 10 volte. La differenza rispetto al codice precedente è che il campione ora non viene prelevato dall’intera tabella, ma solo da un campione di righe. Ad esempio, il codice di esempio sottostante richiede solo 1000 righe. È possibile memorizzare le precisioni di ogni iterazione.

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

Vengono quindi ordinate le precisioni del modello di bootstrapped. Dopo di che, il decimo e il novantesimo quantile della precisione del modello diventa un intervallo di affidabilità del 95% per le precisioni del modello con la dimensione del campione specificata.

![Comando di stampa per visualizzare l&#39;intervallo di affidabilità del punteggio di propensione.](../images/use-cases/confidence-interval.png)

La figura precedente indica che se si impiegano solo 1000 righe per addestrare i modelli, è possibile prevedere che le precisioni scendano tra l’84% e l’88% circa. È possibile regolare le `LIMIT` nelle query Query Service in base alle tue esigenze per garantire le prestazioni dei modelli.


