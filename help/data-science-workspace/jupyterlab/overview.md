---
keywords: Experience Platform;JupyterLab;notebook;Data Science Workspace;argomenti popolari;jupyterlab
solution: Experience Platform
title: Panoramica interfaccia JupyterLab
description: JupyterLab è un'interfaccia utente basata sul web per Project Jupyter ed è strettamente integrata in Adobe Experience Platform. Fornisce un ambiente di sviluppo interattivo per consentire ai data scientist di lavorare con Jupyter Notebooks, codice e dati. Questo documento fornisce una panoramica di JupyterLab e delle sue funzionalità, nonché istruzioni per eseguire azioni comuni.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 2%

---

# [!DNL JupyterLab] Panoramica dell’interfaccia utente

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

[!DNL JupyterLab] è un&#39;interfaccia utente basata sul web per [Project Jupyter](https://jupyter.org/) ed è strettamente integrata in Adobe Experience Platform. Fornisce un ambiente di sviluppo interattivo per consentire ai data scientist di lavorare con Jupyter Notebooks, codice e dati.

In questo documento viene fornita una panoramica delle [!DNL JupyterLab] relative funzionalità, nonché istruzioni per eseguire azioni comuni.

## [!DNL JupyterLab] su [!DNL Experience Platform]

L&#39;integrazione di JupyterLab di Experience Platform è accompagnata da modifiche architetturali, considerazioni di progettazione, estensioni personalizzate per notebook, librerie preinstallate e un&#39;interfaccia a tema Adobe Systems.

L’elenco seguente illustra alcune delle funzioni esclusive di JupyterLab su Platform:

| Funzione | Descrizione |
| --- | --- |
| **Kernel** | I kernel forniscono notebook e altri [!DNL JupyterLab] front-end la capacità di eseguire e introspezione codice in diversi linguaggi di programmazione. [!DNL Experience Platform] fornisce kernel aggiuntivi per supportare lo sviluppo in [!DNL Python], R, PySpark e [!DNL Spark]. Vedi la [sezione kernel](#kernels) per maggiori dettagli. |
| **Data accesso** | Accedi ai set di dati esistenti direttamente dall&#39;interno [!DNL JupyterLab] con il supporto completo per le funzionalità di lettura e scrittura. |
| **[!DNL Platform]Integrazione dei servizi** | Le integrazioni incorporate consentono di utilizzare altri servizi [!DNL Platform] direttamente da [!DNL JupyterLab]. Un elenco completo delle integrazioni supportate è fornito nella sezione relativa all&#39;integrazione di [con altri servizi di Platform](#service-integration). |
| **Autenticazione** | Oltre al <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">modello di sicurezza integrato di JupyterLab, ogni interazione tra il applicazione e il Experience Platform, inclusa Platform comunicazione da servizio a servizio, viene crittografata e autenticata tramite l&#39;IMS<a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System]</a></a>. |
| **librerie di sviluppo** | In [!DNL Experience Platform], [!DNL JupyterLab] fornisce librerie preinstallati per [!DNL Python], R e PySpark. Vedere l&#39;appendice [](#supported-libraries) per un elenco completo dei librerie supportati. |
| **Controller libreria** | Quando le librerie preinstallate non sono sufficienti per le tue esigenze, è possibile installare librerie aggiuntive per Python e R e archiviarle temporaneamente in contenitori isolati per mantenere l&#39;integrità di [!DNL Platform] e proteggere i tuoi dati. Vedi la [sezione kernel](#kernels) per maggiori dettagli. |

>[!NOTE]
>
>I librerie aggiuntivi sono disponibili solo per la sessione in cui sono stati installati. È necessario reinstallare eventuali librerie aggiuntivi necessari all&#39;avvio di nuove sessioni.

## Integrazione con altri [!DNL Platform] servizi {#service-integration}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. L&#39;integrazione di [!DNL JupyterLab] in [!DNL Platform] come IDE incorporato consente di interagire con altri servizi [!DNL Platform], consentendo di utilizzare [!DNL Platform] al massimo delle potenzialità. I seguenti servizi [!DNL Platform] sono disponibili in [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Accedi ed esplora i set di dati con funzionalità di lettura e scrittura.
* **[!DNL Query Service]:** Accedere ed esplorare i set di dati utilizzando SQL, riducendo i costi comuni di accesso ai dati quando si gestiscono grandi quantità di dati.
* **[!DNL Sensei ML Framework]:** sviluppo di modelli con la possibilità di addestrare e valutare i dati, nonché creazione di formule con un solo clic.
* **[!DNL Experience Data Model (XDM)]:** La standardizzazione e l&#39;interoperabilità sono concetti chiave di Adobe Experience Platform. [Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en), guidato da un Adobe, è un tentativo di standardizzare i dati sull&#39;esperienza del cliente e definire schemi per la gestione della customer experience.

>[!NOTE]
>
>Alcune integrazioni del servizio [!DNL Platform] in [!DNL JupyterLab] sono limitate a kernel specifici. Per ulteriori informazioni, consulta la sezione su [kernel](#kernels).

## Funzioni principali e operazioni comuni

Le informazioni sulle caratteristiche chiave di [!DNL JupyterLab] e le istruzioni sull&#39;esecuzione di operazioni comuni sono fornite nelle sezioni seguenti:

* [Accedi a JupyterLab](#access-jupyterlab)
* [Interfaccia di JupyterLab](#jupyterlab-interface)
* [Celle di codice](#code-cells)
* [Kernel](#kernels)
* [Sessioni kernel](#kernel-sessions)
* [Modulo di avvio](#launcher)

### Accesso [!DNL JupyterLab] {#access-jupyterlab}

In [Adobe Experience Platform](https://platform.adobe.com), seleziona **[!UICONTROL Blocchi appunti]** dalla colonna di navigazione a sinistra. Attendere il completamento dell&#39;inizializzazione di [!DNL JupyterLab].

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### Interfaccia [!DNL JupyterLab] {#jupyterlab-interface}

L&#39;interfaccia [!DNL JupyterLab] è costituita da una barra dei menu, una barra laterale a sinistra comprimibile e l&#39;area di lavoro principale contenente schede di documenti e attività.

**Barra dei menu**

La barra dei menu nella parte superiore dell&#39;interfaccia include menu di primo livello che espongono le azioni disponibili in [!DNL JupyterLab] con le relative scelte rapide da tastiera:

* **File:** azioni relative a file e directory
* **Modifica:** azioni relative alla modifica di documenti e altre attività
* **Visualizzazione:** azioni che modificano l&#39;aspetto di [!DNL JupyterLab]
* **Esegui:** azioni per l&#39;esecuzione del codice in attività diverse, ad esempio blocchi appunti e console di codice
* **Kernel:** azioni per la gestione dei kernel
* **Tabulazioni:** un elenco di documenti e attività aperti
* **Impostazioni:** impostazioni comuni e impostazioni avanzate editor
* **Guida:** Un elenco di collegamenti alla guida del [!DNL JupyterLab] kernel

**Barra laterale sinistra**

La barra laterale sinistra contiene cliccabile schede che forniscono accesso alle seguenti funzioni:

* **Browser file:** un elenco di documenti e directory dei blocchi appunti salvati
* **Data Explorer:** Sfoglia, accesso ed esplorare set di dati e schemi
* **Kernel e terminali in esecuzione:** un elenco di sessioni attive del kernel e del terminale con la possibilità di terminare
* **Comandi:** un elenco di comandi utili
* **Ispettore celle:** un editor di cella che fornisce accesso agli strumenti e metadati utile per impostare un blocco appunti a scopo di presentazione
* **schede:** un elenco di schede aperte

Seleziona un scheda per esporne le feature oppure fai clic su un scheda espanso per comprimere la barra laterale sinistra, come illustrato di seguito:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Area di lavoro principale**

L&#39;area di lavoro principale consente [!DNL JupyterLab] di organizzare documenti e altre attività in pannelli di schede che possono essere ridimensionati o suddivisi. Trascinate un scheda al centro di un pannello scheda per eseguire la migrazione della scheda. Dividere un pannello trascinando un scheda a sinistra, a destra, in alto o in basso del pannello:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Configurazione GPU e server di memoria in [!DNL Python]/R

In [!DNL JupyterLab] selezionare l&#39;icona a forma di ingranaggio nell&#39;angolo superiore destro per aprire *la configurazione del* server Notebook. È possibile attivare la GPU e allocare la quantità di memoria necessaria utilizzando il cursore. La quantità di memoria che è possibile allocare dipende dalla quantità di provisioning dell&#39;organizzazione. Seleziona **[!UICONTROL Aggiorna]** configurazioni per salvare.

>[!NOTE]
>
>Viene eseguito il provisioning di una sola GPU per organizzazione per i notebook. Se la GPU è in uso, è necessario attendere che l&#39;utente che ha prenotato la GPU la rilasci. Questa operazione può essere eseguita disconnettendosi o lasciando la GPU inattiva per quattro o più ore.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Termina e riavvia [!DNL JupyterLab]

In [!DNL JupyterLab], puoi terminare la sessione per impedire l&#39;utilizzo di ulteriori risorse. Inizia selezionando l&#39;icona di accensione dell&#39;icona **di accensione, quindi seleziona**[!UICONTROL  Spegni ]**dal popover che sembra terminare la sessione.** ![](/help/images/icons/power.png) Le sessioni del blocco appunti terminano automaticamente dopo 12 ore di inattività.

Per riavviare [!DNL JupyterLab], seleziona l&#39;icona ![**di riavvio dell&#39;icona**](/help/images/icons/restart.png) di riavvio situata direttamente a sinistra dell&#39;icona di accensione, quindi seleziona **[!UICONTROL Riavvia]** dal popover visualizzato.

![Terminare JupyterLab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Code celle {#code-cells}

Code celle sono la contenuto principale dei quaderni. Contengono il codice sorgente nel linguaggio del kernel associato del notebook e l&#39;output come risultato dell&#39;esecuzione della cella di codice. A destra di ogni cella di codice che rappresenta l&#39;ordine di esecuzione viene visualizzato un conteggio di esecuzione.

![](../images/jupyterlab/user-guide/code_cell.png)

Le azioni comuni delle celle sono descritte di seguito:

* **Aggiungere una cella:** fare clic sul simbolo più (**+**) dal menu del blocco appunti per aggiungere una cella vuota. Nuovo celle vengono posizionate sotto la cella con cui si sta interagendo o alla fine del quaderno se non è presente alcuna cella particolare in concentrarsi.

* **Spostare una cella:** posiziona il cursore a destra della cella da spostare, quindi fai clic e trascina la cella in una nuova posizione. Inoltre, lo spostamento di una cella da un blocco appunti a un altro replica la cella insieme al relativo contenuto.

* **Eseguire una cella: fare clic sul corpo della cella che si desidera eseguire,** quindi fare clic sull&#39;icona **di riproduzione** (**▶**) dal menu del blocco appunti. Un asterisco (**\***) viene visualizzato nel contatore di esecuzione della cella durante l&#39;elaborazione dell&#39;esecuzione e viene sostituito con un numero intero al termine.

* **Elimina una cella: fai clic sul corpo della cella che desideri eliminare,** quindi fai clic sull&#39;icona **a forma di forbice** .

### Kernel {#kernels}

I kernel per notebook sono i motori di elaborazione specifici per il linguaggio per l&#39;elaborazione di celle per notebook. Oltre a [!DNL Python], [!DNL JupyterLab] fornisce supporto linguistico aggiuntivo in R, PySpark e [!DNL Spark] (Scala). Quando si apre un documento blocco appunti, viene avviato il kernel associato. Quando viene eseguita una cella del notebook, il kernel esegue il calcolo e produce risultati che possono richiedere notevoli risorse di CPU e memoria. Si noti che la memoria allocata non viene liberata fino alla chiusura del kernel.

Alcune caratteristiche e funzionalità sono limitate a particolari kernel come descritto nella tabella seguente:

| Kernel | Supporto per l&#39;installazione della libreria | [!DNL Platform] Integrazioni |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sì | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sì | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | No | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sessioni kernel {#kernel-sessions}

Ogni notebook o attività attiva utilizza [!DNL JupyterLab] una sessione del kernel. Per trovare tutte le sessioni attive, espandi la scheda **Terminali e kernel in esecuzione** dalla barra laterale a sinistra. Il tipo e lo stato del kernel di un notebook possono essere identificati osservando la parte superiore destra dell&#39;interfaccia del notebook. Nel diagramma seguente, il kernel associato al blocco appunti è **[!DNL Python]3** e il suo stato corrente è rappresentato da un cerchio grigio a destra. Un cerchio cavo implica un kernel inattivo e un cerchio solido implica un kernel occupato.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Se il kernel viene arrestato o inattivo per un periodo prolungato, **Nessun kernel!Viene visualizzato** con un cerchio continuo. Attivate un kernel facendo clic sullo stato del kernel e selezionando il tipo di kernel appropriato come mostrato di seguito:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Modulo di avvio {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Il *modulo di avvio* personalizzato fornisce utili modelli di blocco appunti per i kernel supportati, utili per avviare l&#39;attività, tra cui:

| Modello | Descrizione |
| --- | --- |
| Vuoto | Un file del blocco appunti vuoto. |
| Starter | Un notebook precompilato che illustra l&#39;esplorazione dei dati utilizzando dati di esempio. |
| Vendite al dettaglio | Un quaderno precompilato con la ricetta](../pre-built-recipes/retail-sales.md) di vendita al [dettaglio utilizzando dati di esempio. |
| Generatore di ricette | Modello di blocco appunti per la creazione di una composizione in [!DNL JupyterLab]. È precompilata con codice e commento che illustra e descrive il processo di creazione della ricetta. Fare riferimento al blocco appunti per l&#39;esercitazione [](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) delle ricette per una procedura dettagliata |
| [!DNL Query Service] | Un notebook precompilato che illustra l&#39;utilizzo di flussi di [!DNL Query Service] lavoro di esempio forniti direttamente in [!DNL JupyterLab] dotazione, che analizza i dati su larga scala. |
| Eventi XDM | Un notebook precompilato che illustra l&#39;esplorazione dei dati sui dati postvalue dell&#39;evento dell&#39;esperienza, concentrandosi sulle funzionalità comuni a tutta la struttura dei dati. |
| Query XDM | Un blocco appunti precompilato che illustra query aziendali di esempio sui dati degli eventi esperienza. |
| Aggregazione | Un notebook precompilato che illustra i flussi di lavoro di esempio per aggregato grandi quantità di dati in blocchi più piccoli e gestibili. |
| Clustering | Un notebook precompilato che illustra il processo di modellazione end-to-end di Machine Learning utilizzando algoritmi di clustering. |

Alcuni modelli di notebook sono limitati a determinati kernel. La disponibilità dei template per ogni kernel è mappata nella seguente tabella:

<table>
    <tr>
        <td></td>
        <th><strong>Vuoto</strong></th>
        <th><strong>Avviatore</strong></th>
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

Per aprire un nuovo *modulo di avvio*, fare clic su **File > Nuovo modulo di avvio**. In alternativa, espandi il **File browser** dalla barra laterale sinistra e fai clic sul simbolo più (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Passaggi successivi

Per ulteriori informazioni su ciascuno dei notebook supportati e su come usarli, visita la guida per sviluppatori di [accesso](./access-notebook-data.md) dati dei notebook Jupyterlab. Questa guida è incentrata su come utilizzare i notebook JupyterLab per accesso i dati, inclusi lettura, scrittura e query sui dati. La guida accesso dati contiene inoltre informazioni sulla quantità massima di dati che possono essere letti da ogni notebook supportato.

## librerie supportati {#supported-libraries}

Per un elenco dei pacchetti supportati in Python, R e PySpark, copia e incolla `!conda list` in una nuova cella, quindi esegui la cella. Un elenco di pacchetti supportati viene compilato in ordine alfabetico.

![esempio](../images/jupyterlab/user-guide/libraries.PNG)

Inoltre, vengono utilizzate le dipendenze seguenti, ma non elencate:
* CUDA 11.2
* CUDNN 8.1

