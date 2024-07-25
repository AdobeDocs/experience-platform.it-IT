---
keywords: Experience Platform;JupyterLab;notebook;Data Science Workspace;argomenti popolari;jupyterlab
solution: Experience Platform
title: Panoramica dell’interfaccia utente di JupyterLab
description: JupyterLab è un’interfaccia utente basata su web per Project Jupyter ed è strettamente integrata in Adobe Experience Platform. Fornisce un ambiente di sviluppo interattivo per consentire ai data scientist di lavorare con Jupyter Notebooks, codice e dati. Questo documento fornisce una panoramica di JupyterLab e delle sue funzioni, nonché istruzioni per eseguire azioni comuni.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 2%

---

# [!DNL JupyterLab] Panoramica dell’interfaccia utente

[!DNL JupyterLab] è un&#39;interfaccia utente basata sul Web per [Project Jupyter](https://jupyter.org/) ed è strettamente integrata in Adobe Experience Platform. Fornisce un ambiente di sviluppo interattivo per consentire ai data scientist di lavorare con Jupyter Notebooks, codice e dati.

In questo documento viene fornita una panoramica di [!DNL JupyterLab] e delle relative caratteristiche, nonché istruzioni per l&#39;esecuzione di azioni comuni.

## [!DNL JupyterLab] il [!DNL Experience Platform]

L&#39;integrazione di Experience Platform con JupyterLab è accompagnata da modifiche architetturali, considerazioni di progettazione, estensioni per notebook personalizzate, librerie preinstallate e un&#39;interfaccia a tema Adobe.

L’elenco seguente illustra alcune delle funzioni esclusive di JupyterLab su Platform:

| Funzione | Descrizione |
| --- | --- |
| **Kernel** | I kernel forniscono al blocco appunti e ad altri front-end [!DNL JupyterLab] la possibilità di eseguire e introdurre il codice in diversi linguaggi di programmazione. [!DNL Experience Platform] fornisce kernel aggiuntivi per supportare lo sviluppo in [!DNL Python], R, PySpark e [!DNL Spark]. Per ulteriori dettagli, consulta la sezione [kernel](#kernels). |
| **Accesso ai dati** | Accedere ai set di dati esistenti direttamente da [!DNL JupyterLab] con il supporto completo per le funzionalità di lettura e scrittura. |
| Integrazione del servizio **[!DNL Platform]** | Le integrazioni incorporate consentono di utilizzare altri servizi [!DNL Platform] direttamente da [!DNL JupyterLab]. Un elenco completo delle integrazioni supportate è fornito nella sezione relativa all&#39;integrazione di [con altri servizi di Platform](#service-integration). |
| **Autenticazione** | Oltre al modello di sicurezza integrato di <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">JupyterLab</a>, tutte le interazioni tra l&#39;applicazione e Experience Platform, inclusa la comunicazione da servizio a servizio di Platform, vengono crittografate e autenticate tramite <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Librerie di sviluppo** | In [!DNL Experience Platform], [!DNL JupyterLab] fornisce librerie preinstallate per [!DNL Python], R e PySpark. Per un elenco completo delle librerie supportate, consulta l&#39;[appendice](#supported-libraries). |
| **Controller libreria** | Quando le librerie preinstallate non sono sufficienti per le tue esigenze, è possibile installare librerie aggiuntive per Python e R e archiviarle temporaneamente in contenitori isolati per mantenere l&#39;integrità di [!DNL Platform] e proteggere i tuoi dati. Per ulteriori dettagli, consulta la sezione [kernel](#kernels). |

>[!NOTE]
>
>Le librerie aggiuntive sono disponibili solo per la sessione in cui sono state installate. È necessario reinstallare tutte le librerie aggiuntive necessarie all&#39;avvio di nuove sessioni.

## Integrazione con altri servizi [!DNL Platform] {#service-integration}

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
* [Interfaccia JupyterLab](#jupyterlab-interface)
* [Celle di codice](#code-cells)
* [Kernel](#kernels)
* [Sessioni kernel](#kernel-sessions)
* [Modulo di avvio](#launcher)

### Accedi a [!DNL JupyterLab] {#access-jupyterlab}

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
* **Schede:** un elenco di documenti e attività aperti
* **Impostazioni:** Impostazioni comuni e un editor di impostazioni avanzate
* **Guida:** Un elenco di [!DNL JupyterLab] e collegamenti della Guida del kernel

**Barra laterale a sinistra**

La barra laterale a sinistra contiene schede selezionabili che consentono di accedere alle seguenti funzioni:

* **Browser file:** un elenco di documenti e directory dei blocchi appunti salvati
* **Esplora dati:** Sfogliare, accedere ed esplorare set di dati e schemi
* **Kernel e terminali in esecuzione:** Un elenco di sessioni attive del kernel e del terminale con la possibilità di terminare
* **Comandi:** Elenco di comandi utili
* **Ispettore celle:** editor di celle che consente di accedere a strumenti e metadati utili per la configurazione di un blocco appunti a scopo di presentazione
* **schede:** un elenco di schede aperte

Seleziona una scheda per esporne le funzioni o fai clic su una scheda espansa per comprimere la barra laterale a sinistra, come illustrato di seguito:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Area di lavoro principale**

L&#39;area di lavoro principale in [!DNL JupyterLab] consente di disporre documenti e altre attività in pannelli di schede che possono essere ridimensionati o suddivisi. Trascinare una scheda al centro di un pannello di tabulazione per migrare la scheda. Dividi un pannello trascinando una scheda a sinistra, a destra, in alto o in basso nel pannello:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Configurazione della GPU e del server di memoria in [!DNL Python]/R

In [!DNL JupyterLab] selezionare l&#39;icona a forma di ingranaggio nell&#39;angolo superiore destro per aprire *Configurazione server notebook*. È possibile attivare la GPU e allocare la quantità di memoria necessaria utilizzando il dispositivo di scorrimento. La quantità di memoria che è possibile allocare dipende da quanto è stato eseguito il provisioning dell’organizzazione. Seleziona **[!UICONTROL Aggiorna configurazioni]** da salvare.

>[!NOTE]
>
>Per i notebook viene eseguito il provisioning di una sola GPU per organizzazione. Se la GPU è in uso, è necessario attendere che l&#39;utente che ha prenotato la GPU la rilasci. Questa operazione può essere eseguita disconnettendosi o lasciando la GPU inattiva per quattro o più ore.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Termina e riavvia [!DNL JupyterLab]

In [!DNL JupyterLab], puoi terminare la sessione per impedire l&#39;utilizzo di ulteriori risorse. Iniziare selezionando l&#39;**icona di alimentazione** ![icona di alimentazione](/help/images/icons/power.png), quindi selezionare **[!UICONTROL Chiudi sessione]** dal popover che sembra terminare la sessione. Le sessioni del notebook terminano automaticamente dopo 12 ore di assenza di attività.

Per riavviare [!DNL JupyterLab], selezionare l&#39;icona **riavvia** ![riavvia icona](/help/images/icons/restart.png) situata direttamente a sinistra dell&#39;icona di alimentazione, quindi selezionare **[!UICONTROL Riavvia]** dal popover visualizzato.

![termina jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Celle di codice {#code-cells}

Le celle di codice sono il contenuto principale dei notebook. Contengono codice sorgente nel linguaggio del kernel associato al blocco appunti e l&#39;output risultante dall&#39;esecuzione della cella del codice. A destra di ogni cella di codice che rappresenta l&#39;ordine di esecuzione viene visualizzato un conteggio di esecuzione.

![](../images/jupyterlab/user-guide/code_cell.png)

Le azioni comuni delle celle sono descritte di seguito:

* **Aggiungi cella:** Per aggiungere una cella vuota, fare clic sul simbolo più (**+**) nel menu del blocco appunti. Le nuove celle vengono posizionate sotto la cella con cui si sta interagendo o alla fine del blocco appunti se non è attiva alcuna cella particolare.

* **Spostare una cella:** Posizionare il cursore a destra della cella che si desidera spostare, quindi fare clic e trascinare la cella in una nuova posizione. Inoltre, se si sposta una cella da un blocco appunti a un altro, la cella viene replicata insieme al relativo contenuto.

* **Esegui una cella:** Fare clic sul corpo della cella che si desidera eseguire, quindi fare clic sull&#39;icona **Riproduci** (**▶**) nel menu del blocco appunti. Un asterisco (**\***) viene visualizzato nel contatore di esecuzione della cella durante l&#39;elaborazione dell&#39;esecuzione e viene sostituito con un numero intero al termine.

* **Eliminare una cella:** Fare clic sul corpo della cella che si desidera eliminare, quindi fare clic sull&#39;icona **forbice**.

### Kernel {#kernels}

I kernel per notebook sono i motori di elaborazione specifici per il linguaggio per l&#39;elaborazione di celle per notebook. Oltre a [!DNL Python], [!DNL JupyterLab] fornisce supporto linguistico aggiuntivo in R, PySpark e [!DNL Spark] (Scala). Quando si apre un documento blocco appunti, viene avviato il kernel associato. Quando viene eseguita una cella del notebook, il kernel esegue il calcolo e produce risultati che possono richiedere notevoli risorse di CPU e memoria. Si noti che la memoria allocata non viene liberata fino alla chiusura del kernel.

Alcune caratteristiche e funzionalità sono limitate a determinati kernel come descritto nella tabella seguente:

| Kernel | Supporto per l&#39;installazione della libreria | [!DNL Platform] integrazioni |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sì | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sì | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | No | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sessioni kernel {#kernel-sessions}

Ogni blocco appunti o attività attiva in [!DNL JupyterLab] utilizza una sessione kernel. Per trovare tutte le sessioni attive, espandi la scheda **Terminali e kernel in esecuzione** dalla barra laterale a sinistra. Il tipo e lo stato del kernel di un notebook possono essere identificati osservando la parte superiore destra dell&#39;interfaccia del notebook. Nel diagramma seguente, il kernel associato al blocco appunti è **[!DNL Python]3** e il suo stato corrente è rappresentato da un cerchio grigio a destra. Un cerchio cavo implica un kernel inattivo e un cerchio solido implica un kernel occupato.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Se il kernel viene arrestato o inattivo per un periodo prolungato, **Nessun kernel!Viene visualizzato** con un cerchio continuo. Attivate un kernel facendo clic sullo stato del kernel e selezionando il tipo di kernel appropriato come mostrato di seguito:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Modulo di avvio {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Il *modulo di avvio* personalizzato fornisce utili modelli di blocco appunti per i kernel supportati, utili per avviare l&#39;attività, tra cui:

| Modello | Descrizione |
| --- | --- |
| Vuoto | Un file del blocco appunti vuoto. |
| Starter | Un notebook precompilato che illustra l’esplorazione dei dati utilizzando dati di esempio. |
| Vendite al dettaglio | Un notebook precompilato con [ricetta per la vendita al dettaglio](../pre-built-recipes/retail-sales.md) utilizzando dati di esempio. |
| Generatore di ricette | Modello di blocco appunti per la creazione di una composizione in [!DNL JupyterLab]. È precompilata con codice e commento che illustra e descrive il processo di creazione della ricetta. Per informazioni dettagliate, consulta il [blocco appunti per l&#39;esercitazione sulla ricetta](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en). |
| [!DNL Query Service] | Un blocco appunti precompilato che illustra l&#39;utilizzo di [!DNL Query Service] direttamente in [!DNL JupyterLab] con flussi di lavoro di esempio forniti che analizza i dati su larga scala. |
| Eventi XDM | Un blocco appunti precompilato che illustra l’esplorazione dei dati sui dati post-valore di Experience Event, concentrandosi sulle funzioni comuni all’intera struttura di dati. |
| Query XDM | Un blocco appunti precompilato che illustra query di business di esempio sui dati di Experience Event. |
| Aggregazione | Un notebook precompilato che illustra flussi di lavoro di esempio per aggregare grandi quantità di dati in blocchi più piccoli e gestibili. |
| Clustering | Un notebook precompilato che illustra il processo di modellazione dell’apprendimento automatico end-to-end tramite algoritmi di clustering. |

Alcuni modelli di notebook sono limitati a determinati kernel. La disponibilità del modello per ciascun kernel è mappata nella tabella seguente:

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

Per aprire un nuovo *modulo di avvio*, fare clic su **File > Nuovo modulo di avvio**. In alternativa, espandere **Browser file** dalla barra laterale sinistra e fare clic sul simbolo più (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Passaggi successivi

Per ulteriori informazioni su ciascuno dei notebook supportati e su come utilizzarli, consulta la [Guida per gli sviluppatori di Jupyterlab per l&#39;accesso ai dati dei notebook](./access-notebook-data.md). Questa guida illustra come utilizzare i notebook JupyterLab per accedere ai dati, incluse le operazioni di lettura, scrittura e query. La guida all&#39;accesso ai dati contiene inoltre informazioni sulla quantità massima di dati che può essere letta da ogni blocco appunti supportato.

## Librerie supportate {#supported-libraries}

Per un elenco dei pacchetti supportati in Python, R e PySpark, copiare e incollare `!conda list` in una nuova cella, quindi eseguire la cella. Un elenco di pacchetti supportati viene compilato in ordine alfabetico.

![esempio](../images/jupyterlab/user-guide/libraries.PNG)

Inoltre, vengono utilizzate le dipendenze seguenti, ma non elencate:
* CUDA 11,2
* CUDNN 8.1

