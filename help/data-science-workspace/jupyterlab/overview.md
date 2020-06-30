---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Guida utente di JupyterLab
topic: Overview
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '3645'
ht-degree: 11%

---


# [!DNL JupyterLab] guida utente

[!DNL JupyterLab] è un&#39;interfaccia utente basata sul Web per <a href="https://jupyter.org/" target="_blank">Project Jupyter</a> ed è strettamente integrata in [!DNL Adobe Experience Platform]. Fornisce un ambiente di sviluppo interattivo che consente agli scienziati dei dati di lavorare con notebook, codice e dati Jupyter.

Questo documento fornisce una panoramica delle funzioni [!DNL JupyterLab] e delle istruzioni per eseguire azioni comuni.

## [!DNL JupyterLab] su [!DNL Experience Platform]

&#39;integrazione di Experience Platform JupyterLab è accompagnata da modifiche architettoniche, considerazioni di progettazione, estensioni personalizzate dei notebook, librerie preinstallate e un&#39;interfaccia a tema Adobe.

L&#39;elenco seguente illustra alcune delle funzioni esclusive di JupyterLab su Platform:

| Funzione | Descrizione |
| --- | --- |
| **Kernel** | I kernel forniscono ai notebook e agli altri [!DNL JupyterLab] front-end la possibilità di eseguire e analizzare il codice in diversi linguaggi di programmazione. [!DNL Experience Platform] fornisce ulteriori kernel per supportare lo sviluppo in [!DNL Python], R, PySpark e [!DNL Spark]. Per ulteriori dettagli, consulta la sezione [kernel](#kernels) . |
| **Accesso ai dati** | Accedete ai set di dati esistenti direttamente dall&#39;interno [!DNL JupyterLab] con il supporto completo delle funzionalità di lettura e scrittura. |
| **[!DNL Platform]integrazione dei servizi ** | Le integrazioni integrate consentono di utilizzare altri [!DNL Platform] servizi direttamente dall&#39;interno [!DNL JupyterLab]. Un elenco completo delle integrazioni supportate è disponibile nella sezione [Integrazione con altri servizi](#service-integration)Platform. |
| **Autenticazione** | Oltre al modello <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">di sicurezza integrato di</a>JupyterLab, ogni interazione tra l&#39;applicazione e  Experience Platform, inclusa la comunicazione tra servizi Platform, è criptata e autenticata tramite <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Librerie di Sviluppo** | In [!DNL Experience Platform], [!DNL JupyterLab] fornisce librerie preinstallate per [!DNL Python], R e PySpark. Consultate l&#39; [appendice](#supported-libraries) per un elenco completo delle librerie supportate. |
| **Controller libreria** | Se le librerie preinstallate non sono adatte alle vostre esigenze, è possibile installare librerie aggiuntive per Python e R e memorizzare temporaneamente in contenitori isolati per mantenere l&#39;integrità dei dati [!DNL Platform] e mantenerli al sicuro. Per ulteriori dettagli, consulta la sezione [kernel](#kernels) . |

>[!NOTE] Le librerie aggiuntive sono disponibili solo per la sessione in cui sono state installate. È necessario reinstallare tutte le librerie aggiuntive necessarie all&#39;avvio delle nuove sessioni.

## Integrazione con altri [!DNL Platform] servizi {#service-integration}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. L&#39;integrazione di [!DNL JupyterLab] on [!DNL Platform] come IDE integrato consente di interagire con altri [!DNL Platform] servizi, consentendo di sfruttare [!DNL Platform] al massimo il suo potenziale. I seguenti [!DNL Platform] servizi sono disponibili in [!DNL JupyterLab]:

* **[!DNL Catalog Service]:**Accesso ed esplorazione di set di dati con funzionalità di lettura e scrittura.
* **[!DNL Query Service]:**Accesso ed esplorazione di dataset utilizzando SQL, fornendo costi generali di accesso ai dati inferiori quando si tratta di grandi quantità di dati.
* **[!DNL Sensei ML Framework]:**Sviluppo di modelli con la capacità di formare e valutare i dati, nonché creazione di ricette con un solo clic.
* **[!DNL Experience Data Model (XDM)]:**Standardizzazione e interoperabilità sono concetti chiave  Adobe Experience Platform.[Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en), guidato da Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

>[!NOTE] Alcune integrazioni [!DNL Platform] di servizio [!DNL JupyterLab] sono limitate a specifici kernel. Per ulteriori informazioni, consulta la sezione sui [kernel](#kernels) .

## Funzioni principali e operazioni comuni

Le informazioni relative alle caratteristiche chiave di [!DNL JupyterLab] e le istruzioni sull&#39;esecuzione di operazioni comuni sono fornite nelle sezioni seguenti:

* [Access JupyterLab](#access-jupyterlab)
* [Interfaccia JupyterLab](#jupyterlab-interface)
* [Celle di codice](#code-cells)
* [Kernel](#kernels)
* [Sessioni kernel](#kernel-sessions)
* [Risorsa di esecuzione PySpark/Spark](#execution-resource)
* [Launcher](#launcher)

### Access [!DNL JupyterLab] {#access-jupyterlab}

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

Ogni blocco appunti o attività attiva [!DNL JupyterLab] utilizza una sessione del kernel. Tutte le sessioni attive si trovano espandendo la scheda Terminali **in esecuzione e kernel** dalla barra laterale sinistra. Il tipo e lo stato del kernel di un notebook possono essere identificati osservando l&#39;interfaccia superiore destra del notebook. Nel diagramma seguente, il kernel associato al notebook è **[!DNL Python]3 **e lo stato corrente è rappresentato da un cerchio grigio a destra. Un cerchio vuoto implica un kernel inattivo e un cerchio pieno implica un kernel occupato.

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
| Vendite al dettaglio | Un blocco appunti precompilato con ricetta <a href="https://adobe.ly/2wOgO3L" target="_blank">vendite</a> al dettaglio utilizzando dati di esempio. |
| Generatore di ricette | Un modello per notebook per la creazione di una ricetta in [!DNL JupyterLab]. È precompilato con codice e commenti che mostrano e descrivono il processo di creazione delle ricette. Per informazioni dettagliate, fare riferimento al <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">notebook per l&#39;esercitazione</a> sulle ricette. |
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
>Per i notebook viene fornita una sola GPU per organizzazione. Se la GPU è in uso, è necessario attendere che l&#39;utente che ha attualmente riservato la GPU la rilasci. A questo scopo, disconnettetevi o uscite dalla GPU in uno stato di inattività per quattro o più ore.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## Accesso [!DNL Platform] ai dati tramite i blocchi appunti

Ogni kernel supportato fornisce funzionalità integrate che consentono di leggere [!DNL Platform] i dati da un dataset all&#39;interno di un blocco appunti. Tuttavia, il supporto per l&#39;impaginazione dei dati è limitato ai notebook [!DNL Python] e R.

### Limiti dei dati per notebook

Le informazioni seguenti definiscono la quantità massima di dati leggibili, il tipo di dati utilizzato e il periodo di tempo stimato necessario per la lettura dei dati. Per [!DNL Python] e R, per i benchmark è stato utilizzato un server notebook configurato a 40 GB di RAM. Per PySpark e Scala, un cluster di database configurato a 64 GB di RAM, 8 core, 2 DBU con un massimo di 4 dipendenti è stato utilizzato per i benchmark indicati di seguito.

I dati dello schema ExperienceEvent utilizzati variavano nelle dimensioni a partire da mille (1K) righe fino a un miliardo di righe (1B). Per le metriche PySpark e [!DNL Spark] , per i dati XDM è stato utilizzato un intervallo di date di 10 giorni.

I dati dello schema ad hoc sono stati pre-elaborati utilizzando [!DNL Query Service] Crea tabella come Seleziona (CTAS). Questi dati sono anche variati in dimensioni a partire da mille (1K) righe che vanno fino a un miliardo (1B) righe.

#### [!DNL Python] limiti dei dati del notebook

**Schema ExperienceEvent XDM:** È necessario essere in grado di leggere un massimo di 2 milioni di righe (circa 6,1 GB di dati su disco) di dati XDM in meno di 22 minuti. L&#39;aggiunta di righe aggiuntive potrebbe causare errori.

| Numero di righe | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Dimensioni su disco (MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK (in secondi) | 20.3 | 86.8 | 63 | 659 | 1315 |

**schema ad hoc:** È necessario essere in grado di leggere un massimo di 5 milioni di righe (circa 5,6 GB di dati su disco) di dati non XDM (ad hoc) in meno di 14 minuti. L&#39;aggiunta di righe aggiuntive potrebbe causare errori.

| Numero di righe | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Dimensioni su disco (in MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (in secondi) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

#### Limiti dei dati del notebook R

**Schema ExperienceEvent XDM:** In meno di 13 minuti è possibile leggere al massimo 1 milione di righe di dati XDM (3 GB di dati su disco).

| Numero di righe | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Dimensioni su disco (MB) | 18.73 | 187.5 | 308 | 3000 |
| R Kernel (in secondi) | 14.03 | 69.6 | 86.8 | 775 |

**schema ad hoc:** Dovrebbe essere possibile leggere un massimo di 3 milioni di righe di dati ad hoc (293 MB di dati su disco) in circa 10 minuti.

| Numero di righe | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Dimensioni su disco (in MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| SDK R (in sec) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

#### Limiti dei dati del notebook PySpark ([!DNL Python] kernel):

**Schema ExperienceEvent XDM:** In modalità interattiva è possibile leggere fino a 5 milioni di righe (circa 13,42 GB di dati su disco) di dati XDM in circa 20 minuti. La modalità interattiva supporta solo fino a 5 milioni di righe. Se si desidera leggere set di dati più grandi, è consigliabile passare alla modalità Batch. In modalità Batch dovreste essere in grado di leggere un massimo di 500 milioni di righe (circa 1,31 TB di dati su disco) di dati XDM in circa 14 ore.

| Numero di righe | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Dimensioni su disco | 2.93MB | 4.38MB | 29.02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1.31TB |
| SDK (modalità interattiva) | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK (modalità batch) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**schema ad hoc:** In modalità interattiva è necessario essere in grado di leggere un massimo di 1 miliardo di righe (circa 1,05 TB di dati su disco) di dati non XDM in meno di 3 minuti. In modalità Batch dovreste essere in grado di leggere un massimo di 1 miliardo di righe (circa 1,05 TB di dati su disco) di dati non XDM in circa 18 minuti.

| Numero di righe | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Dimensioni su disco | 1.12MB | 11.24MB | 109.48MB | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1.05TB |
| Modalità interattiva SDK (in secondi) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | 22s | 28.4s | 40s | 97.4s | 154.5s |
| Modalità batch SDK (in secondi) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

#### [!DNL Spark] Limiti dei dati del notebook (kernel Scala):

**Schema ExperienceEvent XDM:** In modalità interattiva è possibile leggere fino a 5 milioni di righe (circa 13,42 GB di dati su disco) di dati XDM in circa 18 minuti. La modalità interattiva supporta solo fino a 5 milioni di righe. Se si desidera leggere set di dati più grandi, è consigliabile passare alla modalità Batch. In modalità Batch dovreste essere in grado di leggere un massimo di 500 milioni di righe (circa 1,31 TB di dati su disco) di dati XDM in circa 14 ore.

| Numero di righe | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Dimensioni su disco | 2.93MB | 4.38MB | 29.02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1.31TB |
| Modalità interattiva SDK (in secondi) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| Modalità batch SDK (in secondi) | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**schema ad hoc:** In modalità interattiva è necessario essere in grado di leggere un massimo di 1 miliardo di righe (circa 1,05 TB di dati su disco) di dati non XDM in meno di 3 minuti. In modalità Batch dovreste essere in grado di leggere un massimo di 1 miliardo di righe (circa 1,05 TB di dati su disco) di dati non XDM in circa 16 minuti.

| Numero di righe | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Dimensioni su disco | 1.12MB | 11.24MB | 109.48MB | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1.05TB |
| Modalità interattiva SDK (in secondi) | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | 29.2s | 29.7s | 36.9s | 83.5s | 139s |
| Modalità batch SDK (in secondi) | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

### Lettura da un set di dati in [!DNL Python]/R

[!DNL Python] e i notebook R consentono di impaginare i dati quando si accede ai set di dati. Di seguito è illustrato il codice di esempio per leggere i dati con e senza impaginazione.

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### Lettura da un set di dati in [!DNL Python]/R senza impaginazione

L&#39;esecuzione del codice seguente consente di leggere l&#39;intero set di dati. Se l&#39;esecuzione ha esito positivo, i dati verranno salvati come fotogramma dati Pandas a cui fa riferimento la variabile `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

* `{DATASET_ID}`: L&#39;identità univoca del dataset a cui accedere

#### Lettura da un set di dati in [!DNL Python]/R con impaginazione

L&#39;esecuzione del codice seguente consente di leggere i dati dal set di dati specificato. La paginazione si ottiene limitando e compensando i dati attraverso le funzioni `limit()` e `offset()` rispettivamente. I dati limitati si riferiscono al numero massimo di punti dati da leggere, mentre l&#39;offset fa riferimento al numero di punti dati da ignorare prima della lettura dei dati. Se l&#39;operazione di lettura viene eseguita correttamente, i dati verranno salvati come fotogramma dati Pandas a cui fa riferimento la variabile `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$limit(100L)$offset(10L)$read() 
```

* `{DATASET_ID}`: L&#39;identità univoca del dataset a cui accedere

### Leggi da un set di dati in PySpark/[!DNL Spark]/Scala

Con un blocco appunti PySpark o Scala attivo aperto, espandere la scheda **Esplora** dati dalla barra laterale sinistra e fare doppio clic su **Set** dati per visualizzare un elenco dei set di dati disponibili. Fare clic con il pulsante destro del mouse sull&#39;elenco di set di dati a cui si desidera accedere e scegliere **Esplora dati nel blocco appunti**. Vengono generate le seguenti celle di codice:

#### PySpark ([!DNL Spark] 2.4) {#pyspark2.4}

Con l&#39;introduzione di Spark 2.4, [`%dataset`](#magic) la magia personalizzata è in dotazione.

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Scala ([!DNL Spark] 2.4) {#spark2.4}

```scala
// Scala (Spark 2.4)

// initialize the session
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()

val dataFrame = spark.read.format("com.adobe.platform.query")
    .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
    .option("ims-org", sys.env("IMS_ORG_ID"))
    .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
    .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
    .option("mode", "batch")
    .option("dataset-id", "{DATASET_ID}")
    .load()
dataFrame.printSchema()
dataFrame.show()
```

>[!TIP]
>In Scala è possibile utilizzare `sys.env()` per dichiarare e restituire un valore dall&#39;interno `option`.

### Utilizzo di %dataset Magic nei notebook PySpark 3 ([!DNL Spark] 2.4) {#magic}

Con l&#39;introduzione di [!DNL Spark] 2.4, `%dataset` la magia personalizzata è fornita per l&#39;uso in nuovi notebook PySpark 3 ([!DNL Spark] 2.4) ([!DNL Python] 3 kernel).

**Utilizzo**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Descrizione**

Comando [!DNL Data Science Workspace] magico personalizzato per la lettura o la scrittura di un dataset da un [!DNL Python] blocco appunti ([!DNL Python] 3 kernel).

* **{action}**: Tipo di azione da eseguire sul set di dati. Sono disponibili due azioni: &quot;read&quot; o &quot;write&quot;.
* **—datasetId {id}**: Utilizzato per fornire l&#39;ID del set di dati da leggere o scrivere. Questo è un argomento obbligatorio.
* **—dataFrame {df}**: Il dataframe panda. Questo è un argomento obbligatorio.
   * Quando l&#39;azione è &quot;read&quot;, {df} è la variabile in cui sono disponibili i risultati dell&#39;operazione di lettura del dataset.
   * Quando l&#39;azione è &quot;scrivi&quot;, il dataframe {df} viene scritto nel dataset.
* **—mode (facoltativo)**: I parametri consentiti sono &quot;batch&quot; e &quot;interattivo&quot;. Per impostazione predefinita, la modalità è impostata su &quot;interattivo&quot;. Si consiglia di utilizzare la modalità &quot;batch&quot; durante la lettura di grandi quantità di dati.

**Esempi**

* **Leggi l&#39;esempio**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **Esempio** di scrittura: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### Dati query con [!DNL Query Service] in [!DNL Python]

[!DNL JupyterLab] on [!DNL Platform] consente di utilizzare SQL in un [!DNL Python] blocco appunti per accedere ai dati tramite <a href="https://www.adobe.com/go/query-service-home-en" target="_blank">Adobe Experience Platform Query Service</a>. L&#39;accesso ai dati [!DNL Query Service] può essere utile per gestire i set di dati di grandi dimensioni a causa dei suoi tempi di esecuzione superiori. Tenere presente che l’esecuzione di query sui dati che utilizzano [!DNL Query Service] ha un limite di tempo di elaborazione di dieci minuti.

Prima di utilizzare [!DNL Query Service] in [!DNL JupyterLab], è necessario avere una conoscenza approfondita della sintassi <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">[!DNL Query Service]</a>SQL.

La query dei dati mediante [!DNL Query Service] richiede di fornire il nome del set di dati di destinazione. È possibile generare le celle di codice necessarie individuando il set di dati desiderato utilizzando **Data Explorer**. Fare clic con il pulsante destro del mouse sull&#39;elenco dei set di dati e scegliere Dati **query nel blocco appunti** per generare le due celle di codice seguenti nel blocco appunti:


Per utilizzare [!DNL Query Service] in [!DNL JupyterLab], è innanzitutto necessario creare una connessione tra il [!DNL Python] blocco appunti e [!DNL Query Service]. Questo può essere ottenuto eseguendo la prima cella generata.

```python
qs_connect()
```

Nella seconda cella generata, la prima riga deve essere definita prima della query SQL. Per impostazione predefinita, la cella generata definisce una variabile opzionale (`df0`) che salva i risultati della query come fotogramma dati Pandas. <br>L&#39; `-c QS_CONNECTION` argomento è obbligatorio e indica al kernel di eseguire la query SQL con [!DNL Query Service]. Per un elenco degli argomenti aggiuntivi, vedere l’ [appendice](#optional-sql-flags-for-query-service) .

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Alle variabili Python è possibile fare riferimento direttamente all&#39;interno di una query SQL utilizzando la sintassi in formato stringa e racchiudendo le variabili tra parentesi graffe (`{}`), come illustrato nell&#39;esempio seguente:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtra i dati ExperienceEvent in [!DNL Python]/R

Per accedere e filtrare un set di dati ExperienceEvent in un blocco appunti [!DNL Python] o R, è necessario fornire l&#39;ID del set di dati (`{DATASET_ID}`) insieme alle regole del filtro che definiscono un intervallo di tempo specifico utilizzando gli operatori logici. Quando viene definito un intervallo di tempo, qualsiasi impaginazione specificata viene ignorata e viene considerato l&#39;intero set di dati.

Di seguito è riportato un elenco di operatori di filtraggio:

* `eq()`: Uguale a
* `gt()`: Maggiore di
* `ge()`: Maggiore o uguale a
* `lt()`: Minore di
* `le()`: Minore o uguale a
* `And()`: Operatore logico AND
* `Or()`: Operatore OR logico

Le celle seguenti filtrano un set di dati ExperienceEvent in dati esistenti esclusivamente tra il 1 gennaio 2019 e la fine del 31 dicembre 2019.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

### Filtrare i dati ExperienceEvent in PySpark/[!DNL Spark]

Per accedere e filtrare un set di dati ExperienceEvent in un blocco appunti PySpark o Scala è necessario fornire l&#39;identità del set di dati (`{DATASET_ID}`), l&#39;identità IMS della propria organizzazione e le regole del filtro che definiscono un intervallo di tempo specifico. Un intervallo di tempo di filtro è definito utilizzando la funzione `spark.sql()`, dove il parametro della funzione è una stringa di query SQL.

Le celle seguenti filtrano un set di dati ExperienceEvent in dati esistenti esclusivamente tra il 1 gennaio 2019 e la fine del 31 dicembre 2019.

#### PySpark 3 ([!DNL Spark] 2.4) {#pyspark3-spark2.4}

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

#### Scala ([!DNL Spark] 2.4) {#scala-spark}

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

>[!TIP]
>In Scala è possibile utilizzare `sys.env()` per dichiarare e restituire un valore dall&#39;interno `option`. Questo elimina la necessità di definire le variabili se sai che verranno utilizzate solo una volta. L&#39;esempio seguente prende `val userToken` spunto dall&#39;esempio precedente e lo dichiara in linea `option` come alternativa:
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

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

## Flag SQL facoltativi per [!DNL Query Service] {#optional-sql-flags-for-query-service}

La tabella riportata di seguito illustra i flag SQL facoltativi utilizzabili per [!DNL Query Service].

| **Flag** | **Descrizione** |
| --- | --- |
| `-h`, `--help` | Visualizza il messaggio della Guida e esci. |
| `-n`, `--notify` | Attiva/disattiva l&#39;opzione per la notifica dei risultati della query. |
| `-a`, `--async` | L&#39;utilizzo di questo flag consente di eseguire la query in modo asincrono e di liberare il kernel durante l&#39;esecuzione della query. Prestate attenzione quando assegnate i risultati della query alle variabili, in quanto potrebbe essere undefined se la query non è completa. |
| `-d`, `--display` | L&#39;utilizzo di questo flag impedisce la visualizzazione dei risultati. |

