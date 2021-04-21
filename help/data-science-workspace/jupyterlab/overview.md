---
keywords: Experience Platform;JupyterLab;notebook;Data Science Workspace;argomenti comuni;jupyterlab
solution: Experience Platform
title: Panoramica dell’interfaccia utente di JupyterLab
topic-legacy: Overview
description: JupyterLab è un’interfaccia utente basata sul Web per Project Jupyter ed è strettamente integrata in Adobe Experience Platform. Offre agli scienziati dei dati un ambiente di sviluppo interattivo per lavorare con i notebook Jupyter, il codice e i dati. Questo documento fornisce una panoramica di JupyterLab e delle sue funzioni, nonché istruzioni per eseguire azioni comuni.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1813'
ht-degree: 3%

---

# [!DNL JupyterLab] Panoramica dell’interfaccia utente

[!DNL JupyterLab] è un’interfaccia utente basata sul Web per  [Project ](https://jupyter.org/) Jupyterand ed è strettamente integrata in Adobe Experience Platform. Offre agli scienziati dei dati un ambiente di sviluppo interattivo per lavorare con i notebook Jupyter, il codice e i dati.

Questo documento fornisce una panoramica di [!DNL JupyterLab] e delle relative funzioni, nonché istruzioni per eseguire le azioni comuni.

## [!DNL JupyterLab] su [!DNL Experience Platform]

L&#39;integrazione JupyterLab di Experience Platform è accompagnata da modifiche architettoniche, considerazioni di progettazione, estensioni personalizzate per i notebook, librerie preinstallate e un&#39;interfaccia a tema Adobe.

L’elenco seguente illustra alcune delle funzioni esclusive di JupyterLab su Platform:

| Funzione | Descrizione |
| --- | --- |
| **Kernel** | I kernel forniscono il blocco appunti e altri [!DNL JupyterLab] front-end la possibilità di eseguire e introdurre il codice in diversi linguaggi di programmazione. [!DNL Experience Platform] fornisce kernel aggiuntivi per supportare lo sviluppo in  [!DNL Python], R, PySpark e  [!DNL Spark]. Per ulteriori informazioni, consulta la sezione [kernel](#kernels) . |
| **Accesso ai dati** | Accedi ai set di dati esistenti direttamente da [!DNL JupyterLab] con il supporto completo per le funzionalità di lettura e scrittura. |
| **[!DNL Platform]integrazione dei servizi** | Le integrazioni integrate consentono di utilizzare altri servizi [!DNL Platform] direttamente da [!DNL JupyterLab]. Un elenco completo delle integrazioni supportate viene fornito nella sezione sull’ [Integrazione con altri servizi Platform](#service-integration). |
| **Autenticazione** | Oltre al <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">modello di sicurezza integrato di JupyterLab</a>, ogni interazione tra l&#39;applicazione e l&#39;Experience Platform, inclusa la comunicazione service-to-service di Platform, viene crittografata e autenticata tramite <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Librerie di Sviluppo** | In [!DNL Experience Platform], [!DNL JupyterLab] fornisce librerie preinstallate per [!DNL Python], R e PySpark. Per un elenco completo delle librerie supportate, consulta l’ [appendice](#supported-libraries) . |
| **Controller libreria** | Se le librerie preinstallate non sono in grado di soddisfare le tue esigenze, è possibile installare librerie aggiuntive per Python e R e archiviarle temporaneamente in contenitori isolati per mantenere l’integrità di [!DNL Platform] e proteggere i tuoi dati. Per ulteriori informazioni, consulta la sezione [kernel](#kernels) . |

>[!NOTE]
>
>Le librerie aggiuntive sono disponibili solo per la sessione in cui sono state installate. Quando avvii nuove sessioni, devi reinstallare tutte le librerie aggiuntive necessarie.

## Integrazione con altri servizi [!DNL Platform] {#service-integration}

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. L’integrazione di [!DNL JupyterLab] su [!DNL Platform] come IDE incorporato consente di interagire con altri servizi [!DNL Platform], consentendoti di utilizzare [!DNL Platform] al massimo del suo potenziale. I seguenti servizi [!DNL Platform] sono disponibili in [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Accedi ed esplora i set di dati con funzionalità di lettura e scrittura.
* **[!DNL Query Service]:** Accedi ed esplora i set di dati utilizzando SQL, fornendo costi generali di accesso ai dati inferiori quando gestisci grandi quantità di dati.
* **[!DNL Sensei ML Framework]:** sviluppo di modelli con la possibilità di addestrare e valutare i dati, nonché creazione di ricette con un solo clic.
* **[!DNL Experience Data Model (XDM)]:** La standardizzazione e l’interoperabilità sono concetti chiave di Adobe Experience Platform. [Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en), basato su un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

>[!NOTE]
>
>Alcune integrazioni di servizi [!DNL Platform] su [!DNL JupyterLab] sono limitate a specifici kernel. Per ulteriori informazioni, consulta la sezione sui [kernel](#kernels) .

## Funzioni principali e operazioni comuni

Le informazioni sulle caratteristiche principali di [!DNL JupyterLab] e le istruzioni sull&#39;esecuzione di operazioni comuni sono fornite nelle sezioni seguenti:

* [Accedere a JupyterLab](#access-jupyterlab)
* [Interfaccia JupyterLab](#jupyterlab-interface)
* [Celle di codice](#code-cells)
* [Kernel](#kernels)
* [Sessioni Kernel](#kernel-sessions)
* [Launcher](#launcher)

### Accedere ad [!DNL JupyterLab] {#access-jupyterlab}

In [Adobe Experience Platform](https://platform.adobe.com), seleziona **[!UICONTROL Notebooks]** dalla colonna di navigazione a sinistra. Consenti l&#39;inizializzazione completa di [!DNL JupyterLab].

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interfaccia {#jupyterlab-interface}

L&#39;interfaccia [!DNL JupyterLab] è costituita da una barra dei menu, una barra laterale sinistra comprimibile e l&#39;area di lavoro principale contenente schede di documenti e attività.

**Barra dei menu**

La barra dei menu nella parte superiore dell’interfaccia dispone di menu di livello principale che espongono le azioni disponibili in [!DNL JupyterLab] con le relative scelte rapide da tastiera:

* **File:** azioni relative a file e directory
* **Modifica:** azioni relative alla modifica di documenti e altre attività
* **Visualizzazione:** azioni che alterano l’aspetto  [!DNL JupyterLab]
* **Esegui:** azioni per l’esecuzione di codice in diverse attività, come blocchi appunti e console di codice
* **Kernel:** azioni per la gestione dei kernel
* **Schede:** Elenco dei documenti e delle attività aperti
* **Impostazioni:** Impostazioni comuni e un editor di impostazioni avanzate
* **Guida:** Elenco dei collegamenti della guida  [!DNL JupyterLab] e del kernel

**Barra laterale sinistra**

La barra laterale sinistra contiene schede selezionabili che consentono di accedere alle seguenti funzioni:

* **Browser file:** elenco dei documenti e delle directory del blocco appunti salvati
* **Data Explorer:** esplorazione, accesso ed esplorazione di set di dati e schemi
* **Canali e terminali in esecuzione:** un elenco di sessioni attive del kernel e dei terminali con la possibilità di terminare
* **Comandi:** elenco di comandi utili
* **Ispettore celle:** editor di celle che consente l&#39;accesso a strumenti e metadati utili per l&#39;impostazione di un blocco appunti a scopo di presentazione
* **schede:** un elenco di schede aperte

Selezionate una scheda per esporne le caratteristiche, oppure selezionate una scheda espansa per comprimere la barra laterale sinistra come illustrato di seguito:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Area di lavoro principale**

L’area di lavoro principale in [!DNL JupyterLab] consente di disporre documenti e altre attività in pannelli di schede che possono essere ridimensionati o suddivisi. Trascina una scheda al centro di un pannello di schede per eseguire la migrazione della scheda. Dividi un pannello trascinando una scheda a sinistra, a destra, in alto o in basso nel pannello:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Configurazione di GPU e server di memoria in [!DNL Python]/R

In [!DNL JupyterLab] seleziona l&#39;icona a forma di ingranaggio nell&#39;angolo in alto a destra per aprire *Configurazione del server appunti*. È possibile attivare la GPU e allocare la quantità di memoria necessaria utilizzando il cursore. La quantità di memoria che è possibile allocare dipende da quanto è stato effettuato il provisioning della tua organizzazione. Selezionare **[!UICONTROL Update configs]** per salvare.

>[!NOTE]
>
>Per i notebook viene fornito un solo GPU per organizzazione. Se la GPU è in uso, è necessario attendere che l&#39;utente che ha attualmente riservato la GPU rilasci. Questo può essere fatto disconnettendo o lasciando la GPU in uno stato di inattività per quattro o più ore.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Termina e riavvia [!DNL JupyterLab]

In [!DNL JupyterLab], puoi terminare la sessione per impedire l’utilizzo di ulteriori risorse. Inizia selezionando l&#39; **icona di alimentazione** ![icona di alimentazione](../images/jupyterlab/user-guide/power_button.png), quindi seleziona **[!UICONTROL Shut Down]** dal puntatore che appare per terminare la sessione. Le sessioni del blocco appunti terminano automaticamente dopo 12 ore di assenza di attività.

Per riavviare [!DNL JupyterLab], selezionare l&#39; **icona di riavvio** ![icona di riavvio](../images/jupyterlab/user-guide/restart_button.png) situata direttamente a sinistra dell&#39;icona di alimentazione, quindi selezionare **[!UICONTROL Restart]** dal puntatore visualizzato.

![terminare jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Celle di codice {#code-cells}

Le celle di codice sono il contenuto principale dei notebook. Contengono codice sorgente nella lingua del kernel associato del blocco appunti e l&#39;output come risultato dell&#39;esecuzione della cella di codice. A destra di ogni cella di codice che rappresenta l’ordine di esecuzione viene visualizzato un conteggio di esecuzione.

![](../images/jupyterlab/user-guide/code_cell.png)

Di seguito sono descritte le azioni comuni della cella:

* **Aggiungi una cella:** fai clic sul simbolo più (**+**) nel menu del blocco appunti per aggiungere una cella vuota. Le nuove celle vengono posizionate sotto la cella con cui si sta interagendo o alla fine del blocco appunti se non è attiva alcuna cella specifica.

* **Sposta una cella:** posizionare il cursore a destra della cella che si desidera spostare, quindi fare clic e trascinare la cella in una nuova posizione. Inoltre, lo spostamento di una cella da un blocco appunti a un altro replica la cella con il relativo contenuto.

* **Esegui una cella:** fai clic sul corpo della cella che desideri eseguire, quindi fai clic sull&#39;icona di  **** riproduzione (**▶**) dal menu del blocco appunti. Un asterisco (**\***) viene visualizzato nel contatore di esecuzione della cella quando il kernel sta elaborando l&#39;esecuzione e viene sostituito con un numero intero al termine.

* **Elimina una cella:** fai clic sul corpo della cella che desideri eliminare, quindi fai clic sull’ **** icona a forma di forbice.

### Kernel {#kernels}

I kernel dei notebook sono motori informatici specifici per la lingua per l&#39;elaborazione delle celle dei notebook. Oltre a [!DNL Python], [!DNL JupyterLab] offre supporto linguistico aggiuntivo in R, PySpark e [!DNL Spark] (Scala). Quando si apre un documento del blocco appunti, viene avviato il kernel associato. Quando viene eseguita una cella del blocco appunti, il kernel esegue il calcolo e produce risultati che possono richiedere notevoli risorse di CPU e memoria. Si noti che la memoria allocata non viene liberata finché il kernel non viene spento.

Alcune caratteristiche e funzionalità sono limitate a particolari kernel come descritto nella tabella seguente:

| Kernel | Supporto per l&#39;installazione della libreria | [!DNL Platform] integrazioni |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sì | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sì | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | No | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sessioni Kernel {#kernel-sessions}

Ogni blocco appunti o attività in [!DNL JupyterLab] utilizza una sessione del kernel. Tutte le sessioni attive si trovano espandendo la scheda **Terminali in esecuzione e kernel** dalla barra laterale sinistra. Il tipo e lo stato del kernel di un notebook possono essere identificati osservando l&#39;interfaccia superiore destra del notebook. Nel diagramma seguente, il kernel associato al notebook è **[!DNL Python]3** e lo stato corrente è rappresentato da un cerchio grigio a destra. Un cerchio cavo implica un kernel inattivo e un cerchio solido implica un kernel occupato.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Se il kernel viene spento o inattivo per un periodo prolungato, allora **Nessun kernel!** viene visualizzato un cerchio pieno. Attivare un kernel facendo clic sullo stato del kernel e selezionando il tipo di kernel appropriato come illustrato di seguito:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Launcher {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Il modulo *Launcher* personalizzato offre utili modelli per i blocchi supportati per avviare in modo più efficace l&#39;attività, tra cui:

| Modello | Descrizione |
| --- | --- |
| Vuoto | Un file di blocco appunti vuoto. |
| Starter | Un blocco appunti precompilato che illustra l&#39;esplorazione dei dati utilizzando dati di esempio. |
| Vendite al dettaglio | Un blocco appunti precompilato con [ricetta vendite al dettaglio](https://adobe.ly/2wOgO3L) utilizzando dati di esempio. |
| Generatore di ricette | Un modello per notebook per la creazione di una ricetta in [!DNL JupyterLab]. È precompilato con codice e commenti che mostrano e descrivono il processo di creazione delle ricette. Per una descrizione dettagliata, fai riferimento al [blocco appunti per l&#39;esercitazione sulle ricette](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en). |
| [!DNL Query Service] | Un blocco appunti precompilato che illustra l&#39;utilizzo di [!DNL Query Service] direttamente in [!DNL JupyterLab] con flussi di lavoro di esempio forniti che analizzano i dati su scala. |
| Eventi XDM | Un blocco appunti precompilato che illustra l&#39;esplorazione dei dati sui dati Experience Event postvalue, concentrandosi sulle funzioni comuni nella struttura dei dati. |
| Query XDM | Un blocco appunti precompilato che illustra query aziendali di esempio sui dati di Experience Event. |
| Aggregazione | Un blocco appunti precompilato che dimostra i flussi di lavoro di esempio per aggregare grandi quantità di dati in blocchi più piccoli e gestibili. |
| Clustering | Un blocco appunti precompilato che illustra il processo di modellazione dell&#39;apprendimento automatico end-to-end utilizzando gli algoritmi di clustering. |

Alcuni modelli di blocco appunti sono limitati a determinati kernel. La disponibilità del modello per ogni kernel è mappata nella seguente tabella:

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

Per aprire un nuovo *Launcher*, fai clic su **File > Nuovo Launcher**. In alternativa, espandi il **Browser file** dalla barra laterale sinistra e fai clic sul simbolo più (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Passaggi successivi

Per ulteriori informazioni su ciascuno dei notebook supportati e su come utilizzarli, visita la guida per gli sviluppatori [Jupyterlab data access](./access-notebook-data.md) . Questa guida si concentra su come utilizzare i notebook JupyterLab per accedere ai tuoi dati, compresi la lettura, la scrittura e la query dei dati. La guida all&#39;accesso ai dati contiene inoltre informazioni sulla quantità massima di dati leggibile da ciascun blocco appunti supportato.

## Librerie supportate {#supported-libraries}

Per un elenco dei pacchetti supportati in Python, R e PySpark, copia e incolla `!pip list --format=columns` in una nuova cella, quindi esegui la cella. Un elenco di pacchetti supportati viene compilato in ordine alfabetico.

![esempio](../images/jupyterlab/user-guide/libraries.PNG)
