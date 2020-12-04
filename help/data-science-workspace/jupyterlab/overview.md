---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: Guida utente di JupyterLab
topic: Overview
description: JupyterLab è un'interfaccia utente basata sul Web per Project Jupyter ed è strettamente integrata in Adobe Experience Platform. Fornisce un ambiente di sviluppo interattivo che consente agli scienziati dei dati di lavorare con notebook, codice e dati Jupyter. Questo documento fornisce una panoramica di JupyterLab e delle sue funzioni, oltre alle istruzioni per eseguire azioni comuni.
translation-type: tm+mt
source-git-commit: d5e7679ac41fd476c77a98920d7f7aeaefacec6d
workflow-type: tm+mt
source-wordcount: '1938'
ht-degree: 9%

---


# [!DNL JupyterLab] guida utente

[!DNL JupyterLab] è un&#39;interfaccia utente basata sul Web per [Project Jupyter](https://jupyter.org/) ed è strettamente integrata in Adobe Experience Platform. Fornisce un ambiente di sviluppo interattivo che consente agli scienziati dei dati di lavorare con notebook, codice e dati Jupyter.

Questo documento fornisce una panoramica delle funzioni [!DNL JupyterLab] e delle istruzioni per eseguire azioni comuni.

## [!DNL JupyterLab] su [!DNL Experience Platform]

&#39;integrazione  JupyterLab è accompagnata da modifiche architettoniche, considerazioni di progettazione, estensioni personalizzate dei notebook, librerie preinstallate e un&#39;interfaccia  a tema Adobe.

L&#39;elenco seguente illustra alcune delle funzioni esclusive di JupyterLab sulla piattaforma:

| Funzione | Descrizione |
| --- | --- |
| **Kernel** | I kernel forniscono ai notebook e agli altri [!DNL JupyterLab] front-end la possibilità di eseguire e analizzare il codice in diversi linguaggi di programmazione. [!DNL Experience Platform] fornisce ulteriori kernel per supportare lo sviluppo in [!DNL Python], R, PySpark e [!DNL Spark]. Per ulteriori dettagli, consulta la sezione [kernel](#kernels) . |
| **Accesso ai dati** | Accedete ai set di dati esistenti direttamente dall&#39;interno [!DNL JupyterLab] con il supporto completo delle funzionalità di lettura e scrittura. |
| **[!DNL Platform]integrazione dei servizi** | Le integrazioni integrate consentono di utilizzare altri [!DNL Platform] servizi direttamente dall&#39;interno [!DNL JupyterLab]. Un elenco completo delle integrazioni supportate è disponibile nella sezione [Integrazione con altri servizi](#service-integration)della piattaforma. |
| **Autenticazione** | Oltre al modello <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">di sicurezza integrato di</a>JupyterLab, ogni interazione tra l&#39;applicazione e  Experience Platform, inclusa la comunicazione tra servizi della piattaforma, viene crittografata e autenticata tramite <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Librerie di Sviluppo** | In [!DNL Experience Platform], [!DNL JupyterLab] fornisce librerie preinstallate per [!DNL Python], R e PySpark. Consultate l&#39; [appendice](#supported-libraries) per un elenco completo delle librerie supportate. |
| **Controller libreria** | Se le librerie preinstallate non sono adatte alle vostre esigenze, è possibile installare librerie aggiuntive per Python e R e memorizzare temporaneamente in contenitori isolati per mantenere l&#39;integrità dei dati [!DNL Platform] e mantenerli al sicuro. Per ulteriori dettagli, consulta la sezione [kernel](#kernels) . |

>[!NOTE]
>
>Le librerie aggiuntive sono disponibili solo per la sessione in cui sono state installate. È necessario reinstallare tutte le librerie aggiuntive necessarie all&#39;avvio delle nuove sessioni.

## Integrazione con altri [!DNL Platform] servizi {#service-integration}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. L&#39;integrazione di [!DNL JupyterLab] on [!DNL Platform] come IDE integrato consente di interagire con altri [!DNL Platform] servizi, consentendo di sfruttare [!DNL Platform] al massimo il suo potenziale. I seguenti [!DNL Platform] servizi sono disponibili in [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Accesso ed esplorazione di set di dati con funzionalità di lettura e scrittura.
* **[!DNL Query Service]:** Accesso ed esplorazione di dataset utilizzando SQL, fornendo costi generali di accesso ai dati inferiori quando si tratta di grandi quantità di dati.
* **[!DNL Sensei ML Framework]:** Sviluppo di modelli con la capacità di formare e valutare i dati, nonché creazione di ricette con un solo clic.
* **[!DNL Experience Data Model (XDM)]:** Standardizzazione e interoperabilità sono concetti chiave di Adobe Experience Platform. [Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en), guidato da  Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

>[!NOTE]
>
>Alcune integrazioni [!DNL Platform] di servizio [!DNL JupyterLab] sono limitate a specifici kernel. Per ulteriori informazioni, consulta la sezione sui [kernel](#kernels) .

## Funzioni principali e operazioni comuni

Le informazioni relative alle caratteristiche chiave di [!DNL JupyterLab] e le istruzioni sull&#39;esecuzione di operazioni comuni sono fornite nelle sezioni seguenti:

* [Access JupyterLab](#access-jupyterlab)
* [Interfaccia JupyterLab](#jupyterlab-interface)
* [Celle di codice](#code-cells)
* [Kernel](#kernels)
* [Sessioni kernel](#kernel-sessions)
* [Launcher](#launcher)

### Accedere ad [!DNL JupyterLab] {#access-jupyterlab}

In [Adobe Experience Platform](https://platform.adobe.com), selezionate **Blocco note** dalla colonna di navigazione a sinistra. Consentire un po&#39; di tempo per [!DNL JupyterLab] l&#39;inizializzazione completa.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interfaccia {#jupyterlab-interface}

L&#39; [!DNL JupyterLab] interfaccia è composta da una barra dei menu, una barra laterale sinistra comprimibile e l&#39;area di lavoro principale contenente schede di documenti e attività.

**Barra dei menu**

Nella barra dei menu nella parte superiore dell&#39;interfaccia sono disponibili menu di livello principale che mostrano le azioni disponibili tramite [!DNL JupyterLab] le relative scelte rapide da tastiera:

* **File:** Azioni relative a file e directory
* **Modifica:** Azioni relative alla modifica di documenti e altre attività
* **Visualizza:** Azioni che modificano l’aspetto [!DNL JupyterLab]
* **Esegui:** Azioni per l’esecuzione di codice in diverse attività, ad esempio blocchi appunti e console di codice
* **Kernel:** Azioni per la gestione dei kernel
* **Schede:** Elenco di documenti e attività aperti
* **Impostazioni:** Impostazioni comuni e un editor di impostazioni avanzato
* **Aiuto:** Elenco di collegamenti della guida [!DNL JupyterLab] e del kernel

**Barra laterale sinistra**

La barra laterale sinistra contiene schede selezionabili che consentono di accedere alle seguenti funzioni:

* **Browser file:** Elenco dei documenti e delle directory del blocco appunti salvati
* **Esploratore dati:** Sfogliare, accedere ed esplorare dataset e schemi
* **Canali e terminali in esecuzione:** Un elenco di sessioni attive del kernel e del terminale con la possibilità di terminare
* **Comandi:** Un elenco di comandi utili
* **Controllo celle:** Editor di celle che consente di accedere a strumenti e metadati utili per impostare un blocco appunti a scopo di presentazione
* **schede:** Un elenco di schede aperte

Fate clic su una scheda per visualizzarne le caratteristiche, oppure fate clic su una scheda espansa per comprimere la barra laterale sinistra come illustrato di seguito:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Area di lavoro principale**

L&#39;area di lavoro principale in [!DNL JupyterLab] consente di disporre documenti e altre attività in pannelli di schede che possono essere ridimensionati o suddivisi in due parti. Trascinare una scheda al centro di un pannello di tabulazione per migrare la scheda. Per dividere un pannello, trascinate una scheda a sinistra, a destra, in alto o in basso nel pannello:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Celle di codice {#code-cells}

Le celle di codice sono il contenuto principale dei blocchi appunti. Contengono codice sorgente nella lingua del kernel associato al notebook e l&#39;output come risultato dell&#39;esecuzione della cella di codice. Viene visualizzato un conteggio di esecuzione a destra di ogni cella di codice che rappresenta il relativo ordine di esecuzione.

![](../images/jupyterlab/user-guide/code_cell.png)

Di seguito sono descritte le azioni comuni delle celle:

* **Aggiungere una cella:** Fare clic sul simbolo più (**+**) dal menu del blocco appunti per aggiungere una cella vuota. Le nuove celle vengono posizionate sotto la cella con la quale è in corso l&#39;interazione oppure alla fine del blocco appunti, se non è attiva alcuna cella particolare.

* **Spostare una cella:** Posizionare il cursore a destra della cella che si desidera spostare, quindi fare clic e trascinare la cella in una nuova posizione. Inoltre, lo spostamento di una cella da un blocco appunti a un altro replica la cella con il relativo contenuto.

* **Eseguire una cella:** Fare clic sul corpo della cella che si desidera eseguire, quindi fare clic sull&#39;icona di **riproduzione** (**▶**) dal menu del blocco appunti. Un asterisco (**\***) viene visualizzato nel contatore di esecuzione della cella quando il kernel sta elaborando l&#39;esecuzione e viene sostituito con un numero intero al termine.

* **Eliminare una cella:** Fare clic sul corpo della cella che si desidera eliminare, quindi fare clic sull&#39;icona **forbici** .

### Kernel {#kernels}

I kernel per notebook sono i motori informatici specifici per la lingua per l&#39;elaborazione delle celle per notebook. Oltre a [!DNL Python], [!DNL JupyterLab] fornisce supporto linguistico aggiuntivo in R, PySpark e [!DNL Spark] (Scala). Quando si apre un documento del blocco appunti, viene avviato il kernel associato. Quando viene eseguita una cella del blocco appunti, il kernel esegue il calcolo e produce risultati che possono richiedere notevoli risorse di CPU e di memoria. Tenere presente che la memoria allocata non viene liberata fino alla chiusura del kernel.

Alcune caratteristiche e funzionalità sono limitate a specifici kernel come descritto nella tabella seguente:

| Kernel | Supporto per l&#39;installazione della libreria | [!DNL Platform] integrazioni |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sì | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sì | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | No | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sessioni kernel {#kernel-sessions}

Ogni blocco appunti o attività attiva [!DNL JupyterLab] utilizza una sessione del kernel. Tutte le sessioni attive si trovano espandendo la scheda Terminali **in esecuzione e kernel** dalla barra laterale sinistra. Il tipo e lo stato del kernel di un notebook possono essere identificati osservando l&#39;interfaccia superiore destra del notebook. Nel diagramma seguente, il kernel associato al notebook è **[!DNL Python]3** e lo stato corrente è rappresentato da un cerchio grigio a destra. Un cerchio vuoto implica un kernel inattivo e un cerchio pieno implica un kernel occupato.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Se il kernel è spento o inattivo per un periodo prolungato, allora **nessun kernel!** con un cerchio pieno viene visualizzato. Attivate un kernel facendo clic sullo stato del kernel e selezionando il tipo di kernel appropriato come mostrato di seguito:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Launcher {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Il modulo *Launcher* personalizzato offre utili modelli per notebook per i kernel supportati, che consentono di avviare rapidamente l&#39;attività, tra cui:

| Modello | Descrizione |
| --- | --- |
| Vuoto | Un file di blocco appunti vuoto. |
| Starter | Un blocco appunti precompilato che illustra l&#39;esplorazione dei dati utilizzando dati di esempio. |
| Vendite al dettaglio | Un blocco appunti precompilato con la ricetta [di vendita al](https://adobe.ly/2wOgO3L) dettaglio utilizzando dati di esempio. |
| Generatore di ricette | Un modello per notebook per la creazione di una ricetta in [!DNL JupyterLab]. È precompilato con codice e commenti che mostrano e descrivono il processo di creazione delle ricette. Per informazioni dettagliate, fare riferimento al [notebook per l&#39;esercitazione](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) sulle ricette. |
| [!DNL Query Service] | Un notebook precompilato che illustra l’utilizzo [!DNL Query Service] diretto di [!DNL JupyterLab] con flussi di lavoro di esempio forniti che analizza i dati in scala. |
| Eventi XDM | Un blocco appunti precompilato che illustra l&#39;esplorazione dei dati relativi ai dati degli eventi di post-valore, con particolare attenzione alle funzioni comuni all&#39;intera struttura di dati. |
| Query XDM | Un blocco appunti precompilato che illustra le query aziendali di esempio sui dati dell&#39;evento esperienza. |
| Aggregazione | Un notebook precompilato che illustra i flussi di lavoro campione per aggregare grandi quantità di dati in blocchi più piccoli e gestibili. |
| Clustering | Un blocco appunti precompilato che illustra il processo di modellazione end-to-end dell&#39;apprendimento automatico utilizzando gli algoritmi di clustering. |

Alcuni modelli per notebook sono limitati a determinati kernel. La disponibilità del modello per ciascun kernel è mappata nella seguente tabella:

<table>
    <tr>
        <td></td>
        <th><strong>Vuoto</strong></th>
        <th><strong>Starter</strong></th>
        <th><strong>Vendite al dettaglio</strong></th>
        <th><strong>Generatore di ricette</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>Eventi XDM</strong></th>
        <th><strong>Query XDM</strong></th>
        <th><strong>Aggregazione</strong></th>
        <th><strong>Clustering</strong></th>
    </tr>
    <tr>
        <th><strong>[!DNL Python]</strong></th>
        <td >sì</td>
        <td >sì</td>
        <td >sì</td>
        <td >sì</td>
        <td >sì</td>
        <td >sì</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >sì</td>
        <td >sì</td>
        <td >sì</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3 ([!DNL Spark] 2.4)</strong></th>
        <td >no</td>
        <td >sì</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >sì</td>
        <td >sì</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>Scala</strong></th>
        <td >sì</td>
        <td >sì</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >sì</td>
    </tr>
</table>

Per aprire un nuovo *avvio*, fai clic su **File > Nuovo avvio**. In alternativa, espandete il browser **** File dalla barra laterale sinistra e fate clic sul simbolo più (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

### Configurazione di GPU e server di memoria in [!DNL Python]/R

Nell&#39; [!DNL JupyterLab] angolo superiore destro selezionate l&#39;icona a forma di ingranaggio per aprire la configurazione *del server* Notebook. È possibile attivare la GPU e allocare la quantità di memoria necessaria utilizzando il cursore. La quantità di memoria che è possibile allocare dipende dalla quantità di provisioning dell&#39;organizzazione. Selezionare **[!UICONTROL Update configs]** per salvare.

>[!NOTE]
>
>Per i notebook viene fornita una sola GPU per organizzazione. Se la GPU è in uso, è necessario attendere che l&#39;utente che ha attualmente riservato la GPU la rilasci. A questo scopo, disconnettetevi o uscite dalla GPU in uno stato di inattività per quattro o più ore.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## Passaggi successivi

Per ulteriori informazioni su ciascuno dei notebook supportati e su come utilizzarli, visitare la guida per gli sviluppatori di accesso [ai dati dei notebook](./access-notebook-data.md) Jupyterlab. Questa guida è incentrata su come utilizzare i notebook JupyterLab per accedere ai dati, inclusi lettura, scrittura e query. La guida all&#39;accesso ai dati contiene inoltre informazioni sulla quantità massima di dati leggibile da ciascun blocco appunti supportato.

## Librerie supportate {#supported-libraries}

### [!DNL Python] / R

| Libreria | Versione |
| :------ | :------ |
| notebook | 6.0.0 |
| requests | 2.22.0 |
| plotly | 4.0.0 |
| folium | 0.10.0 |
| ipywidgets | 7.5.1 |
| bokeh | 1.3.1 |
| gensim | 3.7.3 |
| ipyparallelo | 0.5.2 |
| jq | 1.6 |
| cheras | 2.2.4 |
| nltk | 3.2.5 |
| panda | 0.22.0 |
| pandasql | 0.7.3 |
| cuscino | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0.21.3 |
| sciolto | 1.3.0 |
| grassa | 1.3.0 |
| marinaio | 0.9.0 |
| statsmodels | 0.10.1 |
| elastico | 5.1.0.17 |
| ggplot | 0.11.5 |
| py xgipplo | 0.90 |
| opencv | 3.4.1 |
| pyspark | 2.4.3 |
| torcia | 1.0.1 |
| wxpitone | 4.0.6 |
| colorante | 0.3.0 |
| geopandas | 0.5.1 |
| pirata | 2.1.0 |
| sagomato | 1.6.4 |
| rpy2 | 2.9.4 |
| r-Essentials | 3.6 |
| aruli | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-gtopics | 4.2.0 |
| r-gvis | 0.4.4 |
| r-igrafo | 1.2.4.1 |
| giri | 3.0 |
| ri-manipolare | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| r-sopravvivenza | 2.44_1.1 |
| r-zoo | 1.8_6 |
| r-stringdist | 0.9.5.2 |
| quadrante r | 1.5_7 |
| r-rjson | 0.2.20 |
| r-previsione | 8.7 |
| r-rsolnp | 1.16 |
| reticolare | 1.12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| raccordo | 0.84 |
| r-fnn | 1.1.3 |
| r-lubridato | 1.7.4 |
| r-randomForest | 4.6_14 |
| r-tidyverse | 1.2.1 |
| r-tree | 1.0_39 |
| pymongo | 3.8.0 |
| freccia | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| parquet | 0.3.2 |
| pitone | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| graphviz | 2.40.1 |
| pitone-grafviz | 0.11.1 |
| stoccaggio di azzurro | 0.36.0 |
| [!DNL jupyterlab] | 1.0.4 |
| pandas_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| beffa | 3.0.5 |
| ipympl | 0.3.3 |
| fonts-anacond | 1,0 |
| psycopg2 | 2.8.3 |
| naso | 1.3.7 |
| autovwidget | 0.12.9 |
| altair | 3.1.0 |
| vega_datasets | 0.7.0 |
| cartiere | 1.0.1 |
| sql_magic | 0.0.4 |
| iso3166 | 1,0 |
| nbimporter | 0.3.1 |

### PySpark

| Libreria | Versione |
| :------ | :------ |
| requests | 2.18.4 |
| gensim | 2.3.0 |
| cheras | 2.0.6 |
| nltk | 3.2.4 |
| panda | 0.20.1 |
| pandasql | 0.7.3 |
| cuscino | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| sciolto | 0.19.1 |
| grassa | 1.3.3 |
| statsmodels | 0.8.0 |
| elastico | 4.0.30.44 |
| py xgipplo | 0.60 |
| opencv | 3.1.0 |
| freccia | 0.8.0 |
| boto3 | 1.5.18 |
| azure-storage-blob | 1.4.0 |
| [!DNL python] | 3.6.7 |
| mkl-rt | 11.1 |