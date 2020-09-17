---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: Procedura dettagliata di Data Science Workspace
topic: Walkthrough
description: Questo documento fornisce una panoramica per Adobe Experience Platform Data Science Workspace. In particolare, il flusso di lavoro generale che un esperto di dati dovrebbe affrontare per risolvere un problema utilizzando l'apprendimento automatico.
translation-type: tm+mt
source-git-commit: 0d76b14599bc6b6089f9c760ef6a6be3a19243d4
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 0%

---


# [!DNL Data Science Workspace] guida

Questo documento fornisce una guida dettagliata per Adobe Experience Platform [!DNL Data Science Workspace]. Questa esercitazione illustra un flusso di lavoro generale di data scienziist e come potrebbero affrontare e risolvere un problema utilizzando l&#39;apprendimento automatico.

## Prerequisiti

- Un account Adobe ID  registrato
   - L&#39;account Adobe ID  deve essere stato aggiunto a un&#39;organizzazione con accesso ad Adobe Experience Platform e [!DNL Data Science Workspace].

## Caso di utilizzo al dettaglio

Un rivenditore deve affrontare molte sfide per rimanere competitivo nel mercato attuale. Una delle principali preoccupazioni del rivenditore è quella di decidere il prezzo ottimale di un prodotto e di prevedere le tendenze di vendita. Con un modello di previsione accurato, un rivenditore potrebbe trovare la relazione tra le politiche di domanda e di prezzo e prendere decisioni di prezzo ottimizzate per massimizzare le vendite e i ricavi.

## La soluzione del Data Scienziato

La soluzione di uno scienziato informatico è quella di sfruttare la ricchezza di informazioni storiche fornite da un rivenditore, di prevedere le tendenze future e di ottimizzare le decisioni di prezzo. Questa procedura dettagliata utilizza i dati di vendita passati per formare un modello di machine learning e utilizza il modello per prevedere le tendenze di vendita future. Con questo, puoi generare informazioni utili per apportare modifiche ottimali ai prezzi.

Questa panoramica rispecchia i passi che un esperto di dati dovrebbe compiere per prendere un set di dati e creare un modello per prevedere le vendite settimanali. Questa esercitazione illustra le sezioni seguenti del Sample Retail Sales Notebook di Adobe Experience Platform [!DNL Data Science Workspace]:

- [Configurazione](#setup)
- [Esplorazione dei dati](#exploring-data)
- [Progettazione delle funzioni](#feature-engineering)
- [Formazione e verifica](#training-and-verification)

### Blocco note in [!DNL Data Science Workspace]

Nell’interfaccia utente di Adobe Experience Platform, selezionate **[!UICONTROL Notebooks]** dalla **[!UICONTROL Data Science]** scheda per passare alla pagina della [!UICONTROL Notebooks] panoramica. Da questa pagina, selezionate la [!DNL JupyterLab] scheda per avviare l&#39; [!DNL JupyterLab] ambiente. La pagina di destinazione predefinita per [!DNL JupyterLab] è la **[!UICONTROL Launcher]**.

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

Questa esercitazione utilizza [!DNL Python] 3 in [!DNL JupyterLab Notebooks] per mostrare come accedere ed esplorare i dati. Nella pagina Launcher sono disponibili alcuni blocchi appunti di esempio. Il blocco appunti **[!UICONTROL Retail Sales]** di esempio è utilizzato negli esempi riportati di seguito.

### Configurazione {#setup}

Con il blocco appunti Vendite al dettaglio aperto, la prima cosa da fare è caricare le librerie necessarie per il flusso di lavoro. L&#39;elenco seguente fornisce una breve descrizione per ciascuna libreria utilizzata negli esempi nei passaggi successivi.

- **numpy**: Libreria di informatica scientifica che aggiunge il supporto per array e matrici multidimensionali di grandi dimensioni
- **panda**: Libreria che offre strutture e operazioni di dati utilizzate per la manipolazione e l&#39;analisi dei dati
- **matplotlib.pyplot**: Libreria di plottaggio che fornisce un&#39;esperienza simile a MATLAB durante la stampa
- **marinaio** : Libreria di visualizzazione dei dati dell&#39;interfaccia di alto livello basata su matplotlib
- **sklearn**: Libreria di machine learning con classificazione, regressione, supporto di algoritmi vettoriali e cluster
- **avvertenze**: Libreria che controlla i messaggi di avviso

### Esplorare i dati {#exploring-data}

#### Carica dati

Una volta caricate le librerie, è possibile iniziare a osservare i dati. Il [!DNL Python] codice seguente utilizza la struttura di dati dei panda `DataFrame` e la funzione [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) per leggere il CSV ospitato [!DNL Github] nel DataFrame panda:

![](./images/walkthrough/read_csv.png)

La struttura dati DataFrame dei panda è una struttura dati con etichetta bidimensionale. Per visualizzare rapidamente le dimensioni dei dati, puoi usare `df.shape`. Questo restituisce un tupla che rappresenta la dimensione del DataFrame:

![](./images/walkthrough/df_shape.png)

Infine, potete visualizzare un&#39;anteprima dell&#39;aspetto dei dati. È possibile utilizzare `df.head(n)` per visualizzare le prime `n` righe del DataFrame:

![](./images/walkthrough/df_head.png)

#### Riepilogo statistico

Possiamo sfruttare la libreria [!DNL Python's] panda per ottenere il tipo di dati di ciascun attributo. L&#39;output della seguente chiamata fornisce informazioni sul numero di voci e sul tipo di dati per ciascuna colonna:

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

Questa informazione è utile perché conoscere il tipo di dati per ogni colonna ci permetterà di sapere come trattare i dati.

Guardiamo ora il riepilogo statistico. Vengono visualizzati solo i tipi di dati numerici `date`e non `storeType`vengono `isHoliday` generati:

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

Con questo, potete vedere 6435 istanze per ciascuna caratteristica. Inoltre, vengono fornite informazioni statistiche come la media, la deviazione standard (std), il min, il max e gli interquartili. Questo ci dà informazioni sulla deviazione per i dati. Nella sezione successiva, passerai alla visualizzazione che funziona insieme a queste informazioni per darci una comprensione completa dei tuoi dati.

Osservando i valori minimo e massimo per `store`, è possibile vedere che ci sono 45 archivi univoci che i dati rappresentano. Ci sono anche `storeTypes` che differenziano quello che è un negozio. potete visualizzare la distribuzione di `storeTypes` effettuando le seguenti operazioni:

![](./images/walkthrough/df_groupby.png)

Ciò significa che 22 negozi sono di `storeType A` , 17 sono `storeType B`, e 6 sono `storeType C`.

#### Visualizzare i dati

Ora che conosci i valori dei frame dei dati, vuoi integrarli con le visualizzazioni per rendere le cose più chiare e facili da identificare. Questi grafici sono utili anche per trasmettere i risultati a un pubblico.

#### Grafici univoci

I grafici univoci sono grafici di una singola variabile. Un grafico universale comune usato per visualizzare i dati sono i grafici a scatola e a sussurro.

Utilizzando il set di dati per la vendita al dettaglio da prima, potete generare il grafico box e whisker per ciascuno dei 45 negozi e le loro vendite settimanali. Il grafico viene generato utilizzando la `seaborn.boxplot` funzione.

![](./images/walkthrough/box_whisker.png)

Una trama scatola e sussurro è usato per mostrare la distribuzione dei dati. Le linee esterne della trama mostrano i quarti superiori e inferiori mentre la scatola si estende per l&#39;intervallo interquartile. La linea nella casella indica la mediana. I punti di dati più di 1,5 volte il quartile superiore o inferiore sono contrassegnati come un cerchio. Questi punti sono considerati fuorvianti.

Successivamente, puoi tracciare le vendite settimanali con il tempo. Verrà visualizzato solo l&#39;output del primo store. Il codice nel notebook genera 6 punti corrispondenti a 6 dei 45 punti vendita del nostro set di dati.

![](./images/walkthrough/weekly_sales.png)

Con questo diagramma potete confrontare le vendite settimanali su un periodo di 2 anni. È facile vedere picchi di vendita e attraverso schemi nel tempo.

#### Grafici multivariati

I grafici multivariati sono utilizzati per visualizzare l&#39;interazione tra le variabili. Con la visualizzazione, gli esperti di dati possono verificare se esistono correlazioni o pattern tra le variabili. Un grafico multivariato comune usato è una matrice di correlazione. Con una matrice di correlazione, le dipendenze tra più variabili vengono quantificate con il coefficiente di correlazione.

Utilizzando lo stesso dataset per la vendita al dettaglio, potete generare la matrice di correlazione.

![](./images/walkthrough/correlation_1.png)

Osservate la diagonale di quelle che si trovano al centro. Questo indica che quando confronta una variabile con se stessa, ha una correlazione positiva completa. Una forte correlazione positiva avrà una grandezza più vicina a 1, mentre le correlazioni deboli saranno più vicine a 0. La correlazione negativa è mostrata con un coefficiente negativo che mostra una tendenza inversa.

### Progettazione di funzioni {#feature-engineering}

In questa sezione, la funzionalità di progettazione viene utilizzata per apportare modifiche al dataset Retail eseguendo le seguenti operazioni:

- Aggiungi colonne settimana e anno
- Converti storeType in una variabile indicatore
- Converti isHoliday in una variabile numerica
- Predicazione settimanaleVendite della settimana prossima

#### Aggiungi colonne settimana e anno

Il formato corrente per la data (`2010-02-05`) può rendere difficile distinguere che i dati sono per ogni settimana. Per questo motivo, è necessario convertire la data in modo che contenga settimana e anno.

![](./images/walkthrough/date_to_week_year.png)

Ora la settimana e la data sono le seguenti:

![](./images/walkthrough/date_week_year.png)

#### Converti storeType in variabile indicatore

Quindi, convertire la colonna storeType in colonne che rappresentano ciascuna `storeType`. Esistono 3 tipi di store (`A`, `B`, `C`) da cui si creano 3 nuove colonne. Il valore impostato in ogni è un valore booleano in cui viene impostato un valore &#39;1&#39; a seconda di quale `storeType` era e `0` per le altre 2 colonne.

![](./images/walkthrough/storeType.png)

La `storeType` colonna corrente viene eliminata.

#### Converti isHoliday in tipo numerico

La modifica successiva consiste nel modificare il `isHoliday` valore booleano in una rappresentazione numerica.

![](./images/walkthrough/isHoliday.png)

#### Predicazione settimanaleVendite della settimana prossima

Ora puoi aggiungere le vendite settimanali precedenti e future a ciascun set di dati. Puoi farlo offendendo la tua `weeklySales`. Inoltre, la `weeklySales` differenza viene calcolata. Questo avviene sottraendo `weeklySales` con quello della settimana precedente `weeklySales`.

![](./images/walkthrough/weekly_past_future.png)

Poiché si sta effettuando l&#39;offset dei `weeklySales` dati 45 set di dati in avanti e 45 set di dati all&#39;indietro per creare nuove colonne, i primi e gli ultimi 45 punti dati hanno valori NaN. È possibile rimuovere questi punti dal dataset utilizzando la `df.dropna()` funzione che rimuove tutte le righe che hanno valori NaN.

![](./images/walkthrough/dropna.png)

Di seguito è riportato un riepilogo del set di dati dopo le modifiche:

![](./images/walkthrough/df_info_new.png)

### Formazione e verifica {#training-and-verification}

Ora, è il momento di creare alcuni modelli di dati e selezionare quale modello è il migliore per prevedere le vendite future. Verranno valutati i 5 algoritmi seguenti:

- Regressione lineare
- Albero decisionale
- Foresta casuale
- Incremento sfumatura
- K Vicini

#### Dividi set di dati a sottoinsiemi di formazione e test

È necessario un modo per sapere quanto accurato sarà il modello in grado di prevedere i valori. Questa valutazione può essere effettuata assegnando una parte del dataset da utilizzare come convalida e il resto come dati di formazione. Poiché `weeklySalesAhead` sono i valori futuri effettivi di `weeklySales`, è possibile utilizzarli per valutare la precisione con cui il modello è in grado di prevedere il valore. La divisione è effettuata di seguito:

![](./images/walkthrough/split_data.png)

Ora avete `X_train` e `y_train` per preparare i modelli e `X_test` e `y_test` per la valutazione in seguito.

#### Algoritmi di controllo spot

In questa sezione, tutti gli algoritmi vengono dichiarati in un array denominato `model`. Quindi, ripetete l&#39;array e per ogni algoritmo, inserite i dati di formazione con `model.fit()` cui viene creato un modello `mdl`. Utilizzando questo modello, è possibile prevedere `weeklySalesAhead` i `X_test` dati.

![](./images/walkthrough/training_scoring.png)

Per il punteggio, si sta prendendo la differenza percentuale media tra il previsto `weeklySalesAhead` con i valori effettivi nei `y_test` dati. Poiché si desidera ridurre al minimo la differenza tra la previsione e il risultato effettivo, Regressore incremento sfumatura è il modello con le prestazioni migliori.

#### Visualizzare le previsioni

Infine, puoi visualizzare il modello di previsione con i valori di vendita settimanali effettivi. La linea blu rappresenta i numeri effettivi, mentre quella verde rappresenta la previsione utilizzando Incremento sfumatura. Il codice seguente genera 6 appezzamenti che rappresentano 6 dei 45 punti vendita del dataset. Solo `Store 1` qui:

![](./images/walkthrough/visualize_prediction.png)

## Passaggi successivi

Questo documento ha trattato un flusso di lavoro generale di analisi dei dati per risolvere un problema di vendita al dettaglio. Per riepilogare:

- Caricate le librerie necessarie per il flusso di lavoro.
- Una volta caricate le librerie, è possibile iniziare a osservare i dati utilizzando riepiloghi statistici, visualizzazioni e grafici.
- Successivamente, la funzionalità di progettazione viene utilizzata per apportare modifiche al set di dati per la vendita al dettaglio.
- Infine, creare modelli di dati e selezionare quale modello è il più performante per prevedere le vendite future.

Una volta pronti, leggi la guida [utente](./jupyterlab/overview.md) JupyterLab per una rapida panoramica dei notebook in Adobe Experience Platform Data Science Workspace. Inoltre, se siete interessati a conoscere Modelli e Ricette, iniziare leggendo lo schema di vendita al [dettaglio e l&#39;esercitazione sui dataset](./models-recipes/create-retails-sales-dataset.md) . Questa esercitazione prepara le esercitazioni di Data Science Workspace successive, che possono essere visualizzate nella pagina delle [esercitazioni](../tutorials/data-science-workspace.md)di Data Science Workspace.