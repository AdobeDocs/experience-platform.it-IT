---
keywords: Experience Platform;procedura dettagliata;Data Science Workspace;argomenti comuni
solution: Experience Platform
title: Procedura dettagliata su Data Science Workspace
topic-legacy: Walkthrough
description: Questo documento fornisce una procedura dettagliata per Adobe Experience Platform Data Science Workspace. Nello specifico, il flusso di lavoro generale che un esperto di dati dovrebbe seguire per risolvere un problema utilizzando l'apprendimento automatico.
exl-id: d814846e-52a9-46c6-831a-3399241959f2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 0%

---

# [!DNL Data Science Workspace] passaggio

Questo documento fornisce una procedura dettagliata per Adobe Experience Platform [!DNL Data Science Workspace]. Questa esercitazione descrive un flusso di lavoro generale di data scientist e come potrebbero affrontare e risolvere un problema utilizzando l&#39;apprendimento automatico.

## Prerequisiti

- Un account Adobe ID registrato
   - L’account Adobe ID deve essere stato aggiunto a un’organizzazione con accesso a Adobe Experience Platform e [!DNL Data Science Workspace].

## Caso di utilizzo al dettaglio

Un retailer deve affrontare molte sfide per rimanere competitivo nel mercato attuale. Una delle principali preoccupazioni del rivenditore è quella di decidere il prezzo ottimale di un prodotto e di prevedere le tendenze di vendita. Con un modello di previsione accurato, un rivenditore sarebbe in grado di trovare il rapporto tra le politiche di domanda e di prezzo e di prendere decisioni di prezzo ottimizzate per massimizzare le vendite e i ricavi.

## Soluzione per gli scienziati di dati

La soluzione di uno scienziato dei dati è quella di sfruttare la ricchezza di informazioni storiche fornite da un rivenditore, prevedere le tendenze future e ottimizzare le decisioni in materia di prezzi. Questa procedura dettagliata utilizza i dati di vendita passati per addestrare un modello di apprendimento automatico e utilizza il modello per prevedere le tendenze di vendita future. Con questo, puoi generare informazioni per apportare modifiche ottimali ai prezzi.

Questa panoramica rispecchia i passi che un esperto di dati dovrebbe compiere per prendere un set di dati e creare un modello per prevedere le vendite settimanali. Questa esercitazione copre le sezioni seguenti del Sample Retail Sales Notebook su Adobe Experience Platform [!DNL Data Science Workspace]:

- [Configurazione](#setup)
- [Esplorazione dei dati](#exploring-data)
- [Progettazione delle funzioni](#feature-engineering)
- [Formazione e verifica](#training-and-verification)

### Notebook in [!DNL Data Science Workspace]

Nell’interfaccia utente di Adobe Experience Platform, seleziona **[!UICONTROL Notebooks]** dalla scheda **[!UICONTROL Data Science]** per passare alla pagina di panoramica [!UICONTROL Notebooks]. Da questa pagina, seleziona la scheda [!DNL JupyterLab] per avviare l&#39;ambiente [!DNL JupyterLab]. La pagina di destinazione predefinita per [!DNL JupyterLab] è **[!UICONTROL Launcher]**.

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

Questa esercitazione utilizza [!DNL Python] 3 in [!DNL JupyterLab Notebooks] per mostrare come accedere ai dati ed esplorarli. Nella pagina Launcher sono disponibili alcuni blocchi appunti di esempio. Il blocco appunti di esempio **[!UICONTROL Retail Sales]** viene utilizzato negli esempi forniti di seguito.

### Configurazione {#setup}

Con il blocco appunti Vendite al dettaglio aperto, la prima cosa da fare è caricare le librerie necessarie per il flusso di lavoro. L’elenco seguente fornisce una breve descrizione di ciascuna delle librerie utilizzate negli esempi nei passaggi successivi.

- **numero**: Libreria di elaborazione scientifica che aggiunge supporto per array e matrici multidimensionali di grandi dimensioni
- **panda**: Libreria che offre strutture e operazioni di dati utilizzate per la manipolazione e l’analisi dei dati
- **matplotlib.pyplot**: Libreria di plottaggio che offre un’esperienza simile a MATLAB durante la creazione di un grafico
- **marinaio** : Libreria di visualizzazione dei dati dell’interfaccia di alto livello basata su matplotlib
- **sklearn**: Libreria di apprendimento automatico con classificazione, regressione, supporto di algoritmi vettoriali e cluster
- **avvisi**: Libreria che controlla i messaggi di avviso

### Esplorare i dati {#exploring-data}

#### Caricare dati

Una volta caricate le librerie, puoi iniziare a esaminare i dati. Il codice seguente [!DNL Python] utilizza la struttura dati `DataFrame` dei panda e la funzione [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) per leggere il CSV ospitato su [!DNL Github] nel DataFrame panda:

![](./images/walkthrough/read_csv.png)

La struttura dati DataFrame dei panda è una struttura dati con etichetta bidimensionale. Per visualizzare rapidamente le dimensioni dei dati, puoi utilizzare `df.shape`. Restituisce una tupla che rappresenta la dimensione del DataFrame:

![](./images/walkthrough/df_shape.png)

Infine, puoi visualizzare in anteprima l’aspetto dei tuoi dati. È possibile utilizzare `df.head(n)` per visualizzare le prime `n` righe del DataFrame:

![](./images/walkthrough/df_head.png)

#### Riepilogo statistico

È possibile sfruttare la libreria panda [!DNL Python's] per ottenere il tipo di dati di ciascun attributo. L’output della seguente chiamata ci fornirà informazioni sul numero di voci e sul tipo di dati per ciascuna colonna:

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

Questa informazione è utile in quanto conoscere il tipo di dati per ogni colonna ci consentirà di sapere come trattare i dati.

Ora diamo un&#39;occhiata al riepilogo statistico. Verranno visualizzati solo i tipi di dati numerici in modo che `date`, `storeType` e `isHoliday` non vengano generati:

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

Con questo, potete vedere che ci sono 6435 istanze per ogni caratteristica. Vengono inoltre fornite informazioni statistiche quali la media, la deviazione standard (std), il minimo, il massimo e gli interquartili. Questo ci dà informazioni sulla deviazione per i dati. Nella sezione successiva, passerai alla visualizzazione che funziona insieme a queste informazioni per fornirci una comprensione completa dei tuoi dati.

Osservando i valori minimo e massimo per `store`, puoi notare che sono presenti 45 archivi univoci che i dati rappresentano. Ci sono anche `storeTypes` che differenziano ciò che un negozio è. puoi vedere la distribuzione di `storeTypes` facendo quanto segue:

![](./images/walkthrough/df_groupby.png)

Ciò significa che 22 negozi sono di `storeType A` , 17 sono `storeType B` e 6 sono `storeType C`.

#### Visualizzare i dati

Ora che conosci i valori dei fotogrammi dati, vuoi integrarli con le visualizzazioni per rendere le cose più chiare e più facili da identificare i pattern. Questi grafici sono utili anche per veicolare i risultati a un pubblico.

#### Grafici universali

I grafici univoci sono grafici di una singola variabile. Un grafico universale comune usato per visualizzare i tuoi dati sono disegni box e whisker.

Utilizzando il set di dati per la vendita al dettaglio da prima, è possibile generare il grafico box e whisker per ciascuno dei 45 negozi e le loro vendite settimanali. Il grafico viene generato utilizzando la funzione `seaborn.boxplot` .

![](./images/walkthrough/box_whisker.png)

Per mostrare la distribuzione dei dati viene utilizzato un grafico a scatola e a sussurro. Le linee esterne della trama mostrano i quartili superiori e inferiori mentre la scatola si estende per l&#39;intervallo interquartile. La linea nella casella indica la mediana. I punti di dati più di 1,5 volte il quartile superiore o inferiore sono contrassegnati come cerchio. Questi punti sono considerati come anomali.

Successivamente, puoi tracciare le vendite settimanali con il tempo. Verrà visualizzato solo l&#39;output del primo negozio. Il codice nel blocco appunti genera 6 grafici corrispondenti a 6 dei 45 negozi nel nostro set di dati.

![](./images/walkthrough/weekly_sales.png)

Con questo diagramma è possibile confrontare le vendite settimanali su un periodo di 2 anni. È facile vedere picchi di vendita e schemi di base nel tempo.

#### Grafici multivariati

I grafici multivariati vengono utilizzati per vedere l’interazione tra le variabili. Con la visualizzazione, gli scienziati dei dati possono vedere se ci sono correlazioni o pattern tra le variabili. Un grafico multivariato comune utilizzato è una matrice di correlazione. Con una matrice di correlazione, le dipendenze tra più variabili sono quantificate con il coefficiente di correlazione.

Utilizzando lo stesso set di dati retail, puoi generare la matrice di correlazione.

![](./images/walkthrough/correlation_1.png)

Notate la diagonale di quelle in basso al centro. Questo dimostra che quando si confronta una variabile con se stessa, ha una correlazione completamente positiva. Una forte correlazione positiva avrà una grandezza più vicina a 1, mentre le correlazioni deboli saranno più vicine a 0. La correlazione negativa viene mostrata con un coefficiente negativo che mostra una tendenza inversa.

### Progettazione di funzioni {#feature-engineering}

In questa sezione, l’ingegneria delle funzioni viene utilizzata per apportare modifiche al set di dati Retail eseguendo le seguenti operazioni:

- Aggiungi colonne settimana e anno
- Converti storeType in una variabile indicatore
- Converti isHoliday in una variabile numerica
- Predicazione settimanaleVendite della settimana prossima

#### Aggiungi colonne settimana e anno

Il formato corrente per la data (`2010-02-05`) può rendere difficile distinguere che i dati sono per ogni settimana. Per questo motivo, devi convertire la data in modo che contenga settimana e anno.

![](./images/walkthrough/date_to_week_year.png)

Ora la settimana e la data sono le seguenti:

![](./images/walkthrough/date_week_year.png)

#### Converti storeType in variabile indicatore

Successivamente, convertire la colonna storeType in colonne che rappresentano ogni `storeType`. Sono disponibili 3 tipi di archivio, (`A`, `B`, `C`), dai quali si stanno creando 3 nuove colonne. Il valore impostato in ogni è un valore booleano in cui viene impostato un valore &#39;1&#39; a seconda di quale era `storeType` e `0` per le altre 2 colonne.

![](./images/walkthrough/storeType.png)

La colonna `storeType` corrente viene rilasciata.

#### Converti isHolay in tipo numerico

La modifica successiva consiste nel modificare il valore booleano `isHoliday` in una rappresentazione numerica.

![](./images/walkthrough/isHoliday.png)

#### Predicazione settimanaleVendite della settimana prossima

Ora desideri aggiungere vendite settimanali precedenti e future a ciascuno dei set di dati. Per farlo, offri il tuo `weeklySales`. Inoltre, viene calcolata la differenza `weeklySales`. Questo viene fatto sottraendo `weeklySales` con la settimana precedente `weeklySales`.

![](./images/walkthrough/weekly_past_future.png)

Poiché si sta eseguendo l’offset dei `weeklySales` set di dati in avanti e successivi 45 e retromarcia per creare nuove colonne, i primi e gli ultimi 45 punti di dati hanno valori NaN. Puoi rimuovere questi punti dal set di dati utilizzando la funzione `df.dropna()` che rimuove tutte le righe con valori NaN.

![](./images/walkthrough/dropna.png)

Di seguito è riportato un riepilogo del set di dati dopo le modifiche apportate:

![](./images/walkthrough/df_info_new.png)

### Formazione e verifica {#training-and-verification}

Ora, è il momento di creare alcuni modelli di dati e selezionare quale modello è il più performante per prevedere le vendite future. Verranno valutati i 5 seguenti algoritmi:

- Regressione lineare
- Albero decisionale
- Foresta casuale
- Incremento sfumatura
- Vicini K

#### Dividi set di dati per formare e testare sottoinsiemi

È necessario un modo per sapere quanto accurato sarà il modello in grado di prevedere i valori. Questa valutazione può essere effettuata allocando parte del set di dati da utilizzare come convalida e il resto come dati di formazione. Poiché `weeklySalesAhead` è il valore futuro effettivo di `weeklySales`, puoi utilizzarlo per valutare la precisione del modello nella previsione del valore. La divisione viene eseguita di seguito:

![](./images/walkthrough/split_data.png)

Ora disponi di `X_train` e `y_train` per preparare i modelli e `X_test` e `y_test` per la valutazione in un secondo momento.

#### Algoritmi di controllo a punti

In questa sezione vengono dichiarati tutti gli algoritmi in un array denominato `model`. Successivamente, esegui un&#39;iterazione attraverso questo array e per ogni algoritmo, inserisci i dati di formazione con `model.fit()` che crea un modello `mdl`. Utilizzando questo modello, è possibile prevedere `weeklySalesAhead` con i dati `X_test`.

![](./images/walkthrough/training_scoring.png)

Per il punteggio, si sta prendendo la differenza percentuale media tra il valore previsto `weeklySalesAhead` e i valori effettivi nei dati `y_test`. Poiché si desidera ridurre al minimo la differenza tra la previsione e il risultato effettivo, il Regressore di incremento della sfumatura è il modello con le prestazioni migliori.

#### Visualizzare le previsioni

Infine, puoi visualizzare il modello di previsione con i valori di vendita settimanali effettivi. La linea blu rappresenta i numeri effettivi, mentre il verde rappresenta la previsione utilizzando Incremento sfumatura. Il codice seguente genera 6 grafici che rappresentano 6 dei 45 archivi nel set di dati. Solo `Store 1` viene visualizzato qui:

![](./images/walkthrough/visualize_prediction.png)

## Passaggi successivi

Questo documento ha trattato un flusso di lavoro generale di data scientist per risolvere un problema di vendita al dettaglio. Per riepilogare:

- Carica le librerie necessarie per il flusso di lavoro.
- Una volta caricate le librerie, puoi iniziare a esaminare i dati utilizzando riepiloghi statistici, visualizzazioni e grafici.
- Successivamente, l’ingegneria delle funzioni viene utilizzata per apportare modifiche al set di dati retail.
- Infine, crea modelli dei dati e seleziona quale modello è il più performante per prevedere le vendite future.

Quando sei pronto, inizia leggendo la [Guida utente di JupyterLab](./jupyterlab/overview.md) per una rapida panoramica dei notebook in Adobe Experience Platform Data Science Workspace. Inoltre, se sei interessato a conoscere Modelli e Ricette, inizia leggendo il tutorial [schema di vendita al dettaglio e set di dati](./models-recipes/create-retails-sales-dataset.md) . Questa esercitazione ti prepara per le successive esercitazioni di Data Science Workspace che possono essere visualizzate nella pagina delle esercitazioni di Data Science Workspace [](../tutorials/data-science-workspace.md).
