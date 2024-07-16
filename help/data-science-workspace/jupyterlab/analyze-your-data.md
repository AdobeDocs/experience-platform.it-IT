---
keywords: Experience Platform;JupyterLab;blocchi appunti;Data Science Workspace;argomenti popolari;analizzare i blocchi appunti dati
solution: Experience Platform
title: Analizzare I Dati Utilizzando I Notebook
type: Tutorial
description: Questo tutorial si concentra su come utilizzare Jupyter Notebooks, integrato in Data Science Workspace, per accedere, esplorare e visualizzare i tuoi dati.
exl-id: 3b0148d1-9c08-458b-9601-979cb6c7a0fb
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 0%

---

# Analizzare i dati utilizzando i notebook

Questo tutorial si concentra su come utilizzare Jupyter Notebooks, integrato in Data Science Workspace, per accedere, esplorare e visualizzare i tuoi dati. Al termine di questa esercitazione, avrai acquisito una conoscenza di alcune delle funzioni offerte da Jupyter Notebooks per comprendere meglio i tuoi dati.

Sono introdotti i seguenti concetti:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) è l&#39;interfaccia Web di nuova generazione per Project Jupyter ed è strettamente integrata in [!DNL Adobe Experience Platform].
- **Batch:** I set di dati sono costituiti da batch. Un batch è un insieme di dati raccolti in un periodo di tempo ed elaborati insieme come una singola unità. Quando i dati vengono aggiunti a un set di dati vengono creati nuovi batch.
- **SDK per l&#39;accesso ai dati (obsoleto):** L&#39;SDK per l&#39;accesso ai dati è ora obsoleto. Utilizzare la guida di [[!DNL Platform SDK]](../authoring/platform-sdk.md).

## Esplorare i notebook in Data Science Workspace

In questa sezione vengono esaminati i dati precedentemente acquisiti nello schema di vendita al dettaglio.

Data Science Workspace consente agli utenti di creare [!DNL Jupyter Notebooks] tramite la piattaforma [!DNL JupyterLab], dove possono creare e modificare flussi di lavoro di apprendimento automatico. [!DNL JupyterLab] è uno strumento di collaborazione server-client che consente agli utenti di modificare i documenti del blocco appunti tramite un browser Web. Questi blocchi appunti possono contenere sia codice eseguibile che elementi in formato Rich Text. A tale scopo, utilizzeremo Markdown per la descrizione dell&#39;analisi e il codice eseguibile [!DNL Python] per eseguire l&#39;esplorazione e l&#39;analisi dei dati.

### Scegli il tuo workspace

All&#39;avvio di [!DNL JupyterLab], viene presentata un&#39;interfaccia basata sul Web per Jupyter Notebooks. A seconda del tipo di notebook scelto, verrà avviato un kernel corrispondente.

Quando confrontiamo l’ambiente da utilizzare, dobbiamo tenere conto delle limitazioni di ciascun servizio. Ad esempio, se utilizziamo la libreria [pandas](https://pandas.pydata.org/) con [!DNL Python], come utente normale il limite di RAM è di 2 GB. Anche in qualità di utente avanzato, il limite massimo è di 20 GB di RAM. Per i calcoli di dimensioni maggiori, è consigliabile utilizzare [!DNL Spark], che offre 1,5 TB condivisi con tutte le istanze del blocco appunti.

Per impostazione predefinita, la ricetta Tensorflow funziona in un cluster GPU e Python viene eseguito all’interno di un cluster CPU.

### Crea un nuovo blocco appunti

Nell&#39;interfaccia utente di [!DNL Adobe Experience Platform], seleziona [!UICONTROL Data Science] nel menu principale per passare a Data Science Workspace. Da questa pagina, selezionare [!DNL JupyterLab] per aprire il modulo di avvio [!DNL JupyterLab]. Dovresti visualizzare una pagina simile a questa.

![](../images/jupyterlab/analyze-data/jupyterlab-launcher-new.png)

Nel nostro tutorial, utilizzeremo [!DNL Python] 3 nel Jupyter Notebook per mostrare come accedere ed esplorare i dati. Nella pagina di avvio sono disponibili blocchi appunti di esempio. Verrà utilizzata la ricetta Vendite al dettaglio per [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

La ricetta Vendite al dettaglio è un esempio indipendente che utilizza lo stesso set di dati Vendite al dettaglio per mostrare come i dati possono essere esplorati e visualizzati in Jupyter Notebook. Inoltre, il notebook è ulteriormente approfondito con l&#39;addestramento e la verifica. Ulteriori informazioni su questo blocco appunti specifico sono disponibili in questa [procedura dettagliata](../walkthrough.md).

### Accedere ai dati

>[!NOTE]
>
>`data_access_sdk_python` è obsoleto e non è più consigliato. Fai riferimento all&#39;esercitazione [conversione dell&#39;SDK di accesso ai dati in SDK piattaforma](../authoring/platform-sdk.md) per convertire il codice. Per questa esercitazione valgono ancora gli stessi passaggi indicati di seguito.

L&#39;accesso ai dati interni da [!DNL Adobe Experience Platform] e esterni verrà eseguito. La libreria `data_access_sdk_python` verrà utilizzata per accedere a dati interni come set di dati e schemi XDM. Per i dati esterni, verrà utilizzata la libreria Panda [!DNL Python].

#### Dati esterni

Con il blocco appunti Retail Sales aperto, trovare l&#39;intestazione &quot;Load Data&quot;. Il codice [!DNL Python] seguente utilizza la struttura dati `DataFrame` dei panda e la funzione [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) per leggere il file CSV in hosting su [!DNL Github] nel DataFrame:

![](../images/jupyterlab/analyze-data/read_csv.png)

La struttura dati DataFrame di Pandas è una struttura di dati etichettata bidimensionale. Per visualizzare rapidamente le dimensioni dei dati, è possibile utilizzare `df.shape`. Restituisce una tupla che rappresenta la dimensionalità del DataFrame:

![](../images/jupyterlab/analyze-data/df_shape.png)

Infine, possiamo dare un&#39;occhiata all&#39;aspetto dei nostri dati. È possibile utilizzare `df.head(n)` per visualizzare le prime `n` righe del DataFrame:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] dati

Ora si passa all&#39;accesso ai dati [!DNL Experience Platform].

##### Per ID set di dati

Per questa sezione viene utilizzato il set di dati Vendite al dettaglio, che è lo stesso set di dati utilizzato nel blocco appunti di esempio Vendite al dettaglio.

In Jupyter Notebook, puoi accedere ai tuoi dati dalla scheda **Dati** ![Dati](../images/jupyterlab/analyze-data/dataset-tab.png) a sinistra. Selezionando la scheda, vengono fornite due cartelle. Selezionare la cartella **[!UICONTROL Set di dati]**.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Ora nella directory Set di dati puoi visualizzare tutti i set di dati acquisiti. Se la directory è densamente popolata da set di dati, il caricamento di tutte le voci potrebbe richiedere un minuto.

Poiché il set di dati è lo stesso, vogliamo sostituire i dati di caricamento della sezione precedente che utilizza dati esterni. Selezionare il blocco di codice in **Carica dati** e premere due volte il tasto **&#39;d&#39;** sulla tastiera. Assicurati che lo stato attivo sia sul blocco e non nel testo. È possibile premere **&#39;esc&#39;** per uscire dallo stato attivo prima di premere **&#39;d&#39;** due volte.

Ora è possibile fare clic con il pulsante destro del mouse sul set di dati `Retail-Training-<your-alias>` e selezionare l&#39;opzione &quot;Esplora dati nel blocco appunti&quot; nel menu a discesa. Nel blocco appunti verrà visualizzata una voce di codice eseguibile.

>[!TIP]
>
>Per convertire il codice, consultare la guida di [[!DNL Platform SDK]](../authoring/platform-sdk.md).

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Se stai lavorando su kernel diversi da [!DNL Python], fai riferimento a [questa pagina](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) per accedere ai dati su [!DNL Adobe Experience Platform].

Se si seleziona la cella eseguibile e si preme il pulsante di riproduzione nella barra degli strumenti, verrà eseguito il codice eseguibile. L&#39;output per `head()` sarà una tabella con le chiavi del set di dati come colonne e le prime n righe del set di dati. `head()` accetta un argomento di tipo Integer per specificare il numero di righe da restituire. Per impostazione predefinita è 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Se si riavvia il kernel e si eseguono di nuovo tutte le celle, si dovrebbero ottenere gli stessi output di prima.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Esplora i tuoi dati

Ora che possiamo accedere ai tuoi dati, concentriamoci sui dati stessi utilizzando statistiche e visualizzazioni. Il set di dati che utilizziamo è un set di dati di vendita al dettaglio che fornisce informazioni varie su 45 diversi negozi in un dato giorno. Alcune caratteristiche per un dato `date` e `store` includono:
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

È possibile sfruttare la libreria panda [!DNL Python's] per ottenere il tipo di dati di ciascun attributo. L’output della chiamata seguente fornirà informazioni sul numero di voci e sul tipo di dati per ciascuna colonna:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Queste informazioni sono utili in quanto conoscere il tipo di dati di ciascuna colonna ci consentirà di sapere come trattare i dati.

Vediamo ora il riepilogo statistico. Verranno visualizzati solo i tipi di dati numerici, pertanto `date`, `storeType` e `isHoliday` non verranno generati:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

Con questo, possiamo vedere che ci sono 6435 istanze per ogni caratteristica. Vengono inoltre fornite informazioni statistiche quali media, deviazione standard (std), min, max e interquartili. Questo ci fornisce informazioni sulla deviazione per i dati. Nella prossima sezione presenteremo la visualizzazione che funziona insieme a queste informazioni per consentirci di comprendere bene i nostri dati.

Esaminando i valori minimo e massimo per `store`, è possibile notare che sono presenti 45 archivi univoci rappresentati dai dati. Ci sono anche `storeTypes` che differenziano cosa è un archivio. È possibile visualizzare la distribuzione di `storeTypes` eseguendo le operazioni seguenti:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Ciò significa che 22 archivi sono di `storeType` `A`, 17 sono `storeType` `B` e 6 sono `storeType` `C`.

#### Visualizzazione dati

Ora che conosciamo i valori dei nostri frame di dati, vogliamo integrarli con le visualizzazioni per rendere le cose più chiare e più facili da identificare. I grafici sono utili anche per trasmettere i risultati a un pubblico. Alcune librerie [!DNL Python] utili per la visualizzazione includono:
- [Matplotlib](https://matplotlib.org/)
- [panda](https://pandas.pydata.org/)
- [seaborn](https://seaborn.pydata.org/)
- [ggplot](https://ggplot2.tidyverse.org/)

In questa sezione presenteremo rapidamente alcuni vantaggi relativi all’utilizzo di ogni libreria.

[Matplotlib](https://matplotlib.org/) è il pacchetto di visualizzazione [!DNL Python] più vecchio. Il loro obiettivo è quello di rendere &quot;le cose facili e difficili possibili&quot;. Questo tende ad essere vero in quanto il pacchetto è estremamente potente, ma è anche dotato di complessità. Non è sempre facile ottenere un grafico dall’aspetto ragionevole senza richiedere molto tempo e fatica.

[Pandas](https://pandas.pydata.org/) viene utilizzato principalmente per il relativo oggetto DataFrame che consente la manipolazione dei dati con l&#39;indicizzazione integrata. Tuttavia, i panda includono anche una funzionalità di plottaggio incorporata basata su matplotlib.

[seaborn](https://seaborn.pydata.org/) è una build del pacchetto sopra matplotlib. Il suo obiettivo principale è quello di rendere i grafici predefiniti più accattivanti dal punto di vista visivo e semplificare la creazione di grafici complessi.

[ggplot](https://ggplot2.tidyverse.org/) è un pacchetto creato anche sopra matplotlib. Tuttavia la differenza principale è che l&#39;utensile è una porta di ggplot2 per R. Simile al seaborn, l&#39;obiettivo è quello di migliorare su matplotlib. Gli utenti che hanno familiarità con ggplot2 for R devono considerare questa libreria.


##### Univariati, grafici

I grafici univariati sono grafici di una singola variabile. Un comune grafico univariato viene utilizzato per visualizzare i dati sotto forma di grafico a scatola e sussurro.

Utilizzando i nostri set di dati di vendita al dettaglio precedenti, possiamo generare il box e il whisker plot per ciascuno dei 45 negozi e le loro vendite settimanali. Il plot viene generato utilizzando la funzione `seaborn.boxplot`.

![](../images/jupyterlab/analyze-data/box_whisker.png)

Per mostrare la distribuzione dei dati viene utilizzato un grafico a scatola e a baffi. Le linee esterne del plottaggio mostrano i quartili superiore e inferiore, mentre la casella si estende sull&#39;intervallo interquartile. La riga nella casella contrassegna la mediana. Tutti i punti di dati superiori a 1,5 volte il quartile superiore o inferiore sono contrassegnati da un cerchio. Questi punti sono considerati valori anomali.

##### Grafici multivariati

I grafici multivariati vengono utilizzati per visualizzare l’interazione tra le variabili. Con la visualizzazione, i data scientist possono vedere se ci sono correlazioni o pattern tra le variabili. Un comune grafo multivariato utilizzato è una matrice di correlazione. Con una matrice di correlazione, le dipendenze tra più variabili sono quantificate con il coefficiente di correlazione.

Utilizzando lo stesso set di dati di vendita al dettaglio, possiamo generare la matrice di correlazione.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Osservate la diagonale di 1 in basso rispetto al centro. Questo mostra che quando si confronta una variabile con se stessa, ha una correlazione positiva completa. Una correlazione positiva forte avrà una magnitudine più vicina a 1, mentre le correlazioni deboli saranno più vicine a 0. Viene mostrata una correlazione negativa con un coefficiente negativo che mostra una tendenza inversa.


## Passaggi successivi

Questo tutorial illustra come creare un nuovo blocco appunti Jupyter in Data Science Workspace e come accedere ai dati sia esternamente che da [!DNL Adobe Experience Platform]. Nello specifico, abbiamo esaminato i seguenti passaggi:
- Crea un nuovo Jupyter Notebook
- Accedere a set di dati e schemi
- Esplora i set di dati

Ora puoi passare alla [sezione successiva](../models-recipes/package-source-files-recipe.md) per creare un pacchetto di una ricetta e importarla in Data Science Workspace.
