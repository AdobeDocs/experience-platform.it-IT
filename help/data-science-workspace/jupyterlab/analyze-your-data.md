---
keywords: Experience Platform;JupyterLab;notebook;Data Science Workspace;argomenti comuni;analizzare i notebook di dati
solution: Experience Platform
title: Analizzare i dati utilizzando i notebook
type: Tutorial
description: Questa esercitazione si concentra su come utilizzare i notebook Jupyter, generati in Data Science Workspace, per accedere, esplorare e visualizzare i tuoi dati.
exl-id: 3b0148d1-9c08-458b-9601-979cb6c7a0fb
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 0%

---

# Analizzare i dati utilizzando i notebook

Questa esercitazione si concentra su come utilizzare i notebook Jupyter, generati in Data Science Workspace, per accedere, esplorare e visualizzare i tuoi dati. Al termine di questa esercitazione, dovresti avere una comprensione di alcune delle funzioni offerte da Jupyter Notebooks per comprendere meglio i tuoi dati.

Vengono introdotti i seguenti concetti:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) è l’interfaccia web di nuova generazione per Project Jupyter ed è strettamente integrata in [!DNL Adobe Experience Platform].
- **Batch:** I set di dati sono costituiti da batch. Un batch è un insieme di dati raccolti in un periodo di tempo ed elaborati insieme come una singola unità. Vengono creati nuovi batch quando i dati vengono aggiunti a un set di dati.
- **Data Access SDK (obsoleto):** L’SDK per l’accesso ai dati è ora obsoleto. Utilizza la [[!DNL Platform SDK]](../authoring/platform-sdk.md) guida.

## Esplorare i notebook in Data Science Workspace

In questa sezione vengono esaminati i dati precedentemente acquisiti nello schema vendite al dettaglio.

Data Science Workspace consente agli utenti di creare [!DNL Jupyter Notebooks] attraverso [!DNL JupyterLab] piattaforma in cui possono creare e modificare flussi di lavoro di apprendimento automatico. [!DNL JupyterLab] è uno strumento di collaborazione server-client che consente agli utenti di modificare i documenti del blocco appunti tramite un browser web. Questi blocchi appunti possono contenere sia codice eseguibile che elementi RTF. Per i nostri scopi, utilizzeremo Markdown per la descrizione dell’analisi e l’eseguibile [!DNL Python] codice per eseguire esplorazione e analisi dei dati.

### Scegliere l&#39;area di lavoro

Quando si avvia [!DNL JupyterLab], ti viene presentata un’interfaccia web basata su Jupyter Notebooks. A seconda del tipo di notebook scelto, verrà lanciato un kernel corrispondente.

Quando si confronta l&#39;ambiente da utilizzare, è necessario tenere conto dei limiti di ogni servizio. Ad esempio, se utilizzi il [panda](https://pandas.pydata.org/) libreria con [!DNL Python], in qualità di utente normale, il limite di RAM è di 2 GB. Anche in qualità di utente di alimentazione, saremmo limitati a 20 GB di RAM. Se si tratta di calcoli più grandi, avrebbe senso utilizzare [!DNL Spark] che offre 1,5 TB condivisi con tutte le istanze del notebook.

Per impostazione predefinita, la ricetta di flusso di Tensorflow funziona in un cluster GPU e Python viene eseguito all&#39;interno di un cluster di CPU.

### Crea un nuovo blocco appunti

In [!DNL Adobe Experience Platform] Interfaccia utente, seleziona [!UICONTROL Data Science] nel menu principale per passare a Data Science Workspace. Da questa pagina, seleziona [!DNL JupyterLab] per aprire [!DNL JupyterLab] lanciatore. Dovresti vedere una pagina simile a questa.

![](../images/jupyterlab/analyze-data/jupyterlab-launcher-new.png)

Nel nostro tutorial, utilizzeremo [!DNL Python] 3 nel notebook Jupyter per mostrare come accedere ed esplorare i dati. Nella pagina Launcher sono disponibili alcuni blocchi appunti di esempio. Useremo la ricetta Vendite al dettaglio per [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

La ricetta Vendite al dettaglio è un esempio autonomo che utilizza lo stesso set di dati Vendite al dettaglio per mostrare come è possibile esplorare e visualizzare i dati nel blocco appunti Jupyter. Inoltre, il notebook si spinge oltre con formazione e verifica. Ulteriori informazioni su questo blocco appunti specifico sono disponibili in questo [passaggio](../walkthrough.md).

### Accedere ai dati

>[!NOTE]
>
>La `data_access_sdk_python` è obsoleto e non è più consigliato. Fai riferimento alla [conversione dell’SDK per l’accesso ai dati in Platform SDK](../authoring/platform-sdk.md) esercitazione per convertire il codice. Per questa esercitazione si applicano gli stessi passaggi riportati di seguito.

Accedere ai dati internamente da [!DNL Adobe Experience Platform] e dati esterni. Useremo `data_access_sdk_python` per accedere a dati interni, ad esempio set di dati e schemi XDM. Per i dati esterni, utilizzeremo i panda [!DNL Python] libreria.

#### Dati esterni

Con il blocco appunti Vendite al dettaglio aperto, trovare l&#39;intestazione &quot;Load Data&quot;. I seguenti [!DNL Python] Il codice utilizza i panda&#39; `DataFrame` la struttura dei dati e [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) per leggere il CSV ospitato su [!DNL Github] nel DataFrame:

![](../images/jupyterlab/analyze-data/read_csv.png)

La struttura dati DataFrame dei panda è una struttura dati con etichetta bidimensionale. Per vedere rapidamente le dimensioni dei nostri dati, possiamo utilizzare `df.shape`. Restituisce una tupla che rappresenta la dimensione del DataFrame:

![](../images/jupyterlab/analyze-data/df_shape.png)

Infine, possiamo dare un&#39;occhiata a come sono i nostri dati. Possiamo usare `df.head(n)` per visualizzare il primo `n` righe del DataFrame:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] dati

Ora passeremo oltre l&#39;accesso [!DNL Experience Platform] dati.

##### Per ID set di dati

Per questa sezione, utilizziamo il set di dati Vendite al dettaglio che è lo stesso set di dati utilizzato nel blocco appunti di esempio Vendite al dettaglio.

In Jupyter Notebook, è possibile accedere ai dati da **Dati** scheda ![scheda dati](../images/jupyterlab/analyze-data/dataset-tab.png) a sinistra. Dopo aver selezionato la scheda , vengono fornite due cartelle. Seleziona la **[!UICONTROL Set di dati]** cartella.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Ora nella directory Datasets puoi visualizzare tutti i set di dati acquisiti. Tieni presente che il caricamento di tutte le voci potrebbe richiedere un minuto se la directory è densamente popolata con set di dati.

Poiché il set di dati è lo stesso, sostituiamo i dati di caricamento della sezione precedente che utilizza dati esterni. Seleziona il blocco di codice sotto **Carica dati** e premere **&quot;d&quot;** tenete premuto due volte sulla tastiera. Assicurati che lo stato attivo sia sul blocco e non nel testo. È possibile premere **&quot;esc&quot;** per evitare lo stato attivo del testo prima di premere **&quot;d&quot;** due volte.

Ora possiamo fare clic con il pulsante destro del mouse sul `Retail-Training-<your-alias>` e seleziona l’opzione &quot;Esplora dati nel blocco appunti&quot; nel menu a discesa. Nel blocco appunti verrà visualizzata una voce di codice eseguibile.

>[!TIP]
>
>Fai riferimento a [[!DNL Platform SDK]](../authoring/platform-sdk.md) guida per convertire il codice.

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Se lavori su kernel diversi da [!DNL Python], si prega di fare riferimento a [questa pagina](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) per accedere ai dati [!DNL Adobe Experience Platform].

Quando si seleziona la cella eseguibile e si preme il pulsante di riproduzione nella barra degli strumenti, viene eseguito il codice eseguibile. Uscita per `head()` sarà una tabella con le chiavi del set di dati come colonne e le prime n righe del set di dati. `head()` accetta un argomento integer per specificare il numero di righe da restituire. Per impostazione predefinita è 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Se si riavvia il kernel e si eseguono di nuovo tutte le celle, si dovrebbero ottenere gli stessi output di prima.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Esplorare i dati

Ora che possiamo accedere ai tuoi dati, concentriamoci sui dati stessi utilizzando le statistiche e la visualizzazione. Il set di dati che utilizziamo è un set di dati al dettaglio che fornisce informazioni varie su 45 diversi negozi in un dato giorno. Alcune caratteristiche per una data `date` e `store` includere quanto segue:
- `storeType`
- `weeklySales`
- `storeSize`
- `temperature`
- `regionalFuelPrice`
- `markDown`
- `cpi`
- `unemployment`
- `isHoliday`

#### Riepilogo statistico

Possiamo sfruttare [!DNL Python's] libreria panda per ottenere il tipo di dati di ciascun attributo. L’output della seguente chiamata ci fornirà informazioni sul numero di voci e sul tipo di dati per ciascuna colonna:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Questa informazione è utile in quanto conoscere il tipo di dati per ogni colonna ci consentirà di sapere come trattare i dati.

Ora diamo un&#39;occhiata al riepilogo statistico. Verranno visualizzati solo i tipi di dati numerici, quindi `date`, `storeType`e `isHoliday` non verrà generato:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

Con questo, possiamo vedere che ci sono 6435 istanze per ogni caratteristica. Vengono inoltre fornite informazioni statistiche quali media, deviazione standard (std), min, max e interquartili. Questo ci dà informazioni sulla deviazione per i dati. Nella sezione successiva, passeremo alla visualizzazione che funziona insieme a queste informazioni per darci una buona comprensione dei nostri dati.

Osservare i valori minimo e massimo per `store`, possiamo vedere che ci sono 45 archivi unici che i dati rappresentano. Vi sono anche `storeTypes` che differenziano ciò che è un negozio. Possiamo vedere la distribuzione di `storeTypes` eseguendo le operazioni seguenti:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Ciò significa che 22 negozi sono `storeType` `A`, 17 `storeType` `B`e 6 `storeType` `C`.

#### Visualizzazione dati

Ora che conosciamo i nostri valori dei fotogrammi dati, vogliamo integrarli con le visualizzazioni per rendere le cose più chiare e più facili da identificare i pattern. I grafici sono utili anche per veicolare i risultati a un pubblico. Alcuni [!DNL Python] Le librerie utili per la visualizzazione includono:
- [Matplotlib](https://matplotlib.org/)
- [panda](https://pandas.pydata.org/)
- [marinaio](https://seaborn.pydata.org/)
- [grondaia](https://ggplot2.tidyverse.org/)

In questa sezione presenteremo rapidamente alcuni vantaggi per l’utilizzo di ogni libreria.

[Matplotlib](https://matplotlib.org/) è il più vecchio [!DNL Python] pacchetto di visualizzazione. Il loro obiettivo è quello di rendere &quot;le cose facili e difficili possibili&quot;. Questo tende ad essere vero in quanto il pacchetto è estremamente potente, ma viene anche con la complessità. Non è sempre facile ottenere un grafico dall&#39;aspetto ragionevole senza richiedere molto tempo e fatica.

[Panda](https://pandas.pydata.org/) viene utilizzato principalmente per il suo oggetto DataFrame che consente la manipolazione dei dati con indicizzazione integrata. Tuttavia, i panda includono anche una funzionalità di tracciamento integrata basata su matplotlib.

[marinaio](https://seaborn.pydata.org/) è un pacchetto basato su matplotlib. L&#39;obiettivo principale è rendere i grafici predefiniti più accattivanti visivamente e semplificare la creazione di grafici complicati.

[grondaia](https://ggplot2.tidyverse.org/) è un pacchetto costruito anche sopra matplotlib. Tuttavia, la differenza principale è che lo strumento è una porta di gplot2 per R. Simile al mare, l’obiettivo è quello di migliorare su matplotlib. Gli utenti che hanno familiarità con gplot2 per R devono considerare questa libreria.


##### Grafici universali

I grafici univoci sono grafici di una singola variabile. Un grafico universale comune è usato per visualizzare i vostri dati è la trama box e whisker.

Utilizzando il nostro set di dati retail da prima, possiamo generare la trama box e whisker per ciascuno dei 45 negozi e le loro vendite settimanali. Il tracciato viene generato utilizzando la variabile `seaborn.boxplot` funzione .

![](../images/jupyterlab/analyze-data/box_whisker.png)

Per mostrare la distribuzione dei dati viene utilizzato un grafico a scatola e a sussurro. Le linee esterne della trama mostrano i quartili superiori e inferiori, mentre la scatola si estende per l&#39;intervallo interquartile. La linea nella casella indica la mediana. I punti di dati più di 1,5 volte il quartile superiore o inferiore sono contrassegnati come cerchio. Questi punti sono considerati come anomali.

##### Grafici multivariati

I grafici multivariati vengono utilizzati per vedere l’interazione tra le variabili. Con la visualizzazione, gli scienziati dei dati possono vedere se ci sono correlazioni o pattern tra le variabili. Un grafico multivariato comune utilizzato è una matrice di correlazione. Con una matrice di correlazione, le dipendenze tra più variabili sono quantificate con il coefficiente di correlazione.

Utilizzando lo stesso set di dati per la vendita al dettaglio, possiamo generare la matrice di correlazione.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Notate la diagonale di 1 in basso al centro. Questo dimostra che quando si confronta una variabile con se stessa, ha una correlazione completamente positiva. Una forte correlazione positiva avrà una grandezza più vicina a 1, mentre le correlazioni deboli saranno più vicine a 0. La correlazione negativa viene mostrata con un coefficiente negativo che mostra una tendenza inversa.


## Passaggi successivi

Questa esercitazione illustra come creare un nuovo blocco appunti Jupyter in Data Science Workspace e come accedere ai dati sia esternamente che da [!DNL Adobe Experience Platform]. In particolare, abbiamo seguito i seguenti passaggi:
- Crea un nuovo blocco appunti Jupyter
- Accedere a set di dati e schemi
- Esplorare i set di dati

Ora sei pronto a passare alla [sezione successiva](../models-recipes/package-source-files-recipe.md) creare un pacchetto di una ricetta e importarla in Data Science Workspace.
